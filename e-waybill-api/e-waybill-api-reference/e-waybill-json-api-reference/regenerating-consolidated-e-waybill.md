# Regenerating Consolidated E-Waybill

The API request for regenerating a Consolidated E-Waybill is asynchronous. Once you send a PUT request to regenerate an E-Waybill, you will receive a Workflow ID. Using this Workflow ID, you can check the regeneration status by sending a GET request to another endpoint.

## Regenerate Consolidated E-Waybill

The request for regenerating a Consolidated E-Waybill is sent by submitting a **PUT** request to the E-Waybill API with the following request headers.

This request needs the IDs of E-Waybills with status `PART_A` or `GENERATED` or `UPDATED`. 

| Key | Type | Description |
| :--- | :--- | :--- |
| cewb\_id | String | Required. Consolidated E-Waybill ID |
| vehicle\_number | String | Required. Vehicle number. |
| from\_place | String | Required. City name |
| from\_state | String | Required. Indian state |
| transport\_date | String | Required. Date of transport. |
| transport\_mode | String | Required. Mode of transport. |
| regenerate\_reason | ENUM | Required. Reason for regeneration. Possible values: BREAKDOWN, TRANSHIPMENT, OTHERS |
| regenerate\_remarks | String | Required. Remarks for regeneration. |

{% hint style="warning" %}
Note: All E-waybills sent for generating a Consolidated E-Waybill should have the same status.
{% endhint %}

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/consolidated_ewb/async_action/REGENERATE_CEWB
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/consolidated_ewb/async_action/REGENERATE_CEWB
```

#### Sample Payload

```javascript
{
    "cewb_id": "1710005417", // Consolidated Ewaybill Number
    "vehicle_number": "KA01AA1234",
    "from_place": "BANGALORE",
    "from_state": "KARNATAKA",
    "transport_date": "26/09/2018",
    "transport_mode": "ROAD",
    "regenerate_reason": "BREAKDOWN",
    "regenerate_remarks": "Any remark "
}
```

#### Sample Response:

```javascript
{
    "workflow_id": "5a3f5b0e-6d99-4efa-aa63-20bb68327f60",
    "status": "INIT",
    "error_message": null,
    "total": 5,
    "failed": 0,
    "success": 5
}
```

{% hint style="info" %}
Please note down the `workflow_id` returned by this request. You can use this to poll the updated status with a GET request later.
{% endhint %}

## Get regeneration status

You can get the status of regeneration activity by submitting a **GET** request to the E-Waybill API with following request headers.

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/consolidated_ewb/async_action/{{WORKFLOW_ID}}/status
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| workflow\_id | Path | String | Required. This is the workflow ID received in response to the Consolidate API. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/consolidated_ewb/async_action/5a3f5b0e-6d99-4efa-aa63-20bb68327f60/status
```

#### Sample Response:

{% code title="200" %}
```javascript
{
    "workflow_id": "5a3f5b0e-6d99-4efa-aa63-20bb68327f60",
    "status": "PROCESSED",
    "error_message": null,
    "total": 5, Number of E-waybills consolidated
    "failed": 0, Number of failed documents
    "success": 5 Number of successful documents
}
```
{% endcode %}

{% hint style="info" %}
To know the Consolidated E-Waybill ID `cewb_number`, you can call the [Get E-Waybill endpoint](https://cleartax.gitbook.io/cleartax-for-developers/e-waybill-api/e-waybill-api-reference/e-waybill-json-api-reference/getting-e-waybill#get-an-e-waybill).
{% endhint %}

