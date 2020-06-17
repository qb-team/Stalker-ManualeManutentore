# PresenceApi

HTTP request | Description
------------- | -------------
**GET** [**/presence/organization/{organizationId}/counter**](PresenceApi.md#getOrganizationPresenceCounter) | Gets the number of people currently inside the organization's trackingArea.
**GET** [**/presence/place/{placeId}/counter**](PresenceApi.md#getPlacePresenceCounter) | Gets the number of people currently inside the place's trackingArea.


<a name="getOrganizationPresenceCounter"></a>
## **GET** /presence/organization/{organizationId}/counter

Gets the number of people currently inside the organization's trackingArea. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization.

### Responses
**200**  
Organization presence counter returned successfully. [**OrganizationPresenceCounter**](../model/OrganizationPresenceCounter.md)

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users cannot access this end-point. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="getPlacePresenceCounter"></a>
## **GET** /presence/place/{placeId}/counter

Gets the number of people currently inside the place's trackingArea. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **placeId** | **Long**| ID of a place.

### Responses
**200**  
Place presence counter returned successfully. [**PlacePresenceCounter**](../model/PlacePresenceCounter.md)

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users cannot access this end-point. Nothing gets returned.

**404**  
The place could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

