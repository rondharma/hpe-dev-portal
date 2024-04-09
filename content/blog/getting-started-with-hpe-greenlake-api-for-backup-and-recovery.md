---
title: Getting Started with HPE GreenLake API for Backup and Recovery
date: 2024-04-08T00:16:50.813Z
author: Ron Dharma
authorimage: /img/face-portraitlarge.jpg
thumbnailimage: /img/alletra-element-small.png
disable: false
---
![]()

![]()

## W﻿hat's new?

Recently, a new set of REST APIs for HPE GreenLake for Backup and Recovery Services was introduced in the HPE GreenLake Developer [website](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/). This blog presents some information on how to consume this set of APIs and introduce some useful tips about using this set of APIs. This set of APIs provides capability for manipulation of resources made available by HPE GreenLake for Backup and Recovery services. Consequently, any customer can use these APIs to protect their data in hybrid cloud, as well as anyone can do, using the user interface for HPE GreenLake for Backup and Recovery in the HPE GreenLake console.  This set of API provides user capabilities to perform any of Create, Read, Update and Delete (CRUD) operations against HPE GreenLake Backup and Recovery resources such as: *data-orchestrator, protection store gateway, StoreOnce, protection-stores, protection-policies, snapshots, backups, on-premises assets (VM, DataStore, MSSQL, Storage Volumes).* There will be more resources that are going to be added into this set of APIs in the future releases that will cover *cloud service providers, and cloud assets*. For more information on how to use this HPE GreenLake for Backup and Recovery service, please visit the [website ](https://www.hpe.com/us/en/hpe-greenlake-backup-recovery.html)and the getting started [guide](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=sd00003454en_us). 

The specification of this API is publicized as OpenAPI specification in JSON format, and the specification is available for download from this [section ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/guide/)of the documentation as shown below. The specification follows the OpenAPI standard 3.1, and it contains all required information so that this JSON file can be consumed by any OpenAPI tools to provide client library, server mock, or documentation as described in this [OpenAPI ](https://tools.openapis.org/)Initiative.

**Note:** There are two different sets of API spec that are downloadable from the documentation page of the Backup and Recovery in March 2024 release. The two sets represent the two versions of Backup and Recovery APIs that were made available for separate resources, namely **hypervisor-managers** and **rest of other resources** as shown in this picture below. To get into the page for downloading each of the OpenAPI specification file, please traverse the tree of guides on the left windows and select either page of the API versions. 

![GLBR API documentation website](/img/backup-and-recovery-api-front-download-page.jpg "Front page for Backup & Recovery front page")

The Backup and Recovery API specification files contain information that describe the set of REST APIs for HPE GreenLake for Backup and Recovery such as the endpoints, authentication, syntax of parameters, expected response, and many other objects.

![GLBR openapi spec](/img/backup-and-recovery-json-information.png "JSON open API spec example")

*The above figure shows the example of the downloaded backup-and-recovery v1beta1.json file from the Backup and Recovery API documentation [guide](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/guide/).*

## API Versioning

This set of APIs is released with two different specifications which are identified as revision v1alpha1 and v1beta1 at the time of introduction in March 2024. Moving forward, the API will be updated to next revision toward the long-term release version. As each individual API is updated, there will also be more capabilities added to any of the resources identified under this set of APIs.  For information about update stages, and deprecation, please follow the HPE GreenLake Developer Portal Versioning [guide](https://developer.greenlake.hpe.com/docs/greenlake/guides/public/standards/versioning_basics/). You can expect that the API categorized as v1alpha1 will be updated within a short time; hence, I recommend for monitoring any announcement of the next revision of APIs for Backup and Recovery in this documentation [guide](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/guide/). 

**Note:** At the time of release of March 2024, all of resources for HPE GreenLake API for Backup and Recovery are limited to data protection of on-premises assets. The manipulation of the cloud assets will be made available in the next release.

The below diagram displays those components in the first part of the GreenLake API for Backup and Recovery. This first part of components consists of the resources that are considered as the infrastructure for HPE GreenLake for Backup and Recovery on-premises and at the cloud. These components must be deployed prior to operation of the HPE GreenLake for Backup and Recovery. The on-premises components consist of Protection Store Gateway VM or HPE StoreOnce (purpose built backup appliance). Additionally, the cloud components consist of the data services instance deployed at HPE GreenLake workspace, and the cloud protection store to contain the cloud recovery points (backups).  The information on getting started with HPE GreenLake for Backup and Recovery is available in the support [website](https://support.hpe.com/hpesc/public/docDisplay?docId=sd00003102en_us&page=bar_overview_dscc.html)

1. Data-Orchestrator.
2. Protection-Store-Gateway.
3. StoreOnce.
4. Protection-Stores.

![GLBR architecture 1](/img/glbr-architecture-overview-1.png)

*The above figure shows the resources that are part of the infrastructure to accommodate the data protection for HPE GreenLake for Backup and Recovery.*

The second part of the GreenLake API for Backup Recovery resources is the resources from which HPE GreenLake for Backup and Recovery provides protection for data loss. In below diagram, you will see those assets which contains the components that need to be protected and the components which the assets are allocated at. Those components, such as virtual machine, datastore, or SQL database application, storage volumes, or physical hosts, are the assets that need to be protected. Nevertheless, other assets in this category include the components for the hypervisor, compute servers, storage array, networking, and the VMware vCenter that manage the hypervisor components. This HPE GreenLake API must maintain the inventory of all the assets that are protected by querying the vCenter.

![GLBR architecture 2](/img/glbr-architecture-overview-2.png)