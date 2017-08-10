---
title: "開發 Integration Services 自訂物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6bbb7ccd5d65caa4b5c8cc8f28383b8100e09cd6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="developing-custom-objects-for-integration-services"></a>開發 Integration Services 的自訂物件
  當控制流程和資料流程物件所含的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]未完全符合您的需求，您可以在您自己包括開發許多類型的自訂物件：  
  
-   **自訂工作**。  
  
-   **自訂連接管理員。** 連接到目前不支援的外部資料來源。  
  
-   **自訂記錄提供者。** 記錄封裝事件目前不支援的格式。  
  
-   **自訂列舉值。** 支援反覆運算一組的目前不支援的物件或值的格式。  
  
-   **自訂資料流程元件。** 可以設定為來源、 轉換或目的地。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型使用基底類別來協助此自訂開發，這些基底類別可為您的自訂實作提供一致且可靠的架構。  
  
 如果您不必在多個封裝之間重複使用自訂功能，指令碼工作與指令碼元件提供 Managed 程式語言的完整功能，可大幅減少要撰寫的基礎結構程式碼。 如需詳細資訊，請參閱[比較指令碼的方案和自訂物件](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)。  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>開發 Integration Services 自訂物件的步驟  
 當您開發要用於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的自訂物件時，所開發的類別庫 (DLL) 將在設計階段與執行階段由 SSIS 設計師及 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段載入。 您必須實作的最重要方法，不是從自己的程式碼呼叫的方法，而是執行階段在適當時間呼叫以初始化並驗證您的元件且叫用其功能的方法。  
  
 以下是開發自訂物件所遵循的步驟：  
  
1.  以您慣用的 Managed 程式語言建立「類別庫」類型的新專案。  
  
2.  繼承自適當的基底類別，如下表所示。  
  
3.  將適當的屬性套用至新類別，如下表所示。  
  
4.  視需要覆寫基底類別的方法，並為物件的自訂功能撰寫程式碼。  
  
5.  選擇性地為您的元件建立自訂使用者介面。 為了便於部署，您可能會想要以相同方案中的獨立專案開發使用者介面，並將它建立成個別的組件。  
  
6.  （選擇性） 中顯示範例和自訂物件說明內容的連結**SSIS 工具箱**。  
  
7.  建置、 部署和偵錯新自訂物件中所述[建置、 部署及偵錯自訂物件](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="base-classes-attributes-and-important-methods"></a>基底類別、屬性和重要的方法  
 這個資料表針對您可以開發的各種類型自訂物件，提供 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中最重要元素的便利參考。  
  
|自訂物件|基底類別|Attribute|重要的方法|  
|-------------------|----------------|---------------|-----------------------|  
|工作|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|[ODBC 目的地編輯器]|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|記錄提供者|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>、 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>、 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|列舉值|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|資料流程元件|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>、 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>、 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>提供範例和說明內容的連結  
 若要顯示中的連結**SSIS 工具箱**範例和以 managed 程式碼撰寫的自訂物件說明內容，請使用下列屬性。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 若要顯示範例和以機器碼撰寫之自訂物件說明內容的連結，請在 SamplesTag、HelpKeyword 和 HelpCollection 的登錄指令碼 (.rgs) 檔案中加入項目。 以下是一個範例。  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>提供自訂使用者介面  
 若要允許自訂物件的使用者設定其屬性，您可能也必須開發自訂使用者介面。 在並非絕對需要自訂使用者介面的情況下，您可以選擇建立一個介面以提供比預設編輯器更好用的介面。  
  
 在自訂使用者介面專案或是組件中，通常有兩個類別：針對特定類型的自訂物件之使用者介面實作 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 介面的類別，以及它所顯示的 Windows Form，以蒐集使用者資訊。 您實作的介面只有一些方法，而且自訂使用者介面並不難開發。  
  
> [!NOTE]  
>  許多[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]記錄提供者都有自訂使用者介面，實作<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>取代**組態**具有的篩選下拉式清單可用的連接管理員的文字方塊。 不過，在這個版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中並未實作自訂記錄提供者的自訂使用者介面。 指定 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 屬性值將沒有任何作用。  
  
 下表提供您在為每個類型的自訂物件開發自訂使用者介面時，必須實作的介面之便利參考。 它也會說明使用者看見或如果您選擇不在開發自訂使用者介面物件，如果您無法連結至其使用者介面的物件，使用**UITypeName**屬性中物件的屬性。 雖然強大的 [進階編輯器] 可能可以滿足資料流程元件，不過，[屬性] 視窗對於工作與連接管理員而言較缺乏使用者親和性，而且如果沒有自訂表單，根本無法設定自訂 ForEach 列舉值。  
  
|自訂物件|使用者介面的基底類別|沒有提供自訂使用者介面時的預設編輯行為|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|工作|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|僅 [屬性] 視窗|  
|[ODBC 目的地編輯器]|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|僅 [屬性] 視窗|  
|記錄提供者|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> (尚未在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中實作)|中的文字方塊**組態**資料行|  
|列舉值|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|僅 [屬性] 視窗。 編輯器的 [列舉值組態] 區域是空的。|  
|資料流程元件|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|進階編輯器|  
  
## <a name="external-resources"></a>外部資源  
  
-   部落格文章： [Visual Studio 方案建置流程因為 SSIS 參考而與.NET Framework 組件提供關於間接相依性的警告](http://go.microsoft.com/fwlink/?LinkId=215662)，blogs.msdn.com 上。  
  
## <a name="see-also"></a>另請參閱  
 [保存自訂物件](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [自訂物件的建立、部署和偵錯](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  