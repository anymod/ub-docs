---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://userfront.com/signup'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

<aside class="notice">These docs are for using the API. See the <a href="https://guide.userfront.com" target="_blank">Guide</a> for general information and to set up Userfront.</aside>

You can use the Userfront API to programmatically get information and perform actions on user records in your project.

# Authentication

> To authorize, use your Project Token as a bearer token:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.userfront.com/v0/status"
  -H "Authorization: Bearer uf_live_admin_abcdef_123456abcdef"
```

```javascript
axios({
  method: "GET",
  url: "https://api.userfront.com/v0/status",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
    "Content-Type": "application/json; charset=utf-8",
  },
});
```

> Make sure to replace `uf_live_admin_abcdef_123456abcdef` with your Project Token.

<!-- <a href="#" id="show-token">Show your Project Token</a> -->

Userfront uses API keys called "Project Tokens" to allow your project access to the API. You can find Admin and Readonly Project Tokens for your project in the Settings section of the Userfront [dashboard](https://userfront.com/projects).

Userfront expects the Project Token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer uf_live_admin_abcdef_123456abcdef`

<aside class="notice">
Replace <code>uf_live_admin_abcdef_123456abcdef</code> with your Project Token.
</aside>

# Users

## Create a user

```shell
curl -X "POST" "https://api.userfront.com/v0/users" \
     -H 'Authorization: Bearer uf_live_admin_abcdef_123456abcdef' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "email": "johnny@example.com",
          "username": "johnny1234",
          "name": "Johnny Appleseed",
          "image": "https://example.com/avatar.png",
          "authorization": "member",
          "locked": false
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/users",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    email: "johnny@example.com",
    username: "johnny1234",
    name: "Johnny Appleseed",
    image: "https://example.com/avatar.png",
    authorization: "member",
    locked: false,
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 1,
  "uuid": "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
  "username": "johnny1234",
  "email": "johnny@example.com",
  "name": "Johnny Appleseed",
  "image": "https://example.com/avatar.png",
  "authorization": "member",
  "locked": false,
  "isDev": false,
  "isConfirmed": false,
  "createdAt": "2020-03-02T23:06:23.603Z",
  "updatedAt": "2020-03-02T23:06:23.603Z",
  "project": {
    "eid": "n8bjpqb7",
    "name": "Acme Widgets Inc.",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-39.png",
    "liveLoginRedirectUrl": "/dashboard",
    "liveLogoutRedirectUrl": "/login"
  }
}
```

This endpoint will create a new user with the provided payload.

### HTTP Request

`POST https://api.userfront.com/v0/users/`

### Body Parameters

| Parameter     | Type    | Description                                                                                         |
| ------------- | ------- | --------------------------------------------------------------------------------------------------- |
| email         | String  | The user's email address                                                                            |
| username      | String  | The user's username                                                                                 |
| name          | String  | The user's first and last name                                                                      |
| image         | String  | A URL to the user's image or avatar                                                                 |
| authorization | String  | A custom string of your choice to denote user's access level e.g. 'member', 'admin', 'viewer', etc. |
| locked        | Boolean | If the user's account should be disabled by default                                                 |

## Create or update a user

```shell
curl -X "POST" "https://api.userfront.com/v0/users/createOrUpdate" \
     -H 'Authorization: Bearer uf_live_admin_abcdef_123456abcdef' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "uuid": "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
          "email": "updated-johnny@example.com",
          "username": "johnny1234-updated",
          "name": "Johnny Appleseed Updated",
          "image": "https://example.com/avatar-updated.png",
          "authorization": "admin",
          "locked": true
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/users/createOrUpdate",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    uuid: "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
    email: "updated-johnny@example.com",
    username: "johnny1234-updated",
    name: "Johnny Appleseed Updated",
    image: "https://example.com/avatar-updated.png",
    authorization: "admin",
    locked: true,
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 1,
  "uuid": "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
  "username": "johnny1234-updated",
  "email": "updated-johnny@example.com",
  "name": "Johnny Appleseed Updated",
  "image": "https://example.com/avatar-updated.png",
  "authorization": "admin",
  "locked": true,
  "isDev": false,
  "isConfirmed": false,
  "createdAt": "2020-03-02T23:06:23.603Z",
  "updatedAt": "2020-03-02T23:16:50.957Z",
  "project": {
    "eid": "n8bjpqb7",
    "name": "Acme Widgets Inc.",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-39.png",
    "liveLoginRedirectUrl": "/dashboard",
    "liveLogoutRedirectUrl": "/login"
  }
}
```

This endpoint will update a user if their UUID is provided. If no UUID is provided or the user with provided UUID is not found, a new user will be created with the provided payload (as in `POST https://api.userfront.com/v0/users/`).

### HTTP Request

`POST https://api.userfront.com/v0/users/createOrUpdate`

### Body Parameters

| Parameter     | Type    | Description                                                                                         |
| ------------- | ------- | --------------------------------------------------------------------------------------------------- |
| uuid          | String  | The UUID of the user to update                                                                      |
| email         | String  | The user's email address                                                                            |
| username      | String  | The user's username                                                                                 |
| name          | String  | The user's first and last name                                                                      |
| image         | String  | A URL to the user's image or avatar                                                                 |
| authorization | String  | A custom string of your choice to denote user's access level e.g. 'member', 'admin', 'viewer', etc. |
| locked        | Boolean | If the user's account should be disabled by default                                                 |

## Create and invite a user

```shell
curl -X "POST" "https://api.userfront.com/v0/users/invite" \
     -H 'Authorization: Bearer uf_live_admin_abcdef_123456abcdef' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
          "email": "mike@example.com",
          "username": "mike123",
          "locked": false,
          "authorization": "member",
          "name": "Mike Appleseed",
          "image": "https://example.com/avatar.png"
        }'
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/users/invite",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
    "Content-Type": "application/json; charset=utf-8",
  },
  data: {
    email: "mike@example.com",
    username: "mike123",
    locked: false,
    authorization: "member",
    name: "Mike Appleseed",
    image: "https://example.com/avatar.png",
  },
});
```

> The above request returns a JSON response:

```json
{
  "userId": 2,
  "uuid": "41a0cde9-750e-4d2d-aad1-4bf9f25a233c",
  "username": "mike123",
  "email": "mike@example.com",
  "name": "Mike Appleseed",
  "image": "https://example.com/avatar.png",
  "authorization": "member",
  "locked": false,
  "isDev": false,
  "isConfirmed": false,
  "createdAt": "2020-03-02T23:32:56.120Z",
  "updatedAt": "2020-03-02T23:32:56.120Z",
  "project": {
    "eid": "n8bjpqb7",
    "name": "Acme Widgets Inc.",
    "image": "https://res.cloudinary.com/component/image/upload/avatars/icon-39.png",
    "liveLoginRedirectUrl": "/dashboard",
    "liveLogoutRedirectUrl": "/login"
  }
}
```

This endpoint will create a user and send the new user an invite email to the email provided in the payload.

### HTTP Request

`POST https://api.userfront.com/v0/users/invite`

### Body Parameters

| Parameter     | Type    | Description                                                                                         |
| ------------- | ------- | --------------------------------------------------------------------------------------------------- |
| email         | String  | The user's email address                                                                            |
| username      | String  | The user's username                                                                                 |
| name          | String  | The user's first and last name                                                                      |
| image         | String  | A URL to the user's image or avatar                                                                 |
| authorization | String  | A custom string of your choice to denote user's access level e.g. 'member', 'admin', 'viewer', etc. |
| locked        | Boolean | If the user's account should be disabled by default                                                 |

## Fetch users

```shell
curl -X "POST" "https://api.userfront.com/v0/users/find" \
     -H 'Authorization: Bearer uf_live_admin_abcdef_123456abcdef' \
```

```javascript
axios({
  method: "POST",
  url: "https://api.userfront.com/v0/users/find",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
  },
  data: {},
});
```

> The above request returns a JSON response:

```json
{
  "results": [
    {
      "userId": 2,
      "uuid": "41a0cde9-750e-4d2d-aad1-4bf9f25a233c",
      "email": "mike@example.com",
      "username": "mike123",
      "name": "Mike Appleseed",
      "image": "https://example.com/avatar.png",
      "isConfirmed": false,
      "isDev": false,
      "authorization": "member",
      "locked": false,
      "createdAt": "2020-03-02T23:32:56.120Z"
    },
    {
      "userId": 1,
      "uuid": "09fd26eb-5fe0-4a06-b595-8369aca1d2f8",
      "email": "updated-johnny@example.com",
      "username": "johnny1234-updated",
      "name": "Johnny Appleseed Updated",
      "image": "https://example.com/avatar-updated.png",
      "isConfirmed": false,
      "isDev": false,
      "authorization": "admin",
      "locked": true,
      "createdAt": "2020-03-02T23:06:23.603Z"
    }
    // ...more users
  ],
  "totalCount": 7,
  "meta": {
    "count": 7,
    "totalCount": 7,
    "totalPages": 7,
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

`POST https://api.userfront.com/v0/users/find`

### Query Parameters

| Parameter | Type   | Description                                                                                                                          |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| where     | JSON   | A [Sequelize-style](https://sequelize.org/v5/manual/querying.html#where) query e.g. where="{\"name\":{\"\$iLike\":\"%appleseed%\"}}" |
| order     | String | How results should be returned with attribute_ORDER format e.g. order=lastActiveAt_ASC OR order=username_DESC                        |
| page      | String | The page of results to be returned e.g. page=3                                                                                       |

## Record a user's activity

```shell
curl -X "PUT" "https://api.userfront.com/v0/users/2/active" \
     -H 'Authorization: Bearer uf_live_admin_abcdef_123456abcdef' \
```

```javascript
axios({
  method: "PUT",
  url: "https://api.userfront.com/v0/users/2/active",
  headers: {
    Authorization: "Bearer uf_live_admin_abcdef_123456abcdef",
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

`PUT https://api.userfront.com/v0/users/:userId/active`

### URL Parameters

| Parameter | Type    | Description                  |
| --------- | ------- | ---------------------------- |
| userId    | Integer | The ID of the user to update |
