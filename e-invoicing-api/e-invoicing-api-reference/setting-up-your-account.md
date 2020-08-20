# Setting up your account

{% hint style="warning" %}
**Coming soon**: These APIs are currently **NOT** available in the staging environment.
{% endhint %}

ClearTax E-Invoicing is a value-added platform between your ERP and the Government portal. To start making any transaction via ClearTax, first you will have to update your ClearTax account with your NIC credentials. This is generally a one-time activity per user account unless you decide to change the NIC credentials.

In this guide, you will learn how to update NIC credentials in your ClearTax E-Invoicing account.

## Adding/Updating NIC Credentials

You can add or update NIC credentials in ClearTax by sending a `POST` request to E-Invoicing API with the following request headers. 

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/json
```

{% hint style="info" %}
Note: If you already have NIC credentials on your account, using this API will override existing credentials for the specified owner\_id.
{% endhint %}

### Request URL

```text
POST: {{HOST}}/v2/nic_credentials/store_nic_credentials
```

**Request Header**

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| Content-Type | Header | String | Mandatory. This will always be  "application/json". |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Body | String | User's GSTIN |
| username | Body | String | User's NIC Username |
| password | Body | String | User's NIC Password |

#### 

### Request Body

```text
{
    "gstin": "29AAFCD5862R000",
    "username": "username",
    "password": "password"
}
```

### Sample Response

{% tabs %}
{% tab title="Success" %}
```text
{
		"success": true
}
```
{% endtab %}

{% tab title="Error" %}
```
{
    "success": false
}
```
{% endtab %}
{% endtabs %}

