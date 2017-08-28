---
# required metadata 

title: Service Index reference, NuGet V3 API | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/18/2017
ms.topic: reference
ms.prod: nuget
#ms.service:
ms.technology: null

ms.assetid: 2f6d6cf2-53fb-417a-b1d8-e0ac591c1699

# optional metadata

description: The V3 service index is the entry point of the NuGet V3 and enumerates the capabilities of the V3 server.
#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
- karann
- unnir
#ms.suite:
#ms.tgt_pltfrm:
#ms.custom:
---

# Service index reference

The V3 service index for nuget.org looks something like is this:

[!code-REST [service-index.json](./_data/service-index.json)]

The `"resources"` property contains an array of services supported by this package source.

### Resource

A resource is an entry in the service index. A resource has two significant properties.
