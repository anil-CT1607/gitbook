# Release notes

### Version 1.03:

#### Date: 05/08/2020

#### Release notes for Cleartax and government compatible API’s

* Generation of E-Way Bill as part of IRN registration.
* The response for ‘Generate IRN’ API will have additional attributes "EwbNo","EwbDt", "EwbValidTill".
* Updated the JSON Schema for the generation of IRN as per the schema notified by the Government on 30th July 2020  .
  * IGST\_Applicability\_despite\_Supplier\_and\_Recipient\_located\_in\_same\_State/UT -  new field added - field name= IgstOnIntra
  * Recipient\_State\_Code - Made Mandatory from optional
  * Export\_Duty\_Amount - new field added field name = ExpDuty
  * "TransId" and “TransMode” are optional from Mandatory.
  * BchDtls object moved inside ItemList object.
  * SellerDtls.State field changed to SellerDtls.Stcd
  * PayDtls.Payterm field changed to PayDtls.PayTerm
  * PayDtls.Payinstr  field changed to PayDtls.PayInstr
  * PayDtls.Crtrn field changed to PayDtls.CrTrn
  * PayDtls.Paymtdue field changed to PayDtls.PaymtDue
  * PayDtls.Paidamt field changed to PayDtls.PaidAmt
  * PayDtls.Crday field changed to PayDtls.CrDay
  * PayDtls.Dirdr field changed to PayDtls.DirDr
  * ContrDtls.Porefr field changed to ContrDtls.PORefr
  * ContrDtls.PoRefDt field changed to ContrDtls.PORefDt
  * AddlDocDtls.InfoDtls field changed to AddlDocDtls.Info
* Several new validations are added. A detailed list can be found [here](https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/govt-compatible-apis#validations)
* New API for the generation of E-Way Bill for a given IRN is being provided.
* New API for the cancellation of E-Way Bill is added.
* Error list is updated and can be found [here](https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/error-codes)

{% hint style="success" %}
The version number in the payload will still be  "Version": "1.01" as the Government does not accept it as 1.03
{% endhint %}

