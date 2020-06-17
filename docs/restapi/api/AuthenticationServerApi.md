# AuthenticationServerApi

HTTP request | Description
------------- | -------------
**POST** [**/authenticationserver/userinformation**](AuthenticationServerApi.md#getUserInfoFromAuthServer) | Gets the information on users given their identifier on the organization's authentication server.


<a name="getUserInfoFromAuthServer"></a>
## **POST** /authenticationserver/userinformation

Gets the information on users given their identifier on the organization's authentication server. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description
------------- | ------------- | -------------
 **organizationAuthenticationServerRequest** | [**OrganizationAuthenticationServerRequest**](../model/OrganizationAuthenticationServerRequest.md)|

### Responses
**200**  
Users' information returned successfully. [**List**](../model/OrganizationAuthenticationServerInformation.md)

**204**  
No information was found. Nothing gets returned.

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

