# Agents

## Get all Agents

> Request

```ruby
require 'nx'

agents = NX::Agent.all
```

```shell
curl "http://nexme.us/api/v1/agents"
```

```javascript
const nx = require('nx');

let agents = nx.agents.all();
```
> Response object

```json
[
  {
    "...":"",
    "agent_info": {
      "city": "Bellevue",
      "state": "WA",
      "re_firm": "Keller Williams",
      "birthday": "Jun 11, 1986",
      "license_number": "1234567899"
    },
    "active_agent": true,
    "available_agent": false,
    "latitude": null,
    "longitude": null,
    "payment_info": {
      "card": "Visa",
      "plan": "agent_basic_plan",
      "last4": "4242",
      "customer_id": "cus_A6r9VzPRhHvBXj",
      "subscription_id": "sub_A6r9ARhuOII8sH"
    },
    "...":""
  }
]
```

Retrieve all users who have "become an agent". Response will be an array of user objects that include all user attributes along with agent and subscription information.

### HTTP Request

`GET http://nexme.us/api/v1/agents`

### URL Parameters

Parameter | Description
--------- | -----------
/active | Returns only active agents
/available | Returns active agents who are currently available to accept requests


<!-- ############################################################################################## -->

## Create an Agent

> Request

```ruby
require 'nx'

agent = NX::Agent.new(agent_params)
agent.save
```

```shell
curl -i -X POST -H "Content-Type: application/json" -d '{
  "v1_agent" : {
    "re_firm" : "Real Estate Firm",
    "city" : "Bellevue",
    "state" : "WA",
    "license_number" : "1234567899",
    "phone": "5555555555",
    "birthday" : "Jun 11, 1986",
    "email": "email@example.com",
    "firstname": "Firstname",
    "lastname": "Lastname",
    "cardholder" : "Cardholder Name",
    "card_number" : "4242424242424242",
    "cvv" : "123",
    "expiration" : "12/17",
    "billing_zip" : "98003"    
  }
}' "http://nexme.us/api/v1/agents"
```

```javascript
const nx = require('nx');

let agent = nx.agents.new(agentParams);
```
> Response object

```json
{
  "...":"...",
  "agent_info": {
    "city": "Bellevue",
    "state": "WA",
    "re_firm": "Keller Williams",
    "birthday": "Jun 11, 1986",
    "license_number": "1234567899"
  },
  "active_agent": true,
  "available_agent": false,
  "latitude": null,
  "longitude": null,
  "payment_info": {
    "card": "Visa",
    "plan": "agent_basic_plan",
    "last4": "4242",
    "customer_id": "cus_A6r9VzPRhHvBXj",
    "subscription_id": "sub_A6r9ARhuOII8sH"
  },
  "...":"..."
}
```

Create a new subscription for users how want to be agents on the platform. Collect agent information and credit card information to update their current user object. Having a profile picture/avatar is a requirement before becoming an agent.

<aside class="notice">
Agents are users who have been assigned the <code>agent</code> role in the database.
</aside>

### HTTP Request

`POST http://nexme.us/api/v1/agents`

### Request Parameters

Parameter | Description
--------- | -----------
re_firm | agent real estate firm
city | real estate firm's city
state | WA
license_number | agent license number
phone | user/agent phone number
birthday | user/agent birthday
firstname | user/agent first name
lastname | user/agent last name
cardholder | credit card holder name
card_number | credit card number
cvv | credit card security code
expiration | credit card expiration date
billing_zip | credit card billing zip code

<aside class="notice">
As an agent, user attributes <code>agent_info</code> and <code>payment_info</code> will not be null
</aside>

<!-- ############################################################################################## -->

## Update an Agent

> Request

```ruby
require 'nx'

uid   = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'
agent = NX::Agent.find(uid)

agent.update(agent_info: 'Keller Williams', license_number: 98765432)
```

```shell
curl -i -X PATCH
  -H "Content-Type: application/json"
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  -d '{
        "v1_agent" : {
          "re_firm": "Keller Williams",
          "license_number": "98765432",
          "phone": "5555555555"
        }
      }'
  "http://nexme.us/api/v1/agents/0"
```

```javascript
const nx  = require('nx');

let uid   = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1';
let agent = nx.agents.get(uid);

agent.update(agentInfo: 'Keller Williams', licenseNumber: 98765432)
```

> Response object

```json
{
  "...":"",
  "agent_info": {
    "city": "Bellevue",
    "state": "WA",
    "re_firm": "Keller Williams",
    "birthday": "Jun 11, 1986",
    "license_number": "1234567899"
  },
  "active_agent": true,
  "available_agent": false,
  "latitude": null,
  "longitude": null,
  "payment_info": {
    "card": "Visa",
    "plan": "agent_basic_plan",
    "last4": "4242",
    "customer_id": "cus_A6r9VzPRhHvBXj",
    "subscription_id": "sub_A6r9ARhuOII8sH"
  },
  "...":""
}
```

Update an agent's user attributes and/or agent & payment attribute by sending all parameters directly inside a nested <code>v1_agent</code> object.

### HTTP Request

`PATCH/PUT http://nexme.us/api/v1/agents/0`

### HTTP Header

Parameter | Description
--------- | -----------
uid | identify agent by uid header

### Request Parameters

Parameter | Description
--------- | -----------
re_firm | agent real estate firm
city | real estate firm's city
state | WA
license_number | agent license number
phone | user/agent phone number
birthday | user/agent birthday
firstname | user/agent first name
lastname | user/agent last name
cardholder | credit card holder name
card_number | credit card number
cvv | credit card security code
expiration | credit card expiration date
billing_zip | credit card billing zip code

<!-- ############################################################################################## -->

## Change Status

> Request

```ruby
require 'nx'

uid = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'

agent = NX::Agent.find(uid).toggle_status
agent.save
```

```shell
curl -i -X PUT
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/agents/0/status"
```

```javascript
const nx = require('nx');

let uid = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'

let agent = nx.agents.get(uid);
agent.toggleStatus;
```
> Response object

```json
{
  "active_agent": true
}
```

Agents cannot make themselves "available" for requests until they are verified internally and made active in our database. An agent is verified/active when their <code>active_agent</code> attribute is set to <code>true</code>.

<aside class="notice">
  This endpoint toggles <code>active_agent</code> between true / false upon each request
</aside>

### HTTP Request

`PUT http://nexme.us/api/v1/agents/0/status`

### HTTP Header

Parameter | Description
--------- | -----------
uid | identify agent by uid header

<!-- ############################################################################################## -->

## Delete Agent

> Request

```ruby
require 'nx'

uid = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'

agent = NX::Agent.find(uid)
agent.delete
```

```shell
curl -i -X DELETE
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/agents/0"
```

```javascript
const nx = require('nx');

let uid = '861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1'

let agent = nx.agents.get(uid);
agent.delete();
```
> Response object

```json
{
  "...":"",
  "agent_info": null,
  "payment_info": null,
  "active_agent": false,
  "available_agent": false,
  "...":""
}
```

This endpoint DOES NOT DELETE THE USER. It removes their <code>agent</code> role and reassigns them with the  <code>user</code> role. Their subscription is canceled and their <code>agent_info</code> and <code>payment_info</code> attributes become nullified. The user will still be able to login/use the app just not as an agent.

### HTTP Request

`DELETE http://nexme.us/api/v1/agents/0`

### HTTP Header

Parameter | Description
--------- | -----------
uid | identify agent by uid header


<aside class="notice">
  The entire user object is returned with agent values set as shown in the right pane --->
</aside>

<!-- ############################################################################################## -->
