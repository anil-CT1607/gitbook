---
description: >-
  You can get the list of all upload activities by submitting a GET request to
  the Upload File API
---

# Getting Upload History

{% api-method method="get" host="https://ewb.cleartax.in/api/v0.1/business/" path="{business\_id}/upload\_activity?taxable\_entity\_id={taxable\_entity\_id}&branch\_ids={branch\_id}" %}
{% api-method-summary %}
Get upload history
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the upload history based on GSTIN & Branch.  
**{business\_id}** : taxable entity ID associated to the GSTIN.  
**{taxable\_entity\_id}** : taxable entity ID associated to the GSTIN.  
**{branch\_ids}** : branch IDs associated to the Branch. You can send multiple branch ids to get the upload history.   
**All Branches should be associated to same GSTIN.  
  
Note: For this particular endpoint, you need to use Business ID instead of Taxable Entity ID.**  
  
****`Sample request with multiple branch ids :  
https://ewb.cleartax.in/api/v0.1/business/7a5235d8-c107-483c-b6a0-7ed98417d258/upload_activity?taxable_entity_id=c5cc664c-d473-4ec5-9301-acf43349b7c4&branch_ids=5d2f7742-1484-4bb4-9a5b-b3b8c3586b40&branch_ids=b9356ebb-c114-4e6e-9d37-0bef58d78a61&start=0&limit=20`  
  
****`Sample request with branch_ids : https://ewb.cleartax.in/api/v0.1/business/7a5235d8-c107-483c-b6a0-7ed98417d258/upload_activity?taxable_entity_id=c5cc664c-d473-4ec5-9301-acf43349b7c4&branch_ids=5d2f7742-1484-4bb4-9a5b-b3b8c3586b40&start=0&limit=20`  
  
****`Sample request without branch_ids : https://ewb.cleartax.in/api/v0.1/business/7a5235d8-c107-483c-b6a0-7ed98417d258/upload_activity?taxable_entity_id=c5cc664c-d473-4ec5-9301-acf43349b7c4` 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-Cleartax-Auth-Token: <USER\_AUTH\_TOKEN>" type="string" required=true %}
Auth token will be generated & given upon request..
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="taxable\_entity\_id" type="string" required=true %}
Taxable\_entity\_id of the GSTIN.
{% endapi-method-parameter %}

{% api-method-parameter name="file\_formats" type="array" required=false %}
Based on file format data can be filtered.  
`'XLSX', 'XLS' ,'CSV'`
{% endapi-method-parameter %}

{% api-method-parameter name="status" type="array" required=false %}
Based on status parameter you can fetch the details.  
`'INIT', 'UPLOADED', 'QUEUED', 'PROCESSING', 'PROCESSED', 'ABORTED'`
{% endapi-method-parameter %}

{% api-method-parameter name="upload\_data\_types" type="string" required=false %}
based on data type mentioned in query parameter. it will fetch the details.  
`EWAY_BILLS is the value of this`.
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="string" required=false %}
You can limit the no. of records in the response.
{% endapi-method-parameter %}

{% api-method-parameter name="start" type="string" required=false %}
You can specify the point from where you need the data.  
`By default it starts from 0`
{% endapi-method-parameter %}

{% api-method-parameter name="branch\_ids" type="array" required=false %}
branch id of the branch.  
`You can get data of multiple branches also but all branches should associated to one GSTIN only.`
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Upload history successfully retrieved.  
**Note: Only the response fields relevant for integration are mentioned above. Actual response will have other fields which may not be relevant here.**  
{% endapi-method-response-example-description %}

```javascript
[
    {
        "activity_id": "02de95e9-864d-49b5-a793-5e29f718dd2b",
        "owner_taxable_entity_id": "c5cc664c-d473-4ec5-9301-acf43349b7c4",
        "owner_gstin": "27AACCB1409R1ZH",
        "owner_taxable_entity_name": "Maharashtra",
        "status": "PROCESSED",
        "total_rows_processed": 2,
        "valid_invoice_summary": {
            "totalInvoices": 1,
            "totalValue": null,
            "totalTax": null
        },
        "invalid_invoice_summary": {
            "totalInvoices": 0,
            "totalValue": null,
            "totalTax": null
        },
        "file_url": "https://ewb-prod.s3.ap-south-1.amazonaws.com/c5cc664c-d473-4ec5-9301-acf43349b7c4_5b533998-5373-431b-9a2d-e7345711aa80.xlsx",
        "error_file_url": null,
        "upload_data_type": "EWAY_BILLS",
        "created_at": 1558435350534,
        "updated_at": 1558435351101,
        "error_invoices": null,
        "error_rows": null,
        "error_groups": null,
        "excel_processing_exception": null,
        "file_name": "anto001.xlsx",
        "additional_fields": {
            "return_period": null,
            "vendor_template_type": null,
            "group_id": null,
            "ref_version": null,
            "branch_id": "5d2f7742-1484-4bb4-9a5b-b3b8c3586b40"
        },
        "total_sheets": 7,
        "valid_rows": 2,
        "invalid_rows": 0,
        "total_transactions": 1,
        "file_format": "xlsx",
        "created_by": {
            "userId": 12316,
            "fullName": "Amit Vishwakarma",
            "username": "test25@cleartax.in"
        },
        "has_header_error": false,
        "header_status": "WARNING",
        "error_messages": [],
        "warning_messages": [
            "These headers werent't expected and were ignored: My GSTIN/Transporter ID-if user is Transporter), Customer Shipping Name"
        ],
        "headers": [
            {
                "index": 0,
                "value": "Transaction Type",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 1,
                "value": "Sub Type",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 2,
                "value": "Document Type",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 3,
                "value": "Document Number",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 4,
                "value": "Document Date",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 5,
                "value": "Customer Billing Name",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 6,
                "value": "Customer Billing GSTIN",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 7,
                "value": "Customer Billing Address",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 8,
                "value": "Customer Billing Address 2",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 9,
                "value": "Customer Billing City",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 10,
                "value": "Customer Billing State",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 11,
                "value": "Customer Billing Pincode",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 12,
                "value": "Customer Shipping Name",
                "column_error_message": "This column has been ignored as it was not expected or mapped.",
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "UNKNOWN"
            },
            {
                "index": 13,
                "value": "Customer Shipping Address",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 14,
                "value": "Customer Shipping Address 2",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 15,
                "value": "Customer Shipping City",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 16,
                "value": "Customer Shipping State",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 17,
                "value": "Customer Shipping Pincode",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 18,
                "value": "Product Name",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 19,
                "value": "Item Description",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 20,
                "value": "HSN code",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 21,
                "value": "Item Quantity",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 22,
                "value": "Item Unit of Measurement",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 23,
                "value": "Taxable Value",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 24,
                "value": "CGST Rate",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 25,
                "value": "CGST Amount",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 26,
                "value": "SGST Rate",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 27,
                "value": "SGST Amount",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 28,
                "value": "IGST Rate",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 29,
                "value": "IGST Amount",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 30,
                "value": "CESS Rate",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 31,
                "value": "CESS Amount",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 32,
                "value": "CESS Non Advol Rate",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 33,
                "value": "CESS Non Advol Tax Amount",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 34,
                "value": "Other Value",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 35,
                "value": "Total Transaction Value",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 36,
                "value": "Transportation Mode (Road/Rail/Air/Ship)",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 37,
                "value": "Distance Level (Km)",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 38,
                "value": "Transporter Name",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 39,
                "value": "Transporter ID",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 40,
                "value": "Transporter Doc No",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 41,
                "value": "Transportation Date",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 42,
                "value": "Vehicle Number",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 43,
                "value": "Vehicle Type",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 44,
                "value": "Supplier GSTIN",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 45,
                "value": "Supplier Name",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 46,
                "value": "Supplier Address1",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 47,
                "value": "Supplier Address2",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 48,
                "value": "Supplier Place",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 49,
                "value": "Supplier Pincode",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 50,
                "value": "Supplier State",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": true,
                "status": "KNOWN"
            },
            {
                "index": 51,
                "value": "Dispatch From State",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 52,
                "value": "My GSTIN/Transporter ID-if user is Transporter)",
                "column_error_message": "This column has been ignored as it was not expected or mapped.",
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "UNKNOWN"
            },
            {
                "index": 53,
                "value": "Replace E-way bill",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 54,
                "value": "Is this Supply to/from SEZ unit?",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 55,
                "value": "Eway Bill Transaction Type",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            },
            {
                "index": 56,
                "value": "Sub Type Description",
                "column_error_message": null,
                "has_error": false,
                "row_error_code": 0,
                "key": null,
                "dto_field_identifier": null,
                "dto_field_identifiers": null,
                "is_custom_field": null,
                "type": null,
                "required": false,
                "status": "KNOWN"
            }
        ]
    },
    {
    .....
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
in case provided  details are not valid.
{% endapi-method-response-example-description %}

```
{
    "errors": {
        "err_1": {
            "code": "500",
            "error_group_code": 0,
            "error_id": 0
        }
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



