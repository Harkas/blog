---
layout: post
title:  "ArcGIS Engine VC++中 IActiveView刷新方式"
date:   2010-11-02
categories: ArcGIS Engine VC++
description: ArcGIS Engine在VC++中的应用之--IActiveView刷新方式
---

这是小时候博客里的迁移，可以不看~~

IActiveView接口定义了Map对象的数据显示功能。使用该接口可以改变视图的范围，刷新视图

IActiveView的PartialRefresh(esriViewGeography, pLayer, null)用于刷新指定图层

IActiveView的PartialRefresh(esriViewGeography, null, null) 用于刷新刷新所有图层

IActiveView的PartialRefresh(esriViewGeoSelection, null, null) 用于刷新所选择的对象

IActiveView的PartialRefresh(esriViewGraphics, null, null) 用于刷新所有图形元素

IActiveView的PartialRefresh(esriViewGraphics, pElement, null) 用于刷新指定图形元素

IActiveView的PartialRefresh(esriViewGraphicSelection, null, null)用于刷新所选择的图元
