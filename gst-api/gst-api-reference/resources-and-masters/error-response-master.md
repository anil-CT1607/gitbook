# GST Error Responses

ClearTax Error response will always tell you 2 things:

1. What is the error?
2. Where is the error?

You can get this error responce with different HTTP status code based on the API you are consuming. Example: You can get it with `400` Bad Request or with `200` OK

The `errors`object under `errorResponse`will always have the list of errors found in your payload. The `message` will explain what the error is and it's always paired with the `error_id`

![Error response](../../../.gitbook/assets/image%20%2825%29.png)

The `error_sources` object will direct you to the specific field in which the error was found.

![](../../../.gitbook/assets/image%20%2817%29.png)

