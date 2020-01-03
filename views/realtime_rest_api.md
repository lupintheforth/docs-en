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
