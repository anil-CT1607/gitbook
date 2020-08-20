# Printing Consolidated E-Waybill

You can get PDF version of an E-Waybill by submitting a **GET** request to the E-Waybill API with the following request headers.

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/consolidated_ewb/{{CEWB_NUMBER}}/print
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| cewb\_number | Path | String | Required. This is the Consolidated E-Waybill number. |

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/bf557750-936e-4209-ac46-f3e8426d4780/consolidated_ewb/7313974286/print
```

{% hint style="info" %}
The `content-type` of the response will be  `application/pdf`.
{% endhint %}

#### Sample Response

{% file src="../../../.gitbook/assets/response.pdf" caption="Consolidated EWB Response sample" %}

