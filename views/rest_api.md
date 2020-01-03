{% import "views/_helper.njk" as docs %}
{% import "views/_data.njk" as data %}
# REST API Guide

You can access LeanCloud from any devices supporting HTTP requests with REST API, for example:

- You can manipulate data on LeanCloud with any programming language.
- If you want to migrate from LeanCloud to other services, you can export all your data.
- Your mobile site can fetch data from LeanCloud via JavaScript directly if you think importing LeanCloud JavaScript SDK brings is overkill.
- You can add new data in batch, to be consumed by mobile applications later.
- You can export recent data for offline analysis or additional incremental backup.

## API Version

The current API version is `1.1`.

### Testing

This guide provides curl command line examples.
You may need to modify some syntax if using cmd.exe on Windows.
For example, `\` in curl examples means to be continued on next line, but cmd.exe will consider it as path seperator.
Therefore, we recommend you to use [Postman] for testing.

[Postman]: https://www.getpostman.com/

Postman can [import curl commands][import-curl] directly and automatically [generate code snippets][generate-snippets] in various languages and frameworks.

[import-curl]: https://learning.getpostman.com/docs/postman/collections/data-formats/#importing-curl
[generate-snippets]: https://learning.getpostman.com/docs/postman/sending-api-requests/generate-code-snippets/


Postman also supports 


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
      <td>delete an Object</td>
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
      <td>Push notifications</td>
    </tr>
    <tr>
      <td>/1.1/notifications</td>
      <td>GET</td>
      <td>Query push records</td>
    </tr>
    <tr>
      <td>/1.1/notifications/:notification_id</td>
      <td>GET</td>
      <td>Query a push record via ID</td>
    </tr>
    <tr>
      <td>/1.1/notifications/:notification_id</td>
      <td>DELETE</td>
      <td>Delete a push record</td>
    </tr>
    <tr>
      <td>/1.1/scheduledPushMessages</td>
      <td>GET</td>
      <td>Query all scheduled push notifications</td>
    </tr>
    <tr>
      <td>/1.1/scheduledPushMessages/:id</td>
      <td>DELETE</td>
      <td>Delete an scheduled push notification</td>
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
      <td>Upload installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>GET</td>
      <td>Retrieve installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>PUT</td>
      <td>Update installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations</td>
      <td>GET</td>
      <td>Query installation data</td>
    </tr>
    <tr>
      <td>/1.1/installations/&lt;objectId&gt;</td>
      <td>DELETE</td>
      <td>Delete installation data</td>
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
      <td>Retrieve all schemas</td>
    </tr>
    <tr>
      <td>/1.1/schemas/&lt;className&gt;</td>
      <td>POST</td>
      <td>Retrieve specified class schema</td>
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
      <td>Invoke a cloud function</td>
    </tr>
    <tr>
      <td>/1.1/call/&lt;functionName&gt;</td>
      <td>POST</td>
      <td>Call a cloud function with AVObjects as parameters and return values</td>
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
      <td>Retrieve chat history</td>
    </tr>
    <tr>
      <td>/1.1/rtm/messages</td>
      <td>POST</td>
      <td>Send a message</td>
    </tr>
    <tr>
      <td>/1.1/rtm/transient_group/onlines</td>
      <td>GET</td>
      <td>Count online members of a transient conversation</td>
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
      <td>Retrieve date and time at server side</td>
    </tr>
    <tr>
      <td>/1.1/exportData</td>
      <td>POST</td>
      <td>Request to export data</td>
    </tr>
    <tr>
      <td>/1.1/exportData/&lt;id&gt;</td>
      <td>GET</td>
      <td>Retrieve status and result of export data job</td>
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
| sign      | required   | concat timestamp and App Key (Master Key), then calculate its MD5 hash value |
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

