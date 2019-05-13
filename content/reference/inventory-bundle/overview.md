---
weight: 5
title: Overview
layout: redirect
---

The inventory interface consists of the following parts:

-   The *inventory API* resource returns URIs and URI templates to collections of managed objects, so that all objects, all objects of a particular type and all objects with particular capabilities can be queried.
-   The *managed object collection* resource retrieves sets of managed objects and enables creating new managed objects.
-   The *managed object* resource represents individual managed objects that can be queried and deleted.
-   The *managed object reference collection* resource retrieves sets of references to managed objects. These could be, for example, child devices of a particular managed object. It also enables adding new references to a collection (e.g., adding a new child device).
-   The *managed object reference* resource represents one individual reference to a managed object, which can be retrieved or deleted.

> Note that for all PUT/POST requests accept header should be provided, otherwise an empty response body will be returned.