# Migrating from Karvy EWB GSP

{% hint style="info" %}
Karvy EWB GSP is acquired by ClearTax. The current Karvy APIs will be deprecated by 30th June 2020. Migrate now.
{% endhint %}

## **SAP CPI Customers**

If you are currently using Karvy iflow in your SAP CPI, you can migrate to ClearTax quickly by following the below steps.

### **Prerequisites**

1. ~~SAP EWB GSP Integration Guide \(.pdf file\).~~
2. ~~SAP Cloud Integration Platform - Integration Flow Content package \(.zip file\).~~
3. ~~SAP Cloud Integration Platform - Router Content package \(.zip file\).~~
4. ~~NIC server public key \(Sandbox and Production\) \(.zip file\).~~
5. Register ClearTax as GSP on NIC.
6. ClearTax GSP SSL certificate \(Sandbox and Production\) \(.cer file\).
7. Externalized Parameters \(Sandbox and Production\)

There is no change in points 1 to 4 above.

#### Register ClearTax as GSP on NIC

For the list of sandbox GSTIN username and password, [click here](getting-started-with-gsp-ewb-api/sandbox-gstin-for-ewb-gsp.md). 

To register ClearTax as GSP in NIC portal for production, follow this guide:

{% page-ref page="getting-started-with-gsp-ewb-api/how-to-register-gsp-on-nic.md" %}

#### Download ClearTax GSP SSL certificate

You can download the SSL certificates below:

{% file src="../.gitbook/assets/cleartax.co.cer" caption="ClearTax EWB GSP Sandbox SSL" %}

{% file src="../.gitbook/assets/ewb-gsp.cleartax.in.cer" caption="ClearTax EWB GSP Production SSL " %}

In case you need root certificate, you can download it from [here](e-waybill-gsp-api-reference.md#environments).

#### **Obtain Externalized Parameters**

You need to change only 3 parameters: `karvyclient_secret`, `karvy_auth_url` and `karvy_ewaybill_url`.

**Sandbox**

Update the following parameters with the new values:

| Parameter | Value |
| :--- | :--- |
| karvyclientid | `<same karvyclientid as before>` |
| karvyclient\_secret | `<please check your email or write to integrations-support@cleartax.in>` |
| karvy\_auth\_url | https://ewb-gsp-staging.internal.cleartax.co/ewb-sandbox/v1.03/authenticate |
| karvy\_ewaybill\_url | https://ewb-gsp-staging.internal.cleartax.co/ewb-sandbox/v1.03/ewayapi |

**Production**

Update the following parameters with the new values:

| Parameter | Value |
| :--- | :--- |
| karvyclientid | `<same karvyclientid as before>` |
| karvyclient\_secret | `<please write to integrations-support@cleartax.in>` |
| karvy\_auth\_url | https://ewb-gsp.cleartax.in/ewb/v1.03/authenticate |
| karvy\_ewaybill\_url | https://ewb-gsp.cleartax.in/ewb/v1.03/ewayapi |

The following parameters will remain the same in both sandbox and production.

| Parameter | Value |
| :--- | :--- |
| nicpkalias | niccert |
| nic\_token\_expiry | 300 |

{% hint style="info" %}
Note: NIC public key alias value is alias you have entered as same as the alias of the NIC public key certificate you deployed \(niccert\).
{% endhint %}

### Step by step guide

In your Subaccount &gt; Applications &gt; Subscriptions corresponding to your sandbox \(pre-production\), select the Web UI URL something like: `https://xxx-xxx.xxx.xxx.hana.ondemand.com/itspaces`

**Step 1** – Add and deploy keystore

To deploy keystore, in SCPI Web UI URL, go to Monitor &gt; Manage Security &gt; Keystore &gt; Add keystore \(add an alias and select the ClearTax SSL certificate\) &gt; Deploy &gt; Confirm.

![](../.gitbook/assets/image%20%2813%29.png)

Note: To perform above operation, you need to be a tenant administrator with role AuthGroup.Administrator.

**Step 2** – Test connection

To check the connectivity with GSP, in SCPI Web UI URL, go to Monitor &gt; Manage Security &gt; Connectivity Tests &gt; TLS &gt; Enter the ClearTax EWB GSP base URL without https \(`ewb-gsp-staging.internal.cleartax.co` for sandbox and `ewb-gsp.cleartax.in` for production\) and port &gt; Send. The reponse should be successful.

![](../.gitbook/assets/image%20%2826%29.png)

**Step 3** – Update and deploy GSP iflow

In SCPI Web UI URL, To update the GSP iflow, go to Design &gt; select E-Waybill package &gt; Artifacts &gt; against the gsp iflow, click on actions icon &gt; configure &gt; Define the externalized parameters as provided by ClearTax. Once parameters are updated, click save and then deploy.

![](../.gitbook/assets/image%20%2815%29.png)

![](../.gitbook/assets/image%20%2828%29.png)

After successful deployment, check the integration flows are in `Started` state by choosing Monitor &gt; Manage Integration Content.

![](../.gitbook/assets/image%20%2814%29.png)

**Step 4** – Add user credentials per GSTIN from NIC provided by your GSP.

In SCPI Web UI URL, To add user credentials, go to Monitor &gt; Manage Security &gt; Security Material &gt; Add &gt; User Credentials &gt; Deploy.

![](../.gitbook/assets/image%20%286%29.png)

{% hint style="warning" %}
You can follow the same steps to configure production environment also.

We highly recommend you to test the entire flow with all scenarios in the sandbox environment before moving to production.
{% endhint %}

{% hint style="info" %}
In case there is any change in the API in the future, you will have to update the iFlow which will be provided by ClearTax.
{% endhint %}

### Error Codes

In case you have received an error code from NIC, you can check the description of the code here: [https://docs.ewaybillgst.gov.in/apidocs/api-error-codes-list.html](https://docs.ewaybillgst.gov.in/apidocs/api-error-codes-list.html)

## Other ERP or Mode

If you are using SAP but not CPI, OR if you are not using SAP, please follow this guide:

{% page-ref page="getting-started-with-gsp-ewb-api/" %}



