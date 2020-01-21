{% set deviceprofile_format = "`deviceProfile` 的值必须以字母开头，由大小写字母、数字和下划线组成的字符串，或为空值。" %}
{% import "views/_parts.html" as include %}

{{ include.setService('push') }}

# Push Notification Service Overview

Push notifications, it facilitates the developer to push messages or notifications to users. Keeping interactions with users will validly retain the customers and imporve the user experience. Leancloud integrates the  Android Push, iOS Push and Windows Phone Push into one service.

In addition to iOS, Android SDK, you can take advantage of [REST API](#Use_REST_API_Push Notifications) to push requests.

## Basic Concept

### Installation

{% if node=='qcloud' %}
Installation is the only mark to represent the device is permitted to receive Push. Installations are objects used to store subscription data for installations for subscribers. It matches table `_Installation` in  `LeanStorage`. It includes the following fields:
{% else %}
Installation is the only mark to represent the device is permitted to receive Push. Installations are objects used to store subscription data for installations for subscribers. It matches table `_Installation` in  [LeanStorage](/dashboard/data.html?appid={{appid}}). It includes the following fields:
{% endif %}

Parameters | OS | Description
---|---|---
badge|iOS| number field on top right side representing the pending updating apps or unread messages.
channels||array of the channels subscribed.
deviceProfile || When the app have multiple iOS installations or multiple Android hybrid push environment , device Profile is used to specify the current device certificate and environment name. The value have to align with the name in [Dashboard > Messaging > Settings] (/dashboard/messaging.html?appid={{appid}}#/message/push/conf) , otherwise the push will fail. Please refer to [iOS test and production certificate distinguish](#iOS test and production certificate distinguish) and [Android hybrid Push under multiple environments](#Android hybrid Push under multiple environments). </br></br>{{deviceprofile_format}}
deviceToke|iOS|mark for delivering messages to the APNs push networks.
ansTopic|iOS| based on this Token Authentication ush to set this field. iOS SDK will automatically read iOS app bundle ID as the apnsTopic. Although you have tomannually set them under the following circumstances: 1. iOS SDK version is earlier than v4.2.0 2. no use of iOS SDK (React Native) 3. topic different from bundle ID.
deviceType| | "ios", "android", or "wp" (Windows Phone)
ID|Windows Phone| only works on Microsoft devices.
installationId | Android | LeanCloud SDK generated identifier for each Android device
subscriptionUri |Windows Phone|MPNS (Microsoft Push Notification Service) Push channel
timeZone | |device timezone.

Add and manipulate the devices , please refer to the following SDK introduction and [REST API](#Use_rest_api_to_push).

### Notification

{% if node=='qcloud' %}
In  **Dashboard > Messaging > History** , a record represents one push notification. It includes the following field:
{% else %}
In [Dashboard > Messaging > History](/dashboard/messaging.html?appid={{appid}}#/message/push/list) , one record represents one push notification. It includes the following fields:
{% endif%}

Parameters | OS | Description
---|---|---
data| | push content, JSON object
invalidTokens|iOS|the returned [INVALID TOKEN](https://developer.apple.com/library/mac/technotes/tn2265/_index.html#//apple_ref/doc/uid/DTS40010376-CH1-TNTAG32) in this push from the APNS.**If the number is too large, check the certificate.**
prod|iOS|which environment certificate is used. **dev** represents development certificate, **prod** represents production certificate.
status| | status of the push, **in-queue** , **done** or **scheduled** represents waiting to be activated.
devices| | target devices number . The number is not the number successfully pushed. It is the number of devices valid for the query in `_Installation`. **Valid** means the target has `valid` filed in the `_Installation` table as true and updatedAt field within three months. Much Inactive users(Someone have already uninstall the apps) may include in the attempt. These users cannot receive the push.
successes | |quantity of successfully pushed devices. Success indicates that the target Android devices successfully receive the push. For iOS or Android devices using hybrid push, success means notifications are used to the Apple APNS or device matched push platform.
where| |query conditions in `_Installation` for this push, devices match the conditions will receive the messages.
errors| |error message in the push.

The Nature of the Push is to retrieve all the devices meet the query conditions in `_Installation` table. Then the messages are pushed to the targets. As `_Installation` is a fully configurable Key-Value Object, pushs under various complex conditions are achievable such as subscriptions, Geopoint push , specific user push.

When the field **devices** has a value of 0. It represents no target devices are retrieved under such query conditions. No devices will receive the push. A value larger than 0 represents qualified devices exist, but no devices are ensured to receive the push. It is reasonable to have **devices** larger than **successes** and the gap is larger when there are enormous inactive devices.

Turn the field `valid` into `false` in `_Installation` will disable receiving the push.

**warning** , we only retain the history for one week and the expired push history will get cleared. There is no relation between the expiry of the push and the history clearance. The targets will still receive the push nonetheless the push history are cleared. The expiry date on the push history refer to [Push notification](#Push notification).

{#TODO 


## iOS Push Notification

Refer to [iOS push guide](./ios_push_guide.html).

## Android Push Notification

Refer to [Android push guide](./android_push_guide.html).

## Android Mix Push



We designed an advanced push mechanism named [mix push] to lift up the push rate on some Android device with more restrictive background process management. 

The function is only available for Business Plan users, switch on the function in [Dashboard > Messaging > Push Notification > Settings > mix push](/dashboard/messaging.html?appid={{appid}}#/message/push/conf), switch on the mix push.

Attention, **Swtich on Push Notification** option can adjust at discretion without any adversity. When it is switched off, the next Android Push will work as the normal push via the LeanCloud owned channel to the client terminal. Nothing is changed but the push may get influenced by some background process management. However, the third party channel will get utilized if the mix push is switched on.

Refer to [Android mix push guide](./android_push_guide.html#Mix Push).

{# TODO

## 云引擎和 JavaScript 创建推送

请阅读 [JavaScript SDK 指南 &middot; Push 通知](./leanstorage_guide-js.html#Push_通知)。

}

## REST API Push Notification

