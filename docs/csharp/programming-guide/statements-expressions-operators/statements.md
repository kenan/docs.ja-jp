---
title: ステートメント (C# プログラミング ガイド)
ms.date: 07/20/2015
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
ms.openlocfilehash: 68f7f799ebbfe52c99820083eb22761c79f66483
ms.sourcegitcommit: f6343b070f3c66877338a05c8bfb0be9985255e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2018
ms.locfileid: "39220751"
---
# <a name="statements-c-programming-guide"></a>ステートメント (C# プログラミング ガイド)
プログラムが実行する処理は、ステートメントとして表されます。 一般的な処理には、変数の宣言、値の代入、メソッドの呼び出し、コレクションに対するループ処理、条件に応じたコード ブロックへの分岐などがあります。 プログラム内でステートメントが実行される順序は、制御フローまたは実行フローと呼ばれます。 制御フローは、実行時に渡された入力に対するプログラムの応答に応じて、プログラムを実行するたびに変わる可能性があります。  
  
 ステートメントは、セミコロンで終わる単一行のコードか、1 つのブロックを形成する一連の単一行ステートメントで構成されます。 ステートメント ブロックは中かっこ {} で囲み、入れ子になったブロックを含めることができます。 次のコードは、2 つの単一行ステートメントの例と、1 つの複数行ステートメント ブロックを示しています。  
  
 [!code-csharp[csProgGuideStatements#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_1.cs)]  
  
## <a name="types-of-statements"></a>ステートメントの種類  
 次の表は、C# のさまざまな種類のステートメントと、それぞれに関連付けられているキーワードの一覧です。詳細が記載されているトピックへのリンクも示しています。  
  
|カテゴリ|C# のキーワード/メモ|  
|--------------|---------------------------|  
|宣言ステートメント|宣言ステートメントは、新しい変数または定数を定義します。 変数宣言では、必要に応じて変数に値を代入することができます。 定数宣言では、常に代入が必要です。<br /><br /> [!code-csharp[csProgGuideStatements#23](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_2.cs)]|  
|式ステートメント|値を計算する式ステートメントでは、変数に値を格納する必要があります。<br /><br /> [!code-csharp[csProgGuideStatements#24](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_3.cs)]|  
|[選択ステートメント](../../../csharp/language-reference/keywords/selection-statements.md)|選択ステートメントでは、1 つ以上の指定した条件に応じて、コードのさまざまなセクションに分岐することができます。 詳細については、次のトピックを参照してください。<br /><br /> [if](../../../csharp/language-reference/keywords/if-else.md)、[else](../../../csharp/language-reference/keywords/if-else.md)、[switch](../../../csharp/language-reference/keywords/switch.md)、[case](../../../csharp/language-reference/keywords/switch.md)|  
|[繰り返しステートメント](../../../csharp/language-reference/keywords/iteration-statements.md)|繰り返しステートメントを使用すると、配列などのコレクションをループ処理したり、指定した条件が満たされるまで同じステートメントのセットを繰り返し実行したりできます。 詳細については、次のトピックを参照してください。<br /><br /> [do](../../../csharp/language-reference/keywords/do.md)、[for](../../../csharp/language-reference/keywords/for.md)、[foreach](../../../csharp/language-reference/keywords/foreach-in.md)、[in](../../../csharp/language-reference/keywords/foreach-in.md)、[while](../../../csharp/language-reference/keywords/while.md)|  
|[ジャンプ ステートメント](../../../csharp/language-reference/keywords/jump-statements.md)|ジャンプ ステートメントでは、別のコード セクションに制御を移します。 詳細については、次のトピックを参照してください。<br /><br /> [break](../../../csharp/language-reference/keywords/break.md)、[continue](../../../csharp/language-reference/keywords/continue.md)、[default](../../../csharp/language-reference/keywords/switch.md)、[goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md)、[yield](../../../csharp/language-reference/keywords/yield.md)|  
|[例外処理ステートメント](../../../csharp/language-reference/keywords/exception-handling-statements.md)|例外処理ステートメントを使用すると、実行時に発生する例外状態から適切に回復できます。 詳細については、次のトピックを参照してください。<br /><br /> [throw](../../../csharp/language-reference/keywords/throw.md)、[try-catch](../../../csharp/language-reference/keywords/try-catch.md)、[try-finally](../../../csharp/language-reference/keywords/try-finally.md)、[try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)|  
|[checked と unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)|checked ステートメントと unchecked ステートメントを使用すると、結果の値を保持するには小さすぎる変数に結果が格納される場合に、数値演算でオーバーフローが発生するのを許可するかどうかを指定できます。 詳細については、「[checked](../../../csharp/language-reference/keywords/checked.md)」および「[unchecked](../../../csharp/language-reference/keywords/unchecked.md)」を参照してください。|  
|`await` ステートメント|メソッドに [async](../../../csharp/language-reference/keywords/async.md) 修飾子を付けると、そのメソッドで [await](../../../csharp/language-reference/keywords/await.md) 演算子を使用できます。 コントロールが非同期メソッドの `await` 式に到達すると、コントロールは呼び出し元に戻り、待機中のタスクが完了するまでメソッドの進行状況は中断されます。 タスクが完了すると、メソッドで実行を再開できます。<br /><br /> 簡単な例については、「[メソッド](../../../csharp/programming-guide/classes-and-structs/methods.md)」の「非同期メソッド」セクションを参照してください。 詳細については、「[Async および Await を使用した非同期プログラミング](../../../csharp/programming-guide/concepts/async/index.md)」を参照してください。|  
|`yield return` ステートメント|反復子は、リストや配列など、コレクションに対するカスタム イテレーションを実行します。 反復子は、[yield return](../../../csharp/language-reference/keywords/yield.md) ステートメントを使用して、各要素を 1 回に 1 つ返します。 `yield return` ステートメントに達すると、コードの現在の場所が記憶されます。 反復子が次回呼び出されたとき、この場所から実行が再開されます。<br /><br /> 詳細については、「 [反復子](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)」を参照してください。|  
|`fixed` ステートメント|fixed ステートメントは、移動可能な変数がガベージ コレクターにより再配置されることを防ぎます。 詳細については、「[fixed](../../../csharp/language-reference/keywords/fixed-statement.md)」を参照してください。|  
|`lock` ステートメント|lock ステートメントを使用すると、一度に 1 つのスレッドしかコード ブロックにアクセスしないように制限できます。 詳細については、「[lock](../../../csharp/language-reference/keywords/lock-statement.md)」を参照してください。|  
|ラベル付きステートメント|ステートメントにラベルを付与し、[goto](../../../csharp/language-reference/keywords/goto.md) キーワードを使用して、そのラベル付きステートメントにジャンプできます  (次の行の例を参照してください)。|  
|空のステートメント|空のステートメントは、1 つのセミコロンで構成されます。 このステートメントは何も実行しませんが、ステートメントが必要な場所で、どのような処理も実行する必要がない場合に使用できます。 空のステートメントの 2 つの使用例を次に示します。<br /><br /> [!code-csharp[csProgGuideStatements#25](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_4.cs)]|  
  
## <a name="embedded-statements"></a>埋め込みステートメント  
 [do](../../../csharp/language-reference/keywords/do.md)、[while](../../../csharp/language-reference/keywords/while.md)、[for](../../../csharp/language-reference/keywords/for.md)、[foreach](../../../csharp/language-reference/keywords/foreach-in.md) などの一部のステートメントでは、その後に必ず埋め込みステートメントが続きます。 この埋め込みステートメントは、単一のステートメントか、または複数のステートメントを中かっこ {} で囲んだステートメント ブロックです。 単一行の埋め込みステートメントでも、次の例に示すように中かっこ {} で囲むことができます。  
  
 [!code-csharp[csProgGuideStatements#26](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_5.cs)]  
  
 中かっこ {} で囲まれていない埋め込みステートメントは、宣言ステートメントやラベル付きステートメントにはできません。 以下の例を参照してください。  
  
 [!code-csharp[csProgGuideStatements#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_6.cs)]  
  
 エラーを修正するには、次のように埋め込みステートメントをブロックに配置します。  
  
 [!code-csharp[csProgGuideStatements#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_7.cs)]  
  
## <a name="nested-statement-blocks"></a>入れ子になったステートメント ブロック  
 次のコードに示すように、ステートメント ブロックを入れ子にすることができます。  
  
 [!code-csharp[csProgGuideStatements#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_8.cs)]  
  
## <a name="unreachable-statements"></a>到達できないステートメント  
 コンパイラは、どのような状況でも特定のステートメントに制御フローが到達できないと判断すると、次の例のように、警告 CS0162 を生成します。  
  
 [!code-csharp[csProgGuideStatements#22](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_9.cs)]  
  
## <a name="related-sections"></a>関連項目  
  
-   [ステートメントのキーワード](../../../csharp/language-reference/keywords/statement-keywords.md)  
  
-   [式](../../../csharp/programming-guide/statements-expressions-operators/expressions.md)  
  
-   [演算子](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>参照  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)
