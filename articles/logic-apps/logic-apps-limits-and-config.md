---
title: Limits and configuration - Azure Logic Apps | Microsoft Docs
description: Service limits and configuration values for Azure Logic Apps
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: ''

ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: LADocs; jehollan
---

# Limits and configuration information for Azure Logic Apps

This article describes the limits and configuration details for 
creating and running automated workflows with Azure Logic Apps. 
For Microsoft Flow, see [Limits and configuration in Microsoft Flow](https://docs.microsoft.com/flow/limits-and-config).

<a name="definition-limits"></a>

## Definition limits

Here are the limits for a single logic app definition:

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Actions per workflow | 500 | To extend this limit, you can add nested workflows as needed. |
| Allowed nesting depth for actions | 8 | To extend this limit, you can add nested workflows as needed. | 
| Workflows per region per subscription | 1,000 | | 
| Triggers per workflow | 10 | When working in code view, not the designer | 
| Switch scope cases limit | 25 | | 
| Variables per workflow | 250 | | 
| Characters per expression | 8,192 | | 
| Maximum size for `trackedProperties` | 16,000 characters | 
| Name for `action` or `trigger` | 80 characters | | 
| Length of `description` | 256 characters | | 
| Maximum `parameters` | 50 | | 
| Maximum `outputs` | 10 | | 
||||  

<a name="run-duration-retention-limits"></a>

## Run duration and retention limits

Here are the limits for a single logic app run:

| Name | Limit | 
| ---- | ----- | 
| Run duration | 90 days | 
| Storage retention | 90 days from the run's start time | 
| Minimum recurrence interval | 1 second </br>For logic apps with an App Service Plan: 15 seconds | 
| Maximum recurrence interval | 500 days | 
||| 

To exceed the limits for run duration or 
storage retention in your normal processing flow, 
[contact the Logic Apps team](mailto://logicappsemail@microsoft.com) 
for help with your requirements.

<a name="looping-debatching-limits"></a>

## Looping and debatching limits

Here are the limits for a single logic app run:

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Until iterations | 5,000 | | 
| ForEach items | 100,000 | You can use the [query action](../connectors/connectors-native-query.md) to filter larger arrays as needed. | 
| ForEach Parallelism | 50 | The default is 20. <p>To set a specific level of parallelism in a ForEach loop, set the `runtimeConfiguration` property in the `foreach` action. <p>To sequentially run a ForEach loop, set the `operationOptions` property to "Sequential" in the `foreach` action. | 
| SplitOn items | 100,000 | | 
|||| 

<a name="throughput-limits"></a>

## Throughput limits

Here are the limits for a single logic app run:

| Name | Limit | Notes | 
| ----- | ----- | ----- | 
| Actions executions per 5 minutes | 100,000 | To increase the limit to 300,000, you can run a logic app in `High Throughput` mode. To configure high throughput mode, under the `runtimeConfiguration` of the workflow resource, set the `operationOptions` property to `OptimizedForHighThroughput`. <p>**Note**: High throughput mode is in preview. Also, you can distribute a workload across multiple apps as necessary. | 
| Actions concurrent outgoing calls | ~2,500 | Decrease number of concurrent requests or reduce the duration as needed. | 
| Runtime endpoint: Concurrent incoming calls | ~1,000 | Decrease number of concurrent requests or reduce the duration as needed. | 
| Runtime endpoint: Read calls per 5 minutes  | 60,000 | Can distribute workload across multiple apps as needed. | 
| Runtime endpoint: Invoke calls per 5 minutes| 45,000 |Can distribute workload across multiple apps as needed. | 
|||| 

To exceed these limits in normal processing, 
or run load testing that might exceed these limits, 
[contact the Logic Apps team](mailto://logicappsemail@microsoft.com) 
for help with your requirements.

<a name="request-limits"></a>

## HTTP Request limits

Here are the limits for a single HTTP 
request or synchronous connector call:

#### Timeout

Some connector operations make asynchronous calls or listen for webhook requests, so the timeout for these operations might be longer than these limits. For more information, see the technical details for the specific connector and also [Workflow triggers and actions](../logic-apps/logic-apps-workflow-actions-triggers.md#http-action).

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Outgoing request | 120 seconds | For longer running operations, use an [asynchronous polling pattern](../logic-apps/logic-apps-create-api-app.md#async-pattern) or an [until loop](../logic-apps/logic-apps-workflow-actions-triggers.md#until-action). | 
| Synchronous response | 120 seconds | For the original request to get the response, all steps in the response must finish within the limit unless you call another logic app as a nested workflow. For more information, see [Call, trigger, or nest logic apps](../logic-apps/logic-apps-http-endpoint.md). | 
|||| 

#### Message size

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Message size | 100 MB | Some connectors and APIs might not support 100 MB. | 
| Expression evaluation limit | 131,072 characters | The `@concat()`, `@base64()`, `@string()` expressions can't be longer than this limit. | 
|||| 

#### Retry policy

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Retry attempts | 90 | The default is 4. To change the default, use the [retry policy parameter](../logic-apps/logic-apps-workflow-actions-triggers.md). | 
| Retry max delay | 1 day | To change the default, use the [retry policy parameter](../logic-apps/logic-apps-workflow-actions-triggers.md). | 
| Retry min delay | 5 seconds | To change the default, use the [retry policy parameter](../logic-apps/logic-apps-workflow-actions-triggers.md). |
|||| 

<a name="custom-connector-limits"></a>

## Custom connector limits

Here are the limits for custom connectors that you can create from web APIs.

| Name | Limit | 
| ---- | ----- | 
| Number of custom connectors | 1,000 per Azure subscription | 
| Number of requests per minute for each connection created by a custom connector | 500 requests per connection |
|||| 

<a name="integration-account-limits"></a>

## Integration account limits

<a name="artifact-number-limits"></a>

### Artifact limits per integration account

Here are the limits on the number of artifacts for each integration account.

*Free pricing tier*

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Agreements | 10 | | 
| Other artifact types | 25 | Artifact types include partners, schemas, certificates, and maps. Each type can have up to the maximum number of artifacts. | 
|||| 

*Standard pricing tier*

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Any type of artifact | 500 | Artifact types include agreements, partners, schemas, certificates, and maps. Each type can have up to the maximum number of artifacts. | 
|||| 

<a name="artifact-capacity-limits"></a>

### Artifact capacity limits

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| Schema | 8 MB | To upload files larger than 2 MB, use the [blob URI](../logic-apps/logic-apps-enterprise-integration-schemas.md). | 
| Map (XSLT file) | 2 MB | | 
| Runtime endpoint: Read calls per 5 minutes | 60,000 | You can distribute the workload across multiple accounts as necessary. | 
| Runtime endpoint: Invoke calls per 5 minutes | 45,000 | You can distribute the workload across multiple accounts as necessary. | 
| Runtime endpoint: Tracking calls per 5 minutes | 45,000 | You can distribute the workload across multiple accounts as necessary. | 
| Runtime endpoint: Blocking concurrent calls | ~1,000 | You can decrease the number of concurrent requests or reduce the duration as necessary. | 
||||  

<a name="b2b-protocol-limits"></a>

### B2B protocol (AS2, X12, EDIFACT) message size

Here are the limits that apply to B2B protocols:

| Name | Limit | Notes | 
| ---- | ----- | ----- | 
| AS2 | 50 MB | Applies to decode and encode | 
| X12 | 50 MB | Applies to decode and encode | 
| EDIFACT | 50 MB | Applies to decode and encode | 
|||| 

<a name="configuration"></a>

## Configuration: IP addresses

### Azure Logic Apps service

All logic apps in a region use the same range of IP addresses.
The calls that logic apps directly make with 
[HTTP](../connectors/connectors-native-http.md), 
[HTTP + Swagger](../connectors/connectors-native-http-swagger.md) 
or other HTTP requests, come from IP addresses in this list. 

| Logic Apps region | Outbound IP |
|-------------------|-------------|
| Australia | 13.73.114.207, 13.77.3.139, 13.70.159.205 |
| Australia East | 13.75.149.4, 104.210.91.55, 104.210.90.241 |
| Brazil South | 191.235.82.221, 191.235.91.7, 191.234.182.26 |
| Canada Central | 52.233.29.92, 52.228.39.241, 52.228.39.244 |
| Canada East | 52.232.128.155, 52.229.120.45, 52.229.126.25 |
| Central India | 52.172.154.168, 52.172.186.159, 52.172.185.79 |
| Central US | 13.67.236.125, 104.208.25.27, 40.122.170.198 |
| East Asia | 13.75.94.173, 40.83.127.19, 52.175.33.254 |
| East US | 13.92.98.111, 40.121.91.41, 40.114.82.191 |
| East US 2 | 40.84.30.147, 104.208.155.200, 104.208.158.174 |
| Japan East | 13.71.158.3, 13.73.4.207, 13.71.158.120 |
| Japan West | 40.74.140.4, 104.214.137.243, 138.91.26.45 |
| North Central US | 168.62.248.37, 157.55.210.61, 157.55.212.238 |
| North Europe | 40.113.12.95, 52.178.165.215, 52.178.166.21 |
| South Central US | 104.210.144.48, 13.65.82.17, 13.66.52.232 |
| South India | 52.172.50.24, 52.172.55.231, 52.172.52.0 |
| Southeast Asia | 13.76.133.155, 52.163.228.93, 52.163.230.166 |
| West Central US | 52.161.27.190, 52.161.18.218, 52.161.9.108 |
| West Europe | 40.68.222.65, 40.68.209.23, 13.95.147.65 |
| West India | 104.211.164.80, 104.211.162.205, 104.211.164.136 |
| West US | 52.160.92.112, 40.118.244.241, 40.118.241.243 |
| West US 2 | 13.66.210.167, 52.183.30.169, 52.183.29.132 |
| UK South | 51.140.74.14, 51.140.73.85, 51.140.78.44 |
| UK West | 51.141.54.185, 51.141.45.238, 51.141.47.136 |
| | |

| Logic Apps region | Inbound IP |
|-------------------|-------------|
| Australia East | 3.75.153.66, 104.210.89.222, 104.210.89.244 |
| Australia Southeast | 13.73.115.153, 40.115.78.70, 40.115.78.237 |
| Brazil South | 191.235.86.199, 191.235.95.229, 191.235.94.220 |
| Canada Central | 13.88.249.209, 52.233.30.218, 52.233.29.79 |
| Canada East | 52.232.129.143, 52.229.125.57, 52.232.133.109 |
| Central India | 52.172.157.194, 52.172.184.192, 52.172.191.194 |
| Central US | 13.67.236.76, 40.77.111.254, 40.77.31.87 |
| East Asia | 168.63.200.173, 13.75.89.159, 23.97.68.172 |
| East US | 137.135.106.54, 40.117.99.79, 40.117.100.228 |
| East US 2 | 40.84.25.234, 40.79.44.7, 40.84.59.136 |
| Japan East | 13.71.146.140, 13.78.84.187, 13.78.62.130 |
| Japan West | 40.74.140.173, 40.74.81.13, 40.74.85.215 |
| North Central US | 168.62.249.81, 157.56.12.202, 65.52.211.164 |
| North Europe | 13.79.173.49, 52.169.218.253, 52.169.220.174 |
| South Central US | 52.172.9.47, 52.172.49.43, 52.172.51.140 |
| South India | 52.172.9.47, 52.172.49.43, 52.172.51.140 |
| Southeast Asia | 52.163.93.214, 52.187.65.81, 52.187.65.155 |
| West Central US | 52.161.26.172, 52.161.8.128, 52.161.19.82 |
| West Europe | 13.95.155.53, 52.174.54.218, 52.174.49.6 |
| West India | 104.211.164.112, 104.211.165.81, 104.211.164.25 |
| West US | 52.160.90.237, 138.91.188.137, 13.91.252.184 |
| West US 2 | 13.66.224.169, 52.183.30.10, 52.183.39.67 |
| UK South | 51.140.79.109, 51.140.78.71, 51.140.84.39 |
| UK West | 51.141.48.98, 51.141.51.145, 51.141.53.164 |
| | |

### Connectors

The calls that [connectors](../connectors/apis-list.md) 
make come from the IP addresses in this list.

| Logic Apps region | Outbound IP |
|-------------------|-------------|
| Australia East | 40.126.251.213 |
| Australia Southeast | 40.127.80.34 |
| Brazil South | 191.232.38.129 |
| Canada Central | 52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13 |
| Canada East | 52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52 |
| Central India | 104.211.98.164 |
| Central US | 40.122.49.51 |
| East Asia | 23.99.116.181 |
| East US | 191.237.41.52 |
| East US 2 | 104.208.233.100 |
| Japan East | 40.115.186.96 |
| Japan West | 40.74.130.77 |
| North Central US | 65.52.218.230 |
| North Europe | 104.45.93.9 |
| South Central US | 104.214.70.191 |
| South India | 104.211.227.225 |
| Southeast Asia | 13.76.231.68 |
| West Europe | 40.115.50.13 |
| West India | 104.211.161.203 |
| West US | 104.40.51.248 |
| UK South | 51.140.80.51 |
| UK West | 51.141.47.105 |
| | | 

## Next steps  

* [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md)  
* [Common examples and scenarios](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Video: Automate business processes with Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Video: Integrate your systems with Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
