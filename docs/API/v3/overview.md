---
# required metadata 

title: Overview | NuGet V3 API | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/18/2017
ms.topic: article
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
`dotnet restore`, search in the Visual Studio UI, and `nuget.exe push`.

## Entry Point

The entry point for the V3 API is a JSON document in a well known location. This document is called the **service index**.
For NuGet.org, the location of the service index is here:

```
https://api.nuget.org/v3/index.json
```

This JSON document contains a list of *resources* which provide different functionality and fulfill different
use cases.

Clients that support the V3 API should accept one or more of these service index URL as the means of connecting to the
respective V3-enabled package sources.

For more information about the service index, see the [respective documentation](service-index.md).

## Versioning

The API itself is version 3 of NuGet's HTTP protocol. This protocol is generally referred to as "the V3 API".

The service index schema version is indicated as a JSON property in the document.

```
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

## Schema

The service index is a JSON document. For more information about the service index schema, see the
[respective documentation](service-index.md).

In general, all non-binary data returned by a V3 API resource will be JSON.

The schema of the responses returned by each resource mentioned in the service index is defined individually for that
resource. For more information about each resource, see the respective documentation.

## Resources

The service index mentions a variety of resources. Today, the set of supported resources are:

1. [`PackagePublish` resource](publishing.md) - push and unlist packages
1. [`SearchQueryService` resource](search.md) - filter and search for packages by keyword
1. [`SearchAutocompleteService` resource](autocomplete.md) - discovery package IDs and versions by substring
1. [`RegistrationsBaseUrl` resource](package-metadata.md) - get metadata about packages
1. [`PackageBaseAddress` resource](package-base-address.md) - get package content (.nupkg)

## HTTP Verbs

Verb   | Used for...
------ | -----------
GET    | Perform a read-only operation, typically getting data
PUT    | Create a resource that doesn't exist or, if it does exist, update it
DELETE | Delete or unlist a resource.

## HTTP Status Codes

Code | Notes
---- | -----
200  | Success, and there is a response body
201  | Success, and the resource was created
202  | Success, the request has been accepted but some work may still be incomplete and completed asynchronously
204  | Success, but there is no response body
400  | The parameters in the URL or in the request body aren't valid
401  | The provided credentials are invalid
403  | The action is not allowed given the provided credentials
404  | The requested resource doesn't exist
409  | The request conflicts with an existing resource

## Authentication

Authentication is left up to the package source implementation to define. For NuGet.org, all but the `PackagePublish`
resource require no authentication at all.

For more information on the `PackagePublish` resource, see the [documentation about publishing](publishing.md).

## Timezones

All timestamps returned by the V3 API are UTC or are otherwise specified using ISO 8601 representation. 
