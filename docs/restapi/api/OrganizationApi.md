# OrganizationApi

HTTP request | Description
------------- | -------------
**GET** [**/organization/{organizationId}**](OrganizationApi.md#getOrganization) | Gets the available data for a single organization.
**GET** [**/organization**](OrganizationApi.md#getOrganizationList) | Returns the list of all organizations.
**POST** [**/organization/{organizationId}/requestdeletion**](OrganizationApi.md#requestDeletionOfOrganization) | Sends a deletion request to the system. The request will be examined by Stalker administrators.
**PUT** [**/organization**](OrganizationApi.md#updateOrganization) | Updates one or more properties of an organization.
**PATCH** [**/organization/{organizationId}/trackingArea**](OrganizationApi.md#updateOrganizationTrackingArea) | Updates the coordinates of the tracking area of an organization.


<a name="getOrganization"></a>
## **GET** /organization/{organizationId}

Gets the data available for a single organization.  Both app users and web-app administrators can access this end-point but,  app users can request information for all the organizations while web-app  administrators can only for the organizations they have access to.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization.

### Return type

[**Organization**](/restapi/model/Organization.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="getOrganizationList"></a>
## **GET** /organization

Returns the list of all organizations available in the system. The list can be empty. Only app users can access this end-point.

### Parameters
This endpoint does not need any parameter.

### Return type

[**List**](/restapi/model/Organization.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="requestDeletionOfOrganization"></a>
## **POST** /organization/{organizationId}/requestdeletion

Sends a deletion request to the system.  The request will be examined by Stalker administrators. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization. The administrator must have at least owner permission to the organization.
 **requestReason** | **String**| Request reason for the deletion request.

### Return type

null (empty response body)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/x-www-form-urlencoded
- **Accept**: Not defined

<a name="updateOrganization"></a>
## **PUT** /organization

Updates one or more properties of an organization.  Only web-app administrators (if they have the correct access rights) can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organization** | [**Organization**](/restapi/model/Organization.md)|  |

### Return type

[**Organization**](/restapi/model/Organization.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="updateOrganizationTrackingArea"></a>
## **PATCH** /organization/{organizationId}/trackingArea

Updates the coordinates of the tracking area of an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization. The administrator must have at least manager permission to the organization.
 **trackingArea** | **String**| JSON representation of a tracking trackingArea.

### Return type

[**Organization**](/restapi/model/Organization.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/x-www-form-urlencoded
- **Accept**: application/json

