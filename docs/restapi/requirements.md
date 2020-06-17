# 5.2 Requirements

In order to use these REST API one need to have an available instance of the Stalker Backend running somewhere. Hence, either one runs in its own machine the backend, following the installation and execution rules which can be found [here](../backend/requisiti.md) (in Italian), or connects to an already running backend.

## 5.2.1 Data format
All data sent and received via the REST API is in JSON format (i.e. `application/json`). Currently, only the end-point for updating the tracking area (which can be found [here](api/OrganizationApi.md#updateOrganizationTrackingArea)) sends data as a key-value pair in string format (i.e. `application/x-www-form-urlencoded`).

## 5.2.2 Security
As the authorization data (i.e. accessToken) is sent via HTTP Authorization header in **Bearer** format, one must be sure that all communication between the client and the server is encrypted (HTTPS). It's fairly simple to use and provides a simple way to manage authorization, but it *must* be used over HTTPS.