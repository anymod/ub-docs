---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Userbaser! You can use our API to access Usrbsr API endpoints, which can get information on various cats, users, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'userbaser'

api = Usrbsr::APIClient.authorize!('meowmeowmeow')
```

```python
import userbaser

api = userbaser.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const userbaser = require("userbaser");

let api = userbaser.authorize("meowmeowmeow");
```

> Make sure to replace `meowmeowmeow` with your API key.

Usrbsr uses API keys to allow access to the API. You can register a new Usrbsr API key at our [developer portal](http://example.com/developers).

Usrbsr expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Users

## Get All Users

```ruby
require 'userbaser'

api = Usrbsr::APIClient.authorize!('meowmeowmeow')
api.users.get
```

```python
import userbaser

api = userbaser.authorize('meowmeowmeow')
api.users.get()
```

```shell
curl "http://example.com/api/users"
  -H "Authorization: meowmeowmeow"
```

```javascript
const userbaser = require("userbaser");

let api = userbaser.authorize("meowmeowmeow");
let users = api.users.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all users.

### HTTP Request

`GET http://example.com/api/users`

### Query Parameters

| Parameter    | Default | Description                                                                    |
| ------------ | ------- | ------------------------------------------------------------------------------ |
| include_cats | false   | If set to true, the result will also include cats.                             |
| available    | true    | If set to false, the result will include users that have already been adopted. |

<aside class="success">
Remember — a happy user is an authenticated user!
</aside>

## Get a Specific User

```ruby
require 'userbaser'

api = Usrbsr::APIClient.authorize!('meowmeowmeow')
api.users.get(2)
```

```python
import userbaser

api = userbaser.authorize('meowmeowmeow')
api.users.get(2)
```

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

```ruby
require 'userbaser'

api = Usrbsr::APIClient.authorize!('meowmeowmeow')
api.users.delete(2)
```

```python
import userbaser

api = userbaser.authorize('meowmeowmeow')
api.users.delete(2)
```

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
