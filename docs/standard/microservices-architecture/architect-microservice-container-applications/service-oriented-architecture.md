---
title: サービス指向アーキテクチャ
description: '.NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ | サービス指向アーキテクチャ'
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 67560cc93b3d147be36a691af440bb78f2315557
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2018
ms.locfileid: "37105006"
---
# <a name="service-oriented-architecture"></a>サービス指向アーキテクチャ 

サービス指向アーキテクチャ (SOA) は乱用されている用語であり、人によって異なる意味で使われています。 ただし、共通の基準としての SOA は、アプリケーションをサブシステムや階層などのさまざまな種類に分類できる複数のサービス (通常は HTTP サービス) に分解して、アプリケーションを構築することを意味します。

このようなサービスは Docker コンテナーとして展開できます。すべての依存関係がコンテナー イメージに含まれているため、展開の問題が解決します。 ただし、SOA アプリケーションをスケール アップする必要がある場合、単一の Docker ホストに基づいて展開すると、スケーラビリティと可用性に問題が生じる可能性があります。 このような場合に Docker クラスタリング ソフトウェアまたはオーケストレーターが役立ちます。詳細については、マイクロサービスの展開アプローチについて説明する後述のセクションを参照してください。

Docker コンテナーは、従来のサービス指向アーキテクチャと高度なマイクロサービス アーキテクチャの両方にとって便利な機能です (ただし、必須ではありません)。

マイクロサービスは SOA に由来しますが、SOA はマイクロサービス アーキテクチャとは異なります。 大規模な中央のブローカー、組織レベルの中央のオーケストレーター、[エンタープライズ サービス バス (ESB)](https://en.wikipedia.org/wiki/Enterprise_service_bus) などは、SOA の典型的な機能です。 ただしほとんどの場合、マイクロサービス コミュニティではこれらはアンチパターンです。 実際、一部の人は "マイクロサービス アーキテクチャはきちんとした SOA だ" と主張しています。

このガイドでは、マイクロサービスに焦点を当てています。なぜなら、SOA アプローチは、マイクロサービス アーキテクチャで使用される要件や手法ほど規範的ではないからです。 マイクロサービスベースのアプリケーションを構築する方法がわかれば、より単純なサービス指向アプリケーションを構築する方法もわかります。




>[!div class="step-by-step"]
[前へ](docker-application-state-data.md)
[次へ](microservices-architecture.md)
