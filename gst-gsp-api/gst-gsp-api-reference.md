# GST GSP API Reference

## Environments

ClearTax GST GSP has 2 environments:

1. Sandbox Environment
2. Production Environment

### Sandbox Environment

For testing, it is recommended to always use the sandbox environment. To create an account, contact our sales representative with the following information:

1. Company Name
2. Contact Name
3. Contact Email
4. Contact Phone

{% hint style="danger" %}
Once a request for sandbox GSTIN is placed, it will take around 1 week to get it generated.
{% endhint %}

**Host**:

```text
https://gsp-sandbox.internal.cleartax.co/
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our sandbox host to your trust manager, you can download it here.

{% file src="../.gitbook/assets/cleartax.co.cer" caption="ClearTax GST GSP Sandbox SSL" %}

#### GSTN server public key

You can download the latest public key of GSTN for sandbox environment from [https://developer.gst.gov.in/apiportal/howToStart/download](https://developer.gst.gov.in/apiportal/howToStart/download)

### Production Environment

Once you have completed testing, you can move to production. To create an account, contact our sales representative with the following information:

1. Company Name
2. Contact Name
3. Contact Email
4. Contact Phone

For API requests to the production environment, use the below information.

**Host**:

```text
https://gsp.cleartax.in/
```

**Port**: 443

**IP**: ClearTax does not use static IP for APIs. You can whitelist the endpoints based on the host.

**SSL Certificate**:

Our root Certifying Authority is "Amazon Root CA 1". You can get the CER or PEM file directly from Amazon's website here: [https://www.amazontrust.com/repository/](https://www.amazontrust.com/repository/) or download it here.

{% file src="../.gitbook/assets/amazonrootca1.cer" caption="Amazon Root CA 1" %}

In case you want to add the SSL certificate of our production host to your trust manager, you can download it here.

{% file src="../.gitbook/assets/gsp.cleartax.in.cer" caption="ClearTax GST GSP Production SSL Certificate" %}

{% hint style="info" %}
We recommend adding only the Root CA, since the individual host certificates may change often.
{% endhint %}

#### GSTN server public key

You can download the latest public key of GSTN for production environment from [https://developer.gst.gov.in/apiportal/howToStart/download](https://developer.gst.gov.in/apiportal/howToStart/download)

## API documentation

### Authentication

All requests require the user authentication token in the request header.

```
X-CT-Auth-Token: <YOUR-AUTH-TOKEN-HERE>
```

To generate an authentication token, please contact [ClearTax GST Sales](mailto:gst-sales@cleartax.in).

{% hint style="info" %}
For all new users, you DO NOT have to add `clientid` and `client-secret` to the request headers.

For customers migrating from Karvy, please contact integrations-support@cleartax.in for your updated `karvyclientid` and `karvyclient_secret`.
{% endhint %}

### Sample Request

```bash
curl --location --request POST 'https://gsp.cleartax.in/api/taxpayerapi/v0.2/authenticate' \
--header 'Content-Type: application/json' \
--header 'appkey: 48Kw7zR3L9nsbBJI3BJBmg8K0cx/XoGzR6uJaksufhaksfochguhJk1DTvvHYQqQwaU0yhOqfZHgalD9sGMikaEBmY7Y1YcjP5drvwhmmcqQmCLK3D1FE18ditvlqV4DWou5feLM07QwWTj/i8mDwc5YgWz0cYnr6r7wnd2nlbmMxdHOYbKjOP6SxOdD2Gb6GZDI5+RFkkfGSPKwtvXR9NfZQaLaTIY1w8O0X0NI56C9oqjcqT5+FgdpTnLYc3rodHJuEFVgqfeTpWSk3QfAcnQg9P1N9Azcx2OI+AXbLLhcLLbSpfveelhaK02uEdUDYgGHfztr//9RPfqOzg==' \
--header 'X-CT-Auth-Token: a2ceb341-asf12-1234-a54f-59d934acasaa' \
--header 'state-cd: 33' \
--header 'ip-usr: 123.456.789.100' \
--header 'txn: txn123' \
--header 'gstin: gstinNumber' \
--header 'username: username' \
--data-raw '{"action":"OTPREQUEST","app_key":"48Kw7zR3L9nsbBJI3BJBmg8K0cx/XoGzR6uJaksufhaksfochguhJk1DTvvHYQqQwaU0yhOqfZHgalD9sGMikaEBmY7Y1YcjP5drvwhmmcqQmCLK3D1FE18ditvlqV4DWou5feLM07QwWTj/i8mDwc5YgWz0cYnr6r7wnd2nlbmMxdHOYbKjOP6SxOdD2Gb6GZDI5+RFkkfGSPKwtvXR9NfZQaLaTIY1w8O0X0NI56C9oqjcqT5+FgdpTnLYc3rodHJuEFVgqfeTpWSk3QfAcnQg9P1N9Azcx2OI+AXbLLhcLLbSpfveelhaK02uEdUDYgGHfztr//9RPfqOzg==","username":"yourusername"}'
```

For further information on different endpoints like returns, ledger, payment, etc, please refer to the GSTN documentation at [https://developer.gst.gov.in/apiportal/](https://developer.gst.gov.in/apiportal/)

### Error Codes

In case you have received an error code from GSTN, you can check the description of the code in the respective API page here: [https://developer.gst.gov.in/apiportal/](https://developer.gst.gov.in/apiportal/)

