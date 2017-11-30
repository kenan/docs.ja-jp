---
title: "ICorProfilerCallback::ModuleLoadFinished メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.ModuleLoadFinished
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::ModuleLoadFinished
helpviewer_keywords:
- ModuleLoadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleLoadFinished method [.NET Framework profiling]
ms.assetid: 050649e5-ffc0-4458-a0a4-d9ee128a219e
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 22533187da02d34ac2990f351b13bd892a760620
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilercallbackmoduleloadfinished-method"></a><span data-ttu-id="473a3-102">ICorProfilerCallback::ModuleLoadFinished メソッド</span><span class="sxs-lookup"><span data-stu-id="473a3-102">ICorProfilerCallback::ModuleLoadFinished Method</span></span>
<span data-ttu-id="473a3-103">モジュールの読み込みが完了したことをプロファイラーに通知します。</span><span class="sxs-lookup"><span data-stu-id="473a3-103">Notifies the profiler that a module has finished loading.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="473a3-104">構文</span><span class="sxs-lookup"><span data-stu-id="473a3-104">Syntax</span></span>  
  
```  
HRESULT ModuleLoadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="473a3-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="473a3-105">Parameters</span></span>  
 `moduleId`  
 <span data-ttu-id="473a3-106">[in]読み込みが完了したら、モジュールの ID。</span><span class="sxs-lookup"><span data-stu-id="473a3-106">[in] The ID of the module that has finished loading.</span></span>  
  
 `hrStatus`  
 <span data-ttu-id="473a3-107">[in]モジュールが正常に読み込まれたかどうかを示す HRESULT。</span><span class="sxs-lookup"><span data-stu-id="473a3-107">[in] An HRESULT that indicates whether the module was loaded successfully.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="473a3-108">コメント</span><span class="sxs-lookup"><span data-stu-id="473a3-108">Remarks</span></span>  
 <span data-ttu-id="473a3-109">値`moduleId`まで情報の要求に対して無効です、`ModuleLoadFinished`メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="473a3-109">The value of `moduleId` is not valid for an information request until the `ModuleLoadFinished` method is called.</span></span>  
  
 <span data-ttu-id="473a3-110">モジュールの読み込みの一部が後に続ける可能性があります、`ModuleLoadFinished`コールバック。</span><span class="sxs-lookup"><span data-stu-id="473a3-110">Some parts of loading the module might continue after the `ModuleLoadFinished` callback.</span></span> <span data-ttu-id="473a3-111">失敗を示す HRESULT で`hrStatus`は失敗を示します。</span><span class="sxs-lookup"><span data-stu-id="473a3-111">A failure HRESULT in `hrStatus` indicates a failure.</span></span> <span data-ttu-id="473a3-112">ただし、成功 HRESULT で`hrStatus`のみのモジュールの読み込みの最初の部分が成功したことを示します。</span><span class="sxs-lookup"><span data-stu-id="473a3-112">However, a success HRESULT in `hrStatus` indicates only that the first part of loading the module has succeeded.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="473a3-113">要件</span><span class="sxs-lookup"><span data-stu-id="473a3-113">Requirements</span></span>  
 <span data-ttu-id="473a3-114">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="473a3-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="473a3-115">**ヘッダー** : CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="473a3-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="473a3-116">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="473a3-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="473a3-117">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="473a3-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="473a3-118">関連項目</span><span class="sxs-lookup"><span data-stu-id="473a3-118">See Also</span></span>  
 [<span data-ttu-id="473a3-119">ICorProfilerCallback インターフェイス</span><span class="sxs-lookup"><span data-stu-id="473a3-119">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [<span data-ttu-id="473a3-120">ModuleLoadStarted メソッド</span><span class="sxs-lookup"><span data-stu-id="473a3-120">ModuleLoadStarted Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadstarted-method.md)