# Permission

## Description
Represents what can or cannot do an administrator inside a specified organization.

## Properties

Name | Type | Description
------------ | ------------- | -------------
**administratorId** | **String** | Authentication service's administrator unique identifier.
**organizationId** | **Long** | Unique identifier of the organization the administrator is part of.
**orgAuthServerId** | **String** | Administrator unique identifier from the authentication server of the organization.
**mail** | **String** | Administrator's e-mail address.
**permission** | **Integer** | What can or cannot do an organization's administrator. The permission levels are: - Owner: 3 (higher level) - Manager: 2 - Viewer: 1 (lowest level)
**nominatedBy** | **String** | administratorId of the owner administrator who nominated the current administrators. If this field is equal to administratorId then this administrator is the original owner of the organization (i.e. the one whose account was created during the creation of the organization by Stalker administrators).



