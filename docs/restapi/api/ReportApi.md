# ReportApi

HTTP request | Description
------------- | -------------
**GET** [**/report/place/{placeId}**](ReportApi.md#getTimePerUserReport) | Gets the report of total time spent per user inside the place of an organization.


<a name="getTimePerUserReport"></a>
## **GET** /report/place/{placeId}

Gets the report of total time spent per user inside the place of an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **placeId** | **Long**| ID of the organization. The viewer administrator must have permissions for this organization.

### Responses
**200**  
Report of time spent in the place per user returned successfully. [**List**](../model/TimePerUserReport.md)

**204**  
Report is empty. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

