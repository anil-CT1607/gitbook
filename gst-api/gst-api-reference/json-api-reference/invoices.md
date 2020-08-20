# Invoices

ClearTax Invoices APIs provide you the ability to get invoices from ClearTax account or add new invoice to your ClearTax account.

## Resource Objects

### Invoice Object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| source | String |  | Mandatory. "USER" for documents uploaded from your software. "GOVERNMENT" for documents downloaded from GSTN. |
| id | String |  | Mandatory.  |
| serial\_number | string |  | Mandatory.  |
| type | String |  | Mandatory. "SALE" for outward documents. "PURCHASE" for inward documents. |
| transaction\_date | String |  | Mandatory. |
| place\_of\_supply | string |  | Mandatory. |
| return\_period | string |  | Optional. If not provided, return period will be auto computed based on transaction date. |
| quarterly\_return\_period | string |  | Optional. If not provided, quarterly return period will be auto computed based on transaction date. |
| reverse\_charge\_applicable | boolean |  | Optional. Is reverse charge applicable? Default: False |
| total\_val | number |  | Optional. If not provided, invoice total value will be auto computed based on the line item total values. |
| total\_val\_foreign\_currency | number |  | Optional. If not provided, invoice total value in foreign currency will be auto computed based on line item total values in foreign currency. |
| line\_items | array |  | Mandatory. Array of line item objects. |
| seller | object |  | Mandatory. Instance of party object. |
| receiver | object |  | Mandatory. Instance of party object. |
| consignee | object |  | Optional. Instance of party object. |
| bank\_details | object |  | Optional. |
| export | object |  | Optional. |
| import | object |  | Optional. |
| ecommerce | object |  | Optional. |
| isd | object |  | Optional. |
| advance\_payments | array |  | Optional. Array of advance payment objects. |
| custom\_fields | array |  | Optional. Array of custom field objects. |
| is\_amendment | boolean |  | Conditional. Required only if this is an amendment invoice. |
| is\_amended | boolean |  | Conditional. Required only if this is an amended invoice. |
| amendment\_detail | string | Enum: "AMENDED", "AMENDMENT", "NOT\_AMENDED" | Conditional. Required only if this is an amendment or amended invoice. |
| original\_invoice\_number | string |  | Conditional. Required only if this is an amendment invoice. |
| original\_invoice\_date | string |  | Conditional. Required only if this is an amendment invoice. |
| original\_invoice\_gstin | string |  | Conditional. Required only if this is an amendment invoice. |
| original\_doc\_num | string |  | Conditional. Required only if this is an amendment invoice.  |
| ref\_doc\_number | string |  | Optional. |
| date\_of\_purchase | string |  | Optional. |
| country\_of\_supply | string |  | Optional. |
| customer\_type | string |  | Optional. |
| supplier\_type | string |  | Optional. |
| supplier\_claiming\_refund | string |  | Optional. |
| auto\_populated\_to\_refunds | string |  | Optional. |
| tcs\_applicable | Boolean |  | Optional. |
| tds\_applicable | Boolean |  | Optional. |
| flag\_for\_supply | Boolean |  | Optional. |
| discount\_type | string |  | Optional. |
| shipping\_charge | string |  | Optional. |
| rounding\_factor | string |  | Optional. |
| differential\_tax | string |  | Optional. |
| export\_currency | string |  | Optional. |
| conversion\_rate | string |  | Optional. |
| terms\_and\_conditions | string |  | Optional. |
| payment\_terms | string |  | Optional. |
| notes | string |  | Optional. |
| created\_at | date |  | Read only. |
| updated\_at | date |  | Read only. |
| is\_canceled | boolean |  | Read only. |
| classification | string |  | Read only. |
|  |  |  |  |

### Line item object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| tcs | object |  | Optional. |
| tds | object |  | Optional. |
| total\_val\_foreign\_currency | number |  | Optional. |
| zero\_tax\_category | String | ENUM: 'NILRATED', 'EXEMPTED', 'NONGSTSUPPLY', 'SUPPLYFROMCOMPOSITIONDEALER', 'UINHOLDER' | Conditional when it is a a Nil Rated/Exempt/NonGST Item |
| description | String |  | Optional. |
| notes | String |  | Optional. |
| quantity | Number |  | Optional. |
| serial\_number | Number |  | Optional. This value will be auto computed if not provided. |
| unit\_price | number |  | Optional. |
| unit\_of\_measurement | String |  | Refer [Unit master](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/resources-and-masters/unit-of-measurement-master) |
| total\_val | Number |  | Optional. This value will be auto computed if not provided. |
| taxable\_val | Number |  | Mandatory. |
| sgst\_rate | Number | accepts only GST compliant tax rates \[0, 0.05, 0.125, 0.5, 0.75, 1.5, 2.5, 3.75, 6, 9, 14\] | Conditional. Should be equal to cgst value.  |
| cess\_rate | Number |  | Conditional when applicable |
| cgst\_rate | Number | accepts only GST compliant tax rates \[0, 0.05, 0.125, 0.5, 0.75, 1.5, 2.5, 3.75, 6, 9, 14\] | Conditional. Should be equal to sgst value. |
| igst\_rate | Number |  | Conditional when applicable |
| gst\_type | String |  | Optional. Is it a goods/service |

### Party Object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| name | string |  | Party Name |
| gstin | string |  | Conditional. In case the invoice type is "SALE", gstin is mandatory for seller object. In case the invoice type is "PURCHASE", gstin is mandatory for receiver object. If receiver do not have GSTIN please provide 'NRP'\(non registered person\). Receiver GSTIN is mandatory for Deemed or SEZ export or B2B Sale from Bonded WH |
| address | string |  | Party address |
| city | string |  | Party city |
| state | string |  | Party state. Refer [State Master](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/resources-and-masters/place-is-supply-master) |
| zip\_code | string |  | Party zip code |
| country | string |  | Party Country |
| phone\_number | string |  | Party phone number |

### Bank details object

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Field Validation</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">account_number</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Bank account number</td>
    </tr>
    <tr>
      <td style="text-align:left">bank_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Name of the Bank</td>
    </tr>
    <tr>
      <td style="text-align:left">branch_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Name of the Branch of Bank</td>
    </tr>
    <tr>
      <td style="text-align:left">ifsc_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Max character: 11</p>
        <p>Have to be alpha-numeric</p>
      </td>
      <td style="text-align:left">IFSC Code of the Branch</td>
    </tr>
    <tr>
      <td style="text-align:left">swift_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Swift Code of the Bank</td>
    </tr>
  </tbody>
</table>

### Export object

{% hint style="info" %}
SGST and CGST rate should be Zero for export invoices
{% endhint %}

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| export\_type | String | ENUM \['DEEMED', 'SEZ\_WITHOUT\_IGST', 'SEZ\_WITH\_IGST', 'EXPORT\_WITH\_IGST', 'EXPORT\_UNDER\_BOND', 'SALE\_FROM\_BONDED\_WH', 'REGULAR'\] | Mandatory. |
| shipping\_bill\_num | Integer | MIN length - 3 Max length - 7 | optional. |
| shipping\_port\_num | String |  | optional. |
| shipping\_bill\_date | String | YYYY-MM-DD | optional. |

### Import object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| bill\_of\_entry | String | length = 7 | Mandatory |
| bill\_of\_entry\_value | Number |  | Optional |
| bill\_of\_entry\_date | StringString | YYYY-MM-DD | Mandatory |
| import\_invoice\_type | String | ENUM \['GOODS', 'GOODS\_FROM\_SEZ', 'SERVICE\_FROM\_SEZ', 'SERVICES'\] | Mandatory |
| port\_code | String | 6 character | Mandatory |

### E-commerce object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| ecommerce\_operator | Object |  | Optional. Refer [Party Object](invoices.md#party-object) for fields |
| merchant\_id | String |  | Optional |

### Advance payment object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| document\_number | String |  | Optional. |
| document\_date | String | YYYY-MM-DD | Optional. |
| adjustment\_val | Number |  | Optional. |

### Custom field object

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| label | String |  | Label of custom field |
| value | String |  | Value of Custom field |

## Get an Invoice

You can get an invoice by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/invoices/{{invoice_id}}?source=USER
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| invoice\_id | Path | String | Required. Unique Transaction ID. |
| source | query | String | USER, GOVERNMENT |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/invoices/123abc?source=USER
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "ref_doc_number": null,
    "due_date": null,
    "paid_on": null,
    "shipping_charge": null,
    "invoice_status": "CREATED",
    "payment_terms": null,
    "notes": null,
    "advance_payments": [
        {
            "document_number": null,
            "document_date": null,
            "adjustment_val": null
        }
    ],
    "isd": {
        "original_supplier": null,
        "isd": null
    },
    "export_currency": null,
    "provisional_itc_claimed": null,
    "conversion_rate": null,
    "total_val_foreign_currency": null,
    "due_balance": null,
    "transaction_payment_status": null,
    "cgst_itc_claim_amount": null,
    "sgst_itc_claim_amount": null,
    "igst_itc_claim_amount": null,
    "cess_itc_claim_amount": null,
    "ignored_warnings": null,
    "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
    "id": "EX17_29AAFCD5862R1ZR_SALE_2019_NA",
    "transaction_date": "2019-08-20",
    "return_period": "082019",
    "quarterly_return_period": "142019",
    "source": "USER",
    "total_taxable_val": 40000.00,
    "total_cgst_val": 3600.00,
    "total_sgst_val": 3600.00,
    "total_igst_val": 0.00,
    "total_cess_val": 2000.00,
    "discount_type": null,
    "total_val": 40000.00,
    "gst_status": "STAGED",
    "gst_validation_errors": null,
    "place_of_supply": "OTHERTERRITORY",
    "updated_at": "2020-04-01",
    "user_updated_at": "2020-04-01",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-04-01",
    "rounding_factor": null,
    "section_name": "B2B",
    "fiscal_year": "2019",
    "fiscal_month": "AUGUST",
    "fiscal_quarter": "Q2",
    "total_tax_value": 9200.00,
    "date_of_purchase": "2019-08-20",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": null,
    "receiver_contact_id": null,
    "customer_type": null,
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": null,
    "serial_number": "EX17",
    "type": "SALE",
    "original_invoice_number": null,
    "original_invoice_date": null,
    "original_invoice_gstin": null,
    "classification": "B2B_EXPORT",
    "line_items": [
        {
            "tcs": {
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null
            },
            "tds": {
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null
            },
            "total_val_foreign_currency": null,
            "zero_tax_category": null,
            "item_code": null,
            "gst_code": "2851",
            "gst_type": "GOODS",
            "description": null,
            "notes": null,
            "unit_price": null,
            "unit_price_including_tax": null,
            "unit_of_measurement": null,
            "serial_number": 1,
            "quantity": null,
            "discount_rate": null,
            "discount": null,
            "taxable_val": 40000.00,
            "cgst_rate": 9.00,
            "cgst_val": 3600.00,
            "sgst_rate": 9.00,
            "sgst_val": 3600.00,
            "igst_rate": 0.00,
            "igst_val": 0.00,
            "cess_rate": 200.00,
            "cess_val": 2000.00,
            "total_val": 40000.00,
            "customer_billing_gstin": null
        }
    ],
    "seller": {
        "name": "Karnataka",
        "gstin": "29AAFCD5862R1ZR",
        "address": null,
        "city": null,
        "state": "KARNATAKA",
        "zip_code": null,
        "country": null,
        "phone_number": null
    },
    "receiver": {
        "name": "Apple Inc",
        "gstin": "29ALSPT0208L1ZI",
        "address": null,
        "city": null,
        "state": null,
        "zip_code": null,
        "country": null,
        "phone_number": null
    },
    "consignee": {
        "name": null,
        "gstin": "29ALSPT0208L1ZI",
        "address": null,
        "city": null,
        "state": null,
        "zip_code": null,
        "country": null,
        "phone_number": null
    },
    "reverse_charge_applicable": null,
    "tcs_applicable": null,
    "tds_applicable": null,
    "country_of_supply": null,
    "recon_status": null,
    "flag_for_supply": null,
    "auto_populated_to_refunds": true,
    "supplier_claiming_refund": null,
    "return_period_from_transcation_date": null,
    "document_number": "EX17",
    "doc_number": "EX17",
    "doc_date": 1566259200000,
    "sub_type": "DEEMED",
    "original_doc_num": null,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "export": {
        "export_type": "DEEMED",
        "shipping_bill_num": null,
        "shipping_port_num": null,
        "shipping_bill_date": null
    },
    "import": {
        "bill_of_entry": null,
        "bill_of_entry_value": null,
        "bill_of_entry_date": null,
        "import_invoice_type": null,
        "port_code": null
    },
    "ecommerce": {
        "ecommerce_operator": null,
        "merchant_id": null
    },
    "version_num": 0
}
```
{% endtab %}

{% tab title="404" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "Invoice with id EX17_29AAFCD5862R1R_SALE_2019_NA does not exist",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "400",
            "message": "Must be either GOODS or SERVICES",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "line_items": {
            "0": {
                "gst_type": {
                    "error_refs": [
                        "err_1"
                    ]
                }
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

#### Response Parameters

The response for this API will be a complete [Invoice Object](invoices.md#invoice-object). In addition to the keys specified in the Invoice Object, you may receive the below additional keys which may be relevant for you.

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| invoice\_status | String | Invoice status can be \['DRAFT', 'CREATED', 'APPROVED', 'PAID'\], |
| owner | String | Owner ID of the user Example: 249bf74-7392-4fa2-b3a0-685c6c7ad87e |
| gst\_status | String | Transaction GST filing status, managed by CT \['STAGED', 'SYNCED', 'FILED'\] |
| gst\_validation\_errors | Array | Validation errors reported by govt on SAVE/SUBMIT |
| updated\_at | String | Transaction updated date in YYYY-MM-dd format |
| user\_updated\_at | String | Transaction user updated date in YYYY-MM-dd format |
| created\_at | String | Transaction created date in YYYY-MM-dd format |

#### Error Detail

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| error\_code | String | Error Code  |
| message | String | Error message |
| error\_sources | String | Displays under which object and field the error is in. |

## Get Invoices

You can get multiple invoices by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/invoices?return_period=XXXXXX
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
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

{% hint style="info" %}
If you receive an empty array `[]` in the response with HTTP status code `200`, it means there are no invoices in ClearTax matching the filters specified in the query parameters.
{% endhint %}

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/invoices?fiscal_year=2019&invoice_direction=SALE&start=0
```

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "ref_doc_number": null,
        "due_date": null,
        "paid_on": null,
        "shipping_charge": null,
        "invoice_status": "CREATED",
        "payment_terms": null,
        "notes": null,
        "advance_payments": [
            {
                "document_number": null,
                "document_date": null,
                "adjustment_val": null
            }
        ],
        "isd": {
            "original_supplier": null,
            "isd": null
        },
        "export_currency": null,
        "provisional_itc_claimed": null,
        "conversion_rate": null,
        "total_val_foreign_currency": null,
        "due_balance": null,
        "transaction_payment_status": null,
        "cgst_itc_claim_amount": 0.00,
        "sgst_itc_claim_amount": 0.00,
        "igst_itc_claim_amount": 0.00,
        "cess_itc_claim_amount": 0.00,
        "ignored_warnings": null,
        "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
        "id": "EX17_29AAFCD5862R1ZR_SALE_2019_NA",
        "transaction_date": "2019-08-20",
        "return_period": "082019",
        "quarterly_return_period": "142019",
        "source": "USER",
        "total_taxable_val": 40000.00,
        "total_cgst_val": 3600.00,
        "total_sgst_val": 3600.00,
        "total_igst_val": 0.00,
        "total_cess_val": 2000.00,
        "discount_type": null,
        "total_val": 40000.00,
        "gst_status": "STAGED",
        "gst_validation_errors": null,
        "place_of_supply": "OTHERTERRITORY",
        "updated_at": "2020-04-01",
        "user_updated_at": "2020-04-01",
        "is_amendment": false,
        "amendment_detail": null,
        "uploaded_once": false,
        "is_canceled": false,
        "is_rate_inclusive_of_tax": false,
        "created_at": "2020-04-01",
        "rounding_factor": null,
        "section_name": "B2B",
        "fiscal_year": "2019",
        "fiscal_month": "AUGUST",
        "fiscal_quarter": "Q2",
        "total_tax_value": 9200.00,
        "date_of_purchase": "2019-08-20",
        "validate_warnings": false,
        "seller_contact_id": null,
        "consignee_contact_id": null,
        "receiver_contact_id": null,
        "customer_type": null,
        "supplier_type": null,
        "differential_tax": null,
        "terms_and_conditions": null,
        "serial_number": "EX17",
        "type": "SALE",
        "original_invoice_number": null,
        "original_invoice_date": null,
        "original_invoice_gstin": null,
        "classification": "B2B_EXPORT",
        "line_items": [
            {
                "tcs": {
                    "cgst_rate": null,
                    "cgst_val": null,
                    "sgst_rate": null,
                    "sgst_val": null,
                    "igst_rate": null,
                    "igst_val": null,
                    "cess_rate": null,
                    "cess_val": null
                },
                "tds": {
                    "cgst_rate": null,
                    "cgst_val": null,
                    "sgst_rate": null,
                    "sgst_val": null,
                    "igst_rate": null,
                    "igst_val": null,
                    "cess_rate": null,
                    "cess_val": null
                },
                "total_val_foreign_currency": null,
                "zero_tax_category": null,
                "item_code": null,
                "gst_code": "2851",
                "gst_type": "GOODS",
                "description": null,
                "notes": null,
                "unit_price": null,
                "unit_price_including_tax": null,
                "unit_of_measurement": null,
                "item_id": null,
                "serial_number": 1,
                "quantity": null,
                "discount_rate": null,
                "discount": null,
                "taxable_val": 40000.00,
                "cgst_rate": 9.00,
                "cgst_val": 3600.00,
                "sgst_rate": 9.00,
                "sgst_val": 3600.00,
                "igst_rate": 0.00,
                "igst_val": 0.00,
                "cess_rate": 200.00,
                "cess_val": 2000.00,
                "total_val": 40000.00,
                "customer_billing_gstin": null,
                "itc_details": {
                    "itc_type": null,
                    "itc_claim_percentage": null,
                    "cgst_total_itc": null,
                    "sgst_total_itc": null,
                    "igst_total_itc": null,
                    "cess_total_itc": null,
                    "cgst_claimed_itc": null,
                    "sgst_claimed_itc": null,
                    "igst_claimed_itc": null,
                    "cess_claimed_itc": null
                }
            }
        ],
        "seller": {
            "name": "Karnataka",
            "gstin": "29AAFCD5862R1ZR",
            "address": null,
            "city": null,
            "state": "KARNATAKA",
            "zip_code": null,
            "country": null,
            "phone_number": null
        },
        "receiver": {
            "name": "Apple Inc",
            "gstin": "29ALSPT0208L1ZI",
            "address": null,
            "city": null,
            "state": null,
            "zip_code": null,
            "country": null,
            "phone_number": null
        },
        "consignee": {
            "name": null,
            "gstin": "29ALSPT0208L1ZI",
            "address": null,
            "city": null,
            "state": null,
            "zip_code": null,
            "country": null,
            "phone_number": null
        },
        "reverse_charge_applicable": null,
        "tcs_applicable": null,
        "tds_applicable": null,
        "country_of_supply": null,
        "recon_status": null,
        "flag_for_supply": null,
        "auto_populated_to_refunds": true,
        "supplier_claiming_refund": null,
        "return_period_from_transcation_date": "082019",
        "doc_number": "EX17",
        "document_number": "EX17",
        "sub_type": "DEEMED",
        "original_doc_num": null,
        "doc_date": 1566259200000,
        "is_amended": false,
        "bank_details": null,
        "custom_fields": null,
        "export": {
            "export_type": "DEEMED",
            "shipping_bill_num": null,
            "shipping_port_num": null,
            "shipping_bill_date": null
        },
        "import": {
            "bill_of_entry": null,
            "bill_of_entry_value": null,
            "bill_of_entry_date": null,
            "import_invoice_type": null,
            "port_code": null
        },
        "ecommerce": {
            "ecommerce_operator": null,
            "merchant_id": null
        },
        "version_num": 0
    }
]
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "code": 400,
    "message": "query param invoice_direction must be one of [SALE, PURCHASE]"
}    
```
{% endtab %}
{% endtabs %}

## Add an Invoice

You can add an invoice by submitting a **PUT** request to the GST API:

{% hint style="info" %}
You can cancel an invoice by using the same Add invoice API except changing the request method to **DELETE** instead if **PUT**.
{% endhint %}

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/invoices/{{invoice_id}}?source=USER
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| invoice\_id | Path | String | Required. Unique Transaction ID. |
| source | Query | String | USER |
| invoice | Body | Object | Required. Invoice data in [Invoice Object](invoices.md#resource-objects). |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/invoices/ck9az74tc000pA3b6hb7xbb52b
```

#### Sample Payload

```javascript
{
    "line_items": [
        {
            "cess_rate": "",
            "cess_val": "",
            "cgst_rate": 1.5,
            "cgst_val": 0.15,
            "description": "TESTITEM",
            "discount": "",
            "gst_code": "",
            "gst_type": "GOODS",
            "igst_rate": 0,
            "igst_val": 0,
            "item_id": "",
            "notes": "",
            "quantity": "1",
            "serial_number": 1,
            "sgst_rate": 1.5,
            "sgst_val": 0.15,
            "taxable_val": 10,
            "total_val": 10.3,
            "unit_of_measurement": "BGS",
            "unit_price": "10",
            "taxable_rate": "3"
        }
    ],
    "is_canceled": false,
    "serial_number": "TESTINV1234",
    "is_rate_inclusive_of_tax": false,
    "ref_doc_number": null,
    "transaction_date": "2020-04-22",
    "due_date": "2020-04-22",
    "seller": {
        "name": "Karnataka",
        "gstin": "29AAFCD5862R1ZR",
        "address": "",
        "city": "",
        "state": "KARNATAKA",
        "zip_code": "",
        "country": "",
        "phone_number": "",
        "gstin_business_nature": "REGULAR"
    },
    "receiver": {
        "name": "CUSTOMERNAMEHERE",
        "gstin": "",
        "address": "",
        "city": "",
        "state": "",
        "zip_code": "",
        "country": "",
        "phone_number": ""
    },
    "consignee": {
        "name": "CUSTOMERNAMEHERE",
        "gstin": "",
        "address": "",
        "city": "",
        "state": "",
        "zip_code": "",
        "country": "",
        "phone_number": ""
    },
    "ecommerce": {
        "ecommerce_operator": null,
        "merchant_id": null
    },
    "export": {
        "export_type": "",
        "shipping_bill_date": null,
        "shipping_bill_num": null,
        "shipping_port_num": ""
    },
    "discount_type": "VALUE",
    "place_of_supply": "KARNATAKA",
    "total_cess_val": 0,
    "total_cgst_val": 0.15,
    "total_discount": 0,
    "total_igst_val": 0,
    "total_sgst_val": 0.15,
    "total_taxable_val": 10,
    "total_val": 10.3,
    "reverse_charge_applicable": false,
    "rounding_factor": null,
    "original_invoice_number": null,
    "original_invoice_date": null,
    "original_invoice_gstin": null,
    "return_period": "042020",
    "quarterly_return_period": "132020",
    "receiver_contact_id": null,
    "consignee_contact_id": null,
    "id": "ck9az74tc000pA3b6hb7xbb52b",
    "type": "SALE",
    "source": "USER",
    "version_num": 0,
    "custom_fields": [],
    "bank_details": null,
    "terms_and_conditions": null
}
```

{% tabs %}
{% tab title="200" %}
```javascript
{
    "ref_doc_number": null,
    "due_date": "2020-04-22",
    "paid_on": null,
    "shipping_charge": null,
    "invoice_status": "CREATED",
    "payment_terms": null,
    "notes": null,
    "advance_payments": [
        {
            "document_number": null,
            "document_date": null,
            "adjustment_val": null
        }
    ],
    "isd": {
        "original_supplier": null,
        "isd": null
    },
    "export_currency": null,
    "provisional_itc_claimed": null,
    "conversion_rate": null,
    "total_val_foreign_currency": null,
    "due_balance": 10.30,
    "transaction_payment_status": "UNPAID",
    "cgst_itc_claim_amount": null,
    "sgst_itc_claim_amount": null,
    "igst_itc_claim_amount": null,
    "cess_itc_claim_amount": null,
    "ignored_warnings": null,
    "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
    "id": "ck9az74tc000pA3b6hb7xbb52b",
    "transaction_date": "2020-04-22",
    "return_period": "042020",
    "quarterly_return_period": "132020",
    "source": "USER",
    "total_discount": 0.00,
    "total_taxable_val": 10.00,
    "total_cgst_val": 0.15,
    "total_sgst_val": 0.15,
    "total_igst_val": 0.00,
    "total_cess_val": 0.00,
    "discount_type": "VALUE",
    "total_val": 10.30,
    "gst_status": "NA",
    "gst_validation_errors": null,
    "place_of_supply": "KARNATAKA",
    "updated_at": "2020-04-22",
    "user_updated_at": "2020-04-22",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-04-22",
    "rounding_factor": null,
    "section_name": "B2CS",
    "fiscal_year": "2020",
    "fiscal_month": "APRIL",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.30,
    "date_of_purchase": "2020-04-22",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": "988dc354-3203-4a9f-8b3c-a93223a29ac7",
    "receiver_contact_id": "988dc354-3203-4a9f-8b3c-a93223a29ac7",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": null,
    "serial_number": "TESTINV1234",
    "type": "SALE",
    "original_invoice_number": null,
    "original_invoice_date": null,
    "original_invoice_gstin": null,
    "classification": "B2CS",
    "line_items": [
        {
            "tcs": {
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null
            },
            "tds": {
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null
            },
            "total_val_foreign_currency": null,
            "zero_tax_category": null,
            "item_code": null,
            "gst_code": "",
            "gst_type": "GOODS",
            "description": "TESTITEM",
            "notes": "",
            "unit_price": 10.00,
            "unit_price_including_tax": null,
            "unit_of_measurement": "BGS",
            "item_id": "",
            "serial_number": 1,
            "quantity": 1.0,
            "discount_rate": null,
            "discount": null,
            "taxable_val": 10.00,
            "cgst_rate": 1.50,
            "cgst_val": 0.15,
            "sgst_rate": 1.50,
            "sgst_val": 0.15,
            "igst_rate": 0.00,
            "igst_val": 0.00,
            "cess_rate": 0.00,
            "cess_val": 0.00,
            "total_val": 10.30,
            "customer_billing_gstin": null,
            "itc_details": {
                "itc_type": null,
                "itc_claim_percentage": null,
                "cgst_total_itc": null,
                "sgst_total_itc": null,
                "igst_total_itc": null,
                "cess_total_itc": null,
                "cgst_claimed_itc": null,
                "sgst_claimed_itc": null,
                "igst_claimed_itc": null,
                "cess_claimed_itc": null
            }
        }
    ],
    "seller": {
        "name": "Karnataka",
        "gstin": "29AAFCD5862R1ZR",
        "address": "",
        "city": "",
        "state": "KARNATAKA",
        "zip_code": "",
        "country": "",
        "phone_number": ""
    },
    "receiver": {
        "name": "CUSTOMERNAMEHERE",
        "gstin": "",
        "address": "",
        "city": "",
        "state": null,
        "zip_code": "",
        "country": "",
        "phone_number": ""
    },
    "consignee": {
        "name": "CUSTOMERNAMEHERE",
        "gstin": "",
        "address": "",
        "city": "",
        "state": null,
        "zip_code": "",
        "country": "",
        "phone_number": ""
    },
    "reverse_charge_applicable": false,
    "tcs_applicable": null,
    "tds_applicable": null,
    "country_of_supply": null,
    "recon_status": null,
    "flag_for_supply": null,
    "auto_populated_to_refunds": true,
    "supplier_claiming_refund": null,
    "return_period_from_transcation_date": null,
    "doc_number": "TESTINV1234",
    "document_number": "TESTINV1234",
    "sub_type": null,
    "original_doc_num": null,
    "doc_date": 1587513600000,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "export": {
        "export_type": null,
        "shipping_bill_num": null,
        "shipping_port_num": "",
        "shipping_bill_date": null
    },
    "import": {
        "bill_of_entry": null,
        "bill_of_entry_value": null,
        "bill_of_entry_date": null,
        "import_invoice_type": null,
        "port_code": null
    },
    "ecommerce": {
        "ecommerce_operator": null,
        "merchant_id": null
    },
    "version_num": 0
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "BAD_REQUEST_ATTR",
            "message": "CGST and SGST value should be equal",
            "error_group_code": 0,
            "error_id": 0,
            "severity": "ERROR"
        },
        "err_2": {
            "code": "BAD_REQUEST_ATTR",
            "message": "CGST and SGST rates should be equal",
            "error_group_code": 6,
            "error_id": 6,
            "severity": "ERROR"
        },
        "err_3": {
            "code": "BAD_REQUEST_ATTR",
            "message": "Please use a GST compliant tax rate - [0, 0.05, 0.125, 0.5, 0.75, 1.5, 2.5, 3.75, 6, 9, 14]",
            "error_group_code": 12,
            "error_id": 12,
            "severity": "ERROR"
        }
    },
    "error_sources": {
        "line_items": {
            "0": {
                "cgst_rate": {
                    "error_refs": [
                        "err_3"
                    ]
                }
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Add Invoices

You can add multiple invoices by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/invoicesv2
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/invoicesv2
```

#### Sample Payload

```javascript
[
  {
    "id": "INV-test",
    "serial_number": "INV-test",
    "version_num": 0,
    "transaction_date": "2020-03-15",
    "return_period": "032020",
    "source": "USER",
    "total_discount": 0,
    "total_cgst_val": 10.00,
    "total_sgst_val": 10.00,
    "total_igst_val": 0,
    "total_val": 120,
    "type": "SALE",
    "classification": "B2B",
    "line_items": [
      {
        "quantity": 1,
        "discount": 0,
        "taxable_val": 50,
        "cgst_rate": 6,
        "cgst_val": 5,
        "sgst_rate": 6,
        "sgst_val": 5,
        "igst_rate": 0,
        "igst_val": 0,
        "total_val": 60,
        "serial_number": 1,
        "gst_code": "1011020",
        "gst_type": "GOODS",
        "description": "Pencil"
      },
      {
        "quantity": 1,
        "discount": 0,
        "taxable_val": 50,
        "cgst_rate": 6,
        "cgst_val": 5,
        "sgst_rate": 6,
        "sgst_val": 5,
        "igst_rate": 0,
        "igst_val": 0,
        "total_val": 60,
        "serial_number": 2,
        "gst_code": "1011020",
        "gst_type": "GOODS",
        "description": "Book"
      }
    ],
    "seller": {
      "uuid": "seller-uuid-1",
      "name": "Seller-1",
      "gstin": "29AAFCD5862R1ZR",
      "address": "Street, Road",
      "city": "Bangalore",
      "state": "KARNATAKA",
      "zip_code": "5600002"
    },
    "receiver": {
      "uuid": "receiver-uuid-1",
      "name": "receiver-1",
      "gstin": "",
      "address": "Street, Road",
      "city": "Bangalore",
      "state": "KARNATAKA",
      "zip_code": "5600002"
    },
    "consignee": {
      "uuid": "consignee-uuid-1",
      "name": "consignee-1",
      "gstin": "GSTIn3",
      "address": "Street, Road",
      "city": "Bangalore",
      "state": "KARNATAKA",
      "zip_code": "5600002"
    }
  }
]
```

#### Sample Response

{% hint style="info" %}
This endpoint will send a error details inside 'errorResponse' object with status code 200.
{% endhint %}

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "id": "INV-test",
        "status": true,
        "data": {
            "ref_doc_number": null,
            "due_date": null,
            "paid_on": null,
            "shipping_charge": null,
            "invoice_status": "CREATED",
            "payment_terms": null,
            "notes": null,
            "advance_payments": [
                {
                    "document_number": null,
                    "document_date": null,
                    "adjustment_val": null
                }
            ],
            "isd": {
                "original_supplier": null,
                "isd": null
            },
            "export_currency": null,
            "provisional_itc_claimed": null,
            "conversion_rate": null,
            "total_val_foreign_currency": null,
            "due_balance": 120.00,
            "transaction_payment_status": "UNPAID",
            "cgst_itc_claim_amount": null,
            "sgst_itc_claim_amount": null,
            "igst_itc_claim_amount": null,
            "cess_itc_claim_amount": null,
            "ignored_warnings": null,
            "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
            "id": "INV-test",
            "transaction_date": "2020-03-15",
            "return_period": "032020",
            "quarterly_return_period": "162020",
            "source": "USER",
            "total_discount": 0.00,
            "total_taxable_val": 100.00,
            "total_cgst_val": 10.00,
            "total_sgst_val": 10.00,
            "total_igst_val": 0.00,
            "discount_type": null,
            "total_val": 120.00,
            "gst_status": "NA",
            "gst_validation_errors": null,
            "place_of_supply": "KARNATAKA",
            "updated_at": null,
            "user_updated_at": null,
            "is_amendment": false,
            "amendment_detail": null,
            "uploaded_once": false,
            "is_canceled": false,
            "is_rate_inclusive_of_tax": false,
            "created_at": null,
            "rounding_factor": null,
            "section_name": "B2CS",
            "fiscal_year": "2019",
            "fiscal_month": "MARCH",
            "fiscal_quarter": "Q4",
            "total_tax_value": 20.00,
            "date_of_purchase": "2020-03-15",
            "validate_warnings": false,
            "seller_contact_id": null,
            "consignee_contact_id": null,
            "receiver_contact_id": null,
            "customer_type": "UIN_REGISTERED",
            "supplier_type": null,
            "differential_tax": null,
            "terms_and_conditions": null,
            "serial_number": "INV-test",
            "type": "SALE",
            "original_invoice_number": null,
            "original_invoice_date": null,
            "original_invoice_gstin": null,
            "classification": "B2CS",
            "line_items": [
                {
                    "tcs": {
                        "cgst_rate": null,
                        "cgst_val": null,
                        "sgst_rate": null,
                        "sgst_val": null,
                        "igst_rate": null,
                        "igst_val": null,
                        "cess_rate": null,
                        "cess_val": null
                    },
                    "tds": {
                        "cgst_rate": null,
                        "cgst_val": null,
                        "sgst_rate": null,
                        "sgst_val": null,
                        "igst_rate": null,
                        "igst_val": null,
                        "cess_rate": null,
                        "cess_val": null
                    },
                    "total_val_foreign_currency": null,
                    "zero_tax_category": null,
                    "item_code": null,
                    "gst_code": "01011020",
                    "gst_type": "GOODS",
                    "description": "Pencil",
                    "notes": null,
                    "unit_price": null,
                    "unit_price_including_tax": null,
                    "unit_of_measurement": null,
                    "item_id": null,
                    "serial_number": 1,
                    "quantity": 1.0,
                    "discount_rate": null,
                    "discount": 0.00,
                    "taxable_val": 50.00,
                    "cgst_rate": 6.00,
                    "cgst_val": 5.00,
                    "sgst_rate": 6.00,
                    "sgst_val": 5.00,
                    "igst_rate": 0.00,
                    "igst_val": 0.00,
                    "cess_rate": null,
                    "cess_val": null,
                    "total_val": 60.00,
                    "customer_billing_gstin": null,
                    "itc_details": {
                        "itc_type": null,
                        "itc_claim_percentage": null,
                        "cgst_total_itc": null,
                        "sgst_total_itc": null,
                        "igst_total_itc": null,
                        "cess_total_itc": null,
                        "cgst_claimed_itc": null,
                        "sgst_claimed_itc": null,
                        "igst_claimed_itc": null,
                        "cess_claimed_itc": null
                    }
                },
                {
                    "tcs": {
                        "cgst_rate": null,
                        "cgst_val": null,
                        "sgst_rate": null,
                        "sgst_val": null,
                        "igst_rate": null,
                        "igst_val": null,
                        "cess_rate": null,
                        "cess_val": null
                    },
                    "tds": {
                        "cgst_rate": null,
                        "cgst_val": null,
                        "sgst_rate": null,
                        "sgst_val": null,
                        "igst_rate": null,
                        "igst_val": null,
                        "cess_rate": null,
                        "cess_val": null
                    },
                    "total_val_foreign_currency": null,
                    "zero_tax_category": null,
                    "item_code": null,
                    "gst_code": "01011020",
                    "gst_type": "GOODS",
                    "description": "Book",
                    "notes": null,
                    "unit_price": null,
                    "unit_price_including_tax": null,
                    "unit_of_measurement": null,
                    "item_id": null,
                    "serial_number": 2,
                    "quantity": 1.0,
                    "discount_rate": null,
                    "discount": 0.00,
                    "taxable_val": 50.00,
                    "cgst_rate": 6.00,
                    "cgst_val": 5.00,
                    "sgst_rate": 6.00,
                    "sgst_val": 5.00,
                    "igst_rate": 0.00,
                    "igst_val": 0.00,
                    "cess_rate": null,
                    "cess_val": null,
                    "total_val": 60.00,
                    "customer_billing_gstin": null,
                    "itc_details": {
                        "itc_type": null,
                        "itc_claim_percentage": null,
                        "cgst_total_itc": null,
                        "sgst_total_itc": null,
                        "igst_total_itc": null,
                        "cess_total_itc": null,
                        "cgst_claimed_itc": null,
                        "sgst_claimed_itc": null,
                        "igst_claimed_itc": null,
                        "cess_claimed_itc": null
                    }
                }
            ],
            "seller": {
                "name": "Seller-1",
                "gstin": "29AAFCD5862R1ZR",
                "address": "Street, Road",
                "city": "Bangalore",
                "state": "KARNATAKA",
                "zip_code": "5600002",
                "country": null,
                "phone_number": null
            },
            "receiver": {
                "name": "receiver-1",
                "gstin": "",
                "address": "Street, Road",
                "city": "Bangalore",
                "state": "KARNATAKA",
                "zip_code": "5600002",
                "country": null,
                "phone_number": null
            },
            "consignee": {
                "name": "consignee-1",
                "gstin": "GSTIN3",
                "address": "Street, Road",
                "city": "Bangalore",
                "state": "KARNATAKA",
                "zip_code": "5600002",
                "country": null,
                "phone_number": null
            },
            "reverse_charge_applicable": null,
            "tcs_applicable": null,
            "tds_applicable": null,
            "country_of_supply": null,
            "recon_status": null,
            "flag_for_supply": null,
            "auto_populated_to_refunds": true,
            "supplier_claiming_refund": null,
            "return_period_from_transcation_date": null,
            "document_number": "INV-test",
            "doc_number": "INV-test",
            "doc_date": 1584230400000,
            "sub_type": null,
            "original_doc_num": null,
            "is_amended": false,
            "bank_details": null,
            "custom_fields": null,
            "export": {
                "export_type": null,
                "shipping_bill_num": null,
                "shipping_port_num": null,
                "shipping_bill_date": null
            },
            "import": {
                "bill_of_entry": null,
                "bill_of_entry_value": null,
                "bill_of_entry_date": null,
                "import_invoice_type": null,
                "port_code": null
            },
            "ecommerce": {
                "ecommerce_operator": null,
                "merchant_id": null
            },
            "version_num": 0
        },
        "errorResponse": null,
        "warningResponse": null
    }
]
```
{% endtab %}

{% tab title="200\(error response\)" %}
```
...

"errorResponse": {
            "errors": {
                "err_1": {
                    "code": "BAD_REQUEST_ATTR",
                    "message": "60000 must be between 0.0  and 100.0.",
                    "error_group_code": 0,
                    "error_id": 0,
                    "severity": "ERROR"
                },
                "err_2": {
                    "code": "BAD_REQUEST_ATTR",
                    "message": "Please use a GST compliant tax rate - [0, 0.05, 0.125, 0.5, 0.75, 1.5, 2.5, 3.75, 6, 9, 14]",
                    "error_group_code": 12,
                    "error_id": 12,
                    "severity": "ERROR"
                }
            },
            "error_sources": {
                "line_items": {
                    "0": {
                        "sgst_rate": {
                            "error_refs": [
                                "err_1",
                                "err_2"
                            ]
                        }
                    }
                }
            }
        },
        
...
```
{% endtab %}
{% endtabs %}

## Canceling or Deleting an Invoice

#### Canceling an Invoice

You can cancel a sales invoice by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add an Invoice](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/invoices#add-an-invoice) section.

{% hint style="info" %}
Note: The status of the invoice will be "cancelled" when this action is performed.
{% endhint %}

{% hint style="danger" %}
You can cancel ONLY a sales invoice. A purchase invoice cannot be canceled but only be deleted.
{% endhint %}

#### Deleting an Invoice

You can delete a purchase invoice by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in  [Add an Invoice](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/invoices#add-an-invoice) section. In addition to the following request parameter.

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| delete | query | Boolean | Mandatory, if you want to delete a  document. Value: true |

