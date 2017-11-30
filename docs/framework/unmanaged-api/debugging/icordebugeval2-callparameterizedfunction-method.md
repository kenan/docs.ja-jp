---
title: "ICorDebugEval2::CallParameterizedFunction メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugEval2.CallParameterizedFunction
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugEval2::CallParameterizedFunction
helpviewer_keywords:
- ICorDebugEval2::CallParameterizedFunction method [.NET Framework debugging]
- CallParameterizedFunction method [.NET Framework debugging]
ms.assetid: 72f54a45-dbe6-4bb4-8c99-e879a27368e5
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 720d9c4fb9b997538ee2bb18ac7987350f6bfb57
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugeval2callparameterizedfunction-method"></a><span data-ttu-id="bde53-102">ICorDebugEval2::CallParameterizedFunction メソッド</span><span class="sxs-lookup"><span data-stu-id="bde53-102">ICorDebugEval2::CallParameterizedFunction Method</span></span>
<span data-ttu-id="bde53-103">コンス トラクターは、クラス内で入れ子にできる指定の ICorDebugFunction への呼び出しを設定<xref:System.Type>パラメーター、またはそれ自体がとれる<xref:System.Type>パラメーター。</span><span class="sxs-lookup"><span data-stu-id="bde53-103">Sets up a call to the specified ICorDebugFunction, which can be nested inside a class whose constructor takes <xref:System.Type> parameters, or can itself take <xref:System.Type> parameters.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bde53-104">構文</span><span class="sxs-lookup"><span data-stu-id="bde53-104">Syntax</span></span>  
  
```  
HRESULT CallParameterizedFunction (  
    [in] ICorDebugFunction     *pFunction,  
    [in] ULONG32               nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType *ppTypeArgs[],  
    [in] ULONG32               nArgs,  
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="bde53-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="bde53-105">Parameters</span></span>  
 `pFunction`  
 <span data-ttu-id="bde53-106">[in]ポインター、`ICorDebugFunction`に呼び出される関数を表すオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="bde53-106">[in] A pointer to an `ICorDebugFunction` object that represents the function to be called.</span></span>  
  
 `nTypeArgs`  
 <span data-ttu-id="bde53-107">[in]関数が受け取る引数の数。</span><span class="sxs-lookup"><span data-stu-id="bde53-107">[in] The number of arguments that the function takes.</span></span>  
  
 `ppTypeArgs`  
 <span data-ttu-id="bde53-108">[in]関数の引数を表す ICorDebugType オブジェクトを指し示すそれぞれが、ポインターの配列。</span><span class="sxs-lookup"><span data-stu-id="bde53-108">[in] An array of pointers, each of which points to an ICorDebugType object that represents a function argument.</span></span>  
  
 `nArgs`  
 <span data-ttu-id="bde53-109">[in]値の数は、関数に渡されます。</span><span class="sxs-lookup"><span data-stu-id="bde53-109">[in] The number of values passed in the function.</span></span>  
  
 `ppArgs`  
 <span data-ttu-id="bde53-110">[in]関数の引数の値を表す ICorDebugValue オブジェクトを指し示すそれぞれが、ポインターの配列が渡されます。</span><span class="sxs-lookup"><span data-stu-id="bde53-110">[in] An array of pointers, each of which points to an ICorDebugValue object that represents a value passed in a function argument.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="bde53-111">コメント</span><span class="sxs-lookup"><span data-stu-id="bde53-111">Remarks</span></span>  
 <span data-ttu-id="bde53-112">`CallParameterizedFunction`同様に、 [icordebugeval::callfunction](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md)関数は、型パラメーターを持つクラスの内部である可能性があります、する点を除いてかかる場合があります自体の型パラメーター、またはその両方です。</span><span class="sxs-lookup"><span data-stu-id="bde53-112">`CallParameterizedFunction` is like [ICorDebugEval::CallFunction](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md) except that the function may be inside a class with type parameters, may itself take type parameters, or both.</span></span> <span data-ttu-id="bde53-113">クラスのしてから、関数、型引数を最初に指定してください。</span><span class="sxs-lookup"><span data-stu-id="bde53-113">The type arguments should be given first for the class, and then for the function.</span></span>  
  
 <span data-ttu-id="bde53-114">関数は、別のアプリケーション ドメインでは、遷移が発生します。</span><span class="sxs-lookup"><span data-stu-id="bde53-114">If the function is in a different application domain, a transition will occur.</span></span> <span data-ttu-id="bde53-115">ただし、すべての型と値の引数は、対象のアプリケーション ドメインにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bde53-115">However, all type and value arguments must be in the target application domain.</span></span>  
  
 <span data-ttu-id="bde53-116">関数の評価は、限られたシナリオでのみ実行できます。</span><span class="sxs-lookup"><span data-stu-id="bde53-116">Function evaluation can be performed only in limited scenarios.</span></span> <span data-ttu-id="bde53-117">場合`CallParameterizedFunction`または`ICorDebugEval::CallFunction`失敗した場合、返された HRESULT エラーに対する最も一般的な原因が示されます。</span><span class="sxs-lookup"><span data-stu-id="bde53-117">If `CallParameterizedFunction` or `ICorDebugEval::CallFunction` fails, the returned HRESULT will indicate the most general possible reason for failure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="bde53-118">要件</span><span class="sxs-lookup"><span data-stu-id="bde53-118">Requirements</span></span>  
 <span data-ttu-id="bde53-119">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="bde53-119">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bde53-120">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="bde53-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="bde53-121">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="bde53-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="bde53-122">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="bde53-122">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>