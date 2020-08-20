# Authentication Token

To authenticate any API request to our server, you need to send your user authentication token in the request headers as shown below: 

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
```

This authentication token is scoped to your user account on ClearTax and can be used to access all resources linked to your user account. 

Any request without a valid authentication token will be treated as public access request. For incorrect or missing authentication token, the response will be HTTP Status Code 401 - Unauthorized.

* **Generate** - You can generate an authentication token by logging into your ClearTax account.
* **Label**: It is possible to generate multiple authentication tokens at the same time. To help you identify the tokens in the future, you can name the authentication tokens with labels.
* **Revoke**: You can revoke an authentication token at any time by logging into your ClearTax account.

{% hint style="warning" %}
Warning: ClearTax does not store the token on its side. After generating an authentication token, if you lose or forget the token, it cannot be downloaded from the ClearTax portal again. In such a case, you can generate a new token instead.
{% endhint %}

### Security

Since authentication token is used to authenticate your account access, we highly recommend you to maintain it in a secure manner.

If you suspect that the authentication token may have been compromised, you can revoke the token immediately by logging into the ClearTax account.

