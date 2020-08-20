# E-Waybill GSP API Reference

## Environments

ClearTax E-Waybill GSP has 2 environments:

1. Sandbox Environment
2. Production Environment

### Sandbox Environment

For testing, it is recommended to always use the sandbox environment. To create an account, contact our sales representative.

For API requests to the sandbox environment, use the below information.

{% hint style="danger" %}
Sandbox accepts ONLY some specific GSTIN as seller, receiver and consignee. Please do not use other GSTIN. [See the list of accepted GSTINs](getting-started-with-gsp-ewb-api/sandbox-gstin-for-ewb-gsp.md).
{% endhint %}

**Host**:

```text
https://ewb-gsp-staging.internal.cleartax.co/ewb-sandbox/v1.03/
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our sandbox host to your trust manager, you can download it here.

{% file src="../.gitbook/assets/cleartax.co.cer" caption="ClearTax Sandbox SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

### Production Environment

Once you have completed testing, you can move to production. To create an account, contact our sales representative.

For API requests to the production environment, use the below information.

**Host**:

```text
https://ewb-gsp.cleartax.in/ewb/v1.03/
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our production host to your trust manager, you can download it here.

{% file src="../.gitbook/assets/ewb-gsp.cleartax.in.cer" caption="ClearTax GSP EWB Production SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

## API documentation

### Authentication

All requests require the user authentication token in the request header.

```
X-CT-Auth-Token: <YOUR-AUTH-TOKEN-HERE>
```

To generate authentication token, please contact [ClearTax GST Sales](mailto:gst-sales@cleartax.in).

{% hint style="info" %}
For all new users, you DO NOT have to add `client-id` and `client-secret` to the request headers.

For customers migrating from Karvy, please contact integrations-support@cleartax.in for your updated `karvyclientid` and `karvyclient_secret`.
{% endhint %}

### Sample Request

```bash
curl --location --request POST 'https://ewb-gsp-staging.internal.cleartax.co/ewb-sandbox/v1.03/authenticate' \
--header 'Gstin: 07AAFCD5862R1ZX' \
--header 'X-CT-Auth-Token: 3c469428-5708-479e-a116-294fd57fe052' \
--header 'Content-Type: application/json' \
--data-raw '{
"action":"ACCESSTOKEN",
"username":"07AAFCD5862R1ZX",
"password":"K+6jVyOIk5nlXCLS+wEKl+MSRZdrZCnEbWu+KqW8ssUeEKNpve04pGMDqReyckqjp8Vp9zQ3/D7TPxP2P8fDU1tWAyPYpIaIr152CjpXTBIRWCkBGbNVtPDMnewe/Ja4z5uNqYFQLQF7xtMk1mAJOa18Fcz99fMoRn1jhIDXNl0AZUf/hUIpKUr5qYNlWvdQPsr2bHMTrf4nIxPtk11kViz8HyF2oNV0zFGlrVRRvpUjdqvDx4b2jssjangPy9eHowKKzzkuTZUx9csgZo59jLVycK8ffBllpCbFvyBuh99VFYfCI1CZ7R7r8ulicuqM6WGkZxTzPgY4LUakQdBUAg==",
"app_key":"dvl3KXUbZ/bHNSl/t1TbFZEbSL/VY+s1AKuvZMdLfg2SOdVjGbarpHvqgLk/+L1FLS93XAWN65Ll+Iwutr3p9W56/O5QcR+kRblyzGk8NNuFGBPqrGvyT7j87NnlN/66jdV01lQW64Sjeeh7Dqhy7eg/s3ZXB53m/PQc7ILrVxEW8EHZl3lAP55XGB5zoryXYUJgaphJ+WVcTaEM60ycLV8zkCjnSQioA1PY8RAA8sdZys2+p9YDewhaqvk9juons35TRG5Bnz6LsxjaeDYkciF/8baZcsNK6q/txffRLtR13uCGYogwHRv80hab/sEdOgd2kRawT0c2d13AU6Z7Lg=="
}'
```

For further information on different endpoints like generate, cancel, extend, etc, please refer to the NIC documentation at [https://docs.ewaybillgst.gov.in/apidocs/index.html](https://docs.ewaybillgst.gov.in/apidocs/index.html)

### Error Codes

In case you have received an error code from NIC, you can check the description of the code here: [https://docs.ewaybillgst.gov.in/apidocs/api-error-codes-list.html](https://docs.ewaybillgst.gov.in/apidocs/api-error-codes-list.html)

