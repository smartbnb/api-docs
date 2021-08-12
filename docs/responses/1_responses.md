# HTTP Responses

## HTTP Status Codes

The Hospitable Public API returns [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) with every response, including error codes. All being well, you should expect to see status codes in the 200 range alongside your responses.

In the event of a problem, the status code is a reliable indicator of what went wrong. Return codes in the 400 range indicate that there was an issue with the request that was sent. Status codes in the 500 range may mean that either we or a provider (e.g. Airbnb or HomeAway/VRBO) are experiencing an issue - check our [Status Page](https://status.hospitable.com) for more information on that.

## Response Body Format

The Hospitable API responds in JSON format adhering to the following JSON Schema:

```json json_schema
{
  "type": "object",
  "required": [
    "data",
    "_meta"
  ],
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "_included": {
            "type": "array",
            "items": {
              "type": "object",
              "required": [
                "data",
                "rel"
              ],
              "properties": {
                "rel": {
                  "type": "string"
                },
                "data": {
                  "type": "object"
                }
              }
            }
          }
        }
      }
    },
    "_pagination": {
      "type": "object"
    },
    "_meta": {
      "type": "object",
      "required": [
        "rel",
        "version"
      ],
      "properties": {
        "rel": {
          "type": "string"
        },
        "version": {
          "type": "string"
        },
        "warnings": {
          "type": "array"
        }
      }
    }
  }
}
```

A further explanation of this schema:

- `data`: The requested data, either as an entity or array of entities (if multiple were requested)
- `_included`: Any included resources added onto the request. See [docs on Includes](./3_includes.md).
- `_pagination`: Information on the number of pages available, if the request was paginated. See [pagination docs](./2_pagination.md).
- `_meta`: Further information alongside the request, possibly including links to other resources, or any warnings (e.g. if a deprecated version of the resource was requested).
