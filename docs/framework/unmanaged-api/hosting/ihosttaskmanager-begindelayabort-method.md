---
title: "IHostTaskManager::BeginDelayAbort メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostTaskManager.BeginDelayAbort
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostTaskManager::BeginDelayAbort
helpviewer_keywords:
- BeginDelayAbort method [.NET Framework hosting]
- IHostTaskManager::BeginDelayAbort method [.NET Framework hosting]
ms.assetid: 75f42a8b-ed68-4718-a030-a179cfba7d72
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 17af69c533c62b6a25d498fb245dfefe162690ff
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="ihosttaskmanagerbegindelayabort-method"></a><span data-ttu-id="c3e70-102">IHostTaskManager::BeginDelayAbort メソッド</span><span class="sxs-lookup"><span data-stu-id="c3e70-102">IHostTaskManager::BeginDelayAbort Method</span></span>
<span data-ttu-id="c3e70-103">現在のタスクを中止できません期間が入るマネージ コードをホストに通知します。</span><span class="sxs-lookup"><span data-stu-id="c3e70-103">Notifies the host that managed code is entering a period in which the current task must not be aborted.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c3e70-104">構文</span><span class="sxs-lookup"><span data-stu-id="c3e70-104">Syntax</span></span>  
  
```  
HRESULT BeginDelayAbort ();  
```  
  
## <a name="return-value"></a><span data-ttu-id="c3e70-105">戻り値</span><span class="sxs-lookup"><span data-stu-id="c3e70-105">Return Value</span></span>  
  
|<span data-ttu-id="c3e70-106">HRESULT</span><span class="sxs-lookup"><span data-stu-id="c3e70-106">HRESULT</span></span>|<span data-ttu-id="c3e70-107">説明</span><span class="sxs-lookup"><span data-stu-id="c3e70-107">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="c3e70-108">S_OK</span><span class="sxs-lookup"><span data-stu-id="c3e70-108">S_OK</span></span>|<span data-ttu-id="c3e70-109">`BeginDelayAbort`正常に返されます。</span><span class="sxs-lookup"><span data-stu-id="c3e70-109">`BeginDelayAbort` returned successfully.</span></span>|  
|<span data-ttu-id="c3e70-110">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="c3e70-110">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="c3e70-111">共通言語ランタイム (CLR) が、プロセスに読み込まれていませんまたは CLR は、状態をマネージ コードを実行またはできないの呼び出しは正常に処理します。</span><span class="sxs-lookup"><span data-stu-id="c3e70-111">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="c3e70-112">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="c3e70-112">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="c3e70-113">呼び出しがタイムアウトしました。</span><span class="sxs-lookup"><span data-stu-id="c3e70-113">The call timed out.</span></span>|  
|<span data-ttu-id="c3e70-114">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="c3e70-114">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="c3e70-115">呼び出し元は、ロックを所有していません。</span><span class="sxs-lookup"><span data-stu-id="c3e70-115">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="c3e70-116">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="c3e70-116">HOST_E_ABANDONED</span></span>|<span data-ttu-id="c3e70-117">イベントがキャンセルされましたブロックされたスレッドまたはファイバーが待機しています。</span><span class="sxs-lookup"><span data-stu-id="c3e70-117">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="c3e70-118">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="c3e70-118">E_FAIL</span></span>|<span data-ttu-id="c3e70-119">不明な致命的なエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="c3e70-119">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="c3e70-120">メソッドには、E_FAIL が返される、ときに、CLR は、プロセス内で使用可能ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="c3e70-120">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="c3e70-121">メソッドのホストに以降の呼び出しでは、HOST_E_CLRNOTAVAILABLE を返します。</span><span class="sxs-lookup"><span data-stu-id="c3e70-121">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="c3e70-122">E_UNEXPECTED</span><span class="sxs-lookup"><span data-stu-id="c3e70-122">E_UNEXPECTED</span></span>|<span data-ttu-id="c3e70-123">`BeginDelayAbort`既に呼び出されてに対応する呼び出しが[EndDelayAbort](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enddelayabort-method.md)が受け取られていません。</span><span class="sxs-lookup"><span data-stu-id="c3e70-123">`BeginDelayAbort` has already been called, but the corresponding call to [EndDelayAbort](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enddelayabort-method.md) has not yet been received.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c3e70-124">コメント</span><span class="sxs-lookup"><span data-stu-id="c3e70-124">Remarks</span></span>  
 <span data-ttu-id="c3e70-125">ホストがまで、現在のタスクを中止しなければなりません`EndDelayAbort`と呼びます。</span><span class="sxs-lookup"><span data-stu-id="c3e70-125">The host must not abort the current task until `EndDelayAbort` is called.</span></span> <span data-ttu-id="c3e70-126">別の呼び出しに場合`BeginDelayAbort`せずに中間の呼び出しが行われます`EndDelayAbort`、ホストから E_UNEXPECTED を返す必要があります`BeginDelayAbort`は操作を行わないとします。</span><span class="sxs-lookup"><span data-stu-id="c3e70-126">If another call to `BeginDelayAbort` is made without an intervening call to `EndDelayAbort`, the host should return E_UNEXPECTED from `BeginDelayAbort`, and should take no action.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c3e70-127">要件</span><span class="sxs-lookup"><span data-stu-id="c3e70-127">Requirements</span></span>  
 <span data-ttu-id="c3e70-128">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="c3e70-128">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c3e70-129">**ヘッダー:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="c3e70-129">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="c3e70-130">**ライブラリ:** MSCorEE.dll にリソースとして含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3e70-130">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c3e70-131">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c3e70-131">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c3e70-132">関連項目</span><span class="sxs-lookup"><span data-stu-id="c3e70-132">See Also</span></span>  
 [<span data-ttu-id="c3e70-133">ICLRTask インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c3e70-133">ICLRTask Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)  
 [<span data-ttu-id="c3e70-134">ICLRTaskManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c3e70-134">ICLRTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)  
 [<span data-ttu-id="c3e70-135">IHostTaskManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c3e70-135">IHostTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)  
 [<span data-ttu-id="c3e70-136">IHostTaskManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c3e70-136">IHostTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)