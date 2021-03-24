# Web Push

"function"===typeof importScripts&&importScripts("https://api.useinsider.com/sw.js");

## 測試頁面

https://business.botsnova.com/labs/web_push/firebase/cloud_messaging

## 安裝注意事項

* manifest.json

```
gcm_sender_id設定值
```

* 安裝Botsnova Web Push SDK

```
https://<HTTP_HOST>/local_assets/sdk/web_push/botsnova_web_push.js
```

## Tokens

**Chrome**

djEv17Lu2L5SEFHti4Npb7:APA91bESDmaRAUyQ8DIo7yrBkmvZDVhd7GZA0peuBef66DR9XR-JGFsdn6u0msYFai1AcnWu88R7Jq_cpi1pinPHvOlsIJU_B2_bszq2YDguQml3DesRQjIsJzBX_QvhUO-2YLxGocZR

**Edge**

f5TMMJdDkYDRXRZNOhsy8o:APA91bGbKFOZaV397ptjGpIhTRvYH2By5vpib2ibRyBigTXnChXJwYaIzbVlUtaAC4IX7wdD9GYjoc_je36GOER8waAiZwIOtlB9H_IIuaJ5QktwiAgjnzJa3JsWMZwKDMyy1Fi2iXMY

**Firefox**

cbWFqmjYP4nXCcG8nq-_YC:APA91bHBdYHC4X3KA8gUIzgsC5H3th0GhV3FdqrmF3RBC0GmZ76d_OGBch8RD_aU8bNqN3ApMBewBz-sQ8pNts4KsLs5oxxEVPi5RKtaSCQwujXKOWDxAxKuR6z9bGgUrxGZx06k__7e

## 安裝

```
記得不要與"google/cloud"並存

# sudo composer.phar require google/apiclient
```

# OAuth 2.0 Client IDs

GCP Console > APIs & Services 

[Botsnova for Messenger](https://console.cloud.google.com/apis/credentials/oauthclient/3841792761-sssgkajjkdrqp1sa9cqcnnganhqh20ar.apps.googleusercontent.com?project=deus-shopify-messenger-app)

**Client Id** 

3841792761-sssgkajjkdrqp1sa9cqcnnganhqh20ar.apps.googleusercontent.com

**Client secret** 

f6kNyp3ud1XuNcLj9pxIsHFs

# Service Account

**要在Firebase管理後台生成**

Project Overview > Project settings > Service Accounts

```
目前Botsnova for Business使用的Firebase service account

firebase-adminsdk-0f3d1@deus-shopify-messenger-app.iam.gserviceaccount.com
```

# REST Resource: projects.messages

[API](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages)

### [Legacy Firebase Cloud Messaging HTTP protocol](https://firebase.google.com/docs/cloud-messaging/http-server-ref)

**API endpoint**

https://fcm.googleapis.com/fcm/send

```
curl --location --request POST 'https://fcm.googleapis.com/fcm/send' \
--header 'Authorization: key=AAAAAOT9Gvk:APA91bHXVitP1g5tHl37kzc3tY58zaxRy6mgfOmfZ5ScZ0RC8EEdROz1-9u9w4hUnIKrWw4-PKFDkU1fiSNsibD8UXY3yhNBHcXLONTHZSY3e-H-YfGLoNo5Hgh1xTjF2tJfhCsUz9gJ' \
--header 'Content-Type: application/json' \
--data-raw '{
    "notification": {
        "title": "Test message from Botsnova #002",
        "text": "Test message from Botsnova #002",
        "click_action": "OPEN_ACTIVITY_1" 
    },
    "data": {
        "keyname": "any value " 
    },
    "to": "djEv17Lu2L5SEFHti4Npb7:APA91bESDmaRAUyQ8DIo7yrBkmvZDVhd7GZA0peuBef66DR9XR-JGFsdn6u0msYFai1AcnWu88R7Jq_cpi1pinPHvOlsIJU_B2_bszq2YDguQml3DesRQjIsJzBX_QvhUO-2YLxGocZR"
}'
```

# [Migrate from legacy HTTP to HTTP v1](https://firebase.google.com/docs/cloud-messaging/migrate-v1)

## 使用PHP SDK

```
use Google_Service_FirebaseCloudMessaging_SendMessageRequest;
use Google_Service_FirebaseCloudMessaging_Message;
use Google_Service_FirebaseCloudMessaging_Notification;
use Google_Service_FirebaseCloudMessaging_WebpushConfig;
use Google_Service_FirebaseCloudMessaging_WebpushFcmOptions;

$client = new \Google_Client();
$client->setAuthConfig("{$_SERVER['DOCUMENT_ROOT']}/YouMeb/src/YouMeb/Module/GCP/Firebase/v1/Admin/ServiceAccount/deus-shopify-messenger-app-firebase-adminsdk-0f3d1-a92424f60f.json");
$client->addScope(\Google_Service_FirebaseCloudMessaging::CLOUD_PLATFORM);
$client->setAccessType('offline');
$client->useApplicationDefaultCredentials();

$fcm = new \Google_Service_FirebaseCloudMessaging($client);

```

# 單元測試

[Using OAuth 2.0 for Web Server Applications](https://developers.google.com/identity/protocols/oauth2/web-server)

## 測試取得OAuth URL

```
# phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testGenerateOAuthUrl ./YouMeb/tests/Module/GCP/OAuth/v1/Service/OAuthServiceTest.php
```

## Exchange authorization code for refresh and access tokens(Google SDK)

```
phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testFetchAccessTokenWithAuthCodeByUsingSDK ./YouMeb/tests/Module/GCP/OAuth/v1/Service/OAuthServiceTest.php
```

## Refreshing expired access token by using refresh token(Google SDK)

```
phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testFetchAccessTokenWithRefreshTokenByUsingSDK ./YouMeb/tests/Module/GCP/OAuth/v1/Service/OAuthServiceTest.php
```

## Exchange authorization code for refresh and access tokens(HTTP/REST)

```
phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testFetchAccessTokenWithAuthCodeByUsingRESTfulAPI ./YouMeb/tests/Module/GCP/OAuth/v1/Service/OAuthServiceTest.php
```

## Refreshing expired access token by using refresh token(HTTP/REST)

```
phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testFetchAccessTokenWithRefreshTokenByUsingRESTfulAPI ./YouMeb/tests/Module/GCP/OAuth/v1/Service/OAuthServiceTest.php
```

## 發送測試Web Push

```
# phpunit --verbose --debug --bootstrap ./YouMeb/tests/bootstrap.php --filter testSendMessage ./YouMeb/tests/Module/GCP/FirebaseCloudMessaging/v1/Admin/Service/FirebaseCloudMessagingServiceTest.php
```

# 管理訂閱者

## 儲存訂閱戶

AWS Lambda

[demo-rds](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions/demo-rds?tab=code)

AWS API Gateway

```
POST https://360ay850qi.execute-api.us-west-2.amazonaws.com/dev/web-push/subscribers
```

## AWS API Gateway相關設定

[Enabling CORS for a REST API resource](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html)

[Enable CORS on a resource using the API Gateway console](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors-console.html)