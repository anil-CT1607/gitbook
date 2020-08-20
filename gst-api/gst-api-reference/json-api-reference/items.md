# Items

ClearTax Items API provides you the ability to manage your inventory or stock on your ClearTax account.

#### Item Object

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Item\_code | String | Client Item/SKU code |
| gst\_code | String | Item HSN code |
| gst\_type | String | GOODS/SERVICE |
| description | String | Item description |
| notes | String | Item notes |
| unit\_price | String | Item unit price in Rupees |
| unit\_of\_measurement | String | Refer [Unit master](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/resources-and-masters/unit-of-measurement-master) |
| id | String | Mandatory. Item unique ID |

## Get an Item

You can get all the contact details by submitting a **GET** request to the GST API with the following request headers

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/{{business_id}}/items/{{item_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| item\_id | Path | String | Unique item ID of the item |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/businesses/f33961ec-1c1a-461d-b888-8a5a56577a14/items/ck9uyejks00033b6cketziohz
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
  {
        "item_code": "",
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "penc",
        "notes": "",
        "unit_price": null,
        "unit_price_including_tax": null,
        "unit_of_measurement": "",
        "id": "ck2a41dju00073b6akqkr71tp",
        "unit_cost": null,
        "unit_cost_including_tax": null,
        "discount": 0.00,
        "tax_rate": 0.00,
        "cess_rate": null,
        "cess_val": null,
        "inventory": [
            {
                "opening_quantity": null,
                "opening_price": null,
                "current_quantity": null,
                "safety_stock": null,
                "track_inventory": false,
                "taxable_entity_id": "249baf74-7392-4fa2-b3a0-685c6c7ad87e"
            }
        ],
        "is_active": true,
        "group": null
    }

```
{% endtab %}
{% endtabs %}

## Get all Items

You can get all the contact details by submitting a **GET** request to the GST API with the following request headers

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
```

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/business_id/items?override_pagination=true
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| item\_id | Path | String | Unique item ID of the item |
| override\_pagination | Path | Boolean | Ignores the default limit of 20 in the response |
| item\_ids | Path | String | Unique Item ID |
| item\_codes | Path | String | Item code |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/businesses/f33961ec-1c1a-461d-b888-8a5a56577a14/items?override_pagination=true
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```text
  [
  {
        "item_code": "",
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "penc",
        "notes": "",
        "unit_price": null,
        "unit_price_including_tax": null,
        "unit_of_measurement": "",
        "id": "ck2a41dju00073b6akqkr71tp",
        "unit_cost": null,
        "unit_cost_including_tax": null,
        "discount": 0.00,
        "tax_rate": 0.00,
        "cess_rate": null,
        "cess_val": null,
        "inventory": [
            {
                "opening_quantity": null,
                "opening_price": null,
                "current_quantity": null,
                "safety_stock": null,
                "track_inventory": false,
                "taxable_entity_id": "249baf74-7392-4fa2-b3a0-685c6c7ad87e"
            }
        ],
        "is_active": true,
        "group": null
    }
]
```
{% endtab %}
{% endtabs %}

## Add/Update an Item

You can get all the contact details by submitting a **PUT** request to the GST API with the following request headers

```text
X-Cleartax-Auth-Token: <USER_AUTH_TOKEN>
```

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/business_id/items/item_id
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| item\_id | Path | String | Unique item ID of the item |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/businesses/f33961ec-1c1a-461d-b888-8a5a56577a14/items/ck9uyejks00033b6cketziohz
```

#### Sample Payload

```text
{
    "item_code": "",
    "gst_code": "",
    "gst_type": "GOODS",
    "description": "pencil",
    "unit_of_measurement": "BOX",
    "id": "ck9uzfzh100043b6ceixxirrk",
    "unit_price": "05",
    "unit_price_including_tax": "",
    "unit_cost": "10",
    "unit_cost_including_tax": "",
    "tax_rate": "5",
    "cess_val": "",
    "is_price_including_tax": "",
    "discount": "",
    "notes": "pencil boxes"
}
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```text
  {
        "item_code": "",
        "gst_code": "",
        "gst_type": "GOODS",
        "description": "penc",
        "notes": "",
        "unit_price": null,
        "unit_price_including_tax": null,
        "unit_of_measurement": "",
        "id": "ck2a41dju00073b6akqkr71tp",
        "unit_cost": null,
        "unit_cost_including_tax": null,
        "discount": 0.00,
        "tax_rate": 0.00,
        "cess_rate": null,
        "cess_val": null,
        "inventory": [
            {
                "opening_quantity": null,
                "opening_price": null,
                "current_quantity": null,
                "safety_stock": null,
                "track_inventory": false,
                "taxable_entity_id": "249baf74-7392-4fa2-b3a0-685c6c7ad87e"
            }
        ],
        "is_active": true,
        "group": null
    }
```
{% endtab %}
{% endtabs %}

