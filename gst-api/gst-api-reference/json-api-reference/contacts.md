---
description: >-
  ClearTax Contacts API provides you the ability to manage your customers or
  vendors on your ClearTax account.
---

# Contacts

## Get all Contacts

You can get all the contact details by submitting a **GET** request to the GST API with the following request headers

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/{{business_id}}/contacts?override_pagination=true
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Mandatory. This is the unique ID associated with the GSTIN in your account. |
| override\_pagination | Query | Boolean | Unique contact ID. |
| start | Query | String | Default: 0 /used for pagination |
| limit | Query | String | Default: 20 / number of contacts to limit in the response |
| email | Query | String | Email ID of the user |
| pan\_number | Query | String | Pan number of the user |
| mobile\_number | Query | String | Mobile number of the user |
| contact\_id | Query | String | Unique Contact ID of the user |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/businesses/f33961ec-1c1a-461d-b888-8a5a56577a14/contacts?override_pagination=true
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
[
    {
        "id": "1fde8896-b288-4d0d-a037-9f3cd3447852",
        "business_name": "Apple Inc",
        "nick_name": "Apple Inc(OT)",
        "gstin": "29ALSPT0208L1ZI",
        "organization_type": "COMPANY",
        "state": "OTHERTERRITORY",
        "country": "INDIA",
        "system_generated": true
    }
]
```
{% endtab %}
{% endtabs %}

#### Contact Objects

| Parameters | Type | Description |
| :--- | :--- | :--- |
| id | String | Mandatory. Unique Contact ID |
| business\_name | String | Mandatory. Business Name given |
| nick\_name | String | Nick name given |
| gstin | String | GSTIN number of the contact |
| organization\_type | String | Mandatory. Organization type of the contact \['COMPANY', 'INDIVIDUAL'\] |
| state | String | Mandatory. Refer [State Master](https://cleartax.gitbook.io/cleartax-for-developers/gst-api/gst-api-reference/resources-and-masters/place-is-supply-master) |
| country | String | Country |

## Get a Contact

You can get a contact details by submitting a **GET** request to the GST API with the following request headers

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/{{business_id}}/contacts/{{contact_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| contact\_id | Path | String | Required. Unique contact ID. |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/taxable_entities/249af74-7392-4fa2-b3a0-685c6c7ad87e/cdns/ck9kyln2a00063b6nqqcgfrkd
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "id": "1fde896-b288-4d0d-a037-9f3cd3447852",
    "business_name": "Apple Inc",
    "nick_name": "Apple Inc(OT)",
    "gstin": "29ALSPT0208L1ZI",
    "organization_type": "COMPANY",
    "state": "OTHERTERRITORY",
    "country": "INDIA",
    "system_generated": true
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "404",
            "message": "Customer doesn't exist",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Create/Update a Contact

You can get all the contact details by submitting a **PUT** request to the GST API with the following request headers

#### URL Query String

```text
{{HOST}}/api/v0.1/businesses/{{business_id}}/contacts/{{contact_id}}
```

#### Request Parameter

| Parameters | Parameters Type | Type | Description |
| :--- | :--- | :--- | :--- |
| business\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| contact\_id | Path | String | Unique Contact ID of the user |

#### Sample Request

```text
https://gst.cleartax.in/api/v0.1/businesses/f33961ec-1c1a-461d-b888-8a5a56577a14/contacts/dd7fc145-d263-4ef5-a2d6-d193e99ba12e
```

#### Sample Payload

```javascript
{
    "id": "dd7fc145-d263-4ef5-a2d6-d193e99ba12e",
    "business_name": "Star International FZC",
    "nick_name": "International FZCO(OT)",
    "gstin": "",
    "state": "OTHERTERRITORY",
    "organization_type": "COMPANY",
    "contact_person_name": "",
    "email": "",
    "mobile_number": "",
    "land_line_number": "",
    "address": "",
    "city": "",
    "zip_code": "",
    "pan_number": "",
    "country": "INDIA"
}
```

#### Sample Response

{% tabs %}
{% tab title="200" %}
```javascript
{
    "id": "dd7fc145-d263-4ef5-a2d6-d193e99ba12e",
    "business_name": "Blue Star International FZC",
    "nick_name": "Blue Star International FZC(OT)",
    "gstin": "",
    "organization_type": "COMPANY",
    "contact_person_name": "",
    "email": "",
    "pan_number": "",
    "mobile_number": "",
    "land_line_number": "",
    "address": "",
    "city": "",
    "state": "OTHERTERRITORY",
    "zip_code": "",
    "country": "INDIA"
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "errors": {
        "err_1": {
            "code": "BAD_REQUEST_ATTR",
            "message": "This field cannot be empty",
            "error_group_code": 0,
            "error_id": 0,
            "severity": "ERROR"
        }
    },
    "error_sources": {
        "business_name": {
            "error_refs": [
                "err_1"
            ]
        }
    }
}
```
{% endtab %}
{% endtabs %}

