# Government Compatible APIs

{% hint style="warning" %}
The current version of E-Invoicing APIs is based on the Sandbox APIs of the Government. Since the production APIs are not yet released, the current APIs may change any time.

**Subscribe**: To receive an email notification on updates, please subscribe [here](https://forms.gle/YDTpwt5E61xXLWJ47). We'll not spam you :\)
{% endhint %}

These are lightweight APIs that covers the basic functionalities of e-invoicing.  The schema of these services is similar to the Government schema.

## Generating IRN \(with govt schema\)

You can generate an IRN by sending a **`POST`** request to E-Invoicing API with the following request headers.

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/json
Schema-Type: govt_schema_v1.1
owner_id: {{OWNER_ID}}
gstin: {{GSTIN}}
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| Content-Type | Header | String | Mandatory. This will always be  "application/json". |
| Schema-Type | Header | String | Mandatory. Schema type of the request payload. The current version is "govt\_schema\_v1". |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(Account, PAN, GSTIN, Branch\) of the transaction. This will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | GSTIN for which you are generating IRN. |

**Request URL**

```text
POST: {{HOST}}/v1/govt/api/Invoice/
```

**Request Parameters**

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| Version | Body | String | Mandatory. Version. Eg: "1.01" |
| Irn | Body | String | Optional. This is NOT required to be sent in the request payload. |
| TranDtls | Body | Object | Mandatory. Transaction details object. |
| DocDtls | Body | Object | Mandatory. Document details object. |
| SellerDtls | Body | Object | Mandatory. Seller details object. |
| BuyerDtls | Body | Object | Mandatory. Buyer details object. |
| DispDtls | Body | Object | Conditional. Dispatch From details object. Required only if the Dispatch From address is different from Seller Details address. |
| ShipDtls | Body | Object | Conditional. Ship To details object. Required only if the Ship To address is different from Buyer Details address. |
| ItemList | Body | List | Mandatory. List of one or more Item objects. |
| ValDtls | Body | Object | Mandatory. Value details object. |
| PayDtls | Body | Object | Optional. Payment details object. |
| RefDtls | Body | Object | Optional. Reference details object. |
| AddlDocDtls | Body | Object | Optional. Additional Document details object. |
| ExpDtls | Body | Object | Conditional. Export details object. Required only if the document type is Export. |
| EwbDtls | Body | Object | Optional. Eway Bill Details object. |

**Transaction Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">TaxSch</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">minLength: 3
        <br />maxLength: 10</td>
      <td style="text-align:left">Mandatory. Tax Schema. The value should be &quot;GST&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">SupTyp</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3
          <br />maxLength: 10</p>
        <p>enum: &quot;B2B&quot;, &quot;SEZWP&quot;, &quot;SEZWOP&quot;, &quot;EXPWP&quot;,
          &quot;EXPWOP&quot;, &quot;DEXP&quot;</p>
      </td>
      <td style="text-align:left">
        <p>Mandatory. Type of Supply:</p>
        <p>B2B-Business to Business,</p>
        <p>SEZWP - SEZ with payment,</p>
        <p>SEZWOP - SEZ without payment,</p>
        <p>EXPWP - Export with Payment,</p>
        <p>EXPWOP - Export without payment,</p>
        <p>DEXP - Direct EXport</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">RegRev</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1
          <br />maxLength: 1</p>
        <p>enum: &quot;Y&quot;, &quot;N&quot;</p>
      </td>
      <td style="text-align:left">Optional. Y - whether the tax liability is payable under reverse charge.
        Default: N</td>
    </tr>
    <tr>
      <td style="text-align:left">EcmGstin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 15</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;([0-9]{2}[0-9|A-Z]{13})&quot;</p>
      </td>
      <td style="text-align:left">Optional. GSTIN of e-Commerce operator</td>
    </tr>
    <tr>
      <td style="text-align:left">IgstOnIntra</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1
          <br />maxLength: 1</p>
        <p>enum: &quot;Y&quot;, &quot;N&quot;</p>
      </td>
      <td style="text-align:left">Optional. Y - indicates the supply is intrastate but chargeable to IGST.
        Default: N</td>
    </tr>
  </tbody>
</table>

**Document Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Typ</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3
          <br />maxLength: 3
          <br />
        </p>
        <p>enum: &quot;INV&quot;, &quot;CRN&quot;, &quot;DBN&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Document Type: INV-INVOICE, CRN-CREDIT NOTE, DBN-DEBIT NOTE</td>
    </tr>
    <tr>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1
          <br />
        </p>
        <p>maxLength: 16
          <br />
        </p>
        <p>pattern: &quot;^([A-Z1-9]{1}[A-Z0-9/-]{0,15})$&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Document Number. Small case alphabets are NOT allowed in Document
        Number</td>
    </tr>
    <tr>
      <td style="text-align:left">Dt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10,
          <br />
        </p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Document Date</td>
    </tr>
  </tbody>
</table>

**Seller Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Gstin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 15</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;([0-9]{2}[0-9|A-Z]{13})&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Seller GSTIN</td>
    </tr>
    <tr>
      <td style="text-align:left">LglNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Seller Legal Name</td>
    </tr>
    <tr>
      <td style="text-align:left">TrdNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Seller Trade name</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr1</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Seller Building/Flat no, Road/Street</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr2</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Address 2 of the supplier (Floor no., Name of the premises/building)</td>
    </tr>
    <tr>
      <td style="text-align:left">Loc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 50</p>
      </td>
      <td style="text-align:left">Mandatory. Seller Location</td>
    </tr>
    <tr>
      <td style="text-align:left">Pin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 100000</p>
        <p>
          <br />maximum: 999999</p>
      </td>
      <td style="text-align:left">Mandatory. Seller Pincode</td>
    </tr>
    <tr>
      <td style="text-align:left">Stcd</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Mandatory. State Code of the Seller. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/state-master">Refer to the state master.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Ph</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 6</p>
        <p>maxLength: 12</p>
      </td>
      <td style="text-align:left">Optional. Seller Phone or Mobile No.</td>
    </tr>
    <tr>
      <td style="text-align:left">Em</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 6</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Seller Email-Id</td>
    </tr>
  </tbody>
</table>

**Buyer Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Gstin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;^(([0-9]{2}[0-9A-Z]{13})|URP)$&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. GSTIN of the buyer. If the document type is export, then the
        value should be &quot;URP&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">LglNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Buyer Legal Name</td>
    </tr>
    <tr>
      <td style="text-align:left">TrdNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Buyer Trade name</td>
    </tr>
    <tr>
      <td style="text-align:left">Pos</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">minLength: 1, maxLength: 2</td>
      <td style="text-align:left">Mandatory. State code of Place of supply. If POS lies outside the country,
        the code shall be provided. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/country-code-master">Refer to the country code master</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Addr1</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Buyer Building/Flat no, Road/Street</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr2</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Address 2 of the buyer (Floor no., Name of the premises/building)</td>
    </tr>
    <tr>
      <td style="text-align:left">Loc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Buyer Location</td>
    </tr>
    <tr>
      <td style="text-align:left">Pin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 100000</p>
        <p>
          <br />maximum: 999999</p>
      </td>
      <td style="text-align:left">Optional. Buyer Pincode</td>
    </tr>
    <tr>
      <td style="text-align:left">Stcd</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Mandatory. Buyer State code. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/state-master">Refer to the state master.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Ph</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 6</p>
        <p>maxLength: 12</p>
      </td>
      <td style="text-align:left">Optional. Buyer Phone or Mobile No.</td>
    </tr>
    <tr>
      <td style="text-align:left">Em</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 6</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Buyer Email-Id</td>
    </tr>
  </tbody>
</table>

**Dispatch From Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Nm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Name of the company from which the goods are dispatched</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr1</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Address 1 of the entity from which goods are dispatched. (Building/Flat
        No. Road/Street etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr2</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Address 2 of the entity from which goods are dispatched. (Floor
        no., Name of the premises/building)</td>
    </tr>
    <tr>
      <td style="text-align:left">Loc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Location</td>
    </tr>
    <tr>
      <td style="text-align:left">Pin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 100000</p>
        <p>
          <br />maximum: 999999</p>
      </td>
      <td style="text-align:left">Mandatory. Pincode</td>
    </tr>
    <tr>
      <td style="text-align:left">Stcd</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Mandatory. State code. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/state-master">Refer to the state master.</a>
      </td>
    </tr>
  </tbody>
</table>

**Ship To Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Gstin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;^(([0-9]{2}[0-9A-Z]{13})|URP)$&quot;</p>
      </td>
      <td style="text-align:left">Optional. GSTIN of entity to whom goods are shipped. If the document type
        is export, then the value shall be &quot;URP&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left">LglNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Legal Name</td>
    </tr>
    <tr>
      <td style="text-align:left">TrdNm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Trade name</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr1</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Address1 of the entity to whom the supplies are shipped to
        (Building/Flat no., Road/Street etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Addr2</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Address 2 of the entity to whom the supplies are shipped to
        (Floor no., Name of the premises/building)</td>
    </tr>
    <tr>
      <td style="text-align:left">Loc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Mandatory. Place (City, Town, Village) entity to whom the supplies are
        shipped to</td>
    </tr>
    <tr>
      <td style="text-align:left">Pin</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 100000</p>
        <p>
          <br />maximum: 999999</p>
      </td>
      <td style="text-align:left">Mandatory. Pincode</td>
    </tr>
    <tr>
      <td style="text-align:left">Stcd</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Mandatory. State Code to which supplies are shipped to. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/state-master">Refer to the state master</a>.</td>
    </tr>
  </tbody>
</table>

**Item Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">SlNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 6</p>
      </td>
      <td style="text-align:left">Mandatory. Serial Number of Item</td>
    </tr>
    <tr>
      <td style="text-align:left">PrdDesc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 300</p>
      </td>
      <td style="text-align:left">Optional. Product Description</td>
    </tr>
    <tr>
      <td style="text-align:left">IsServc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 1,</p>
        <p>Values: &quot;Y&quot;, &quot;N&quot;</p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Mandatory. Specify whether the supply is service or not. Specify Y-for
          Service</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HsnCd</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 4</p>
        <p>maxLength: 8</p>
      </td>
      <td style="text-align:left">Mandatory. HSN Code</td>
    </tr>
    <tr>
      <td style="text-align:left">Barcde</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 30</p>
      </td>
      <td style="text-align:left">Optional. Bar Code</td>
    </tr>
    <tr>
      <td style="text-align:left">Qty</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 9999999999.999</p>
      </td>
      <td style="text-align:left">Optional. Quantity</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeQty</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minLengthL: 0</p>
        <p>maxLength: 9999999999.999</p>
      </td>
      <td style="text-align:left">Optional. Free Quantity</td>
    </tr>
    <tr>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 8</p>
      </td>
      <td style="text-align:left">
        <p>Optional. Unit</p>
        <p><a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/unit-master">Refer to Unit master.</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UnitPrice</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.999</p>
      </td>
      <td style="text-align:left">Mandatory. Unit Price - Rate</td>
    </tr>
    <tr>
      <td style="text-align:left">TotAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Mandatory. Total Amount (Unit Price * Quantity)</td>
    </tr>
    <tr>
      <td style="text-align:left">Discount</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Discount on line item.</td>
    </tr>
    <tr>
      <td style="text-align:left">PreTaxVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Pre Tax value</td>
    </tr>
    <tr>
      <td style="text-align:left">AssAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Mandatory. Assessable Amount (Total Amount - Discount)</td>
    </tr>
    <tr>
      <td style="text-align:left">GstRt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999.999</p>
      </td>
      <td style="text-align:left">Mandatory. The GST rate, represented as percentage that applies to the
        invoiced item. It will be IGST rate (OR sum of CGST and SGST rates).</td>
    </tr>
    <tr>
      <td style="text-align:left">IgstAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Amount of IGST payable</td>
    </tr>
    <tr>
      <td style="text-align:left">CgstAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Amount of CGST payable</td>
    </tr>
    <tr>
      <td style="text-align:left">SgstAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Amount of SGST payable</td>
    </tr>
    <tr>
      <td style="text-align:left">CesRt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999.999</p>
      </td>
      <td style="text-align:left">Optional. Cess Rate</td>
    </tr>
    <tr>
      <td style="text-align:left">CesAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Cess Amount(advolorem) on basis of rate and quantity of item</td>
    </tr>
    <tr>
      <td style="text-align:left">CesNonAdvlAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Cess Non-Advol Amount</td>
    </tr>
    <tr>
      <td style="text-align:left">StateCesRt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999.999</p>
      </td>
      <td style="text-align:left">Optional. State Cess Rate</td>
    </tr>
    <tr>
      <td style="text-align:left">StateCesAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. State Cess Amount</td>
    </tr>
    <tr>
      <td style="text-align:left">StateCesNonAdvlAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. State CESS Non advol Amount</td>
    </tr>
    <tr>
      <td style="text-align:left">OthChrg</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Other Charges on line item.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotItemVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">
        <p>Mandatory. Total Item Value = AssAmt +</p>
        <p>IgstAmt +
          <br />CgstAmt +</p>
        <p>SgstAmt +</p>
        <p>CesAmt +</p>
        <p>CesNonAdvlAmt +</p>
        <p>StateCesAmt + StateCesNonAdvlAmt +</p>
        <p>OthChrg</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">OrdLineRef</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 50</p>
      </td>
      <td style="text-align:left">Optional. Order line referencee</td>
    </tr>
    <tr>
      <td style="text-align:left">OrgCntry</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 2</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Optional. Origin Country Code. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/country-code-master">Refer to Country master.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PrdSlNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
      </td>
      <td style="text-align:left">Optional. Serial number in case of each item having a unique number.</td>
    </tr>
    <tr>
      <td style="text-align:left">BchDtls</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">List</td>
      <td style="text-align:left">Optional. Batch details object. See below.</td>
    </tr>
    <tr>
      <td style="text-align:left">AttribDtls</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">List</td>
      <td style="text-align:left">Optional. List of one or more Attribute Details object. See below.</td>
    </tr>
  </tbody>
</table>

#### Batch Details

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Nm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">minLength: 3 maxLength: 20</td>
      <td style="text-align:left">Mandatory. Batch number</td>
    </tr>
    <tr>
      <td style="text-align:left">ExpDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. Batch Expiry Date</td>
    </tr>
    <tr>
      <td style="text-align:left">WrDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. Warranty Date</td>
    </tr>
  </tbody>
</table>

#### Attribute Details

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Nm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Attribute details of the item</td>
    </tr>
    <tr>
      <td style="text-align:left">Val</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Attribute details of the item</td>
    </tr>
  </tbody>
</table>

**Value Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">AssVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Mandatory. Total Assessable value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">CgstVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total CGST value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">SgstVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total SGST value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">IgstVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total IGST value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">CesVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total CESS value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">StCesVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total State CESS value of all items</td>
    </tr>
    <tr>
      <td style="text-align:left">Discount</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Total invoice Discount</td>
    </tr>
    <tr>
      <td style="text-align:left">OthChrg</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Other charges</td>
    </tr>
    <tr>
      <td style="text-align:left">RndOffAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99.99</p>
      </td>
      <td style="text-align:left">Optional. Rounding off amount</td>
    </tr>
    <tr>
      <td style="text-align:left">TotInvVal</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Mandatory. Final Invoice value</td>
    </tr>
    <tr>
      <td style="text-align:left">TotInvValFc</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Final Invoice value in Additional Currency</td>
    </tr>
  </tbody>
</table>

**Payment Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Nm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Payee Name</td>
    </tr>
    <tr>
      <td style="text-align:left">AcctDet</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 18</p>
      </td>
      <td style="text-align:left">Optional. Bank account number of payee</td>
    </tr>
    <tr>
      <td style="text-align:left">Mode</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 18</p>
      </td>
      <td style="text-align:left">Optional. Mode of Payment: Cash, Credit, Direct Transfer</td>
    </tr>
    <tr>
      <td style="text-align:left">FinInsBr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 11</p>
      </td>
      <td style="text-align:left">Optional. Branch or IFSC code</td>
    </tr>
    <tr>
      <td style="text-align:left">PayTerm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Terms of Payment</td>
    </tr>
    <tr>
      <td style="text-align:left">PayInstr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Payment Instruction</td>
    </tr>
    <tr>
      <td style="text-align:left">CrTrn</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Credit Transfer</td>
    </tr>
    <tr>
      <td style="text-align:left">DirDr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Direct Debit</td>
    </tr>
    <tr>
      <td style="text-align:left">CrDay</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 9999</p>
      </td>
      <td style="text-align:left">Optional. Credit Days</td>
    </tr>
    <tr>
      <td style="text-align:left">PaidAmt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. The sum of amount which have been paid in advance.</td>
    </tr>
    <tr>
      <td style="text-align:left">PaymtDue</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 0</p>
        <p>maximum: 99999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Outstanding amount that is required to be paid.</td>
    </tr>
  </tbody>
</table>

**Reference Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">InvRm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
        <p>pattern: &quot;^[0-9A-Za-z/-]{3,100}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Invoice Remarks/Notes</td>
    </tr>
    <tr>
      <td style="text-align:left">DocPerdDtls</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional. Document Period Details object.</td>
    </tr>
    <tr>
      <td style="text-align:left">PrecDocDtls</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional. List of one or more Preceding Document Details objects.</td>
    </tr>
    <tr>
      <td style="text-align:left">ContrDtls</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional. List of one or more Contract Details objects.</td>
    </tr>
  </tbody>
</table>

#### Document Period Details Object

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validation</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">InvStDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Invoice Period Start Date</td>
    </tr>
    <tr>
      <td style="text-align:left">InvEndDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Invoice Period End Date</td>
    </tr>
  </tbody>
</table>

#### Preceding Document Details

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">InvNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 16</p>
        <p>pattern: &quot;^[1-9A-Z]{1}[0-9A-Z/-]{1,15}$&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Reference of original invoice, if any</td>
    </tr>
    <tr>
      <td style="text-align:left">InvDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Mandatory. Date of preceding invoice</td>
    </tr>
    <tr>
      <td style="text-align:left">OthRefNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
      </td>
      <td style="text-align:left">Optional. Other Reference</td>
    </tr>
  </tbody>
</table>

#### Contract Details Object

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">RecAdvRef</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,20}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Receipt Advice No.</td>
    </tr>
    <tr>
      <td style="text-align:left">RecAdvDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. Date of Receipt Advice</td>
    </tr>
    <tr>
      <td style="text-align:left">TendRefr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,20}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Lot/Batch Reference No.</td>
    </tr>
    <tr>
      <td style="text-align:left">ContrRefr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,20}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Contract Reference Number</td>
    </tr>
    <tr>
      <td style="text-align:left">ExtRefr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,20}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Any other reference</td>
    </tr>
    <tr>
      <td style="text-align:left">ProjRefr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,20}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Project Reference Number</td>
    </tr>
    <tr>
      <td style="text-align:left">PORefr</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 16</p>
        <p>pattern: &quot;^([0-9A-Za-z/-]){1,16}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. PO Reference Number</td>
    </tr>
    <tr>
      <td style="text-align:left">PORefDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. PO Reference Date</td>
    </tr>
  </tbody>
</table>

#### Additional Document Details Object

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Url</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Supporting document URL</td>
    </tr>
    <tr>
      <td style="text-align:left">Docs</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 1000</p>
      </td>
      <td style="text-align:left">Optional. Supporting document in Base64 format</td>
    </tr>
    <tr>
      <td style="text-align:left">Info</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 1000</p>
      </td>
      <td style="text-align:left">Optional. Any additional InfoDtlsrmation</td>
    </tr>
  </tbody>
</table>

**Export Details Object**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ShipBNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 20</p>
      </td>
      <td style="text-align:left">Optional. Shipping Bill No.</td>
    </tr>
    <tr>
      <td style="text-align:left">ShipBDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. Shipping Bill Date</td>
    </tr>
    <tr>
      <td style="text-align:left">Port</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 2</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;^[0-9A-Za-z]{2,10}$&quot;</p>
      </td>
      <td style="text-align:left">
        <p>Optional. Port Code</p>
        <p><a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/port-code-master">Refer to Port code master</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">RefClm</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 1</p>
        <p>value: &quot;Y&quot;, &quot;N&quot;</p>
      </td>
      <td style="text-align:left">Optional. Claiming refund. Y/N</td>
    </tr>
    <tr>
      <td style="text-align:left">ForCur</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 16</p>
      </td>
      <td style="text-align:left">Optional. Additional Currency Code. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/currency-code-master">Refer to currency master.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CntCode</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 2</p>
        <p>maxLength: 2</p>
      </td>
      <td style="text-align:left">Optional. Country Code. <a href="https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/resources-and-master/country-code-master">Refer to Country master.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ExpDuty</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum&quot;: 0,</p>
        <p>maximum: 999999999999.99</p>
      </td>
      <td style="text-align:left">Optional. Export duty</td>
    </tr>
  </tbody>
</table>

#### Eway Bill Details

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validations</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">TransId</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 15</p>
        <p>maxLength: 15</p>
      </td>
      <td style="text-align:left">Optional. Transin/GSTIN</td>
    </tr>
    <tr>
      <td style="text-align:left">TransName</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Optional. Name of the transporter</td>
    </tr>
    <tr>
      <td style="text-align:left">TransMode</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 1</p>
        <p>enum: [ &quot;1&quot;, &quot;2&quot;, &quot;3&quot;, &quot;4&quot; ]</p>
      </td>
      <td style="text-align:left">Optional. Mode of transport (Road-1, Rail-2, Air-3, Ship-4)</td>
    </tr>
    <tr>
      <td style="text-align:left">Distance</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 1</p>
        <p>maximum: 9999</p>
      </td>
      <td style="text-align:left">
        <p>Mandatory.</p>
        <p>Distance between source and destination PIN codes</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">TransDocNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;^([0-9A-Z/-]){1,15}$&quot;</p>
      </td>
      <td style="text-align:left">Optional. Tranport Document Number</td>
    </tr>
    <tr>
      <td style="text-align:left">TransDocDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Optional. Transport Document Date</td>
    </tr>
    <tr>
      <td style="text-align:left">VehNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 4</p>
        <p>maxLength: 20</p>
      </td>
      <td style="text-align:left">Optional. Vehicle Number</td>
    </tr>
    <tr>
      <td style="text-align:left">VehType</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 1</p>
        <p>enum: [ &quot;O&quot;, &quot;R&quot; ]</p>
      </td>
      <td style="text-align:left">Optional. Whether O-ODC or R-Regular</td>
    </tr>
  </tbody>
</table>

**Sample Request Body**

```text
{
  "Version": "1.01",
  "TranDtls": {
    "TaxSch": "GST",
    "SupTyp": "B2B",
    "RegRev": "Y",
    "EcmGstin": null,
    "IgstOnIntra": "N"
  },
  "DocDtls": {
    "Typ": "INV",
    "No": "DOC/007",
    "Dt": "08/08/2020"
  },
  "SellerDtls": {
    "Gstin": "24AAFCD5862R005",
    "LglNm": "NIC company pvt ltd",
    "TrdNm": "NIC Industries",
    "Addr1": "5th block, kuvempu layout",
    "Addr2": "kuvempu layout",
    "Loc": "GANDHINAGAR",
    "Pin": 382010,
    "Stcd": "24",
    "Ph": "9000000000",
    "Em": "abc@gmail.com"
  },
  "BuyerDtls": {
    "Gstin": "29AWGPV7107B1Z1",
    "LglNm": "XYZ company pvt ltd",
    "TrdNm": "XYZ Industries",
    "Pos": "12",
    "Addr1": "7th block, kuvempu layout",
    "Addr2": "kuvempu layout",
    "Loc": "GANDHINAGAR",
    "Pin": 562160,
    "Stcd": "29",
    "Ph": "91111111111",
    "Em": "xyz@yahoo.com"
  },
  "DispDtls": {
    "Nm": "ABC company pvt ltd",
    "Addr1": "7th block, kuvempu layout",
    "Addr2": "kuvempu layout",
    "Loc": "Banagalore",
    "Pin": 562160,
    "Stcd": "29"
  },
  "ShipDtls": {
    "Gstin": "29AWGPV7107B1Z1",
    "LglNm": "CBE company pvt ltd",
    "TrdNm": "kuvempu layout",
    "Addr1": "7th block, kuvempu layout",
    "Addr2": "kuvempu layout",
    "Loc": "Banagalore",
    "Pin": 562160,
    "Stcd": "29"
  },
  "ItemList": [
    {
      "SlNo": "1",
      "PrdDesc": "Rice",
      "IsServc": "N",
      "HsnCd": "1001",
      "Barcde": "123456",
      "Qty": 100.345,
      "FreeQty": 10,
      "Unit": "BAG",
      "UnitPrice": 99.545,
      "TotAmt": 9988.84,
      "Discount": 10,
      "PreTaxVal": 1,
      "AssAmt": 9978.84,
      "GstRt": 12.0,
      "IgstAmt": 1197.46,
      "CgstAmt": 0,
      "SgstAmt": 0,
      "CesRt": 5,
      "CesAmt": 498.94,
      "CesNonAdvlAmt": 10,
      "StateCesRt": 12,
      "StateCesAmt": 1197.46,
      "StateCesNonAdvlAmt": 5,
      "OthChrg": 10,
      "TotItemVal": 12897.7,
      "OrdLineRef": "3256",
      "OrgCntry": "AG",
      "PrdSlNo": "12345",
      "BchDtls": {
        "Nm": "123456",
        "ExpDt": "01/08/2020",
        "WrDt": "01/09/2020"
      },
      "AttribDtls": [
        {
          "Nm": "Rice",
          "Val": "10000"
        }
      ]
    }
  ],
  "ValDtls": {
    "AssVal": 9978.84,
    "CgstVal": 0,
    "SgstVal": 0,
    "IgstVal": 1197.46,
    "CesVal": 508.94,
    "StCesVal": 1202.46,
    "Discount": 10,
    "OthChrg": 20,
    "RndOffAmt": 0.3,
    "TotInvVal": 12908,
    "TotInvValFc": 12897.7
  },
  "PayDtls": {
    "Nm": "ABCDE",
    "AccDet": "5697389713210",
    "Mode": "Cash",
    "FininsBr": "SBIN11000",
    "PayTerm": "100",
    "PayInstr": "Gift",
    "CrTrn": "test",
    "DirDr": "test",
    "CrDay": 100,
    "PaidAmt": 10000,
    "PaymtDue": 5000
  },
  "RefDtls": {
    "InvRm": "TEST",
    "DocPerdDtls": {
      "InvStDt": "01/08/2020",
      "InvEndDt": "01/09/2020"
    },
    "PrecDocDtls": [
      {
        "InvNo": "DOC/002",
        "InvDt": "01/08/2020",
        "OthRefNo": "123456"
      }
    ],
    "ContrDtls": [
      {
        "RecAdvRefr": "Doc/003",
        "RecAdvDt": "01/08/2020",
        "Tendrefr": "Abc001",
        "Contrrefr": "Co123",
        "Extrefr": "Yo456",
        "Projrefr": "Doc-456",
        "Porefr": "Doc-789",
        "PoRefDt": "01/08/2020"
      }
    ]
  },
  "AddlDocDtls": [
    {
      "Url": "https://einv-apisandbox.nic.in",
      "Docs": "Test Doc",
      "Info": "Document Test"
    }
  ],
  "ExpDtls": {
    "ShipBNo": "A-248",
    "ShipBDt": "01/08/2020",
    "Port": "INABG1",
    "RefClm": "N",
    "ForCur": "AED",
    "CntCode": "AE"
  },
  "EwbDtls": {
    "TransId": "12AWGPV7107B1Z1",
    "TransName": "XYZ EXPORTS",
    "Distance": 100,
    "TransDocNo": "DOC01",
    "TransDocDt": "08/08/2020",
    "VehNo": "ka123456",
    "VehType": "R",
    "TransMode": "1"
  }
}

```

{% hint style="info" %}
Since you can generate IRN for an invoice only once, make sure to change the Document Number `DocDtls.No` for every new request.
{% endhint %}

#### Response Parameters

* For Successful request

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Success</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>&quot;Y&quot; if the request is successful,</p>
        <p>&quot;N&quot; otherwise</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AckNo</td>
      <td style="text-align:left">Long</td>
      <td style="text-align:left">Acknowledgement Number</td>
    </tr>
    <tr>
      <td style="text-align:left">AckDt</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Format YYYY-MM-DD HH:MM:SS,</p>
        <p>Acknowledgement date</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Irn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Invoice Reference Number. SHA256 hash of Gstin, DocDtls.No, DocDtls.Typ,
          financial year of DoctDtls.Dt
          <br />
        </p>
        <p>There is no need to decode or decrypt this string.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SignedInvoice</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Signed Invoice Data</td>
    </tr>
    <tr>
      <td style="text-align:left">SignedQRCode</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">QR Code for Invoice</td>
    </tr>
    <tr>
      <td style="text-align:left">Status</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>&quot;ACT&quot; for active invoice,</p>
        <p>&quot;CNL&quot; for cancelled invoice</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EwbNo</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">E-waybill number. This will be null if E-Waybill is not generated.</td>
    </tr>
    <tr>
      <td style="text-align:left">EwbDt</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">E-Waybill date. This will be null if E-Waybill is not generated.</td>
    </tr>
    <tr>
      <td style="text-align:left">EwbValidTill</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">E-waybill valid till. This will be null if E-Waybill is not generated.</td>
    </tr>
  </tbody>
</table>

* For Failed requests 

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| Success | String | "N" for failed request |
| ErrorDetails | Array of Error Detail | Details of all errors |
| Info | Array of Info Detail | Additional Information |

#### Error Detail

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| error\_code | String | Error Code  |
| error\_message | String | Error Message |
| error\_source | String | Error Source can either be GOVT or CLEARTAX |
| error\_id | String | Optional |

#### Info Details

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| InfCd | String | Information Code |
| Desc | Object | Description or additional details |

**Sample Response**

{% tabs %}
{% tab title="Valid Response" %}
```text
{
  "Success": "Y",
  "AckNo": 162010000001700,
  "AckDt": "2020-08-08 11:23:00",
  "Irn": "58f1669d31c5725ddcc39eeecd465e69543c639daeb1d582546aa3d28d66c3f8",
  "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxNjIwMTAwMDAwMDE3MDAsXCJBY2tEdFwiOlwiMjAyMC0wOC0wOCAxMToyMzowMFwiLFwiSXJuXCI6XCI1OGYxNjY5ZDMxYzU3MjVkZGNjMzllZWVjZDQ2NWU2OTU0M2M2MzlkYWViMWQ1ODI1NDZhYTNkMjhkNjZjM2Y4XCIsXCJWZXJzaW9uXCI6XCIxLjAxXCIsXCJUcmFuRHRsc1wiOntcIlRheFNjaFwiOlwiR1NUXCIsXCJTdXBUeXBcIjpcIkIyQlwiLFwiUmVnUmV2XCI6XCJZXCIsXCJJZ3N0T25JbnRyYVwiOlwiTlwifSxcIkRvY0R0bHNcIjp7XCJUeXBcIjpcIklOVlwiLFwiTm9cIjpcIkRPQy8wMDdcIixcIkR0XCI6XCIwOC8wOC8yMDIwXCJ9LFwiU2VsbGVyRHRsc1wiOntcIkdzdGluXCI6XCIyNEFBRkNENTg2MlIwMDVcIixcIkxnbE5tXCI6XCJOSUMgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwiTklDIEluZHVzdHJpZXNcIixcIkFkZHIxXCI6XCI1dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlBpblwiOjM4MjAxMCxcIlN0Y2RcIjpcIjI0XCIsXCJQaFwiOlwiOTAwMDAwMDAwMFwiLFwiRW1cIjpcImFiY0BnbWFpbC5jb21cIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcIlhZWiBJbmR1c3RyaWVzXCIsXCJQb3NcIjpcIjEyXCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjo1NjIxNjAsXCJQaFwiOlwiOTExMTExMTExMTFcIixcIkVtXCI6XCJ4eXpAeWFob28uY29tXCIsXCJTdGNkXCI6XCIyOVwifSxcIkRpc3BEdGxzXCI6e1wiTm1cIjpcIkFCQyBjb21wYW55IHB2dCBsdGRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJTaGlwRHRsc1wiOntcIkdzdGluXCI6XCIyOUFXR1BWNzEwN0IxWjFcIixcIkxnbE5tXCI6XCJDQkUgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUmljZVwiLFwiSHNuQ2RcIjpcIjEwMDFcIixcIkJhcmNkZVwiOlwiMTIzNDU2XCIsXCJRdHlcIjoxMDAuMzQ1LFwiRnJlZVF0eVwiOjEwLjAsXCJVbml0XCI6XCJCQUdcIixcIlVuaXRQcmljZVwiOjk5LjU0NSxcIlRvdEFtdFwiOjk5ODguODQsXCJEaXNjb3VudFwiOjEwLFwiUHJlVGF4VmFsXCI6MSxcIkFzc0FtdFwiOjk5NzguODQsXCJHc3RSdFwiOjEyLjAwMCxcIklnc3RBbXRcIjoxMTk3LjQ2LFwiQ2dzdEFtdFwiOjAsXCJTZ3N0QW10XCI6MCxcIkNlc1J0XCI6NS4wMDAsXCJDZXNBbXRcIjo0OTguOTQsXCJDZXNOb25BZHZsQW10XCI6MTAsXCJTdGF0ZUNlc1J0XCI6MTIuMDAwLFwiU3RhdGVDZXNBbXRcIjoxMTk3LjQ2LFwiU3RhdGVDZXNOb25BZHZsQW10XCI6NSxcIk90aENocmdcIjoxMCxcIlRvdEl0ZW1WYWxcIjoxMjg5Ny43LFwiT3JkTGluZVJlZlwiOlwiMzI1NlwiLFwiT3JnQ250cnlcIjpcIkFHXCIsXCJQcmRTbE5vXCI6XCIxMjM0NVwiLFwiQmNoRHRsc1wiOntcIk5tXCI6XCIxMjM0NTZcIn0sXCJBdHRyaWJEdGxzXCI6W3tcIk5tXCI6XCJSaWNlXCIsXCJWYWxcIjpcIjEwMDAwXCJ9XX1dLFwiVmFsRHRsc1wiOntcIkFzc1ZhbFwiOjk5NzguODQsXCJDZ3N0VmFsXCI6MCxcIlNnc3RWYWxcIjowLFwiSWdzdFZhbFwiOjExOTcuNDYsXCJDZXNWYWxcIjo1MDguOTQsXCJTdENlc1ZhbFwiOjEyMDIuNDYsXCJEaXNjb3VudFwiOjEwLFwiT3RoQ2hyZ1wiOjIwLFwiUm5kT2ZmQW10XCI6MC4zLFwiVG90SW52VmFsXCI6MTI5MDgsXCJUb3RJbnZWYWxGY1wiOjEyODk3Ljd9LFwiUGF5RHRsc1wiOntcIk5tXCI6XCJBQkNERVwiLFwiTW9kZVwiOlwiQ2FzaFwifSxcIlJlZkR0bHNcIjp7XCJJbnZSbVwiOlwiVEVTVFwiLFwiRG9jUGVyZER0bHNcIjp7XCJJbnZTdER0XCI6XCIwMS8wOC8yMDIwXCIsXCJJbnZFbmREdFwiOlwiMDEvMDkvMjAyMFwifSxcIlByZWNEb2NEdGxzXCI6W3tcIkludk5vXCI6XCJET0MvMDAyXCIsXCJJbnZEdFwiOlwiMDEvMDgvMjAyMFwiLFwiT3RoUmVmTm9cIjpcIjEyMzQ1NlwifV0sXCJDb250ckR0bHNcIjpbe1wiUmVjQWR2RHRcIjpcIjAxLzA4LzIwMjBcIn1dfSxcIkFkZGxEb2NEdGxzXCI6W3tcIlVybFwiOlwiaHR0cHM6Ly9laW52LWFwaXNhbmRib3gubmljLmluXCIsXCJEb2NzXCI6XCJUZXN0IERvY1wiLFwiSW5mb1wiOlwiRG9jdW1lbnQgVGVzdFwifV0sXCJFeHBEdGxzXCI6e1wiU2hpcEJOb1wiOlwiQS0yNDhcIixcIlNoaXBCRHRcIjpcIjAxLzA4LzIwMjBcIixcIlBvcnRcIjpcIklOQUJHMVwiLFwiUmVmQ2xtXCI6XCJOXCIsXCJGb3JDdXJcIjpcIkFFRFwiLFwiQ250Q29kZVwiOlwiQUVcIn0sXCJFd2JEdGxzXCI6e1wiVHJhbnNJZFwiOlwiMTJBV0dQVjcxMDdCMVoxXCIsXCJUcmFuc05hbWVcIjpcIlhZWiBFWFBPUlRTXCIsXCJUcmFuc01vZGVcIjpcIjFcIixcIkRpc3RhbmNlXCI6MTAwLFwiVHJhbnNEb2NOb1wiOlwiRE9DMDFcIixcIlRyYW5zRG9jRHRcIjpcIjA4LzA4LzIwMjBcIixcIlZlaE5vXCI6XCJrYTEyMzQ1NlwiLFwiVmVoVHlwZVwiOlwiUlwifX0iLCJpc3MiOiJOSUMifQ.qLdolsRy-W00xbHzME5U65jRf9c6R3tYTnEYzMG2hEZdBmFQzPCnw-T273OW_EmRUrYlp-7XjHRbInoW-kTfIieJpWfH20sSnf_siQO19YgbtoRuXQNE7uig7TqpJMGAIHH5QsAI1QLzJj1m98NucKGUcXhk2906MLtqHKMb5Ug0InaP4JweX2Dfmiqj5RiN5dLBFfIpgWhGT_2fSJBWdRg8w9CoQZwhdqN-2sP_SHdgNDzdH6eHtTp5eMyyLJNKA7estyqNoNvl8EpZHHeDZiISE4JXCf6yBq_8BaNKE9bsN_VCua_WCcBcNxYH3373F275PQhxybRMrGAntdUiNQ",
  "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI0QUFGQ0Q1ODYyUjAwNVwiLFwiQnV5ZXJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJEb2NOb1wiOlwiRE9DLzAwN1wiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIwOC8wOC8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMjkwOCxcIkl0ZW1DbnRcIjoxLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiNThmMTY2OWQzMWM1NzI1ZGRjYzM5ZWVlY2Q0NjVlNjk1NDNjNjM5ZGFlYjFkNTgyNTQ2YWEzZDI4ZDY2YzNmOFwifSIsImlzcyI6Ik5JQyJ9.aQYuyV9pQzBaaFQUPJloj76GxEOVZ7xJCy09yxQIaL2gjPu16QcRNGksIlH3LBPFkA1b0wSNbi7e-nek65Pv5JHbyPjt4ihw9Z-YPqyzOdOU26lDP4ci0Ea_B1pSmOIv8itroLf2zVx5w6eUUqNYffI9h_JMF-E_BD0DoLE-axLvl-NM1Xb7kBFMQyzK-Y8AlXQEf_oAOxZcxqR8amJfIrN4mSTbcjcfUxT_16DECTW0Bbm83BFi1jtf_CQX4qZio-4WPCKbo1iZNzD9LXzAd8nt9ErzAqud8pKFWTHo3fVcX7TdfSc19G6PIk7GWy3FeQCvC_sZSkWfOR9eOJowNQ",
  "Status": "ACT",
  "EwbNo": 681008686014,
  "EwbDt": "2020-08-08 11:23:00",
  "EwbValidTill": "2020-08-09 23:59:00"
}

```
{% endtab %}

{% tab title="Invalid Response" %}
```
{
  "Success": "N",
  "ErrorDetails": [
    {
      "error_code": "2150",
      "error_message": "Duplicate IRN",
      "error_source": "GOVT"
    }
  ],
  "info": [
    {
      "InfCd": "DUPIRN",
      "Desc": {
        "AckNo": 162010000001700,
        "AckDt": "2020-08-08 11:23:00",
        "Irn": "58f1669d31c5725ddcc39eeecd465e69543c639daeb1d582546aa3d28d66c3f8"
      }
    }
  ]
}

```
{% endtab %}
{% endtabs %}

## Cancelling IRN

You can cancel an already generated IRN by sending a `POST` request to E-Invoicing API with the following request headers.

{% hint style="danger" %}
If the E-Invoice has a valid/active E-Waybill linked, then you cannot cancel the IRN.
{% endhint %}

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | Users GSTIN |

**Request URL**

```text
POST: {{HOST}}/v1/govt/api/Cancel
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| irn | Body | String | Mandatory. IRN generated for the invoice. |
| CnlRsn | Body | String | Mandatory. Reason for cancellation. |
| CnlRem | Body | String | Mandatory. Remarks for cancellation. |

#### Sample Request Body

```text
{
  "irn": "a5c12dca80e743321740b001fd70953e8738d109865d28ba4013750f2046f229",
  "CnlRsn": "1",
  "CnlRem": "Duplicate Invoice"
}
```

#### Response Parameters

* For Successful request

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Success</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>&quot;Y&quot; if request is successful,</p>
        <p>&quot;N&quot; otherwise</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CancelDate</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Format YYYY-MM-DD HH:MM:SS,</p>
        <p>Cancellation date</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Irn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Invoice Reference Number</td>
    </tr>
  </tbody>
</table>

* For Failed requests 

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| Success | String | "N" for failed request |
| ErrorDetails | Array of Error Detail | Details of all errors |

#### Error Detail

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| error\_code | String | Error Code  |
| error\_message | String | Error Message |
| error\_source | String | Error Source can either be GOVT or CLEARTAX |
| error\_id | String | Optional |

#### Sample Response

{% tabs %}
{% tab title="Valid Response" %}
```text
{
  "Success":"Y",
  "Irn": "a5c12dca80e743321740b001fd70953e8738d109865d28ba4013750f2046f229",
  "CancelDate": "2019-12-05 14:26:00"
}
```
{% endtab %}

{% tab title="Invalid Response" %}
```text
{
    "Success": "N",
    "ErrorDetails": [
        {
            "error_code": "2230",
            "error_message": "This IRN cannot be cancelled because  e-way bill has been generated , you can cancel   e-way bill and then try cancelling IRN",
            "error_source": "GOVT"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Please note that you will be able to cancel an E-Invoice only within the time limit \(24 hours since generation\) specified by the Government.
{% endhint %}

## Getting Invoice by IRN

You can get an Invoice by IRN by sending a `GET` request to E-Invoicing API with the following request headers.

```
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

**Request URL**

```text
GET: {{HOST}}/v1/govt/api/Invoice/irn/{{IRN}}
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| IRN | Path | String | Mandatory. IRN generated for the invoice. |

**Sample Request:**

```text
https://einvoicing.internal.cleartax.co/v1/govt/api/Invoice/irn/2d5b90edf2819c91f660a6d6843346fab0d57a27badf92ac8f7fbc8762f50ab1
```

#### Response Parameters

* For Successful request

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter</b>
      </th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Success</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>&quot;Y&quot; if request is successful,</p>
        <p>&quot;N&quot; otherwise</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AckNo</td>
      <td style="text-align:left">Long</td>
      <td style="text-align:left">Acknowledgement Number</td>
    </tr>
    <tr>
      <td style="text-align:left">AckDt</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Format YYYY-MM-DD HH:MM:SS,</p>
        <p>Acknowledgement date</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Irn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Invoice Reference Number</td>
    </tr>
    <tr>
      <td style="text-align:left">SignedInvoice</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Signed Invoice Data</td>
    </tr>
    <tr>
      <td style="text-align:left">SignedQRCode</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">QR Code for Invoice</td>
    </tr>
    <tr>
      <td style="text-align:left">Status</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>&quot;ACT&quot; for active invoice,</p>
        <p>&quot;CNL&quot; for cancelled invoice</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EwbNo</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">E-waybill number</td>
    </tr>
    <tr>
      <td style="text-align:left">EwbDt</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">E-Waybill date</td>
    </tr>
    <tr>
      <td style="text-align:left">EwbValidTill</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">E-waybill valid till</td>
    </tr>
  </tbody>
</table>

* For Failed requests 

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| Success | String | "N" if the request failed. |
| ErrorDetails | Array | Details of all errors |

#### Error Detail

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| error\_code | String | Error Code  |
| error\_message | String | Error Message |
| error\_source | String | Error Source can either be GOVT or CLEARTAX |

**Sample Response**

{% tabs %}
{% tab title="Valid Response" %}
```text
{
  "Success": "Y",
  "AckNo": 162010000001700,
  "AckDt": "2020-08-08 11:23:00",
  "Irn": "58f1669d31c5725ddcc39eeecd465e69543c639daeb1d582546aa3d28d66c3f8",
  "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxNjIwMTAwMDAwMDE3MDAsXCJBY2tEdFwiOlwiMjAyMC0wOC0wOCAxMToyMzowMFwiLFwiSXJuXCI6XCI1OGYxNjY5ZDMxYzU3MjVkZGNjMzllZWVjZDQ2NWU2OTU0M2M2MzlkYWViMWQ1ODI1NDZhYTNkMjhkNjZjM2Y4XCIsXCJWZXJzaW9uXCI6XCIxLjAxXCIsXCJUcmFuRHRsc1wiOntcIlRheFNjaFwiOlwiR1NUXCIsXCJTdXBUeXBcIjpcIkIyQlwiLFwiUmVnUmV2XCI6XCJZXCIsXCJJZ3N0T25JbnRyYVwiOlwiTlwifSxcIkRvY0R0bHNcIjp7XCJUeXBcIjpcIklOVlwiLFwiTm9cIjpcIkRPQy8wMDdcIixcIkR0XCI6XCIwOC8wOC8yMDIwXCJ9LFwiU2VsbGVyRHRsc1wiOntcIkdzdGluXCI6XCIyNEFBRkNENTg2MlIwMDVcIixcIkxnbE5tXCI6XCJOSUMgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwiTklDIEluZHVzdHJpZXNcIixcIkFkZHIxXCI6XCI1dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlBpblwiOjM4MjAxMCxcIlN0Y2RcIjpcIjI0XCIsXCJQaFwiOlwiOTAwMDAwMDAwMFwiLFwiRW1cIjpcImFiY0BnbWFpbC5jb21cIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcIlhZWiBJbmR1c3RyaWVzXCIsXCJQb3NcIjpcIjEyXCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjo1NjIxNjAsXCJQaFwiOlwiOTExMTExMTExMTFcIixcIkVtXCI6XCJ4eXpAeWFob28uY29tXCIsXCJTdGNkXCI6XCIyOVwifSxcIkRpc3BEdGxzXCI6e1wiTm1cIjpcIkFCQyBjb21wYW55IHB2dCBsdGRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJTaGlwRHRsc1wiOntcIkdzdGluXCI6XCIyOUFXR1BWNzEwN0IxWjFcIixcIkxnbE5tXCI6XCJDQkUgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUmljZVwiLFwiSHNuQ2RcIjpcIjEwMDFcIixcIkJhcmNkZVwiOlwiMTIzNDU2XCIsXCJRdHlcIjoxMDAuMzQ1LFwiRnJlZVF0eVwiOjEwLjAsXCJVbml0XCI6XCJCQUdcIixcIlVuaXRQcmljZVwiOjk5LjU0NSxcIlRvdEFtdFwiOjk5ODguODQsXCJEaXNjb3VudFwiOjEwLFwiUHJlVGF4VmFsXCI6MSxcIkFzc0FtdFwiOjk5NzguODQsXCJHc3RSdFwiOjEyLjAwMCxcIklnc3RBbXRcIjoxMTk3LjQ2LFwiQ2dzdEFtdFwiOjAsXCJTZ3N0QW10XCI6MCxcIkNlc1J0XCI6NS4wMDAsXCJDZXNBbXRcIjo0OTguOTQsXCJDZXNOb25BZHZsQW10XCI6MTAsXCJTdGF0ZUNlc1J0XCI6MTIuMDAwLFwiU3RhdGVDZXNBbXRcIjoxMTk3LjQ2LFwiU3RhdGVDZXNOb25BZHZsQW10XCI6NSxcIk90aENocmdcIjoxMCxcIlRvdEl0ZW1WYWxcIjoxMjg5Ny43LFwiT3JkTGluZVJlZlwiOlwiMzI1NlwiLFwiT3JnQ250cnlcIjpcIkFHXCIsXCJQcmRTbE5vXCI6XCIxMjM0NVwiLFwiQmNoRHRsc1wiOntcIk5tXCI6XCIxMjM0NTZcIn0sXCJBdHRyaWJEdGxzXCI6W3tcIk5tXCI6XCJSaWNlXCIsXCJWYWxcIjpcIjEwMDAwXCJ9XX1dLFwiVmFsRHRsc1wiOntcIkFzc1ZhbFwiOjk5NzguODQsXCJDZ3N0VmFsXCI6MCxcIlNnc3RWYWxcIjowLFwiSWdzdFZhbFwiOjExOTcuNDYsXCJDZXNWYWxcIjo1MDguOTQsXCJTdENlc1ZhbFwiOjEyMDIuNDYsXCJEaXNjb3VudFwiOjEwLFwiT3RoQ2hyZ1wiOjIwLFwiUm5kT2ZmQW10XCI6MC4zLFwiVG90SW52VmFsXCI6MTI5MDgsXCJUb3RJbnZWYWxGY1wiOjEyODk3Ljd9LFwiUGF5RHRsc1wiOntcIk5tXCI6XCJBQkNERVwiLFwiTW9kZVwiOlwiQ2FzaFwifSxcIlJlZkR0bHNcIjp7XCJJbnZSbVwiOlwiVEVTVFwiLFwiRG9jUGVyZER0bHNcIjp7XCJJbnZTdER0XCI6XCIwMS8wOC8yMDIwXCIsXCJJbnZFbmREdFwiOlwiMDEvMDkvMjAyMFwifSxcIlByZWNEb2NEdGxzXCI6W3tcIkludk5vXCI6XCJET0MvMDAyXCIsXCJJbnZEdFwiOlwiMDEvMDgvMjAyMFwiLFwiT3RoUmVmTm9cIjpcIjEyMzQ1NlwifV0sXCJDb250ckR0bHNcIjpbe1wiUmVjQWR2RHRcIjpcIjAxLzA4LzIwMjBcIn1dfSxcIkFkZGxEb2NEdGxzXCI6W3tcIlVybFwiOlwiaHR0cHM6Ly9laW52LWFwaXNhbmRib3gubmljLmluXCIsXCJEb2NzXCI6XCJUZXN0IERvY1wiLFwiSW5mb1wiOlwiRG9jdW1lbnQgVGVzdFwifV0sXCJFeHBEdGxzXCI6e1wiU2hpcEJOb1wiOlwiQS0yNDhcIixcIlNoaXBCRHRcIjpcIjAxLzA4LzIwMjBcIixcIlBvcnRcIjpcIklOQUJHMVwiLFwiUmVmQ2xtXCI6XCJOXCIsXCJGb3JDdXJcIjpcIkFFRFwiLFwiQ250Q29kZVwiOlwiQUVcIn0sXCJFd2JEdGxzXCI6e1wiVHJhbnNJZFwiOlwiMTJBV0dQVjcxMDdCMVoxXCIsXCJUcmFuc05hbWVcIjpcIlhZWiBFWFBPUlRTXCIsXCJUcmFuc01vZGVcIjpcIjFcIixcIkRpc3RhbmNlXCI6MTAwLFwiVHJhbnNEb2NOb1wiOlwiRE9DMDFcIixcIlRyYW5zRG9jRHRcIjpcIjA4LzA4LzIwMjBcIixcIlZlaE5vXCI6XCJrYTEyMzQ1NlwiLFwiVmVoVHlwZVwiOlwiUlwifX0iLCJpc3MiOiJOSUMifQ.qLdolsRy-W00xbHzME5U65jRf9c6R3tYTnEYzMG2hEZdBmFQzPCnw-T273OW_EmRUrYlp-7XjHRbInoW-kTfIieJpWfH20sSnf_siQO19YgbtoRuXQNE7uig7TqpJMGAIHH5QsAI1QLzJj1m98NucKGUcXhk2906MLtqHKMb5Ug0InaP4JweX2Dfmiqj5RiN5dLBFfIpgWhGT_2fSJBWdRg8w9CoQZwhdqN-2sP_SHdgNDzdH6eHtTp5eMyyLJNKA7estyqNoNvl8EpZHHeDZiISE4JXCf6yBq_8BaNKE9bsN_VCua_WCcBcNxYH3373F275PQhxybRMrGAntdUiNQ",
  "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI0QUFGQ0Q1ODYyUjAwNVwiLFwiQnV5ZXJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJEb2NOb1wiOlwiRE9DLzAwN1wiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIwOC8wOC8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMjkwOCxcIkl0ZW1DbnRcIjoxLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiNThmMTY2OWQzMWM1NzI1ZGRjYzM5ZWVlY2Q0NjVlNjk1NDNjNjM5ZGFlYjFkNTgyNTQ2YWEzZDI4ZDY2YzNmOFwifSIsImlzcyI6Ik5JQyJ9.aQYuyV9pQzBaaFQUPJloj76GxEOVZ7xJCy09yxQIaL2gjPu16QcRNGksIlH3LBPFkA1b0wSNbi7e-nek65Pv5JHbyPjt4ihw9Z-YPqyzOdOU26lDP4ci0Ea_B1pSmOIv8itroLf2zVx5w6eUUqNYffI9h_JMF-E_BD0DoLE-axLvl-NM1Xb7kBFMQyzK-Y8AlXQEf_oAOxZcxqR8amJfIrN4mSTbcjcfUxT_16DECTW0Bbm83BFi1jtf_CQX4qZio-4WPCKbo1iZNzD9LXzAd8nt9ErzAqud8pKFWTHo3fVcX7TdfSc19G6PIk7GWy3FeQCvC_sZSkWfOR9eOJowNQ",
  "Status": "ACT",
  "EwbNo": 681008686014,
  "EwbDt": "2020-08-08 11:23:00",
  "EwbValidTill": "2020-08-09 23:59:00"
}

```
{% endtab %}

{% tab title="Invalid Response" %}
```
{
  "Success": "N",
  "ErrorDetails": [
    {
      "error_code": "2148",
      "error_message": "Requested IRN data is not available",
      "error_source": "GOVT"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

## Generate E-Waybill by IRN

You can use this API to generate the e-waybill using Invoice Registration Number \(IRN\).

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | Users GSTIN |

**Request URL**

```text
POST: {{HOST}}/v1/govt/api/einvewb/ewaybill
```

#### Request Parameters:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Parameter Type</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Validation</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Irn</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 64
          <br />
        </p>
        <p>maxLength: 64</p>
      </td>
      <td style="text-align:left">Mandatory. IRN generated for the invoice.</td>
    </tr>
    <tr>
      <td style="text-align:left">Distance</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>minimum: 1</p>
        <p>maximum: 9999</p>
      </td>
      <td style="text-align:left">Mandatory. Distance between source and destination PIN codes</td>
    </tr>
    <tr>
      <td style="text-align:left">TransMode</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 1
          <br />
        </p>
        <p>enum: [&quot;1&quot;, &quot;2&quot;, &quot;3&quot;, &quot;4&quot;]</p>
      </td>
      <td style="text-align:left">Mode of transport (Road-1, Rail-2, Air-3, Ship-4)</td>
    </tr>
    <tr>
      <td style="text-align:left">TransId</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 15</p>
        <p>maxLength: 15</p>
      </td>
      <td style="text-align:left">Transin/GSTIN</td>
    </tr>
    <tr>
      <td style="text-align:left">TransName</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 3</p>
        <p>maxLength: 100</p>
      </td>
      <td style="text-align:left">Name of the transporter</td>
    </tr>
    <tr>
      <td style="text-align:left">TransDocDt</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 10</p>
        <p>maxLength: 10</p>
        <p>pattern: &quot;[0-3][0-9]/[0-1][0-9]/[2][0][1-2][0-9]&quot;</p>
      </td>
      <td style="text-align:left">Transport Document Date</td>
    </tr>
    <tr>
      <td style="text-align:left">TransDocNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1</p>
        <p>maxLength: 15</p>
        <p>pattern: &quot;^([0-9A-Z/-]){1,15}$&quot;</p>
      </td>
      <td style="text-align:left">Tranport Document Number</td>
    </tr>
    <tr>
      <td style="text-align:left">VehNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 4</p>
        <p>maxLength: 20</p>
      </td>
      <td style="text-align:left">Vehicle Number</td>
    </tr>
    <tr>
      <td style="text-align:left">VehType</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>minLength: 1,
          <br />maxLength: 1,
          <br />
        </p>
        <p>enum: [&quot;O&quot;, &quot;R&quot;],</p>
      </td>
      <td style="text-align:left">Whether O-ODC or R-Regular</td>
    </tr>
  </tbody>
</table>

#### Sample Request Body

```text
 {
  "Irn": "a5c12dca80e743321740b001fd70953e8738d109865d28ba4013750f2046f229",
  "Distance": 100,
  "TransMode": "1",
  "TransId":"12AWGPV7107B1Z1",  
  "TransName": "trans name",
  "TransDocDt": "01/08/2020",
  "TransDocNo": "TRAN/DOC/11",
  "VehNo": "KA01AB1234",
  "VehType": "R"
}
```

#### Response Parameters

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| EwbNo | String | e-waybill Number |
| EwbDt | String | e-waybill date |
| EwbValidTill | String | e-waybill validity |

#### Sample Response

{% tabs %}
{% tab title="Valid Response" %}
```text
 {
   "EwbNo":"16510609282",
   "EwbDt":"2020-04-24 11:28:00",
   "EwbValidTill":"2020-04-26 23:59:00"
}
```
{% endtab %}

{% tab title="Invalid Response" %}
```text
{
  "Irn": "834ecbf400d73ae25e9e5bbd2fb090510b476b8b3ded109fab7d819314c9b7c3",
  "TransId": "12AWGPV7107B1Z1",
  "TransName": "XYZ EXPORTS",
  "TransMode": "1",
  "Distance": 100,
  "TransDocNo": "DOC01",
  "TransDocDt": "08/08/2020",
  "VehNo": "ka123456",
  "VehType": "R",
  "EwbStatus": "FAILED",
  "errors": {
    "errors": [
      {
        "error_code": "4002",
        "error_message": "EwayBill is already generated for this IRN",
        "error_source": "GOVT"
      }
    ]
  }
}

```
{% endtab %}
{% endtabs %}

## Cancel E-Waybill \(Not live\)

{% hint style="danger" %}
E-way bill can be cancelled by the generator of the e-way bill only.

E-way bill can be cancelled within 24 hours of generation of e-way bill
{% endhint %}

You can use this API to cancel the generated e-waybill.

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | Users GSTIN |

**Request URL**

```text
POST: {{HOST}}​/v1​/govt​/api​/Cancel
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
      <td style="text-align:left">ewbNo</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">EwayBill Number</td>
    </tr>
    <tr>
      <td style="text-align:left">cancelRsnCode</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>Reason for cancellation Enum:[1,2]</p>
        <p>1= Duplicate</p>
        <p>2= Data Entry Mistake</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">cancelRmrk</td>
      <td style="text-align:left">Body</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Remarks</td>
    </tr>
  </tbody>
</table>

#### Sample Request Body

```text
{  
"ewbNo": 111000609282,
"cancelRsnCode": 2,
"cancelRmrk": "Cancelled the order"
}
```

#### Response Parameters

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| ewayBillNo | String | e-waybill Number |
| cancelDate | String | e-waybill cancel date |

#### Sample Response

{% tabs %}
{% tab title="Valid Response" %}
```text
{   
"ewayBillNo": 16510609282,
"cancelDate": "15/07/202011:35:00 AM"
}
```
{% endtab %}

{% tab title="Invalid Response" %}
```
Coming soon
```
{% endtab %}
{% endtabs %}

## Validations

**Validations in e-Invoicing System**

1. E-Invoice request JSON data has to be validated as per the e-Invoice JSON Schema given in the portal.
2. The version of the Schema is mandatory and should be latest as per the notified in API portal.
3. IRN should not be passed as part of the request; it is generated by the e-Invoice system and sent as a response.
4. The following fields should have one of the values given in the master codes.
   * Supply Type of Transaction
   * Document Type
5. The category of the transaction of ‘Business to Consumer \(B2C\)’ invoices will not be considered and hence the API interface should not request for IRN for these transactions.
6. Document number should not be starting with 0, / and -. Also, alphabets in document number should not have alphabets in lower cases. If so, then request is rejected.
7. The supplier should ensure that the unique invoice number is being generated for the financial year for each invoice, in his ERP/manual system. For the purpose of the financial year, the date of the invoice is considered. The financial year starts on 1st April and ends on 31st March.
8. Duplicate IRN requests are not considered. That is, if the IRN is already generated on a particular type of document and document number of the supplier for the financial year, then one more IRN cannot be generated on the same combination.
9. e-invoice\(IRN\) cannot be re-generated for the cancelled e-invoice\(IRN\) also.
10. IRN cannot be cancelled, if the Valid/Active E-way Bill exists for the same.
11. Request for the IRN/e-Invoice can be made only by the supplier of the goods or services.
12. In the case of e-commerce transactions, the e-Commerce Operator can request for the IRN/e-invoice on behalf of the supplier. In this case, the e-Commerce Operator should have been registered on the GST portal as e-Commerce Operator and pass eCom\_GSTIN accordingly.
13. In case the supplier is an SEZ unit, then he cannot generate e-Invoice.
14. The Document Date can be yesterday or today’s date.
15. ‘Reverse Charges’ can be set as ‘Y’ in case of B2B invoices only and tax is being paid in a reverse manner as per rule. Even in case of Reverse Charged invoices, the seller has to generate the IRN.
16. Recipient GSTIN should be registered and active. In case of transaction of direct export, recipient GSTIN has to be URP and state code has to be 96, POS should be 96
17. In case, Buyer is SEZ, the Bill to State code should be 96.
18. In the case of Export, POS should be 96 and in all other cases, POS should be a valid state code.
19. In the case of Export, Port details are mandatory.
20. PIN Codes are validated against the States, they belong to.
21. If ‘Shipping party’ is provided, then the transaction is considered as ‘Bill To-Ship To’.
22. In the case of B2B, If ship to details is given, ship-to state code should be equal to the POS.
23. If ‘Dispatching party’ is provided, then the transaction is considered as ‘Bill From – Dispatch From’.
24. If Shipping and Dispatching parties are provided, then the transaction is considered as ‘Combination of Both’.
25. In case of export transactions, the ‘Ship-To’ address should be of the place/port from where the goods are being exported.
26. In the case of Goods, the state code of the Seller GSTIN and state code of the Buyer GSTIN will decide whether the supply type is Interstate or Intrastate. That is, if the State code of Seller and buyer is the same, then it is intra-state, otherwise, it is inter-state.
27. In the case of services, the state code of the Seller GSTIN and state code of POS will decide whether the supply type is Interstate or Intrastate. That is, if the State code of Seller and state code of POS is the same, then it is intra-state, otherwise, it is inter-state.
28. In the case of Exports, the supply is always Interstate whether Goods or Services.

**Validations on Items:**

1. no of the item is verified for duplicate values.
2. Each item needs to have a valid HSN code with at least 4 digits. That is, items of goods type should be 4 or 6 or 8 digits and items of service type should be 4 or 5 or 6 digits. HSN Code should be valid as per the GST master.
3. If Is\_Service is selected, then the HSN codes must belong to services.
4. Each item should have a valid Unit Quantity Code \(UQC\) as per the master codes, in case of goods.
5. Quantity and Unit Quantity Code are mandatory for Goods and optional for Services.
6. Tax rates are being validated. Only the allowed tax rates will be accepted.
7. In the case of an intrastate transaction, the sum of SGST and CGST tax rates should be entered as GST Rate.
8. In the case of an inter-state transaction, the IGST tax rate and value have to be passed.
9. In case of an export transaction, IGST tax rate and value have to be passed.
10. In case the buyer is SEZ unit, then IGST tax rate and value have to be passed irrespective of the state of the buyer.
11. The maximum number of items in each invoice should not exceed more than 1000 items and a minimum of 1 item should be available.

**Calculation of Values:**

1. The following summation validations are to be done for items
   * Gross Amount of Item = Quantity X Selling Unit Price \(Rounded to 2 decimal places\)
   * Taxable Value of Item = Gross Amount of Item – Discount
   * SGST Value of Item = Taxable Value of Item X GST Rate / 2, if intra-state \(Rounded to 2 decimal places\)
   * CGST Value of Item = Taxable Value of Item X GST Rate / 2, if intra-state \(Rounded to 2 decimal places\)
   * IGST Value of Item = Taxable Value of Item X GST Rate, if inter-state \(Rounded to 2 decimal places\)
   * Cess Value of Item = Taxable Value of Item X Cess Rate \(Rounded to 2 decimal places\)
   * State Cess Value of Item = Taxable Value of Item X State Cess Rate \(Rounded to 2 decimal places\)
   * Total Value of Item = Taxable Value of Item + SGST Value of Item + CGST Value of Item + IGST Value of Item + Cess Value of Item + State Cess Value of Item + Non-Advol Cess Value of Item + State Cess Non-ad vol value of Item + Other charges.
2. The following summation validations are to be done on Invoice total
   * Total Taxable Value = Taxable Value of all Items
   * Total SGST Value = SGST Value of all Items
   * Total CGST Value = CGST Value of all Items
   * Total IGST Value = IGST Value of all Items
   * Total Cess Value = Cess Value of all Items + Non-Advol Cess Value of all Items
   * Total State Cess Value = State Cess Value of all Items + State Cess Nonadvol Value of all Items
   * Total Invoice Value = Total Taxable Value + Total SGST Value + Total CGST Value + Total IGST Value + Total Cess Value + Total State Cess Value + Total Non-Advol Cess Value
3. The round-off value can be + or – RS 10

**Validations on e-waybill:**

1. E-waybill can be generated only if E-way Bill related details are passed.
2. E-way Bill is not generated for document types of Debit Note and Credit Note and Services.
3. E Way Bill can be generated provided at least HSN of one item belongs to goods.
4. If only Transporter –Id is provided, then only Part-A is generated.
5. If the mode of transportation in ‘Road’, then the Vehicle number and vehicle type should be passed.
6. If the mode of transportation is Ship, Air, Rail, then the transport document number and date should be passed.
7. The Vehicle no. should match with specified format and exist in Vahan database.
8. E-Waybill will not be generated if the seller or buyer GSTIN is blocked due to non-filing of Returns.
9. Pincode of Recipient GSTIN is mandatory if Ship-To details are not entered
10. PIN-PIN distance is validated.

