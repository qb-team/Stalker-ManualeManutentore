# MovementApi

HTTP request | Description
------------- | -------------
**POST** [**/movement/track/organization**](MovementApi.md#trackMovementInOrganization) | Tracks the user movement inside the trackingArea of an organization.
**POST** [**/movement/track/place**](MovementApi.md#trackMovementInPlace) | Tracks the user movement inside the trackingArea of a place of an organization.


<a name="trackMovementInOrganization"></a>
## **POST** /movement/track/organization

Tracks the user movement inside the trackingArea of an organization.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationMovement** | [**OrganizationMovement**](../model/OrganizationMovement.md)|  |

### Responses
**201**  
Entrance movement successfully tracked. The movement with the exitToken gets returned. [**OrganizationMovement**](../model/OrganizationMovement.md)

**202**  
Exit movement successfully tracked. The movement gets returned. [**OrganizationMovement**](../model/OrganizationMovement.md)

**400**  
Exit movement was requested without the exitToken. It will not be tracked. Nothing gets returned.

**401**  
The user is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.


### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="trackMovementInPlace"></a>
## **POST** /movement/track/place

Tracks the user movement inside the trackingArea of a place of an organization.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **placeMovement** | [**PlaceMovement**](../model/PlaceMovement.md)|  |

### Responses
**201**  
Entrance movement successfully tracked. The movement with the exitToken gets returned. [**PlaceMovement**](../model/PlaceMovement.md)

**202**  
Exit movement successfully tracked. The movement gets returned. [**PlaceMovement**](../model/PlaceMovement.md)

**400**  
Exit movement was requested without the exitToken. It will not be tracked. Nothing gets returned.

**401**  
The user is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.


### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

