---
title: "方法 : コード内でクライアント バインディングを指定する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6bee5da4-adf7-42e6-8f78-63a9e5c6dbad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 方法 : コード内でクライアント バインディングを指定する
この例では、電卓サービスを使用するためのクライアントを作成し、そのクライアントのバインディングを強制的にコードで指定します。クライアントは `CalculatorService` にアクセスします。これにより、`ICalculator` インターフェイスが実装され、サービスとクライアントの両方で <xref:System.ServiceModel.BasicHttpBinding> クラスが使用されます。  
  
 ここで説明する手順では、電卓サービスが実行されていることを前提としています。サービスの構築については、「[方法 : 構成でサービス バインディングを指定する](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)」を参照してください。クライアント コンポーネントを自動的に生成するために、[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] に付属する [ServiceModel メタデータ ユーティリティ ツール \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) も使用します。このツールでは、サービスにアクセスするためのクライアント コードが生成されます。  
  
 クライアントは 2 つの部分で構成されます。Svcutil.exe によって、`ICalculator` インターフェイスを実装する `ClientCalculator` が生成されます。次に、`ClientCalculator` のインスタンスを作成し、サービスのバインディングとアドレスをコードで指定して、このクライアント アプリケーションを作成します。  
  
 この例のソースのコピーについては、「[BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md)」のサンプルを参照してください。  
  
### コード内でカスタム バインディングを指定するには  
  
1.  コマンド ラインから Svcutil.exe を実行して、サービス メタデータからコードを生成します。  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  生成されたクライアントには、クライアントの実装時に満たされなければならないサービス コントラクトを定義する `ICalculator` インターフェイスが含まれます。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#1)]
     [!code-vb[C_HowTo_CodeClientBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#1)]  
  
3.  生成されたクライアントは `ClientCalculator` も実装します。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#2)]
     [!code-vb[C_HowTo_CodeClientBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#2)]  
  
4.  クライアント アプリケーション内で <xref:System.ServiceModel.BasicHttpBinding> クラスを使用する `ClientCalculator` のインスタンスを作成し、指定したアドレスのサービス操作を呼び出します。  
  
     [!code-csharp[C_HowTo_CodeClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#3)]
     [!code-vb[C_HowTo_CodeClientBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#3)]  
  
5.  クライアントをコンパイルして実行します。  
  
## 参照  
 [サービスとクライアントを構成するためのバインディングの使用](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)