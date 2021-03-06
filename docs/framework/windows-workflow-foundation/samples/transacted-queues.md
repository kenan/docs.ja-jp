---
title: トランザクション キュー
ms.date: 03/30/2017
ms.assetid: b1b011dd-5e0b-482c-9bb0-9d8727038f14
ms.openlocfilehash: b125158a113079d87eb6926393d5a2b5fe326824
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33519682"
---
# <a name="transacted-queues"></a>トランザクション キュー
このサンプルでは、キューおよびトランザクションの Windows Workflow Foundation (WF) 信頼性が高く、スケーラブルなサービスを作成するを統合する方法を示します。 A <!--zz <xref:System.Activities.TransactionScope>--> `System.Activities.TransactionScope`を使用してトランザクション内でキューにメッセージを送信するクライアント ワークフローで使用される、<xref:System.ServiceModel.NetMsmqBinding>です。 <xref:System.ServiceModel.Activities.TransactedReceiveScope> は、キューからメッセージを受信して同じトランザクション内でワークフローの状態を更新するためにサーバーで使用されます。  
  
## <a name="demonstrates"></a>使用例  
 <xref:System.Activities.Statements.TransactionScope>、<xref:System.ServiceModel.Activities.TransactedReceiveScope>、<xref:System.ServiceModel.NetMsmqBinding>、<xref:System.ServiceModel.Activities.Receive>、およびコンテンツ ベースの相関関係。  
  
## <a name="discussion"></a>説明  
 このサンプルで取り上げる機能について説明するために、特定のアカウント用に取得されて使用されるポイントを追跡する `RewardsPoints` ワークフロー サービスが作成されます。 クライアントは、<xref:System.Activities.WorkflowInvoker> を使用してキューへのさまざまな要求の送信をシミュレートします。 トランザクション内でキューにメッセージを送信するために、<xref:System.ServiceModel.Activities.Send> アクティビティを <xref:System.Activities.Statements.TransactionScope.Body%2A> の <xref:System.Activities.Statements.TransactionScope> 内に配置できます。 このサンプルでは、キューに置かれたメッセージがクライアント アプリケーションとサーバー アプリケーションを切り離す方法について説明するために、最初にクライアントが実行され、次にサーバーが実行されます。  
  
 クライアントが完了したら、サービスが構成されてホストされます。 サービスが開くとすぐに、既にキューに置かれているメッセージの処理が開始されます。 各メッセージが同じサーバー トランザクション内で受信および処理されます。 このサンプルでは、最初に受信するメッセージは、要求メッセージの一部として渡されるアカウント名に基づいてインスタンスを作成してコンテンツ ベースの相関関係を初期化する `CreateAccount` 要求です。 実際に必要となる可能性のある種類のサービスをモデル化するために、<xref:System.ServiceModel.Activities.TransactedReceiveScope> メッセージと `AddPoints` メッセージを処理する次の 2 つの `UsePoints` アクティビティが `while` ループ内の並行分岐に配置されており、これらのメッセージを任意の順序で繰り返し処理できるようになっています。  
  
 <xref:System.Activities.Statements.TransactionScope> および <xref:System.ServiceModel.Activities.TransactedReceiveScope> は、それぞれスコープの末尾に暗黙的な永続化ポイントを持つので、これらのアクティビティをキューと組み合わせて [!INCLUDE[wf1](../../../../includes/wf1-md.md)] で使用すると、メッセージが失われないようにしながら、ワークフローを一貫性のある状態から次の一貫性のある状態に確実に移行できます。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1.  MSMQ をインストールして構成します。 参照してください[メッセージ キューをインストールする](http://go.microsoft.com/fwlink/?LinkId=178526)詳細についてはします。  
  
2.  コマンド ラインで次のコマンドを実行して、MSDTC が実行されていることを確認します。 `net start msdtc`  
  
3.  プロジェクトをコンパイルして実行可能ファイルを開くか、[!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] でプロジェクトを開いてデバッグ メニューから開始オプションを選択します。 最初にキューが作成され、次にクライアントが実行されてキューにメッセージが送信され、最後にサービスが開始されてメッセージが処理されます。 プログラムを終了するには、Enter キーを押します。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合に、 [Windows Communication Foundation (WCF) および .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](http://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプルです。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedQueues`
