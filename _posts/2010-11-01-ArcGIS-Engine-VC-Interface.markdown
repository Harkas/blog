---
layout: post
title:  "ArcGIS Engine VC++中几种接口的通用性"
date:   2010-11-01
categories: ArcGIS Engine VC++
description: ArcGIS Engine在VC++中的应用之--几种接口的通用性
---

这是小时候博客里的迁移，可以不看~~

ArcGIS Engine VC++中，几种接口的通用性，都可以得到想得到的对象，前提是一个地图中只有一个map对象时，并且只有一个GraphicsLayer图形图层：

```c++
IActiveViewPtr pActiveV = m_MapCtrl.get_ActiveView();
IMapPtr pMap = pActiveV->GetFocusMap();
IMapPtr pMapM = m_MapCtrl.get_Map();
```

pMap与 pMapM是指向同一对象的指针

```c++
ICompositeGraphicsLayerPtr pGraLayer = pMap->GetBasicGraphicsLayer();
ILayerPtr pLayer = pMap->GetActiveGraphicsLayer();
ICompositeGraphicsLayerPtr pGraLayer1 = pLayer;
```

pGraLayer 与pGraLayer1 是指向同一对象的指针

```c++
IGraphicsContainerPtr pGraCont = pActiveV->GetGraphicsContainer();
IGraphicsContainerPtr pGraCont1 = pMap;
```

pGraCont 与pGraCont1 是指向同一对象的指针
