# Messages

## Get all Threads

> Request

```ruby
require 'nx'

threads = NX::Message.all
```

```shell
curl
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/messages"
```

```javascript
const nx = require('nx');

let threads = nx.messaegs.all();
```
> Response object

```json
[
  {
    "id": 1,
    "created_at": "2017-02-14T08:59:01.724Z",
    "updated_at": "2017-02-14T08:59:01.724Z",
    "message": {
      "id": 2,
      "signal": "message",
      "content": "thanks for showing me the house, how do we move forward?",
      "sender_id": "861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1",
      "recipient_id": "861f7f7f-36f0-4e8d-9f0e-57fg9769e8b1",
      "message_thread_id": 1,
      "created_at": "2017-02-14T09:20:27.290Z",
      "updated_at": "2017-02-14T09:59:05.170Z"
    }
  }
]
```

This endpoint returns all threads related to the user, each thread includes that last/most recently sent/received message. Threads are returned in order of <code>updated_at</code> descending.

### HTTP Request

`GET http://nexme.us/api/v1/messages`

### HTTP Headers

Parameter | Description
--------- | -----------
uid | identify user by uid header

<!-- ############################################################################################## -->


## Get Messages

> Request

```ruby
require 'nx'


thread = NX::MessageThread.find(uid)

thread.messages
```

```shell
curl
  -H "uid: 861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1"
  "http://nexme.us/api/v1/messages/1"
```

```javascript
const nx = require('nx');

let thread = nx.messagesThreads.get(uid);

thread.messages;
```
> Response object

```json
{
  "participants": [
    {
      "uid": "user1@email.com",
      "fullname": "User One"
    },
    {
      "uid": "user2@email.com",
      "fullname": "User Two"
    }
  ],
  "messages": [
    {
      "id": 2,
      "signal": "message",
      "content": "lets me for coffee and go over next steps",
      "sender_id": "861f7f7f-36f0-4e8d-9f0e-57fg9769e8b1",
      "recipient_id": "861f7f7f-36f0-4e8d-9f0e-57fg9769e8b1",
      "message_thread_id": 1,
      "created_at": "2017-02-14T09:20:27.290Z",
      "updated_at": "2017-02-14T09:59:05.170Z"
    },
    {
      "id": 1,
      "signal": "message",
      "content": "thanks for showing me the house, how do we move forward?",
      "sender_id": "861f7f7f-36f0-4e8d-9f0e-c1cfc769e8b1",
      "recipient_id": "861f7f7f-36f0-4e8d-9f0e-57fg9769e8b1",
      "message_thread_id": 1,
      "created_at": "2017-02-14T09:06:00.102Z",
      "updated_at": "2017-02-14T09:59:05.134Z"
    }
  ]
}
```

Get all messages within a single thread, ordered by <code>updated_at</code> descending, along with the name and email of all participants.

### HTTP Request

`GET http://nexme.us/api/v1/messages/{id}`

### HTTP Headers

Parameter | Description
--------- | -----------
uid | identify user by uid header

### URL Parameters

Parameter | Description
--------- | -----------
id | database id of message thread

<aside class="notice">
  The <code>recipient_id</code> attribute is only used for initiating a conversation. Afterwards, the attribute value may remain the same or become null.
</aside>

<!-- ############################################################################################## -->
