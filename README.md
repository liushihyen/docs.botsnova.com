# Audience API

**Creating**

You can make a POST request to audiences edge from the following paths:

```
POST https://<API_HOST>/v1/businesses/{business_id}/audiences
```

When posting to this edge, an Audience will be created.

| Parameter         | Type            | Required | Description                         |
| ------------------|:----------------| :--------| :-----------------------------------|
| name              | string          | no       | ex. LIU SHIH YEN                    |
| email             | string          | yes      | ex. service@deus.com.tw             |
| asid              | string          | no       | Facebook App-Scoped User Id         |
| psid              | string          | no       | Facebook Page-Scoped User Id        |
