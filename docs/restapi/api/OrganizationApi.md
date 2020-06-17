# OrganizationApi

HTTP request | Description
------------- | -------------
**GET** [**/organization/{organizationId}**](OrganizationApi.md#getOrganization) | Gets the available data for a single organization.
**GET** [**/organization**](OrganizationApi.md#getOrganizationList) | Returns the list of all organizations.
**POST** [**/organization/requestdeletion**](OrganizationApi.md#requestDeletionOfOrganization) | Sends a deletion request to the system. The request will be examined by Stalker administrators.
**PUT** [**/organization**](OrganizationApi.md#updateOrganization) | Updates one or more properties of an organization.
**PATCH** [**/organization/{organizationId}/trackingArea**](OrganizationApi.md#updateOrganizationTrackingArea) | Updates the coordinates of the tracking area of an organization.


<a name="getOrganization"></a>
## **GET** /organization/{organizationId}

Gets the data available for a single organization.  Both app users and web-app administrators can access this end-point but,  app users can request information for all the organizations while web-app  administrators can only for the organizations they have access to.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization.

### Responses
**200**  
Organization returned successfully. [**Organization**](../model/Organization.md)

**401**  
The user or the administrator is not authenticated. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="getOrganizationList"></a>
## **GET** /organization

Returns the list of all organizations available in the system. The list can be empty. Only app users can access this end-point.

### Parameters
This endpoint does not need any parameter.

### Responses
**200**  
List of all organizations is non-empty and gets returned successfully. [**List**](../model/Organization.md)

**204**  
List of all organizations is empty. Nothing gets returned.

**401**  
The user is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="requestDeletionOfOrganization"></a>
## **POST** /organization/requestdeletion

Sends a deletion request to the system.  The request will be examined by Stalker administrators. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description
------------- | ------------- | -------------
 **organizationDeletionRequest** | [**OrganizationDeletionRequest**](../model/OrganizationDeletionRequest.md)|

### Responses
**204**  
Request sent successfully. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users and administrators who do not own the organization cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="updateOrganization"></a>
## **PUT** /organization

Updates one or more properties of an organization.  Only web-app administrators (if they have the correct access rights) can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organization** | [**Organization**](../model/Organization.md)|  |

### Responses
**200**  
Organization updated successfully. The updated organization gets returned. [**Organization**](../model/Organization.md)

**400**  
The inserted data has some issues. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users and administrators who do not own the organization cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

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

### Responses
**200**  
The tracking area of the organization was updated successfully. The organization gets returned. [**Organization**](../model/Organization.md)

**400**  
The new tracking area does not respect the area constraints for the organization. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer permission cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/x-www-form-urlencoded
- **Accept**: application/json

