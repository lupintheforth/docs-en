# Realtime Message REST API User Guide

## Request Format

For POST and PUT requests, the body of the requests should be JSON. The Content-Type need configured as `application/json`.

## Authentication

Authentication of the request is via the key-value pair included in the HTTP Header, the parameters are as follows:

Key|Value|Meaning|Source
---|----|---|---
`X-LC-Id`|{{appid}}| App Id of the Current Application| Check in Dashboard -> Settings -> App keys
`X-LC-Key`|{{appkey}}|App key of the Current Application | Check in Dashboard -> Settings -> App keys

Some administrative interfaces require master key.

## Relevant Concept

`_Conversation` table includes some built-in fields to define the attributes and participants of the conversations. For One-on-One Chatting/Group Chats, Chat Rooms, Official Accounts and bots, see [LeanMessage Overview - Conversation](./realtime_v2.html#conversation) for more information.

## Architecture

With regard to the concept of "Conversation" , we have categorized it into three subclasses:

- One-on-One Chatting/Group Chats, related API is labelled with `rtm/conversations`.
- Chat Rooms, related API is labelled with `rtm/chatrooms`. In `_Conversation` table, `tr` is set to true to indicate this.
- Official Accounts and bots, related API is labelled with `rtm/service-conversations`. In `_Conversation` table , `sys` is set to true to indicate this.

In addition, the client related requests are labelled with `rtm/clients`.  

Lastly, some [global APIs](#Global_API) are labelled with `rtm/{function}`, like `rtm/all-conversations` will search for conversations of all types.

## Global API

### Count the Users

This interface will return the total number of the online users and the total number of the independent users with logged in history. This interface requires master key.

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  https://{{host}}/1.2/rtm/stats
```

return

```
{"result":{"online_user_count":10212,"user_count_today":1002324}}
```

`online_user_count` indicates the current online users on the app and `user_count_today` indicates the independent users with logged in history today.

### Query all the conversations

This interface will return all the One-on-One Chatting/Group Chats/Chat Rooms/Official Accounts and bots. In `_Conversation` the default ACL authority requires the master key to access.

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  https://{{host}}/1.2/rtm/all-conversations
```

Parameters | Optionality | description
---|---|---
skip |optional |
limit | optional | together with 'skip' to realize paging
where | optional | see [Leanstorage - Query](rest_api.html#Query).

return
```
{"results"=>[{"name"=>"test conv1", "m"=>["tom", "jerry"], "createdAt"=>"2018-01-17T04:15:33.386Z", "updatedAt"=>"2018-01-17T04:15:33.386Z", "objectId"=>"5a5ecde6c3422b738c8779d7"}]}
```

### Global broadcasts

This interface is able to broadcast messages (at most 30 per day) to clients in the app. This interface requires mater key to access.

```
curl -X POST \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  -H "Content-Type: application/json" \
  -d '{"from_client": "1a", "message": "{\"_lctype\":-1,\"_lctext\":\"pure text message\",\"_lcattrs\":{\"a\":\"_lcattrs to hold some user-specified key-value pairs\"}}", "conv_id": "..."}' \
  https://{{host}}/1.2/rtm/broadcasts
```

Parameters | Optionality | Type | Description
---|---|---|---
from_client | requried | string | sender ID
conv_id | required | string | converation id to send (only in the official accounts)
message | requried | string | message content (generally the content should be of string type but no rigorous limitations on the type. <br/> as long as the size is less than 5kb, the developer can send message of any types.)
valid_till | Optional | number | expiry time, UTC timestamp(millisecond), at most and default on 1 month later.
push | Optional | string or JSON | attached push, **all** the iOS and Windows Phone users will receive the notification if sets.
transient | Optional | boolean | default as false. This field is marked as whether the broadcast is transient. This will broadcast to all the online users. The offline users will not receive the copies after later logging in.

Push formats are in align with the `data` part of  [Push Notification REST API message content](push_guide.html#message content_Data). If you need specified developer certificate push, you have to configure the `"_profile": "dev"` in the JSON for example:

```
{
   "alert": "message content",
   "category": "push category",
   "badge": "Increment",
   "_profile": "dev"
}
```

Frequency limitation:

this interface has frequency limitation , click [here](#interface requests frequency limitation) to view.

### Modify the broadcast messages

This interface requires the master key.

The modification will only occur on the devices do not receive the original message yet. The received broadcast cannot be modified. Please be cautious to broadcast.

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  -H "Content-Type: application/json" \
  -d '{"from_client": "", "message": "", "timestamp": 123}' \
  https://{{host}}/1.2/rtm/service-conversations/{conv_id}/messages/{message_id}
```

Parameters | Optionality | Description
---|---|---
from_client | required | sender ID
message | required | message content
timestamp | required | timestamp of the message

return

```
{"result": {}}
```

Frequency limitation:

this interface has frequency limitation , click [here](#interface requests frequency limitation) to view.

### Delete broadcast messages

The deletions will only occur on the devices do not receive the original message yet. The received broadcast cannot be deleted. This interface requires the master key.

```sh
curl -X DELETE \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  https://{{host}}/1.2/rtm/broadcasts/{message_id}
```

Parameters | Optionality | Description
---|---|---
message_id | required | target id, String

return:

blank JSON object `{}`.

### Query the broadcast messages

Invoke this API to query all the valid broadcast messages, this interface requires master key to query.

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  https://{{host}}/1.2/rtm/broadcasts?conv_id={conv_id}
```

Paramters | Optionality | Description
---|---|---
conv_id | required | official account ID
limit | optional | quantity of the messages returned
skip | optional | number of the messages to skip, for paging.

### Query all the messages history in the app

This interface requires the master key.

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{masterkey}},master" \
  https://{{host}}/1.2/rtm/messages
```

Parameters and the returned value can refer to [One-on-One Chatting/Group Chats query the history messages](realtime_rest_api.html#query history messages) interface.

## Interface requests frequency limitation

Operations related to realtime messages invoking REST API has request frequency and quantity limitations (**realtime message SDK API is not influenced**),  details as follows:

* [One-on-One Chatting/Group Chats- send messages](#One-on-One Chatting/Group Chats- send messages)
* [One-on-One Chatting/Group Chats- modify messages](#One-on-One Chatting/Group Chats- modify messages)
* [One-on-One Chatting/Group Chats- recall messages](#One-on-One Chatting/Group Chats- recall messages)
* [Chats Rooms- send messages](#Chats Rooms- send messages)
* [Chats Rooms- modify messages](#Chats Rooms- modify messages)
* [Chats Rooms- recall messages](#Chats Rooms- recalll messages)
* [Official accounts- send message to any user individually](#send message to any user individually)
* [Official accounts- modify message to any user individually](#modify message to any user individually)
* [Official accounts- recall message to any user individually](#recall message to any user individually)
