---
title: "ICorProfilerCallback::AssemblyUnloadFinished メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.AssemblyUnloadFinished
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::AssemblyUnloadFinished
helpviewer_keywords:
- AssemblyUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::AssemblyUnloadFinished method [.NET Framework profiling]
ms.assetid: 53fca564-84b1-44d4-9e21-17a492d2aae7
topic_type: apiref
caps.latest.revision: "14"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 144f7af59afbb403d9ec1894f06c5c028b767416
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilercallbackassemblyunloadfinished-method"></a><span data-ttu-id="4a598-102">ICorProfilerCallback::AssemblyUnloadFinished メソッド</span><span class="sxs-lookup"><span data-stu-id="4a598-102">ICorProfilerCallback::AssemblyUnloadFinished Method</span></span>
<span data-ttu-id="4a598-103">アセンブリがアンロードされたことをプロファイラーに通知します。</span><span class="sxs-lookup"><span data-stu-id="4a598-103">Notifies the profiler that an assembly has been unloaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4a598-104">構文</span><span class="sxs-lookup"><span data-stu-id="4a598-104">Syntax</span></span>  
  
```  
HRESULT AssemblyUnloadFinished(  
    [in] AssemblyID assemblyId,  
    [in] HRESULT    hrStatus);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="4a598-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="4a598-105">Parameters</span></span>  
 `assemblyId`  
 <span data-ttu-id="4a598-106">[in]モジュールはアンロードされているアセンブリを識別します。</span><span class="sxs-lookup"><span data-stu-id="4a598-106">[in] Identifies the assembly that is being unloaded.</span></span>  
  
 `hrStatus`  
 <span data-ttu-id="4a598-107">[in]かどうか、アセンブリがアンロードされました正常を示す HRESULT。</span><span class="sxs-lookup"><span data-stu-id="4a598-107">[in] An HRESULT that indicates whether the assembly was unloaded successfully.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4a598-108">コメント</span><span class="sxs-lookup"><span data-stu-id="4a598-108">Remarks</span></span>  
 <span data-ttu-id="4a598-109">値`assemblyId`後情報の要求に対して無効です、 [icorprofilercallback::assemblyunloadstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyunloadstarted-method.md)メソッドを返します。</span><span class="sxs-lookup"><span data-stu-id="4a598-109">The value of `assemblyId` is not valid for an information request after the [ICorProfilerCallback::AssemblyUnloadStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyunloadstarted-method.md) method returns.</span></span>  
  
 <span data-ttu-id="4a598-110">アセンブリをアンロードの一部が後に続ける可能性があります、`AssemblyUnloadFinished`コールバック。</span><span class="sxs-lookup"><span data-stu-id="4a598-110">Some parts of unloading the assembly might continue after the `AssemblyUnloadFinished` callback.</span></span> <span data-ttu-id="4a598-111">失敗を示す HRESULT で`hrStatus`は失敗を示します。</span><span class="sxs-lookup"><span data-stu-id="4a598-111">A failure HRESULT in `hrStatus` indicates a failure.</span></span> <span data-ttu-id="4a598-112">ただし、成功 HRESULT で`hrStatus`のみのアセンブリをアンロードの最初の部分が成功したことを示します。</span><span class="sxs-lookup"><span data-stu-id="4a598-112">However, a success HRESULT in `hrStatus` indicates only that the first part of unloading the assembly has succeeded.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4a598-113">要件</span><span class="sxs-lookup"><span data-stu-id="4a598-113">Requirements</span></span>  
 <span data-ttu-id="4a598-114">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="4a598-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4a598-115">**ヘッダー** : CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="4a598-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="4a598-116">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4a598-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4a598-117">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4a598-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4a598-118">関連項目</span><span class="sxs-lookup"><span data-stu-id="4a598-118">See Also</span></span>  
 [<span data-ttu-id="4a598-119">ICorProfilerCallback インターフェイス</span><span class="sxs-lookup"><span data-stu-id="4a598-119">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)