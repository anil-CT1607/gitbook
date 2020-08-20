# Printing E-Waybill

You can get PDF version of an E-Waybill by submitting a **POST** request to the E-Waybill API with the following request headers.

#### URL query string:

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/ewaybill/download
```

#### Request Parameters:

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
      <td style="text-align:left">content-type</td>
      <td style="text-align:left">Header</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Mandatory. Application/json</td>
    </tr>
    <tr>
      <td style="text-align:left">taxable_entity_id</td>
      <td style="text-align:left">Path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Required. This is the unique ID associated with the GSTIN in your account.</td>
    </tr>
    <tr>
      <td style="text-align:left">print_type</td>
      <td style="text-align:left">Query</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Optional. Accepted values include BASIC, DETAILED.</p>
        <p>Default: BASIC</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">List</td>
      <td style="text-align:left">Required. List of document IDs. Multiple allowed</td>
    </tr>
  </tbody>
</table>

#### Sample Request:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst/v0.1/taxable_entities/bf557750-936e-4209-ac46-f3e8426d4780/ewaybill/download?print_type=detailed
```

#### Sample Payload

```text
[
    "DOC500"
]
```

#### Sample response

{% file src="../../../.gitbook/assets/basic-2-.pdf" %}

{% file src="../../../.gitbook/assets/detailed-2-.pdf" %}

