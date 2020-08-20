# Value Add APIs

{% hint style="warning" %}
**Coming soon**: These APIs are currently **NOT** available in the staging environment.
{% endhint %}

## Validating Invoice

API for validating transaction details for selected invoices based on Transaction Search Filter. 

### Request URL

Request URL contains following path parameters.

* `owner_id`: UUID corresponding to a user

```text
PUT {host}/v1/{owner_id}/transactions/validate_transaction/
```

### Request Parameters

Mandatory fields: 

* any one of **`validate_e_invoice`**, **`validate_gst_invoice`**, **`validate_ewb_invoice`** and
* any one of **`transaction_id` or `validation_status`** are mandatory

| Query Param | Description | Example |
| :--- | :--- | :--- |
| transaction\_id | Transaction Identifier | 891382d2-4041-4503-89f8-61696f30c0ee |
| validation\_status | Validation status of Transaction | INVALID\_EINVOICE |
| validate\_e\_invoice | Validate whether selected are valid e-invoice | true |
| validate\_gst\_invoice | Validate whether selected are valid GST-Invoice | true |
| validate\_ewb\_invoice | Validate whether selected are valid EWB Invoices | false |

### Sample Response

Valid Response:

```text
[
    {
        "owner_id": "891382d2-4041-4503-89f8-61696f30c0ee",
        "transaction_id": "891382d2-4041-4503-89f8-61696f30c0ee",
        "document": {
            "transaction_details": {
                "category": "B2B",
                "regular_or_reverse_charge": "RG",
                "transaction_type": "REG",
                "is_ecommerce_transaction": true,
                "ecommerce_gstin": "37BZNPM9430M1KL"
            },
            "document_details": {
                "type": "INV",
                "no": "5b247bc4-3c5e-11",
                "date": "2019-05-12",
                "original_invoice_no": null
            },
            "seller_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "buyer_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "dispatch_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "shipping_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "line_items": [
                {
                    "product_name": "WHEAT AND MESLIN",
                    "product_description": "WHEAT AND MESLIN",
                    "hsn_code": "1001",
                    "bar_code": "1212",
                    "quantity": 2,
                    "free_quantity": 1,
                    "unit": "BAG",
                    "unit_price": 100,
                    "total_amount": 200,
                    "discount": 5,
                    "other_charge": 10,
                    "assessable_amount": 205,
                    "sgst_rate": 1,
                    "cgst_rate": 1,
                    "igst_rate": 0,
                    "cess_rate": 1,
                    "cess_non_advol_amount": 10,
                    "state_cess_rate": 2,
                    "total_item_value": 225.25,
                    "batch_details": {
                        "name": "aaa",
                        "expiry_date": "2020-02-01",
                        "warranty_date": "2020-02-20"
                    }
                }
            ],
            "value_details": {
                "total_assessable_value": 10000,
                "total_sgst_value": 1200,
                "total_cgst_value": 1200,
                "total_igst_value": 0,
                "total_cess_value": 0,
                "total_state_cess_value": 0,
                "total_cess_non_advol_value": 0,
                "total_discount_on_invoice": 0,
                "other_charges": 0,
                "total_invoice_value": 12400
            },
            "payment_details": {
                "payee_name": "xlp",
                "payment_mode": "CASH",
                "branch_or_ifsc_code": "IFSC-0012",
                "payment_terms": "Pay before Due Date",
                "payment_instruction": "Pay Via Cash",
                "credit_transfer": "",
                "direct_debit": "",
                "credit_days": 10,
                "balance_amount": 56,
                "payment_due_date": "2017-12-06",
                "account_details": "KeaQbsnmRMhHfErVCEkcH"
            },
            "reference_details": {
                "invoice_remarks": "Valid Invoice",
                "invoice_start_date": "2015-03-02",
                "invoice_end_date": "2013-01-21",
                "preceeding_invoice_no": "",
                "preceeding_invoice_date": "",
                "receipt_advice_no": "",
                "batch_reference_no": "",
                "contract_reference_no": "",
                "any_other_reference": "",
                "project_reference_no": "",
                "purchasers_po_reference_no": ""
            },
            "export_details": {
                "export_category": "DIR",
                "with_payment": "N",
                "shipping_bill_no": "1234",
                "shipping_bill_date": "2019-03-27",
                "shipping_port_code": "INAII6",
                "total_invoice_value_in_foreign_currency": 12,
                "foreign_currency": "USD",
                "country_code": "US"
            }
        },
        "govt_response": null,
        "document_status": "CREATED",
        "validation_statuses": [
            VALID_EINVOICE
        ],
        "error_details": {
            "is_error_response": false,
            "errors": [
            ]
        }
    }
]
```

Invalid Sample Response:

```text
[
    {
        "owner_id": "891382d2-4041-4503-89f8-61696f30c0ee",
        "transaction_id": "71c1001a-1527-4f13-bdf5-4940a739bcb2",
        "document": {
            "transaction_details": {
                "category": "B2B",
                "regular_or_reverse_charge": "RG",
                "transaction_type": "REG",
                "is_ecommerce_transaction": true,
                "ecommerce_gstin": "37BZNPM9430M1KL"
            },
            "document_details": {
                "type": "INV",
                "no": "5b247bc4-3c5e-11",
                "date": "2019-05-12",
                "original_invoice_no": null
            },
            "seller_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "buyer_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "dispatch_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "shipping_details": {
                "gstin": "29AAACG0569P1Z3",
                "trade_name": "AMBIKA CEMENTS",
                "building_no": "1",
                "building_name": "AMBIKA CEMENTS",
                "floor_no": "2",
                "location": "BENGALURU",
                "district": "BANGALURU",
                "pin_code": 560090,
                "state_code": 29,
                "phone": 9898989898,
                "email": "abc123@gmail.com"
            },
            "line_items": [
                {
                    "product_name": "WHEAT AND MESLIN",
                    "product_description": "WHEAT AND MESLIN",
                    "hsn_code": "1001",
                    "bar_code": "1212",
                    "quantity": 2,
                    "free_quantity": 1,
                    "unit": "BAG",
                    "unit_price": 100,
                    "total_amount": 200,
                    "discount": 5,
                    "other_charge": 10,
                    "assessable_amount": 205,
                    "sgst_rate": 1,
                    "cgst_rate": 1,
                    "igst_rate": 0,
                    "cess_rate": 1,
                    "cess_non_advol_amount": 10,
                    "state_cess_rate": 2,
                    "total_item_value": 225.25,
                    "batch_details": {
                        "name": "aaa",
                        "expiry_date": "2020-02-01",
                        "warranty_date": "2020-02-20"
                    }
                }
            ],
            "value_details": {
                "total_assessable_value": 10000,
                "total_sgst_value": 1200,
                "total_cgst_value": 1200,
                "total_igst_value": 0,
                "total_cess_value": 0,
                "total_state_cess_value": 0,
                "total_cess_non_advol_value": 0,
                "total_discount_on_invoice": 0,
                "other_charges": 0,
                "total_invoice_value": 12400
            },
            "payment_details": {
                "payee_name": "xlp",
                "payment_mode": "CASH",
                "branch_or_ifsc_code": "IFSC-0012",
                "payment_terms": "Pay before Due Date",
                "payment_instruction": "Pay Via Cash",
                "credit_transfer": "",
                "direct_debit": "",
                "credit_days": 10,
                "balance_amount": 56,
                "payment_due_date": "2017-12-06",
                "account_details": "KeaQbsnmRMhHfErVCEkcH"
            },
            "reference_details": {
                "invoice_remarks": "Valid Invoice",
                "invoice_start_date": "2015-03-02",
                "invoice_end_date": "2013-01-21",
                "preceeding_invoice_no": "",
                "preceeding_invoice_date": "",
                "receipt_advice_no": "",
                "batch_reference_no": "",
                "contract_reference_no": "",
                "any_other_reference": "",
                "project_reference_no": "",
                "purchasers_po_reference_no": ""
            },
            "export_details": {
                "export_category": null,
                "with_payment": "N",
                "shipping_bill_no": "1234",
                "shipping_bill_date": "2019-03-27",
                "shipping_port_code": "INAII6",
                "total_invoice_value_in_foreign_currency": 12,
                "foreign_currency": "USD",
                "country_code": "US"
            }
        },
        "govt_response": null,
        "document_status": "CREATED",
        "validation_statuses": [
            "INVALID_EINVOICE"
        ],
        "error_details": {
            "is_error_response": true,
            "errors": [
                {
                    "error_code": "1010",
                    "error_message": "Export Category is Mandatory",
                    "error_source": "CTX"
                }
            ]
        }
    }
]
```

## 

