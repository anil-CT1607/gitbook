---
description: Listed below are errors that will be returned in response to a Failure.
---

# Error Codes

## Error Source - Government

## Error Source - Cleartax

| Error Code | Error Message |
| :--- | :--- |
| 201 | NIC Credentials are not Present In Database |
| 101 | Invoice with the Same Transaction ID is Present In the Database |
| 500 | Please contact support with the given Error ID |

## Error Source - Government

#### Invoice

| Error Code | Error Message |
| :--- | :--- |
| 2139 | Error while creating invoice |
| 2140 | Error while validating invoice |
| 2141 | Error while cancelling invoice |
| 2142 | Incomplete request parameters |
| 2143 | Invoice does not belongs to the user GSTIN |
| 2144 | Document date should be in the format \(dd/MM/yyyy\) |
| 2145 | IRN is not valid |
| 2146 | Unable to create IRN, Pls. try after some time |
| 2147 | Unable to sign invoice, Pl try after some time |
| 2148 | Requested IRN data is not available |
| 2150 | Duplicate IRN |
| 2154 | IRN details are not found |
| 2155 | Supplier GSTIN is required |
| 2156 | Invalid format - fromDate\(The correct format is dd/MM/yyyy\) |
| 2157 | Invalid format - toDate \(The correct format is dd/MM/yyyy\) |
| 2159 | Invalid value for  reverse charge applicable field |
| 2161 | Invalid Document Type |
| 2162 | Reverse Charge is applicable only for B2B invoices |
| 2163 | The document date should be yesterday or today . |
| 2169 | Either supplier GSTIN or e-Commerce GSTIN can generate IRN. |
| 2171 | The recipient GSTIN cannot be URP, in case of Deemed Export transaction |
| 2172 | For intra state transaction IGST Amounts are not applicable for item - {0} ,Only Cgst and Sgst Amounts are applicable |
| 2173 | You have exceeded the limit of number of items |
| 2174 | For inter state transaction,  CGST  and SGST  Amounts are not applicable for item - {0}, only Igst Amounts are  Applicable |
| 2176 | Invalid HSN code\(s\)-{0} |
| 2177 | Invalid item unit code\(s\)-{0} |
| 2178 | PIN code does not belong to the state - {0} |
| 2179 | Please check the Tax Rates for valid values\(CGST ,IGST ,SGST Amounts\) |
| 2180 | For export transaction CGST  and SGST Amounts are not allowed for item -{0} |
| 2181 | Intra State transaction are not allowed for export transaction |
| 2182 | Taxable value of all items must be equal to total taxable value |
| 2183 | SGST value of all items must be equal to total SGST Value |
| 2184 | CGST value of all items must be equal to total CGST value |
| 2185 | IGST value of all items must be equal to total IGST Value |
| 2186 | Cess value of all items must be equal to total CessValue |
| 2187 | State Cess Value of all items must be equal to total State CessValue |
| 2188 | Non Advol Cess Value of all items must be equal to total Non Advol CessValue |
| 2189 | Invalid total Invoice Value |
| 2190 | The recipient  Tax type is not valid for this kind of Transaction\(exp\) |
| 2191 | Original invoice number is required in case of Credit / Debit note |
| 2192 | TotAmt value should be equal to  \(Qty \* UnitPrice\) for HSN {0} |
| 2193 | AssAmt value should be equal to \(TotAmt - Discount\) for HSN - {0} |
| 2194 | Invalid total item value for HSN - {0} |
| 2195 | e-Commerce Gstin  should be TCS |
| 2196 | URP is not allowed for export category |
| 2197 | e-commerce GSTIN is mandatory  for e-com Transaction |
| 2198 | Ship details and dispatch details cannot be supplied for transaction type - Regular |
| 2199 | HSN Error |
| 2200 | Invalid state code {0} in dispatch details or ship details |
| 2201 | Invalid Port Code |
| 2202 | Invalid Country Code |
| 2203 | Invalid Foreign Currency |
| 2204 | Ship details should not be sent in case of transaction type Dispatch-from |
| 2205 | Dispatch-from details should not be sent in case of Ship-to transaction |
| 2206 | Ship details are required |
| 2207 | Dispatch details are required |
| 2208 | Export details are required |
| 2209 | Ship details and dispatch details are required |
| 2210 | Original invoice number is not required for the document type Invoice |
| 2211 | Supplier and recipient GSTIN should not be the same. |
| 2212 | The recipient GSTIN cannot be URP for supply type {0} |
| 2213 | The supplier GSTIN cannot be URP |
| 2214 | GSTIN is required For - {0} |
| 2215 | PIN Code and State Code are required  - {0} |
| 2216 | Trade Name is required - {0} |
| 2217 | Location is required - {0} |
| 2218 | The date must be lesser or equal to todays date \(or\) please check the date format |
| 2219 | The from date should be equal or earlier than the to date |
| 2220 | Total discount value cannot be greater than or equal total invoice value |
| 2221 | Select GST Payment for export transaction |
| 2222 | StateCess Rate is incorrect for HSN - {0} |
| 2223 | StateCess is required for HSN - {0} |
| 2224 | e-com Gstin should not be provided |
| 2225 | Incorrect date format in document details |
| 2226 | You are not authorised to get IRN data |
| 2227 | SGST and CGST Amounts should be equal for HSN - {0} |
| 2228 | Item list cannot be empty |
| 2229 | Recipient POS should be other country\(96\) incase of transaction -{0} |
| 2230 | This IRN cannot be cancelled because  e-way bill has been generated , you can cancel   e-way bill and then try cancelling IRN |
| 2231 | Cannot generate e-Invoice as the supplier GSTIN - {0} is SEZ |
| 2232 | POS should be other country\(code: 96 \) for {0} transaction |
| 2233 | Duplicate SI nos are not allowed in items |
| 2234 | Invalid SGST and CGST Amounts for HSN - {0}. |
| 2235 | IGST amount given  with HSN -{0} is Invalid |
| 2236 | In case of export transactions, the ‘Ship-To’ address should be of the place or port from where the goods are being exported. |
| 2237 | The recipient tax payer of is of type SEZ , CGST and SGST Amounts are not allowed for HSN  -{0} |
| 2238 | Quantity is required for HSN - {0} |
| 2239 | Unit is required for HSN - {0} |
| 2240 | Invalid GST rate for HSN -{0} |
| 2241 | CGST and SGST amounts with HSN{0} are required for intra state transaction |
| 2242 | Recipient POS should not  be Other Country\(code -96\) incase of transaction type {0} |
| 2243 | POS should be valid state for {0} transaction |
| 2244 | Recipient PIN code is mandatory for transaction -{0} |
| 2245 | ShipTo state code should be same as POS for B2B transaction |
| 2246 | Recipient  cannot be SEZ for - {0} transaction |
| 2247 | Recipient  should be SEZ for transaction {0} |
| 2248 | Recipient  has to be URP in case of export transactions |
| 2249 | Combination of goods and service items are not allowed for inter state transaction with POS same as the supplier state |
| 2251 | E-Way Bill can be generated provided at least HSN of one item belongs to goods |
| 2252 | E-way Bill  is not generated for document types of Debit Note and Credit Note and Services. |
| 2253 | Vehicle number and vehicle type should be passed in case of transportation mode is Road. |
| 2254 | The transport document number and date should be passed in case of transportation mode is other than Road. |
| 2255 | Requested Payload is empty |
| 2256 | Invalid Signature |
| 2257 | Invalid Credentials for respective IRN |
| 2258 | Supplier GSTIN state code should be same  as the sate code passed in supplier  details |
| 2259 | Invalid supplier  state code |
| 2260 | Invalid recipient  state code |
| 2261 | Recipient  state code should be other country\(code: 96 \) for {0} transaction |
| 2262 | Supplier statecode and POS should be same for intra state supply but chargeable to IGST |
| 2263 | Invalid value for IGSTonIntra field |
| 2264 | Total of other charges in  all items must be equal to other charge in Document total. |
| 2265 | Recipient  GSTIN state code should be same  as the sate code passed in recipient details |
| 2266 | Cess amount given  with HSN -{0} is invalid |
| 2267 | State Cess amount given  with HSN -{0} is Invalid |
| 5001 | Application Error, Please Contact the help desk |
| 5002 | Request body too large |

### Ewaybill

| Error Code | Error Message |
| :--- | :--- |
| 4000 | Status of the IRN is not active |
| 4001 | Error ocurred while creating Eway Bill |
| 4002 | EwayBill is already generated for this IRN |
| 4003 | Requested IRN data is not available |
| 4004 | Error while retrieving IRN details |
| 4005 | Eway Bill details are not found |
| 4006 | Requesting parameter cannot be empty |
| 4007 | Requested e-Way Bill is not available |
| 4008 | Please enter valid e-waybill number |
| 4009 | E Way Bill can be generated provided at least HSN of one item belongs to goods. |
| 4010 | E-way Bill  cannot generated for Debit Note, Credit Note and Services. |
| 4011 | Vehicle number  should be passed in case of transportation mode is Road. |
| 4012 | The transport document number should be passed in case of transportation mode is other than Road. |
| 4013 | The distance between the pincodes given is too high. |
| 4014 | Invalid Vehicle Number |
| 4015 | EWayBill will not be  generated  for blocked User -{0} |
| 4016 | Transport document date cannot be a future date |
| 4017 | Incorrect date format |
| 4018 | Invalid Transporter ID |
| 4019 | Provide Transporter ID in order to generate Part A of e-Way Bill |
| 4020 | Invalid vehicle type . |
| 4021 | Transporter document date cannot be earlier than the invoice date. |
| 4022 | vehicle type should be passed in case of transportation mode is Road. |
| 4023 | The transport document date should be passed in case of transportation mode is other than Road. |
| 4024 | Vehicle type should not be ODC when transmode is other than road |
| 4025 | Invalid User-Id |
| 4026 | Duplicate EwayBill for  document number - \({0}\) |
| 4027 | Transporter Id is mandatory for generation of Part A slip |
| 4028 | Transport mode is mandatory as Vehicle Number/Transport Document Number is given |

