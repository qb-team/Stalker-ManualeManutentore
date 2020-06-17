# PlaceApi

HTTP request | Description
------------- | -------------
**POST** [**/place**](PlaceApi.md#createNewPlace) | Creates a new place for an organization.
**DELETE** [**/place/{placeId}**](PlaceApi.md#deletePlace) | Deletes a place of an organization.
**GET** [**/place/organization/{organizationId}**](PlaceApi.md#getPlaceListOfOrganization) | Returns the list of places of the organization.
**PUT** [**/place**](PlaceApi.md#updatePlace) | Updates one or more properties of a place of an organization.


<a name="createNewPlace"></a>
## **POST** /place

Creates a new place for an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **place** | [**Place**](../model/Place.md)|  |

### Responses
**201**  
The new place of the organization was created. The place gets returned. [**Place**](../model/Place.md)

**400**  
The new tracking area does not respect the area constraints for the organization. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer permission cannot have access. Nothing gets returned.


### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="deletePlace"></a>
## **DELETE** /place/{placeId}

Deletes a place of an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **placeId** | **Long**| ID of a place.

### Responses
**205**  
Place successfully removed from the list of places of the organization. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users and administrators with viewer permissions cannot have access. Nothing gets returned.

**404**  
The place could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: Not defined

<a name="getPlaceListOfOrganization"></a>
## **GET** /place/organization/{organizationId}

Returns the list of places of the organization. Both app users and web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization.

### Responses
**200**  
Place list of organization returned successfully. [**List**](../model/Place.md)

**204**  
Place list of organization is empty. Nothing gets returned.

**401**  
The administrator or the user is not authenticated. Nothing gets returned.

**403**  
Administrators who are not bound to the organization cannot access this end-point. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="updatePlace"></a>
## **PUT** /place

Updates one or more properties of a place of an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **place** | [**Place**](../model/Place.md)|  |

### Responses
**200**  
Place updated successfully. The updated place gets returned. [**Place**](../model/Place.md)

**400**  
The inserted data has some issues. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer permission cannot have access. Nothing gets returned.

**404**  
Invalid place ID supplied. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

