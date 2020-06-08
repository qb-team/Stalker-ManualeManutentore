# AccessApi

HTTP request | Description
------------- | -------------
**GET** [**/access/organization/{organizationId}/anonymous/{exitTokens}**](AccessApi.md#getAnonymousAccessListInOrganization) | Returns all the anonymous accesses in an organization registered of the user owning the exitTokens (exitTokens are separated by commas).
**GET** [**/access/place/{placeId}/anonymous/{exitTokens}**](AccessApi.md#getAnonymousAccessListInPlace) | Returns all the anonymous accesses in a place registered of the user owning the exitTokens (exitTokens are separated by commas).
**GET** [**/access/organization/{organizationId}/authenticated/{orgAuthServerIds}**](AccessApi.md#getAuthenticatedAccessListInOrganization) | Returns all the authenticated accesses in an organization registered of one or more users (orgAuthServerIds are separated by commas).
**GET** [**/access/place/{placeId}/authenticated/{orgAuthServerIds}**](AccessApi.md#getAuthenticatedAccessListInPlace) | Returns all the authenticated accesses in a place registered of one or more users (orgAuthServerIds are separated by commas).


<a name="getAnonymousAccessListInOrganization"></a>
## **GET** /access/organization/{organizationId}/anonymous/{exitTokens}

Returns all the anonymous accesses in an organization registered of the user owning the exitTokens (exitTokens are separated by commas) that are fully registered. Fully registered means that there are both the entrance and the exit timestamp. Only app users can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **exitTokens** | **String array**| One or more exitTokens.
 **organizationId** | **Long**| ID of an organization.

### Return type

[**List**](/restapi/model/OrganizationAccess.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="getAnonymousAccessListInPlace"></a>
## **GET** /access/place/{placeId}/anonymous/{exitTokens}

Returns all the anonymous accesses in a place registered of the user owning the exitTokens (exitTokens are separated by commas) that are fully registered. Fully registered means that there are both the entrance and the exit timestamp. Only app users can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **exitTokens** | **String array**| One or more exitTokens.
 **placeId** | **Long**| ID of a place.

### Return type

[**List**](/restapi/model/PlaceAccess.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="getAuthenticatedAccessListInOrganization"></a>
## **GET** /access/organization/{organizationId}/authenticated/{orgAuthServerIds}

Returns all the authenticated accesses in an organization registered of one or more users (orgAuthServerIds are separated by commas) that are fully registered. Fully registered means that there are both the entrance and the exit timestamp. Both app users and web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **orgAuthServerIds** | **String array**| One or more orgAuthServerIds. If it is called by the app user, the orgAuthServerIds parameter can only consist in one identifier. Otherwise it can be more than one identifier.
 **organizationId** | **Long**| ID of an organization

### Return type

[**List**](/restapi/model/OrganizationAccess.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

<a name="getAuthenticatedAccessListInPlace"></a>
## **GET** /access/place/{placeId}/authenticated/{orgAuthServerIds}

Returns all the authenticated accesses in a place registered of one or more users (orgAuthServerIds are separated by commas) that are fully registered. Fully registered means that there are both the entrance and the exit timestamp. Both app users and web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **orgAuthServerIds** | **String array**| One or more orgAuthServerIds. If it is called by the app user, the orgAuthServerIds parameter can only consist in one identifier. Otherwise it can be more than one identifier.
 **placeId** | **Long**| ID of a place.

### Return type

[**List**](/restapi/model/PlaceAccess.md)

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

