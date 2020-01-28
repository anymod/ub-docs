---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Userbaser! You can use the Userbaser API to get information and perform actions on various users in your project.

We have language bindings in Shell (Terminal), JavaScript, Ruby, and Python. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use your Project Token as a bearer token:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.userbaser.com/v0/status"
  -H "Authorization: Bearer ub_live_admin_abcdef_1234567890abcdefghijklmnopqrstuvwxyz"
```

```javascript
const userbaser = require("userbaser");

let api = userbaser.authorize("meowmeowmeow");
```

> Make sure to replace `ub_live_admin_...` with your Project Token.

<a href="#" id="show-token">Show your Project Token</a>

Userbaser uses API keys to allow access to the API. You can register a new Userbaser API key at our [developer portal](http://example.com/developers).

Userbaser expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer ub_live_admin_abcdef_1234567890abcdefghijklmnopqrstuvwxyz`

<aside class="notice">
You must replace <code>ub_live_admin_abcdef_1234567890abcdefghijklmnopqrstuvwxyz</code> with your Project Token.
</aside>

# Users

## Find Users

```shell
curl "https://api.userbaser.com/v0/users/find"
  -H "Authorization: Bearer ub_live_admin_abcdef_1234567890abcdefghijklmnopqrstuvwxyz"
```

```javascript
var request = require("request");

var payload = {
  json: true,
  uri: "https://api.userbaser.com/v0/users/find",
  body: {
    order: "createdAt_DESC",
    where: {
      name: { $iLike: "%Sample%" }
    },
    page: 1
  },
  headers: {
    authorization:
      "Bearer ub_live_admin_abcdef_1234567890abcdefghijklmnopqrstuvwxyz"
  }
};

request.post(payload, function(err, res, body) {
  if (err) return console.error(err);
  console.log(body);
});
```

> The above command returns JSON structured like this:

```json
{
  "results": [
    {
      "userId": 1,
      "uuid": "6ab6de7b-5990-4d97-88be-0c7a981aa92e",
      "email": "user@example.com",
      "username": "exampleuser",
      "name": "Sample User",
      "image": "https://res.cloudinary.com/component/image/upload/avatars/avatar-03.png",
      "authorization": "member",
      "locked": false,
      "createdAt": "2020-01-27T15:16:39.955Z",
      "confirmedAt": null,
      "lastActiveAt": "2020-01-28T16:30:45.948Z"
    }
    ...
  ],
  "meta": {
    "count": 24,
    "totalCount": 100,
    "totalPages": 5
  }
}
```

This endpoint finds users based on criteria in the request `body`. To retrieve all users, omit the `body` attribute.

### HTTP Request

`POST https://api.userbaser.com/v0/users/find`

### Body Parameters

| Parameter | Default             | Description                            |
| --------- | ------------------- | -------------------------------------- |
| order     | `lastActiveAt_DESC` | The order users should be returned in. |
| where     | `{}`                | A query object based on Sequelize.     |

<aside class="success">
Remember — finding users is fun
</aside>

## Get a Specific User

```shell
curl "http://example.com/api/users/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const userbaser = require("userbaser");

let api = userbaser.authorize("meowmeowmeow");
let max = api.users.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific user.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/users/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

## Delete a Specific User

```shell
curl "http://example.com/api/users/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const userbaser = require("userbaser");

let api = userbaser.authorize("meowmeowmeow");
let max = api.users.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific user.

### HTTP Request

`DELETE http://example.com/users/<ID>`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to delete |
