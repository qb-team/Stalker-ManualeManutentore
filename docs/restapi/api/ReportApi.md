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

### Return type

[**List**](/restapi/model/TimePerUserReport.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

