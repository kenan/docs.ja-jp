---
title: "二重 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "二重のサービス コントラクト"
ms.assetid: bc5de6b6-1a63-42a3-919a-67d21bae24e0
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# 二重
双方向サンプルでは、双方向コントラクトを定義して実装する方法を示します。  双方向通信は、クライアントがサービスとのセッションを確立し、サービスからクライアントにメッセージを返信できるチャネルがサービスに提供されると発生します。  このサンプルは、「[概要](../../../../docs/framework/wcf/samples/getting-started-sample.md)」に基づいています。  双方向コントラクトは、クライアントからサービスへのプライマリ インターフェイスとサービスからクライアントへのコールバック インターフェイスという 2 つのインターフェイスのペアとして定義されます。  このサンプルでは、`ICalculatorDuplex` インターフェイスを使用することにより、クライアントは算術演算を実行し、セッション経由で結果を計算できます。  サービスは、`ICalculatorDuplexCallback` インターフェイスで結果を返します。  コンテキストを確立して、クライアントとサービスの間で送信される一連のメッセージを相互に関連付ける必要があるため、二重のコントラクトにはセッションが必要です。  
  
> [!NOTE]
>  このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 この例では、クライアントはコンソール アプリケーション \(.exe\) であり、サービスはインターネット インフォメーション サービス \(IIS\) によってホストされます。  双方向コントラクトは、次のように定義されます。  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required,  
                 CallbackContract=typeof(ICalculatorDuplexCallback))]  
public interface ICalculatorDuplex  
{  
    [OperationContract(IsOneWay = true)]  
    void Clear();  
    [OperationContract(IsOneWay = true)]  
    void AddTo(double n);  
    [OperationContract(IsOneWay = true)]  
    void SubtractFrom(double n);  
    [OperationContract(IsOneWay = true)]  
    void MultiplyBy(double n);  
    [OperationContract(IsOneWay = true)]  
    void DivideBy(double n);  
}  
  
public interface ICalculatorDuplexCallback  
{  
    [OperationContract(IsOneWay = true)]  
    void Result(double result);  
    [OperationContract(IsOneWay = true)]  
    void Equation(string eqn);  
}  
  
```  
  
 `CalculatorService` クラスは、プライマリ `ICalculatorDuplex` インターフェイスを実装します。  このサービスは <xref:System.ServiceModel.InstanceContextMode> インスタンス モードを使用して、各セッションの結果を保持します。  クライアントへのコールバック チャネルへのアクセスには、`Callback` というプライベート プロパティを使用します。  サービスはこのコールバックを使用し、コールバック インターフェイスを介してメッセージをクライアントに返信します。  
  
```  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
public class CalculatorService : ICalculatorDuplex  
{  
    double result = 0.0D;  
    string equation;  
  
    public CalculatorService()  
    {  
        equation = result.ToString();  
    }  
  
    public void Clear()  
    {  
        Callback.Equation(equation + " = " + result.ToString());  
        equation = result.ToString();  
    }  
  
    public void AddTo(double n)  
    {  
        result += n;  
        equation += " + " + n.ToString();  
        Callback.Result(result);  
    }  
    ...  
    ICalculatorDuplexCallback Callback  
    {  
        get  
        {  
            return OperationContext.Current.GetCallbackChannel<ICalculatorDuplexCallback>();  
        }  
    }  
}  
```  
  
 クライアントは、サービスからのメッセージを受信するために、双方向コントラクトのコールバック インターフェイスを実装するクラスを提供する必要があります。  このサンプルでは、`CallbackHandler` クラスは `ICalculatorDuplexCallback` インターフェイスを実装するように定義されています。  
  
```  
public class CallbackHandler : ICalculatorDuplexCallback  
{  
   public void Result(double result)  
   {  
      Console.WriteLine("Result({0})", result);  
   }  
  
   public void Equation(string equation)  
   {  
      Console.WriteLine("Equation({0}", equation);  
   }  
}  
  
```  
  
 双方向コントラクト用に生成されるプロキシは、コンストラクト時に <xref:System.ServiceModel.InstanceContext> が提供される必要があります。  この <xref:System.ServiceModel.InstanceContext> がコールバック インターフェイスを実装するオブジェクトのサイトとして使用され、サービスから返信されるメッセージを処理します。  <xref:System.ServiceModel.InstanceContext> は、`CallbackHandler` クラスのインスタンスを使用して構築されます。  このオブジェクトは、コールバック インターフェイスでサービスからクライアントに送信されるメッセージを処理します。  
  
```  
// Construct InstanceContext to handle messages on callback interface.  
InstanceContext instanceContext = new InstanceContext(new CallbackHandler());  
  
// Create a client.  
CalculatorDuplexClient client = new CalculatorDuplexClient(instanceContext);  
  
Console.WriteLine("Press <ENTER> to terminate client once the output is displayed.");  
Console.WriteLine();  
  
// Call the AddTo service operation.  
double value = 100.00D;  
client.AddTo(value);  
  
// Call the SubtractFrom service operation.  
value = 50.00D;  
client.SubtractFrom(value);  
  
// Call the MultiplyBy service operation.  
value = 17.65D;  
client.MultiplyBy(value);  
  
// Call the DivideBy service operation.  
value = 2.00D;  
client.DivideBy(value);  
  
// Complete equation.  
client.Clear();  
  
Console.ReadLine();  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
```  
  
 この構成は、セッション通信と双方向通信の両方をサポートするバインディングを提供するように変更されています。  `wsDualHttpBinding` はセッション通信をサポートし、どちらの方向にも HTTP 接続が 1 つ用意される双方向 HTTP 接続を提供して双方向通信を実現します。  サービスでの構成の唯一の違いは、使用されるバインディングです。  クライアントで、サーバーがクライアントへの接続に使用するアドレスを構成する必要があります。次のサンプル構成を参照してください。  
  
```  
<client>  
  <endpoint name=""  
            address="http://localhost/servicemodelsamples/service.svc"   
            binding="wsDualHttpBinding"   
            bindingConfiguration="DuplexBinding"   
            contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex" />  
</client>  
  
<bindings>  
  <!-- Configure a binding that support duplex communication. -->  
  <wsDualHttpBinding>  
    <binding name="DuplexBinding"   
             clientBaseAddress="http://localhost:8000/myClient/">  
    </binding>  
  </wsDualHttpBinding>  
</bindings>  
  
```  
  
 サンプルを実行すると、クライアントに戻ってきたメッセージがサービスから送信されたコールバック インターフェイスに表示されます。  それぞれの中間結果が表示され、その後にすべての操作が完了したときの数式全体が表示されます。  Enter キーを押してクライアントをシャットダウンします。  
  
### サンプルをセットアップ、ビルド、および実行するには  
  
1.  「[Windows Communication Foundation サンプルの 1 回限りのセットアップの手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)」が実行済みであることを確認します。  
  
2.  ソリューションの C\# 版、C\+\+ 版、または Visual Basic .NET 版をビルドするには、「[Windows Communication Foundation サンプルのビルド](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。  
  
3.  単一コンピューター構成か複数コンピューター構成かに応じて、「[Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)」の手順に従います。  
  
    > [!IMPORTANT]
    >  複数コンピューター構成でクライアントを実行する場合は、[\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md) 要素内の [endpoint](http://msdn.microsoft.com/ja-jp/13aa23b7-2f08-4add-8dbf-a99f8127c017) 要素の `address` 属性と、[\<binding\>](../../../../docs/framework/misc/binding.md) 要素の `clientBaseAddress` 属性の両方に含まれる "localhost" を、適切なコンピューターの名前で置き換える必要があります。次を参照してください。  
  
    ```  
    <client>  
    <endpoint name = ""  
    address="http://service_machine_name/servicemodelsamples/service.svc"  
    ... />  
    </client>  
    ...  
    <wsDualHttpBinding>  
    <binding name="DuplexBinding" clientBaseAddress="http://client_machine_name:8000/myClient/">  
    </binding>  
    </wsDualHttpBinding>  
    ```  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。  続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」に移動して、すべての [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] サンプルおよび [!INCLUDE[wf1](../../../../includes/wf1-md.md)] サンプルをダウンロードしてください。  このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Duplex`  
  
## 参照