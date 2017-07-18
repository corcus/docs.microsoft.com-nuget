---
# required metadata 

title: NuGet API Introduction | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/18/2017
ms.topic: article
ms.prod: nuget
#ms.service:
ms.technology: null

ms.assetid: 100606fd-0a03-4274-8ebf-7d778f73869c

# optional metadata

description: "There are a variety of ways to interact with NuGet programmatically: fetching package information and extending authentication with package sources"
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

# NuGet API Introduction

There are a variety of ways to interact with NuGet programmatically.

## Consuming and publishing packages

To interact with packages available on NuGet.org and other V3-enabled NuGet package sources such as MyGet and Visual
Studio Team Services package management, you can either:

1. Use the <a href="v3/overview.md">HTTP-based V3 API</a> and write your own client code.
1. Use the <a href="nuget-client-sdk.md">NuGet client SDK</a>, a set of .NET libraries used by the official NuGet clients.

## Extending authentication

NuGet supports extensions on how users authenticate with packages sources via **credential providers**. There are two
forms of credential providers each used by a different client experience.

1. <a href="NuGet-Credential-Providers-for-Visual-Studio.md">Credential providers for Visual Studio</a>.
1. <a href="nuget-exe-Credential-Providers.md">Credential providers for nuget.exe</a>.
