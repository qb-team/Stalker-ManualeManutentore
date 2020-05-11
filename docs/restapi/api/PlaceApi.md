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
 **place** | [**Place**](/restapi/model/Place.md)|  |

### Return type

[**Place**](/restapi/model/Place.md)

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

### Return type

null (empty response body)

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

### Return type

[**List**](/restapi/model/Place.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="updatePlace"></a>
## **PUT** /place

Updates one or more properties of a place of an organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **place** | [**Place**](/restapi/model/Place.md)|  |

### Return type

[**Place**](/restapi/model/Place.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

