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

![GLBR architecture 1](/img/glbr-architecture-overview-1.png)

*The above figure shows the resources that are part of the infrastructure to accommodate the data protection for HPE GreenLake for Backup and Recovery.*

The second part of the GreenLake API for Backup Recovery resources is the resources from which HPE GreenLake for Backup and Recovery provides protection for data loss. In below diagram, you will see those assets which contains the components that need to be protected and the components which the assets are allocated at. Those components, such as virtual machine, datastore, or SQL database application, storage volumes, or physical hosts, are the assets that need to be protected. Nevertheless, other assets in this category include the components for the hypervisor, compute servers, storage array, networking, and the VMware vCenter that manage the hypervisor components. This HPE GreenLake API must maintain the inventory of all the assets that are protected by querying the vCenter.

![GLBR architecture 2](/img/glbr-architecture-overview-2.png)

*The above figure display resources that are parts of the hypervisor and on-premises components that can be protected.*

> ***NOTE:*** 
> In the current HPE Developer website, there is a single resource categorized as v1alpha1 that will be used to register, unregister, and update the hypervisor-manager. The current supported hypervisor-manager is VMware vCenter, and it contains the cluster, virtual machines, and datastore used for the source of data-protection. The hypervisor-manager enabled HPE GreenLake Backup and Recovery to discover the vCenter which control the assets for data protection. This a crucial discovery will lead to application of protection-policy, setup the schedule, assign the protection-store where the copy protections will be allocated, and rest of the data protection operations. 

### What about the components in HPE GreenLake Backup and Recovery that are not mentioned above?

There are other resources exist in the HPE GreenLake for Backup and Recovery that are not mentioned above; however, they are available in the user-interface for HPE GreenLake for Backup and Recovery. A couple of those resources are protection policy, and protection group. The protection group is used to consolidate multiple number of assets with a particular protection policy. On the other hand, the protection-policy is a resource to consolidate the schedule of protection-jobs and the flow of the recovery points at different tiers of protection-store. Together, both protection policy and protection group deliver the management of the Recovery Point Objective for data protection using HPE GreenLake for Backup and Recovery.

![Protection policy for vmware schedule](/img/protection-policy-ui-for-vmware-scheduling.png)

*The above figure display resources for schedule and the flow of the recovery-points part of the protection policy.*

Additionally, there is also a resource called a protection job that is not shown in the user-interface; however, it is required to perform the operation of data protection. You will need to manipulate protection jobs to create a protection or to recover an existing recovery point. Additionally, the protection-job is the resource that can be manipulated to suspend or to resume a protection schedule. 

![Protection jobs for scheduling and protection tiers](/img/protection-jobs-ui.png)

*The above figure displays the representation of protection jobs which are the resources available after a protection policy applied to a protection group of many assets or a single asset.*

Beyond protection-jobs, there are recovery points (also known as copies). These are resources that used to represent a copy that is inside the protection store, and they are used to perform the recovery. Note that even though there are three different categories of recovery-points that are available in the protection policy, there are only two different resources. The first resource is called snapshots to represent copies that exist inside the storage array. The second resource is called backups to represent copies that exist inside the on-premises protection store such as Protection Store Gateway, and copies that exist inside the cloud protection store. The cloud protection store is repository that sits in the cloud public providers that are managed by HPE, and these can exist either in AWS or Azure. All of these recovery points exist in relation to the assets, where the recovery can be initiated using the HPE GreenLake API.

![Protection copies for hierarchy](/img/protection-copies.png)

## Using the Backup and Recovery APIs

This set of virtualization APIs uses the same authorization and permission as the rest of the family of HPE GreenLake API for data services. To ensure that all programmatic interaction with the HPE GreenLake platform services and resources is secure and authenticated, these APIs require an access token. The token is generated using the client ID and client Secret you acquired during the creation of the client API credentials. Documentation about getting started with the HPE GreenLake API is provided on the HPE Developer Community [website](https://developer.hpe.com/blog/oauth2-for-hpe-greenlake-data-services-cloud-console/), and on the HPE GreenLake Developer portal [website](https://developer.greenlake.hpe.com/docs/greenlake/services/). Nevertheless, there is also blog [post](https://developer.hpe.com/blog/learn-what-you-can-do-with-hpe-data-services-cloud-console-api-in-just-3-minutes/)that describes how to use publicly available tool to manipulate this API without a programming language, such as Postman. An additional blog post that describes using Postman for this API is also available in this [link](https://developer.hpe.com/blog/oauth2-for-hpe-greenlake-data-services-cloud-console/). Moreover, there will be blog posts available that provide guidance on how to convert this OpenAPI specifications based on the OAS 3.1 to any scripting language library in the future.  Lastly, anyone can follow the examples provided by each API reference in the documentation page, such as the GET /backup-recovery/v1beta1/protection-jobs which is shown on the below figure. The documentation provides detail on the API syntax for a particular method, arguments used for the API, expected successful and failed responses, and several examples of creating the automation script using cURL, JavaScript, Python, and Go. The documentation page also provides the ability to execute the API directly on the documentation page as explained in the previous blog [post ](https://developer.hpe.com/blog/getting-started-with-hpe-greenlake-api-for-data-services/)(Getting started with HP GreenLake Data Services API).

![HPE GLBR API documentation ](/img/reference-document-for-hpe-glbr.png)

*The above figure shows the three-pane of the interactive API reference documentation for one of HPE GreenLake API for Backup and Recovery.*

## Some Tips and Examples

The interactive API reference documentation guide provides information about the parameters and request payload (body) key-pair values required for every available HPE GreenLake API for Backup and Recovery. Additionally, I am presenting some use cases with detail information on providing the correct parameters or building the correct request payload (body) key-pairs JSON structure required to achieve the use case.

> ***NOTE:*** 
> The below examples assumed that HPE GreenLake Backup and Recovery had been deployed, it was connected to an HPE array onboarded to HPE GreenLake, a VMware vCenter had been discovered, some virtual machines had been deployed and onboarded into HPE GreenLake Backup and Recovery. For more information on getting started with HPE GreenLake Backup and Recovery, please visit Getting Started guide on HPE support [website](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=sd00003454en_us&page=GUID-F25ABD00-C36B-42D8-A443-82584EE8E35A.html).

### Creating a cloud protection store

A protection store is the critical resource that is required to store the recovery points on-premises and in the cloud. The cloud protection stores are created on top of either the Protection Store Gateway or HPE StoreOnce because they are providing the connectivity to the cloud protection-store. To perform this use case, we will need to discover the StoreOnce and the storage location of the cloud protection store. As you can see now, we will be using the HPE GreenLake API for the data-services to discover the storage location of the cloud protection store. This example below displays the creation of the cloud protection store at HPE GreenLake protection store in Azure cloud storage.

![UI to create cloud protection in Azure](/img/ui-to-create-cloud-protection.png)

*T﻿he figure above shows the user interface used to create a cloud store protection at Azure in eastus2 storage location using the user interface.*

The list of the steps to perform this use case using GreenLake API

1. Use the [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/StoreOncesList/)to discover the StoreOnce instance that can connect to the cloud protection store and select the id which will be used as the value for storageSystemId as shown in below JSON request body.

![Discover deployed StoreOnce to create cloud protection store](/img/api-discover-storeonce.png)

2. Discover the cloud storage in the correct location from the list of the available storage location and copy the **storageLocationId** as shown in below JSON request body. The REST [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/data-services/public/openapi/data-services-public-v1beta1/operation/ListLocations/)that I used is **GET /data-services/v1beta1/storage-locations** part of HPE GreenLake data services API which is another set of APIs from the data services family of REST API. Note from the below figure that I used ***filter “backup-and-recovery” in capabilities*** to capture selected storage locations with the correct capability. The below figure shows information about the location (region) where the data will be stored; conversely, it’s located at “**Richmond**”, cloud service provide was “**AZURE**”, and cloud services provider identification is “**eastus2**”. 

![API to figure out the Azure storage location](/img/figure-out-storage-location.png)

3. Compose the cloud protection store at that location which is connected through the StoreOnce using POST /backup-recovery/v1beta1/protection-stores. For this [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/ProtectionStoreCreate/)execution, I provided a JSON body structure for the request **POST /backup-recovery/v1beta1/protection-stores** that contains the key-pair values from the previous API response. The below figure shows how to construct that JSON body in order to compose the cloud protection store that is connected to the HPE StoreOnce. The complete information about this JSON body structures is provided on the interactive [documentation ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/ProtectionStoreCreate/)of POST /backup-recovery/v1beta1/protection-stores. 

![API composing the protection store](/img/api-compose-protection-store.png)

4. After roughly about 5 minutes, the cloud protection store was completely created based on response of the following GET ../async-operations API as shown in the below figure. Note that I used a set of filtering parameters in the below figure to summarize the information from this task information: **GET /data-services/v1beta1/async-operations/{taskId}/select=associatedResources,createdAt,displayName,customerId,logMessages,progressPercent,state**.  I copied the task’s id from the response header’s location value of the prior API execution (POST ../protection-stores) into a Postman’s variable called taskId, and incorporated taskId variable to the async-operations.

![Task completion on POST protectoin-stores](/img/api-async-on-post-protection-stores.png)

For reference, I went into the Protection Stores menu as shown in the below figure to show that HPE GreenLake Backup and Recovery confirmed that the desired protection store was available.

![Validating cloud protection store has been created](/img/ui-validated-cloud-protection-store-completed.png)

### Creating a Protection-Policy

One of the common use-case that every user of HPE GreenLake Backup and Recovery will deploy is the creation of a protection-policy. This resource is important because it sets up the schedule for creation of recovery point; additionally, it sets up the flow of a recovery point from a primary storage to a storage snapshot, to on-premises protection-store and eventually to the cloud protection-store. 
Protection policies contain several different components:

1. A Schedule that contains the frequency for creation of the copy and time to retain the copies.
2. Protection store where the copies are stored: snapshot (in the primary array), on-premises store, and cloud store.
3. Length of time when the copy is being locked to satisfy immutability.
4. The prescript information prior to the creation of the copy.
5. The postscript information after the creation of the copy. 

To simplify this example, I created a three-tier protection-policy for VMware as depicted by this snippet from the protection policy’s menu.

![3 Tiers protection policy ](/img/backup-protection-policy-with-3-tiers.png)

The list of the steps to create this protection policy:

1. From the figure below, inside the protection store gateways menu, I discovered the serial number of the protection-store gateway as the filtering parameter to obtain the protection store gateway instance. 

![PSG UI](/img/psg-ui-to-show-the-serial-no.png)

2. Afterward, I used **GET /backup-recovery/v1beta1/protection-store-gateways** [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/ProtectionStoreGatewaysList/)to figure out the **protection-store-gateway id** that was associated with the protection-stores that would be incorporated into the protection-policy.

![API show registered PSG](/img/api-display-registered-psg.png)

3. From the figure below, I used **GET /backup-recovery/v1beta1/protection-stores** [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/ProtectionStoreList/)to obtain the protection-store id for both the on-premises protection store and the cloud protection store. To display related protection-stores to the protection storage gateway id, I provided the API parameter of filter to list the protection-store associated with the id for protection storage gateway of **“<onprem-protection-store-id>”**.  The filter parameter that I used are **protectionStoreType eq 'ON_PREMISES'** and **storageSystemInfo/id eq '<protection-store-gateway-id>'**. Additionally, I used the following parameter **select: name,displayName,id,status,state,protectionStoreType** to provide shorter response to simplify the discovery of the protection-store on-premises.

![API to obtain the onpremises protection store id](/img/api-to-get-onpremises-protection-store-id.png)

4. I repeat the same execution of the **GET /backup-recovery/v1beta1/protection-stores** to obtain the **“<cloud-protection-store-id>”**. To accomplish that, I used the following **filter**: **protectionStoreType eq 'CLOUD' and storageSystemInfo/id eq “<protection-store-gateway-id>”**.  Additionally, I also used the  parameter **select: name,displayName,id,status,state,protectionStoreType** to provide shorter response for simpler discovery of the protection-store-id in the cloud.

![API to obtain cloud protection store id](/img/api-discover-cloud-protection-store-id.png)

5. For the next step, I created a request body JSON structure that represents the protection policy schedule and each of the protection stores. Inside this JSON structures for request body, I defined the three objects that represent the SNAPSHOT, BACKUP (on-premises), CLOUD_BACKUP. Note that this structure can be expanded or contracted depending on the required backup strategy. The SNAPSHOT object did not require **<protection-store-Id>** as that recovery points will exist inside the primary storage array. This request JSON body structure was required to create the protection policy using HPE GreenLake [API ](https://developer.greenlake.hpe.com/docs/greenlake/services/backup-recovery/public/openapi/backup-recovery-public-v1beta1/operation/ProtectionStoreCreate/)POST /backup-recovery/v1beta1/protection-policies. 

   >  ***NOTE:*** I didn’t include objects for immutability, prescript, and postscript into the JSON structure. If it’s not intended, you don’t need to include unused key-pair values into the JSON structure. Additionally, the SNAPSHOT object does no require a **protectionStoreId**. 

   The below figure shows JSON structure for request body of **POST /backup-recovery/v1beta1/protection-policies** for the creation of protection-policy as intended.

```json
{
  "name": "VMware create three tiers",
  "description": "Snapshot-local-cloud",
  "protections": [
    {
      "type": "SNAPSHOT",
      "schedules": [
        {
          "scheduleId": 1,
          "name": "Array_Snapshot_1",
          "namePattern": {
            "format": "Array_Snapshot_{DateFormat}"
          },
          "expireAfter": {
            "unit": "DAYS",
            "value": 1
          },
          "schedule": {
            "recurrence": "HOURLY",
            "repeatInterval": {
              "every": 4
            },
            "activeTime": {
              "activeFromTime": "00:00",
              "activeUntilTime": "23:59"
            }
          }
        }
      ]
    },
    {
      "type": "BACKUP",
      "protectionStoreId": "<onprem-protection-store-id>",
      "schedules": [
        {
          "scheduleId": 2,
          "name": "On-Premises_Protection_Store_2",
          "sourceProtectionScheduleId": 1,
          "namePattern": {
            "format": "On-Premises_Protection_Store_{DateFormat}"
          },
          "expireAfter": {
            "unit": "DAYS",
            "value": 3
          },
          "schedule": {
            "recurrence": "DAILY",
            "repeatInterval": {
              "every": 1
            },
            "startTime": "00:00"
          }
        }
      ]
    },
    {
      "type": "CLOUD_BACKUP",
      "protectionStoreId": "<cloud-protection-store-id>",
      "schedules": [
        {
          "scheduleId": 3,
          "name": "HPE_Cloud_Protection_Store_3",
          "sourceProtectionScheduleId": 2,
          "namePattern": {
            "format": "HPE_Cloud_Protection_Store_{DateFormat}"
          },
          "expireAfter": {
            "unit": "WEEKS",
            "value": 1
          },
          "schedule": {
            "recurrence": "DAILY",
            "repeatInterval": {
              "every": 2
            },
            "startTime": "00:00"
          }
        }
      ]
    }
  ],
  "applicationType": "VMWARE"
}
```

6. Execute the creation of the protection policies using the GreenLake API for Backup and Recovery **POST /backup-recovery/v1beta1/protection-policies**, and I used the above JSON structure in the request body. This is a special POST API execution where the response is returned immediately. The response of this API contained the body of JSON structure that will be useful to identify the protection-jobs such as the **<protection-policies-id>**

![API to create protection policy](/img/api-to-create-protection-policy.png)

The below figure shows the complete response JSON body from the above API that shows the construction of the protection policy with different protection tiers and the schedules associated with the protection tier. The important values were the ids obtained from different protection tiers:

1. **ID: “\<protection-policies-id\>**
2. **SNAPSHOT: “\<snapshot-protection-id\>”**
3. **ON-PREMISES: “\<onprem-protection-id\>”**
4. **CLOUD: “\<cloud-protection-id\>”**

```json
{
    "assigned": false,
    "description": "Snapshot-local-cloud",
    "id": "<protection-policies-id",
    "name": "VMware create three tiers",
    "protections": [
        {
            "id": "<snapshot-protection-id>",           
            "schedules": [
                {
                    "scheduleId": 1,
                    "name": "Array_Snapshot_1",
                    "schedule": {
                        "activeTime": {
                            "activeFromTime": "00:00",
                            "activeUntilTime": "23:59"
                        },
                        "recurrence": "HOURLY",
                        "repeatInterval": {
                            "every": 4
                        }
                    },
                    "expireAfter": {
                        "unit": "DAYS",
                        "value": 1
                    },
                    "namePattern": {
                        "format": "Array_Snapshot_{DateFormat}"
                    }
                }
            ],
            "type": "SNAPSHOT"
        },
        {
            "id": "<onprem-protection-id>",
            "schedules": [
                {
                    "scheduleId": 2,
                    "sourceProtectionScheduleId": 1,
                    "name": "On-Premises_Protection_Store_2",
                    "schedule": {
                        "recurrence": "DAILY",
                        "repeatInterval": {
                            "every": 1
                        },
                        "startTime": "00:00"
                    },
                    "expireAfter": {
                        "unit": "DAYS",
                        "value": 3
                    },
                    "namePattern": {
                        "format": "On-Premises_Protection_Store_{DateFormat}"
                    }
                }
            ],
            "protectionStoreInfo": {
                "id": "onprem-protectio-store-id",
                "name": "Local_CDS-TPM-PSG#1",
                "type": "backup-recovery/protection-store",
                "resourceUri": "/backup-recovery/v1beta1/protection-stores/501a99e7-fb79-4fd7-89d5-a5dfb3441859",
                "protectionStoreType": "ON_PREMISES"
            },
            "type": "BACKUP"
        },
        {
            "id": “<cloud-protection-id>”,
            "schedules": [
                {
                    "scheduleId": 3,
                    "sourceProtectionScheduleId": 2,
                    "name": "HPE_Cloud_Protection_Store_3",
                    "schedule": {
                        "recurrence": "DAILY",
                        "repeatInterval": {
                            "every": 2
                        },
                        "startTime": "00:00"
                    },
                    "expireAfter": {
                        "unit": "WEEKS",
                        "value": 1
                    },
                    "namePattern": {
                        "format": "HPE_Cloud_Protection_Store_{DateFormat}"
                    }
                }
            ],
            "protectionStoreInfo": {
                "id": "cloud-protection-store-id",
                "name": "Cloud_CDS-TPM-PSGno1_USA, North Virginia",
                "type": "backup-recovery/protection-store",
                "region": "USA, North Virginia",
                "resourceUri": "/backup-recovery/v1beta1/protection-stores/25611df9-f136-424b-b447-aa3a4887869f",
                "protectionStoreType": "CLOUD"
            },
            "type": "CLOUD_BACKUP"
        }
    ],
    "createdAt": "2024-04-05T03:28:03.000000Z",
    "createdBy": {
        "id": "<user-id>",
        "name": "ronald.dharma@hpe.com"
    },
    "generation": 1,
    "resourceUri": "/backup-recovery/v1beta1/protection-policies/f572ce6e-3470-4149-bb5b-530284bf2bc4",
    "consoleUri": "/backup-and-recovery/protection-policies/f572ce6e-3470-4149-bb5b-530284bf2bc4",
    "applicationType": "VMWARE",
    "type": "backup-recovery/protection-policy",
    "updatedAt": "2024-04-05T03:28:03.000000Z"
}
```

Applying protection policy to a Virtual Machine
Next in the list of use cases for this blog post, I followed the progression for the day one activities required to protect a virtual machine which is applying this protection policy to a virtual machine (or any other assets)
The steps required to apply the protection policy against a virtual machine:
1. Obtain the values from virtual machine id, name, and type keys which were going to be used as the key-pair values required for the key assetInfo as shown in below figures. To obtain those, I used the HPE GreenLake API for virtualization to discover the detail information of a virtual machine “0-Linux-Demo-VM02” as shown in below figure.  Additionally, I used filter such as name, and select a bunch of keys as part of the execution the GET /virtualization/v1beta1/virtual-machines. 




