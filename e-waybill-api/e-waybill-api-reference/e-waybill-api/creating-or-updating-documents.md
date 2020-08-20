---
description: >-
  All files containing documents are sent by submitting a POST request to the
  Upload File API with the following request headers.
---

# Creating or Updating Documents

{% api-method method="post" host="https://ewb.cleartax.in/api" path="/v0.2/taxable\_entities/{taxable\_entity\_id}/transactions/upload" %}
{% api-method-summary %}
Upload Documents to ClearTax E-Waybill 
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to upload document on ClearTax E- Waybill portal.  
{taxable\_entity\_id} : taxable entity ID associated to the GSTIN.    
  
Sample request  
`https://ewb.cleartax.in/api/v0.2/taxable_entities/c5cc664c-d473-4ec5-9301-acf43349b7c4/transactions/upload?data_type=EWAY_BILLS&branch_id=5d2f7742-1484-4bb4-9a5b-b3b8c3586b40`
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-Cleartax-Auth-Token: <USER\_AUTH\_TOKEN>" type="string" required=true %}
Auth token will be generated and given upon request.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="custom\_mapper\_id" type="string" required=false %}
custom  mapper id of the template which has been already mapped into the business account on ClearTax E-Waybill portal. 
{% endapi-method-parameter %}

{% api-method-parameter name="branch\_id" type="string" required=true %}
Cleartax E-Waybill Branch\_id of that location for which data in the file belongs
{% endapi-method-parameter %}

{% api-method-parameter name="data\_type" type="string" required=true %}
EWAY\_BILLS will be the value   
Ex. `data_type:EWAY_BILLS`
{% endapi-method-parameter %}

{% api-method-parameter name="excelFile" type="object" required=true %}
File which contains documents either in ClearTax template, Govt template or Custom template.  
**`The file should be sent as form-data`**  
**`Here the parameter type of excelFile will be FILE.`**  
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
If the request completed successfully then only API will give status code 200 and response message.  
  
**activity\_id :** activity\_id is the unique ID associated with this upload activity. To fetch upload activity status or details, you will have to send this ID along with consequent corresponding API calls.  
**status** : Based on traffic on server, you may get status from given list.  
`'INIT', 'UPLOADED', 'QUEUED', 'PROCESSING', 'PROCESSED', 'ABORTED'`   
  
**queued\_count**: No. of documents already in the current processing queue.
{% endapi-method-response-example-description %}

```javascript
{
    "activity_id": "c11e2e14-4060-4ecb-b801-2cc22d7e727a",
    "error_response": null,
    "group_id": null,
    "other_activity_ids": null,
    "status": "UPLOADED",
    "queued_count": 0
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
In case provided parameter are incorrect.
{% endapi-method-response-example-description %}

```javascript
{
    "errors": {
        "err_1": {
            "code": "400",
            "message": "HTTP 400 Bad Request",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
When request is made using some invalid parameters.
{% endapi-method-response-example-description %}

```
{
    "errors": {
        "err_1": {
            "code": "500",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



