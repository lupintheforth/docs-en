{% import "views/_helper.njk" as docs %}
{% import "views/_data.njk" as data %}
# REST API Guide

You can access LeanCloud from any devices supporting HTTP requests with REST API, for example:

- You can manipulate data on LeanCloud with any programming language.
- If you want to migrate from LeanCloud to other services, you can export all your data.
- Your mobile site can fetch data from LeanCloud via JavaScript directly if you regard importing LeanCloud JavaScript SDK as overkill.
- You can add new data in batch, to be consumed by mobile applications later.
- You can export recent data for offline analysis or additional incremental backup.

## API Version

The current API version is `1.1`.

### Testing

This guide provides curl command line examples.
You may need to modify some syntax if using cmd.exe on Windows.
For example, `\` in curl examples means to be continued on next line, but cmd.exe will consider it as path separator.
Therefore, we recommend you to use [Postman] for testing on Windows.

[Postman]: https://www.getpostman.com/

Postman can [import curl commands][import-curl] directly and automatically [generate code snippets][generate-snippets] in various languages and frameworks.

[import-curl]: https://learning.getpostman.com/docs/postman/collections/data-formats/#importing-curl
[generate-snippets]: https://learning.getpostman.com/docs/postman/sending-api-requests/generate-code-snippets/

### Objects

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP Method</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/classes/&lt;className&gt;</td>
      <td>POST</td>
      <td>create an object</td>
    </tr>
    <tr>
      <td>/1.1/classes/&lt;className&gt;/&lt;objectId&gt;</td>
      <td>GET</td>
      <td>retrieve an object</td>
    </tr>
    <tr>
      <td>/1.1/classes/&lt;className&gt;/&lt;objectId&gt;</td>
      <td>PUT</td>
      <td>update an object</td>
    </tr>
    <tr>
      <td>/1.1/classes/&lt;className&gt;</td>
      <td>GET</td>
      <td>query objects</td>
    </tr>
    <tr>
      <td>/1.1/classes/&lt;className&gt;/&lt;objectId&gt;</td>
      <td>DELETE</td>
      <td>delete an object</td>
    </tr>
    <tr>
      <td>/1.1/scan/classes/&lt;className&gt;</td>
      <td>GET</td>
      <td>iterate over objects</td>
    </tr>
  </tbody>
</table>

### Users

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP Method</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/users</td>
      <td>POST</td>
      <td>register</td>
    </tr>
    <tr>
      <td>/1.1/usersByMobilePhone</td>
      <td>POST</td>
      <td>register or login via mobile phone</td>
    </tr>
    <tr>
      <td>/1.1/login</td>
      <td>POST</td>
      <td>login</td>
    </tr>
    <tr>
      <td>/1.1/users/&lt;objectId&gt;</td>
      <td>GET</td>
      <td>retrieve a user</td>
    </tr>
    <tr>
      <td>/1.1/users/me</td>
      <td>GET</td>
      <td>retrieve a user via session token</td>
    </tr>
    <tr>
      <td>/1.1/users/&lt;objectId&gt;/refreshSessionToken</td>
      <td>PUT</td>
      <td>reset session token</td>
    </tr>
    <tr>
      <td>/1.1/users/&lt;objectId&gt;/updatePassword</td>
      <td>PUT</td>
      <td>reset password via email</td>
    </tr>
    <tr>
      <td>/1.1/users/&lt;objectId&gt;</td>
      <td>PUT</td>
      <td>update user info</td>
    </tr>
    <tr>
      <td>/1.1/users</td>
      <td>GET</td>
      <td>query users</td>
    </tr>
    <tr>
      <td>/1.1/users/&lt;objectId&gt;</td>
      <td>DELETE</td>
      <td>delete a user</td>
    </tr>
    <tr>
      <td>/1.1/requestPasswordReset</td>
      <td>POST</td>
      <td>request to reset password via email</td>
    </tr>
    <tr>
      <td>/1.1/requestEmailVerify</td>
      <td>POST</td>
      <td>request to verify email</td>
    </tr>
    <tr>
      <td>/1.1/requestMobilePhoneVerify</td>
      <td>POST</td>
      <td>request to verify mobile phone</td>
    </tr>
    <tr>
      <td>/1.1/verifyMobilePhone/&lt;code&gt;</td>
      <td>POST</td>
      <td>verify mobile phone number</td>
    </tr>
    <tr>
      <td>/1.1/requestChangePhoneNumber</td>
      <td>POST</td>
      <td>request to change mobile phone number</td>
    </tr>
    <tr>
      <td>/1.1/changePhoneNumber</td>
      <td>POST</td>
      <td>change mobile phone number</td>
    </tr>
    <tr>
      <td>/1.1/requestLoginSmsCode</td>
      <td>POST</td>
      <td>request to send an SMS for logging in</td>
    </tr>
    <tr>
      <td>/1.1/requestPasswordResetBySmsCode</td>
      <td>POST</td>
      <td>request to reset password via SMS</td>
    </tr>
    <tr>
      <td>/1.1/resetPasswordBySmsCode/&lt;code&gt;</td>
      <td>PUT</td>
      <td>reset password via SMS</td>
    </tr>
  </tbody>
</table>

### Roles

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP Method</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/roles</td>
      <td>POST</td>
      <td>create a role</td>
    </tr>
    <tr>
      <td>/1.1/roles/&lt;objectId&gt;</td>
      <td>GET</td>
      <td>retrieve a role</td>
    </tr>
    <tr>
      <td>/1.1/roles/&lt;objectId&gt;</td>
      <td>PUT</td>
      <td>update a role</td>
    </tr>
    <tr>
      <td>/1.1/roles</td>
      <td>GET</td>
      <td>query roles</td>
    </tr>
    <tr>
      <td>/1.1/roles/&lt;objectId&gt;</td>
      <td>DELETE</td>
      <td>delete a role</td>
    </tr>
  </tbody>
</table>

### Push Notifications

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/push</td>
      <td>POST</td>
      <td>push notifications</td>
    </tr>
    <tr>
      <td>/1.1/notifications</td>
      <td>GET</td>
      <td>query push records</td>
    </tr>
    <tr>
      <td>/1.1/notifications/:notification_id</td>
      <td>GET</td>
      <td>query a push record via ID</td>
    </tr>
    <tr>
      <td>/1.1/notifications/:notification_id</td>
      <td>DELETE</td>
      <td>delete a push record</td>
    </tr>
    <tr>
      <td>/1.1/scheduledPushMessages</td>
      <td>GET</td>
      <td>query all scheduled push notifications</td>
    </tr>
    <tr>
      <td>/1.1/scheduledPushMessages/:id</td>
      <td>DELETE</td>
      <td>delete an scheduled push notification</td>
    </tr>
  </tbody>
</table>

### Installations

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/installations</td>
      <td>POST</td>
      <td>upload installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>GET</td>
      <td>retrieve installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>PUT</td>
      <td>update installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations</td>
      <td>GET</td>
      <td>query installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>DELETE</td>
      <td>delete installation data</td>
    </tr>
  </tbody>
</table>

### Data Schema

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/schemas</td>
      <td>GET</td>
      <td>retrieve all schemas</td>
    </tr>
    <tr>
      <td>/1.1/schemas/&lt;className&gt;</td>
      <td>POST</td>
      <td>retrieve specified class schema</td>
    </tr>
  </tbody>
</table>

### Cloud Functions

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/functions/&lt;functionName&gt;</td>
      <td>POST</td>
      <td>invoke a cloud function</td>
    </tr>
    <tr>
      <td>/1.1/call/&lt;functionName&gt;</td>
      <td>POST</td>
      <td>call a cloud function with AVObjects as parameters and return values</td>
    </tr>
  </tbody>
</table>

### LeanMessage

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/rtm/messages/logs</td>
      <td>GET</td>
      <td>retrieve chat history</td>
    </tr>
    <tr>
      <td>/1.1/rtm/messages</td>
      <td>POST</td>
      <td>send a message</td>
    </tr>
    <tr>
      <td>/1.1/rtm/transient_group/onlines</td>
      <td>GET</td>
      <td>count online members of a transient conversation</td>
    </tr>
  </tbody>
</table>

### Other

<table>
  <thead>
    <tr>
      <th>URL</th>
      <th>HTTP</th>
      <th>Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/1.1/date</td>
      <td>GET</td>
      <td>retrieve date and time at server side</td>
    </tr>
    <tr>
      <td>/1.1/exportData</td>
      <td>POST</td>
      <td>request to export data</td>
    </tr>
    <tr>
      <td>/1.1/exportData/&lt;id&gt;</td>
      <td>GET</td>
      <td>retrieve status and result of export data job</td>
    </tr>
  </tbody>
</table>

### Request Format

The request body should be JSON, and the `Content-Type` should be `application/json` accordingly.

`X-LC-Id` and `X-LC-Key` http headers are used for authentication.

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"content": "update blog post"}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

`X-LC-Id` is App ID.
`X-LC-Key` is App Key or Master Key.
A `,master` postfix is used to distinguish Master Key and App Key, e.g.:

```
X-LC-Key: {{masterkey}},master
```

Cross-origin resource sharing is supported, so you can use these headers with XMLHttpRequest in JavaScript.

#### X-LC-Sign

You may also authenticate requests via `X-LC-Sign` instead of `X-LC-Key`:

```
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Sign: d5bcbb897e19b2f6633c716dfdfaf9be,1453014943466" \
  -H "Content-Type: application/json" \
  -d '{"content": "reduce risk of App Key exposure"}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

The value of `X-LC-Sign` is a string `sign,timestamp[,master]`:

| Name       | Optionality   | Description                                       |
| --------- | ---- | ---------------------------------------- |
| sign      | required   | concat timestamp and App Key (or Master Key), then calculate its MD5 hash value |
| timestamp | required   | unix timestamp of current request, accurate to **milliseconds**  |
| master    | optional   | use this postfix to indicate Master Key is used |

For example, given the following application:

<table class="noheading">
  <tbody>
    <tr>
      <td scope="row">App Id</td>
      <td><code>FFnN2hso42Wego3pWq4X5qlu</code></td>
    </tr>
    <tr>
      <td scope="row">App Key</td>
      <td><code>UtOCzqb67d3sN12Kts4URwy8</code></td>
    </tr>
    <tr>
      <td scope="row">Master Key</td>
      <td><code>DyJegPlemooo4X1tg94gQkw1</code></td>
    </tr>
    <tr>
      <td scope="row">Request date</td>
      <td>2016-01-17 7:15:43.466 UTC</td>
    </tr>
    <tr>
      <td scope="row">timestamp</td>
      <td><code>1453014943466</code></td>
    </tr>
  </tbody>
</table>

**Calculate sign with App Key**

>md5( timestamp + App Key ) <br/>
>= md5( <code><u>1453014943466</u>UtOCzqb67d3sN12Kts4URwy8</code> )<br/>= d5bcbb897e19b2f6633c716dfdfaf9be

```sh
  -H "X-LC-Sign: d5bcbb897e19b2f6633c716dfdfaf9be,1453014943466" \
```

**Calculate sign with Master Key**

>md5( timestamp + Master Key )<br/>
>= md5( <code><u>1453014943466</u>DyJegPlemooo4X1tg94gQkw1</code> ) <br>
>= e074720658078c898aa0d4b1b82bdf4b

```sh
  -H "X-LC-Sign: e074720658078c898aa0d4b1b82bdf4b,1453014943466,master" \
```

<div class="callout callout-danger">Using master key will bypass all permission validations. Make sure you do not leak the master key and only use it in restrained environments.</div>

#### Specify hook invocation environment

Requests may trigger [hooks](leanengine_cloudfunction_guide-node.html#Hooking), and you can use `X-LC-Prod` http header to specify the invocation environment:

| X-LC-Prod Value | Environment |
| - | - |
| 0 | stage |
| 1 | production |

If you do not specify the `X-LC-Prod` http header, LeanCloud will invoke the hook in production environment.

### Response Format

The response body is a JSON object.

HTTP status code is used to indicate whether a request succeeded or failed.
A 2xx status code indicates success, and a 4xx/5xx status code indicates an error is encountered.
When an error is encountered, the response body is a JSON object with two fields: `code` and `error`,
where `code` is the error code (integer) and `error` is a brief error message (string).
The `code` may be identical to the http status code,
but usually it is a customized error code more specific than the http status code.
For example, if you try to save an object with an invalid key name:

```json
{
  "code":105,
  "error":"Invalid key name. Keys are case-sensitive and 'a-zA-Z0-9_' are the only valid characters. The column is: 'invalid?'."}
```

{# TODO 错误代码请看 [错误代码详解](./error_code.html)。#}

## Object

### Object Format

LeanStorage is built around objects.
Each object is consist of several key-value pairs,
where values are in a JSON compatible format.
Objects are schemaless, thus you do not need to allocate keys at the beginning.
You only need to set key-value pairs as you wish and when needed.

For example, if you are implementing a Twitter-like social App, and a tweet may contain the following attributes (key-value pairs):

```json
{
  "content": "Serverless cloud for lightning-fast development.",
  "pubUser": "LeanCloud",
  "pubTimestamp": 1435541999
}
```

Keys can only contain letters, numbers, and underscores.
Values can be anything encoded in JSON.

Each object belongs to a class (table in traditional database terms).
We recommend to use `CapitalizedWords` to name your classes, and `mixedCases` to name your attributes.
This naming style helps to improve code readability.

Each time when an objects is saved to the cloud, a unique `objectId` will be assigned to it.
`createdAt` and `updatedAt` will also be filled in by the cloud which indicate the time the object is created and updated.
These attributes are preserved, and you cannot modify them yourself.
For example, the object above could look like this when retrieved:

```json
{
  "content": "Serverless cloud for lightning-fast development.",
  "pubUser": "LeanCloud",
  "pubTimestamp": 1435541999,
  "createdAt": "2015-06-29T01:39:35.931Z",
  "updatedAt": "2015-06-29T01:39:35.931Z",
  "objectId": "558e20cbe4b060308e3eb36c"
}
```

`createdAt` and `updatedAt` are strings whose content is a UTC timestamps in ISO 8601 format with millisecond precision `YYYY-MM-DDTHH:MM:SS.MMMZ`.
`objectId` is a string unique in the class,
like the primary key of a relational database.

In LeanCloud's REST API, class-level operations use the class name as its endpoint.
For example:

```
https://{{host}}/1.1/classes/Post
```

Users (the built-in `_User` class) have a special endpoint:

```
https://{{host}}/1.1/users
```

Object specific operations use nested URLs under the class.
For example:

```
https://{{host}}/1.1/classes/Post/<objectId>
```

### Creating Objects

To create a new object:

```sh
curl -X POST \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"content": "Serverless cloud for lightning-fast development.","pubUser": "LeanCloud","pubTimestamp": 1435541999}' \
  https://{{host}}/1.1/classes/Post
```

If succeed, you will receive `201 Created` with a `Location` header point to the URL of the object just created:

```sh
Status: 201 Created
Location: https://{{host}}/1.1/classes/Post/558e20cbe4b060308e3eb36c
```

And the response body is a JSON object with `objectedId` and `createdAt` key-value pairs:

```json
{
  "createdAt": "2015-06-29T01:39:35.931Z",
  "objectId": "558e20cbe4b060308e3eb36c"
}
```

To tell LeanCloud to return full data, set the `fetchWhenSave` parameter to `true`:

```sh
curl -X POST \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"content": "Serverless cloud for lightning-fast development.","pubUser": "LeanCloud","pubTimestamp": 1435541999}' \
  https://{{host}}/1.1/classes/Post?fetchWhenSave=true
```

Class names can only contain letters, numbers, and underscores.
Every application can contain up to 500 classes, and there is no limit on objects in each class.

### Retrieving Objects

To fetch the object we just created:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  https://{{host}}/1.1/classes/Post/558e20cbe4b060308e3eb36c
```

The response body is a JSON object containing all attributes you specified above, and three preserved attributes `objectId`, `createdAt`, and `updatedAt`:

```json
{
  "content": "Serverless cloud for lightning-fast development.",
  "pubUser": "LeanCloud",
  "pubTimestamp": 1435541999,
  "createdAt": "2015-06-29T01:39:35.931Z",
  "updatedAt": "2015-06-29T01:39:35.931Z",
  "objectId": "558e20cbe4b060308e3eb36c"
}
```

To fetch other objects this object points to, specify them in `include` parameter:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'include=author' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

If the class does not exist, you will receive a `404 Not Found` error:

```json
{
  "code": 101,
  "error": "Class or object doesn't exists."
}
```

If LeanCloud cannot find the object according to the  `objectId` you specified, you will receive an empty object (`200 OK`）:

```json
{}
```

Some built-in classes (class names with leading underscore) may return different result when object does not exist.
For example:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  https://{{host}}/1.1/classes/_User/<NonexistObjectId>
```

will return:

```json
{
  "code": 211,
  "error": "Could not find user."
}
```

BTW, we recommend using `GET /users/<objectId>` to fetch user information, instead of directly querying the `_User` class.
See also [Retrieving Users](#Retrieving_Users).

### Updating Objects

To update an object, you can send a PUT request to the object URL.
LeanCloud will only update attributes you explicitly specified in the request (except for `updatedAt`).
For example, just update the content of a post:


```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"content": "Serverless cloud for lightning-fast development. https://leancloud.app"}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

If update succeed, `updatedAt` will be returned:

```json
{
  "updatedAt": "2015-06-30T18:02:52.248Z"
}
```

You can also pass the `fetchWhenSave` parameter,
which will return all updated attributes.

#### Counter

LeanCloud provides an `Increment` atomic operator to increase a counter like attribute.

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"upvotes":{"__op":"Increment","amount":1}}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

There is also an `Decrement` operator.
`Decrement` a positive number is equivalent to `Increment` a negative number.

#### Bitwise Operators

LeanCloud provides three bitwise operators for integers:

* `BitAnd`: bitwise `and`
* `BitOr`: bitwise `or`
* `BitXor`: bitwise `xor`

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"flags":{"__op":"BitOr","value": 0x0000000000000004}}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

#### Arrays

LeanCloud provides three atomic operators for arrays:

* `Add` extends an array attribute by appending elements from the given array.
* `AddUnique` is similar to `Add`, but only appending elements not already contained in the array attribute.
* `Remove` removes all occurrences of elements specified in the given array.

The given array mentioned above is passed in as the value of the `objects` key.

For example, to add some tags to the post:

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"tags":{"__op":"AddUnique","objects":["Frontend","JavaScript"]}}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

#### Conditional Updates

Suppose we are going to deduct some money from an `Account`, and we want to make sure this deduction will not result in a negative balance.
Then we can use conditional updates.

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"balance":{"__op":"Decrement","amount": 30}}' \
  "https://{{host}}/1.1/classes/Account/558e20cbe4b060308e3eb36c?where=%7B%22balance%22%3A%7B%22%24gte%22%3A%2030%7D%7D"
```

Here `%7B%22balance%22%3A%7B%22%24gte%22%3A%2030%7D%7D` is the URL-encoded condition `{"balance":{"$gte": 30}}`.
Refer to [Queries](#Queries) for more examples.

If the condition is not met, the update will not be performed, and you will receive an `305` error:

```json
{
  "code" : 305,
  "error": "No effect on updating/deleting a document."
}
```

**Note: `where` must be passed in as the query parameter of URL.**

### Deleting Objects

To delete an object, send a `DELETE` request:

```sh
curl -X DELETE \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  https://{{host}}/1.1/classes/Post/<objectId>
```

To delete an attribute from an object, send a `PUT` request with the `Delete` operator:

```sh
curl -X PUT \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{"downvotes":{"__op":"Delete"}}' \
  https://{{host}}/1.1/classes/Post/<objectId>
```

#### Conditional Delete

Similar to conditional updates, we pass an URL-encoded `where` parameter to the `DELETE` request.

```sh
curl -X DELETE \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  "https://{{host}}/1.1/classes/Post/<objectId>?where=%7B%22clicks%22%3A%200%7D" # {"clicks": 0}
```

Again, if the condition is not met, the update will not be performed, and you will receive an `305` error: 

```json
{
  "code" : 305,
  "error": "No effect on updating/deleting a document."
}
```

### Iterate over Objects

For classes with moderate amount of objects, we can iterate over all objects in the class via queries (with `skip` and `limit`).
However, for classes with large amount of objects, `skip` is inefficient.
Thus LeanCloud provides an `scan` endpoint to iterate over objects of a class efficiently.
By default `scan` returns 100 results in ascending order by `objectId`.
You can ask LeanCloud to return up to 1000 results via specifying the `limit` parameter.

```sh
curl -X GET \
   -H "X-LC-Id: {{appid}}" \
   -H "X-LC-Key: {{masterkey}},master" \ # requires master key
   -G \
   --data-urlencode 'limit=10' \
   https://{{host}}/1.1/scan/classes/Article
```

LeanCloud will return an `results` array and a `cursor`.

```json
{
  "results":
   [
      {
        "tags"     :  ["clojure","\u7b97\u6cd5"],
        "createdAt":  "2016-07-07T08:54:13.250Z",
        "updatedAt":  "2016-07-07T08:54:50.268Z",
        "title"    :  "clojure persistent vector",
        "objectId" :  "577e18b50a2b580057469a5e"
       },
       ...
    ],
    "cursor": "pQRhIrac3AEpLzCA"}
```

The `cursor` will be `null` if there are no more results.
When `cursor` is not `null`, you can pass the `cursor` value to continue the iteration:

```sh
curl -X GET \
   -H "X-LC-Id: {{appid}}" \
   -H "X-LC-Key: {{masterkey}},master" \
   -G \
   --data-urlencode 'limit=10' \
   --data-urlencode 'cursor=pQRhIrac3AEpLzCA' \
   https://{{host}}/1.1/scan/classes/Article
```

Each `cursor` must be consumed in 10 minutes.
After 10 minutes it becomes invalid.

You can also specify `where` conditions for filtering:

```sh
curl -X GET \
   -H "X-LC-Id: {{appid}}" \
   -H "X-LC-Key: {{masterkey}},master" \
   -G \
   --data-urlencode 'limit=10' \
   --data-urlencode 'where={"score": 100}' \
   https://{{host}}/1.1/scan/classes/Article
```

As mentioned above, by default the results are in ascending order by `objectId`.
To return results ordered by other attribute,
pass that attribute as the `scan_key` parameter.

```sh
curl -X GET \
   -H "X-LC-Id: {{appid}}" \
   -H "X-LC-Key: {{masterkey}},master" \
   -G \
   --data-urlencode 'limit=10' \
   --data-urlencode 'scan_key=score' \
   https://{{host}}/1.1/scan/classes/Article
```

To return results in descending order, prefix a minus sign (`-`) to the value of the `scan_key`, e.g. `-score`.

The value of the `scan_key` passed must be strictly monotonous, and it cannot be used in where conditions.

### Batch Operations

To reduce network interactions, you can wrap create, update, and delete operations on multiple objects in one request.

```sh
curl -X POST \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{
        "requests": [
          {
            "method": "POST",
            "path": "/1.1/classes/Post",
            "body": {
              "content": "Most Internet-based applications are data-driven and share a very similar architecture...",
              "pubUser": "LeanCloud"
            }
          },
          {
            "method": "POST",
            "path": "/1.1/classes/Post",
            "body": {
              "content": "LeanMessage is designed with the following goals:...",
              "pubUser": "LeanCloud"
            }
          }
        ]
      }' \
  https://{{host}}/1.1/batch
```

Currently there is no limit on wrapped requests number,
but LeanCloud has a 20 MB size limit on request body for all API requests.

The wrapped operations will be performed according to the order given in the `requests` array.
And the response body will also be an array,
with corresponding length and order.
Each member of the results array will be a JSON object with one and only one key, and that key will be either `success` or `error`.
The value of `success` or `error` will be the response to the corresponding single request on success or failure respectively.  

```
[
  {
    "error": {
      "code": 1,
      "error": "Could not find object by id '558e20cbe4b060308e3eb36c' for class 'Post'."
    }
  },
  {
    "success": {
      "updatedAt": "2017-02-22T06:35:29.419Z",
      "objectId": "58ad2e850ce463006b217888"
    }
  }
]
```

Be aware that the http status `200` returned by a batch request only means LeanCloud had received and performed the operations.
It does not mean all operations within the batch request succeeded.

Besides `POST` requests in the above example,
you can also wrap `PUT` and `DELETE` requests in a batch request:

```sh
curl -X POST \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -d '{
        "requests": [
          {
            "method": "PUT",
            "path": "/1.1/classes/Post/55a39634e4b0ed48f0c1845b",
            "body": {
              "upvotes": 2
            }
          },
          {
            "method": "DELETE",
            "path": "/1.1/classes/Post/55a39634e4b0ed48f0c1845c"
          }
        ]
      }' \
  https://{{host}}/1.1/batch
```

Batch requests can also be used to replaces requests with very long URLs (usually constructed via very complex queries or conditions), to bypass the limit on URL length enforced by service side or client side.

### Advanced Data Types

Besides standard JSON values, LeanCloud also supports advanced data types like Date and Files.
These advanced data types are encoded as a JSON object with a `__type` key.

**Date** contains an `iso` key, whose value is a UTC timestamp string in ISO 8601 format with millisecond precision `YYYY-MM-DDTHH:MM:SS.MMMZ`.


```json
{
  "__type": "Date",
  "iso": "2015-06-21T18:02:52.249Z"
}
```

As mentioned above, built-in date attributes `createdAt` and `updatedAt` are UTC timestamp strings, not enclosed in an JSON object.

**Byte** contains a `base64` key, whose value is a MIME base64 string (no whitespace characters).

```json
{
  "__type": "Bytes",
  "base64": "5b6I5aSa55So5oi36KGo56S65b6I5Zac5qyi5oiR5Lus55qE5paH5qGj6aOO5qC877yM5oiR5Lus5bey5bCGIExlYW5DbG91ZCDmiYDmnInmlofmoaPnmoQgTWFya2Rvd24g5qC85byP55qE5rqQ56CB5byA5pS+5Ye65p2l44CC"
}
```

**Pointer** contains a `className` key and an `objectId` key, whose values are the corresponding class name and objectId of the pointed value.

```json
{
  "__type": "Pointer",
  "className": "Post",
  "objectId": "55a39634e4b0ed48f0c1845c"
}
```

Pointers to users contains a `className` of `_User`.
The leading underscore indicates the `_User` class is built-in.
Similar, pointers to roles and installations contain a `className` of `_Role` or `_Installation` respectively.
However, a pointer to a file is special:

```json
{
  "id": "543cbaede4b07db196f50f3c",
  "__type": "File"
}
```

**GeoPoint** contains `latitude` and `longitude` of the location:

```json
{
  "__type": "GeoPoint",
  "latitude": 39.9,
  "longitude": 116.4
}
```

We may add more advanced data types in future, thus you should not use the `__type` on your own JSON objects.

## Queries

### Basic Queries

To list objects in a class, just send a GET request to the class URL:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  https://{{host}}/1.1/classes/Post
```

The response body is a JSON object containing a `results` key,
whose value is an array of objects:

```json
{
  "results": [
    {
      "content": "Most Internet-based applications are data-driven and share a very similar architecture...",
      "pubUser": "LeanCloud",
      "upvotes": 2,
      "createdAt": "2015-06-29T03:43:35.931Z",
      "objectId": "55a39634e4b0ed48f0c1845b"
    },
    {
      "content": "LeanMessage is designed with the following goals:...",
      "pubUser": "LeanCloud",
      "pubTimestamp": 1435541999,
      "createdAt": "2015-06-29T01:39:35.931Z",
      "updatedAt": "2015-06-29T01:39:35.931Z",
      "objectId": "558e20cbe4b060308e3eb36c"
    }
  ]
}
```

### Query Constraints

The `where` parameter applies query constraints.
It should be encoded as JSON first, then URL encoded.

The simplest form of `where` parameter is a key value pair (exact match).
For example, to query posts published by LeanCloud:


```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"pubUser":"LeanCloud"}' \
  https://{{host}}/1.1/classes/Post
```

Other operators available in the `where` parameter:

| Operator      | Description                           |
| ------------- | ------------------------------------- |
| `$ne`         | not equal to                          |
| `$lt`         | less than                             |
| `$lte`        | less than or equal to                 |
| `$gt`         | greater than                          |
| `$gte`        | greater than or equal to              |
| `$regex`      | match a regular expression            |
| `$in`         | contain                               |
| `$nin`        | not contain                           |
| `$all`        | contain all (for array type)          |
| `$exists`     | the given key exists                  |
| `$select`     | match the result of another query     |
| `$dontSelect` | not match the result of another query |

To query posts published on 2015-06-29 ：

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"createdAt":{"$gte":{"__type":"Date","iso":"2015-06-29T00:00:00.000Z"},"$lt":{"__type":"Date","iso":"2015-06-30T00:00:00.000Z"}}}' \
  https://{{host}}/1.1/classes/Post
```

Posts whose votes is an odd number less than 10:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"upvotes":{"$in":[1,3,5,7,9]}}' \
  https://{{host}}/1.1/classes/Post
```

Posts *not* published by LeanCloud:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"pubUser":{"$nin":["LeanCloud"]}}' \
  https://{{host}}/1.1/classes/Post
```

Posts have been voted by someone:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"upvotes":{"$exists":true}}' \
  https://{{host}}/1.1/classes/Post
```

Posts have not been voted:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"upvotes":{"$exists":false}}' \
  https://{{host}}/1.1/classes/Post
```

Suppose we use `_Followee` and `_Follower` classes for following relationship, then we can query posts published by someone followed by current user like this:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={
    "author": {
      "$select": {
        "query": {
          "className":"_Followee",
           "where": {
             "user":{
               "__type": "Pointer",
               "className": "_User",
               "objectId": "55a39634e4b0ed48f0c1845c"
             }
           }
        },
        "key":"followee"
      }
    }
  }' \
  https://{{host}}/1.1/classes/Post
```

Other parameters:

Parameter | Description
- | -
order | order by, prefix `-` for descending
limit | the number of returned objects, default 100, max 1000
skip | for pagination
keys | only return specified keys, prefix `-` for not including

To query posts ordered by creation time:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'order=createdAt' \ # ascending
  https://{{host}}/1.1/classes/Post

curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'order=-createdAt' \ # descending 
  https://{{host}}/1.1/classes/Post
```

To sort results by multiple keys, use a comma to separate them:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'order=createdAt,-pubUser' \
  https://{{host}}/1.1/classes/Post
```

An example of pagination:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'limit=200' \
  --data-urlencode 'skip=400' \
  https://{{host}}/1.1/classes/Post
```

If you only care about the content and author of posts:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'keys=pubUser,content' \
  https://{{host}}/1.1/classes/Post
```

Note that returned objects will always contain preserved attributes such as `objectId`, `createdAt`, and `updatedAt`.

If you do not care about post author:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'keys=-author' \
  https://{{host}}/1.1/classes/Post
```

The parameters mentioned above can be combined with each other.

### Regex Queries

To query posts whose title begins with `WTO`:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -H "Content-Type: application/json" \
  -G \
  --data-urlencode 'where={"title":{"$regex":"^WTO.*","$options":"i"}}' \
  https://{{host}}/1.1/classes/Post
```

The above example specifies `i` in `options`.
Thus it is a case-insensitive search.

Available options (flags):

Options | Description | Notes
- | - | -
`i` | case-insensitive search | same as in JavaScript 
`m` | multi-line search | same as in JavaScript
`s` | allow `.` to match newline characters | added in ES2018
`x` | free-spacing and line comments | same as in Perl

Options can be combined, for example `"$options":"sixm"`.

### Array Queries

Queries on keys with an array type overloads some operators mentioned above:

Operators | Example | k is not an array | k is an array
- | - | - | -
n/a | `where={"k":2}` | `k == 2` | `k` contains 2
`in` | `where={"k":{"$in":[2,3]}}` | `k` is 2 or 3 | `k` contains 2 or 3
`all` | `where={"arrayKey":{"$all":[2,3]}}` | n/a | `k` contains 2 and 3

### Pointer Queries

To query a Pointer type attribute:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'where={"post":{"__type":"Pointer","className":"Post","objectId":"558e20cbe4b060308e3eb36c"}}' \
  https://{{host}}/1.1/classes/Comment
```

To query objects with pointers according to another query on the pointed object, you can use the `$inQuery` operator.

For example, to query comments on posts with attached images:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'where={"post":{"$inQuery":{"where":{"image":{"$exists":true}},"className":"Post"}}}' \
  https://{{host}}/1.1/classes/Comment
```

Be aware that the `limit` parameter (default 100, max 1000) also applies to inner queries.
Thus you may need to deliberately construct queries to get expected result.
Refer to [Caveats about Inner Queries](leanstorage_guide-js.html#Caveats_about_Inner_Queries) for more details.

To include pointed objects in one query, use `include` parameter.
For example, to query most recent 10 comments with the posts commented on:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'order=-createdAt' \
  --data-urlencode 'limit=10' \
  --data-urlencode 'include=post' \
  https://{{host}}/1.1/classes/Comment
```

Without the `include` parameter, the post attribute of returned comments will look like this:

```json
{
  "__type": "Pointer",
  "className": "Post",
  "objectId": "51e3a359e4b015ead4d95ddc"
}
```

With the `include=post` parameter, the post attribute will be dereferenced:

```json
{
  "__type": "Object",
  "className": "Post",
  "objectId": "51e3a359e4b015ead4d95ddc",
  "createdAt": "2015-06-29T09:31:20.371Z",
  "updatedAt": "2015-06-29T09:31:20.371Z",
  "content": "this is a post",
  "author": "LeanCloud"
}
```

You can use dot (`.`) for multi-level dereference:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'order=-createdAt' \
  --data-urlencode 'limit=10' \
  --data-urlencode 'include=post.author' \
  https://{{host}}/1.1/classes/Comment
```

And you can use comma (`,`) to separate multiple pointers to `include`.

### Counting Results

You can pass `count=1` parameter to retrieve the count of matched results.
For example, if you just need to know a specific user have posted how many posts:

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'where={"pubUser":"LeanCloud"}' \
  --data-urlencode 'count=1' \
  --data-urlencode 'limit=0' \
  https://{{host}}/1.1/classes/Post
```

Since `limit=0`, LeanCloud will only return the count, and the results array will be empty.

```json
{
  "results": [],
  "count": 7
}
```

Given a nonzero `limit` parameter, LeanCloud will also return results together with the count.

### Compound Queries

You can use `$or` operator to query objects matching any one of several queries.

```sh
curl -X GET \
  -H "X-LC-Id: {{appid}}" \
  -H "X-LC-Key: {{appkey}}" \
  -G \
  --data-urlencode 'where={"$or":[{"priority":{"$gt":2}},{"isComplete":true}]}' \
  https://{{host}}/1.1/classes/Todo
```

Similarly, you can use `$and` operator to query objects matching all subqueries.

```
--data-urlencode 'where={"$and":[{"price": {"$ne":0}},{"price":{"$exists":true}}]}' \
```

Be aware that non-filtering constrains such as `limit`, `skip`, `order`, `include` are not allowed in subqueries of a compound query.
