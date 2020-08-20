# Extending Validity of E-Waybill

E-Waybill validity can be extended by updating the extension details. You can do this by getting the E-Waybill object using Get E-Waybill endpoint and then appending the required extension details to the object. Before calling the E-Waybill Extend API, you need to update the E-Waybill with the updated object.

## Update extension details

E-Waybill can be updated by submitting a **`PUT`**request to the E-Waybill API with the following request headers.

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybill/{{ID}}?activity_type=EXTEND_VALIDITY
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| id | Path | String | Required. Unique Transaction ID. |
| activity\_type | Query | String | Required. EXTEND\_VALIDITY |

Append the following key value pairs to the E-Waybill object received from Get E-Waybill API.

| Key | Type | Description |
| :--- | :--- | :--- |
| transport\_doc\_number | String | Required. Transport document number. |
| vehicle\_number | String | Required. Vehicle number. |
| transporter\_from\_place | String | Required. Transporter's city. |
| transporter\_from\_state | String | Required. Transporter's state. |
| dispatch\_from\_state | String | Required. Indian state from where dispatched. |
| remaining\_distance | Number | Required. Remaining distance in kilometers |
| extend\_validity\_reason | ENUM | Required. NATURAL\_CALAMITY, LAW & ORDER, DUE\_TO\_TRANSHIPMENT, ACCIDENT, OTHERS |
| extend\_validity\_remarks | String | Required. Remarks for extending validity. |
| consignment\_status | ENUM | Required. M,T \[Movement,Transit\] |
| transit\_type | ENUM | Required. on-road-"R", warehouse-"W", other="O" |
| transport\_mode | ENUM | Required. ROAD,TRAIN,SHIP,AIR |
| from\_pincode | String | Required. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/ewaybill/260920181261?activity_type=EXTEND_VALIDITY
```

#### Sample Payload

```text
{
    ...
    
    "transport_doc_number": "29AAACW6288M1ZH",
    "vehicle_number": "KA01AA1234",
    "transporter_from_place": "BANGALORE",
    "transporter_from_state": "KARNATAKA",
    "dispatch_from_state": "KARNATAKA",
    "remaining_distance": 10,
    "extend_validity_reason": "TRANSHIPMENT",
    "extend_validity_remarks": "Some remarks"
    
    ...
}
```

#### Sample Response:

{% tabs %}
{% tab title="201" %}
```text
{
    ...
    Updated E-Waybill object
    ...
}
```
{% endtab %}

{% tab title="400" %}
```
{
    "errors": {
        "err_1": {
            "code": "400",
            "message": "Cannot deserialize reason-for-updation from key DUE_TO_TRANSHIPMENT",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "extend_validity_reason": {
            "error_refs": [
                "err_1"
            ]
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Extend validity

E-Waybill validity can be extended by submitting a **`PUT`** request to the E-Waybill API with the following request headers.

{% hint style="danger" %}
**This request must to be sent within 8 hours before or 8 hours after the expiry of the E-Waybill.**
{% endhint %}

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/eway_bills/async_action/EXTEND_VALIDITY
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| - | Body | String | Required. ID of the document. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/eway_bills/async_action/EXTEND_VALIDITY
```

```text
[
    "260920181262"
]
```

#### Sample Response:

{% tabs %}
{% tab title="201" %}
```text
{
    workflow_id: "xxxxx-xxxxx-xxxxx-xxxxx"
}
```
{% endtab %}

{% tab title="400" %}
```
[
    {
        "ewb_id": "DOC502",
        "document_number": "DOC513",
        "field_name": "ewb_due_date",
        "error_message": "Can extend validity only before or after 8 hours of expiry of eway Bill."
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Please note down the `workflow_id` returned by this request. You can use this to poll the updated status with a GET request later.
{% endhint %}

## Check Status

E-Waybill async action status can be polled by submitting a **GET** request to the E-Waybill API with the following request headers.

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/async_action/{{WORKFLOW_ID}}/status
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| workflow\_id | Path | String | Required. This is the unique ID associated with the async workflow. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/async_action/9636b647-08ac-46a1-bd43-bd875906d166/status
```

#### Sample Response:

{% code title="200" %}
```text
{
    "workflow_id": "9636b647-08ac-46a1-bd43-bd875906d166",
    "status": "PROCESSED_WITH_ERRORS",
    "error_message": "Error: 711, Invalid pincode, 710",
    "total": 1,
    "failed": 1,
    "success": 0
}
```
{% endcode %}

{% hint style="info" %}
To know the new validity of E-Waybill, you can call the Get E-Waybill endpoint.
{% endhint %}

