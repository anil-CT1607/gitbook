---
description: >-
  You can get the status of an upload activity by submitting a GET request to
  the Upload File API .
---

# Getting Upload Status

{% api-method method="get" host="https://ewb.cleartax.in/api" path="/v0.2/taxable\_entities/{taxable\_entity\_id}/upload\_activity/{activity\_id}/status" %}
{% api-method-summary %}
Get upload status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get file upload status.  
{taxable\_entity\_id} : taxable entity ID associated to the GSTIN.  
{activity\_id} : activity id given by Creating or Updating Documents API.  
  
Sample request : `https://ewb.cleartax.in/api/v0.2/taxable_entities/c5cc664c-d473-4ec5-9301-acf43349b7c4/upload_activity/02de95e9-864d-49b5-a793-5e29f718dd2b/status`  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-Cleartax-Auth-Token: <USER\_AUTH\_TOKEN>" type="string" required=true %}
Auth token will be generated & given upon request.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
status successfully retrieved.  
**status** : Based on traffic on server, you may get status from given list. `'INIT', 'UPLOADED', 'QUEUED', 'PROCESSING', 'PROCESSED', 'ABORTED'`
{% endapi-method-response-example-description %}

```javascript
{
    "activityId": "02de95e9-864d-49b5-a793-5e29f718dd2b",
    "status": "PROCESSED",
    "errorMessage": null,
    "queuedCount": 0
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
in case provided activity\_id or parameter incorrect
{% endapi-method-response-example-description %}

```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "No activity found for id 02de95e9-864d-49b5-a793-5e29f718dd2",
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



