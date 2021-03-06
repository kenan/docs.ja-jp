---
title: WebRequest の問題と例外について
ms.date: 03/30/2017
ms.assetid: 74a361a5-e912-42d3-8f2e-8e9a96880a2b
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: c7def5c041c5d16a8ea58479664402b7346e52b0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33398067"
---
# <a name="understanding-webrequest-problems-and-exceptions"></a>WebRequest の問題と例外について
<xref:System.Net.WebRequest> とその派生クラス (<xref:System.Net.HttpWebRequest>、<xref:System.Net.FtpWebRequest>、<xref:System.Net.FileWebRequest>) は例外をスローし、異常な状態を信号で伝えます。 このような問題の解決はすぐにわからないことがあります。  
  
## <a name="solutions"></a>ソリューション  
 <xref:System.Net.WebException> の <xref:System.Net.WebException.Status%2A> プロパティを調べ、問題を判断します。 次の表は、いくつかの状態値と可能な解決策をまとめたものです。  
  
|Status|説明|ソリューション|  
|------------|-------------|--------------|  
|<xref:System.Net.WebExceptionStatus.SendFailure><br /><br /> - または -<br /><br /> <xref:System.Net.WebExceptionStatus.ReceiveFailure>|基盤となるソケットに問題があります。 接続がリセットされた可能性があります。|再接続し、要求を再送信します。<br /><br /> 最新のサービス パックがインストールされていることを確認します。<br /><br /> <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A?displayProperty=nameWithType> プロパティの値を増やします。<br /><br /> <xref:System.Net.HttpWebRequest.KeepAlive%2A?displayProperty=nameWithType> を `false` に設定します。<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> プロパティで最大接続数を増やします。<br /><br /> プロキシ構成を確認します。<br /><br /> SSL を利用するとき、証明書ストアにアクセスするアクセス許可がサーバー プロセスに与えられていることを確認してください。<br /><br /> 大量のデータを送信する場合、<xref:System.Net.HttpWebRequest.AllowWriteStreamBuffering%2A> を `false` に設定します。|  
|<xref:System.Net.WebExceptionStatus.TrustFailure>|サーバー証明書を検証できませんでした。|Internet Explorer で URI を開いてみてください。 セキュリティ警告が IE で表示されたら、それを解決します。 セキュリティ警告を解決できない場合、`true` を返す <xref:System.Net.ICertificatePolicy> を実装する証明書ポリシー クラスを作成し、それを <xref:System.Net.ServicePointManager.CertificatePolicy%2A> に渡すことができます。<br /><br /> [http://support.microsoft.com/?id=823177](http://go.microsoft.com/fwlink/?LinkID=179653) をご覧ください。<br /><br /> サーバー証明書に署名した証明書機関の証明書が Internet Explorer の信頼された証明機関一覧に追加されていることを確認してください。<br /><br /> URL 内のホスト名がサーバー証明書の共通名と一致していることを確認してください。|  
|<xref:System.Net.WebExceptionStatus.SecureChannelFailure>|SSL トランザクションでエラーが発生しました。あるいは、証明書に問題があります。|.NET Framework バージョン 1.1 は、SSL バージョン 3.0 にのみ対応しています。 サーバーが TLS バージョン 1.0 か SSL バージョン 2.0 だけを利用している場合、例外がスローされます。 .NET Framework バージョン 2.0 にアップグレードし、サーバーに合わせて <xref:System.Net.ServicePointManager.SecurityProtocol%2A> を設定します。<br /><br /> クライアント証明書に署名した証明書機関 (CA) をサーバーは信頼していません。 サーバーに CA の証明書をインストールしてください。 [http://support.microsoft.com/?id=332077](http://go.microsoft.com/fwlink/?LinkID=179654) をご覧ください。<br /><br /> 最新のサービス パックがインストールされていることを確認します。|  
|<xref:System.Net.WebExceptionStatus.ConnectFailure>|接続に失敗しました。|ファイアウォールまたはプロキシが接続をブロックしています。 接続を許可するようにファイアウォールまたはプロキシを変更します。<br /><br /> <xref:System.Net.WebProxy> コンストラクター (WebServiceProxyClass.Proxy = new WebProxy([http://server:80](http://server/), true)) を呼び出し、クライアント アプリケーションに <xref:System.Net.WebProxy> を明示的に指名します。<br /><br /> Filemon または Regmon を実行し、ワーカー プロセス ID に WSPWSP.dll、HKLM\System\CurrentControlSet\Services\DnsCache または HKLM\System\CurrentControlSet\Services\WinSock2 にアクセスするために必要なアクセス許可が与えられていることを確認します。|  
|<xref:System.Net.WebExceptionStatus.NameResolutionFailure>|ドメイン ネーム サービスがホスト名を解決できませんでした。|プロキシを正しく構成します。 [http://support.microsoft.com/?id=318140](http://go.microsoft.com/fwlink/?LinkID=179655) をご覧ください。<br /><br /> インストールしているアンチウイルス ソフトウェアまたはファイアウォールが接続をブロックしていないことを確認してください。|  
|<xref:System.Net.WebExceptionStatus.RequestCanceled>|<xref:System.Net.WebRequest.Abort%2A> が呼び出されたか、エラーが発生しました。|この問題は、クライアントまたはサーバーの負荷が大きいことで発生する場合もあります。 負荷を減らしてください。<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 設定を増やします。<br /><br /> Web サービス パフォーマンス設定の変更方法については、[http://support.microsoft.com/?id=821268](http://go.microsoft.com/fwlink/?LinkID=179656) をご覧ください。|  
|<xref:System.Net.WebExceptionStatus.ConnectionClosed>|既に閉じられているソケットへの書き込みをアプリケーションが試行しました。|クライアントまたはサーバーがオーバーロードの状態になっています。 負荷を減らしてください。<br /><br /> <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 設定を増やします。<br /><br /> Web サービス パフォーマンス設定の変更方法については、[http://support.microsoft.com/?id=821268](http://go.microsoft.com/fwlink/?LinkID=179656) をご覧ください。|  
|<xref:System.Net.WebExceptionStatus.MessageLengthLimitExceeded>|メッセージ長に設定された制限 (<xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>) を超えています。|<xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A> プロパティの値を増やします。|  
|<xref:System.Net.WebExceptionStatus.ProxyNameResolutionFailure>|ドメイン ネーム サービスがプロキシ ホスト名を解決できませんでした。|プロキシを正しく構成します。 [http://support.microsoft.com/?id=318140](http://go.microsoft.com/fwlink/?LinkID=179655) をご覧ください。<br /><br /> <xref:System.Net.HttpWebRequest.Proxy%2A> プロパティを `null` に設定し、プロキシを使用しないことを <xref:System.Net.HttpWebRequest> に適用します。|  
|<xref:System.Net.WebExceptionStatus.ServerProtocolViolation>|サーバーからの応答が有効な HTTP 応答ではありません。 サーバー応答が HTTP 1.1 RFC に準拠しないことを .NET Framework が検出したとき、この問題が発生します。 応答に含まれるヘッダーまたはヘッダー区切り文字が正しくないとき、この問題が発生することがあります。RFC 2616 は HTTP 1.1 とサーバーからの応答の有効な形式を定義します。 詳細については、「[http://www.ietf.org](http://go.microsoft.com/fwlink/?LinkID=147388)」を参照してください。|トランザクションのネットワーク トレースを取得し、応答のヘッダーを調べます。<br /><br /> アプリケーションが解析せずに (セキュリティ上、これは問題になる可能性があります) サーバー応答を要求する場合、構成ファイルで `useUnsafeHeaderParsing` を `true` に設定します。 [\<httpWebRequest> 要素 (ネットワーク設定)](../../../docs/framework/configure-apps/file-schema/network/httpwebrequest-element-network-settings.md) を参照してください。|  
  
## <a name="see-also"></a>参照  
 <xref:System.Net.HttpWebRequest>  
 <xref:System.Net.HttpWebResponse>  
 <xref:System.Net.Dns>
