# AdministratorBindingRequest

## Description
Request object for creating a new administrator account and binding it to the organization or just binding an already existent administrator.

## Properties

Name | Type | Description
------------ | ------------- | -------------
**organizationId** | **Long** | Unique identifier of the organization the administrator is part of.
**orgAuthServerId** | **String** | Administrator unique identifier from the authentication server of the organization.
**mail** | **String** | Administrator's e-mail address.
**password** | **String** | Administrator's new password.
**permission** | **Integer** | What can or cannot do an organization's administrator. The permission levels are: - Owner: 3 (higher level) - Manager: 2 - Viewer: 1 (lowest level)



