# Migrating from Karvy GST GSP

{% hint style="info" %}
Karvy GST GSP is acquired by ClearTax. The current Karvy APIs will be deprecated by 15th July 2020. Migrate now.
{% endhint %}

## **SAP CPI Customers**

If you are currently using Karvy iflow in your SAP CPI, you can migrate to ClearTax quickly by following the below steps.

### **Prerequisites**

1. ~~SAP GST GSP Integration Guide \(.pdf file\).~~
2. ~~SAP Cloud Integration Platform - Integration Flow Content package \(.zip file\).~~
3. ~~SAP Cloud Integration Platform - Router Content package \(.zip file\).~~
4. GSTN server public key \(Sandbox and Production\) \(.zip file\).
5. ClearTax GSP SSL certificate \(Sandbox and Production\) \(.cer file\).
6. Externalized Parameters \(Sandbox and Production\)

There is no change in points 1 to 3 above.

#### Download the GSTN server public key

You can download the latest public key of GSTN for both sandbox and production environment from the below link:

[https://developer.gst.gov.in/apiportal/howToStart/download](https://developer.gst.gov.in/apiportal/howToStart/download)

#### Download ClearTax GSP SSL certificate

You can download the SSL certificates below:

{% file src="../.gitbook/assets/cleartax.co.cer" caption="ClearTax GSP Sandbox SSL" %}

{% file src="../.gitbook/assets/gsp.cleartax.in.cer" caption="ClearTax GSP Production SSL" %}

In case you need the root certificate, you can download it from [here](../e-waybill-gsp-api/e-waybill-gsp-api-reference.md#environments).

#### **Obtain Externalized Parameters**

You need to change the following parameters in respective environments.

**Sandbox**

Update the following parameters with the new values:

| Parameter | Value |
| :--- | :--- |
| client-secret | `<same client-secret as before>` |
| clientid | `<same clientid as before>` |
| gspurl | https://gsp-sandbox.internal.cleartax.co/api/ |
| karvyclient-secret | `<please check your email or write to integrations-support@cleartax.in>` |
| karvyclientid | `<same karvyclientid as before>` |
| karvy\_gstn\_auth | https://gsp-sandbox.internal.cleartax.co/api/taxpayerapi/v1.0/authenticate |
| karvy\_gstn\_ret | https://gsp-sandbox.internal.cleartax.co/api/taxpayerapi/v1.1/returns |

**Production**

Update the following parameters with the new values:

| Parameter | Value |
| :--- | :--- |
| client-secret | `<same client-secret as before>` |
| clientid | `<same clientid as before>` |
| gspurl | https://gsp.cleartax.in/api/ |
| karvyclient-secret | `<please write to integrations-support@cleartax.in>` |
| karvyclientid | `<same karvyclientid as before>` |
| karvy\_gstn\_auth | https://gsp.cleartax.in/api/taxpayerapi/v1.0/authenticate |
| karvy\_gstn\_comm | https://gsp.cleartax.in/api/commonapi/v1.1/search |
| karvy\_gstn\_comm\_track\_ret | https://gsp.cleartax.in/api/commonapi/v1.0/returns |
| karvy\_gstn\_ledr | https://gsp.cleartax.in/api/taxpayerapi/v0.3/ledgers |
| karvy\_gstn\_ret | https://gsp.cleartax.in/api/taxpayerapi/v1.1/returns |

The following parameters will remain the same in both sandbox and production.

## Other ERP or Mode

If you are using SAP but not CPI, OR if you are not using SAP, please follow this guide:

{% page-ref page="getting-started-with-gst-gsp-api.md" %}

