# Errors

The Userfront API uses the following error codes:

| Error Code | Meaning                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------- |
| 400        | **Bad Request** - The request is invalid.                                                    |
| 401        | **Unauthorized** - The API key is incorrect.                                                 |
| 403        | **Forbidden** - The route you requested is not allowed.                                      |
| 404        | **Not Found** - The user could not be found.                                                 |
| 429        | **Too Many Requests** - Too many requests in a short period. Please wait before re-trying.   |
| 500        | **Internal Server Error** - We had a problem with our server. Try again later.               |
| 503        | **Service Unavailable** - We're temporarily offline for maintenance. Please try again later. |
