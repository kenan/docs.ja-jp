---
title: "イベントのデザイン | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "前のイベント"
  - "イベント [.NET Framework] のデザイン ガイドライン"
  - "メンバー デザインのガイドライン、イベント"
  - "イベント デザインのガイドラインのイベント ハンドラー [.NET Framework]"
  - "後のイベント"
  - "署名、イベント処理"
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# イベントのデザイン
イベントは、コールバック \(ユーザー コードを呼び出すために、フレームワークを許可するコンストラクト\) の最もよく使用される形式です。 その他のコールバック機構には、デリゲート、仮想メンバー、およびインターフェイス ベースのプラグインを取得するメンバーが含まれます。 ユーザビリティに関する調査からのデータは、開発者の大部分が使いやすいその他のコールバック メカニズムを使用しているよりも、イベントを使用することを示します。 イベントは、Visual Studio および多くの言語とうまく統合されています。  
  
 イベントの 2 つのグループがあることを確認することが重要: 前のイベント、および状態が変更された後に発生するイベントと呼ばれるシステムの変更の状態の前に発生したイベントには、後のイベントと呼ばれます。 イベントの前の例としては `Form.Closing`, 、フォームが閉じられる前にこれが発生します。 イベントの後の例としては `Form.Closed`, 、フォームが閉じられた後は、発生します。  
  
 **✓ は** イベントではなく"fire"や「トリガー」の「生成」という用語を使用して  
  
 **✓ は** を使用して <xref:System.EventHandler%601?displayProperty=fullName> イベント ハンドラーとして使用する新しいデリゲートを手動で作成する代わりにします。  
  
 **✓ を検討してください** のサブクラスを使用して <xref:System.EventArgs> イベントの引数としてを除いて確信イベントがイベント処理メソッドでは、対象のデータを実行する必要はありませんがいる場合に使用できます、 `EventArgs` を直接入力します。  
  
 API を使用して、出荷する場合は、 `EventArgs` を直接しないことができます互換性を損なうことがなく、イベントに実行されるように、データを追加します。 サブクラスを使用する場合でもかどうか最初に完全に空ことができます必要なときに、サブクラスにプロパティを追加します。  
  
 **✓ は** 各イベントを発生させる保護された仮想メソッドを使用します。 これは、構造体、シール クラス、または静的イベントが、封印されていないクラスで静的でないイベントに適用できるのみです。  
  
 メソッドの目的は、上書きを使用して、イベントを処理する派生クラスの手段を提供します。 オーバーライドは、派生クラスで基本クラス イベントを処理するより柔軟で、高速より自然な方法です。 規則では、メソッドの名前は"On"で起動し、直後に、イベントの名前を付ける。  
  
 派生クラスは、そのオーバーライドで、メソッドの基本実装を呼び出していないを選択できます。 正常に動作する基本クラスに必要なメソッドでどのような処理を含めないことでこれを準備します。  
  
 **✓ は** イベントを発生させるプロテクト メソッドにパラメーターを 1 つを実行します。  
  
 パラメーターに名前を付ける `e` と、イベント引数クラスとして自動的に入力する必要があります。  
  
 **X のしないで** 非静的イベントを発生させる場合、送信側として null を渡します。  
  
 **✓ は** 静的イベントを発生させる場合、送信側として null を渡します。  
  
 **X のしないで** イベントを発生させるときにイベント データ パラメーターとして null を渡します。  
  
 渡す必要があります `EventArgs.Empty` イベント処理メソッドに、データの受け渡ししたくない場合。 開発者は、いない null にするには、このパラメーターを期待しています。  
  
 **✓ を検討してください** エンド ユーザーで取り消すことができるイベントの発生します。 これは、前のイベントにのみ適用されます。  
  
 使用 <xref:System.ComponentModel.CancelEventArgs?displayProperty=fullName> またはエンドユーザーのイベントをキャンセルできるイベントの引数としてそのサブクラスです。  
  
### カスタム イベント ハンドラーのデザイン  
 場合がある `EventHandler<T>` 、framework がジェネリックをサポートしないと、CLR の以前のバージョンを使用する必要がある場合など、使用することはできません。 このような場合は、デザインおよびカスタム イベント ハンドラーのデリゲートを作成する必要があります。  
  
 **✓ は** イベント ハンドラーの void の戻り値の型を使用します。  
  
 イベント ハンドラーは、おそらく複数のオブジェクト上のメソッドを処理する複数のイベントを呼び出すことができます。 イベント処理メソッドの戻り値が許可された場合は、イベントの呼び出しごとの複数の戻り値があります。  
  
 **✓ は** を使用して `object` イベント ハンドラーの最初のパラメーターの型とそれを呼び出す `sender`します。  
  
 **✓ は** を使用して <xref:System.EventArgs?displayProperty=fullName> またはそのサブクラスのイベント ハンドラーの 2 番目のパラメーターの型としてそれを呼び出す `e`します。  
  
 **X のしないで** イベント ハンドラーに 3 つ以上のパラメーターがあります。  
  
 *部分 © 2005年、2009 Microsoft Corporation します。 All rights reserved.*  
  
 *翔泳社からのアクセス許可によって検出 [Framework デザイン ガイドライン: 規則が、表現方法と再利用可能な .NET ライブラリを 2 nd Edition パターン](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) は Cwalina Brad エイブラムスによる、Microsoft Windows の開発シリーズの一部として Addison\-wesley Professional、2008 年 10 月 22 日を公開します。*  
  
## 参照  
 [メンバー デザインのガイドライン](../../../docs/standard/design-guidelines/member.md)   
 [Framework デザイン ガイドライン](../../../docs/standard/design-guidelines/index.md)