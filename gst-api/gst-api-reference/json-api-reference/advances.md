---
description: >-
  You can create advance receipts (towards outward supply) or advance payments
  (towards inward supply).
---

# Advances

## Add a Advance

The request and response objects are same as [invoice objects](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/invoices#invoice-object).

You can add an advance receipt or an advance payment by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/advance_payments/{{advance_payment_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| advance\_payment\_id | Path | String | Required. Unique advance payment ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/advance_payments/ck9uzrsp100083b6cu3glr4u9
```

#### Sample Request Payload

{% tabs %}
{% tab title="200" %}
```javascript
{
    "line_items": [
        {
            "cgst_rate": 2.5,
            "description": "pencil",
            "gst_type": "GOODS",
            "notes": "pencil boxes",
            "quantity": "1",
            "serial_number": 1,
            "sgst_rate": 2.5,
            "taxable_val": 5,
            "total_val": 5.26,
            "unit_of_measurement": "BOX",
            "unit_price": 5,
            "taxable_rate": 5
        }
    ],
    "transaction_date": "2020-05-06",
    "due_date": "2020-05-06",
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
        "name": "test1",
        "gstin": "",
        "state": "KARNATAKA",
        "country": "INDIA",
        "phone_number": ""
    },
    "consignee": {
        "name": "test1",
        "gstin": "",
        "state": "KARNATAKA",
        "country": "INDIA",
        "phone_number": ""
    },
    "place_of_supply": "KARNATAKA",
    "total_taxable_val": 5,
    "total_val": 5.26,
    "return_period": "052020",
    "quarterly_return_period": "132020",
    "document_number": "123",
    "id": "ck9uzrsp100083b6cu3glr4u9",
    "type": "SALE",
    "source": "USER"
}
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "document_number": "123",
    "line_items": [
        {
            "tcs": null,
            "tds": null,
            "total_val_foreign_currency": null,
            "zero_tax_category": null,
            "item_code": null,
            "gst_code": null,
            "gst_type": "GOODS",
            "description": "pencil",
            "notes": "pencil boxes",
            "unit_price": 5.00,
            "unit_price_including_tax": null,
            "unit_of_measurement": "BOX",
            "item_id": null,
            "serial_number": 1,
            "quantity": 1.0,
            "discount_rate": null,
            "discount": null,
            "taxable_val": 5.00,
            "cgst_rate": 2.50,
            "cgst_val": 0.13,
            "sgst_rate": 2.50,
            "sgst_val": 0.13,
            "igst_rate": null,
            "igst_val": null,
            "cess_rate": null,
            "cess_val": null,
            "total_val": 5.26,
            "customer_billing_gstin": null,
            "itc_details": null
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
        "name": "test1",
        "gstin": "",
        "address": "",
        "city": "",
        "state": "KARNATAKA",
        "zip_code": "",
        "country": "INDIA",
        "phone_number": ""
    },
    "consignee": {
        "name": "test1",
        "gstin": "",
        "address": "",
        "city": "",
        "state": "KARNATAKA",
        "zip_code": "",
        "country": "INDIA",
        "phone_number": ""
    },
    "type": "SALE",
    "original_invoice_serial_num": null,
    "original_invoice_date": null,
    "original_document_number": null,
    "original_document_date": null,
    "reverse_charge_applicable": null,
    "against_bill_of_supply": null,
    "notes": null,
    "ignored_warnings": null,
    "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
    "id": "ck9uzrsp100083b6cu3glr4u9",
    "transaction_date": "2020-05-06",
    "return_period": "052020",
    "quarterly_return_period": "132020",
    "source": null,
    "total_taxable_val": 5.00,
    "total_cgst_val": 0.13,
    "total_sgst_val": 0.13,
    "discount_type": null,
    "total_val": 5.26,
    "gst_status": "NA",
    "gst_validation_errors": null,
    "place_of_supply": "KARNATAKA",
    "updated_at": "2020-05-21",
    "user_updated_at": "2020-05-21",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-05-06",
    "rounding_factor": null,
    "section_name": "AT",
    "fiscal_year": "2020",
    "due_balance": null,
    "transaction_payment_status": null,
    "fiscal_month": "MAY",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.25,
    "date_of_purchase": "2020-05-06",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
    "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": null,
    "original_doc_num": null,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "version_num": 8
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
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
                "cgst_val": {
                    "error_refs": [
                        "err_1"
                    ]
                },
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

## Get Advances

You can get advance receipts or an advance payments by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/advance_payments?{{return_period}}=MMYYY
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
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
| start | Query | String | Default: 0 /used for pagination |
| limit | Query | String | Default: 20 / number of invoices to limit in the response |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/advance_payments?fiscal_year=2020&invoice_direction=SALE
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "document_number": "123",
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
                "description": "pencil",
                "notes": "pencil boxes",
                "unit_price": 5.00,
                "unit_price_including_tax": null,
                "unit_of_measurement": "BOX",
                "item_id": "ck9uzfzh100043b6ceixxirrk",
                "serial_number": 1,
                "quantity": 1.0,
                "discount_rate": null,
                "discount": 0.00,
                "taxable_val": 5.00,
                "cgst_rate": 2.50,
                "cgst_val": 0.13,
                "sgst_rate": 2.50,
                "sgst_val": 0.13,
                "igst_rate": 0.00,
                "igst_val": 0.00,
                "cess_rate": 0.00,
                "cess_val": 0.00,
                "total_val": 5.26,
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
            "name": "test1",
            "gstin": "",
            "address": null,
            "city": null,
            "state": "KARNATAKA",
            "zip_code": null,
            "country": "INDIA",
            "phone_number": ""
        },
        "consignee": {
            "name": "test1",
            "gstin": "",
            "address": null,
            "city": null,
            "state": "KARNATAKA",
            "zip_code": null,
            "country": "INDIA",
            "phone_number": ""
        },
        "type": "SALE",
        "original_invoice_serial_num": null,
        "original_invoice_date": null,
        "original_document_number": null,
        "original_document_date": null,
        "reverse_charge_applicable": false,
        "against_bill_of_supply": null,
        "notes": null,
        "ignored_warnings": null,
        "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
        "id": "ck9uzrsp100083b6cu3glr4u9",
        "transaction_date": "2020-05-06",
        "return_period": "052020",
        "quarterly_return_period": "132020",
        "source": null,
        "total_discount": 0.00,
        "total_taxable_val": 5.00,
        "total_cgst_val": 0.13,
        "total_sgst_val": 0.13,
        "total_igst_val": 0.00,
        "total_cess_val": 0.00,
        "discount_type": "VALUE",
        "total_val": 5.26,
        "gst_status": "NA",
        "gst_validation_errors": null,
        "place_of_supply": "KARNATAKA",
        "updated_at": "2020-05-06",
        "user_updated_at": "2020-05-06",
        "is_amendment": false,
        "amendment_detail": null,
        "uploaded_once": false,
        "is_canceled": false,
        "is_rate_inclusive_of_tax": false,
        "created_at": "2020-05-06",
        "rounding_factor": null,
        "section_name": "AT",
        "fiscal_year": "2020",
        "due_balance": null,
        "transaction_payment_status": null,
        "fiscal_month": "MAY",
        "fiscal_quarter": "Q1",
        "total_tax_value": 0.26,
        "date_of_purchase": "2020-05-06",
        "validate_warnings": false,
        "seller_contact_id": null,
        "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "customer_type": "UIN_REGISTERED",
        "supplier_type": null,
        "differential_tax": null,
        "terms_and_conditions": null,
        "original_doc_num": null,
        "is_amended": false,
        "bank_details": null,
        "custom_fields": null,
        "version_num": 0
    }
]
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": [
        "query param invoice_direction may not be null"
    ]
}
```
{% endtab %}
{% endtabs %}

## Get an Advance

You can get an advance receipt or an advance payment by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}api/v0.1/taxable_entities/{{taxable_entity_id}}/advance_payments/{{advance_payment_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| advance\_payment\_id | Path | String | Required. Unique advance payment ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/advance_payments/ck9uzrsp100083b6cu3glr4u9
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
    {
        "document_number": "123",
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
                "description": "pencil",
                "notes": "pencil boxes",
                "unit_price": 5.00,
                "unit_price_including_tax": null,
                "unit_of_measurement": "BOX",
                "item_id": "ck9uzfzh100043b6ceixxirrk",
                "serial_number": 1,
                "quantity": 1.0,
                "discount_rate": null,
                "discount": 0.00,
                "taxable_val": 5.00,
                "cgst_rate": 2.50,
                "cgst_val": 0.13,
                "sgst_rate": 2.50,
                "sgst_val": 0.13,
                "igst_rate": 0.00,
                "igst_val": 0.00,
                "cess_rate": 0.00,
                "cess_val": 0.00,
                "total_val": 5.26,
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
            "name": "test1",
            "gstin": "",
            "address": null,
            "city": null,
            "state": "KARNATAKA",
            "zip_code": null,
            "country": "INDIA",
            "phone_number": ""
        },
        "consignee": {
            "name": "test1",
            "gstin": "",
            "address": null,
            "city": null,
            "state": "KARNATAKA",
            "zip_code": null,
            "country": "INDIA",
            "phone_number": ""
        },
        "type": "SALE",
        "original_invoice_serial_num": null,
        "original_invoice_date": null,
        "original_document_number": null,
        "original_document_date": null,
        "reverse_charge_applicable": false,
        "against_bill_of_supply": null,
        "notes": null,
        "ignored_warnings": null,
        "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
        "id": "ck9uzrsp100083b6cu3glr4u9",
        "transaction_date": "2020-05-06",
        "return_period": "052020",
        "quarterly_return_period": "132020",
        "source": null,
        "total_discount": 0.00,
        "total_taxable_val": 5.00,
        "total_cgst_val": 0.13,
        "total_sgst_val": 0.13,
        "total_igst_val": 0.00,
        "total_cess_val": 0.00,
        "discount_type": "VALUE",
        "total_val": 5.26,
        "gst_status": "NA",
        "gst_validation_errors": null,
        "place_of_supply": "KARNATAKA",
        "updated_at": "2020-05-06",
        "user_updated_at": "2020-05-06",
        "is_amendment": false,
        "amendment_detail": null,
        "uploaded_once": false,
        "is_canceled": false,
        "is_rate_inclusive_of_tax": false,
        "created_at": "2020-05-06",
        "rounding_factor": null,
        "section_name": "AT",
        "fiscal_year": "2020",
        "due_balance": null,
        "transaction_payment_status": null,
        "fiscal_month": "MAY",
        "fiscal_quarter": "Q1",
        "total_tax_value": 0.26,
        "date_of_purchase": "2020-05-06",
        "validate_warnings": false,
        "seller_contact_id": null,
        "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "customer_type": "UIN_REGISTERED",
        "supplier_type": null,
        "differential_tax": null,
        "terms_and_conditions": null,
        "original_doc_num": null,
        "is_amended": false,
        "bank_details": null,
        "custom_fields": null,
        "version_num": 0
    }
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": [
        "query param invoice_direction may not be null"
    ]
}
```
{% endtab %}
{% endtabs %}

## Canceling or Deleting an Advance

#### Canceling an Advance

You can cancel a sales advance by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add an advance](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/advances#add-a-advance-payment) section.

{% hint style="info" %}
Note: The status of the advance will be "cancelled" when this action is performed.
{% endhint %}

{% hint style="danger" %}
You can cancel ONLY a sales advance. A purchase advance cannot be canceled but only be deleted.
{% endhint %}

#### Deleting a purchase advance

You can delete a purchase advance by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add an advance](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/advances#add-a-advance-payment) section. In addition to the following request parameter.

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| delete | query | Boolean | Mandatory, if you want to delete a document. Value: true |

