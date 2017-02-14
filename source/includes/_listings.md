# Listings

## Get all Listings

> Request

```ruby
require 'nx'

listings = NX::Listing.all
```

```shell
curl "http://nexme.us/api/v1/listings"
```

```javascript
const nx = require('nx');

let listings = nx.listings.all();
```
> Response object

```json
[
  {
    "id": 1,
    "property_type": null,
    "listing_type": "MANU",
    "mls_number": "000000",
    "location": {
      "zip": "98004",
      "city": "Bellevue",
      "state": "Washington",
      "address": "0000 Main St.",
      "latitude": 47.2710612,
      "longitude": -122.3006935
    },
    "details": {
      "beds": 3,
      "baths": 2,
      "price": "$53,000",
      "photos": [
        {
          "url": "https://reference-to-image",
          "order": 1
        },
        {
          "url": "https://reference-to-image",
          "order": 2
        },
        {
          "url": "https://reference-to-image",
          "order": 3
        }
      ],
      "status": "A",
      "year_built": 1840,
      "date_listed": "10/21/16",
      "description": "Earum aliquam tempore repellendus ex. Error enim ut sed maxime consequatur. Optio et dolorem laboriosam magnam animi. Adipisci sed sed blanditiis qui nostrum consequatur sequi. Sit fugiat quae velit sint rem.",
      "estmortgage": "$269",
      "square_feet": "1,950"
    },
    "taxes": {
      "amount": 345,
      "tax_year": 2017,
      "parcel_number": 12345678
    },
    "history": {},
    "schools": {
      "EL": "Woodland Elementary School",
      "HS": "Woodland High School",
      "JH": "Woodland Middle School"
    },
    "slug": null,
    "vacant": null,
    "active": true,
    "user_id": 12,
    "created_at": "2017-01-31T00:27:02.298Z",
    "updated_at": "2017-01-31T00:27:02.298Z",
    "likes": 0
  }
]
```

Retrieve all active and pending MLS listings that have their object's <code>active</code> value set to <code>true</code>.

<aside class="notice">
  The <code>active</code> object attribute is not in relation to the property listing's status. The <code>active</code> attribute determines whether the listing is or isn't to be included in the response.
</aside>

### HTTP Request

`GET http://nexme.us/api/v1/listings`

### URL Parameters

Parameter | Description
--------- | -----------
/all | Returns all listings, even if <code>active</code> is false

<!-- ############################################################################################## -->


## Like a Listing

> Request

```ruby
require 'nx'

id = 1
listing = NX::Listing.find(id)

listing.toggle_like
```

```shell
curl -i -X PUT
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/listings/1/like"
```

```javascript
const nx = require('nx');

let id = 1;
let listing = nx.listings.get(id);

listing.toggleLike;
```
> Response object

```json
{
  "id": 9,
  "liked": true,
  "likes": 13
}
```

Liking listings is a matter of toggling a user's "vote" on a listing between 1 and 0, which will translate to true or false for liking a home. The response object includes the listing id, total "like" count, and true / false "liked" for the current user.

### HTTP Request

`PUT http://nexme.us/api/v1/listings/{id}/like`

### HTTP Headers

Parameter | Description
--------- | -----------
uid | identify user by uid header

### URL Parameters

Parameter | Description
--------- | -----------
id | database id of listing to like/unlike

<!-- ############################################################################################## -->


## Get Liked Listings

> Request

```ruby
require 'nx'

listings = NX::Listing.liked
```

```shell
curl
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/listings/liked"
```

```javascript
const nx = require('nx');

let listings = nx.listings.liked();
```
> Response object

```json
[
  {
    "id": 1,
    "property_type": null,
    "listing_type": "MANU",
    "mls_number": "000000",
    "location": {
      "zip": "98004",
      "city": "Bellevue",
      "state": "Washington",
      "address": "0000 Main St.",
      "latitude": 47.2710612,
      "longitude": -122.3006935
    },
    "details": {
      "beds": 3,
      "baths": 2,
      "price": "$53,000",
      "photos": [
        {
          "url": "https://reference-to-image",
          "order": 1
        },
        {
          "url": "https://reference-to-image",
          "order": 2
        },
        {
          "url": "https://reference-to-image",
          "order": 3
        }
      ],
      "status": "A",
      "year_built": 1840,
      "date_listed": "10/21/16",
      "description": "Earum aliquam tempore repellendus ex. Error enim ut sed maxime consequatur. Optio et dolorem laboriosam magnam animi. Adipisci sed sed blanditiis qui nostrum consequatur sequi. Sit fugiat quae velit sint rem.",
      "estmortgage": "$269",
      "square_feet": "1,950"
    },
    "taxes": {
      "amount": 345,
      "tax_year": 2017,
      "parcel_number": 12345678
    },
    "history": {},
    "schools": {
      "EL": "Woodland Elementary School",
      "HS": "Woodland High School",
      "JH": "Woodland Middle School"
    },
    "slug": null,
    "vacant": null,
    "active": true,
    "user_id": 12,
    "created_at": "2017-01-31T00:27:02.298Z",
    "updated_at": "2017-01-31T00:27:02.298Z",
    "likes": 14
  }
]
```

Retrieve all listings (active records) that have been liked by a particular user.

### HTTP Request

`GET http://nexme.us/api/v1/listings/liked`

### HTTP Headers

Parameter | Description
--------- | -----------
uid | identify user by uid header

<!-- ############################################################################################## -->
