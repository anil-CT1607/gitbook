# E-Invoicing API Reference

## Environments

ClearTax E-Invoicing has 2 environments:

1. Sandbox Environment
2. Production Environment

### Sandbox Environment

For testing, it is recommended to always use the sandbox environment.

For API requests to the sandbox environment, use the below information.

**Host**:

```text
https://einvoicing.internal.cleartax.co
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate:**

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our sandbox host to your trust manager, you can download it here.

{% file src="../../.gitbook/assets/cleartax.co.cer" caption="ClearTax Sandbox SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

### Production Environment

{% hint style="info" %}
The production environment will be available once the government production APIs are published.
{% endhint %}

## Different sets of E-Invoicing API 

ClearTax E-Invoicing provides 2 kinds of APIs:

1. Government Compatible APIs
2. ClearTax E-Invoicing APIs

These are synchronous APIs that cater to basic e-invoicing functionalities and the schema is compatible with the schema provided by the government.

* Generate IRN
* Cancel IRN
* Get Invoice by IRN

These APIs are available for consumption in the staging environment.

{% page-ref page="govt-compatible-apis.md" %}

{% page-ref page="cleartax-e-invoicing-apis-xml-schema/" %}

### Difference between ClearTax API and Government Compatible API

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Actions</b>
        <br />
      </th>
      <th style="text-align:left">Government Compatible API
        <br />
      </th>
      <th style="text-align:left">
        <p>
          <br />
        </p>
        <p>ClearTax API
          <br />
        </p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Generating IRN</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Ability to send Custom fields</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Retry IRN Generation (for invoices failed due to IRP failures)</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Invoice Validation</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Generating IRN (Bulk)</b>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Canceling IRN</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Getting IRN details</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Printing E-invoice</b>
      </td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Y</td>
    </tr>
  </tbody>
</table>

#### 

