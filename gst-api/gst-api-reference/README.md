# GST API Reference

## Environments

### Production Environment

You can create a testing or a production account at [https://gst.cleartax.in](https://gst.cleartax.in)

For API requests to the production environment, use the below information.

**Host**:

```text
https://gst.cleartax.in/api
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our production host to your trust manager, you can download it here.

{% file src="../../.gitbook/assets/cleartax-gst-production-ssl.cer" caption="ClearTax GST Production SSL" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

## GST JSON API Reference

The JSON Upload API gives you the ability to upload your documents to ClearTax GST with real-time validation check. 

{% page-ref page="json-api-reference/" %}

## GST File Upload API Reference

The File Upload API gives you the ability to upload your documents to ClearTax GST with staged validation checks.

{% page-ref page="file-upload-api-reference.md" %}



