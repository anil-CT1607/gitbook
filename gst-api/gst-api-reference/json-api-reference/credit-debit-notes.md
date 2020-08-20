# Credit Debit Notes \(CDN\)

When goods supplied are returned or when there is a revision in the invoice value due to goods \(or services\) not being up to the mark or extra goods being issued a Debit Note or Credit Note is issued.

## Resource Objects

### Credit debit note Object

The request and response objects are same as [invoice objects](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/invoices#invoice-object) except the following.

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| cdn\_status | String |  | Is the document created? |
| cdn\_type | String | \[CREDIT, DEBIT\] | Mandatory. |
| original\_invoice\_serial\_num | String |  | Mandatory. Original invoice document number against which this CDN is raised. |
| original\_invoice\_date | String |  | Mandatory. Original invoice data |
| original\_note\_number | String |  | Conditional. Original note number, mandatory if you are amending a CDN |
| original\_note\_date | String |  | Conditional. Original note date,  mandatory if you are amending a CDN |
| note\_num | String |  | Mandatory. CDN number |
| transaction\_date | String |  | Mandatory. Credit note issued date |

## Get a CDN

You can get a CDN  by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/cdns/{{cdn_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| cdn\_id | Path | String | Required. Unique CDN ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/cdns/ck9kyln2a00063b6nqqcgfrkd
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "ignored_warnings": null,
    "owner": "0a694afd-b756-44a3-b2ef-79acc4a0aa9f",
    "id": "ckacfqk1u00063b6aw1mwh4u7",
    "transaction_date": "2020-05-18",
    "return_period": "052020",
    "quarterly_return_period": "132020",
    "source": "USER",
    "total_discount": 0.00,
    "total_taxable_val": 10.00,
    "total_cgst_val": 0.00,
    "total_sgst_val": 0.00,
    "total_igst_val": 0.00,
    "total_cess_val": 0.00,
    "discount_type": "VALUE",
    "total_val": 10.00,
    "gst_status": "NA",
    "gst_validation_errors": null,
    "place_of_supply": "KARNATAKA",
    "updated_at": "2020-05-18",
    "user_updated_at": "2020-05-18",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-05-18",
    "rounding_factor": null,
    "section_name": "B2CS",
    "fiscal_year": "2020",
    "due_balance": null,
    "transaction_payment_status": null,
    "fiscal_month": "MAY",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.00,
    "date_of_purchase": "2020-05-18",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": "2512ac2a-728b-421c-b333-eb06bf9d8fa2",
    "receiver_contact_id": "2512ac2a-728b-421c-b333-eb06bf9d8fa2",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": "terms here",
    "original_invoice_classification": "B2CS",
    "export_type": null,
    "import_type": null,
    "return_period_from_transcation_date": "052020",
    "linked_sales_invoice_category": null,
    "linked_purchase_invoice_category": null,
    "inward_supply_type": null,
    "note_num": "testcreditnote",
    "original_note_number": "",
    "original_note_gstin": "",
    "original_note_date": null,
    "original_invoice_serial_num": "123",
    "original_invoice_date": "2020-05-14",
    "original_invoice_type": "SALE",
    "reason": null,
    "cdn_type": "CREDIT",
    "differential_val": 10.00,
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
        "total_val_foreign_currency": null,
        "zero_tax_category": null,
        "item_code": null,
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "item1",
        "notes": "",
        "unit_price": 10.00,
        "unit_price_including_tax": null,
        "unit_of_measurement": "CCM",
        "item_id": "",
        "serial_number": 1,
        "quantity": 1.0,
        "discount_rate": null,
        "discount": null,
        "taxable_val": 10.00,
        "cgst_rate": 0.00,
        "cgst_val": 0.00,
        "sgst_rate": 0.00,
        "sgst_val": 0.00,
        "igst_rate": 0.00,
        "igst_val": 0.00,
        "cess_rate": 0.00,
        "cess_val": 0.00,
        "total_val": 10.00,
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
      "name": "test",
      "gstin": "",
      "address": "",
      "city": "",
      "state": null,
      "zip_code": "",
      "country": "",
      "phone_number": ""
    },
    "consignee": {
      "name": "test",
      "gstin": "",
      "address": "",
      "city": "",
      "state": null,
      "zip_code": "",
      "country": "",
      "phone_number": ""
    },
    "reverse_charge_applicable": false,
    "pre_gst": null,
    "recon_status": null,
    "flag_for_supply": null,
    "auto_populated_to_refunds": true,
    "supplier_claiming_refund": null,
    "notes": "customer notes here",
    "cdn_status": "CREATED",
    "export_currency": null,
    "conversion_rate": null,
    "total_val_foreign_currency": null,
    "country_of_supply": null,
    "provisional_itc_claimed": null,
    "cgst_itc_claim_amount": 0.00,
    "sgst_itc_claim_amount": 0.00,
    "igst_itc_claim_amount": 0.00,
    "cess_itc_claim_amount": 0.00,
    "linked_transaction_client_id": "cka6iio0800063b6i8f7nsekr",
    "linked_transaction_type": "INVOICE",
    "ref_doc_number": null,
    "doc_number": "testcreditnote",
    "document_number": "testcreditnote",
    "original_doc_num": "",
    "doc_date": 1589760000000,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "export": null,
    "import": null,
    "ecommerce": {
      "ecommerce_operator": null,
      "merchant_id": null
    },
    "version_num": 1
  }
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "Credit/Debit note with id Test123 does not exist.",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endtab %}
{% endtabs %}

## GET CDNs

You can get multiple CDNs by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/cdns?return_period=MMYYYY
```

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
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/cdns?id=ck9kyln2a00063b6nqqcgfrkd&invoice_direction=sale
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
[
{
    "ignored_warnings": null,
    "owner": "0a694afd-b756-44a3-b2ef-79acc4a0aa9f",
    "id": "ckacfqk1u00063b6aw1mwh4u7",
    "transaction_date": "2020-05-18",
    "return_period": "052020",
    "quarterly_return_period": "132020",
    "source": "USER",
    "total_discount": 0.00,
    "total_taxable_val": 10.00,
    "total_cgst_val": 0.00,
    "total_sgst_val": 0.00,
    "total_igst_val": 0.00,
    "total_cess_val": 0.00,
    "discount_type": "VALUE",
    "total_val": 10.00,
    "gst_status": "NA",
    "gst_validation_errors": null,
    "place_of_supply": "KARNATAKA",
    "updated_at": "2020-05-18",
    "user_updated_at": "2020-05-18",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-05-18",
    "rounding_factor": null,
    "section_name": "B2CS",
    "fiscal_year": "2020",
    "due_balance": null,
    "transaction_payment_status": null,
    "fiscal_month": "MAY",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.00,
    "date_of_purchase": "2020-05-18",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": "2512ac2a-728b-421c-b333-eb06bf9d8fa2",
    "receiver_contact_id": "2512ac2a-728b-421c-b333-eb06bf9d8fa2",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": "terms here",
    "original_invoice_classification": "B2CS",
    "export_type": null,
    "import_type": null,
    "return_period_from_transcation_date": "052020",
    "linked_sales_invoice_category": null,
    "linked_purchase_invoice_category": null,
    "inward_supply_type": null,
    "note_num": "testcreditnote",
    "original_note_number": "",
    "original_note_gstin": "",
    "original_note_date": null,
    "original_invoice_serial_num": "123",
    "original_invoice_date": "2020-05-14",
    "original_invoice_type": "SALE",
    "reason": null,
    "cdn_type": "CREDIT",
    "differential_val": 10.00,
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
        "total_val_foreign_currency": null,
        "zero_tax_category": null,
        "item_code": null,
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "item1",
        "notes": "",
        "unit_price": 10.00,
        "unit_price_including_tax": null,
        "unit_of_measurement": "CCM",
        "item_id": "",
        "serial_number": 1,
        "quantity": 1.0,
        "discount_rate": null,
        "discount": null,
        "taxable_val": 10.00,
        "cgst_rate": 0.00,
        "cgst_val": 0.00,
        "sgst_rate": 0.00,
        "sgst_val": 0.00,
        "igst_rate": 0.00,
        "igst_val": 0.00,
        "cess_rate": 0.00,
        "cess_val": 0.00,
        "total_val": 10.00,
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
      "name": "test",
      "gstin": "",
      "address": "",
      "city": "",
      "state": null,
      "zip_code": "",
      "country": "",
      "phone_number": ""
    },
    "consignee": {
      "name": "test",
      "gstin": "",
      "address": "",
      "city": "",
      "state": null,
      "zip_code": "",
      "country": "",
      "phone_number": ""
    },
    "reverse_charge_applicable": false,
    "pre_gst": null,
    "recon_status": null,
    "flag_for_supply": null,
    "auto_populated_to_refunds": true,
    "supplier_claiming_refund": null,
    "notes": "customer notes here",
    "cdn_status": "CREATED",
    "export_currency": null,
    "conversion_rate": null,
    "total_val_foreign_currency": null,
    "country_of_supply": null,
    "provisional_itc_claimed": null,
    "cgst_itc_claim_amount": 0.00,
    "sgst_itc_claim_amount": 0.00,
    "igst_itc_claim_amount": 0.00,
    "cess_itc_claim_amount": 0.00,
    "linked_transaction_client_id": "cka6iio0800063b6i8f7nsekr",
    "linked_transaction_type": "INVOICE",
    "ref_doc_number": null,
    "doc_number": "testcreditnote",
    "document_number": "testcreditnote",
    "original_doc_num": "",
    "doc_date": 1589760000000,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "export": null,
    "import": null,
    "ecommerce": {
      "ecommerce_operator": null,
      "merchant_id": null
    },
    "version_num": 1
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

## Add a CDN

You can add a CDN by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/cdns/{{cdn_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| cdn\_id | Path | String | Required. Unique CDN ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/cdns/ck9kyln2a00063b6nqqcgfrkd
```

#### Sample Request Payload

{% tabs %}
{% tab title="200" %}
```javascript
{
  "line_items": [
    {
      "cess_rate": "",
      "cgst_rate": 0,
      "description": "pencil",
      "gst_type": "GOODS",
      "igst_rate": 0,
      "quantity": "1",
      "serial_number": 1,
      "sgst_rate": 0,
      "taxable_val": 10,
      "total_val": 10,
      "unit_of_measurement": "BOX",
      "unit_price": "10"
    }
  ],
  "cdn_type": "DEBIT",
  "transaction_date": "2020-04-29",
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
    "gstin": "",
    "address": "Street, Road",
    "city": "Bangalore",
    "state": "KARNATAKA",
    "zip_code": "5600002",
    "country": null,
    "phone_number": null
  },
  "place_of_supply": "KARNATAKA",
  "differential_val": 10,
  "total_val": 10,
  "reverse_charge_applicable": false,
  "rounding_factor": null,
  "original_invoice_serial_num": "INV-test",
  "original_invoice_date": "2020-03-15",
  "original_invoice_gstin": "",
  "original_note_number": "",
  "original_note_date": null,
  "original_note_gstin": "",
  "return_period": "042020",
  "quarterly_return_period": "132020",
  "note_num": "12fgh3",
  "linked_transaction_client_id": "INV-test",
  "id": "ck9kyln2a00063b6nqqcgfrkd",
  "type": "SALE",
  "source": "USER",
  "original_invoice_type": "SALE"
}
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "ignored_warnings": null,
    "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
    "id": "ck9kyln2a00063b6nqqcgfrkd",
    "transaction_date": "2020-04-29",
    "return_period": "042020",
    "quarterly_return_period": "132020",
    "source": "USER",
    "total_taxable_val": 10.00,
    "total_cgst_val": 0.00,
    "total_sgst_val": 0.00,
    "total_igst_val": 0.00,
    "total_cess_val": 0.00,
    "discount_type": null,
    "total_val": 10.00,
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
    "created_at": "2020-04-29",
    "rounding_factor": null,
    "section_name": "B2CS",
    "fiscal_year": "2020",
    "due_balance": null,
    "transaction_payment_status": null,
    "fiscal_month": "APRIL",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.00,
    "date_of_purchase": "2020-04-29",
    "validate_warnings": false,
    "seller_contact_id": null,
    "consignee_contact_id": "5ab54e93-bd29-4dbb-903f-db21e012ecea",
    "receiver_contact_id": "5ab54e93-bd29-4dbb-903f-db21e012ecea",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": null,
    "original_invoice_classification": "B2CS",
    "export_type": null,
    "import_type": null,
    "return_period_from_transcation_date": null,
    "linked_sales_invoice_category": null,
    "linked_purchase_invoice_category": null,
    "inward_supply_type": null,
    "note_num": "12fgh3",
    "original_note_number": "",
    "original_note_gstin": "",
    "original_note_date": null,
    "original_invoice_serial_num": "INV-test",
    "original_invoice_date": "2020-03-15",
    "original_invoice_type": "SALE",
    "reason": null,
    "cdn_type": "DEBIT",
    "differential_val": 10.00,
    "line_items": [
        {
            "tcs": null,
            "total_val_foreign_currency": null,
            "zero_tax_category": null,
            "item_code": null,
            "gst_code": null,
            "gst_type": "GOODS",
            "description": "pencil",
            "notes": null,
            "unit_price": 10.00,
            "unit_price_including_tax": null,
            "unit_of_measurement": "BOX",
            "item_id": null,
            "serial_number": 1,
            "quantity": 1.0,
            "discount_rate": null,
            "discount": null,
            "taxable_val": 10.00,
            "cgst_rate": 0.00,
            "cgst_val": 0.00,
            "sgst_rate": 0.00,
            "sgst_val": 0.00,
            "igst_rate": 0.00,
            "igst_val": 0.00,
            "cess_rate": 0.00,
            "cess_val": 0.00,
            "total_val": 10.00,
            "customer_billing_gstin": null,
            "itc_details": null
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
        "gstin": "",
        "address": "Street, Road",
        "city": "Bangalore",
        "state": "KARNATAKA",
        "zip_code": "5600002",
        "country": null,
        "phone_number": null
    },
    "reverse_charge_applicable": false,
    "pre_gst": null,
    "recon_status": null,
    "flag_for_supply": null,
    "auto_populated_to_refunds": true,
    "supplier_claiming_refund": null,
    "notes": null,
    "cdn_status": "CREATED",
    "export_currency": null,
    "conversion_rate": null,
    "total_val_foreign_currency": null,
    "country_of_supply": null,
    "provisional_itc_claimed": null,
    "cgst_itc_claim_amount": null,
    "sgst_itc_claim_amount": null,
    "igst_itc_claim_amount": null,
    "cess_itc_claim_amount": null,
    "linked_transaction_client_id": "INV-test",
    "linked_transaction_type": "INVOICE",
    "ref_doc_number": null,
    "doc_number": "12fgh3",
    "document_number": "12fgh3",
    "original_doc_num": "",
    "doc_date": 1588118400000,
    "is_amended": false,
    "bank_details": null,
    "custom_fields": null,
    "export": null,
    "import": null,
    "ecommerce": {
        "ecommerce_operator": null,
        "merchant_id": null
    },
    "version_num": 11
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "400",
            "message": "Unable to parse 202-03-15 as yyyy-MM-dd",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "original_invoice_date": {
            "error_refs": [
                "err_1"
            ]
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Add CDNs

You can add multiple CDNs  by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/taxable_entity_id/cdnsv2
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/cdns/ck9kyln2a00063b6nqqcgfrkd
```

#### Sample Request Payload

{% tabs %}
{% tab title="200" %}
```javascript
[
{
  "line_items": [
    {
      "description": "pencil",
      "gst_type": "GOODS",
      "quantity": "1",
      "serial_number": 1,
      "taxable_val": 10,
      "total_val": 10,
      "unit_of_measurement": "BOX",
      "unit_price": "10"
    }
  ],
  "cdn_type": "CREDIT",
  "transaction_date": "2020-04-29",
  "seller": {
    "name": "Seller-1",
    "gstin": "29AAFCD5862R1ZR",
    "address": "Street, Road",
    "city": "Bangalore",
    "state": "KARNATAKA",
    "zip_code": "5600002"
  },
  "receiver": {
    "name": "receiver-1",
    "gstin": "",
    "address": "Street, Road",
    "city": "Bangalore",
    "state": "KARNATAKA",
    "zip_code": "5600002"
  },
  "consignee": {
    "name": "consignee-1",
    "gstin": "",
    "address": "Street, Road",
    "city": "Bangalore",
    "state": "KARNATAKA",
    "zip_code": "5600002"
  },
  "place_of_supply": "KARNATAKA",
  "differential_val": 10,
  "total_val": 10,
  "original_invoice_serial_num": "123",
  "original_invoice_date": "2020-05-11",
  "original_invoice_gstin": "",
  "original_note_number": "",
  "original_note_date": null,
  "original_note_gstin": "",
  "return_period": "042020",
  "quarterly_return_period": "132020",
  "note_num": "12sfgh3",
  "linked_transaction_client_id": "INV-test",
  "id": "ck9kyjln2a00063b6nqqcgfrkd",
  "type": "SALE",
  "source": "USER",
  "original_invoice_type": "SALE"
}
]
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "id": "ck9kyjln2a00063b6nqqcgfrkd",
        "status": CREATED,
        "data": {
            "ignored_warnings": null,
            "owner": "d2155258-76e8-49a0-93a5-e00983c13c8d",
            "id": "ck9kyjln2a00063b6nqqcgfrkd",
            "transaction_date": "2020-04-29",
            "return_period": "042020",
            "quarterly_return_period": "132020",
            "source": "USER",
            "total_taxable_val": 10.00,
            "discount_type": null,
            "total_val": 10.00,
            "gst_status": "STAGED",
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
            "section_name": null,
            "fiscal_year": "2020",
            "due_balance": null,
            "transaction_payment_status": null,
            "fiscal_month": "APRIL",
            "fiscal_quarter": "Q1",
            "total_tax_value": 0.00,
            "date_of_purchase": "2020-04-29",
            "validate_warnings": false,
            "seller_contact_id": null,
            "consignee_contact_id": null,
            "receiver_contact_id": null,
            "customer_type": "UIN_REGISTERED",
            "supplier_type": null,
            "differential_tax": null,
            "terms_and_conditions": null,
            "original_invoice_classification": null,
            "export_type": null,
            "import_type": null,
            "return_period_from_transcation_date": null,
            "linked_sales_invoice_category": null,
            "linked_purchase_invoice_category": null,
            "inward_supply_type": null,
            "note_num": "12sfgh3",
            "original_note_number": "",
            "original_note_gstin": "",
            "original_note_date": null,
            "original_invoice_serial_num": "123",
            "original_invoice_date": "2020-05-11",
            "original_invoice_type": "SALE",
            "reason": null,
            "cdn_type": "CREDIT",
            "differential_val": 10.00,
            "line_items": [
                {
                    "tcs": null,
                    "total_val_foreign_currency": null,
                    "zero_tax_category": null,
                    "item_code": null,
                    "gst_code": null,
                    "gst_type": "GOODS",
                    "description": "pencil",
                    "notes": null,
                    "unit_price": 10.00,
                    "unit_price_including_tax": null,
                    "unit_of_measurement": "BOX",
                    "item_id": null,
                    "serial_number": 1,
                    "quantity": 1.0,
                    "discount_rate": null,
                    "discount": null,
                    "taxable_val": 10.00,
                    "cgst_rate": null,
                    "cgst_val": null,
                    "sgst_rate": null,
                    "sgst_val": null,
                    "igst_rate": null,
                    "igst_val": null,
                    "cess_rate": null,
                    "cess_val": null,
                    "total_val": 10.00,
                    "customer_billing_gstin": null,
                    "itc_details": null
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
                "gstin": "",
                "address": "Street, Road",
                "city": "Bangalore",
                "state": "KARNATAKA",
                "zip_code": "5600002",
                "country": null,
                "phone_number": null
            },
            "reverse_charge_applicable": null,
            "pre_gst": null,
            "recon_status": null,
            "flag_for_supply": null,
            "auto_populated_to_refunds": true,
            "supplier_claiming_refund": null,
            "notes": null,
            "cdn_status": null,
            "export_currency": null,
            "conversion_rate": null,
            "total_val_foreign_currency": null,
            "country_of_supply": null,
            "provisional_itc_claimed": null,
            "cgst_itc_claim_amount": null,
            "sgst_itc_claim_amount": null,
            "igst_itc_claim_amount": null,
            "cess_itc_claim_amount": null,
            "linked_transaction_client_id": "INV-test",
            "linked_transaction_type": "INVOICE",
            "ref_doc_number": null,
            "document_number": "12sfgh3",
            "doc_number": "12sfgh3",
            "original_doc_num": "",
            "doc_date": 1588118400000,
            "is_amended": false,
            "bank_details": null,
            "custom_fields": null,
            "export": null,
            "import": null,
            "ecommerce": null,
            "version_num": null
        },
        "errorResponse": null
        "warningResponse": null
    }
]
```
{% endtab %}
{% endtabs %}

## Canceling or Deleting a CDN

#### Canceling a CDN

You can cancel a sales CDN  by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add a CDN](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/credit-debit-notes#add-a-cdn) section.

{% hint style="info" %}
Note: The status of the CDN will be "cancelled" when this action is performed.
{% endhint %}

{% hint style="danger" %}
You can cancel ONLY a sales CDN. A purchase CDN cannot be canceled but only be deleted.
{% endhint %}

#### Deleting a CDN

You can delete a purchase CDN by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add a CDN](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/credit-debit-notes#add-a-cdn) section. In addition to the following request parameter.

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| delete | query | Boolean | Mandatory, if you want to delete a  document. Value: true |

