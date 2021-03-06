---
title: サポートされている UI オートメーション コントロール パターンの取得
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, getting
- UI Automation, getting control patterns
- getting, control patterns
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
author: Xansky
ms.author: mhopkins
manager: markl
ms.openlocfilehash: fe492aa322f005e3bd118031e97e3837e3314093
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33410193"
---
# <a name="get-supported-ui-automation-control-patterns"></a>サポートされている UI オートメーション コントロール パターンの取得
> [!NOTE]
>  このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージ <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI Automation (Windows のオートメーション API: UI オートメーション)](http://go.microsoft.com/fwlink/?LinkID=156746)」を参照してください。  
  
 このトピックからコントロール パターン オブジェクトを取得する方法を示しています。[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]要素。  
  
### <a name="obtain-all-control-patterns"></a>すべてのコントロール パターンの取得  
  
1.  取得、<xref:System.Windows.Automation.AutomationElement>をコントロールが対象とするパターンします。  
  
2.  呼び出す<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>要素からすべてのコントロール パターンを取得します。  
  
> [!CAUTION]
>  クライアントが使用しないことを強くお勧め<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>です。 パフォーマンスに深刻な影響ようにこのメソッドを呼び出します<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>の各既存のコントロール パターンを内部的にします。 可能であれば、クライアントが呼び出す必要があります<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>の主なパターンです。  
  
### <a name="obtain-a-specific-control-pattern"></a>特定のコントロール パターンの取得  
  
1.  取得、<xref:System.Windows.Automation.AutomationElement>をコントロールが対象とするパターンします。  
  
2.  呼び出す<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>または<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>特定のパターンを照会します。 これらのメソッドと同様に、パターンが見つからない場合は<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>、例外が発生し、<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>を返します`false`です。  
  
## <a name="example"></a>例  
 次の例を取得、<xref:System.Windows.Automation.AutomationElement>リスト項目を取得し、<xref:System.Windows.Automation.SelectionItemPattern>その要素から。  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a>関連項目  
 [クライアントの UI オートメーション コントロール パターン](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
