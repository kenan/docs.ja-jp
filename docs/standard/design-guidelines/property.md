---
title: プロパティのデザイン
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, properties
- properties [.NET Framework], design guidelines
ms.assetid: 127cbc0c-cbed-48fd-9c89-7c5d4f98f163
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4a4aec965753fe8f89b8bd89469f8dc5739a6a7c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33577102"
---
# <a name="property-design"></a>プロパティのデザイン
プロパティはメソッドに技術的には非常に似ていますは、使用シナリオの観点からはまったく異なります。 これらは、スマート フィールドと考える必要があります。 フィールドの呼び出し構文とメソッドの柔軟性があります。  
  
 **✓ DO** 呼び出し元が、プロパティの値を変更すべき場合取得専用のプロパティを作成します。  
  
 留意する場合の種類、プロパティが変更可能な参照型、プロパティは get-only 場合でも、プロパティの値を変更できます。  
  
 **X DO NOT** 設定専用のプロパティまたはプロパティを get アクセス操作子よりも広範なアクセシビリティを持つ set アクセス操作子を提供します。  
  
 たとえば、プロパティを使用しないパブリック set アクセス操作子と保護された get アクセス操作子を使用します。  
  
 プロパティの get アクセス操作子を提供できない場合は、代わりにメソッドとして機能を実装します。 メソッド名での開始を検討してください`Set`内容は指定済みの場合、プロパティに従います。 たとえば、<xref:System.AppDomain>というメソッドを持ち`SetCachePath`という設定専用のプロパティではなく`CachePath`です。  
  
 **✓ DO** 既定の設定がセキュリティ ホールや重大な非効率的なコードで発生しないようにする、すべてのプロパティの既定値を指定します。  
  
 **✓ DO** 場合でも、この結果、オブジェクトの一時的な無効な状態で、任意の順序で設定するプロパティを許可します。  
  
 通常は、いくつかの値を 1 つのプロパティの無効になるポイントに相互関連する 2 つ以上のプロパティの同じオブジェクトに対して他のプロパティの値を指定します。 このような場合、相互に関連するプロパティがオブジェクトで一緒に使用が実際になるまで無効な状態に起因する例外を延期する必要があります。  
  
 **✓ DO** プロパティ set アクセス操作子は例外をスローする場合は、以前の値を保持します。  
  
 **X AVOID** プロパティ get アクセス操作子から例外をスローします。  
  
 プロパティの getter は、単純な操作をする必要があり、すべての前提条件にはできません。 場合は、get アクセス操作子は例外をスローできます、その必要があります可能性があります再設計するメソッド。 このルールは、インデクサー、ここで、引数の検証の結果として例外予測には適用されませんに注意してください。  
  
### <a name="indexed-property-design"></a>インデックス付きプロパティのデザイン  
 インデックス付きプロパティは、パラメーターを持つことができますし、配列のインデックスのような特別な構文を使用して呼び出すことができる特別なプロパティです。  
  
 インデックス付きプロパティは、インデクサーとも呼ばれます。 インデクサーは、論理的なコレクション内の項目へのアクセスを提供する Api でのみ使用する必要があります。 たとえば、文字列は、一連の文字とでインデクサー<xref:System.String?displayProperty=nameWithType>その文字にアクセスするようになりました。  
  
 **✓ CONSIDER** 内部配列に格納されたデータへのアクセスを提供するインデクサーを使用します。  
  
 **✓ CONSIDER** 項目のコレクションを表す型のインデクサーを提供します。  
  
 **X AVOID** 1 つ以上のパラメーターを持つプロパティを使用してインデックスを作成します。  
  
 設計には、複数のパラメーターが必要とする場合は、プロパティが実際にアクセサーを表す論理的なコレクションにするかどうかを再確認します。 そうでない場合は、代わりにメソッドを使用します。 まず、メソッド名で`Get`または`Set`です。  
  
 **X AVOID** 以外のパラメーターの型を持つインデクサー <xref:System.Int32?displayProperty=nameWithType>、 <xref:System.Int64?displayProperty=nameWithType>、 <xref:System.String?displayProperty=nameWithType>、 <xref:System.Object?displayProperty=nameWithType>、または列挙型。  
  
 デザインには、その他の種類のパラメーターが必要な厳密 API が実際にアクセサーを表す論理的なコレクションにするかどうかを再評価します。 そうでない場合は、メソッドを使用します。 まず、メソッド名で`Get`または`Set`です。  
  
 **✓ DO** 名前を使用して`Item`の言うまでもなく、名前がある場合を除き、インデックス付きプロパティ (などを参照してください、<xref:System.String.Chars%2A>プロパティを`System.String`)。  
  
 C# の場合、インデクサーは既定では名前付きアイテムです。 <xref:System.Runtime.CompilerServices.IndexerNameAttribute>この名前をカスタマイズするために使用できます。  
  
 **X DO NOT** インデクサーと意味的に等しいメソッドの両方を提供します。  
  
 **X DO NOT** 1 つの型でのオーバー ロードされたインデクサーの 1 つ以上のファミリを指定します。  
  
 これは、c# コンパイラによって強制されます。  
  
 **X DO NOT** 使用する既定以外のインデックス付きプロパティです。  
  
 これは、c# コンパイラによって強制されます。  
  
### <a name="property-change-notification-events"></a>プロパティ変更通知イベント  
 プロパティ値の変更のユーザーに通知するイベントを提供すると便利ですがあります。 たとえば、`System.Windows.Forms.Control`を発生させます、`TextChanged`イベントの値の後にその`Text`プロパティが変更されました。  
  
 **✓ CONSIDER** 大まかな Api (通常、デザイナー コンポーネント) のプロパティ値が変更されたときに通知イベントを変更させるとします。  
  
 ユーザーがオブジェクトのプロパティを変更する場合を判断するための適切なシナリオがある場合、オブジェクトは、プロパティの変更通知イベントを発生させます。  
  
 ただし、イベントを発生させるような低レベルの Api の基本型、コレクションなどのオーバーヘッドすべきである可能性はありません。 たとえば、<xref:System.Collections.Generic.List%601>がない新しい項目が一覧に追加されたときに、このようなイベントを発生させると、`Count`プロパティが変更されました。  
  
 **✓ CONSIDER** 外的要因を使用して、プロパティの値が変更されたときに、通知イベントを発生させる変更します。  
  
 何らかの外的要因 (形で以外のオブジェクトでメソッドを呼び出すことにより) を使用してプロパティ値が変更された場合に発生させるイベントことを示すため、開発者に値が変更が変更されました。 良い例は、`Text`テキスト ボックス コントロールのプロパティです。 ユーザーが内のテキストを入力するときに、`TextBox`プロパティの値が自動的に変更します。  
  
 *部分 © 2005、2009 Microsoft Corporation します。All rights reserved.*  
  
 *ピアソン教育, Inc. からのアクセス許可によって検出[Framework デザイン ガイドライン: 規則、表現方法、および再利用可能な .NET ライブラリを第 2 版パターン](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)は Cwalina と Brad Abrams、2008 年 10 月 22 日で発行されました。Microsoft Windows 開発シリーズの一部として、Addison-wesley Professional。*  
  
## <a name="see-also"></a>関連項目  
 [メンバーのデザインのガイドライン](../../../docs/standard/design-guidelines/member.md)  
 [フレームワーク デザインのガイドライン](../../../docs/standard/design-guidelines/index.md)
