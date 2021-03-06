---
title: Windows Communication Foundation で使用するための Windows プロセス アクティブ化サービスを設定する
ms.date: 03/30/2017
ms.assetid: 1d50712e-53cd-4773-b8bc-a1e1aad66b78
ms.openlocfilehash: 3a4d771c3f2d5e7e6ec4fd6a1e229548e063a6d1
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33489769"
---
# <a name="configuring-the-windows-process-activation-service-for-use-with-windows-communication-foundation"></a>Windows Communication Foundation で使用するための Windows プロセス アクティブ化サービスを設定する
このトピックでは、Windows プロセス アクティブ化サービス (WAS とも呼ばれます) を設定するために必要な手順を説明で[!INCLUDE[wv](../../../../includes/wv-md.md)]HTTP 経由で通信を行わないサービスのネットワーク プロトコルの Windows Communication Foundation (WCF) をホストします。 以降の各セクションで、この構成に関する手順について概説します。  
  
-   インストール (またはのインストールを確認する) 必要とする WCF アクティブ化コンポーネントです。  
  
-   使用するネットワーク プロトコル バインドを含む WAS サイトを作成するか、新しいプロトコル バインドを既存のサイトに追加します。  
  
-   サービスをホストするアプリケーションを作成し、必要なネットワーク プロトコルを使用するようにそのアプリケーションを設定します。  
  
-   非 HTTP エンドポイントを公開する WCF サービスを構築します。  
  
## <a name="configuring-a-site-with-non-http-bindings"></a>非 HTTP バインドを使用したサイトの構成  
 WAS で非 HTTP バインドを使用するには、サイト バインドを WAS 構成に追加する必要があります。 WAS の構成ストアは、%windir%\system32\inetsrv\config ディレクトリにある applicationHost.config ファイルです。 この構成ストアは、WAS と IIS 7.0 の両方で共有されます。  
  
 applicationHost.config は、任意の標準テキスト エディター (メモ帳など) で開くことが可能な XML テキスト ファイルです。 ただし、[!INCLUDE[iisver](../../../../includes/iisver-md.md)] コマンド ライン構成ツール (appcmd.exe) の方が、非 HTTP サイトのバインディングの追加には適しています。  
  
 次のコマンドは、appcmd.exe を使用して、既定の Web サイトに net.tcp サイト バインドを追加します (このコマンドは 1 行で入力します)。  
  
```  
appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
```  
  
 このコマンドは、次に示す行を applicationHost.config ファイルに追加することによって、既定の Web サイトに新しい net.tcp バインドを追加します。  
  
```xml  
<sites>  
    <site name="Default Web Site" id="1">  
        <bindings>  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            //The following line is added by the command.  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
        </bindings>  
    </site>  
</sites>  
```  
  
## <a name="enabling-an-application-to-use-non-http-protocols"></a>非 HTTP プロトコルを使用するためのアプリケーションの設定  
 有効にするにまたは個々 のネットワーク protocolsat アプリケーション レベルを無効にすることができます。 次のコマンドは、`Default Web Site` で動作するアプリケーションに対して、HTTP プロトコルと net.tcp プロトコルの両方を有効にする方法を示しています。  
  
```  
appcmd.exe set app "Default Web Site/appOne" /enabledProtocols:net.tcp  
```  
  
 有効なプロトコルの一覧設定することもできます、 \<applicationDefaults > ApplicationHost.config に保存されたサイトの XML 構成の要素。  
  
 次の applicationHost.config からの XML コードは、HTTP プロトコルと非 HTTP プロトコルの両方にバインドされたサイトを示しています。 非 HTTP プロトコルのサポートに必要な追加の構成は、コメントで付記されています。  
  
```xml  
<sites>  
    <site name="Default Web Site" id="1">  
    <application path="/">  
        <virtualDirectory path="/" physicalPath="D:\inetpub\wwwroot" />  
    </application>  
       <bindings>  
            //The following two lines are added by the command.  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
       </bindings>  
    </site>  
    <siteDefaults>  
        <logFile   
        customLogPluginClsid="{FF160663-DE82-11CF-BC0A-00AA006111E0}"  
          directory="D:\inetpub\logs\LogFiles" />  
        <traceFailedRequestsLogging   
          directory="D:\inetpub\logs\FailedReqLogFiles" />  
    </siteDefaults>  
    <applicationDefaults   
      applicationPool="DefaultAppPool"   
      //The following line is inserted by the command.  
      enabledProtocols="http, net.tcp" />  
    <virtualDirectoryDefaults allowSubDirConfig="true" />  
</sites>  
```  
  
 非 HTTP アクティブ化の WAS を使用するサービスをアクティブ化しようとしたときに、WAS をインストールおよび構成していない場合、次のエラーが表示されることがあります。  
  
```Output  
[InvalidOperationException: The protocol 'net.tcp' does not have an implementation of HostedTransportConfiguration type registered.]   System.ServiceModel.AsyncResult.End(IAsyncResult result) +15778592   System.ServiceModel.Activation.HostedHttpRequestAsyncResult.End(IAsyncResult result) +15698937   System.ServiceModel.Activation.HostedHttpRequestAsyncResult.ExecuteSynchronous(HttpApplication context, Boolean flowContext) +265   System.ServiceModel.Activation.HttpModule.ProcessRequest(Object sender, EventArgs e) +227   System.Web.SyncEventExecutionStep.System.Web.HttpApplication.IExecutionStep.Execute() +80   System.Web.HttpApplication.ExecuteStep(IExecutionStep step, Boolean& completedSynchronously) +171  
```  
  
 このエラーが表示された場合は、非 HTTP アクティブ化の WAS が適切にインストールおよび構成されていることを確認してください。 詳細については、次を参照してください。[する方法: WCF アクティブ化コンポーネントの構成のインストールと](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)です。  
  
## <a name="building-a-wcf-service-that-uses-was-for-non-http-activation"></a>非 HTTP のアクティブ化で WAS を使用する WCF サービスの構築  
 一度インストールし、WAS を構成する手順を実行すると (を参照してください[する方法: WCF アクティブ化コンポーネントの構成のインストールと](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md))、ライセンス認証は IIS でホストされているサービスを構成するように WAS を使用するサービスを構成します。  
  
 WAS アクティブ化された WCF サービスの構築に関する詳細な手順については、次を参照してください。[する方法: WAS で WCF サービスをホスト](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)です。  
  
## <a name="see-also"></a>関連項目  
 [Windows プロセス アクティブ化サービスでのホスティング](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)  
 [Windows Server App Fabric のホスティング機能](http://go.microsoft.com/fwlink/?LinkId=201276)
