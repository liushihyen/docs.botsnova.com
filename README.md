# Audience API

**Creating**

You can make a POST request to audiences edge from the following paths:

```
POST https://<API_HOST>/v1/businesses/{business_id}/audiences
```

When posting to this edge, an Audience will be created.

| Parameter         | Type            | Required | Description                         |
|:------------------|:----------------|:---------|:------------------------------------|
| external_user_id  | string          | no       | ex. CRM user id                     |
| name              | string          | no       | ex. LIU SHIH YEN                    |
| last_name         | string          | no       | ex. SHIH YEN                        |
| first_name        | string          | no       | ex. LIU                             |
| note              | string          | no       | A note about the audience.          |
| email             | string          | yes      | ex. service@deus.com.tw             |
| phone_number      | string          | no       | ex. +886952881344                   |
| picture           | string          | no       | User profile picture URL            |
| asid              | string          | no       | Facebook App-Scoped User Id         |
| psid              | string          | no       | Facebook Page-Scoped User Id        |
| line_user_id      | string          | no       | LINE user id                        |
| currency          | string          | no       | ex. USD                             |
| addresses         | JSON            | no       |                                     |
| default_address   | JSON            | no       |                                     |
