---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://userfront.com/signup'>Create a project</a>

includes:
  - errors

search: true
---

# Introduction

<aside class="notice">These docs are for using the Userfront API. See the <a href="https://userfront.com/guide" target="_blank">Guide</a> for general information and to set up Userfront.</aside>

You can use the Userfront API to programmatically read and manipulate user, tenant, and role records in your project.

# Authentication

> To authenticate, use your project's API key in the Authorization header:

```shell
# With shell, you can pass the correct header with each request
curl "https://api.userfront.com/v0/status"
  -H "Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q"
```

```javascript
axios({
  method: "GET",
  url: "https://api.userfront.com/v0/status",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
    "Content-Type": "application/json; charset=utf-8",
  },
});
```

> Make sure to replace `uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q` with your API key.

<!-- <a href="#" id="show-key">Show your API key</a> -->

Userfront uses API keys to allow your project access to the API. You can find Admin and Readonly API keys for your project in the Settings section of the Userfront [dashboard](https://userfront.com/projects).

Userfront expects the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q`

<aside class="notice">
Replace <code>uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q</code> with your API key.
</aside>

# Users

## Create a user

```shell
curl -X "POST" "https://api.userfront.com/v0/tenants/abcdefgh/users" \
     -H 'Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "email": "johnny@example.com",
          "username": "johnny1234",
          "name": "Johnny Appleseed",
          "image": "https://example.com/avatar.png",
          "locked": false
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/tenants/abcdefgh/users",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    email: "johnny@example.com",
    username: "johnny1234",
    name: "Johnny Appleseed",
    image: "https://example.com/avatar.png",
    locked: false,
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 4,
  "username": "johnny1234",
  "email": "johnny@example.com",
  "name": "Johnny Appleseed",
  "image": "https://example.com/avatar.png",
  "locked": false,
  "isDev": false,
  "isConfirmed": false,
  "lastActiveAt": null,
  "uuid": "2e6b8f41-eb6d-4deb-9d75-6159c4ac4397",
  "createdAt": "2020-10-12T23:23:17.930Z",
  "tenant": {
    "tenantId": "abcdefgh",
    "name": "Example project",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-03.png",
    "loginRedirectPath": "/dashboard",
    "logoutRedirectPath": "/login"
  },
  "authorization": {}
}
```

This endpoint will create a new user with the provided payload.

### HTTP Request

`POST https://api.userfront.com/v0/tenants/abcdefgh/users/`

### Body Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| email     | String  | The user's email address                 |
| username  | String  | The user's username                      |
| name      | String  | The user's first and last name           |
| image     | String  | A URL to the user's image or avatar      |
| locked    | Boolean | If the user's account should be disabled |

## Create or update a user

```shell
curl -X "POST" "https://api.userfront.com/v0/tenants/abcdefgh/users/createOrUpdate" \
     -H 'Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "userId": 4,
          "email": "updated-johnny@example.com",
          "username": "johnny1234-updated",
          "name": "Johnny Appleseed Updated",
          "image": "https://example.com/avatar-updated.png",
          "locked": true
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/tenants/abcdefgh/users/createOrUpdate",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    userId: 4,
    email: "updated-johnny@example.com",
    username: "johnny1234-updated",
    name: "Johnny Appleseed Updated",
    image: "https://example.com/avatar-updated.png",
    locked: true,
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 4,
  "username": "johnny1234-updated",
  "email": "updated-johnny@example.com",
  "name": "Johnny Appleseed Updated",
  "image": "https://example.com/avatar-updated.png",
  "locked": true,
  "isDev": false,
  "isConfirmed": false,
  "lastActiveAt": null,
  "uuid": "2e6b8f41-eb6d-4deb-9d75-6159c4ac4397",
  "createdAt": "2020-10-12T23:23:17.930Z",
  "tenant": {
    "tenantId": "abcdefgh",
    "name": "Example project",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-03.png",
    "loginRedirectPath": "/dashboard",
    "logoutRedirectPath": "/login"
  },
  "authorization": {}
}
```

This endpoint will update a user if their UUID is provided. If no UUID is provided or the user with provided UUID is not found, a new user will be created with the provided payload (as in `POST https://api.userfront.com/v0/tenants/abcdefgh/users/`).

### HTTP Request

`POST https://api.userfront.com/v0/tenants/abcdefgh/users/createOrUpdate`

### Body Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| userId    | String  | The userId of the user to update         |
| email     | String  | The user's email address                 |
| username  | String  | The user's username                      |
| name      | String  | The user's first and last name           |
| image     | String  | A URL to the user's image or avatar      |
| locked    | Boolean | If the user's account should be disabled |

## Create and invite a user

```shell
curl -X "POST" "https://api.userfront.com/v0/tenants/abcdefgh/users/invite" \
     -H 'Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "email": "mike@example.com",
          "username": "mike123",
          "name": "Mike Appleseed",
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/tenants/abcdefgh/users/invite",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    email: "mike@example.com",
    username: "mike123",
    name: "Mike Appleseed",
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 5,
  "username": "mike123",
  "email": "mike@example.com",
  "name": "Mike Appleseed",
  "image": "https://example.com/avatar.png",
  "locked": false,
  "isDev": false,
  "isConfirmed": false,
  "lastActiveAt": null,
  "uuid": "34e98163-e4c5-488b-86b6-009d315db0d2",
  "createdAt": "2020-10-12T23:35:42.791Z",
  "tenant": {
    "tenantId": "abcdefgh",
    "name": "Example project",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-03.png",
    "loginRedirectPath": "/dashboard",
    "logoutRedirectPath": "/login"
  },
  "authorization": {}
}
```

This endpoint will create a user and send the new user an invite email to the email provided in the payload.

### HTTP Request

`POST https://api.userfront.com/v0/tenants/abcdefgh/users/invite`

### Body Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| email     | String  | The user's email address                 |
| username  | String  | The user's username                      |
| name      | String  | The user's first and last name           |
| image     | String  | A URL to the user's image or avatar      |
| locked    | Boolean | If the user's account should be disabled |

## Fetch users

```shell
curl -X "POST" "https://api.userfront.com/v0/tenants/abcdefgh/users/find" \
     -H 'Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q' \
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/tenants/abcdefgh/users/find",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
  },
  data: {},
});
```

> The above request returns a JSON response:

```json
{
  "results": [
    {
      "userId": 5,
      "email": "mike@example.com",
      "username": "mike123",
      "name": "Mike Appleseed",
      "image": "https://example.com/avatar.png",
      "isConfirmed": false,
      "isDev": false,
      "locked": false,
      "uuid": "41a0cde9-750e-4d2d-aad1-4bf9f25a233c",
      "createdAt": "2020-03-02T23:32:56.120Z"
    },
    {
      "userId": 4,
      "email": "updated-johnny@example.com",
      "username": "johnny1234-updated",
      "name": "Johnny Appleseed Updated",
      "image": "https://example.com/avatar-updated.png",
      "isConfirmed": false,
      "isDev": false,
      "locked": true,
      "uuid": "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
      "createdAt": "2020-03-02T23:06:23.603Z"
    }
    // ...more users
  ],
  "totalCount": 5,
  "meta": {
    "count": 5,
    "totalCount": 5,
    "totalPages": 5,
    "next": "/users/find",
    "previous": "/users/find",
    "self": "/users/find",
    "first": "/users/find",
    "last": "/users/find"
  }
}
```

This endpoint will find users in your project based on the query parameters provided. All of the user attributes are available to query against and order on.

### HTTP Request

`POST https://api.userfront.com/v0/tenants/abcdefgh/users/find`

### Query Parameters

| Parameter | Type   | Description                                                                                                                          |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| where     | JSON   | A [Sequelize-style](https://sequelize.org/v5/manual/querying.html#where) query e.g. where="{\"name\":{\"\$iLike\":\"%appleseed%\"}}" |
| order     | String | How results should be returned with attribute_ORDER format e.g. order=lastActiveAt_ASC OR order=username_DESC                        |
| page      | String | The page of results to be returned e.g. page=3                                                                                       |

## Record a user's activity

```shell
curl -X "PUT" "https://api.userfront.com/v0/tenants/abcdefgh/users/2/active" \
     -H 'Authorization: Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q' \
```

```javascript
axios({
  method: "PUT",
  url: "https://api.userfront.com/v0/tenants/abcdefgh/users/2/active",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdefgh_1z2x3y4w5v6u7t8s9r0q",
  },
  data: {},
});
```

> The above request returns a JSON response:

```json
{ "message": "ok", "lastActiveAt": "2020-03-03T00:21:10.323Z" }
```

This endpoint is used to record a user's activity, which will then show in project analytics like Cohort Analysis and Calendar Heatmaps.

Each request will also update the user's `lastActiveAt` property to the time the request is made.

### HTTP Request

`PUT https://api.userfront.com/v0/tenants/abcdefgh/users/:userId/active`

### URL Parameters

| Parameter | Type    | Description                  |
| --------- | ------- | ---------------------------- |
| userId    | Integer | The ID of the user to update |
