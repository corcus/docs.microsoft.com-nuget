---
# required metadata 

title: Overview | NuGet V3 API | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/28/2017
ms.topic: reference
ms.prod: nuget
#ms.service:
ms.technology: null

ms.assetid: 8c81f1ac-18c7-44d1-b2e3-584fe85dee6f

# optional metadata

description: The NuGet V3 API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, etc.
#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
- jver 
- karann
- unnir
#ms.suite:
#ms.tgt_pltfrm:
#ms.custom:
---

# NuGet V3 API

The NuGet V3 API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages,
and perform most other operations available in the official NuGet clients.

This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as
[`dotnet restore`](https://docs.microsoft.com/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../../Tools/nuget-exe-CLI-Reference.md#push).

## Service Index

The entry point for the V3 API is a JSON document in a well known location. This document is called the **service index**.
The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`/

This JSON document contains a list of *resources* which provide different functionality and fulfill different
use cases.

Clients that support the V3 API should accept one or more of these service index URL as the means of connecting to the
respective V3-enabled package sources.

For more information about the service index, see [Service Index](service-index.md).

## Versioning

The API is version 3 of NuGet's HTTP protocol. This protocol is generally referred to as "the V3 API".

The service index schema version is indicated by the `version` property in the service index.

```json
{
    "version": "3.0.0-beta.1"
    ...
}
```

The V3 API mandates that the version string has a major version number of `3`. As non-breaking changes are made to the
service index schema, the version string's minor version will be incremented.

Each resource in the service index is versioned independently from the service index schema version.

Older clients (such as nuget.exe 2.x) do not support the V3 API and support the older V2 API, which is not documented
here.

## Resources and schema

The service index describes a variety of resources. The current set of supported resources are as follows:

Resource name | Description
--- | ---
[`PackagePublish` resource](package-publish-resource.md) | Push and unlist packages.
[`SearchQueryService` resource](search-query-service-resource.md) | Filter and search for packages by keyword.
[`SearchAutocompleteService` resource](search-autocomplete-service-resource.md) | Discovery package IDs and versions by substring.
[`RegistrationsBaseUrl` resource](registration-base-url-resource.md) | Get package metadata.
[`PackageBaseAddress` resource](package-base-address-resource.md) | Get package content (.nupkg).

In general, all non-binary data returned by a V3 API resource will be JSON. The response schema returned by each resource in the service index is defined individually for that resource. For more information about each resource, see the resource topics noted above.

## Timestamps

All timestamps returned by the V3 API are UTC or are otherwise specified using ISO 8601 representation. 

## HTTP Verbs

Verb   | Use
------ | -----------
GET    | Performs a read-only operation, typically retrieving data.
PUT    | Creates a resource that doesn't exist or, if it does exist, updates it.
DELETE | Deletes or unlists a resource.

## HTTP Status Codes

Code | Description
---- | -----
200  | Success, and there is a response body.
201  | Success, and the resource was created.
202  | Success, the request has been accepted but some work may still be incomplete and completed asynchronously.
204  | Success, but there is no response body.
400  | The parameters in the URL or in the request body aren't valid.
401  | The provided credentials are invalid.
403  | The action is not allowed given the provided credentials.
404  | The requested resource doesn't exist.
409  | The request conflicts with an existing resource.

## Authentication

Authentication is left up to the package source implementation to define. For nuget.org, only the `PackagePublish`
resource requires authentication. See [PackagePublish resource](packagepublish-resource.md) for details.
