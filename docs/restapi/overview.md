# 5.2 Overview of Stalker API

## API endpoints
HTTP request | Description
------------- | -------------
**GET** [**/access/organization/{organizationId}/anonymous/{exitTokens}**](api/AccessApi.md#getAnonymousAccessListInOrganization) | Returns all the anonymous accesses in an organization registered of the user owning the exitTokens (exitTokens are separated by commas).
**GET** [**/access/place/{placeId}/anonymous/{exitTokens}**](api/AccessApi.md#getAnonymousAccessListInPlace) | Returns all the anonymous accesses in a place registered of the user owning the exitTokens (exitTokens are separated by commas).
**GET** [**/access/organization/{organizationId}/authenticated/{orgAuthServerIds}**](api/AccessApi.md#getAuthenticatedAccessListInOrganization) | Returns all the authenticated accesses in an organization registered of one or more users (orgAuthServerIds are separated by commas).
**GET** [**/access/place/{placeId}/authenticated/{orgAuthServerIds}**](api/AccessApi.md#getAuthenticatedAccessListInPlace) | Returns all the authenticated accesses in a place registered of one or more users (orgAuthServerIds are separated by commas).
**POST** [**/administrator/bindadministrator**](api/AdministratorApi.md#bindAdministratorToOrganization) | Bind an already existent administrator to the organization.
**POST** [**/administrator/createadministrator**](api/AdministratorApi.md#createNewAdministratorInOrganization) | Creates and binds a new administrator to the organization.
**GET** [**/administrator/organization/{organizationId}**](api/AdministratorApi.md#getAdministratorListOfOrganization) | Returns the list of administrators of the organization.
**GET** [**/administrator/permission/{administratorId}**](api/AdministratorApi.md#getPermissionList) | Gets the list of permission that an administrator has permissions to view/manage/own.
**POST** [**/administrator/unbindadministrator**](api/AdministratorApi.md#unbindAdministratorFromOrganization) | Unbind an administrator to the organization.
**PATCH** [**/administrator/updatepermission**](api/AdministratorApi.md#updateAdministratorPermission) | Update the permission for an already existent administrator in the organization.
**POST** [**/favorite/addfavorite**](api/FavoriteApi.md#addFavoriteOrganization) | Adds a new organization to the user's favorite organization list.
**GET** [**/favorite/{userId}**](api/FavoriteApi.md#getFavoriteOrganizationList) | Gets the list of favorite organizations of a user.
**POST** [**/favorite/removefavorite**](api/FavoriteApi.md#removeFavoriteOrganization) | Removes the organization from the user's favorite organization list.
**POST** [**/movement/track/organization**](api/MovementApi.md#trackMovementInOrganization) | Tracks the user movement inside the trackingArea of an organization.
**POST** [**/movement/track/place**](api/MovementApi.md#trackMovementInPlace) | Tracks the user movement inside the trackingArea of a place of an organization.
**GET** [**/organization/{organizationId}**](api/OrganizationApi.md#getOrganization) | Gets the available data for a single organization.
**GET** [**/organization**](api/OrganizationApi.md#getOrganizationList) | Returns the list of all organizations.
**POST** [**/organization/{organizationId}/requestdeletion**](api/OrganizationApi.md#requestDeletionOfOrganization) | Sends a deletion request to the system. The request will be examined by Stalker administrators.
**PUT** [**/organization**](api/OrganizationApi.md#updateOrganization) | Updates one or more properties of an organization.
**PATCH** [**/organization/{organizationId}/trackingArea**](api/OrganizationApi.md#updateOrganizationTrackingArea) | Updates the coordinates of the tracking area of an organization.
**POST** [**/place**](api/PlaceApi.md#createNewPlace) | Creates a new place for an organization.
**DELETE** [**/place/{placeId}**](api/PlaceApi.md#deletePlace) | Deletes a place of an organization.
**GET** [**/place/organization/{organizationId}**](api/PlaceApi.md#getPlaceListOfOrganization) | Returns the list of places of the organization.
**PUT** [**/place**](api/PlaceApi.md#updatePlace) | Updates one or more properties of a place of an organization.
**GET** [**/presence/organization/{organizationId}/counter**](api/PresenceApi.md#getOrganizationPresenceCounter) | Gets the number of people currently inside the organization's trackingArea.
**GET** [**/presence/place/{placeId}/counter**](api/PresenceApi.md#getPlacePresenceCounter) | Gets the number of people currently inside the place's trackingArea.
**GET** [**/report/place/{placeId}**](api/ReportApi.md#getTimePerUserReport) | Gets the report of total time spent per user inside the place of an organization.


<a name="documentation-for-models"></a>
## Model documentation

 - [AdministratorBindingRequest](model/AdministratorBindingRequest.md)
 - [Favorite](model/Favorite.md)
 - [Organization](model/Organization.md)
 - [OrganizationAccess](model/OrganizationAccess.md)
 - [OrganizationMovement](model/OrganizationMovement.md)
 - [OrganizationPresenceCounter](model/OrganizationPresenceCounter.md)
 - [Permission](model/Permission.md)
 - [Place](model/Place.md)
 - [PlaceAccess](model/PlaceAccess.md)
 - [PlaceMovement](model/PlaceMovement.md)
 - [PlacePresenceCounter](model/PlacePresenceCounter.md)
 - [TimePerUserReport](model/TimePerUserReport.md)


<a name="documentation-for-authorization"></a>
## Authorization documentation

<a name="bearerAuth"></a>
### bearerAuth

- **Type**: HTTP basic authentication


