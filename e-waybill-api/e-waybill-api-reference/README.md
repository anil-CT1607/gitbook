# E-Waybill API Reference

## Environments

ClearTax E-Waybill has 2 environments:

1. Sandbox Environment
2. Production Environment

### Sandbox Environment

For testing, it is recommended to always use the sandbox environment. To create an account go to [https://ewbfrontend-preprodpub-http.internal.cleartax.co/](https://ewbfrontend-preprodpub-http.internal.cleartax.co/)

For API requests to the sandbox environment, use the below information.

{% hint style="danger" %}
Sandbox accepts ONLY the following GSTIN as seller, receiver and consignee. Please do not use other GSTIN.

Seller - 29AEKPV7203E1Z9

Receiver - 29AAACW6288M1ZH

Consignee - 29AAACW4202F1ZM
{% endhint %}

**Host**:

```text
https://ewbbackend-preprodpub-http.internal.cleartax.co/gst
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our sandbox host to your trust manager, you can download it here.

{% file src="../../.gitbook/assets/cleartax.co.cer" caption="ClearTax Sandbox SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

### Production Environment

Once you have completed testing, you can create a production account at [https://ewb.cleartax.in](https://ewb.cleartax.in)

For API requests to the production environment, use the below information.

**Host**:

```text
https://ewb.cleartax.in/api
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our production host to your trust manager, you can download it here.

{% file src="../../.gitbook/assets/ewb.cleartax.in.cer" caption="ClearTax E-Waybill Production SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

## E-Waybill JSON API Reference

The JSON Upload API gives you the ability to upload your documents to ClearTax E-Waybill with real-time validation check.

{% page-ref page="e-waybill-json-api-reference/" %}

## E-Waybill File Upload API Reference

The File Upload API gives you the ability to upload your documents to ClearTax E-Waybill with staged validation checks.

{% page-ref page="e-waybill-api/" %}

