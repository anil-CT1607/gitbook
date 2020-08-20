# Generating API Auth Token

This API is used to generate API token. This token is used for authenticating all subsequent API requests.

#### API Endpoint

```text
{{HOST}}/v3/auth/login
```

#### METHOD: POST

#### Header

```text
Content-Type: application/json
```

#### Body

```text
{
  "login_type": "CREDENTIALS",
  "email": "string",
  "password": "string"
}
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| login\_type | Body | String | Set this field to "CREDENTIALS". Other login types are currently not supported for API integrations. |
| email | Body | String | Email id of the account registered with ClearTax |
| password | Body | String | Password of the account registered with Cleartax |

#### Response

{% tabs %}
{% tab title="200" %}
```
{
  "username": "string",
  "product_type": "PRO",
  "user_state": "PROFILE_COMPLETE",
  "api_token": "string",
  "tags": {},
  "external_id": "string",
  "account_type": "PAID_CA",
  "role_name": "string"
}
```
{% endtab %}

{% tab title="401" %}
```text
Invalid credentials
```
{% endtab %}

{% tab title="404" %}
```
User not found. Please signup
```
{% endtab %}
{% endtabs %}



