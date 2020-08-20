---
description: >-
  If the upload activity status as seen above is PROCESSED, you can get the
  validation details of the upload activity by submitting a GET request to the
  Upload File API with following request headers.
---

# Getting Upload Validation

{% api-method method="get" host="https://ewb.cleartax.in/api/" path="v0.2/taxable\_entities/{taxable\_entity\_id}/upload\_activity/{activity\_id}" %}
{% api-method-summary %}
Get upload validation
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get file upload validation.  
**{taxable\_entity\_id}** : taxable entity ID associated to the GSTIN.  
**{activity\_id}** : activity id given by Creating or Updating Documents API.  
  
`Sample request : https://ewb.cleartax.in/api/v0.2/taxable_entities/c5cc664c-d473-4ec5-9301-acf43349b7c4/upload_activity/02de95e9-864d-49b5-a793-5e29f718dd2b`
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
file upload validation successfully retrieved.  
**`Note: Only the response fields relevant for integration are mentioned above. Actual response will have other fields which may not be relevant here.`**  
{% endapi-method-response-example-description %}

```javascript
{
    "activity_id": "02de95e9-864d-49b5-a793-5e29f718dd2b",
    "owner_taxable_entity_id": "c5cc664c-d473-4ec5-9301-acf43349b7c4",
    "owner_gstin": "27AACCB1409R1ZH",
    "owner_taxable_entity_name": "Maharashtra",
    "status": "PROCESSED",
    "total_rows_processed": 2,
    ........
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
In case provided activity\_id or parameter is incorrect.
{% endapi-method-response-example-description %}

```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "Unknown activity id 02de95e9-864d-49b5-a793-5e29f718dd2",
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



