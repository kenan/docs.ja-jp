---
title: "IHostMemoryManager::VirtualFree メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostMemoryManager.VirtualFree
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostMemoryManager::VirtualFree
helpviewer_keywords:
- IHostMemoryManager::VirtualFree method [.NET Framework hosting]
- VirtualFree method [.NET Framework hosting]
ms.assetid: 1a436e89-eb28-4d15-bcf1-a072f86dbd99
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 468228101403c7ce3c123401e906e3ccbe301e28
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="ihostmemorymanagervirtualfree-method"></a><span data-ttu-id="d14fb-102">IHostMemoryManager::VirtualFree メソッド</span><span class="sxs-lookup"><span data-stu-id="d14fb-102">IHostMemoryManager::VirtualFree Method</span></span>
<span data-ttu-id="d14fb-103">対応する Win32 関数の論理ラッパーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="d14fb-103">Serves as a logical wrapper for the corresponding Win32 function.</span></span> <span data-ttu-id="d14fb-104">Win32 実装`VirtualFree`解放、デコミット、またはを解放し、呼び出し元プロセスの仮想アドレス空間内のページの領域をデコミットします。</span><span class="sxs-lookup"><span data-stu-id="d14fb-104">The Win32 implementation of `VirtualFree` releases, decommits, or releases and decommits a region of pages within the virtual address space of the calling process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d14fb-105">構文</span><span class="sxs-lookup"><span data-stu-id="d14fb-105">Syntax</span></span>  
  
```  
HRESULT VirtualFree (  
    [in] LPVOID  lpAddress,  
    [in] SIZE_T  dwSize,  
    [in] DWORD   dwFreeType  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="d14fb-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="d14fb-106">Parameters</span></span>  
 `lpAddress`  
 <span data-ttu-id="d14fb-107">[in]解放される仮想メモリ ページの基本アドレスへのポインター。</span><span class="sxs-lookup"><span data-stu-id="d14fb-107">[in] A pointer to the base address of the virtual memory pages to be freed.</span></span>  
  
 `dwSize`  
 <span data-ttu-id="d14fb-108">[in](バイト単位) が解放される領域のサイズ。</span><span class="sxs-lookup"><span data-stu-id="d14fb-108">[in] The size, in bytes, of the region to be freed.</span></span>  
  
 `dwFreeType`  
 <span data-ttu-id="d14fb-109">[in]解放操作の種類。</span><span class="sxs-lookup"><span data-stu-id="d14fb-109">[in] The type of freeing operation.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d14fb-110">戻り値</span><span class="sxs-lookup"><span data-stu-id="d14fb-110">Return Value</span></span>  
  
|<span data-ttu-id="d14fb-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="d14fb-111">HRESULT</span></span>|<span data-ttu-id="d14fb-112">説明</span><span class="sxs-lookup"><span data-stu-id="d14fb-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="d14fb-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="d14fb-113">S_OK</span></span>|<span data-ttu-id="d14fb-114">`VirtualFree`正常に返されます。</span><span class="sxs-lookup"><span data-stu-id="d14fb-114">`VirtualFree` returned successfully.</span></span>|  
|<span data-ttu-id="d14fb-115">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="d14fb-115">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="d14fb-116">共通言語ランタイム (CLR) が、プロセスに読み込まれていませんまたは CLR は、状態をマネージ コードを実行またはできないの呼び出しは正常に処理します。</span><span class="sxs-lookup"><span data-stu-id="d14fb-116">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="d14fb-117">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="d14fb-117">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="d14fb-118">呼び出しがタイムアウトしました。</span><span class="sxs-lookup"><span data-stu-id="d14fb-118">The call timed out.</span></span>|  
|<span data-ttu-id="d14fb-119">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="d14fb-119">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="d14fb-120">呼び出し元は、ロックを所有していません。</span><span class="sxs-lookup"><span data-stu-id="d14fb-120">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="d14fb-121">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="d14fb-121">HOST_E_ABANDONED</span></span>|<span data-ttu-id="d14fb-122">イベントがキャンセルされましたブロックされたスレッドまたはファイバーが待機しています。</span><span class="sxs-lookup"><span data-stu-id="d14fb-122">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="d14fb-123">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="d14fb-123">E_FAIL</span></span>|<span data-ttu-id="d14fb-124">不明な致命的なエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="d14fb-124">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="d14fb-125">メソッドには、E_FAIL が返される、ときに、CLR は、プロセス内で使用可能ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="d14fb-125">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="d14fb-126">メソッドのホストに以降の呼び出しでは、HOST_E_CLRNOTAVAILABLE を返します。</span><span class="sxs-lookup"><span data-stu-id="d14fb-126">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="d14fb-127">HOST_E_INVALIDOPERATION</span><span class="sxs-lookup"><span data-stu-id="d14fb-127">HOST_E_INVALIDOPERATION</span></span>|<span data-ttu-id="d14fb-128">ホストが割り当てられていないメモリを解放しようとしました。</span><span class="sxs-lookup"><span data-stu-id="d14fb-128">An attempt was made to free memory that was not allocated through the host.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="d14fb-129">コメント</span><span class="sxs-lookup"><span data-stu-id="d14fb-129">Remarks</span></span>  
 <span data-ttu-id="d14fb-130">`VirtualFree`関連付けられている仮想メモリ ページの解放、`lpAddress`事前に呼び出したを通じてパラメーター、 [ihostmemorymanager::virtualalloc](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualalloc-method.md)関数。</span><span class="sxs-lookup"><span data-stu-id="d14fb-130">`VirtualFree` frees virtual memory pages associated with the `lpAddress` parameter through an earlier call to the [IHostMemoryManager::VirtualAlloc](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualalloc-method.md) function.</span></span> <span data-ttu-id="d14fb-131">ホストが割り当てられていないメモリを解放する試行は、HOST_E_INVALIDOPERATION を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d14fb-131">Attempts to free memory that was not allocated through the host should return HOST_E_INVALIDOPERATION.</span></span>  
  
 <span data-ttu-id="d14fb-132">セマンティクスは次の Win32 実装のものと同じ`VirtualFree`です。</span><span class="sxs-lookup"><span data-stu-id="d14fb-132">The semantics are identical to those of the Win32 implementation of `VirtualFree`.</span></span> <span data-ttu-id="d14fb-133">詳細については、Windows プラットフォームのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d14fb-133">For more information, see the Windows Platform documentation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d14fb-134">要件</span><span class="sxs-lookup"><span data-stu-id="d14fb-134">Requirements</span></span>  
 <span data-ttu-id="d14fb-135">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="d14fb-135">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d14fb-136">**ヘッダー:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="d14fb-136">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="d14fb-137">**ライブラリ:** MSCorEE.dll にリソースとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="d14fb-137">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="d14fb-138">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d14fb-138">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d14fb-139">関連項目</span><span class="sxs-lookup"><span data-stu-id="d14fb-139">See Also</span></span>  
 [<span data-ttu-id="d14fb-140">IHostMemoryManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="d14fb-140">IHostMemoryManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)  
 [<span data-ttu-id="d14fb-141">IHostMalloc インターフェイス</span><span class="sxs-lookup"><span data-stu-id="d14fb-141">IHostMalloc Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-interface.md)