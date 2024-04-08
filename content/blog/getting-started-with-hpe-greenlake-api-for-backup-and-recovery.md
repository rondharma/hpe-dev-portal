---
title: Getting Started with HPE GreenLake API for Backup and Recovery
date: 2024-04-08T00:16:50.813Z
author: Ron Dharma
authorimage: /img/face-portraitlarge.jpg
thumbnailimage: /img/alletra-element-small.png
disable: false
---






# W﻿hat's new?

Recently, a new set of REST APIs for HPE GreenLake for Backup and Recovery Services was introduced in the HPE GreenLake Developer [website](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/). This blog presents some information on how to consume this set of APIs and introduce some useful tips about using this set of APIs. This set of APIs provides capability for manipulation of resources made available by HPE GreenLake for Backup and Recovery services. Consequently, any customer can use these APIs to protect their data in hybrid cloud, as well as anyone can do, using the user interface for HPE GreenLake for Backup and Recovery in the HPE GreenLake console.  This set of API provides user capabilities to perform any of Create, Read, Update and Delete (CRUD) operations against HPE GreenLake Backup and Recovery resources such as: *data-orchestrator, protection store gateway, StoreOnce, protection-stores, protection-policies, snapshots, backups, on-premises assets (VM, DataStore, MSSQL, Storage Volumes).* There will be more resources that are going to be added into this set of APIs in the future releases that will cover *cloud service providers, and cloud assets*. For more information on how to use this HPE GreenLake for Backup and Recovery service, please visit the [website ](https://www.hpe.com/us/en/hpe-greenlake-backup-recovery.html)and the getting started [guide](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=sd00003454en_us). 

The specification of this API is publicized as OpenAPI specification in JSON format, and the specification is available for download from this [section ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/guide/)of the documentation as shown below. The specification follows the OpenAPI standard 3.1, and it contains all required information so that this JSON file can be consumed by any OpenAPI tools to provide client library, server mock, or documentation as described in this [OpenAPI ](https://tools.openapis.org/)Initiative.

**Note:** There are two different sets of API spec that are downloadable from the documentation page of the Backup and Recovery in March 2024 release. The two sets represent the two versions of Backup and Recovery APIs that were made available for separate resources, namely **hypervisor-managers** and **rest of other resources** as shown in this picture below. To get into the page for downloading each of the OpenAPI specification file, please traverse the tree of guides on the left windows and select either page of the API versions. 

![](/img/backup-and-recovery-api-front-download-page.jpg "Front page for Backup & Recovery front page")

The Backup and Recovery API specification files contain information that describe the set of REST APIs for HPE GreenLake for Backup and Recovery such as the endpoints, authentication, syntax of parameters, expected response, and many other objects.

![](/img/backup-and-recovery-json-information.png)