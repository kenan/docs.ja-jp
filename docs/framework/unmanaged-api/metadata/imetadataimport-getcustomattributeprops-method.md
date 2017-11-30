---
title: "IMetaDataImport::GetCustomAttributeProps メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataImport.GetCustomAttributeProps
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataImport::GetCustomAttributeProps
helpviewer_keywords:
- GetCustomAttributeProps method [.NET Framework metadata]
- IMetaDataImport::GetCustomAttributeProps method [.NET Framework metadata]
ms.assetid: 6eefb243-a281-41c1-bcdc-7e17513bc446
topic_type: apiref
caps.latest.revision: "14"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 415b1dc67bd3ae3638edd61558cc9e13ebf03fd8
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataimportgetcustomattributeprops-method"></a><span data-ttu-id="c2a1a-102">IMetaDataImport::GetCustomAttributeProps メソッド</span><span class="sxs-lookup"><span data-stu-id="c2a1a-102">IMetaDataImport::GetCustomAttributeProps Method</span></span>
<span data-ttu-id="c2a1a-103">指定したメタデータ トークンのカスタム属性の値を取得します。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-103">Gets the value of the custom attribute, given its metadata token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c2a1a-104">構文</span><span class="sxs-lookup"><span data-stu-id="c2a1a-104">Syntax</span></span>  
  
```  
HRESULT GetCustomAttributeProps (  
   [in]            mdCustomAttribute   cv,  
   [out, optional] mdToken             *ptkObj,  
   [out, optional] mdToken             *ptkType,  
   [out, optional] void const          **ppBlob,  
   [out, optional] ULONG               *pcbSize  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="c2a1a-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c2a1a-105">Parameters</span></span>  
 `cv`  
 <span data-ttu-id="c2a1a-106">[in] 取得するカスタム属性を表すメタデータ トークン。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-106">[in] A metadata token that represents the custom attribute to be retrieved.</span></span>  
  
 `ptkObj`  
 <span data-ttu-id="c2a1a-107">[out](省略可能) カスタム属性が変更されるオブジェクトを表すメタデータ トークン。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-107">[out, optional] A metadata token representing the object that the custom attribute modifies.</span></span> <span data-ttu-id="c2a1a-108">この値には、`mdCustomAttribute` を除く任意の種類のトークンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-108">This value can be any type of metadata token except `mdCustomAttribute`.</span></span>  
  
 `ptkType`  
 <span data-ttu-id="c2a1a-109">[out](省略可能) 返されるカスタム属性の <xref:System.Type> を表す `mdMethodDef` または `mdMemberRef` メタデータ トークン。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-109">[out, optional] An `mdMethodDef` or `mdMemberRef` metadata token representing the <xref:System.Type> of the returned custom attribute.</span></span>  
  
 `ppBlob`  
 <span data-ttu-id="c2a1a-110">[out](省略可能) カスタム属性の値であるデータの配列へのポインター。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-110">[out, optional] A pointer to an array of data that is the value of the custom attribute.</span></span>  
  
 `pcbSize`  
 <span data-ttu-id="c2a1a-111">[out](省略可能) *`ppBlob` に返されたデータのサイズ (バイト単位)。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-111">[out, optional] The size in bytes of the data returned in *`ppBlob`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c2a1a-112">コメント</span><span class="sxs-lookup"><span data-stu-id="c2a1a-112">Remarks</span></span>  
 <span data-ttu-id="c2a1a-113">カスタム属性はデータの配列として格納され、その形式はメタデータ エンジンによって解釈されます。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-113">A custom attribute is stored as an array of data, the format which is understood by the metadata engine.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c2a1a-114">要件</span><span class="sxs-lookup"><span data-stu-id="c2a1a-114">Requirements</span></span>  
 <span data-ttu-id="c2a1a-115">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c2a1a-116">**ヘッダー:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="c2a1a-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="c2a1a-117">**ライブラリ:** MsCorEE.dll にリソースとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="c2a1a-117">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="c2a1a-118">**.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c2a1a-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c2a1a-119">関連項目</span><span class="sxs-lookup"><span data-stu-id="c2a1a-119">See Also</span></span>  
 [<span data-ttu-id="c2a1a-120">IMetaDataImport インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c2a1a-120">IMetaDataImport Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [<span data-ttu-id="c2a1a-121">IMetaDataImport2 インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c2a1a-121">IMetaDataImport2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)