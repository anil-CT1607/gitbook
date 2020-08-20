# GST File Upload API Reference

## Introduction

The File Upload API gives you the ability to upload your documents to ClearTax GST with staged validation checks. 

### Types of documents supported

With this API, you will be able to upload following types of documents from your local file system in CSV or Excel format:

1. Sales Invoices or Outward Bills of Supply
2. Purchase Invoices or Inward Bills of Supply
3. Advance Receipts
4. Advance Payments
5. Outward Credit Debit Notes
6. Inward Credit Debit Notes

### Why File Upload API?

Using this API gets your documents staged in ClearTax database, removing the overhead of correcting validation errors at the time of sending the documents. This lets business user send documents faster and in more efficient manner. Once a file containing documents is uploaded, the File Upload API will return an `activity_id` that can be used for future requests to check upload status and validation errors.

### Steps to upload a document

File Upload API is a set of requests that allow you to upload documents to ClearTax GST in CSV or Excel format in 3 easy steps:

1. Upload the file with a POST request.
2. Once uploaded, these files will be processed asynchronously and you can get the processing status with a subsequent GET request.
3. Once the processing status is changed to `PROCESSED`, you can get the validation details with a subsequent GET request.

{% hint style="info" %}
All requests require the user authentication token in the request headers. To learn more about how to generate user authentication token, click the below link.
{% endhint %}

{% page-ref page="../getting-started-with-gst-api/how-to-authenticate-api-requests.md" %}

## Uploading a document

The request for uploading a document is slightly different for ClearTax template and Government template. In case of ClearTax Template, you will need to send `custom_mapper_id` whereas in case of Government Template, you will need to send `vendor_type`.

### Uploading a document in ClearTax Template

The file containing documents in ClearTax Template, e-commerce template or custom template is sent by submitting a **POST** request to the Upload File API with the following request headers.

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
Content-Type: multipart/form-data
Accept: application/json
```

URL query string:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/transactions/upload?data_type={{DATA_TYPE}}&custom_mapper_id={{CUSTOM_MAPPER_ID}}
```

Request Parameters:

| Parameter | Parameter type | Type | Description |
| :--- | :--- | :--- | :--- |
| custom\_mapper\_id | Query | String | Required. Cannot be sent with `vendor_type`. For supported types and more information, see below. |
| data\_type | Query | String | Required. This is the identifier for the base document type. For supported types and more information, see below. |
| delimiter | Query | String | Optional. This is the character that separates values. Defaults to `,` \(comma\). |
| excelFile | formData | File | Required. This is the file in CSV or Excel format. In case of Excel, only the first sheet will be processed. |
| return\_period | Query | String | Required. This is the return period of the documents in the file. Format MMYYYY. Eg: 082018 for August 2018 |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |

Supported values for parameters:

| Template name | data\_type | custom\_mapper\_id |
| :--- | :--- | :--- |
| Sales Invoice and Outward Bill of Supply | GSTR1\_INVOICE | 9b34f966-d78d-40a1-90c2-6acb1e1fcf42 |
| Outward Credit Debit Note | GSTR1\_CDN | 44271028-4b8f-4228-9f99-9398ea5680ae |
| Advance Receipts | GSTR1\_ADVANCE\_PAYMENT | 62f6f212-9d5e-44b4-8a7f-35ab0b765f38 |
| Purchase Invoice and Inward Bill of Supply | GSTR2\_PURCHASE\_INVOICE | d541c80e-906e-49ed-9ee2-46c1d5497c4b |
| Inward Credit Debit Note | GSTR2\_CDN | db48eb86-4e80-4814-894b-efe721ca789c |
| Advance Payments | GSTR2\_ADVANCE\_PAYMENT | fd2e71b9-94cc-48fb-a772-7a81fea46f27 |

Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/a4d61a08-64d8-404d-b375-14d8c466771e/transactions/upload?data_type=GSTR2_PURCHASE_INVOICE&custom_mapper_id=d541c80e-906e-49ed-9ee2-46c1d5497c4b&return_period=012019
```

Sample Response:

```text
{
    "activity_id": "a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5",
    "error_response": null,
    "group_id": null,
    "other_activity_ids": null,
    "status": "UPLOADED",
    "queued_count": 1
}
```

### Uploading a document in Government Template

The file containing documents in Government template is sent by submitting a **POST** request to the Upload File API with the following request headers.

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
Content-Type: multipart/form-data
Accept: application/json
```

URL query string for Government template:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/transactions/upload?data_type={{DATA_TYPE}}&vendor_type={{VENDOR_TYPE}}
```

Request Parameters:

| Parameter | Parameter type | Type | Description |
| :--- | :--- | :--- | :--- |
| data\_type | Query | String | Required. This is the identifier for the base document type. For supported types and more information, see below. |
| delimiter | Query | String | Optional. This is the character that separates values. Defaults to `,` \(comma\). |
| excelFile | formData | File | Required. This is the file in CSV or Excel format. In case of Excel, only the first sheet will be processed. |
| return\_period | Query | String | Required. This is the return period of the documents in the file. Format MMYYYY. Eg: 082018 for August 2018 |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| vendor\_type | Query | String | Required. Cannot be sent with `custom_mapper_id`. For supported types and more information, see below. |

Supported values for parameters:

| Return | Sheet | data\_type | vendor\_type |
| :--- | :--- | :--- | :--- |
| GSTR1 | B2B |  GSTR1\_INVOICE | GOVT\_GSTR1\_B2B\_V1\_2 |
| GSTR1 | B2CL | GSTR1\_INVOICE | GOVT\_GSTR1\_B2CL\_V1\_2 |
| GSTR1 | B2CS | GSTR1\_B2CS\_AGG | GOVT\_GSTR1\_B2CS\_V1\_2 |
| GSTR1 | EXP | GSTR1\_INVOICE | GOVT\_GSTR1\_EXP\_V1\_2 |
| GSTR1 | CDNR | GSTR1\_CDN | GOVT\_GSTR1\_CDNR\_V1\_2 |
| GSTR1 | CDNUR | GSTR1\_CDN | GOVT\_GSTR1\_CDNUR\_V1\_2 |
| GSTR1 | AT | GSTR1\_ADVANCE\_AGG | GOVT\_GSTR1\_AT\_V1\_2 |
| GSTR1 | ATADJ | GSTR1\_ADVANCE\_ADJ\_AGG | GOVT\_GSTR1\_ATADJ\_V1\_2 |
| GSTR1 | EXEMP | GSTR1\_EXEMPTION\_AGG | GOVT\_GSTR1\_EXEMP\_V1\_2 |
| GSTR1 | HSN | GSTR1\_HSN\_AGG | GOVT\_GSTR1\_HSN\_V1\_2 |
| GSTR1 | DOC | GSTR1\_DOCS\_AGG | GOVT\_GSTR1\_DOCS\_V1\_2 |
| GSTR2 | B2B | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR2\_B2B\_V1\_0 |
| GSTR2 | B2CL | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR2\_B2BUR\_V1\_0 |
| GSTR2 | IMPS | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR2\_IMPS\_V1\_0 |
| GSTR2 | IMPG | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR2\_IMPG\_V1\_0 |
| GSTR2 | CDNR | GSTR2\_CDN | GOVT\_GSTR2\_CDNR\_V1\_0 |
| GSTR2 | CDNUR | GSTR2\_CDN | GOVT\_GSTR2\_CDNUR\_V1\_0 |
| GSTR2 | AT | GSTR2\_ADVANCE\_AGG | GOVT\_GSTR2\_AT\_V1\_0 |
| GSTR2 | ATADJ | GSTR2\_ADVANCE\_ADJ\_AGG | GOVT\_GSTR2\_ATADJ\_V1\_0 |
| GSTR2 | HSN | GSTR2\_HSN\_AGG | GOVT\_GSTR2\_HSNSUM\_V1\_0 |
| GSTR2 | EXEMP | GSTR2\_EXEMPTION\_AGG | GOVT\_GSTR2\_EXEMP\_V1\_0 |
| GSTR2 | ITCR | GSTR2\_ITCR\_AGG | GOVT\_GSTR2\_ITCR\_V1\_0 |
| GSTR3B | GSTR-3B | GSTR3B\_GOVT |  |
| GSTR4 | 4B\(B2B\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_B2B\_V1\_0 |
| GSTR4 | 4C\(B2BUR\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_B2BUR\_V1\_0 |
| GSTR4 | 4D\(IMPS\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_IMPS\_V1\_0 |
| GSTR4 | 5B\(CDNR\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_CDNR\_V1\_0 |
| GSTR4 | 5B\(CDNUR\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_CDNUR\_V1\_0 |
| GSTR4 | 6\(TXOS\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_TXOS\_V1\_0 |
| GSTR4 | 8A\(AT\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_AT\_V1\_0 |
| GSTR4 | 8B\(ATADJ\) | GSTR2\_PURCHASE\_INVOICE | GOVT\_GSTR4\_ATADJ\_V1\_0 |

Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/a4d61a08-64d8-404d-b375-14d8c466771e/transactions/upload?data_type=GSTR1_INVOICE&vendor_type=GOVT_GSTR1_B2B_V1_2
```

Sample Response:

{% code title="200" %}
```text
{
    "activity_id": "a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5",
    "error_response": null,
    "group_id": null,
    "other_activity_ids": null,
    "status": "UPLOADED",
    "queued_count": 1
}
```
{% endcode %}

## Getting upload status

You can get the status of an upload activity by submitting a **GET** request to the Upload File API with following request headers.

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
```

URL query string:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/upload_activity/{{ACTIVITY_ID}}/status
```

Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| activity\_id | Path | String | Required. This is the activity ID received in response to the Upload API. |

Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/a4d61a08-64d8-404d-b375-14d8c466771e/upload_activity/a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5/status
```

Sample Response:

```text
{
    "activityId": "a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5",
    "status": "PROCESSED",
    "errorMessage": null,
    "queuedCount": 0,
    "hasHeaderError": false,
    "headerStatus": "SUCCESS"
}
```

In the response, `status` can be either QUEUED, PROCESSING, ABORTED or PROCESSED.

## Getting upload validation

If the upload activity status as seen above is PROCESSED, you can get the validation details of the upload activity by submitting a **GET** request to the Upload File API with following request headers.

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
```

URL query string:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/<TAXABLE_ENTITY_ID>/upload_activity/<ACTIVITY_ID>
```

Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| activity\_id | Path | String | Required. This is the activity ID received in response to the Upload API. |

Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/a4d61a08-64d8-404d-b375-14d8c466771e/upload_activity/a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5
```

Sample Response:

```text
{
    "activity_id": "a2fe6607-b9ed-4e5c-9c19-9fbd951c0cb5",
    "status": "PROCESSED",
    "total_rows_processed": 1,
    "valid_invoice_summary": {
        "totalInvoices": 1,
        "totalValue": null,
        "totalTax": null
    },
    "invalid_invoice_summary": {
        "totalInvoices": 0,
        "totalValue": null,
        "totalTax": null
    },
    "error_messages": [],
    "warning_messages": [],
    ...
}
```

{% hint style="info" %}
Only the response fields relevant for integration are mentioned above. Actual response will have other fields which may not be relevant here.
{% endhint %}

## Getting upload history

You can get the list of all upload activities by submitting a **GET** request to the Upload File API with following request headers.

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
```

URL query string:

```text
https://gst.cleartax.in/api/v0.1/business/{{BUSINESS_ID}}/upload_activity
```

Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the Business in your account. |

{% hint style="info" %}
For this particular endpoint, you need to use Business ID instead of Taxable Entity ID.
{% endhint %}

Sample Request:

```text
https://gst.cleartax.in/api/v0.1/business/4657-e4a629ee-056954c4f3fb0123-b104/upload_activity
```

Sample Response:

```text
[
​ ​ ​{
​ ​ ​ ​ ​"activity_id":​ ​Excel​ ​Upload​ ​Activity​ ​ID,
​ ​ ​ ​ ​"owner_taxable_entity_id":​ ​Taxable​ ​Entity​ ​ID,
​ ​ ​ ​ ​"owner_gstin":​ ​Taxable​ ​Entity​ ​GSTIN,​ ​for​ ​which​ ​file​ ​was​ ​uploaded,
​ ​ ​ ​ ​"owner_taxable_entity_name":​ ​Taxable​ ​Entity​ ​Name​ ​in​ ​Cleartax,
​ ​ ​ ​ ​"status":​ ​Status​ ​of​ ​the​ ​file​ ​(​QUEUED​,​PROCESSING​,​PROCESSED​,​ABORTED)​,
​ ​ ​ ​ ​"total_rows_processed":​ ​Number​ ​of​ ​rows​ ​processed,
​ ​ ​ ​ ​"valid_invoice_summary":​ ​{
​ ​ ​ ​ ​ ​ ​"totalInvoices":​ ​Number​ ​of​ ​valid​ ​invoices​ ​created,
​ ​ ​ ​ ​ ​ ​"totalValue":​ ​Total​ ​Invoice​ ​value​ ​of​ ​created​ ​invoices,
​ ​ ​ ​ ​ ​ ​"totalTax":​ ​Total​ ​tax​ ​value​ ​of​ ​created​ ​invoices,
​ ​ ​ ​ ​},
​ ​ ​ ​ ​​"invalid_invoice_summary":​ {
​ ​ ​ ​ ​ ​ ​"totalInvoices":​ ​Number​ ​of​ ​failed​ ​invoices
​ ​ ​ ​ ​},
​ ​ ​ ​ ​"upload_data_type":​ ​Type​ ​of​ ​data,
​ ​ ​ ​ ​"created_at":​ ​Activity​ ​created​ ​datetime,
​ ​ ​ ​ ​"excel_processing_exception":​ ​Reason​ ​for​ ​aborts,​ ​if​ ​unknown​ ​exception​ ​happens,
​ ​ ​ ​ ​"file_name":​ ​Attached​ ​file​ ​name​ ​for​ ​activity
​ ​ ​ ​},
...
]
```

{% hint style="info" %}
Only the response fields relevant for integration are mentioned above. Actual response will have other fields which may not be relevant here.
{% endhint %}

## Rate Limiting

Currently, there is no rate limit. You are requested to apply judicial discretion while using ClearTax APIs to ensure overall level of service on our API server for all users.

## Best Practices

1. Upload only 1 file at a time.
2. Space out multiple requests evenly to reduce load on our server.
3. Limit file size to 3 Mb to ensure faster processing and validation.
4. While there is practically no limitation on the number of rows or documents per file, for the purpose of optimization, we have a maximum limit of 5000 line items per document in a file.

