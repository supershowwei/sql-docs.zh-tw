---
title: "Binding 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Binding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d252931193ef06109c1d353ddc8fa42b3e4b6dfb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="binding-data-type-assl"></a>Binding 資料類型 (ASSL)
  定義代表兩個物件之間相依關聯性的抽象基本資料類型，其中某個物件的資料或中繼資料相依於繫結物件的資料或中繼資料。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)， [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)， [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)， [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)， [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md)， [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Binding>。  
  
 如需資料繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Binding 類型的元素  
 下表列出類型的項目**繫結**。  
  
|父元素|類型的項目**繫結**|註解|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)的[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) (型別[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|輸入的**繫結**必須[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding （行的外）](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[量值群組](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|輸入的**繫結**必須[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**繫結**可以是任何型別|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)，或[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[資料行](../../../analysis-services/scripting/objects/column-element-assl.md)|輸入的**繫結**必須[CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)或[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)(型別[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|輸入的**繫結**必須[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)，或[RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[量值群組](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)的[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) (型別[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|輸入的**繫結**必須[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)，或[InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|輸入的**繫結**必須[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|輸入的**繫結**必須[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|輸入的**繫結**必須[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)，或[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|輸入的**繫結**必須[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [CubeAttributeBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)，或[MeasureBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|輸入的**繫結**必須[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  