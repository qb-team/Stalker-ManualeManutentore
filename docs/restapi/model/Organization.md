# Organization
## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | **Long** | Unique identifier for an organization.
**name** | **String** | Name of the organization.
**description** | **String** | Small description of what the organization does.
**image** | **String** | Image/logo for the organization which gets shown on the application.
**street** | **String** | The street where the organization is located.
**number** | **String** | The number in the street where the organization is located.
**postCode** | **Integer** | The postcode where the organization is located.
**city** | **String** | The city where the organization is located.
**country** | **String** | The country where the organization is located.
**authenticationServerURL** | **String** | URL or IP address of the authentication server of the organization. If it&#39;s required a specific port or protocol it must be specified. Needed only if trackingMethod is set to authenticated.
**creationDate** | **DateTime** | When the organization was added to the system.
**lastChangeDate** | **DateTime** | When the organization parameters were last changed.
**trackingArea** | **String** | Area subjected to movement tracking of people. It is a collection of (longitude, latitude) pairs consisting in a polygon. The string is expressed in JSON format.
**trackingMode** | **String** | How an user who added to its favorites the organization can be tracked inside the organization&#39;s trackingArea and its places.



