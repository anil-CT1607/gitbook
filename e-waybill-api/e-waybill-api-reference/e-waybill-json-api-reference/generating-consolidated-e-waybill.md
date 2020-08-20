# Generating Consolidated E-Waybill

The API request for creating a Consolidated E-Waybill is asynchronous. Once you send a PUT request to create a Consolidated E-Waybill, you will receive a Workflow ID. Using this Workflow ID, you can check the regeneration status by sending a GET request to another endpoint.

## Generate Consolidated E-Waybill

The request for generating a Consolidated E-Waybill is sent by submitting a **PUT** request to the E-Waybill API with the following request headers.

This request needs the IDs of E-Waybills with status `PART_A` or `GENERATED` or `UPDATED`. 

{% hint style="warning" %}
Note: All E-waybills sent for generating a Consolidated E-Waybill should have the same status.
{% endhint %}

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/consolidated_ewb/async_action/GENERATE_CEWB
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| - | Body | Array | Required. Array of Unique Transaction IDs to be consolidated. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/consolidated_ewb/async_action/GENERATE_CEWB
```

#### Sample payload

```text
[
    "DOC500",
    "DOC501"
]
```

#### Sample Response:

{% code title="200" %}
```text
{
    "workflow_id": "21ae06f2-65f8-475d-8e60-8d1cab696c1b",
    "status": "INIT",
    "error_message": null,
    "total": 2,
    "failed": 0,
    "success": 2
}
```
{% endcode %}

{% hint style="info" %}
Please note down the `workflow_id` returned by this request. You can use this to poll the updated status with a GET request later.
{% endhint %}

In the response, `status` can be either of the following:

| Status | Description |
| :--- | :--- |
| INIT | Initial state |
| PROCESSING | Processing the request |
| PROCESSED | Request processed successfully. |
| PROCESSED\_WITH\_ERRORS | Request processed with errors. |

## Get consolidation status

You can get the status of consolidation activity by submitting a **GET** request to the E-Waybill API with following request headers.

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
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/consolidated_ewb/async_action/21ae06f2-65f8-475d-8e60-8d1cab696c1b/status
```

#### Sample Response:

{% code title="200" %}
```text
{
    "workflow_id": "21ae06f2-65f8-475d-8e60-8d1cab696c1b",
    "status": "PROCESSED",
    "error_message": null,
    "total": 2, Number of E-waybills consolidated
    "failed": 0, Number of failed documents
    "success": 2 Number of successful documents
}
```
{% endcode %}

{% hint style="info" %}
To know the Consolidated E-Waybill number `cewb_number`, you can call the Get E-Waybill endpoint. 
{% endhint %}

## 

