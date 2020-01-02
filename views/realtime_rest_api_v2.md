# Realtime Message REST API User Guide

## Request Format

For POST and PUT request, the main body of the request should be JSON. The Content-Type need configured as `application/json`.

## Authentication

Authentication of the request is via the key-value pair included in the HTTP Header, the parameters are as follows:

Key|Value|Meaning|Source
---|----|---|---
`X-LC-Id`|{{appid}}| App Id of the Current Application| Check in Control Panel -> Settings -> App keys
`X-LC-Key`|{{appkey}}|App key of the Current Application | Check in Control Panel -> Settings -> App keys

Part of the administrative interfaces require master key.

## Relevant Concept

`_Conversation` table included some embedded key strings to define the attributes and participants of the conversations. One-on-One chatting/Group Chats , Chat Rooms , Official Accounts and bots  are in this table [LeanMessage Overview - Conversation](./realtime_v2.html#conversation).

## New Features

With regard to the concept of 「Conversation」 , we have categorized it into three subclasses:

- One-on-One Chatting/Group Chats, related API is labelled with `rtm/conversations`.
- Chat Rooms, related API is labelled with `rtm/chatrooms`. In `_Conversation` table, `tr` is short for true.
- Official Accounts and bots, related API is labelled with `rtm/service-conversations`. In `-Conversation` table , `sys` is short for true.

In addition to that, the client related request is labelled with `rtm/clients`.  
Eventually, some [Global API] (#Global API) are labelled with `rtm/{function}`, like `rtm/all-conversations` will search for conversations of all types.

{% include "views/_rtm_rest_api_v2_normal.njk" %}
{% include "views/_rtm_rest_api_v2_chatroom.njk" %}
{% include "views/_rtm_rest_api_v2_system.njk" %}
{% include "views/_rtm_rest_api_v2_client.njk" %}
