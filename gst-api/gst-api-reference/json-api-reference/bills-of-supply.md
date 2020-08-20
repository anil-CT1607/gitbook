# Bills of Supply

A bill of supply is a document of transaction that is different from a normal tax invoice. These bills do not contain any tax amount, as input tax cannot be charged in these cases.

## Resource Objects

### Bill of supply Object

The request and response objects are same as [invoice objects](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/invoices#invoice-object) except the following.

| Parameter | Type | Field Validation | Description |
| :--- | :--- | :--- | :--- |
| supply\_num | String |  | Mandatory. Document Number |

## Get a Bill of Supply

You can get a bill of supply by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/billofsupply/{{bill_of_supply_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| bill\_of\_supply\_id | Path | String | Required. Unique bill of supply ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/billofsupply/INV-test
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
  "supply_num": "billno1234",
  "transaction_date": "2020-05-18",
  "due_date": "2020-05-18",
  "return_period": "082017",
  "quarterly_return_period": "132020",
  "receiver": {
    "gstin": "",
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "country": "INDIA"
  },
  "place_of_supply": "KARNATAKA",
  "consignee": {
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "",
    "country": "INDIA"
  },
  "seller": {
    "name": "Karnataka",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "29AAFCD5862R1ZR",
    "country": ""
  },
  "line_items": [
    {
      "serial_number": 1,
      "description": "box",
      "notes": "",
      "gst_type": "GOODS",
      "gst_code": "",
      "quantity": "1",
      "item_id": "",
      "unit_of_measurement": "CCM",
      "taxable_val": "10",
      "unit_price": "10",
      "discount": "",
      "total_val": "10"
    }
  ],
  "total_discount": "0",
  "total_val": "10",
  "type": "SALE",
  "id": "ckac1wpk9000c3b6cgx8s9710",
  "terms_and_conditions": "no terms and confitions applied",
  "notes": "test notes"
}
```
{% endtab %}

{% tab title="404" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "Bill of supply with id INV-tes does not exist.",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Get Bills of Supply

You can get multiple bill of supply's by submitting a **GET** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/billofsupply?fiscal_year=2020&invoice_direction=SALE
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
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/billofsupply?fiscal_year=2020&invoice_direction=SALE
```

{% hint style="info" %}
If you receive an empty array \[\] in the response with HTTP status code 200, it means there are no invoices in ClearTax matching the filters specified in the query parameters.
{% endhint %}

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
[
  {
    "supply_num": "testbill1",
    "type": "SALE",
    "ref_doc_number": "123",
    "due_date": "2020-04-23",
    "seller": {
      "name": "Karnataka",
      "gstin": "29AAFCD5862R1ZR",
      "address": "",
      "city": "",
      "state": "KARNATAKA",
      "zip_code": "",
      "country": null,
      "phone_number": null
    },
    "receiver": {
      "name": "test1",
      "gstin": "",
      "address": "",
      "city": "",
      "state": "KARNATAKA",
      "zip_code": "",
      "country": null,
      "phone_number": null
    },
    "consignee": {
      "name": "test1",
      "gstin": "",
      "address": "",
      "city": "",
      "state": "KARNATAKA",
      "zip_code": "",
      "country": null,
      "phone_number": null
    },
    "nil_rated_val": null,
    "exempted_val": 10.00,
    "non_gst_supply_val": null,
    "supply_from_composition_dealer_val": null,
    "notes": null,
    "due_balance": 10.00,
    "transaction_payment_status": "UNPAID",
    "line_items": [
      {
        "item_code": null,
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "Pencil",
        "notes": "",
        "unit_price": 10.00,
        "unit_price_including_tax": null,
        "unit_of_measurement": "BOX",
        "item_id": "",
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
        "zero_tax_category": null
      }
    ],
    "ignored_warnings": null,
    "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
    "id": "ck9cjb8oi000c3b6cgzpvm5mz",
    "transaction_date": "2020-04-23",
    "return_period": "042020",
    "quarterly_return_period": "132020",
    "source": "USER",
    "total_discount": 0.00,
    "total_taxable_val": 10.00,
    "discount_type": "VALUE",
    "total_val": 10.00,
    "gst_status": "NA",
    "gst_validation_errors": null,
    "place_of_supply": "KARNATAKA",
    "updated_at": "2020-04-23",
    "user_updated_at": "2020-04-23",
    "is_amendment": false,
    "amendment_detail": null,
    "uploaded_once": false,
    "is_canceled": false,
    "is_rate_inclusive_of_tax": false,
    "created_at": "2020-04-23",
    "rounding_factor": null,
    "section_name": "NIL",
    "fiscal_year": "2020",
    "fiscal_month": "APRIL",
    "fiscal_quarter": "Q1",
    "total_tax_value": 0.00,
    "date_of_purchase": "2020-04-23",
    "validate_warnings": false,
    "seller_contact_id": "",
    "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
    "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
    "customer_type": "UIN_REGISTERED",
    "supplier_type": null,
    "differential_tax": null,
    "terms_and_conditions": null,
    "document_number": "testbill1",
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
    "code": 400,
    "message": "query param invoice_direction must be one of [SALE, PURCHASE]"
}
```
{% endtab %}
{% endtabs %}

## Add a Bill of Supply

You can add a bill of supply by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/billofsupply/{{bill_of_supply_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| bill\_of\_supply\_id | Path | String | Required. Unique bill of supply ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/billofsupply/ck9ck06sr000k3b6cn8l2enrn
```

#### Sample Payload

{% tabs %}
{% tab title="Payload" %}
```javascript
{
  "supply_num": "billno1234",
  "transaction_date": "2020-05-18",
  "due_date": "2020-05-18",
  "return_period": "082017",
  "quarterly_return_period": "132020",
  "receiver": {
    "gstin": "",
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "country": "INDIA"
  },
  "place_of_supply": "KARNATAKA",
  "consignee": {
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "",
    "country": "INDIA"
  },
  "seller": {
    "name": "Karnataka",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "29AAFCD5862R1ZR",
    "country": ""
  },
  "line_items": [
    {
      "serial_number": 1,
      "description": "box",
      "notes": "",
      "gst_type": "GOODS",
      "gst_code": "",
      "quantity": "1",
      "item_id": "",
      "unit_of_measurement": "CCM",
      "taxable_val": "10",
      "unit_price": "10",
      "discount": "",
      "total_val": "10"
    }
  ],
  "total_discount": "0",
  "total_val": "10",
  "type": "SALE",
  "id": "ckac1wpk9000c3b6cgx8s9710",
  "terms_and_conditions": "no terms and confitions applied",
  "notes": "test notes"
}
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="201" %}
```javascript
    {
        "supply_num": "BOS123",
        "type": "SALE",
        "ref_doc_number": "123",
        "due_date": "2020-04-23",
        "seller": {
            "name": "Karnataka",
            "gstin": "29AAFCD5862R1ZR",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "receiver": {
            "name": "test1",
            "gstin": "",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "consignee": {
            "name": "test1",
            "gstin": "",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "nil_rated_val": null,
        "exempted_val": 20.00,
        "non_gst_supply_val": null,
        "supply_from_composition_dealer_val": null,
        "notes": null,
        "due_balance": 20.00,
        "transaction_payment_status": "UNPAID",
        "line_items": [
            {
                "item_code": null,
                "gst_code": "",
                "gst_type": "GOODS",
                "description": "box",
                "notes": "",
                "unit_price": 20.00,
                "unit_price_including_tax": null,
                "unit_of_measurement": "BDL",
                "item_id": "",
                "serial_number": 1,
                "quantity": 1.0,
                "discount_rate": null,
                "discount": null,
                "taxable_val": 20.00,
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null,
                "total_val": 20.00,
                "customer_billing_gstin": null,
                "zero_tax_category": null
            }
        ],
        "ignored_warnings": null,
        "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
        "id": "ck9ck06sr000k3b6cn8l2enrn",
        "transaction_date": "2020-04-23",
        "return_period": "042020",
        "quarterly_return_period": "132020",
        "source": "USER",
        "total_discount": 0.00,
        "total_taxable_val": 20.00,
        "discount_type": "VALUE",
        "total_val": 20.00,
        "gst_status": "NA",
        "gst_validation_errors": null,
        "place_of_supply": "KARNATAKA",
        "updated_at": "2020-06-09",
        "user_updated_at": "2020-06-09",
        "is_amendment": false,
        "amendment_detail": null,
        "uploaded_once": false,
        "is_canceled": false,
        "is_rate_inclusive_of_tax": false,
        "created_at": "2020-04-23",
        "rounding_factor": null,
        "section_name": "NIL",
        "fiscal_year": "2020",
        "fiscal_month": "APRIL",
        "fiscal_quarter": "Q1",
        "total_tax_value": 0.00,
        "date_of_purchase": "2020-04-23",
        "validate_warnings": false,
        "seller_contact_id": "",
        "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "customer_type": "UIN_REGISTERED",
        "supplier_type": null,
        "differential_tax": null,
        "terms_and_conditions": null,
        "document_number": "BOS123",
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
    "errors": {
        "err_1": {
            "code": "400",
            "message": "Unable to parse 200-04-23 as yyyy-MM-dd",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "due_date": {
            "error_refs": [
                "err_1"
            ]
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Add Bills of Supply

You can add multiple bills of supply by submitting a **PUT** request to the GST API:

#### URL Query String

```text
{{HOST}}/api/v0.1/taxable_entities/{{taxable_entity_id}}/billofsupply
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249baf74-7392-4fa2-b3a0-685c6c7ad87e/billofsupply
```

#### Sample Payload

{% tabs %}
{% tab title="200" %}
```javascript
[
{
  "supply_num": "billno1234",
  "transaction_date": "2020-05-18",
  "due_date": "2020-05-18",
  "return_period": "082017",
  "quarterly_return_period": "132020",
  "receiver": {
    "gstin": "",
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "country": "INDIA"
  },
  "place_of_supply": "KARNATAKA",
  "consignee": {
    "name": "test",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "",
    "country": "INDIA"
  },
  "seller": {
    "name": "Karnataka",
    "address": "",
    "city": "",
    "state": "KARNATAKA",
    "zip_code": "",
    "gstin": "29AAFCD5862R1ZR",
    "country": ""
  },
  "line_items": [
    {
      "serial_number": 1,
      "description": "box",
      "notes": "",
      "gst_type": "GOODS",
      "gst_code": "",
      "quantity": "1",
      "item_id": "",
      "unit_of_measurement": "CCM",
      "taxable_val": "10",
      "unit_price": "10",
      "discount": "",
      "total_val": "10"
    }
  ],
  "total_discount": "0",
  "total_val": "10",
  "type": "SALE",
  "id": "ckac1wpk9000c3b6cgx8s9710",
  "terms_and_conditions": "no terms and confitions applied",
  "notes": "test notes"
}
]
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="201" %}
```javascript
[
    {
        "supply_num": "BOS123",
        "type": "SALE",
        "ref_doc_number": "123",
        "due_date": "2020-04-23",
        "seller": {
            "name": "Karnataka",
            "gstin": "29AAFCD5862R1ZR",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "receiver": {
            "name": "test1",
            "gstin": "",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "consignee": {
            "name": "test1",
            "gstin": "",
            "address": "",
            "city": "",
            "state": "KARNATAKA",
            "zip_code": "",
            "country": null,
            "trade_name": null,
            "phone_number": null
        },
        "nil_rated_val": null,
        "exempted_val": 20.00,
        "non_gst_supply_val": null,
        "supply_from_composition_dealer_val": null,
        "notes": null,
        "due_balance": 20.00,
        "transaction_payment_status": "UNPAID",
        "line_items": [
            {
                "item_code": null,
                "gst_code": "",
                "gst_type": "GOODS",
                "description": "box",
                "notes": "",
                "unit_price": 20.00,
                "unit_price_including_tax": null,
                "unit_of_measurement": "BDL",
                "item_id": "",
                "serial_number": 1,
                "quantity": 1.0,
                "discount_rate": null,
                "discount": null,
                "taxable_val": 20.00,
                "cgst_rate": null,
                "cgst_val": null,
                "sgst_rate": null,
                "sgst_val": null,
                "igst_rate": null,
                "igst_val": null,
                "cess_rate": null,
                "cess_val": null,
                "total_val": 20.00,
                "customer_billing_gstin": null,
                "zero_tax_category": null
            }
        ],
        "ignored_warnings": null,
        "owner": "249baf74-7392-4fa2-b3a0-685c6c7ad87e",
        "id": "ck9ck06sr000k3b6cn8l2enrn",
        "transaction_date": "2020-04-23",
        "return_period": "042020",
        "quarterly_return_period": "132020",
        "source": "USER",
        "total_discount": 0.00,
        "total_taxable_val": 20.00,
        "discount_type": "VALUE",
        "total_val": 20.00,
        "gst_status": "NA",
        "gst_validation_errors": null,
        "place_of_supply": "KARNATAKA",
        "updated_at": "2020-06-09",
        "user_updated_at": "2020-06-09",
        "is_amendment": false,
        "amendment_detail": null,
        "uploaded_once": false,
        "is_canceled": false,
        "is_rate_inclusive_of_tax": false,
        "created_at": "2020-04-23",
        "rounding_factor": null,
        "section_name": "NIL",
        "fiscal_year": "2020",
        "fiscal_month": "APRIL",
        "fiscal_quarter": "Q1",
        "total_tax_value": 0.00,
        "date_of_purchase": "2020-04-23",
        "validate_warnings": false,
        "seller_contact_id": "",
        "consignee_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "receiver_contact_id": "227d5bd5-2eac-471a-a6cf-0a711b7e02e2",
        "customer_type": "UIN_REGISTERED",
        "supplier_type": null,
        "differential_tax": null,
        "terms_and_conditions": null,
        "document_number": "BOS123",
        "original_doc_num": null,
        "is_amended": false,
        "bank_details": null,
        "custom_fields": null,
        "version_num": 1
    }
]
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "400",
            "message": "Cannot deserialize indian state from key KARNATKA",
            "error_group_code": 0,
            "error_id": 0
        }
    },
    "error_sources": {
        "null": {
            "0": {
                "seller": {
                    "state": {
                        "error_refs": [
                            "err_1"
                        ]
                    }
                }
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Canceling or deleting Bill of Supply

#### Canceling a Bill of supply

You can cancel a sales bill of supply  by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in [Add a Bill of Supply](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/bills-of-supply#add-a-bill-of-supply) section.

{% hint style="info" %}
Note: The status of the Bill of supply will be "cancelled" when this action is performed.
{% endhint %}

{% hint style="danger" %}
You can cancel ONLY a sales bill of supply. A purchase bill of supply cannot be canceled but only be deleted.
{% endhint %}

#### Deleting a bill of supply

You can delete a purchase bill of supply by submitting a **`DELETE`** request to the GST API where the request URL and headers remain same as in  [Add a Bill of Supply](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/json-api-reference/bills-of-supply#add-a-bill-of-supply) section. In addition to the following request parameter.

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| delete | query | Boolean | Mandatory, if you want to delete a  document. Value: true |

