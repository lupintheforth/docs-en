# Realtime Message REST API User Guide

## Request Format

For POST and PUT request, the body of the requests should be JSON. The Content-Type need configured as `application/json`.

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
Lastly, some [global APIs] (#Global API) are labelled with `rtm/{function}`, like `rtm/all-conversations` will search for conversations of all types.

<!-- {% include "views/_rtm_rest_api_v2_normal.njk" %}
{% include "views/_rtm_rest_api_v2_chatroom.njk" %}
{% include "views/_rtm_rest_api_v2_system.njk" %}
{% include "views/_rtm_rest_api_v2_client.njk" %} -->

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
