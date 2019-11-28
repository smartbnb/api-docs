# Pagination

When requesting an endpoint that returns a collection of multiple resources, it's likely that you'll run into a paginated response.

Paginated responses can be recognised by the `_pagination` metadata that's included with the response body.

The pagination metadata has the following JSON schema:

```json json_schema
{
  "type": "object",
  "properties": {
    "_pagination": {
      "type": "object",
      "required": [
        "total",
        "count",
        "per_page",
        "current_page",
        "total_pages"
      ],
      "properties": {
        "total": {
          "type": "integer",
          "minimum": 1
        },
        "count": {
          "type": "integer",
          "minimum": 1
        },
        "per_page": {
          "type": "integer",
          "minimum": 1,
          "maximum": 50
        },
        "current_page": {
          "type": "integer",
          "minimum": 1
        },
        "total_pages": {
          "type": "integer",
          "minimum": 1
        }
      }
    }
  }
}
```

More information on this schema:

- `total`: The total number of results found.
- `count`: The number of results shown on the current page.
- `per_page`: The number of results that are shown on a page. Defaults to 10.
- `current_page`: The current page of results being shown in this response.
- `total_pages`: The total number of pages available.



## Manipulating pages

Pagination can be manipulated via two query string parameters common to all paginated endpoints:

- `page` (integer): The page of results to fetch. Defaults to 1 if omitted. Trying to request a page beyond the maximum will result in a `404` error.
- `per_page` (integer): The number of items to show on a single page. Defaults to 10 if omitted, maximum is 50.

