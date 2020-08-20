# Setting up NIC Credentials

NIC credentials need to be setup with ClearTax for subsequent interactions with NIC. This API allows you to setup NIC credentials on ClearTax.

{% hint style="warning" %}
Warning: If you are using the sandbox host, do not use your production NIC credentials. You can reach out to integrations-support@cleartax.in for sandbox GSTIN credentials.
{% endhint %}

#### API Endpoint

```text
{{HOST}}/v0.1/taxable_entities/{{TAXABLE_ENTITY_ID}}/nic_credentials
```

#### METHOD: PUT

#### Header

```text
X-cleartax-auth-token: {{X-CLEARTAX-AUTH-TOKEN}}
Content-Type:application/json
```

#### Body

```text
{
  "nic_username": "string",
  "nic_password": "string"
}
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| taxable\_entity\_id | Path | String | Required. This is the unique ID associated with the GSTIN in your account. |
| X-cleartax-auth-token | Header | String | Authentication token obtained by calling the "Generating API Auth Token API". |
| nic\_username | Body | String | Username registered on NIC for the GSTIN. |
| nic\_password | Body | String | Latest updated password on NIC for the GSTIN. |

#### Response

{% tabs %}
{% tab title="201" %}
```
Updated the E-Way Bill Credentials
```
{% endtab %}

{% tab title="401" %}
```text
You are not authorised to set/update the credentials for this taxable entity.
```
{% endtab %}
{% endtabs %}

