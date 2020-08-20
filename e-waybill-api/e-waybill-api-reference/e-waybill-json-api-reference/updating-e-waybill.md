# Updating E-Waybill

Update E-Waybill API can be used to add Transporter details or PART\_B to the already generated E-Waybill.

PART\_B Object:

| Key | Type | Description |
| :--- | :--- | :--- |
| transport\_mode | ENUM | Required. Mode of Transport. Possible Values: ROAD, RAIL, AIR, SHIP. |
| transporter\_gstin | String | Required. GSTIN of Transporter. |
| transporter\_name | String | Required. Name of Transporter. |
| transporter\_from\_place | String | Required. Transporter City. |
| transporter\_from\_state | String | Required. Transporter State. |
| transport\_doc\_number | String | Required. Transport document number. |
| transport\_date | String | Required. Date of transport. |
| vehicle\_number | String | Required. Vehicle number. |
| vehicle\_type | String | Required. Vehicle type. |
| update\_reason | ENUM | Required. Reason for updating. Possible values: FIRST\_TIME, BREAKDOWN, TRANSHIPMENT, OTHERS. |
| update\_remarks | String | Required. Remarks for updating. |
| id | String | Required. Unique Transaction ID. |

## Update an E-Waybill

The request for updating an E-Waybill is sent by submitting a **`PUT`** ``request to the E-Waybill API with the following request headers.

{% hint style="info" %}
This request needs the IDs of E-Waybill with status as `PART_A`. 
{% endhint %}

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybill/{{ID}}/update_transporter?activity_type=UPDATE_EWB
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| id | Path | String | Required. Unique Transaction ID. |
| - | Body | Object | Required. PART\_B object. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/ewaybill/EWB10293847/update_transporter?activity_type=UPDATE_EWB
```

#### Sample Payload

```javascript
{
    "transport_mode": "ROAD",
    "transporter_gstin": "29AAACW6288M1ZH",
    "transporter_name": "ABC",
    "transporter_from_place": "Bangalore",
    "transporter_from_state": "KARNATAKA",
    "transport_doc_number": "string",
    "transport_date": "31/07/2018",
    "vehicle_number": "KA01AA1234",
    "vehicle_type": "REGULAR",
    "update_reason": "FIRST_TIME",
    "update_remarks": "string",
    "id": "EWB10293847"
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
            "code": "BAD_REQUEST",
            "message": "Cannot update an EWay Bill which is already generated and has no transporter updates made in it.",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "ewb_status": {
            "error_refs": [
                "err_1"
            ]
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Update many E-Waybills

The request for updating E-Waybills is sent by submitting a **PUT** request to the E-Waybill API with the following request headers.

This request needs the IDs of E-Waybills with status `PART_A`. 

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybills/update_transporter?activity_type=UPDATE_EWB
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| - | Body | Array | Required. Array of PART\_B objects. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/269ea15f-5e27-4203-bb11-3bb911fc5724/ewaybills/update_transporter?activity_type=UPDATE_EWB
```

#### Sample Payload

```javascript
[
    {
        "transport_mode": "ROAD",
        "transporter_gstin": "29AAACW6288M1ZH",
        "transporter_name": "ABC",
        "transporter_from_place": "Bangalore",
        "transporter_from_state": "KARNATAKA",
        "transport_doc_number": "string",
        "transport_date": "31/07/2018",
        "vehicle_number": "KA01AA1234",
        "vehicle_type": "REGULAR",
        "update_reason": "FIRST_TIME",
        "update_remarks": "string",
        "id": "DOC512"
    }
]
```

#### Sample Response:

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "id": "DOC512",
        "status": true,
        "data": {
            "ewb_number": "151001638120",
            "ewb_generated_date": "04-04-2019 22:06:00",
            "ewb_valid_from_date": "04-04-2019 22:06:00",
            "ewb_due_date": "05-04-2019 23:59:00",
            "ewb_govt_sync_status": "COMPLETE",
            "ewb_status": "GENERATED",
            ...
            E-Waybill object
            ...
        },
        "errorResponse": null,
        "error_msgs": null
    }
]
```
{% endtab %}

{% tab title="200 \(with errors\)" %}
```javascript
[
    {
        "id": "DOC512",
        "status": false,
        "data": {E-Waybill object},
        "errorResponse": {error response object},
        "error_msgs": "Cannot update an EWay Bill which is already generated and has no transporter updates made in it."
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Bulk update API always returns 200 status code even if there are any errors from NIC. To get error message, you need to parse the response JSON.
{% endhint %}

