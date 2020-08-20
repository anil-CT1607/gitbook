# Getting E-Waybill

The response objects here will be same as describer in [generate E-Waybill](https://cleartax.gitbook.io/cleartax-for-developers/e-waybill-api/e-waybill-api-reference/e-waybill-json-api-reference/generating-e-waybill)

## Get an E-Waybill

You can get an E-Waybill by submitting a **GET** request to the E-Waybill API with the following request headers.

URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybill/{{ID}}?source={{SOURCE}}
```

Request Parameters:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">X-Cleartax-Auth-Token</td>
      <td style="text-align:left">Header</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Mandatory. The auth token generated from ClearTax user id and password.</td>
    </tr>
    <tr>
      <td style="text-align:left">taxable_entity_id</td>
      <td style="text-align:left">Path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Required. This is the unique ID associated with the GSTIN in your account.</td>
    </tr>
    <tr>
      <td style="text-align:left">id</td>
      <td style="text-align:left">Path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Required. Unique Transaction ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">source</td>
      <td style="text-align:left">Query</td>
      <td style="text-align:left">ENUM</td>
      <td style="text-align:left">
        <p>Optional. Possible values: USER, GOVERNMENT.</p>
        <p>Default: USER.</p>
      </td>
    </tr>
  </tbody>
</table>

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/bf557750-936e-4209-ac46-f3e8426d4780/ewaybill/EWB270920180650?source=USER
```

#### Sample Response:

{% tabs %}
{% tab title="200" %}
```javascript
    {
        "ignored_warnings": null,
        "owner": null,
        "id": "doca09",
        "transaction_date": "18/09/2019",
        "return_period": "092019",
        "source": "USER",
        "total_discount": 12.00,
        "total_taxable_val": 10000.00,
        "total_cgst_val": 600.00,
        "total_sgst_val": 600.00,
        "total_igst_val": 0.00,
        "discount_type": null,
        "total_val": 9200.00,
        "tags": null,
        "gst_status": null,
        "gst_validation_errors": null,
        "place_of_supply": "MAHARASHTRA",
        "updated_at": "18/09/2019",
        "user_updated_at": "18/09/2019",
        "is_canceled": false,
        "created_at": "18/09/2019",
        "cancel_reason": null,
        "cancel_remarks": null,
        "seller_contact_id": null,
        "consignee_contact_id": null,
        "receiver_contact_id": null,
        "bank_details": null,
        "custom_fields": null,
        "branch_id": null,
        "document_number": "sarthakparta09",
        "type": "SALE",
        "seller": {
            "name": null,
            "gstin": "29AEKPV7203E1Z9",
            "address1": null,
            "address2": null,
            "city": "VADGAON",
            "state": "MAHARASHTRA",
            "zip_code": "412106",
            "country": null,
            "phone_number": null
        },
        "receiver": {
            "name": "XYZ",
            "gstin": "29AAACW6288M1ZH",
            "address1": null,
            "address2": null,
            "city": null,
            "state": "MAHARASHTRA",
            "zip_code": "412106",
            "country": null,
            "phone_number": null
        },
        "consignee": {
            "name": "XYZ",
            "gstin": "29AAACW4202F1ZM",
            "address1": null,
            "address2": null,
            "city": null,
            "state": "MAHARASHTRA",
            "zip_code": "412106",
            "country": null,
            "phone_number": null
        },
        "ewb_number": "171001662857",
        "ewb_generated_date": "18-09-2019 11:24:00",
        "ewb_valid_from_date": "18-09-2019 11:24:00",
        "ewb_due_date": null,
        "ewb_govt_sync_status": "COMPLETE",
        "other_val": -2000.00,
        "total_cess_non_advol_val": 0.00,
        "is_multi_vehicle": false,
        "ewb_status": "PART_A",
        "transporter_history_dtos": null,
        "document_type": "INV",
        "transport_mode": null,
        "transporter_gstin": "29AAACW6288M1ZH",
        "transporter_name": null,
        "transporter_from_place": null,
        "transporter_from_state": null,
        "transport_doc_number": null,
        "transport_date": null,
        "vehicle_number": null,
        "vehicle_type": null,
        "update_reason": null,
        "update_remarks": null,
        "extend_validity_reason": null,
        "extend_validity_remarks": null,
        "sub_supply": "SUPPLY",
        "ewb_errors": null,
        "cewb_number": null,
        "distance": 100,
        "remaining_distance": null,
        "extended_date": null,
        "dispatch_from_state": null,
        "nic_ewb_status": null,
        "export_type": null,
        "generation_interaction_type": "API",
        "sub_supply_desc": null,
        "transaction_type": "ShipTo",
        "from_pincode": null,
        "consignment_status": null,
        "transit_type": null,
        "line_items": [
            {
                "item_code": "4101PSP475",
                "gst_code": "72111490",
                "gst_type": "GOODS",
                "description": null,
                "notes": "KOL-105 BOTTAM SPACER",
                "unit_price": null,
                "unit_price_including_tax": null,
                "unit_of_measurement": null,
                "item_id": null,
                "serial_number": 0,
                "quantity": 1.0,
                "discount_rate": null,
                "discount": 12.00,
                "taxable_val": 10000.00,
                "cgst_rate": 6.00,
                "cgst_val": 600.00,
                "sgst_rate": 6.00,
                "sgst_val": 600.00,
                "igst_rate": null,
                "igst_val": 0.00,
                "cess_rate": null,
                "cess_val": null,
                "total_val": 11200.00,
                "tags": null,
                "cess_non_advol_rate": null,
                "cess_non_advol_val": null
            }
        ],
        "transporter_code": null,
        "owned_by": "bf557750-936e-4209-ac46-f3e8426d4780",
        "owner_gstin": null,
        "branch_name": null,
        "active": false,
        "version_num": 1
    }
```
{% endtab %}

{% tab title="404" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "You do not have enough permissions to view this page/ access this feature. Please contact your Account Admin, if you require access.",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Get many E-Waybills

You can get many E-Waybills by submitting a **GET** request to the E-Waybill API with the following request headers.

URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybill?return_period=&transaction_status=&start_date=&end_date=&seller_gstin=&buyer_gstin=&invoice_direction=&id=&is_amended=&section_name=&owner_taxable_entity_id=&start=0&limit=20&min_total=&max_total=&sort_by=&include_canceled=&channel_value=&channel_type=&document_numbers=&contacts=&gstins=&sub_supply_type=&document_types=&vehicleNumbers=&transporter_gstins=&ewb_status=&min_distance=&max_distance=
```

#### Request Parameters:

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| source | Query | String | USER, GOVERNMENT |
| return\_period | Query | String | Return period in the format MMYYYY |
| start\_date | Query | String | Start date by which you need to filter |
| end\_date | Query | String | End date by which you need to filter |
| seller\_gstin | Query | Array | Seller GSTIN number |
| buyer\_gstin | Query | Array | Buyer GSTIN number |
| invoice\_direction | Query | ENUM | SALE, PURCHASE |
| id | Query | Array | Unique Transaction ID |
| is\_ammended | Query | Boolean  | TRUE, FALSE |
| invoice\_type | Query | Array | B2B , B2BUR , B2BA , B2CL , B2CS , EXPORT , IMPORT , ISD , COMPOSITE , B2B\_EXPORT |
| start | Query | String | Default: 0 /used for pagination |
| limit | Query | String | Default: 20 / number of invoices to limit in the response |
| ewb\_numbers | Query | String | Eway Bill number |
| ewb\_status | Query | Array | PENDING, PART\_A, GENERATED, CANCELLED |
| min\_distance | Query | String | Minimum distance |
| max\_distance | Query | String | Maximum distance |
| transporter\_gstins | Query | String | Transporter GSTIN |
| vehicleNumbers | Query | String | Vehicle number |
| sub\_supply\_type | Query | Array | SUPPLY, EXPORT, JOB\_WORK, OWN\_USE, SKD\_CKD, LINE\_SALES, RECIPIENT\_UNKNOWN, EXHIBITION, FAIRS, SALES\_RETURN, JOB\_WORK\_RETURNS, IMPORT, OTHERS |

#### Sample Request:

```text
https://ewbfrontend-preprodpub-http.internal.cleartax.co/api/v0.1/taxable_entities/bf557750-936e-4209-ac46-f3e8426d4780/ewaybill?document_numbers=A0fg180660&branches=5ae1bbae-27e2-48e6-8d5b-0fa80c0ee8ca&branches
```

#### Sample Response:

```javascript
[
    {
        "ignored_warnings": null,
        "owner": null,
        "id": "2st12367",
        "transaction_date": "27/09/2018",
        "return_period": "062018",
        "source": "USER",
        "total_taxable_val": 150024.85,
        "total_cgst_val": 9001.45,
        "total_sgst_val": 9001.45,
        "discount_type": null,
        "total_val": 168027.76,
        "tags": null,
        "gst_status": null,
        "gst_validation_errors": null,
        "place_of_supply": "KARNATAKA",
        "updated_at": "02/06/2020",
        "user_updated_at": "02/06/2020",
        "is_canceled": false,
        "created_at": "02/06/2020",
        "cancel_reason": null,
        "cancel_remarks": null,
        "seller_contact_id": null,
        "consignee_contact_id": null,
        "receiver_contact_id": null,
        "bank_details": null,
        "custom_fields": null,
        "branch_id": "5ae1bbae-27e2-48e6-8d5b-0fa80c0ee8ca",
        "document_number": "A0fg180660",
        "type": "SALE",
        "seller": {
            "name": "Test stores",
            "gstin": "29AEKPV7203E1Z9",
            "address1": "Maharashtra",
            "address2": "Maharashtra",
            "city": "Bangalore",
            "state": "KARNATAKA",
            "zip_code": "560068",
            "country": null,
            "phone_number": null
        },
        "receiver": {
            "name": "BILLING NAME",
            "gstin": "29AAACW6288M1ZH",
            "address1": "BILLING ADDRESS, 1 DR BURMAN MARG,UPSIDE IND. AREA SAHIBABAD-201010, GHAZIABAD UTTER PRADESH",
            "address2": "BILLING ADDRESS 2",
            "city": "Bangore",
            "state": "KARNATAKA",
            "zip_code": "560068",
            "country": null,
            "phone_number": null
        },
        "consignee": {
            "name": "SHIPPING NAME",
            "gstin": "29AAACW4202F1ZM",
            "address1": "SHIPPING ADDRESS, 1 DR BURMAN MARG,UPSIDE IND. AREA SAHIBABAD-201010, GHAZIABAD UTTER PRADESH",
            "address2": "SHIPPING ADDRESS 1",
            "city": "Bangalore",
            "state": "KARNATAKA",
            "zip_code": "560068",
            "country": null,
            "phone_number": null
        },
        "ewb_number": "141001710537",
        "ewb_generated_date": "02-06-2020 12:15:00",
        "ewb_valid_from_date": "02-06-2020 12:15:00",
        "ewb_due_date": "03-06-2020 23:59:00",
        "ewb_govt_sync_status": "COMPLETE",
        "other_val": 0.00,
        "total_cess_non_advol_val": 0.00,
        "is_multi_vehicle": false,
        "ewb_status": "GENERATED",
        "transporter_history_dtos": null,
        "document_type": "INV",
        "transport_mode": "ROAD",
        "transporter_gstin": "29AAACW6288M1ZH",
        "transporter_name": null,
        "transporter_from_place": "",
        "transporter_from_state": null,
        "transport_doc_number": null,
        "transport_date": null,
        "vehicle_number": "KA19ED2843",
        "vehicle_type": null,
        "update_reason": null,
        "update_remarks": null,
        "extend_validity_reason": null,
        "extend_validity_remarks": null,
        "sub_supply": "SUPPLY",
        "ewb_errors": null,
        "cewb_number": null,
        "distance": 100,
        "remaining_distance": null,
        "extended_date": null,
        "dispatch_from_state": "KARNATAKA",
        "nic_ewb_status": null,
        "export_type": null,
        "generation_interaction_type": "API",
        "sub_supply_desc": null,
        "transaction_type": "Regular",
        "from_pincode": null,
        "consignment_status": null,
        "transit_type": null,
        "line_items": [
            {
                "item_code": null,
                "gst_code": "61091000",
                "gst_type": "GOODS",
                "description": "READYMADE GARMENT",
                "notes": null,
                "unit_price": null,
                "unit_price_including_tax": null,
                "unit_of_measurement": "BOX",
                "item_id": null,
                "serial_number": 1,
                "quantity": 82.0,
                "discount_rate": null,
                "discount": null,
                "taxable_val": 150024.85,
                "cgst_rate": 2.50,
                "cgst_val": 9000.45,
                "sgst_rate": 2.50,
                "sgst_val": 9000.46,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null,
                "total_val": 168027.76,
                "tags": null,
                "cess_non_advol_rate": null,
                "cess_non_advol_val": null
            }
        ],
        "transporter_code": null,
        "owned_by": "bf557750-936e-4209-ac46-f3e8426d4780",
        "owner_gstin": null,
        "branch_name": null,
        "active": false,
        "version_num": 1
    }
]
```

