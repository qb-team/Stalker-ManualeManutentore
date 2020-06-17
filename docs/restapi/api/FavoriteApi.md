# FavoriteApi

HTTP request | Description
------------- | -------------
**POST** [**/favorite/addfavorite**](FavoriteApi.md#addFavoriteOrganization) | Adds a new organization to the user's favorite organization list.
**GET** [**/favorite/{userId}**](FavoriteApi.md#getFavoriteOrganizationList) | Gets the list of favorite organizations of a user.
**POST** [**/favorite/removefavorite**](FavoriteApi.md#removeFavoriteOrganization) | Removes the organization from the user's favorite organization list.


<a name="addFavoriteOrganization"></a>
## **POST** /favorite/addfavorite

Adds a new organization to the user's favorite organization list. If the organization has trackingMode: authenticated, then the user account of the organization must be linked to Stalker's account. Only app users can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **favorite** | [**Favorite**](../model/Favorite.md)|  |

### Responses
**201**  
Organization successfully added to the list of favorite. The favorite record just added (including the organization) gets returned. [**Favorite**](../model/Favorite.md)

**400**  
The user already added the organization to the list of favorite organizations.

**401**  
The user is not authenticated. Nothing gets returned.

**403**  
Users who did not bind their account with their organization's account and administrators cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="getFavoriteOrganizationList"></a>
## **GET** /favorite/{userId}

Gets the list of favorite organizations of a user.  Only app users can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **userId** | **String**| ID of the user. It must be the same of the userId of the authenticated user.

### Responses
**200**  
List of favorite organizations returned successfully. [**List**](../model/Organization.md)

**204**  
List of favorite organizations is empty. Nothing gets returned.

**400**  
The supplied userId is incorrect. Nothing gets returned.

**401**  
The user or the administrator is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="removeFavoriteOrganization"></a>
## **POST** /favorite/removefavorite

Removes the organization from the user's favorite organization list. Only app users can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **favorite** | [**Favorite**](../model/Favorite.md)|  |

### Responses
**205**  
Organization successfully removed from the list of favorites.

**401**  
The user is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.

**404**  
The favorite was not found, hence it was not removed. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

