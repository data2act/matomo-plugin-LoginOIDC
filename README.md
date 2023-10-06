![CI Pipeline](https://github.com/dominik-th/matomo-plugin-LoginOIDC/actions/workflows/ci-pipeline.yml/badge.svg)
# Matomo LoginOIDC Plugin

## Description

Login via third party authentication services.

Easily add a "Login with GitHub" button your Matomo instance. You can also setup any other service to do the authentication for you.

## LoginOIDC extensions

The LoginOIDC (https://github.com/dominik-th/matomo-plugin-LoginOIDC) Matomo plugin is extended by data2act as follows:

### Forwarded-headers

In the Searchdata Matomo configuration, Matomo talks directly to the Keycloak service and does not use the public (https) site address. This makes that when retrieving the OIDC User Info, Keycloak would reject the JWT because the issuer (`iss` field) in the JWT does not match the Keycloak frontend URL. To work around this, the following modifications are made:
* In the userinfo call, a `X-Forwarded-Host` header is sent with the same host as the one from the Authorize-URL.
* In the userinfo call, a `X-Forwarded-Proto` header is sent with the same protocol (http/https) as the one from the Authorize-URL.

### Check for user roles (optional)

To allow access to Matomo for only specific (admin) users, a check is made on the Keycloak realm roles field to contain a role, configured as plugin setting `keycloakRealmRole`.


### New user site id 1 access

When the plugin creates a new Matomo user, it assigns site id `1` to them, so that the user has access to the default site.


## Installation

Install it via Matomo Marketplace.

Alternatively put the files from this repo in <MATOMO_INSTALLATION>/plugins/LoginOIDC and activate it in the settings.

## License

GNU General Public License v3.0
