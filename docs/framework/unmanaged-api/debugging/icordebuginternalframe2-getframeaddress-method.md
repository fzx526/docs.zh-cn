---
title: "ICorDebugInternalFrame2::GetFrameAddress 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugInternalFrame2.GetFrameAddress Method
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugInternalFrame2::GetFrameAddress
helpviewer_keywords:
- GetFrameAddress method [.NET Framework debugging]
- ICorDebugInternalFrame2::GetFrameAddress method [.NET Framework debugging]
ms.assetid: 4ee8d058-ffc8-4967-9133-a5adfef4e518
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 9ee867afe99fc5d2f2eb27bb1e6888aef8341d71
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="icordebuginternalframe2getframeaddress-method"></a><span data-ttu-id="3525a-102">ICorDebugInternalFrame2::GetFrameAddress 方法</span><span class="sxs-lookup"><span data-stu-id="3525a-102">ICorDebugInternalFrame2::GetFrameAddress Method</span></span>
<span data-ttu-id="3525a-103">返回内部帧的堆栈地址。</span><span class="sxs-lookup"><span data-stu-id="3525a-103">Returns the stack address of the internal frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3525a-104">语法</span><span class="sxs-lookup"><span data-stu-id="3525a-104">Syntax</span></span>  
  
```  
HRESULT GetFrameAddress([out] CORDB_ADDRESS *pAddress);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="3525a-105">参数</span><span class="sxs-lookup"><span data-stu-id="3525a-105">Parameters</span></span>  
 `pAddress`  
 <span data-ttu-id="3525a-106">[out]指向`CORDB_ADDRESS`内部的帧。</span><span class="sxs-lookup"><span data-stu-id="3525a-106">[out] Pointer to the `CORDB_ADDRESS` for the internal frame.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="3525a-107">返回值</span><span class="sxs-lookup"><span data-stu-id="3525a-107">Return Value</span></span>  
 <span data-ttu-id="3525a-108">此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。</span><span class="sxs-lookup"><span data-stu-id="3525a-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="3525a-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="3525a-109">HRESULT</span></span>|<span data-ttu-id="3525a-110">描述</span><span class="sxs-lookup"><span data-stu-id="3525a-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="3525a-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="3525a-111">S_OK</span></span>|<span data-ttu-id="3525a-112">成功地返回内部帧的地址。</span><span class="sxs-lookup"><span data-stu-id="3525a-112">The address of the internal frame was successfully returned.</span></span>|  
|<span data-ttu-id="3525a-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="3525a-113">E_FAIL</span></span>|<span data-ttu-id="3525a-114">不会返回内部帧的地址。</span><span class="sxs-lookup"><span data-stu-id="3525a-114">The address of the internal frame could not be returned.</span></span>|  
|<span data-ttu-id="3525a-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="3525a-115">E_INVALIDARG</span></span>|<span data-ttu-id="3525a-116">`pAddress` 为 `null`。</span><span class="sxs-lookup"><span data-stu-id="3525a-116">`pAddress` is `null`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3525a-117">备注</span><span class="sxs-lookup"><span data-stu-id="3525a-117">Remarks</span></span>  
 <span data-ttu-id="3525a-118">返回的值`pAddress`可以用于确定相对于堆栈上的其他框架的内部帧的位置。</span><span class="sxs-lookup"><span data-stu-id="3525a-118">The value returned in `pAddress` can be used to determine the location of the internal frame relative to other frames on the stack.</span></span> <span data-ttu-id="3525a-119">即使在基于 IA-64 的计算机，内部框架依赖堆栈仅，并且没有指向备份存储没有对应的指针。</span><span class="sxs-lookup"><span data-stu-id="3525a-119">Even on IA-64-based computers, the internal frame lives on the stack only, and there is no corresponding pointer to a backing store.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3525a-120">要求</span><span class="sxs-lookup"><span data-stu-id="3525a-120">Requirements</span></span>  
 <span data-ttu-id="3525a-121">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3525a-121">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3525a-122">**标头：** CorDebug.idl、 CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3525a-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3525a-123">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3525a-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3525a-124">**.NET framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3525a-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3525a-125">另请参阅</span><span class="sxs-lookup"><span data-stu-id="3525a-125">See Also</span></span>  
 [<span data-ttu-id="3525a-126">ICorDebugInternalFrame2 接口</span><span class="sxs-lookup"><span data-stu-id="3525a-126">ICorDebugInternalFrame2 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md)  
 [<span data-ttu-id="3525a-127">调试接口</span><span class="sxs-lookup"><span data-stu-id="3525a-127">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="3525a-128">调试</span><span class="sxs-lookup"><span data-stu-id="3525a-128">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)