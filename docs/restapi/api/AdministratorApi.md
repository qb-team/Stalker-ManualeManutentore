# AdministratorApi

HTTP request | Description
------------- | -------------
**POST** [**/administrator/bindadministrator**](AdministratorApi.md#bindAdministratorToOrganization) | Bind an already existent administrator to the organization.
**POST** [**/administrator/createadministrator**](AdministratorApi.md#createNewAdministratorInOrganization) | Creates and binds a new administrator to the organization.
**GET** [**/administrator/organization/{organizationId}**](AdministratorApi.md#getAdministratorListOfOrganization) | Returns the list of administrators of the organization.
**GET** [**/administrator/permission/{administratorId}**](AdministratorApi.md#getPermissionList) | Gets the list of permission that an administrator has permissions to view/manage/own.
**POST** [**/administrator/unbindadministrator**](AdministratorApi.md#unbindAdministratorFromOrganization) | Unbind an administrator to the organization.
**PATCH** [**/administrator/updatepermission**](AdministratorApi.md#updateAdministratorPermission) | Update the permission for an already existent administrator in the organization.


<a name="bindAdministratorToOrganization"></a>
## **POST** /administrator/bindadministrator

Bind an already existent administrator to the organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **administratorBindingRequest** | [**AdministratorBindingRequest**](../model/AdministratorBindingRequest.md)|  |

### Responses
**201**  
Administrator bound successfully. The permission record gets returned. [**Permission**](../model/Permission.md)

**400**  
Administrators cannot bind an administrator to an organization with permissions higher than theirs. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer or manager permission cannot have access. Nothing gets returned.

**404**  
The organization or the administrator could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="createNewAdministratorInOrganization"></a>
## **POST** /administrator/createadministrator

Creates and binds a new administrator to the current organization.  Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **administratorBindingRequest** | [**AdministratorBindingRequest**](../model/AdministratorBindingRequest.md)|  |

### Responses
**201**  
Administrator created and bound successfully. The permission record gets returned. [**Permission**](../model/Permission.md)

**400**  
The administrator to be created has already an account. The process could not succeed. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer or manager permission cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="getAdministratorListOfOrganization"></a>
## **GET** /administrator/organization/{organizationId}

Returns the list of administrators of the organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **organizationId** | **Long**| ID of an organization. The administrator must have at least owner permission to the organization.

### Responses
**200**  
Administrators' information returned successfully. [**List**](../model/Permission.md)

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer or manager permission cannot have access. Nothing gets returned.

**404**  
The organization could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="getPermissionList"></a>
## **GET** /administrator/permission/{administratorId}

Gets the list of organizations that an administrator has permissions to view/manage/own. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **administratorId** | **String**| ID of the administrator. It must be the same of the administratorId of the authenticated administrator.

### Responses
**200**  
List of permissions returned successfully. [**List**](../model/Permission.md)

**204**  
List of permissions is empty. Nothing gets returned.

**401**  
The user or the administrator is not authenticated. Nothing gets returned.

**403**  
Administrators cannot have access. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="unbindAdministratorFromOrganization"></a>
## **POST** /administrator/unbindadministrator

Unbind an administrator to the organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **permission** | [**Permission**](../model/Permission.md)|  |

### Responses
**204**  
Administrator unbound successfully. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer or manager permission cannot have access. Nothing gets returned.

**404**  
The permission record could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

<a name="updateAdministratorPermission"></a>
## **PATCH** /administrator/updatepermission

Update the permission for an already existent administrator in the organization. Only web-app administrators can access this end-point.

### Parameters

Name | Type | Description 
------------- | ------------- | -------------
 **permission** | [**Permission**](../model/Permission.md)|  |

### Responses
**201**  
Administrator's permissions updated successfully. The permission record gets returned. [**Permission**](../model/Permission.md)

**400**  
Only the permission can be changed. The request was not satisfied. Nothing gets returned.

**401**  
The administrator is not authenticated. Nothing gets returned.

**403**  
Users or administrator with viewer or manager permission cannot have access. Nothing gets returned.

**404**  
The organization or the administrator could not be found. Nothing gets returned.

### Authorization

[bearerAuth](../overview.md#bearerAuth)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

