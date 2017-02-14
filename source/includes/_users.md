# Users

## Get all Users

> Request

```ruby
require 'nx'

users = NX::User.all
```

```shell
curl "http://nexme.us/api/v1/users"
```

```javascript
const nx = require('nx');

let users = nx.users.all();
```
> Response object

```json
[
  {
    "active_agent": false,
    "firstname": "Firstname",
    "lastname": "Lastname",
    "email": "user@email.com",
    "phone": "1234567890",
    "uid": "861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1",
    "id": 19,
    "provider": "email",
    "image": null,
    "fullname": "Firstname Lastname",
    "nickname": "firstlast",
    "agent_info": null,
    "available_agent": false,
    "latitude": null,
    "longitude": null,
    "payment_info": null,
    "created_at": "2017-02-05T09:17:50.886Z",
    "updated_at": "2017-02-13T06:08:29.583Z"
  }
]
```

Retrieve all users who do not have the <code>agent</code> role assigned to them

### HTTP Request

`GET http://nexme.us/api/v1/users`

<!-- ############################################################################################## -->

## Update a User

> Request

```ruby
require 'nx'

uid   = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'
user = NX::User.find(uid)

user.update(lastname: 'Newname', phone: 5555555555)
```

```shell
curl -i -X PATCH
  -H "Content-Type: application/json"
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  -d '{
        "v1_user" : {
          "lastname": "Newname",
          "phone": "5555555555"
        }
      }'
  "http://nexme.us/api/v1/users/0"
```

```javascript
const nx  = require('nx');

let uid   = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1';
let user = nx.users.get(uid);

user.update(lastname: 'Newname', phone: 98765432)
```

> Response object

```json
{
  "active_agent": false,
  "firstname": "Firstname",
  "lastname": "Newname",
  "email": "user@email.com",
  "phone": "5555555555",
  "uid": "861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1",
  "id": 19,
  "provider": "email",
  "image": "http://reference-to-base64-decoded-image-upload",
  "fullname": "Firstname Newname",
  "nickname": "firstnew",
  "agent_info": null,
  "available_agent": false,
  "latitude": null,
  "longitude": null,
  "payment_info": null,
  "created_at": "2017-02-05T09:17:50.886Z",
  "updated_at": "2017-02-13T06:08:29.583Z"
}
```

Update user attributes by sending all parameters directly inside a nested <code>v1_user</code> object.

### HTTP Request

`PATCH/PUT http://nexme.us/api/v1/users/0`

### HTTP Header

Parameter | Description
--------- | -----------
uid | identify user by uid header

### Request Parameters

Parameter | Description
--------- | -----------
phone | user phone number
birthday | user birthday
firstname | user first name
lastname | user last name
image | base64 encoded string

<aside class="notice">
  <code>fullname</code> is updated automatically based on the <code>firstname</code> and <code>lastname</code> attributes
</aside>

<!-- ############################################################################################## -->
