# Including Resources

In some cases, it's possible to request a superset of data to be returned. These are labelled as `Allowed Includes` in the documentation. Using this may save you from making a second API request to get more information.

In order to do this, add a URL parameter of `include` to your request. For example, when requesting Reservations, it's possible to include data on the Guest without having to make separate HTTP requests by adding `include=guest` as a URL parameter:

```bash
curl -H 'Content-Type: application/vnd.hospitable.20190904+json' -H 'Authorization: Bearer <token>' https://api.hospitable.com/calendar/reservations?include=guest
```

This will embed the included resource in the API response, under an `_included` key. For example:

```json
{
  "data": [
    {
      "guest_uuid": "c9bc3e39-4275-4199-944c-cf52079903f9",
      "reservation_code": "AHDKVUCVYEM",
      
      // ...
      
      "_included": [
        {
          "rel": "guest",
          "data": {
            "uuid": "c9bc3e39-4275-4199-944c-cf52079903f9",
            "first_name": "Albert",
            "last_name": "Einstein",
            "email": "al@gmx.de",
            "phone": "+49 555 8349 612"
          }
        }
      ]
    }
  ],
	
  // ...
}
```
