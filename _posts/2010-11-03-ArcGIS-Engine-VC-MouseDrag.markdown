---
layout: post
title:  "ArcGIS Engine VC++中选中鼠标单击处的元素并移动"
date:   2010-11-03
categories: ArcGIS Engine VC++
description: ArcGIS Engine在VC++中的应用之--鼠标拖拽
---

这是小时候博客里的迁移，可以不看~~

```c++
IPointPtr pPnt(CLSID_Point);
pPnt->PutCoords(mapX,mapY);

IEnumElementPtr pEnumEle;
IElementPtr pElement;
IActiveViewPtr pActiveV = m_MapCtrl.get_ActiveView();
IGraphicsContainerPtr pGraCont = NULL;
pActiveV->get_GraphicsContainer(&pGraCont);
IGraphicsContainerSelectPtr pGraConSel = (IGraphicsContainerSelectPtr)pGraCont;


pEnumEle = pGraCont->LocateElements(pPnt,10); //选中单击点10范围内的元素
if(pEnumEle != NULL)
{
    IScreenDisplayPtr pScreemDis(CLSID_ScreenDisplay);
    pActiveV->get_ScreenDisplay(&pScreemDis);
    IDisplayFeedbackPtr pDisFeedBack(CLSID_MovePointFeedback);
    pDisFeedBack->putref_Display(pScreemDis);
    IMovePointFeedbackPtr pMPDisFeedBack = (IDisplayFeedbackPtr)pDisFeedBack;

    pElement = pEnumEle->Next();
    if(pElement != NULL)
    {
        IGeometryPtr pGeometry = NULL;
        pElement->get_Geometry(&pGeometry);
        pMPDisFeedBack->Start((IPointPtr)pGeometry,pPnt);
        IPointPtr pMPnt(CLSID_Point);
        pMPnt->PutCoords(mapX+10,mapY+10);
        pDisFeedBack->MoveTo(pMPnt);
        IPointPtr pPntResult = NULL;
        pMPDisFeedBack->Stop(&pPntResult);
        pElement->put_Geometry(pMPnt);
        pGraCont->UpdateElement(pElement);
        pElement = pEnumEle->Next(); //得到元素枚举中的下一个元素
    }
    pActiveV->PartialRefresh(esriViewGraphics,NULL,NULL);
 }
```

GraphicsContainerSelect是用来控制Graphics Container中选择的元素。以下是它的几个主要方法：
UnselectAllElements：不选中任何元素;
SelectAllElements：选中所有元素；
SelectElement：选中指定的元素；
Get_SelectedElements才是得到所选中元素的集合.

IGraphicsContainer是用来控制Graphics Container中所有元素。在本例中主要用到它以下两个方法：
LocateElements：根据点和偏差值选择元素；
LocateElementsByEnvelope：根据范围选择元素.

