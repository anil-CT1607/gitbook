---
description: >-
  You can use this API If the consignment of an e-way bill have to be moved in
  multiple vehicles.
---

# Multi-vehicle E-Waybill

## Multi-vehicle E-Waybill <a id="update-an-e-waybill"></a>

The request for generating a Multi-vehicle E-Waybill is sent by submitting a **PUT** request to the E-Waybill API with the following request headers.

This request needs the IDs of E-Waybill that you have generated

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{taxable_entity_id}/ewaybill/{id}/multi_vehicle
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| id | Path | String | Required. Unique Transaction ID. |
| Source | Path | String | USER, GOVERNMENT, TRANSPORTER, ACTIVE\_EWB |
| transport\_mode | Body | String | Mandatory.  ROAD, RAIL, AIR, SHIP, IN\_TRANSIT |
| from\_place | Body | String | Mandatory.  |
| quantity | Body | String | Mandatory.  |
| unit\_of\_measurement | Body | String | Mandatory.  Refer [unit master](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/resources-and-masters/unit-of-measurement-master) |
| update\_reason | Body | String | Mandatory. BREAKDOWN, 'RANSHIPMENT, OTHERS, FIRST\_TIME |
| remarks | Body | String | Mandatory.  |
| ewb\_client\_id | Body | String | Mandatory.  ID of the original E waybill |
| to\_place | Body | String | Mandatory.  |
| to\_state | Body | String | Mandatory.  |
| to\_state | Body | String | Mandatory.  |
| transporter\_history\_dtos | Body | List | Vehicle details are updated here |
| group\_number | Body | String | You can add multiple vehicle in a group and you can also add multiple groups |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/bf557750-936e-4209-ac46-f3e8426d4780/ewaybill/123456123/multi_vehicle
```

#### Sample Payload

```javascript
{
    "id": "",
    "group_number": 0,
    "owner": "bf557750-936e-4209-ac46-f3e8426d4780",
    "transport_mode": "ROAD",
    "from_place": "Hosur",
    "from_state": "Tamil Nadu",
    "quantity": "82",
    "unit_of_measurement": "BOX",
    "update_reason": "TRANSHIPMENT",
    "remarks": "no remark",
    "ewb_client_id": "tes123",
    "to_place": "Bangalore",
    "to_state": "Karnataka",
    "transporter_history_dtos": [
        {
            "id": "tes123",
            "revision_number": 0,
            "group_number": 1,
            "owner": "bf557750-936e-4209-ac46-f3e8426d4780",
            "transport_mode": "ROAD",
            "from_place": "Hosur",
            "from_state": "TAMILNADU",
            "quantity": "82",
            "unit_of_measurement": "BOX",
            "update_reason": "TRANSHIPMENT",
            "remarks": "no remark",
            "transport_history_state": "SYNCED_WITH_GOVT",
            "transporter_gstin": "29AAACW6288M1ZH",
            "transporter_name": null,
            "transport_doc_number": "12345",
            "transport_date": "2020-06-12",
            "vehicle_number": "tn70ab6565",
            "vehicle_type": null,
            "entered_by_gstin": "",
            "entered_on": "",
            "cewb_number": null,
            "is_cancelled": false
        }
    ]
}
```

{% hint style="success" %}
You will get an empty response if multi vehicle is successfully updated
{% endhint %}

