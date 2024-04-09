---
title: Getting Started with HPE GreenLake API for Backup and Recovery
date: 2024-04-08T00:16:50.813Z
author: Ron Dharma
authorimage: /img/face-portraitlarge.jpg
thumbnailimage: /img/alletra-element-small.png
disable: false
---
## W﻿hat's new?

Recently, a new set of REST APIs for HPE GreenLake for Backup and Recovery Services was introduced in the HPE GreenLake Developer [website](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/). This blog presents some information on how to consume this set of APIs and introduce some useful tips about using this set of APIs. This set of APIs provides capability for manipulation of resources made available by HPE GreenLake for Backup and Recovery services. Consequently, any customer can use these APIs to protect their data in hybrid cloud, as well as anyone can do, using the user interface for HPE GreenLake for Backup and Recovery in the HPE GreenLake console.  This set of API provides user capabilities to perform any of Create, Read, Update and Delete (CRUD) operations against HPE GreenLake Backup and Recovery resources such as: *data-orchestrator, protection store gateway, StoreOnce, protection-stores, protection-policies, snapshots, backups, on-premises assets (VM, DataStore, MSSQL, Storage Volumes).* There will be more resources that are going to be added into this set of APIs in the future releases that will cover *cloud service providers, and cloud assets*. For more information on how to use this HPE GreenLake for Backup and Recovery service, please visit the [website ](https://www.hpe.com/us/en/hpe-greenlake-backup-recovery.html)and the getting started [guide](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=sd00003454en_us). 

The specification of this API is publicized as OpenAPI specification in JSON format, and the specification is available for download from this [section ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/guide/)of the documentation as shown below. The specification follows the OpenAPI standard 3.1, and it contains all required information so that this JSON file can be consumed by any OpenAPI tools to provide client library, server mock, or documentation as described in this [OpenAPI ](https://tools.openapis.org/)Initiative.

> ***NOTE:*** 
> There are two different sets of API spec that are downloadable from the documentation page of the Backup and Recovery in March 2024 release. The two sets represent the two versions of Backup and Recovery APIs that were made available for separate resources, namely **hypervisor-managers** and **rest of other resources** as shown in this picture below. To get into the page for downloading each of the OpenAPI specification file, please traverse the tree of guides on the left windows and select either page of the API versions.

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

*The above figure display resources that are parts of the hypervisor and on-premises components that can be protected.*

> ***NOTE:*** 
> In the current HPE Developer website, there is a single resource categorized as v1alpha1 that will be used to register, unregister, and update the hypervisor-manager. The current supported hypervisor is VMware vCenter, and it contains the cluster, virtual machines, and datastore used for the source of data-protection. The hypervisor-manager enabled HPE GreenLake Backup and Recovery to discover the vCenter which control the assets for data protection. This a crucial discovery will lead to application of protection-policy, setup the schedule, assign the protection-store where the copy protections will be allocated, and rest of the data protection operations.

### What about the components in HPE GreenLake Backup and Recovery that are not mentioned above?

There are other resources exist in the HPE GreenLake for Backup and Recovery that are not mentioned above; however, they are available in the user-interface for HPE GreenLake for Backup and Recovery. A couple of those resources are protection policy, and protection group. The protection group is used to consolidate multiple number of assets with a particular protection policy. On the other hand, the protection-policy is a resource to consolidate the schedule of protection-jobs and the flow of the recovery points at different tiers of protection-store. Together, both protection policy and protection group deliver the management of the Recovery Point Objective for data protection using HPE GreenLake for Backup and Recovery.

![Protection policy for vmware schedule](/img/protection-policy-ui-for-vmware-scheduling.png)

*The above figure display resources for schedule and the flow of the recovery-points part of the protection policy.*

Additionally, there is also a resource called a protection job that is not shown in the user-interface; however, it is required to perform the operation of data protection. You will need to manipulate protection jobs to create a protection or to recover an existing recovery point. Additionally, the protection-job is the resource that can be manipulated to suspend or to resume a protection schedule. 

![Protection jobs for scheduling and protection tiers](/img/protection-jobs-ui.png)

*The above figure displays the protection jobs which are the resources available after a protection policy applied to a protection group of many assets or a single asset.*

Beyond protection-jobs, there are recovery points (also known as copies). These are resources that used to represent a copy that is inside the protection store, and they are used to perform the recovery. Note that even though there are three different categories of recovery-points that are available in the protection policy, there are only two different resources. The first resource is called snapshots to represent copies that exist inside the storage array. The second resource is called backups to represent copies that exist inside the on-premises protection store such as Protection Store Gateway, and copies that exist inside the cloud protection store. The cloud protection store is repository that sits in the cloud public providers that are managed by HPE, and these can exist either in AWS or Azure. All of these recovery points exist in relation to the assets, where the recovery can be initiated using the HPE GreenLake API.

![Protection copies for hierarchy](/img/protection-copies.png)

## Using the Backup and Recovery APIs

This set of virtualization APIs uses the same authorization and permission as the rest of the family of HPE GreenLake API for data services. To ensure that all programmatic interaction with the HPE GreenLake platform services and resources is secure and authenticated, these APIs require an access token. The token is generated using the client ID and client Secret you acquired during the creation of the client API credentials. Documentation about getting started with the HPE GreenLake API is provided on the HPE Developer Community website, and on the HPE GreenLake Developer portal website. Nevertheless, there is also blog posts that describes how to use publicly available tools to manipulate this API without a programming language, such as Postman. An additional blog post that describes using Postman for this API is also available in this link. Moreover, there will be blog posts available that provide guidance on how to convert this OpenAPI specifications based on the OAS 3.1 to any scripting language library in the future.  Lastly, anyone can follow the examples provided by each API reference in the documentation page, such as the GET /backup-recovery/v1beta1/protection-jobs which is shown on the below figure. The documentation provides detail on the API syntax for a particular method, arguments used for the API, expected successful and failed responses, and several examples of creating the automation script using cURL, JavaScript, Python, and Go. The documentation page also provides the ability to execute the API directly on the documentation page as explained in the previous blog post (Getting started with HP GreenLake Data Services API).