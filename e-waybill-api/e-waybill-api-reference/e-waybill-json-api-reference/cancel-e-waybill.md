# Cancelling E-Waybill

The cancel E-Waybill API takes reference of generated E-Waybill through ClearTax and cancels the generated E-Waybill.

Using this API, Maximum of 5 E-Waybills can be cancelled per request.

E-Waybill can be cancelled by submitting a **PUT** request to the E-Waybill API with the following request headers.

{% hint style="warning" %}
**Note:**

1. E-way bills can be cancelled by the generator of such e-way bills only.
2. The time-limit to cancel is within 24 hours of generating the e-way bill.
3. Once canceled, it is illegal to use such E-Way Bill.
4. If the e-Way Bill verified by any empowered officer it **cannot be** canceled.
{% endhint %}

#### URL query string

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewb_activity/CANCEL_EWB
```

#### Sample Payload

```text
{
  "ewb_client_ids": [
    "E-Waybill ID"
  ], 
  "cancel_reason": "DUPLICATE", 
  "remark": "string"
}
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| ewb\_client\_ids | Body | List | Required. List of unique IDs of E-Waybill on ClearTax. |
| cancel\_reason | Body | Enum | Required. Allowed enums include DUPLICATE, ORDER\_CANCELLED, DATA\_ENTRY\_MISTAKE, OTHERS. |
| remark | Body | String | Required. Remarks for cancellation. |

{% hint style="info" %}
Cancellation of E-Waybill depends on the business rules set by the Government.
{% endhint %}

#### Sample Response

{% code title="200" %}
```javascript
[
    {
        ...
        ...
        "ewb_number": "161001660902",
        "ewb_generated_date": "22-08-2019 12:01:00",
        "ewb_valid_from_date": "22-08-2019 12:01:00",
        "ewb_due_date": "23-08-2019 23:59:00",
        "ewb_govt_sync_status": "COMPLETE",
        "other_val": 0.00,
        "total_cess_non_advol_val": 0.00,
        "is_multi_vehicle": false,
        "ewb_status": "CANCELLED",
       ...
       ...
    }
]
```
{% endcode %}

{% hint style="info" %}
In case of any error the API will return status code 200 but the body will be blank.
{% endhint %}



