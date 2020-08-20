# Taxpayer Information

ClearTax provides APIs to verify if a GSTIN number is valid as per the Government.

* Never have a wrong GSTIN for your Vendor/Customer in your ERP.
* System/Product On-boarding Avoid GST Compliance errors.
* Improve overall efficiency by reducing back and forth due to mistakes in GSTINs.
* Get additional details related to the GSTIN you already have.

## Get Taxpayer Profile

You can verify the GSTIN number and avoid any mistakes in invoice preparation, tax payments.

You can get the taxpayer profile of a GSTIN by submitting a **GET** request to the GST API with the following request headers.

#### URL query String:

```text
{{host}}/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/gstin_verification?gstin={{GSTIN_NUMBER_HERE}}
```

#### Request parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| gstin | query | String | Required. GSTIN number you wanted to validate |

#### Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/249ba4-7392-4fa2-b3a0-685c6c7ad87e/gstin_verification?gstin=29AAFCD5862R1ZR
```

#### Sample Response:

{% tabs %}
{% tab title="200" %}
```javascript
{
    "stjCd": "KA004",
    "lgnm": "DEFMACRO SOFTWARE PRIVATE LIMITED",
    "stj": "LVO 015 A - BENGALURU",
    "dty": "Regular",
    "adadr": [],
    "cxdt": "",
    "gstin": "29AAFCD5862R1ZR",
    "nba": [
        "Leasing Business",
        "Supplier of Services",
        "Recipient of Goods or Services",
        "Import"
    ],
    "lstupdt": "30/05/2019",
    "rgdt": "01/08/2017",
    "ctb": "Private Limited Company",
    "pradr": {
        "addr": {
            "bnm": "AMR TECH PARK",
            "loc": "BANGALORE",
            "st": "HOSUR MAIN ROAD",
            "bno": "87/1",
            "stcd": "Karnataka",
            "dst": "Bengaluru (Bangalore) Urban",
            "city": "",
            "flno": "BLOCK 2A FIRST FLOOR",
            "lt": "",
            "pncd": "560068",
            "lg": ""
        },
        "ntr": "Leasing Business, Supplier of Services, Recipient of Goods or Services, Import"
    },
    "tradeNam": "DEFMACRO SOFTWARE PRIVATE LIMITED",
    "sts": "Active",
    "ctjCd": "YV0701",
    "ctj": "RANGE-ASD7"
}
```
{% endtab %}

{% tab title="400" %}
```javascript
{
    "success": false,
    "message": "Invalid GSTIN format. Please enter a valid Format"
}
```
{% endtab %}
{% endtabs %}

#### Taxpayer API Objects

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">stjCd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>
          <br />
        </p>
        <p>State Jurisdiction Code
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lgnm</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Legal Name of Business</td>
    </tr>
    <tr>
      <td style="text-align:left">stj</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <br />State Jurisdiction
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">dty</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Taxpayer type</td>
    </tr>
    <tr>
      <td style="text-align:left">adadr</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left">
        <br />Additional Place of Business Fields
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">cxdt</td>
      <td style="text-align:left">Date [DD/MM/YYYY]</td>
      <td style="text-align:left">
        <br />Date Of Cancellation
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">gstin</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">GSTIN of the Tax Payer</td>
    </tr>
    <tr>
      <td style="text-align:left">nba</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left">Nature of Business Activity</td>
    </tr>
    <tr>
      <td style="text-align:left">lstupdt</td>
      <td style="text-align:left">Date [DD/MM/YYYY]</td>
      <td style="text-align:left">Last Updated Date</td>
    </tr>
    <tr>
      <td style="text-align:left">rgdt</td>
      <td style="text-align:left">Date [DD/MM/YYYY]</td>
      <td style="text-align:left">Date of Registration</td>
    </tr>
    <tr>
      <td style="text-align:left">ctb</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Constitution of Business</td>
    </tr>
    <tr>
      <td style="text-align:left">pradr</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">Principal Place of Business objects.</td>
    </tr>
    <tr>
      <td style="text-align:left">tradeNam</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Trade Name</td>
    </tr>
    <tr>
      <td style="text-align:left">sts</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">GSTIN Status</td>
    </tr>
    <tr>
      <td style="text-align:left">ctjCd</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <br />Centre Jurisdiction Code
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ctj</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <br />Centre Jurisdiction
        <br />
      </td>
    </tr>
  </tbody>
</table>

#### Principal Place of Business object & fields

| Key | Type | Description |
| :--- | :--- | :--- |
| bnm | String | Building Name |
| st | String | Street |
| loc | String | Location |
| bno | String | Door Number |
| stcd | String | State Name |
| dst | String | District |
| city | String | City |
| flno | String | Floor Number |
| lt | String | Latitude |
| pncd | Integer | Pin Code |
| lg | String | Longitude |
| ntr | String | Nature of principle place of business |

## Get Taxpayer Compliance

#### URL query String:

```text
{{host}}/v0.2/taxable_entities/{{TAXABLE_ENTITY_ID}}/returns_filing_status?gstin={{GSTIN_NUMBER_HERE}}
```

#### Request parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| gstin | Query | String | Required. GSTIN number you wanted to validate |

#### Sample Request:

```text
https://gst.cleartax.in/api/v0.2/taxable_entities/249f74-7392-4fa2-b3a0-685c6c7ad87e/gstin_verification?gstin=29AAFCD5862R1ZR
```

#### Sample Response:

{% tabs %}
{% tab title="200" %}
```text
[
  {
      "EFiledlist": [
          {
              "arn": "AA2702188342463",
              "ret_prd": "022018",
              "mof": "ONLINE",
              "dof": "20-03-2018",
              "rtntype": "GSTR3B",
              "status": "Filed",
              "valid": "Y",
              "is_filed_through_ct": false,
              "filedThroughCT": false
          }
      ]
  },
  {
      "EFiledlist": [
          {
              "arn": "AB270219056196Y",
              "ret_prd": "022019",
              "mof": "ONLINE",
              "dof": "20-03-2019",
              "rtntype": "GSTR3B",
              "status": "Filed",
              "valid": "Y",
              "is_filed_through_ct": false,
              "filedThroughCT": false
          }
      ]
  },
  {
      "EFiledlist": [
          {
              "arn": "AB270220282959T",
              "ret_prd": "022020",
              "mof": "ONLINE",
              "dof": "20-03-2020",
              "rtntype": "GSTR3B",
              "status": "Filed",
              "valid": "Y",
              "is_filed_through_ct": false,
              "filedThroughCT": false
          }
      ]
  }
]
```
{% endtab %}
{% endtabs %}

#### Filed list object & fields

| Key | Type | Description |
| :--- | :--- | :--- |
| arn | String | GSTIN number |
| ret\_prd | String | Return period |
| mof | String | Mode of filing |
| dof | String | Date of filing |
| rtntype | String | Return type |
| status | String | Filing status |
| valid | Boolean | Validity |
| is\_filed\_through\_ct | String | If it's filed through ClearTax |

