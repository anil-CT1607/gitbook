# How to upload an invoice from File?

ClearTax supports uploading of documents in different types of templates. For the purpose of this walk-through, let us upload a sales invoice in ClearTax template. Download a sample file from here.

## Upload a sales invoice

You can upload the sales invoice in ClearTax template by submitting a POST request to the URL query string:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/transactions/upload?data_type=<DATA_TYPE>&custom_mapper_id={{CUSTOM_MAPPER_ID}}&return_period={{RETURN_PERIOD}}
```

The request should have the following headers:

```text
x-cleartax-auth-token: <USER_AUTH_TOKEN>
Content-Type: multipart/form-data
Accept: application/json
```

{% hint style="info" %}
If you do not have a user authentication token, click here to learn how to generate an authentication token.
{% endhint %}

The body of the request is sent as form-data and requires the following properties:

`excelFile` - The location of the asset on your file system.

Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/e4a629ee-0569-4657-b104-54c4f3fb0123/transactions/upload?data_type=GSTR1_INVOICE&custom_mapper_id=9b34f966-d78d-40a1-90c2-6acb1e1fcf42&return_period=042018
```

Sample Response:

```text
{
    activity_id​: b104-e4a629ee-0569-54c4f3fb0123-4657,
    error_response​: {},
    group_id​: {},
    other_activity_ids​: {}
}
```

The activity\_id is the unique ID associated with this upload activity. To fetch the status or any details of the upload activity, you will have to send this ID along with consequent API calls.

For a complete list of File Upload API calls and request properties, see the File Upload API Reference.

{% page-ref page="../gst-api-reference/file-upload-api-reference.md" %}



