---
weight: 40
title: Subscribing applications
layout: redirect
---

The application concept of Cumulocity includes a basic application marketplace. 

Tenants can be subscribed to applications which have been deployed by their super tenant (management tenant or enterprise edition tenant). 

Granting access to subtenants and subscribing to applications is done in the Administration application. 

![Application Subscription](/guides/images/concepts-guide/applicationsubscription.png)

Tenants can also have their own application marketplace, which can be viewed in the "Own Applications" page in the Administration application.

<img src="/guides/images/users-guide/Administration/Admin_OwnApplications.png" alt="Own applications" style="max-width: 100%">

Owned applications and granted applications can also be subscribed to the subtenants by the tenant.

For details refer to [Managing tenants](/guides/users-guide/administration#tenants) in the User guide.

### Service Discovery

A tenant can have multiple available applications but to use an application's functionality a subscription to the application must be established for the tenant. As an example, when a custom decoder microservice is available in the tenant's marketplace, it is not enabled to be used until the tenant subscribes for the microservice application.

To see the list of subscribed applications for the tenant, Cumulocity Rest API can be used to get [specific tenant information](/guides/reference/tenants/#tenant). Those applications will be listed under the "applications" fragment.