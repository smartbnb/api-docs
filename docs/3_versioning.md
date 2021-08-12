# Versioning

As we iterate on the Hospitable Public API, it's possible that we will make changes that could cause your application to break. In order to minimise the impact of this, requests that you send to our API should be accompanied by a version, to help us understand what format to respond with.

This version takes the form of a datestamp, and should be sent in the `Content-Type` HTTP header of the request, like so:

```http
Content-Type: `application/vnd.hospitable.20210308+json`
```

The requested datestamp should be the latest known working date for a resource. If no datestamp is sent, the API will respond with the latest version of the resource, along with a warning.

So for example, if a request for the `/foo` endpoint was made without a version header on 2019-09-04 and your client application succeded at processing the response, then this date should be sent with all API requests for that endpoint in production. This effectively locks the response format you'll receive to this tested-against format.

In short: **send the date you have last tested your API integration on**.

> #### Invalid version headers
> 
> Please note that making a request with an invalid version header will cause the latest version of a resource to be returned (along with a warning). This may result in a response schema unexpectedly changing.

### Old versions

Of course, we can't keep old versions of every endpoint around forever. Once a newer version of an endpoint comes out, the older versions will be available for a *minimum* of two months before being retired. Retirement dates will be clearly communicated to provide a chance to upgrade, and API responses will include a warning that you are using a deprecated version. This warning will be included in the response metadata:

```json
"_meta": {
  "rel": "calendar",
  "version": "20191127",
  "warnings": [
    "Requested version is obsolete. You may be receiving unexpected payloads."
  ]
}
```

After the retirement date, it's possible that you will be automatically upgraded to the most recent version as we remove the old endpoint.

Our API Versioning is endpoint-specific, allowing us to update the version datestamp of one endpoint without changing the others. This has the benefit of allowing you to update your integration one endpoint at a time, rather than having to do them all in one go.
