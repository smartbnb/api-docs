# Introduction

Welcome to the Hospitable Public API documentation! This early access release of the Hospitable Public API allows you to read calendar data of your active listings in a simple, programmatic way, using conventional HTTP requests.

The API documentation will start with a general overview about the design and technology that has been implemented, followed by reference information about specific endpoints.

## Requests

The Hospitable API conforms to the [REST Architectural Standards](https://en.wikipedia.org/wiki/Representational_state_transfer). Entities are represented as resources, each one with an URL and unique identifier, and can be manipulated with the `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` HTTP methods. All methods with the exception of `POST` are idempotent.

## Security

The API follows [OAuth 2.0](https://tools.ietf.org/html/rfc6749) to protect its endpoints. You may authorise your application to make requests on your account's behalf by using the Client Credentials flow. Generate API credentials from the "Apps" page in your Hospitable account.

[More information on security](./2_security.md).

## Versioning

To reduce risk when using the Hospitable Public API in production, you **must** send a Content-Type header along with all requests containing the version of the API you are using. If this is not sent, you will be served the newest version of the API, including BC breaking changes. 

[More information on versioning](./3_versioning.md).

## Including Resources

In some cases, it's possible to request a superset of data to be returned. These are labelled as `Allowed Includes` in the documentation. Using this may save you from making a second API request to get more information.

[More information on includes](./responses/3_includes.md).
