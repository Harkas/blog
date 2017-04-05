---
layout: post
title:  "ArcGIS Engine VC++中对象实例化方法"
date:   2010-11-04
categories: ArcGIS Engine VC++
description: ArcGIS Engine在VC++中的应用之--实例化
---

这是小时候博客里的迁移，可以不看~~

```c++
1.在变量声明的同时直接使用CLSID进行构造
示例：

```c++
IPropertySetPtr ipPropertySet(CLSID_PropertySet);
ipPropertySet->SetProperty(CComBSTR(L"DATABASE"),CComVariant(path));
```

2.CoCreateInstance方法(ATL CComPtr 模板类成员 atlbase.h)
示例：

```c++
CComPtr<IWorkspaceFactory> ipWorkspaceFactory;
ipWorkspaceFactory.CoCreateInstance(CLSID_ShapefileWorkspaceFactory);
```

3.CreateInstance方法(COM interface pointer 模板类_com_ptr_t成员 comip.h)
示例：

```c++
IFeatureLayerPtr ipFeatureLayer;
HRESULT hr = ipFeatureLayer.CreateInstance(CLSID_FeatureLayer);
```

用下来感觉后两种方法比较灵活，可以在创建时再决定对象的具体类。我们可以将变量声明为抽象类或者接口，在实例化时再根据需要创建为特定的具体类。