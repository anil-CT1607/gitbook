# Cleartax E-Invoicing APIs

{% hint style="warning" %}
The current version of E-Invoicing APIs are based on the Sandbox APIs of the Government. Since the production APIs are not yet released, the current APIs may change any time.

**Subscribe**: To receive email notification on updates, please subscribe [here](https://forms.gle/YDTpwt5E61xXLWJ47). We'll not spam you :\)
{% endhint %}

These are APIs that covers the basic functionalities of e-invoicing.  These APIs support both JSON and XML data.

**The request and response objects are the same as**[ **objects**](https://cleartax.gitbook.io/cleartax-for-developers/e-invoicing-api/e-invoicing-api-reference/govt-compatible-apis#generating-irn-with-govt-schema) **in government compatible except the custom fields object.**

## Generating IRN

You can generate an IRN by sending a **`PUT`** request to E-Invoicing API with the following request headers.

**Request URL**

```
PUT: {{HOST}}/v2/eInvoice/generate
```

#### Request Headers

{% tabs %}
{% tab title="JSON" %}
```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/json
owner_id:{{owner_id}}
gstin:{{gstin_number}}
```
{% endtab %}

{% tab title="XML" %}
```
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/xml
owner_id:{{owner_id}}
gstin:{{gstin_number}}
```
{% endtab %}
{% endtabs %}

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| Content-Type | Header | String | Mandatory. This will always be  "application/json" for JSON and "application/xml" for XML |
| gstin | Header | String | Mandatory. GSTIN number for the user |
| owner\_id | Header | String | Mandatory. Owner\_id of the user |

#### Sample Request Body

{% tabs %}
{% tab title="JSON" %}
```text
[
  {
    "transaction": {
      "Version": "1.01",
      "TranDtls": {
        "TaxSch": "GST",
        "SupTyp": "B2B",
        "RegRev": "Y",
        "EcmGstin": null,
        "IgstOnIntra": "N"
      },
      "DocDtls": {
        "Typ": "INV",
        "No": "DAOC/007",
        "Dt": "10/08/2020"
      },
      "SellerDtls": {
        "Gstin": "29AAFCD5862R000",
        "LglNm": "NIC company pvt ltd",
        "TrdNm": "NIC Industries",
        "Addr1": "5th block, kuvempu layout",
        "Addr2": "kuvempu layout",
        "Loc": "GANDHINAGAR",
        "Pin": 560037,
        "Stcd": "29",
        "Ph": "9000000000",
        "Em": "abc@gmail.com"
      },
      "BuyerDtls": {
        "Gstin": "29AWGPV7107B1Z1",
        "LglNm": "XYZ company pvt ltd",
        "TrdNm": "XYZ Industries",
        "Pos": "12",
        "Addr1": "7th block, kuvempu layout",
        "Addr2": "kuvempu layout",
        "Loc": "GANDHINAGAR",
        "Pin": 562160,
        "Stcd": "29",
        "Ph": "91111111111",
        "Em": "xyz@yahoo.com"
      },
      "DispDtls": {
        "Nm": "ABC company pvt ltd",
        "Addr1": "7th block, kuvempu layout",
        "Addr2": "kuvempu layout",
        "Loc": "Banagalore",
        "Pin": 562160,
        "Stcd": "29"
      },
      "ShipDtls": {
        "Gstin": "29AWGPV7107B1Z1",
        "LglNm": "CBE company pvt ltd",
        "TrdNm": "kuvempu layout",
        "Addr1": "7th block, kuvempu layout",
        "Addr2": "kuvempu layout",
        "Loc": "Banagalore",
        "Pin": 562160,
        "Stcd": "29"
      },
      "ItemList": [
        {
          "SlNo": "1",
          "PrdDesc": "Rice",
          "IsServc": "N",
          "HsnCd": "1001",
          "Barcde": "123456",
          "Qty": 100.345,
          "FreeQty": 10,
          "Unit": "BAG",
          "UnitPrice": 99.545,
          "TotAmt": 9988.84,
          "Discount": 10,
          "PreTaxVal": 1,
          "AssAmt": 9978.84,
          "GstRt": 12.0,
          "IgstAmt": 1197.46,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 5,
          "CesAmt": 498.94,
          "CesNonAdvlAmt": 10,
          "StateCesRt": 12,
          "StateCesAmt": 1197.46,
          "StateCesNonAdvlAmt": 5,
          "OthChrg": 10,
          "TotItemVal": 12897.7,
          "OrdLineRef": "3256",
          "OrgCntry": "AG",
          "PrdSlNo": "12345",
          "BchDtls": {
            "Nm": "123456",
            "ExpDt": "01/08/2020",
            "WrDt": "01/09/2020"
          },
          "AttribDtls": [
            {
              "Nm": "Rice",
              "Val": "10000"
            }
          ]
        }
      ],
      "ValDtls": {
        "AssVal": 9978.84,
        "CgstVal": 0,
        "SgstVal": 0,
        "IgstVal": 1197.46,
        "CesVal": 508.94,
        "StCesVal": 1202.46,
        "Discount": 10,
        "OthChrg": 20,
        "RndOffAmt": 0.3,
        "TotInvVal": 12908,
        "TotInvValFc": 12897.7
      },
      "PayDtls": {
        "Nm": "ABCDE",
        "AccDet": "5697389713210",
        "Mode": "Cash",
        "FininsBr": "SBIN11000",
        "PayTerm": "100",
        "PayInstr": "Gift",
        "CrTrn": "test",
        "DirDr": "test",
        "CrDay": 100,
        "PaidAmt": 10000,
        "PaymtDue": 5000
         },
      "RefDtls": {
        "InvRm": "TEST",
        "DocPerdDtls": {
          "InvStDt": "01/08/2020",
          "InvEndDt": "01/09/2020"
        },
        "PrecDocDtls": [
          {
            "InvNo": "DOC/002",
            "InvDt": "01/08/2020",
            "OthRefNo": "123456"
          }
        ],
        "ContrDtls": [
          {
            "RecAdvRefr": "Doc/003",
            "RecAdvDt": "01/08/2020",
            "Tendrefr": "Abc001",
            "Contrrefr": "Co123",
            "Extrefr": "Yo456",
            "Projrefr": "Doc-456",
            "Porefr": "Doc-789",
            "PoRefDt": "01/08/2020"
          }
        ]
      },
      "AddlDocDtls": [
        {
          "Url": "https://einv-apisandbox.nic.in",
          "Docs": "Test Doc",
          "Info": "Document Test"
        }
      ],
      "ExpDtls": {
        "ShipBNo": "A-248",
        "ShipBDt": "01/08/2020",
        "Port": "INABG1",
        "RefClm": "N",
        "ForCur": "AED",
        "CntCode": "AE"
      },
      "EwbDtls": {
        "TransId": "12AWGPV7107B1Z1",
        "TransName": "XYZ EXPORTS",
        "Distance": 100,
        "TransDocNo": "DOC01",
        "TransDocDt": "10/08/2020",
        "VehNo": "ka123456",
        "VehType": "R",
        "TransMode": "1"
      }
    }
  }
]
```
{% endtab %}

{% tab title="XML" %}
```
<?xml version="1.0" encoding="UTF-8"?>
<transaction_requests>
    <transaction_request>
        <transaction>
            <Version>1.01</Version>
            <AddlDocDtls>
                <element>
                    <Docs>Test Doc</Docs>
                    <Info>Document Test</Info>
                    <Url>https://einv-apisandbox.nic.in</Url>
                </element>
            </AddlDocDtls>
            <BuyerDtls>
                <Addr1>7th block, kuvempu layout</Addr1>
                <Addr2>kuvempu layout</Addr2>
                <Em>xyz@yahoo.com</Em>
                <Gstin>29AWGPV7107B1Z1</Gstin>
                <LglNm>XYZ company pvt ltd</LglNm>
                <Loc>GANDHINAGAR</Loc>
                <Ph>91111111111</Ph>
                <Pin>562160</Pin>
                <Pos>12</Pos>
                <Stcd>29</Stcd>
                <TrdNm>XYZ Industries</TrdNm>
            </BuyerDtls>
            <DispDtls>
                <Addr1>7th block, kuvempu layout</Addr1>
                <Addr2>kuvempu layout</Addr2>
                <Loc>Banagalore</Loc>
                <Nm>ABC company pvt ltd</Nm>
                <Pin>562160</Pin>
                <Stcd>29</Stcd>
            </DispDtls>
            <DocDtls>
                <Dt>11/08/2020</Dt>
                <No>DOC/P07</No>
                <Typ>INV</Typ>
            </DocDtls>
            <EwbDtls>
                <Distance>100</Distance>
                <TransDocDt>08/08/2020</TransDocDt>
                <TransDocNo>DOC01</TransDocNo>
                <TransId>12AWGPV7107B1Z1</TransId>
                <TransMode>1</TransMode>
                <TransName>XYZ EXPORTS</TransName>
                <VehNo>ka123456</VehNo>
                <VehType>R</VehType>
            </EwbDtls>
            <ExpDtls>
                <CntCode>AE</CntCode>
                <ForCur>AED</ForCur>
                <Port>INABG1</Port>
                <RefClm>N</RefClm>
                <ShipBDt>11/08/2020</ShipBDt>
                <ShipBNo>A-248</ShipBNo>
            </ExpDtls>
            <ItemList>
                <AssAmt>9978.84</AssAmt>
                <AttribDtls>
                        <Nm>Rice</Nm>
                        <Val>10000</Val>
                </AttribDtls>
                <Barcde>123456</Barcde>
                <BchDtls>
                    <Expdt>01/08/2020</Expdt>
                    <Nm>123456</Nm>
                    <wrDt>01/09/2020</wrDt>
                </BchDtls>
                <CesAmt>498.94</CesAmt>
                <CesNonAdvlAmt>10</CesNonAdvlAmt>
                <CesRt>5</CesRt>
                <CgstAmt>0</CgstAmt>
                <Discount>10</Discount>
                <FreeQty>10</FreeQty>
                <GstRt>12.0</GstRt>
                <HsnCd>1001</HsnCd>
                <IgstAmt>1197.46</IgstAmt>
                <IsServc>N</IsServc>
                <OrdLineRef>3256</OrdLineRef>
                <OrgCntry>AG</OrgCntry>
                <OthChrg>10</OthChrg>
                <PrdDesc>Rice</PrdDesc>
                <PrdSlNo>12345</PrdSlNo>
                <PreTaxVal>1</PreTaxVal>
                <Qty>100.345</Qty>
                <SgstAmt>0</SgstAmt>
                <SlNo>1</SlNo>
                <StateCesAmt>1197.46</StateCesAmt>
                <StateCesNonAdvlAmt>5</StateCesNonAdvlAmt>
                <StateCesRt>12</StateCesRt>
                <TotAmt>9988.84</TotAmt>
                <TotItemVal>12897.7</TotItemVal>
                <Unit>BAG</Unit>
                <UnitPrice>99.545</UnitPrice>
            </ItemList>
            <PayDtls>
                <Accdet>5697389713210</Accdet>
                <Crday>100</Crday>
                <Crtrn>test</Crtrn>
                <Dirdr>test</Dirdr>
                <Fininsbr>SBIN11000</Fininsbr>
                <Mode>Cash</Mode>
                <Nm>ABCDE</Nm>
                <Paidamt>10000</Paidamt>
                <Payinstr>Gift</Payinstr>
                <Paymtdue>5000</Paymtdue>
                <Payterm>100</Payterm>
            </PayDtls>
            <RefDtls>
                <ContrDtls>
                        <Contrrefr>Co123</Contrrefr>
                        <Extrefr>Yo456</Extrefr>
                        <PoRefDt>01/08/2020</PoRefDt>
                        <Porefr>Doc-789</Porefr>
                        <Projrefr>Doc-456</Projrefr>
                        <RecAdvDt>01/08/2020</RecAdvDt>
                        <RecAdvRefr>Doc/003</RecAdvRefr>
                        <Tendrefr>Abc001</Tendrefr>
                </ContrDtls>
                <ContrDtls>
                        <Contrrefr>Co124</Contrrefr>
                        <Extrefr>Y1456</Extrefr>
                        <PoRefDt>02/08/2020</PoRefDt>
                        <Porefr>Doc-189</Porefr>
                        <Projrefr>Doc-156</Projrefr>
                        <RecAdvDt>02/08/2020</RecAdvDt>
                        <RecAdvRefr>Doc/103</RecAdvRefr>
                        <Tendrefr>Abc201</Tendrefr>
                </ContrDtls>
                <DocPerdDtls>
                    <InvEndDt>01/09/2020</InvEndDt>
                    <InvStDt>01/08/2020</InvStDt>
                </DocPerdDtls>
                <InvRm>TEST</InvRm>
                <PrecDocDtls>
                        <InvDt>01/08/2020</InvDt>
                        <InvNo>DOC/002</InvNo>
                        <OthRefNo>123456</OthRefNo>
                </PrecDocDtls>
            </RefDtls>
            <SellerDtls>
                <Addr1>5th block, kuvempu layout</Addr1>
                <Addr2>kuvempu layout</Addr2>
                <Em>abc@gmail.com</Em>
                <Gstin>24AAFCD5862R005</Gstin>
                <LglNm>NIC company pvt ltd</LglNm>
                <Loc>GANDHINAGAR</Loc>
                <Ph>9000000000</Ph>
                <Pin>382010</Pin>
                <Stcd>24</Stcd>
                <TrdNm>NIC Industries</TrdNm>
            </SellerDtls>
            <ShipDtls>
                <Addr1>7th block, kuvempu layout</Addr1>
                <Addr2>kuvempu layout</Addr2>
                <Gstin>29AWGPV7107B1Z1</Gstin>
                <LglNm>CBE company pvt ltd</LglNm>
                <Loc>Banagalore</Loc>
                <Pin>562160</Pin>
                <Stcd>29</Stcd>
                <TrdNm>kuvempu layout</TrdNm>
            </ShipDtls>
            <TranDtls>
                <IgstOnIntra>N</IgstOnIntra>
                <RegRev>Y</RegRev>
                <SupTyp>B2B</SupTyp>
                <TaxSch>GST</TaxSch>
            </TranDtls>
            <ValDtls>
                <AssVal>9978.84</AssVal>
                <CesVal>508.94</CesVal>
                <CgstVal>0</CgstVal>
                <Discount>10</Discount>
                <IgstVal>1197.46</IgstVal>
                <OthChrg>20</OthChrg>
                <RndOffAmt>0.3</RndOffAmt>
                <SgstVal>0</SgstVal>
                <StCesVal>1202.46</StCesVal>
                <TotInvVal>12908</TotInvVal>
                <TotInvValFc>12897.7</TotInvValFc>
            </ValDtls>
        </transaction>
    </transaction_request>
</transaction_requests>
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="JSON Response - Success" %}
```text
[
    {
        "custom_fields": null,
        "document_status": "IRN_GENERATED",
        "errors": null,
        "govt_response": {
            "Success": "Y",
            "AckNo": 112010000022258,
            "AckDt": "2020-08-10 11:10:00",
            "Irn": "6308a69f88be31fcdb9ac2c4424bd776aba888bfb44e5a33486b1bdaac726769",
            "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxMTIwMTAwMDAwMjIyNTgsXCJBY2tEdFwiOlwiMjAyMC0wOC0xMCAxMToxMDowMFwiLFwiSXJuXCI6XCI2MzA4YTY5Zjg4YmUzMWZjZGI5YWMyYzQ0MjRiZDc3NmFiYTg4OGJmYjQ0ZTVhMzM0ODZiMWJkYWFjNzI2NzY5XCIsXCJWZXJzaW9uXCI6XCIxLjAxXCIsXCJUcmFuRHRsc1wiOntcIlRheFNjaFwiOlwiR1NUXCIsXCJTdXBUeXBcIjpcIkIyQlwiLFwiUmVnUmV2XCI6XCJZXCIsXCJJZ3N0T25JbnRyYVwiOlwiTlwifSxcIkRvY0R0bHNcIjp7XCJUeXBcIjpcIklOVlwiLFwiTm9cIjpcIkRBT0MvMDA3XCIsXCJEdFwiOlwiMTAvMDgvMjAyMFwifSxcIlNlbGxlckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBQUZDRDU4NjJSMDAwXCIsXCJMZ2xObVwiOlwiTklDIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcIk5JQyBJbmR1c3RyaWVzXCIsXCJBZGRyMVwiOlwiNXRoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjo1NjAwMzcsXCJTdGNkXCI6XCIyOVwiLFwiUGhcIjpcIjkwMDAwMDAwMDBcIixcIkVtXCI6XCJhYmNAZ21haWwuY29tXCJ9LFwiQnV5ZXJEdGxzXCI6e1wiR3N0aW5cIjpcIjI5QVdHUFY3MTA3QjFaMVwiLFwiTGdsTm1cIjpcIlhZWiBjb21wYW55IHB2dCBsdGRcIixcIlRyZE5tXCI6XCJYWVogSW5kdXN0cmllc1wiLFwiUG9zXCI6XCIxMlwiLFwiQWRkcjFcIjpcIjd0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIyXCI6XCJrdXZlbXB1IGxheW91dFwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiUGluXCI6NTYyMTYwLFwiUGhcIjpcIjkxMTExMTExMTExXCIsXCJFbVwiOlwieHl6QHlhaG9vLmNvbVwiLFwiU3RjZFwiOlwiMjlcIn0sXCJEaXNwRHRsc1wiOntcIk5tXCI6XCJBQkMgY29tcGFueSBwdnQgbHRkXCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkJhbmFnYWxvcmVcIixcIlBpblwiOjU2MjE2MCxcIlN0Y2RcIjpcIjI5XCJ9LFwiU2hpcER0bHNcIjp7XCJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJMZ2xObVwiOlwiQ0JFIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkJhbmFnYWxvcmVcIixcIlBpblwiOjU2MjE2MCxcIlN0Y2RcIjpcIjI5XCJ9LFwiSXRlbUxpc3RcIjpbe1wiSXRlbU5vXCI6MSxcIlNsTm9cIjpcIjFcIixcIklzU2VydmNcIjpcIk5cIixcIlByZERlc2NcIjpcIlJpY2VcIixcIkhzbkNkXCI6XCIxMDAxXCIsXCJCYXJjZGVcIjpcIjEyMzQ1NlwiLFwiUXR5XCI6MTAwLjM0NSxcIkZyZWVRdHlcIjoxMC4wLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjo5OS41NDUsXCJUb3RBbXRcIjo5OTg4Ljg0LFwiRGlzY291bnRcIjoxMCxcIlByZVRheFZhbFwiOjEsXCJBc3NBbXRcIjo5OTc4Ljg0LFwiR3N0UnRcIjoxMi4wMDAsXCJJZ3N0QW10XCI6MTE5Ny40NixcIkNnc3RBbXRcIjowLFwiU2dzdEFtdFwiOjAsXCJDZXNSdFwiOjUuMDAwLFwiQ2VzQW10XCI6NDk4Ljk0LFwiQ2VzTm9uQWR2bEFtdFwiOjEwLFwiU3RhdGVDZXNSdFwiOjEyLjAwMCxcIlN0YXRlQ2VzQW10XCI6MTE5Ny40NixcIlN0YXRlQ2VzTm9uQWR2bEFtdFwiOjUsXCJPdGhDaHJnXCI6MTAsXCJUb3RJdGVtVmFsXCI6MTI4OTcuNyxcIk9yZExpbmVSZWZcIjpcIjMyNTZcIixcIk9yZ0NudHJ5XCI6XCJBR1wiLFwiUHJkU2xOb1wiOlwiMTIzNDVcIixcIkJjaER0bHNcIjp7XCJObVwiOlwiMTIzNDU2XCJ9LFwiQXR0cmliRHRsc1wiOlt7XCJObVwiOlwiUmljZVwiLFwiVmFsXCI6XCIxMDAwMFwifV19XSxcIlZhbER0bHNcIjp7XCJBc3NWYWxcIjo5OTc4Ljg0LFwiQ2dzdFZhbFwiOjAsXCJTZ3N0VmFsXCI6MCxcIklnc3RWYWxcIjoxMTk3LjQ2LFwiQ2VzVmFsXCI6NTA4Ljk0LFwiU3RDZXNWYWxcIjoxMjAyLjQ2LFwiRGlzY291bnRcIjoxMCxcIk90aENocmdcIjoyMCxcIlJuZE9mZkFtdFwiOjAuMyxcIlRvdEludlZhbFwiOjEyOTA4LFwiVG90SW52VmFsRmNcIjoxMjg5Ny43fSxcIlBheUR0bHNcIjp7XCJObVwiOlwiQUJDREVcIixcIk1vZGVcIjpcIkNhc2hcIn0sXCJSZWZEdGxzXCI6e1wiSW52Um1cIjpcIlRFU1RcIixcIkRvY1BlcmREdGxzXCI6e1wiSW52U3REdFwiOlwiMDEvMDgvMjAyMFwiLFwiSW52RW5kRHRcIjpcIjAxLzA5LzIwMjBcIn0sXCJQcmVjRG9jRHRsc1wiOlt7XCJJbnZOb1wiOlwiRE9DLzAwMlwiLFwiSW52RHRcIjpcIjAxLzA4LzIwMjBcIixcIk90aFJlZk5vXCI6XCIxMjM0NTZcIn1dLFwiQ29udHJEdGxzXCI6W3tcIlJlY0FkdkR0XCI6XCIwMS8wOC8yMDIwXCJ9XX0sXCJBZGRsRG9jRHRsc1wiOlt7XCJVcmxcIjpcImh0dHBzOi8vZWludi1hcGlzYW5kYm94Lm5pYy5pblwiLFwiRG9jc1wiOlwiVGVzdCBEb2NcIixcIkluZm9cIjpcIkRvY3VtZW50IFRlc3RcIn1dLFwiRXhwRHRsc1wiOntcIlNoaXBCTm9cIjpcIkEtMjQ4XCIsXCJTaGlwQkR0XCI6XCIwMS8wOC8yMDIwXCIsXCJQb3J0XCI6XCJJTkFCRzFcIixcIlJlZkNsbVwiOlwiTlwiLFwiRm9yQ3VyXCI6XCJBRURcIixcIkNudENvZGVcIjpcIkFFXCJ9LFwiRXdiRHRsc1wiOntcIlRyYW5zSWRcIjpcIjEyQVdHUFY3MTA3QjFaMVwiLFwiVHJhbnNOYW1lXCI6XCJYWVogRVhQT1JUU1wiLFwiVHJhbnNNb2RlXCI6XCIxXCIsXCJEaXN0YW5jZVwiOjEwMCxcIlRyYW5zRG9jTm9cIjpcIkRPQzAxXCIsXCJUcmFuc0RvY0R0XCI6XCIxMC8wOC8yMDIwXCIsXCJWZWhOb1wiOlwia2ExMjM0NTZcIixcIlZlaFR5cGVcIjpcIlJcIn19IiwiaXNzIjoiTklDIn0.jrFylbCSdwyOIKlE2d6XZZ-F-95kq5HkP0-c8NyykW7OuX9ikoof6SQdt-KyVwxWAZPRYT2JhQq3GcBn1EiZL1XxZB2O-rOYjiwNRmxH-evdfbevlb7wQm7-vzCaOqxb6yI4k6jbyeZFtpzF8vI6qn2isXDIMSeRAorbGb8GEkc-IoV7VNm_iGgisoUZDVIxsG4xPsw9hgH-QMFuo6TrHqTq9kAkgA9r6MflWZ8k1Gid9-gVugU5IMRItyd7WuHllYID57cwvob4SKO37ZglzaLjkbaCQo-69-Jf7Zgt4m-yoS9yYq-SJDOmBWZWaWzkuCbxgXLTOgTrjVK6IatiRA",
            "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJEb2NOb1wiOlwiREFPQy8wMDdcIixcIkRvY1R5cFwiOlwiSU5WXCIsXCJEb2NEdFwiOlwiMTAvMDgvMjAyMFwiLFwiVG90SW52VmFsXCI6MTI5MDgsXCJJdGVtQ250XCI6MSxcIk1haW5Ic25Db2RlXCI6XCIxMDAxXCIsXCJJcm5cIjpcIjYzMDhhNjlmODhiZTMxZmNkYjlhYzJjNDQyNGJkNzc2YWJhODg4YmZiNDRlNWEzMzQ4NmIxYmRhYWM3MjY3NjlcIn0iLCJpc3MiOiJOSUMifQ.O6Rk7nazmLby_iIcp00ttLf6MeTIGqWt94fjsHIKZY9FiBK944OXO9yqxOJPme0L-ncFZLiyTtVgpjkaH93gXP6flEALQjq0YGwCTrjAUMzbVdh25wRIkp8_mz_tMXMkqSxEOgvEYUZ_wrf_u1hMZNdFefRp50bMzDUro9GcYiNd7aa8Q4Jt7sk2tFypmD5uH0uw8vGYwo3R0Gx_lLAZON6UjPLKyvqPJ2NOGY7zlltMQRWs-xO0oCuuiYUyzeuIPwcYRhnQYyxTBAgqZgZre6cgwN9rx16T1L1Ldi7LWHOTEvOId1HIX9vo4JBcTBOl_vqfeaYpBJqMbuSTKi54-A",
            "Status": "ACT",
            "EwbNo": 171008690004,
            "EwbDt": "2020-08-10 11:10:00",
            "EwbValidTill": "2020-08-11 23:59:00"
        },
        "group_id": null,
        "gstin": "29AAFCD5862R000",
        "owner_id": "147e2-967a-4ebe-ba04-1dedc7b80513",
        "transaction": {
            "Version": "1.01",
            "TranDtls": {
                "TaxSch": "GST",
                "RegRev": "Y",
                "SupTyp": "B2B",
                "IgstOnIntra": "N"
            },
            "DocDtls": {
                "Typ": "INV",
                "No": "DAOC/007",
                "Dt": "10/08/2020"
            },
            "SellerDtls": {
                "Gstin": "29AAFCD5862R000",
                "LglNm": "NIC company pvt ltd",
                "TrdNm": "NIC Industries",
                "Addr1": "5th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "GANDHINAGAR",
                "Pin": 560037,
                "Stcd": "29",
                "Ph": "9000000000",
                "Em": "abc@gmail.com"
            },
            "BuyerDtls": {
                "Gstin": "29AWGPV7107B1Z1",
                "LglNm": "XYZ company pvt ltd",
                "TrdNm": "XYZ Industries",
                "Pos": "12",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "GANDHINAGAR",
                "Pin": 562160,
                "Stcd": "29",
                "Ph": "91111111111",
                "Em": "xyz@yahoo.com"
            },
            "DispDtls": {
                "Nm": "ABC company pvt ltd",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "Banagalore",
                "Pin": 562160,
                "Stcd": "29"
            },
            "ShipDtls": {
                "Gstin": "29AWGPV7107B1Z1",
                "LglNm": "CBE company pvt ltd",
                "TrdNm": "kuvempu layout",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "Banagalore",
                "Pin": 562160,
                "Stcd": "29"
            },
            "ItemList": [
                {
                    "SlNo": "1",
                    "PrdDesc": "Rice",
                    "IsServc": "N",
                    "HsnCd": "1001",
                    "Barcde": "123456",
                    "Qty": 100.345,
                    "FreeQty": 10.0,
                    "Unit": "BAG",
                    "UnitPrice": 99.545,
                    "TotAmt": 9988.84,
                    "Discount": 10,
                    "PreTaxVal": 1,
                    "AssAmt": 9978.84,
                    "GstRt": 12.000,
                    "IgstAmt": 1197.46,
                    "CgstAmt": 0,
                    "SgstAmt": 0,
                    "CesRt": 5.000,
                    "CesAmt": 498.94,
                    "CesNonAdvlAmt": 10,
                    "StateCesRt": 12.000,
                    "StateCesAmt": 1197.46,
                    "StateCesNonAdvlAmt": 5,
                    "OthChrg": 10,
                    "TotItemVal": 12897.7,
                    "OrdLineRef": "3256",
                    "OrgCntry": "AG",
                    "PrdSlNo": "12345",
                    "BchDtls": {
                        "Nm": "123456"
                    },
                    "AttribDtls": [
                        {
                            "Nm": "Rice",
                            "Val": "10000"
                        }
                    ]
                }
            ],
            "ValDtls": {
                "AssVal": 9978.84,
                "CgstVal": 0,
                "SgstVal": 0,
                "IgstVal": 1197.46,
                "CesVal": 508.94,
                "StCesVal": 1202.46,
                "Discount": 10,
                "OthChrg": 20,
                "RndOffAmt": 0.3,
                "TotInvVal": 12908,
                "TotInvValFc": 12897.7
            },
            "PayDtls": {
                "Nm": "ABCDE",
                "Mode": "Cash"
            },
            "RefDtls": {
                "InvRm": "TEST",
                "DocPerdDtls": {
                    "InvStDt": "01/08/2020",
                    "InvEndDt": "01/09/2020"
                },
                "PrecDocDtls": [
                    {
                        "InvNo": "DOC/002",
                        "InvDt": "01/08/2020",
                        "OthRefNo": "123456"
                    }
                ],
                "ContrDtls": [
                    {
                        "RecAdvDt": "01/08/2020"
                    }
                ]
            },
            "AddlDocDtls": [
                {
                    "Url": "https://einv-apisandbox.nic.in",
                    "Docs": "Test Doc",
                    "Info": "Document Test"
                }
            ],
            "ExpDtls": {
                "ShipBNo": "A-248",
                "ShipBDt": "01/08/2020",
                "Port": "INABG1",
                "RefClm": "N",
                "ForCur": "AED",
                "CntCode": "AE"
            },
            "EwbDtls": {
                "TransId": "12AWGPV7107B1Z1",
                "TransName": "XYZ EXPORTS",
                "TransMode": "1",
                "Distance": 100,
                "TransDocNo": "DOC01",
                "TransDocDt": "10/08/2020",
                "VehNo": "ka123456",
                "VehType": "R"
            }
        },
        "transaction_id": "29AAFCD5862R000_DAOC/007_INV_2020",
        "transaction_metadata": null
    }
]
```
{% endtab %}

{% tab title="JSON Response - Failure" %}
```
[
  {
    "owner_id": "87gh1c92-cf28-4174-aacc-245fda688b17",
    "gstin": "29AAFCD5862R000",
    "group_id": "37699782-f02e-400a-b864-51fb6bd7ad99",
    "transaction_id": "29AAFCD5862R000_I-03_INV_2019",
    "transaction": {
      "Version": "1.01",
      "TranDtls": {
        "TaxSch": "GST",
        "RegRev": "Y",
        "SupTyp": "B2B"
      },
      "DocDtls": {
        "Typ": "INV",
        "No": "I-03",
        "Dt": "13/03/2020"
      },
      "SellerDtls": {
        "Gstin": "29AAFCD5862R000",
        "LglNm": "TAN TEST NI",
        "TrdNm": "TAN TEST NI",
        "Addr1": "TEST2",
        "Addr2": "TEST2",
        "Loc": "GANDHINAGAR",
        "Pin": "560002",
        "State": "KARNATAKA",
        "Ph": "9999999999",
        "Em": "ABC@GMAIL.COM"
      },
      "BuyerDtls": {
        "Gstin": "37BZNPM9430M1kl",
        "LglNm": "TAN TEST NI",
        "Pos": "37",
        "Addr1": "TEST2",
        "Addr2": "TEST2",
        "Loc": "GANDHINAGAR",
        "Pin": "560002",
        "State": "KARNATAKA",
        "Ph": "9999999999",
        "Em": "ABC@GMAIL.COM"
      },
      "ItemList": [
        {
          "SlNo": "1",
          "PrdDesc": "dfdfsdf",
          "IsServc": "N",
          "HsnCd": "1001",
          "Qty": "10",
          "Unit": "BAG",
          "UnitPrice": 10,
          "TotAmt": 151,
          "Discount": 0,
          "AssAmt": 151,
          "GstRt": 10,
          "IgstAmt": 10,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 15,
          "CesAmt": 123.89,
          "CesNonAdvlAmt": 0,
          "StateCesRt": 36,
          "StateCesAmt": 151,
          "StateCesNonAdvlAmt": 0,
          "OthChrg": 0,
          "TotItemVal": 100
        }
      ],
      "ValDtls": {
        "AssVal": 100,
        "CgstVal": 0,
        "SgstVal": 0,
        "IgstVal": 0,
        "CesVal": 15,
        "StCesVal": 36,
        "RndOffAmt": 0,
        "TotInvVal": 0
      }
    },
    "custom_fields": {
      "doc_no": "678",
      "name": "Business Name"
    },
    "transaction_metadata": {
      "tag": "Invoice"
    },
    "document_status": "NOT_CREATED",
    "errors": {
      "errors": [
        {
          "error_code": "101",
          "error_message": "Invoice already present in the Database",
          "error_source": "CLEARTAX"
        }
      ]
    },
    "govt_response": {
      "Success": "N",
      "ErrorDetails": [
        {
          "error_code": "2150",
          "error_message": "Duplicate IRN",
          "error_source": "GOVT"
        }
      ],
      "info": [
        {
          "InfCd": "DUPIRN",
          "Desc": {
            "AckNo": "17100216493",
            "AckDt": "2020-03-13 15:49:00",
            "Irn": "488fb4c5fe006062bac4b0e112946bf8679f1db002b300c06738035b84a147cb"
          }
        }
      ]
    }
  }
]
```
{% endtab %}

{% tab title="XML Response - Success" %}
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <eInvoiceTransactionDTOes>
    <invoice_details>
      <owner_id>AnudhiJain</owner_id>
      <gstin>24AAFCD5862R005</gstin>
      <transaction>
        <Version>1.01</Version>
        <TranDtls>
          <TaxSch>GST</TaxSch>
          <RegRev>Y</RegRev>
          <SupTyp>B2B</SupTyp>
          <IgstOnIntra>N</IgstOnIntra>
        </TranDtls>
        <DocDtls>
          <Typ>INV</Typ>
          <No>DOC/P17</No>
          <Dt>11/08/2020</Dt>
        </DocDtls>
        <SellerDtls>
          <Gstin>24AAFCD5862R005</Gstin>
          <LglNm>NIC company pvt ltd</LglNm>
          <TrdNm>NIC Industries</TrdNm>
          <Addr1>5th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>382010</Pin>
          <Stcd>24</Stcd>
          <Ph>9000000000</Ph>
          <Em>abc@gmail.com</Em>
        </SellerDtls>
        <BuyerDtls>
          <Gstin>29AWGPV7107B1Z1</Gstin>
          <LglNm>XYZ company pvt ltd</LglNm>
          <TrdNm>XYZ Industries</TrdNm>
          <Pos>12</Pos>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
          <Ph>91111111111</Ph>
          <Em>xyz@yahoo.com</Em>
        </BuyerDtls>
        <DispDtls>
          <Nm>ABC company pvt ltd</Nm>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>Banagalore</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
        </DispDtls>
        <ShipDtls>
          <Gstin>29AWGPV7107B1Z1</Gstin>
          <LglNm>CBE company pvt ltd</LglNm>
          <TrdNm>kuvempu layout</TrdNm>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>Banagalore</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
        </ShipDtls>
        <ItemList>
          <SlNo>1</SlNo>
          <PrdDesc>Rice</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Barcde>123456</Barcde>
          <Qty>100.345</Qty>
          <FreeQty>10.0</FreeQty>
          <Unit>BAG</Unit>
          <UnitPrice>99.545</UnitPrice>
          <TotAmt>9988.84</TotAmt>
          <Discount>10</Discount>
          <PreTaxVal>1</PreTaxVal>
          <AssAmt>9978.84</AssAmt>
          <GstRt>12.000</GstRt>
          <IgstAmt>1197.46</IgstAmt>
          <CgstAmt>0</CgstAmt>
          <SgstAmt>0</SgstAmt>
          <CesRt>5.000</CesRt>
          <CesAmt>498.94</CesAmt>
          <CesNonAdvlAmt>10</CesNonAdvlAmt>
          <StateCesRt>12.000</StateCesRt>
          <StateCesAmt>1197.46</StateCesAmt>
          <StateCesNonAdvlAmt>5</StateCesNonAdvlAmt>
          <OthChrg>10</OthChrg>
          <TotItemVal>12897.7</TotItemVal>
          <OrdLineRef>3256</OrdLineRef>
          <OrgCntry>AG</OrgCntry>
          <PrdSlNo>12345</PrdSlNo>
          <BchDtls>
            <Nm>123456</Nm>
          </BchDtls>
          <AttribDtls>
            <Nm>Rice</Nm>
            <Val>10000</Val>
          </AttribDtls>
        </ItemList>
        <ValDtls>
          <AssVal>9978.84</AssVal>
          <CgstVal>0</CgstVal>
          <SgstVal>0</SgstVal>
          <IgstVal>1197.46</IgstVal>
          <CesVal>508.94</CesVal>
          <StCesVal>1202.46</StCesVal>
          <Discount>10</Discount>
          <OthChrg>20</OthChrg>
          <RndOffAmt>0.3</RndOffAmt>
          <TotInvVal>12908</TotInvVal>
          <TotInvValFc>12897.7</TotInvValFc>
        </ValDtls>
        <PayDtls>
          <Nm>ABCDE</Nm>
          <Mode>Cash</Mode>
        </PayDtls>
        <RefDtls>
          <InvRm>TEST</InvRm>
          <DocPerdDtls>
            <InvStDt>01/08/2020</InvStDt>
            <InvEndDt>01/09/2020</InvEndDt>
          </DocPerdDtls>
          <PrecDocDtls>
            <InvNo>DOC/002</InvNo>
            <InvDt>01/08/2020</InvDt>
            <OthRefNo>123456</OthRefNo>
          </PrecDocDtls>
          <ContrDtls>
            <RecAdvDt>01/08/2020</RecAdvDt>
          </ContrDtls>
          <ContrDtls>
            <RecAdvDt>02/08/2020</RecAdvDt>
          </ContrDtls>
        </RefDtls>
        <AddlDocDtls/>
        <ExpDtls>
          <ShipBNo>A-248</ShipBNo>
          <ShipBDt>11/08/2020</ShipBDt>
          <Port>INABG1</Port>
          <RefClm>N</RefClm>
          <ForCur>AED</ForCur>
          <CntCode>AE</CntCode>
        </ExpDtls>
        <EwbDtls>
          <TransId>12AWGPV7107B1Z1</TransId>
          <TransName>XYZ EXPORTS</TransName>
          <TransMode>1</TransMode>
          <Distance>100</Distance>
          <TransDocNo>DOC01</TransDocNo>
          <TransDocDt>08/08/2020</TransDocDt>
          <VehNo>ka123456</VehNo>
          <VehType>R</VehType>
        </EwbDtls>
      </transaction>
      <document_status>IRN_GENERATED</document_status>
      <govt_response>
        <Success>Y</Success>
        <AckNo>162010000008493</AckNo>
        <AckDt>2020-08-11 13:48:00</AckDt>
        <Irn>9f0f3edd6c7a8e4d4a0a57afb91bc336315f47c87158e42082e0715094506145</Irn>
        <SignedInvoice>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxNjIwMTAwMDAwMDg0OTMsXCJBY2tEdFwiOlwiMjAyMC0wOC0xMSAxMzo0ODowMFwiLFwiSXJuXCI6XCI5ZjBmM2VkZDZjN2E4ZTRkNGEwYTU3YWZiOTFiYzMzNjMxNWY0N2M4NzE1OGU0MjA4MmUwNzE1MDk0NTA2MTQ1XCIsXCJWZXJzaW9uXCI6XCIxLjAxXCIsXCJUcmFuRHRsc1wiOntcIlRheFNjaFwiOlwiR1NUXCIsXCJTdXBUeXBcIjpcIkIyQlwiLFwiUmVnUmV2XCI6XCJZXCIsXCJJZ3N0T25JbnRyYVwiOlwiTlwifSxcIkRvY0R0bHNcIjp7XCJUeXBcIjpcIklOVlwiLFwiTm9cIjpcIkRPQy9QMTdcIixcIkR0XCI6XCIxMS8wOC8yMDIwXCJ9LFwiU2VsbGVyRHRsc1wiOntcIkdzdGluXCI6XCIyNEFBRkNENTg2MlIwMDVcIixcIkxnbE5tXCI6XCJOSUMgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwiTklDIEluZHVzdHJpZXNcIixcIkFkZHIxXCI6XCI1dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlBpblwiOjM4MjAxMCxcIlN0Y2RcIjpcIjI0XCIsXCJQaFwiOlwiOTAwMDAwMDAwMFwiLFwiRW1cIjpcImFiY0BnbWFpbC5jb21cIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcIlhZWiBJbmR1c3RyaWVzXCIsXCJQb3NcIjpcIjEyXCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjo1NjIxNjAsXCJQaFwiOlwiOTExMTExMTExMTFcIixcIkVtXCI6XCJ4eXpAeWFob28uY29tXCIsXCJTdGNkXCI6XCIyOVwifSxcIkRpc3BEdGxzXCI6e1wiTm1cIjpcIkFCQyBjb21wYW55IHB2dCBsdGRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJTaGlwRHRsc1wiOntcIkdzdGluXCI6XCIyOUFXR1BWNzEwN0IxWjFcIixcIkxnbE5tXCI6XCJDQkUgY29tcGFueSBwdnQgbHRkXCIsXCJUcmRObVwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIxXCI6XCI3dGggYmxvY2ssIGt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMlwiOlwia3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiQmFuYWdhbG9yZVwiLFwiUGluXCI6NTYyMTYwLFwiU3RjZFwiOlwiMjlcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUmljZVwiLFwiSHNuQ2RcIjpcIjEwMDFcIixcIkJhcmNkZVwiOlwiMTIzNDU2XCIsXCJRdHlcIjoxMDAuMzQ1LFwiRnJlZVF0eVwiOjEwLjAsXCJVbml0XCI6XCJCQUdcIixcIlVuaXRQcmljZVwiOjk5LjU0NSxcIlRvdEFtdFwiOjk5ODguODQsXCJEaXNjb3VudFwiOjEwLFwiUHJlVGF4VmFsXCI6MSxcIkFzc0FtdFwiOjk5NzguODQsXCJHc3RSdFwiOjEyLjAwMCxcIklnc3RBbXRcIjoxMTk3LjQ2LFwiQ2dzdEFtdFwiOjAsXCJTZ3N0QW10XCI6MCxcIkNlc1J0XCI6NS4wMDAsXCJDZXNBbXRcIjo0OTguOTQsXCJDZXNOb25BZHZsQW10XCI6MTAsXCJTdGF0ZUNlc1J0XCI6MTIuMDAwLFwiU3RhdGVDZXNBbXRcIjoxMTk3LjQ2LFwiU3RhdGVDZXNOb25BZHZsQW10XCI6NSxcIk90aENocmdcIjoxMCxcIlRvdEl0ZW1WYWxcIjoxMjg5Ny43LFwiT3JkTGluZVJlZlwiOlwiMzI1NlwiLFwiT3JnQ250cnlcIjpcIkFHXCIsXCJQcmRTbE5vXCI6XCIxMjM0NVwiLFwiQmNoRHRsc1wiOntcIk5tXCI6XCIxMjM0NTZcIn0sXCJBdHRyaWJEdGxzXCI6W3tcIk5tXCI6XCJSaWNlXCIsXCJWYWxcIjpcIjEwMDAwXCJ9XX1dLFwiVmFsRHRsc1wiOntcIkFzc1ZhbFwiOjk5NzguODQsXCJDZ3N0VmFsXCI6MCxcIlNnc3RWYWxcIjowLFwiSWdzdFZhbFwiOjExOTcuNDYsXCJDZXNWYWxcIjo1MDguOTQsXCJTdENlc1ZhbFwiOjEyMDIuNDYsXCJEaXNjb3VudFwiOjEwLFwiT3RoQ2hyZ1wiOjIwLFwiUm5kT2ZmQW10XCI6MC4zLFwiVG90SW52VmFsXCI6MTI5MDgsXCJUb3RJbnZWYWxGY1wiOjEyODk3Ljd9LFwiUGF5RHRsc1wiOntcIk5tXCI6XCJBQkNERVwiLFwiTW9kZVwiOlwiQ2FzaFwifSxcIlJlZkR0bHNcIjp7XCJJbnZSbVwiOlwiVEVTVFwiLFwiRG9jUGVyZER0bHNcIjp7XCJJbnZTdER0XCI6XCIwMS8wOC8yMDIwXCIsXCJJbnZFbmREdFwiOlwiMDEvMDkvMjAyMFwifSxcIlByZWNEb2NEdGxzXCI6W3tcIkludk5vXCI6XCJET0MvMDAyXCIsXCJJbnZEdFwiOlwiMDEvMDgvMjAyMFwiLFwiT3RoUmVmTm9cIjpcIjEyMzQ1NlwifV0sXCJDb250ckR0bHNcIjpbe1wiUmVjQWR2RHRcIjpcIjAxLzA4LzIwMjBcIn0se1wiUmVjQWR2RHRcIjpcIjAyLzA4LzIwMjBcIn1dfSxcIkFkZGxEb2NEdGxzXCI6W3t9XSxcIkV4cER0bHNcIjp7XCJTaGlwQk5vXCI6XCJBLTI0OFwiLFwiU2hpcEJEdFwiOlwiMTEvMDgvMjAyMFwiLFwiUG9ydFwiOlwiSU5BQkcxXCIsXCJSZWZDbG1cIjpcIk5cIixcIkZvckN1clwiOlwiQUVEXCIsXCJDbnRDb2RlXCI6XCJBRVwifSxcIkV3YkR0bHNcIjp7XCJUcmFuc0lkXCI6XCIxMkFXR1BWNzEwN0IxWjFcIixcIlRyYW5zTmFtZVwiOlwiWFlaIEVYUE9SVFNcIixcIlRyYW5zTW9kZVwiOlwiMVwiLFwiRGlzdGFuY2VcIjoxMDAsXCJUcmFuc0RvY05vXCI6XCJET0MwMVwiLFwiVHJhbnNEb2NEdFwiOlwiMDgvMDgvMjAyMFwiLFwiVmVoTm9cIjpcImthMTIzNDU2XCIsXCJWZWhUeXBlXCI6XCJSXCJ9fSIsImlzcyI6Ik5JQyJ9.i06l4MmPrGJxbhWwbAKrpGZmB44WV_PsVgWBckzKs6SNiq-m3I995dB--XkDsyEXIHnUj-1rTjXvPGovQQAwJztQu1JXbIodYVSI7treF8qO2j45siex_1l8A218ASujhMTCZfzTtHfTGaUBdZY-uQDLo9eQzxMVGE8IQg_WZeUokDpBhw4YZRL3BT8RTVT0wvhg4n1x9USxtE4A2qtty0OHzgbWe68mE_-_4nTmwf1lb-LPjpNOsWdnwmJPGPE2S1s4ghbqpMUgAEO9lxXgRTn8BJwm4cvKrn2FzU5_go8nsj1Tfk9qAn2OW_lGxhHfcTe5Rg3sDoU3piGZbi6Osw</SignedInvoice>
        <SignedQRCode>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI0QUFGQ0Q1ODYyUjAwNVwiLFwiQnV5ZXJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJEb2NOb1wiOlwiRE9DL1AxN1wiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIxMS8wOC8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMjkwOCxcIkl0ZW1DbnRcIjoxLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiOWYwZjNlZGQ2YzdhOGU0ZDRhMGE1N2FmYjkxYmMzMzYzMTVmNDdjODcxNThlNDIwODJlMDcxNTA5NDUwNjE0NVwifSIsImlzcyI6Ik5JQyJ9.YzWUq_pj6Yj6-3uy06YOmagEZqgg6IOBHs-Nq0bjuDbrpVMbW_-kfHx4gQHG5bWiAesSsYQuFe5Kwng6k94_fMMCbyzKYVKb0s_vgoZo1CND6cCgY0QUQpOMtgGtCfDsZpEEheIuKjFi7LSx12xwuk_ZpVrAwaXIDfhCtQB4RnhWn6gLZfzZeLWmXzd2NDmEVZ1dwhod7xb82LW7ACR9LBqKPVYzOT7GMbiHR25BOEQCnsTwEDPajVJ1KLW4hwd80R-i99zFNj-xZlQoL6Y3mC1RT7WaADUgjwxyfStTjhCJ7ohwu-bkXknLIezDfu3v_XeNuMTnP224-_lXcLVfNg</SignedQRCode>
        <Status>ACT</Status>
        <info>
          <InfCd>EWBERR</InfCd>
          <Desc/>
        </info>
      </govt_response>
    </invoice_details>
  </eInvoiceTransactionDTOes>
```
{% endtab %}

{% tab title="XML Response - Failure" %}
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <eInvoiceTransactionDTOes>
    <invoice_details>
      <owner_id>AnudhiJain</owner_id>
      <gstin>24AAFCD5862R005</gstin>
      <transaction>
        <Version>1.01</Version>
        <TranDtls>
          <TaxSch>GST</TaxSch>
          <RegRev>Y</RegRev>
          <SupTyp>B2B</SupTyp>
          <IgstOnIntra>N</IgstOnIntra>
        </TranDtls>
        <DocDtls>
          <Typ>INV</Typ>
          <No>DOC/P07</No>
          <Dt>11/08/2020</Dt>
        </DocDtls>
        <SellerDtls>
          <Gstin>24AAFCD5862R005</Gstin>
          <LglNm>NIC company pvt ltd</LglNm>
          <TrdNm>NIC Industries</TrdNm>
          <Addr1>5th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>382010</Pin>
          <Stcd>24</Stcd>
          <Ph>9000000000</Ph>
          <Em>abc@gmail.com</Em>
        </SellerDtls>
        <BuyerDtls>
          <Gstin>29AWGPV7107B1Z1</Gstin>
          <LglNm>XYZ company pvt ltd</LglNm>
          <TrdNm>XYZ Industries</TrdNm>
          <Pos>12</Pos>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
          <Ph>91111111111</Ph>
          <Em>xyz@yahoo.com</Em>
        </BuyerDtls>
        <DispDtls>
          <Nm>ABC company pvt ltd</Nm>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>Banagalore</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
        </DispDtls>
        <ShipDtls>
          <Gstin>29AWGPV7107B1Z1</Gstin>
          <LglNm>CBE company pvt ltd</LglNm>
          <TrdNm>kuvempu layout</TrdNm>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Addr2>kuvempu layout</Addr2>
          <Loc>Banagalore</Loc>
          <Pin>562160</Pin>
          <Stcd>29</Stcd>
        </ShipDtls>
        <ItemList>
          <SlNo>1</SlNo>
          <PrdDesc>Rice</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Barcde>123456</Barcde>
          <Qty>100.345</Qty>
          <FreeQty>10.0</FreeQty>
          <Unit>BAG</Unit>
          <UnitPrice>99.545</UnitPrice>
          <TotAmt>9988.84</TotAmt>
          <Discount>10</Discount>
          <PreTaxVal>1</PreTaxVal>
          <AssAmt>9978.84</AssAmt>
          <GstRt>12.000</GstRt>
          <IgstAmt>1197.46</IgstAmt>
          <CgstAmt>0</CgstAmt>
          <SgstAmt>0</SgstAmt>
          <CesRt>5.000</CesRt>
          <CesAmt>498.94</CesAmt>
          <CesNonAdvlAmt>10</CesNonAdvlAmt>
          <StateCesRt>12.000</StateCesRt>
          <StateCesAmt>1197.46</StateCesAmt>
          <StateCesNonAdvlAmt>5</StateCesNonAdvlAmt>
          <OthChrg>10</OthChrg>
          <TotItemVal>12897.7</TotItemVal>
          <OrdLineRef>3256</OrdLineRef>
          <OrgCntry>AG</OrgCntry>
          <PrdSlNo>12345</PrdSlNo>
          <BchDtls>
            <Nm>123456</Nm>
          </BchDtls>
          <AttribDtls>
            <Nm>Rice</Nm>
            <Val>10000</Val>
          </AttribDtls>
        </ItemList>
        <ValDtls>
          <AssVal>9978.84</AssVal>
          <CgstVal>0</CgstVal>
          <SgstVal>0</SgstVal>
          <IgstVal>1197.46</IgstVal>
          <CesVal>508.94</CesVal>
          <StCesVal>1202.46</StCesVal>
          <Discount>10</Discount>
          <OthChrg>20</OthChrg>
          <RndOffAmt>0.3</RndOffAmt>
          <TotInvVal>12908</TotInvVal>
          <TotInvValFc>12897.7</TotInvValFc>
        </ValDtls>
        <PayDtls>
          <Nm>ABCDE</Nm>
          <Mode>Cash</Mode>
        </PayDtls>
        <RefDtls>
          <InvRm>TEST</InvRm>
          <DocPerdDtls>
            <InvStDt>01/08/2020</InvStDt>
            <InvEndDt>01/09/2020</InvEndDt>
          </DocPerdDtls>
          <PrecDocDtls>
            <InvNo>DOC/002</InvNo>
            <InvDt>01/08/2020</InvDt>
            <OthRefNo>123456</OthRefNo>
          </PrecDocDtls>
          <ContrDtls>
            <RecAdvDt>01/08/2020</RecAdvDt>
          </ContrDtls>
          <ContrDtls>
            <RecAdvDt>02/08/2020</RecAdvDt>
          </ContrDtls>
        </RefDtls>
        <AddlDocDtls/>
        <ExpDtls>
          <ShipBNo>A-248</ShipBNo>
          <ShipBDt>11/08/2020</ShipBDt>
          <Port>INABG1</Port>
          <RefClm>N</RefClm>
          <ForCur>AED</ForCur>
          <CntCode>AE</CntCode>
        </ExpDtls>
        <EwbDtls>
          <TransId>12AWGPV7107B1Z1</TransId>
          <TransName>XYZ EXPORTS</TransName>
          <TransMode>1</TransMode>
          <Distance>100</Distance>
          <TransDocNo>DOC01</TransDocNo>
          <TransDocDt>08/08/2020</TransDocDt>
          <VehNo>ka123456</VehNo>
          <VehType>R</VehType>
        </EwbDtls>
      </transaction>
      <document_status>NOT_CREATED</document_status>
      <errors>
        <errorDetails>
          <error_code>101</error_code>
          <error_message>Invoice with the Same Transaction ID is Present In the Database</error_message>
          <error_source>CLEARTAX</error_source>
        </errorDetails>
      </errors>
      <govt_response>
        <Success>N</Success>
        <ErrorDetails>
          <error_code>2150</error_code>
          <error_message>Duplicate IRN</error_message>
          <error_source>GOVT</error_source>
        </ErrorDetails>
        <info>
          <InfCd>DUPIRN</InfCd>
          <Desc/>
        </info>
      </govt_response>
    </invoice_details>
  </eInvoiceTransactionDTOes>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For bulk generation, you can send a list of up to 10 Invoice Objects in the same request body.
{% endhint %}

## Getting Invoice by IRN

You can get an Invoice by IRN by sending a `GET` request to E-Invoicing API with the following request headers.

```
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

**Request URL**

```text
GET: {{HOST}}/v2/eInvoice/get
```

#### Request Parameters:

| Parameters | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| IRN | Path | String | Mandatory. IRN generated for the invoice. |

**Sample Request:**

```text
https://einvoicing.internal.cleartax.co/v2/eInvoice/get/irn/2d5b90edf2819c91f660a6d6843346fab0d57a27badf92ac8f7fbc8762f50ab1
```

**Sample Response**

{% tabs %}
{% tab title="Valid Response" %}
```text
[
    {
        "custom_fields": null,
        "document_status": "IRN_GENERATED",
        "errors": null,
        "govt_response": {
            "Success": "Y",
            "AckNo": 112010000022258,
            "AckDt": "2020-08-10 11:10:00",
            "Irn": "6308a69f88be31fcdb9ac2c4424bd776aba888bfb44e5a33486b1bdaac726769",
            "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxMTIwMTAwMDAwMjIyNTgsXCJBY2tEdFwiOlwiMjAyMC0wOC0xMCAxMToxMDowMFwiLFwiSXJuXCI6XCI2MzA4YTY5Zjg4YmUzMWZjZGI5YWMyYzQ0MjRiZDc3NmFiYTg4OGJmYjQ0ZTVhMzM0ODZiMWJkYWFjNzI2NzY5XCIsXCJWZXJzaW9uXCI6XCIxLjAxXCIsXCJUcmFuRHRsc1wiOntcIlRheFNjaFwiOlwiR1NUXCIsXCJTdXBUeXBcIjpcIkIyQlwiLFwiUmVnUmV2XCI6XCJZXCIsXCJJZ3N0T25JbnRyYVwiOlwiTlwifSxcIkRvY0R0bHNcIjp7XCJUeXBcIjpcIklOVlwiLFwiTm9cIjpcIkRBT0MvMDA3XCIsXCJEdFwiOlwiMTAvMDgvMjAyMFwifSxcIlNlbGxlckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBQUZDRDU4NjJSMDAwXCIsXCJMZ2xObVwiOlwiTklDIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcIk5JQyBJbmR1c3RyaWVzXCIsXCJBZGRyMVwiOlwiNXRoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjo1NjAwMzcsXCJTdGNkXCI6XCIyOVwiLFwiUGhcIjpcIjkwMDAwMDAwMDBcIixcIkVtXCI6XCJhYmNAZ21haWwuY29tXCJ9LFwiQnV5ZXJEdGxzXCI6e1wiR3N0aW5cIjpcIjI5QVdHUFY3MTA3QjFaMVwiLFwiTGdsTm1cIjpcIlhZWiBjb21wYW55IHB2dCBsdGRcIixcIlRyZE5tXCI6XCJYWVogSW5kdXN0cmllc1wiLFwiUG9zXCI6XCIxMlwiLFwiQWRkcjFcIjpcIjd0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIyXCI6XCJrdXZlbXB1IGxheW91dFwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiUGluXCI6NTYyMTYwLFwiUGhcIjpcIjkxMTExMTExMTExXCIsXCJFbVwiOlwieHl6QHlhaG9vLmNvbVwiLFwiU3RjZFwiOlwiMjlcIn0sXCJEaXNwRHRsc1wiOntcIk5tXCI6XCJBQkMgY29tcGFueSBwdnQgbHRkXCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkJhbmFnYWxvcmVcIixcIlBpblwiOjU2MjE2MCxcIlN0Y2RcIjpcIjI5XCJ9LFwiU2hpcER0bHNcIjp7XCJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJMZ2xObVwiOlwiQ0JFIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiVHJkTm1cIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcImt1dmVtcHUgbGF5b3V0XCIsXCJMb2NcIjpcIkJhbmFnYWxvcmVcIixcIlBpblwiOjU2MjE2MCxcIlN0Y2RcIjpcIjI5XCJ9LFwiSXRlbUxpc3RcIjpbe1wiSXRlbU5vXCI6MSxcIlNsTm9cIjpcIjFcIixcIklzU2VydmNcIjpcIk5cIixcIlByZERlc2NcIjpcIlJpY2VcIixcIkhzbkNkXCI6XCIxMDAxXCIsXCJCYXJjZGVcIjpcIjEyMzQ1NlwiLFwiUXR5XCI6MTAwLjM0NSxcIkZyZWVRdHlcIjoxMC4wLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjo5OS41NDUsXCJUb3RBbXRcIjo5OTg4Ljg0LFwiRGlzY291bnRcIjoxMCxcIlByZVRheFZhbFwiOjEsXCJBc3NBbXRcIjo5OTc4Ljg0LFwiR3N0UnRcIjoxMi4wMDAsXCJJZ3N0QW10XCI6MTE5Ny40NixcIkNnc3RBbXRcIjowLFwiU2dzdEFtdFwiOjAsXCJDZXNSdFwiOjUuMDAwLFwiQ2VzQW10XCI6NDk4Ljk0LFwiQ2VzTm9uQWR2bEFtdFwiOjEwLFwiU3RhdGVDZXNSdFwiOjEyLjAwMCxcIlN0YXRlQ2VzQW10XCI6MTE5Ny40NixcIlN0YXRlQ2VzTm9uQWR2bEFtdFwiOjUsXCJPdGhDaHJnXCI6MTAsXCJUb3RJdGVtVmFsXCI6MTI4OTcuNyxcIk9yZExpbmVSZWZcIjpcIjMyNTZcIixcIk9yZ0NudHJ5XCI6XCJBR1wiLFwiUHJkU2xOb1wiOlwiMTIzNDVcIixcIkJjaER0bHNcIjp7XCJObVwiOlwiMTIzNDU2XCJ9LFwiQXR0cmliRHRsc1wiOlt7XCJObVwiOlwiUmljZVwiLFwiVmFsXCI6XCIxMDAwMFwifV19XSxcIlZhbER0bHNcIjp7XCJBc3NWYWxcIjo5OTc4Ljg0LFwiQ2dzdFZhbFwiOjAsXCJTZ3N0VmFsXCI6MCxcIklnc3RWYWxcIjoxMTk3LjQ2LFwiQ2VzVmFsXCI6NTA4Ljk0LFwiU3RDZXNWYWxcIjoxMjAyLjQ2LFwiRGlzY291bnRcIjoxMCxcIk90aENocmdcIjoyMCxcIlJuZE9mZkFtdFwiOjAuMyxcIlRvdEludlZhbFwiOjEyOTA4LFwiVG90SW52VmFsRmNcIjoxMjg5Ny43fSxcIlBheUR0bHNcIjp7XCJObVwiOlwiQUJDREVcIixcIk1vZGVcIjpcIkNhc2hcIn0sXCJSZWZEdGxzXCI6e1wiSW52Um1cIjpcIlRFU1RcIixcIkRvY1BlcmREdGxzXCI6e1wiSW52U3REdFwiOlwiMDEvMDgvMjAyMFwiLFwiSW52RW5kRHRcIjpcIjAxLzA5LzIwMjBcIn0sXCJQcmVjRG9jRHRsc1wiOlt7XCJJbnZOb1wiOlwiRE9DLzAwMlwiLFwiSW52RHRcIjpcIjAxLzA4LzIwMjBcIixcIk90aFJlZk5vXCI6XCIxMjM0NTZcIn1dLFwiQ29udHJEdGxzXCI6W3tcIlJlY0FkdkR0XCI6XCIwMS8wOC8yMDIwXCJ9XX0sXCJBZGRsRG9jRHRsc1wiOlt7XCJVcmxcIjpcImh0dHBzOi8vZWludi1hcGlzYW5kYm94Lm5pYy5pblwiLFwiRG9jc1wiOlwiVGVzdCBEb2NcIixcIkluZm9cIjpcIkRvY3VtZW50IFRlc3RcIn1dLFwiRXhwRHRsc1wiOntcIlNoaXBCTm9cIjpcIkEtMjQ4XCIsXCJTaGlwQkR0XCI6XCIwMS8wOC8yMDIwXCIsXCJQb3J0XCI6XCJJTkFCRzFcIixcIlJlZkNsbVwiOlwiTlwiLFwiRm9yQ3VyXCI6XCJBRURcIixcIkNudENvZGVcIjpcIkFFXCJ9LFwiRXdiRHRsc1wiOntcIlRyYW5zSWRcIjpcIjEyQVdHUFY3MTA3QjFaMVwiLFwiVHJhbnNOYW1lXCI6XCJYWVogRVhQT1JUU1wiLFwiVHJhbnNNb2RlXCI6XCIxXCIsXCJEaXN0YW5jZVwiOjEwMCxcIlRyYW5zRG9jTm9cIjpcIkRPQzAxXCIsXCJUcmFuc0RvY0R0XCI6XCIxMC8wOC8yMDIwXCIsXCJWZWhOb1wiOlwia2ExMjM0NTZcIixcIlZlaFR5cGVcIjpcIlJcIn19IiwiaXNzIjoiTklDIn0.jrFylbCSdwyOIKlE2d6XZZ-F-95kq5HkP0-c8NyykW7OuX9ikoof6SQdt-KyVwxWAZPRYT2JhQq3GcBn1EiZL1XxZB2O-rOYjiwNRmxH-evdfbevlb7wQm7-vzCaOqxb6yI4k6jbyeZFtpzF8vI6qn2isXDIMSeRAorbGb8GEkc-IoV7VNm_iGgisoUZDVIxsG4xPsw9hgH-QMFuo6TrHqTq9kAkgA9r6MflWZ8k1Gid9-gVugU5IMRItyd7WuHllYID57cwvob4SKO37ZglzaLjkbaCQo-69-Jf7Zgt4m-yoS9yYq-SJDOmBWZWaWzkuCbxgXLTOgTrjVK6IatiRA",
            "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMjlBV0dQVjcxMDdCMVoxXCIsXCJEb2NOb1wiOlwiREFPQy8wMDdcIixcIkRvY1R5cFwiOlwiSU5WXCIsXCJEb2NEdFwiOlwiMTAvMDgvMjAyMFwiLFwiVG90SW52VmFsXCI6MTI5MDgsXCJJdGVtQ250XCI6MSxcIk1haW5Ic25Db2RlXCI6XCIxMDAxXCIsXCJJcm5cIjpcIjYzMDhhNjlmODhiZTMxZmNkYjlhYzJjNDQyNGJkNzc2YWJhODg4YmZiNDRlNWEzMzQ4NmIxYmRhYWM3MjY3NjlcIn0iLCJpc3MiOiJOSUMifQ.O6Rk7nazmLby_iIcp00ttLf6MeTIGqWt94fjsHIKZY9FiBK944OXO9yqxOJPme0L-ncFZLiyTtVgpjkaH93gXP6flEALQjq0YGwCTrjAUMzbVdh25wRIkp8_mz_tMXMkqSxEOgvEYUZ_wrf_u1hMZNdFefRp50bMzDUro9GcYiNd7aa8Q4Jt7sk2tFypmD5uH0uw8vGYwo3R0Gx_lLAZON6UjPLKyvqPJ2NOGY7zlltMQRWs-xO0oCuuiYUyzeuIPwcYRhnQYyxTBAgqZgZre6cgwN9rx16T1L1Ldi7LWHOTEvOId1HIX9vo4JBcTBOl_vqfeaYpBJqMbuSTKi54-A",
            "Status": "ACT",
            "EwbNo": 171008690004,
            "EwbDt": "2020-08-10 11:10:00",
            "EwbValidTill": "2020-08-11 23:59:00"
        },
        "group_id": null,
        "gstin": "29AAFCD5862R000",
        "owner_id": "147ee2-967a-4ebe-ba04-1dedc7b80513",
        "transaction": {
            "Version": "1.01",
            "Irn": "6308a69f88be31fcdb9ac2c4424bd776aba888bfb44e5a33486b1bdaac726769",
            "TranDtls": {
                "TaxSch": "GST",
                "RegRev": "Y",
                "SupTyp": "B2B",
                "IgstOnIntra": "N"
            },
            "DocDtls": {
                "Typ": "INV",
                "No": "DAOC/007",
                "Dt": "10/08/2020"
            },
            "SellerDtls": {
                "Gstin": "29AAFCD5862R000",
                "LglNm": "NIC company pvt ltd",
                "TrdNm": "NIC Industries",
                "Addr1": "5th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "GANDHINAGAR",
                "Pin": 560037,
                "Stcd": "29",
                "Ph": "9000000000",
                "Em": "abc@gmail.com"
            },
            "BuyerDtls": {
                "Gstin": "29AWGPV7107B1Z1",
                "LglNm": "XYZ company pvt ltd",
                "TrdNm": "XYZ Industries",
                "Pos": "12",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "GANDHINAGAR",
                "Pin": 562160,
                "Stcd": "29",
                "Ph": "91111111111",
                "Em": "xyz@yahoo.com"
            },
            "DispDtls": {
                "Nm": "ABC company pvt ltd",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "Banagalore",
                "Pin": 562160,
                "Stcd": "29"
            },
            "ShipDtls": {
                "Gstin": "29AWGPV7107B1Z1",
                "LglNm": "CBE company pvt ltd",
                "TrdNm": "kuvempu layout",
                "Addr1": "7th block, kuvempu layout",
                "Addr2": "kuvempu layout",
                "Loc": "Banagalore",
                "Pin": 562160,
                "Stcd": "29"
            },
            "ItemList": [
                {
                    "SlNo": "1",
                    "PrdDesc": "Rice",
                    "IsServc": "N",
                    "HsnCd": "1001",
                    "Barcde": "123456",
                    "Qty": 100.345,
                    "FreeQty": 10.0,
                    "Unit": "BAG",
                    "UnitPrice": 99.545,
                    "TotAmt": 9988.84,
                    "Discount": 10,
                    "PreTaxVal": 1,
                    "AssAmt": 9978.84,
                    "GstRt": 12.000,
                    "IgstAmt": 1197.46,
                    "CgstAmt": 0,
                    "SgstAmt": 0,
                    "CesRt": 5.000,
                    "CesAmt": 498.94,
                    "CesNonAdvlAmt": 10,
                    "StateCesRt": 12.000,
                    "StateCesAmt": 1197.46,
                    "StateCesNonAdvlAmt": 5,
                    "OthChrg": 10,
                    "TotItemVal": 12897.7,
                    "OrdLineRef": "3256",
                    "OrgCntry": "AG",
                    "PrdSlNo": "12345",
                    "BchDtls": {
                        "Nm": "123456"
                    },
                    "AttribDtls": [
                        {
                            "Nm": "Rice",
                            "Val": "10000"
                        }
                    ]
                }
            ],
            "ValDtls": {
                "AssVal": 9978.84,
                "CgstVal": 0,
                "SgstVal": 0,
                "IgstVal": 1197.46,
                "CesVal": 508.94,
                "StCesVal": 1202.46,
                "Discount": 10,
                "OthChrg": 20,
                "RndOffAmt": 0.3,
                "TotInvVal": 12908,
                "TotInvValFc": 12897.7
            },
            "PayDtls": {
                "Nm": "ABCDE",
                "Mode": "Cash"
            },
            "RefDtls": {
                "InvRm": "TEST",
                "DocPerdDtls": {
                    "InvStDt": "01/08/2020",
                    "InvEndDt": "01/09/2020"
                },
                "PrecDocDtls": [
                    {
                        "InvNo": "DOC/002",
                        "InvDt": "01/08/2020",
                        "OthRefNo": "123456"
                    }
                ],
                "ContrDtls": [
                    {
                        "RecAdvDt": "01/08/2020"
                    }
                ]
            },
            "AddlDocDtls": [
                {
                    "Url": "https://einv-apisandbox.nic.in",
                    "Docs": "Test Doc",
                    "Info": "Document Test"
                }
            ],
            "ExpDtls": {
                "ShipBNo": "A-248",
                "ShipBDt": "01/08/2020",
                "Port": "INABG1",
                "RefClm": "N",
                "ForCur": "AED",
                "CntCode": "AE"
            },
            "EwbDtls": {
                "TransId": "12AWGPV7107B1Z1",
                "TransName": "XYZ EXPORTS",
                "TransMode": "1",
                "Distance": 100,
                "TransDocNo": "DOC01",
                "TransDocDt": "10/08/2020",
                "VehNo": "ka123456",
                "VehType": "R"
            }
        },
        "transaction_id": "29AAFCD5862R000_DAOC/007_INV_2020",
        "transaction_metadata": null
    }
]
```
{% endtab %}

{% tab title="Invalid Response" %}
```
[
    {
        "custom_fields": null,
        "document_status": "IRN_GENERATION_FAILED",
        "errors": null,
        "govt_response": {
            "Success": "N",
            "ErrorDetails": [
                {
                    "error_code": "2148",
                    "error_message": "Requested IRN data is not available",
                    "error_source": "GOVT"
                }
            ]
        },
        "group_id": null,
        "gstin": "29AAFCD5862R000",
        "owner_id": "147f8ee2-967a-4ebe-ba04-1dedc7b80513",
        "transaction": null,
        "transaction_id": null,
        "transaction_metadata": null
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
The invoice you receive in response to this API is the invoice persisted by ClearTax. This may include fields sent by you at the time of generation which may not be part of the invoice returned by the Government.
{% endhint %}

## Cancelling IRN

You can cancel an IRN by sending a **`PUT`** request to E-Invoicing API with the following request headers.

{% hint style="danger" %}
IRN cannot be cancelled, if the Valid/Active E-way Bill exists for the same.
{% endhint %}

**Request URL**

```text
PUT {{HOST}}/v2/eInvoice​/cancel
```

#### Request Headers

{% tabs %}
{% tab title="JSON" %}
```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/json
gstin:{{gstin_number}}
owner_id:{{owner_id}}
```
{% endtab %}

{% tab title="XML" %}
```
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
Content-Type: application/xml
```
{% endtab %}
{% endtabs %}

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| Content-Type | Header | String | Mandatory. This will always be  "application/json" for JSON and "application/xml" for XML |
| gstin | Header | String | Mandatory. GSTIN number for the user |
| owner\_id | Header | String | Mandatory. Owner\_id of the user |

#### Sample Request Body

{% tabs %}
{% tab title="JSON" %}
```text
[
  {
    "irn": "9a3d2e1d74e4db5e007862e85028fb047e6ff6aba2415cfb45c049a4564e80d8",
    "CnlRsn": "1",
    "CnlRem": "string"
  }
]
```
{% endtab %}

{% tab title="XML" %}
```
<?xml version="1.0" encoding="UTF-8" ?>
<cancel_irn_requests>
    <cancel_irn_request>
        <irn>dc0bf021c9d1180a82443bd29a63abb6935aa15db8c1f399813f68ceb5043dc6</irn>
        <CnlRsn>1</CnlRsn>
        <CnlRem>Random</CnlRem>
    </cancel_irn_request>
</cancel_irn_requests>
```
{% endtab %}
{% endtabs %}

#### Sample Response

{% tabs %}
{% tab title="JSON Response - Success" %}
```text
[
  {
    "owner_id": "87gh1c92-cf28-4174-aacc-245fda688b17",
    "gstin": "29AAFCD5862R000",
    "group_id": "3fe6e245-4489-448a-b438-316991ce3db8",
    "transaction_id": "29AAFCD5862R000_INV-970_INV_2019",
    "transaction": {
      "Version": "1.01",
      "Irn": "9a3d2e1d74e4db5e007862e85028fb047e6ff6aba2415cfb45c049a4564e80d8",
      "TranDtls": {
        "TaxSch": "GST",
        "RegRev": "N",
        "SupTyp": "B2B"
      },
      "DocDtls": {
        "Typ": "INV",
        "No": "INV-970",
        "Dt": "12/03/2020"
      },
      "SellerDtls": {
        "Gstin": "29AAFCD5862R000",
        "LglNm": "ABC company pvt ltd",
        "Addr1": "5th block, kuvempu layout",
        "Addr2": "QvBQYuxiXXVytGCxzVllpgTJKhRQq",
        "Loc": "GANDHINAGAR",
        "Pin": "560002",
        "State": "KARNATAKA"
      },
      "BuyerDtls": {
        "Gstin": "37BZNPM9430M1kl",
        "LglNm": "XYZ company pvt ltd",
        "Pos": "37",
        "Addr1": "7th block, kuvempu layout",
        "Loc": "GANDHINAGAR",
        "State": "KARNATAKA"
      },
      "ItemList": [
        {
          "SlNo": "1",
          "PrdDesc": "Prod Desc",
          "IsServc": "N",
          "HsnCd": "1001",
          "Qty": "10",
          "Unit": "BAG",
          "UnitPrice": 10,
          "TotAmt": 151,
          "Discount": 0,
          "AssAmt": 151,
          "GstRt": 10,
          "IgstAmt": 10,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 15,
          "CesAmt": 123.89,
          "CesNonAdvlAmt": 0,
          "StateCesRt": 36,
          "StateCesAmt": 151,
          "StateCesNonAdvlAmt": 0,
          "OthChrg": 0,
          "TotItemVal": 100
        },
        {
          "SlNo": "2",
          "PrdDesc": "Prod Desc",
          "IsServc": "N",
          "HsnCd": "1001",
          "Qty": "10",
          "Unit": "BAG",
          "UnitPrice": 10,
          "TotAmt": 151,
          "Discount": 0,
          "AssAmt": 151,
          "GstRt": 10,
          "IgstAmt": 10,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 15,
          "CesAmt": 123.89,
          "CesNonAdvlAmt": 0,
          "StateCesRt": 36,
          "StateCesAmt": 151,
          "StateCesNonAdvlAmt": 0,
          "OthChrg": 0,
          "TotItemVal": 100
        }
      ],
      "ValDtls": {
        "AssVal": 100,
        "CgstVal": 0,
        "SgstVal": 0,
        "IgstVal": 0,
        "CesVal": 15,
        "StCesVal": 36,
        "RndOffAmt": 0,
        "TotInvVal": 100
      }
    },
    "document_status": "IRN_CANCELLED",
    "govt_response": {
      "Success": "Y",
      "AckNo": 19100216521,
      "AckDt": "2020-03-13 15:54:00",
      "Irn": "9a3d2e1d74e4db5e007862e85028fb047e6ff6aba2415cfb45c049a4564e80d8",
      "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxOTEwMDIxNjUyMSxcIkFja0R0XCI6XCIyMDIwLTAzLTEzIDE1OjU0OjAwXCIsXCJJcm5cIjpcIjlhM2QyZTFkNzRlNGRiNWUwMDc4NjJlODUwMjhmYjA0N2U2ZmY2YWJhMjQxNWNmYjQ1YzA0OWE0NTY0ZTgwZDhcIixcIlZlcnNpb25cIjpcIjEuMDFcIixcIlRyYW5EdGxzXCI6e1wiVGF4U2NoXCI6XCJHU1RcIixcIlN1cFR5cFwiOlwiQjJCXCIsXCJSZWdSZXZcIjpcIk5cIn0sXCJEb2NEdGxzXCI6e1wiVHlwXCI6XCJJTlZcIixcIk5vXCI6XCJJTlYtOTcwXCIsXCJEdFwiOlwiMTIvMDMvMjAyMFwifSxcIlNlbGxlckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBQUZDRDU4NjJSMDAwXCIsXCJMZ2xObVwiOlwiQUJDIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiQWRkcjFcIjpcIjV0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIyXCI6XCJRdkJRWXV4aVhYVnl0R0N4elZsbHBnVEpLaFJRcVwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiUGluXCI6XCI1NjAwMDJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiUG9zXCI6XCIzN1wiLFwiQWRkcjFcIjpcIjd0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfSx7XCJJdGVtTm9cIjoyLFwiU2xOb1wiOlwiMlwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfV0sXCJWYWxEdGxzXCI6e1wiQXNzVmFsXCI6MTAwLjAsXCJDZ3N0VmFsXCI6MC4wLFwiU2dzdFZhbFwiOjAuMCxcIklnc3RWYWxcIjowLjAsXCJDZXNWYWxcIjoxNS4wLFwiU3RDZXNWYWxcIjozNi4wLFwiUm5kT2ZmQW10XCI6MC4wLFwiVG90SW52VmFsXCI6MTAwLjB9fSIsImlzcyI6Ik5JQyJ9.Irvso5SlsDy7K9LawcN9upVcPuDp-9VLzWmKpzpxvqlv_qbDfjV0NsBpKznduEEnmKMWTl16Mb4AVBOKi3-krdvVpKSGiNPoQBbc3Buo42puWOgsYGi75gx9Kx3Z34ZLRCBCxWv7MdU0TALZJZYcX63orY1FrqSj9PuUhxo0DafMdNavMik2TQ8BDxDgizqY7SNdlf9Mlr6w3FbZ8tl4J9sgJho0wUpCSslrUhkhFu8BJJXrmfLRlFBExLFMngiVK6Gb5h8UVyZ4kTNjtMS0WPM4T8T3SUcrWDyQli9SBo_E7TO4hiVNeHlr4FdOVAtWL2LD3_D0QwnTELgYFDWkEA",
      "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJEb2NOb1wiOlwiSU5WLTk3MFwiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIxMi8wMy8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMDAuMCxcIkl0ZW1DbnRcIjoyLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiOWEzZDJlMWQ3NGU0ZGI1ZTAwNzg2MmU4NTAyOGZiMDQ3ZTZmZjZhYmEyNDE1Y2ZiNDVjMDQ5YTQ1NjRlODBkOFwifSIsImlzcyI6Ik5JQyJ9.l1mnY1U-3FaPHngamuAkxdKY94B8h9zOotv7rY4i5yNtcmWb5SasE3vugG85WdqrOZV09Vg9QVXI59k0RiI62-7lgTs3VD8ZSiZxbruZkZIhfx65EUPADCEA25GiPDzTfRnKBeb8SF3UgGx2CKxS3defonN2nna529aagf3JM80T9OzdTpAqOw-3DdDgMEUVabvUWZXfTZYuGGSHeCeDu294a8APiW7CQ7EWQrA6EuBmSKFEWLWOzMZbPLEfucNFes9We9tGIKb4D0TtgDDcpSl07ZehBrLoV4V8pOerFlTcWSLciN1T7YJ0B9F4ScSjiCKQKgfLU5rh4u5e3gvJjQ",
      "Status": "CNL",
      "CancelDate": "2020-03-13 16:16:00"
    }
  }
]
```
{% endtab %}

{% tab title="XML Response - Success" %}
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <eInvoiceTransactionDTOes>
    <invoice_details>
      <owner_id>87gh1c92-cf28-4174-aacc-245fda688b17</owner_id>
      <gstin>29AAFCD5862R000</gstin>
      <group_id>26dc290f-34ad-40f8-94fe-8e7d9f6cd445</group_id>
      <transaction_id>1aed8616-b360-475b-9080-4f5774a1ba2e</transaction_id>
      <transaction>
        <Version>1.01</Version>
        <Irn>dc0bf021c9d1180a82443bd29a63abb6935aa15db8c1f399813f68ceb5043dc6</Irn>
        <TranDtls>
          <TaxSch>GST</TaxSch>
          <RegRev>N</RegRev>
          <SupTyp>B2B</SupTyp>
        </TranDtls>
        <DocDtls>
          <Typ>INV</Typ>
          <No>O92</No>
          <Dt>12/03/2020</Dt>
        </DocDtls>
        <SellerDtls>
          <Gstin>29AAFCD5862R000</Gstin>
          <LglNm>ABC company pvt ltd</LglNm>
          <Addr1>5th block, kuvempu layout</Addr1>
          <Addr2>QvBQYuxiXXVytGCxzVllpgTJKhRQq</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>560002</Pin>
          <State>KARNATAKA</State>
        </SellerDtls>
        <BuyerDtls>
          <Gstin>37BZNPM9430M1kl</Gstin>
          <LglNm>XYZ company pvt ltd</LglNm>
          <Pos>37</Pos>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Loc>GANDHINAGAR</Loc>
          <State>KARNATAKA</State>
        </BuyerDtls>
        <ItemList>
          <SlNo>1</SlNo>
          <PrdDesc>Prod Desc</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Qty>10</Qty>
          <Unit>BAG</Unit>
          <UnitPrice>10.0</UnitPrice>
          <TotAmt>151.0</TotAmt>
          <Discount>0.0</Discount>
          <AssAmt>151.0</AssAmt>
          <GstRt>10.000</GstRt>
          <IgstAmt>10.0</IgstAmt>
          <CgstAmt>0.0</CgstAmt>
          <SgstAmt>0.0</SgstAmt>
          <CesRt>15.000</CesRt>
          <CesAmt>123.89</CesAmt>
          <CesNonAdvlAmt>0.0</CesNonAdvlAmt>
          <StateCesRt>36.000</StateCesRt>
          <StateCesAmt>151.0</StateCesAmt>
          <StateCesNonAdvlAmt>0.0</StateCesNonAdvlAmt>
          <OthChrg>0.0</OthChrg>
          <TotItemVal>100.0</TotItemVal>
        </ItemList>
        <ItemList>
          <SlNo>2</SlNo>
          <PrdDesc>Prod Desc</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Qty>10</Qty>
          <Unit>BAG</Unit>
          <UnitPrice>10.0</UnitPrice>
          <TotAmt>151.0</TotAmt>
          <Discount>0.0</Discount>
          <AssAmt>151.0</AssAmt>
          <GstRt>10.000</GstRt>
          <IgstAmt>10.0</IgstAmt>
          <CgstAmt>0.0</CgstAmt>
          <SgstAmt>0.0</SgstAmt>
          <CesRt>15.000</CesRt>
          <CesAmt>123.89</CesAmt>
          <CesNonAdvlAmt>0.0</CesNonAdvlAmt>
          <StateCesRt>36.000</StateCesRt>
          <StateCesAmt>151.0</StateCesAmt>
          <StateCesNonAdvlAmt>0.0</StateCesNonAdvlAmt>
          <OthChrg>0.0</OthChrg>
          <TotItemVal>100.0</TotItemVal>
        </ItemList>
        <ValDtls>
          <AssVal>100.0</AssVal>
          <CgstVal>0.0</CgstVal>
          <SgstVal>0.0</SgstVal>
          <IgstVal>0.0</IgstVal>
          <CesVal>15.0</CesVal>
          <StCesVal>36.0</StCesVal>
          <RndOffAmt>0.0</RndOffAmt>
          <TotInvVal>100.0</TotInvVal>
        </ValDtls>
      </transaction>
      <document_status>IRN_CANCELLED</document_status>
      <govt_response>
        <Success>Y</Success>
        <AckNo>18100215808</AckNo>
        <AckDt>2020-03-13 14:04:00</AckDt>
        <Irn>dc0bf021c9d1180a82443bd29a63abb6935aa15db8c1f399813f68ceb5043dc6</Irn>
        <SignedInvoice>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxODEwMDIxNTgwOCxcIkFja0R0XCI6XCIyMDIwLTAzLTEzIDE0OjA0OjAwXCIsXCJJcm5cIjpcImRjMGJmMDIxYzlkMTE4MGE4MjQ0M2JkMjlhNjNhYmI2OTM1YWExNWRiOGMxZjM5OTgxM2Y2OGNlYjUwNDNkYzZcIixcIlZlcnNpb25cIjpcIjEuMDFcIixcIlRyYW5EdGxzXCI6e1wiVGF4U2NoXCI6XCJHU1RcIixcIlN1cFR5cFwiOlwiQjJCXCIsXCJSZWdSZXZcIjpcIk5cIn0sXCJEb2NEdGxzXCI6e1wiVHlwXCI6XCJJTlZcIixcIk5vXCI6XCJPOTJcIixcIkR0XCI6XCIxMi8wMy8yMDIwXCJ9LFwiU2VsbGVyRHRsc1wiOntcIkdzdGluXCI6XCIyOUFBRkNENTg2MlIwMDBcIixcIkxnbE5tXCI6XCJBQkMgY29tcGFueSBwdnQgbHRkXCIsXCJBZGRyMVwiOlwiNXRoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiQWRkcjJcIjpcIlF2QlFZdXhpWFhWeXRHQ3h6VmxscGdUSktoUlFxXCIsXCJMb2NcIjpcIkdBTkRISU5BR0FSXCIsXCJQaW5cIjpcIjU2MDAwMlwiLFwiU3RhdGVcIjpcIktBUk5BVEFLQVwifSxcIkJ1eWVyRHRsc1wiOntcIkdzdGluXCI6XCIzN0JaTlBNOTQzME0xa2xcIixcIkxnbE5tXCI6XCJYWVogY29tcGFueSBwdnQgbHRkXCIsXCJQb3NcIjpcIjM3XCIsXCJBZGRyMVwiOlwiN3RoIGJsb2NrLCBrdXZlbXB1IGxheW91dFwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiU3RhdGVcIjpcIktBUk5BVEFLQVwifSxcIkl0ZW1MaXN0XCI6W3tcIkl0ZW1Ob1wiOjEsXCJTbE5vXCI6XCIxXCIsXCJJc1NlcnZjXCI6XCJOXCIsXCJQcmREZXNjXCI6XCJQcm9kIERlc2NcIixcIkhzbkNkXCI6XCIxMDAxXCIsXCJRdHlcIjpcIjEwXCIsXCJVbml0XCI6XCJCQUdcIixcIlVuaXRQcmljZVwiOjEwLjAsXCJUb3RBbXRcIjoxNTEuMCxcIkRpc2NvdW50XCI6MC4wLFwiQXNzQW10XCI6MTUxLjAsXCJHc3RSdFwiOjEwLjAwMCxcIklnc3RBbXRcIjoxMC4wLFwiQ2dzdEFtdFwiOjAuMCxcIlNnc3RBbXRcIjowLjAsXCJDZXNSdFwiOjE1LjAwMCxcIkNlc0FtdFwiOjEyMy44OSxcIkNlc05vbkFkdmxBbXRcIjowLjAsXCJTdGF0ZUNlc1J0XCI6MzYuMDAwLFwiU3RhdGVDZXNBbXRcIjoxNTEuMCxcIlN0YXRlQ2VzTm9uQWR2bEFtdFwiOjAuMCxcIk90aENocmdcIjowLjAsXCJUb3RJdGVtVmFsXCI6MTAwLjB9LHtcIkl0ZW1Ob1wiOjIsXCJTbE5vXCI6XCIyXCIsXCJJc1NlcnZjXCI6XCJOXCIsXCJQcmREZXNjXCI6XCJQcm9kIERlc2NcIixcIkhzbkNkXCI6XCIxMDAxXCIsXCJRdHlcIjpcIjEwXCIsXCJVbml0XCI6XCJCQUdcIixcIlVuaXRQcmljZVwiOjEwLjAsXCJUb3RBbXRcIjoxNTEuMCxcIkRpc2NvdW50XCI6MC4wLFwiQXNzQW10XCI6MTUxLjAsXCJHc3RSdFwiOjEwLjAwMCxcIklnc3RBbXRcIjoxMC4wLFwiQ2dzdEFtdFwiOjAuMCxcIlNnc3RBbXRcIjowLjAsXCJDZXNSdFwiOjE1LjAwMCxcIkNlc0FtdFwiOjEyMy44OSxcIkNlc05vbkFkdmxBbXRcIjowLjAsXCJTdGF0ZUNlc1J0XCI6MzYuMDAwLFwiU3RhdGVDZXNBbXRcIjoxNTEuMCxcIlN0YXRlQ2VzTm9uQWR2bEFtdFwiOjAuMCxcIk90aENocmdcIjowLjAsXCJUb3RJdGVtVmFsXCI6MTAwLjB9XSxcIlZhbER0bHNcIjp7XCJBc3NWYWxcIjoxMDAuMCxcIkNnc3RWYWxcIjowLjAsXCJTZ3N0VmFsXCI6MC4wLFwiSWdzdFZhbFwiOjAuMCxcIkNlc1ZhbFwiOjE1LjAsXCJTdENlc1ZhbFwiOjM2LjAsXCJSbmRPZmZBbXRcIjowLjAsXCJUb3RJbnZWYWxcIjoxMDAuMH19IiwiaXNzIjoiTklDIn0.SLYa8N5jH6FYcx6ZAK94lhV3k-kfL1Z0mJHRMnDPljpySGMORAg-oj43b9-P1Yvrpa4mhzvREgeb56nJ2GFyyr5jpYoga9sTgSQA0l-XuosOQjYTqI2LV77OIRJteefBvZ81opnrMyv58F2noojnSsS6kqcoVXb_-BZEqbjSdKfC-i2x3EkeR045UMz-U8qURFm0lB0YwFKNvOQgT31RRJKPw4zGNjzVG1qJVKKQXzZs0xEbZRxzyuUkMmRPPnO7LvZvWY1lv1qMwAbu4Id7YwyHJx5AlU0Fqtx0O45O7HXk8WWQIt7O7StLTUfsclkq5xX4NTvp3w3PVW4b6yuw_w</SignedInvoice>
        <SignedQRCode>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJEb2NOb1wiOlwiTzkyXCIsXCJEb2NUeXBcIjpcIklOVlwiLFwiRG9jRHRcIjpcIjEyLzAzLzIwMjBcIixcIlRvdEludlZhbFwiOjEwMC4wLFwiSXRlbUNudFwiOjIsXCJNYWluSHNuQ29kZVwiOlwiMTAwMVwiLFwiSXJuXCI6XCJkYzBiZjAyMWM5ZDExODBhODI0NDNiZDI5YTYzYWJiNjkzNWFhMTVkYjhjMWYzOTk4MTNmNjhjZWI1MDQzZGM2XCJ9IiwiaXNzIjoiTklDIn0.ZSx4-bB0k98asz1lAilKh5pcm0_oHMnB84KlyjTymkje14UMYs8c2lB9M4CEtK7RIn21QYLCOIkcVcnZJdFYffmmaXEEFWXhgNb9M7M8-LEtr360PKPWZcTtliwQGHRsJDD48aARrdCoru9560r1MaTgVHSRgZhNk-GbBrCobUgXYltRQybW3UmZxduDr5EOUcUlUb0s-ooR56YBcZMvES03RtF9U2CPvfQo9GJdV7AoAt-52rF89hjZ6JsK-8BojkXazWhEhYQ5haFJwgDGH1rZT_6SxZ5ROyLJBz9HedVkBxngB1BC9jPlPLOysMQ0J451ouSUC-a47bxq7v6y5w</SignedQRCode>
        <Status>CNL</Status>
      </govt_response>
    </invoice_details>
  </eInvoiceTransactionDTOes>
```
{% endtab %}
{% endtabs %}

## Getting E-Invoice by IRN

You can get details of an invoice by sending a **`GET`** request to E-Invoicing API with the following request headers.

**Request URL**

```
GET {{HOST}}/v2/eInvoice/get?irn={{IRN_number}}
```

#### Request Headers

{% tabs %}
{% tab title="Headers" %}
```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
gstin:{{gstin_number}}
owner_id:{{owner_id}}
```
{% endtab %}
{% endtabs %}

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| gstin | Header | String | Mandatory. GSTIN number for the user |
| owner\_id | Header | String | Mandatory. Owner\_id of the user |

#### Query Param

You can pass a list of IRNs to get the invoice details.

| Key | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| irn | Query | String | Mandatory. IRN number. Multiple allowed |

#### Sample Response

{% tabs %}
{% tab title="JSON Response - Success" %}
```text
[
  {
    "owner_id": "87gh1c92-cf28-4174-aacc-245fda688b17",
    "gstin": "29AAFCD5862R000",
    "group_id": "2d662240-7d6e-427b-8799-a63987200c2f",
    "transaction_id": "29AAFCD5862R000_B672_INV_2019",
    "transaction": {
      "Version": "1.01",
      "Irn": "f127d018933f1a4bcb0bbf37fca57db5fac28b10f48292490d3ff8ff76cc0812",
      "TranDtls": {
        "TaxSch": "GST",
        "RegRev": "N",
        "SupTyp": "B2B"
      },
      "DocDtls": {
        "Typ": "INV",
        "No": "B672",
        "Dt": "12/03/2020"
      },
      "SellerDtls": {
        "Gstin": "29AAFCD5862R000",
        "LglNm": "ABC company pvt ltd",
        "Addr1": "5th block, kuvempu layout",
        "Addr2": "QvBQYuxiXXVytGCxzVllpgTJKhRQq",
        "Loc": "GANDHINAGAR",
        "Pin": "560002",
        "State": "KARNATAKA"
      },
      "BuyerDtls": {
        "Gstin": "37BZNPM9430M1kl",
        "LglNm": "XYZ company pvt ltd",
        "Pos": "37",
        "Addr1": "7th block, kuvempu layout",
        "Loc": "GANDHINAGAR",
        "State": "KARNATAKA"
      },
      "ItemList": [
        {
          "SlNo": "1",
          "PrdDesc": "Prod Desc",
          "IsServc": "N",
          "HsnCd": "1001",
          "Qty": "10",
          "Unit": "BAG",
          "UnitPrice": 10,
          "TotAmt": 151,
          "Discount": 0,
          "AssAmt": 151,
          "GstRt": 10,
          "IgstAmt": 10,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 15,
          "CesAmt": 123.89,
          "CesNonAdvlAmt": 0,
          "StateCesRt": 36,
          "StateCesAmt": 151,
          "StateCesNonAdvlAmt": 0,
          "OthChrg": 0,
          "TotItemVal": 100
        },
        {
          "SlNo": "2",
          "PrdDesc": "Prod Desc",
          "IsServc": "N",
          "HsnCd": "1001",
          "Qty": "10",
          "Unit": "BAG",
          "UnitPrice": 10,
          "TotAmt": 151,
          "Discount": 0,
          "AssAmt": 151,
          "GstRt": 10,
          "IgstAmt": 10,
          "CgstAmt": 0,
          "SgstAmt": 0,
          "CesRt": 15,
          "CesAmt": 123.89,
          "CesNonAdvlAmt": 0,
          "StateCesRt": 36,
          "StateCesAmt": 151,
          "StateCesNonAdvlAmt": 0,
          "OthChrg": 0,
          "TotItemVal": 100
        }
      ],
      "ValDtls": {
        "AssVal": 100,
        "CgstVal": 0,
        "SgstVal": 0,
        "IgstVal": 0,
        "CesVal": 15,
        "StCesVal": 36,
        "RndOffAmt": 0,
        "TotInvVal": 100
      }
    },
    "document_status": "IRN_GENERATED",
    "govt_response": {
      "Success": "Y",
      "AckNo": 19100216248,
      "AckDt": "2020-03-13 15:25:00",
      "Irn": "f127d018933f1a4bcb0bbf37fca57db5fac28b10f48292490d3ff8ff76cc0812",
      "SignedInvoice": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxOTEwMDIxNjI0OCxcIkFja0R0XCI6XCIyMDIwLTAzLTEzIDE1OjI1OjAwXCIsXCJJcm5cIjpcImYxMjdkMDE4OTMzZjFhNGJjYjBiYmYzN2ZjYTU3ZGI1ZmFjMjhiMTBmNDgyOTI0OTBkM2ZmOGZmNzZjYzA4MTJcIixcIlZlcnNpb25cIjpcIjEuMDFcIixcIlRyYW5EdGxzXCI6e1wiVGF4U2NoXCI6XCJHU1RcIixcIlN1cFR5cFwiOlwiQjJCXCIsXCJSZWdSZXZcIjpcIk5cIn0sXCJEb2NEdGxzXCI6e1wiVHlwXCI6XCJJTlZcIixcIk5vXCI6XCJCNjcyXCIsXCJEdFwiOlwiMTIvMDMvMjAyMFwifSxcIlNlbGxlckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBQUZDRDU4NjJSMDAwXCIsXCJMZ2xObVwiOlwiQUJDIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiQWRkcjFcIjpcIjV0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIyXCI6XCJRdkJRWXV4aVhYVnl0R0N4elZsbHBnVEpLaFJRcVwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiUGluXCI6XCI1NjAwMDJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiUG9zXCI6XCIzN1wiLFwiQWRkcjFcIjpcIjd0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfSx7XCJJdGVtTm9cIjoyLFwiU2xOb1wiOlwiMlwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfV0sXCJWYWxEdGxzXCI6e1wiQXNzVmFsXCI6MTAwLjAsXCJDZ3N0VmFsXCI6MC4wLFwiU2dzdFZhbFwiOjAuMCxcIklnc3RWYWxcIjowLjAsXCJDZXNWYWxcIjoxNS4wLFwiU3RDZXNWYWxcIjozNi4wLFwiUm5kT2ZmQW10XCI6MC4wLFwiVG90SW52VmFsXCI6MTAwLjB9fSIsImlzcyI6Ik5JQyJ9.Anff6z--diEGBlvPAeeM6kAeJ3TpgWaFpfGuk6aUsrazOLEZUkrK0Gfs0PVu0x6_K_S2ZDczIy1n7JFF6iHWYpjcdtPA0W3ZPMx7slIXT31DVppHB21OerOSJc4ERcEjdG5joT3INsKRhJgnjo3bAZgKzsBAEGwMtjtE3HhT0PM3voiK19Op1t7_fCjChi46BVlDuuqNhj7mGiyTI573NUZq4mpOlBKZcNRit-pY2kjSy8De13m3-CDuTjjnZjftT5eVDaNQiSTIY9eAXrXGha6BGl_fOudz9W1B1d9Db2BvWhkf7fOnWLwkwuuS9L0MDtPHrkmxIrfsj8-puez_TQ",
      "SignedQRCode": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJEb2NOb1wiOlwiQjY3MlwiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIxMi8wMy8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMDAuMCxcIkl0ZW1DbnRcIjoyLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiZjEyN2QwMTg5MzNmMWE0YmNiMGJiZjM3ZmNhNTdkYjVmYWMyOGIxMGY0ODI5MjQ5MGQzZmY4ZmY3NmNjMDgxMlwifSIsImlzcyI6Ik5JQyJ9.af9u7pt-UBUQ1ASGDz7efx21axwmmGtAiNPJGlWMmMV-F7ygPv-HFu-E85-fpx_yvLpz7sJfsfSfbCpXGqraaJJ65H8T9LrNxoMk1knHMCmZN6gLS9mUW-oz8j7LbmAJcNE_E67vHsZFHfwWoUOA-I6vyKHHa-g_XFST08nuAXv0qbkFoXFU8lS06qnLhraTAxqCTjOF1owMj8iAXMXKSJT5iLXaHJVdE4p-VwCeXoA11WxeUbqQ7v-sbMbN84XVnDQ4K2yxEyT9YWMycBUX7jkBix2uj9enFSHSC8wEli1r-OYpZMbpg-8guFsY5SKx_hGka5kzpKesC7rWwCNVkg",
      "Status": "ACT"
      "EwbNo": 681008686014,
      "EwbDt": "2020-08-08 11:23:00",
      "EwbValidTill": "2020-08-09 23:59:00"
    }
  }
]
```
{% endtab %}

{% tab title="XML Response - Success" %}
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <eInvoiceTransactionDTOes>
    <invoice_details>
      <owner_id>87gh1c92-cf28-4174-aacc-245fda688b17</owner_id>
      <gstin>29AAFCD5862R000</gstin>
      <group_id>637f4056-87d8-45c6-9dcb-bc3df100e365</group_id>
      <transaction_id>29AAFCD5862R000_B672_INV_2019</transaction_id>
      <transaction>
        <Version>1.01</Version>
        <Irn>f127d018933f1a4bcb0bbf37fca57db5fac28b10f48292490d3ff8ff76cc0812</Irn>
        <TranDtls>
          <TaxSch>GST</TaxSch>
          <RegRev>N</RegRev>
          <SupTyp>B2B</SupTyp>
        </TranDtls>
        <DocDtls>
          <Typ>INV</Typ>
          <No>B672</No>
          <Dt>12/03/2020</Dt>
        </DocDtls>
        <SellerDtls>
          <Gstin>29AAFCD5862R000</Gstin>
          <LglNm>ABC company pvt ltd</LglNm>
          <Addr1>5th block, kuvempu layout</Addr1>
          <Addr2>QvBQYuxiXXVytGCxzVllpgTJKhRQq</Addr2>
          <Loc>GANDHINAGAR</Loc>
          <Pin>560002</Pin>
          <State>KARNATAKA</State>
        </SellerDtls>
        <BuyerDtls>
          <Gstin>37BZNPM9430M1kl</Gstin>
          <LglNm>XYZ company pvt ltd</LglNm>
          <Pos>37</Pos>
          <Addr1>7th block, kuvempu layout</Addr1>
          <Loc>GANDHINAGAR</Loc>
          <State>KARNATAKA</State>
        </BuyerDtls>
        <ItemList>
          <SlNo>1</SlNo>
          <PrdDesc>Prod Desc</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Qty>10</Qty>
          <Unit>BAG</Unit>
          <UnitPrice>10.0</UnitPrice>
          <TotAmt>151.0</TotAmt>
          <Discount>0.0</Discount>
          <AssAmt>151.0</AssAmt>
          <GstRt>10.000</GstRt>
          <IgstAmt>10.0</IgstAmt>
          <CgstAmt>0.0</CgstAmt>
          <SgstAmt>0.0</SgstAmt>
          <CesRt>15.000</CesRt>
          <CesAmt>123.89</CesAmt>
          <CesNonAdvlAmt>0.0</CesNonAdvlAmt>
          <StateCesRt>36.000</StateCesRt>
          <StateCesAmt>151.0</StateCesAmt>
          <StateCesNonAdvlAmt>0.0</StateCesNonAdvlAmt>
          <OthChrg>0.0</OthChrg>
          <TotItemVal>100.0</TotItemVal>
        </ItemList>
        <ItemList>
          <SlNo>2</SlNo>
          <PrdDesc>Prod Desc</PrdDesc>
          <IsServc>N</IsServc>
          <HsnCd>1001</HsnCd>
          <Qty>10</Qty>
          <Unit>BAG</Unit>
          <UnitPrice>10.0</UnitPrice>
          <TotAmt>151.0</TotAmt>
          <Discount>0.0</Discount>
          <AssAmt>151.0</AssAmt>
          <GstRt>10.000</GstRt>
          <IgstAmt>10.0</IgstAmt>
          <CgstAmt>0.0</CgstAmt>
          <SgstAmt>0.0</SgstAmt>
          <CesRt>15.000</CesRt>
          <CesAmt>123.89</CesAmt>
          <CesNonAdvlAmt>0.0</CesNonAdvlAmt>
          <StateCesRt>36.000</StateCesRt>
          <StateCesAmt>151.0</StateCesAmt>
          <StateCesNonAdvlAmt>0.0</StateCesNonAdvlAmt>
          <OthChrg>0.0</OthChrg>
          <TotItemVal>100.0</TotItemVal>
        </ItemList>
        <ValDtls>
          <AssVal>100.0</AssVal>
          <CgstVal>0.0</CgstVal>
          <SgstVal>0.0</SgstVal>
          <IgstVal>0.0</IgstVal>
          <CesVal>15.0</CesVal>
          <StCesVal>36.0</StCesVal>
          <RndOffAmt>0.0</RndOffAmt>
          <TotInvVal>100.0</TotInvVal>
        </ValDtls>
      </transaction>
      <document_status>IRN_GENERATED</document_status>
      <govt_response>
        <Success>Y</Success>
        <AckNo>19100216248</AckNo>
        <AckDt>2020-03-13 15:25:00</AckDt>
        <Irn>f127d018933f1a4bcb0bbf37fca57db5fac28b10f48292490d3ff8ff76cc0812</Irn>
        <SignedInvoice>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiQWNrTm9cIjoxOTEwMDIxNjI0OCxcIkFja0R0XCI6XCIyMDIwLTAzLTEzIDE1OjI1OjAwXCIsXCJJcm5cIjpcImYxMjdkMDE4OTMzZjFhNGJjYjBiYmYzN2ZjYTU3ZGI1ZmFjMjhiMTBmNDgyOTI0OTBkM2ZmOGZmNzZjYzA4MTJcIixcIlZlcnNpb25cIjpcIjEuMDFcIixcIlRyYW5EdGxzXCI6e1wiVGF4U2NoXCI6XCJHU1RcIixcIlN1cFR5cFwiOlwiQjJCXCIsXCJSZWdSZXZcIjpcIk5cIn0sXCJEb2NEdGxzXCI6e1wiVHlwXCI6XCJJTlZcIixcIk5vXCI6XCJCNjcyXCIsXCJEdFwiOlwiMTIvMDMvMjAyMFwifSxcIlNlbGxlckR0bHNcIjp7XCJHc3RpblwiOlwiMjlBQUZDRDU4NjJSMDAwXCIsXCJMZ2xObVwiOlwiQUJDIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiQWRkcjFcIjpcIjV0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkFkZHIyXCI6XCJRdkJRWXV4aVhYVnl0R0N4elZsbHBnVEpLaFJRcVwiLFwiTG9jXCI6XCJHQU5ESElOQUdBUlwiLFwiUGluXCI6XCI1NjAwMDJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJCdXllckR0bHNcIjp7XCJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJMZ2xObVwiOlwiWFlaIGNvbXBhbnkgcHZ0IGx0ZFwiLFwiUG9zXCI6XCIzN1wiLFwiQWRkcjFcIjpcIjd0aCBibG9jaywga3V2ZW1wdSBsYXlvdXRcIixcIkxvY1wiOlwiR0FOREhJTkFHQVJcIixcIlN0YXRlXCI6XCJLQVJOQVRBS0FcIn0sXCJJdGVtTGlzdFwiOlt7XCJJdGVtTm9cIjoxLFwiU2xOb1wiOlwiMVwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfSx7XCJJdGVtTm9cIjoyLFwiU2xOb1wiOlwiMlwiLFwiSXNTZXJ2Y1wiOlwiTlwiLFwiUHJkRGVzY1wiOlwiUHJvZCBEZXNjXCIsXCJIc25DZFwiOlwiMTAwMVwiLFwiUXR5XCI6XCIxMFwiLFwiVW5pdFwiOlwiQkFHXCIsXCJVbml0UHJpY2VcIjoxMC4wLFwiVG90QW10XCI6MTUxLjAsXCJEaXNjb3VudFwiOjAuMCxcIkFzc0FtdFwiOjE1MS4wLFwiR3N0UnRcIjoxMC4wMDAsXCJJZ3N0QW10XCI6MTAuMCxcIkNnc3RBbXRcIjowLjAsXCJTZ3N0QW10XCI6MC4wLFwiQ2VzUnRcIjoxNS4wMDAsXCJDZXNBbXRcIjoxMjMuODksXCJDZXNOb25BZHZsQW10XCI6MC4wLFwiU3RhdGVDZXNSdFwiOjM2LjAwMCxcIlN0YXRlQ2VzQW10XCI6MTUxLjAsXCJTdGF0ZUNlc05vbkFkdmxBbXRcIjowLjAsXCJPdGhDaHJnXCI6MC4wLFwiVG90SXRlbVZhbFwiOjEwMC4wfV0sXCJWYWxEdGxzXCI6e1wiQXNzVmFsXCI6MTAwLjAsXCJDZ3N0VmFsXCI6MC4wLFwiU2dzdFZhbFwiOjAuMCxcIklnc3RWYWxcIjowLjAsXCJDZXNWYWxcIjoxNS4wLFwiU3RDZXNWYWxcIjozNi4wLFwiUm5kT2ZmQW10XCI6MC4wLFwiVG90SW52VmFsXCI6MTAwLjB9fSIsImlzcyI6Ik5JQyJ9.Anff6z--diEGBlvPAeeM6kAeJ3TpgWaFpfGuk6aUsrazOLEZUkrK0Gfs0PVu0x6_K_S2ZDczIy1n7JFF6iHWYpjcdtPA0W3ZPMx7slIXT31DVppHB21OerOSJc4ERcEjdG5joT3INsKRhJgnjo3bAZgKzsBAEGwMtjtE3HhT0PM3voiK19Op1t7_fCjChi46BVlDuuqNhj7mGiyTI573NUZq4mpOlBKZcNRit-pY2kjSy8De13m3-CDuTjjnZjftT5eVDaNQiSTIY9eAXrXGha6BGl_fOudz9W1B1d9Db2BvWhkf7fOnWLwkwuuS9L0MDtPHrkmxIrfsj8-puez_TQ</SignedInvoice>
        <SignedQRCode>eyJhbGciOiJSUzI1NiIsImtpZCI6IjExNUY0NDI2NjE3QTc5MzhCRTFCQTA2REJFRTkxQTQyNzU4NEVEQUIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJFVjlFSm1GNmVUaS1HNkJ0dnVrYVFuV0U3YXMifQ.eyJkYXRhIjoie1wiU2VsbGVyR3N0aW5cIjpcIjI5QUFGQ0Q1ODYyUjAwMFwiLFwiQnV5ZXJHc3RpblwiOlwiMzdCWk5QTTk0MzBNMWtsXCIsXCJEb2NOb1wiOlwiQjY3MlwiLFwiRG9jVHlwXCI6XCJJTlZcIixcIkRvY0R0XCI6XCIxMi8wMy8yMDIwXCIsXCJUb3RJbnZWYWxcIjoxMDAuMCxcIkl0ZW1DbnRcIjoyLFwiTWFpbkhzbkNvZGVcIjpcIjEwMDFcIixcIklyblwiOlwiZjEyN2QwMTg5MzNmMWE0YmNiMGJiZjM3ZmNhNTdkYjVmYWMyOGIxMGY0ODI5MjQ5MGQzZmY4ZmY3NmNjMDgxMlwifSIsImlzcyI6Ik5JQyJ9.af9u7pt-UBUQ1ASGDz7efx21axwmmGtAiNPJGlWMmMV-F7ygPv-HFu-E85-fpx_yvLpz7sJfsfSfbCpXGqraaJJ65H8T9LrNxoMk1knHMCmZN6gLS9mUW-oz8j7LbmAJcNE_E67vHsZFHfwWoUOA-I6vyKHHa-g_XFST08nuAXv0qbkFoXFU8lS06qnLhraTAxqCTjOF1owMj8iAXMXKSJT5iLXaHJVdE4p-VwCeXoA11WxeUbqQ7v-sbMbN84XVnDQ4K2yxEyT9YWMycBUX7jkBix2uj9enFSHSC8wEli1r-OYpZMbpg-8guFsY5SKx_hGka5kzpKesC7rWwCNVkg</SignedQRCode>
        <Status>ACT</Status>
        <EwbNo>681008686014</EwbNo>
        <EwbDt>2020-08-08 11:23:00</EwbDt>
        <EwbValidTill>2020-08-09 23:59:00</EwbValidTill>
      </govt_response>
    </invoice_details>
  </eInvoiceTransactionDTOes>
```
{% endtab %}
{% endtabs %}

## Generate E-Waybill by IRN

You can use this API to generate the e-waybill using Invoice Registration Number \(IRN\).

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | Users GSTIN |

**Request URL**

```text
POST: {{HOST}}/v2/eInvoice/ewaybill
```

#### Sample Request Body

```text
 [
 {
  "Irn": "a5c12dca80e743321740b001fd70953e8738d109865d28ba4013750f2046f229",
  "Distance": 100,
  "TransMode": "1",
  "TransId":"12AWGPV7107B1Z1",  
  "TransName": "trans name",
  "TrnDocDt": "01/08/2020",
  "TrnDocNo": "TRAN/DOC/11",
  "VehNo": "KA01AB1234",
  "VehType": "R"
}
]
```

#### Sample Response

{% tabs %}
{% tab title="Valid Response" %}
```text
 {
  "Irn": "a5c12dca80e743321740b001fd70953e8738d109865d28ba4013750f2046f229",
  "Distance": 100,
  "TransMode": "1",
  "TransId":"12AWGPV7107B1Z1",  
  "TransName": "trans name",
  "TrnDocDt": "01/08/2020",
  "TrnDocNo": "TRAN/DOC/11",
  "VehNo": "KA01AB1234",
  "VehType": "R"
  "EwbNo":"16510609282",
  "EwbDt":"2020-04-24 11:28:00",
  "EwbValidTill":"2020-04-26 23:59:00"
  "EwbStatus": "GENERATED",
}
```
{% endtab %}

{% tab title="Invalid Response" %}
```
Coming soon
```
{% endtab %}
{% endtabs %}

## Cancel E-Waybill

{% hint style="danger" %}
E-way bill can be cancelled by the generator of the e-way bill only.

E-way bill can be cancelled within 24 hours of generation of e-way bill
{% endhint %}

You can use this API to cancel the generated e-waybill.

```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
owner_id: Owner ID
gstin: GSTIN
```

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| owner\_id | Header | String | Mandatory. This is the user scoped Unique ID of the owner \(PAN, GSTIN, Branch\) of the transaction. In sandbox environment, you can use any UUID. For production environment, this will correspond to the resource in your ClearTax user account. |
| gstin | Header | String | Users GSTIN |

**Request URL**

```text
POST: {{HOST}}/v2/eInvoice/ewaybill/cancel
```

#### Sample Request Body

```text
{  
"ewbNo": 111000609282,
"cancelRsnCode": 2,
"cancelRmrk": "Cancelled the order"
}
```

#### Sample Response

{% tabs %}
{% tab title="Valid Response" %}
```text
{   
"ewayBillNo": 16510609282,
"cancelDate": "15/07/202011:35:00 AM"
}
```
{% endtab %}

{% tab title="Invalid Response" %}
```
Coming soon
```
{% endtab %}
{% endtabs %}

## Printing E-Invoice

You can get PDF version of an Invoice by submitting a `GET`request to  E-Invoicing API with the following request headers.

**Request URL**

```
GET {{HOST}}/v2/eInvoice/download
```

#### Request Headers

{% tabs %}
{% tab title="Headers" %}
```text
X-Cleartax-Auth-Token: {{USER_AUTH_TOKEN}}
gstin:{{gstin_number}}
owner_id:{{owner_id}}
```
{% endtab %}
{% endtabs %}

| Parameter | Parameter Type | Type | Description |
| :--- | :--- | :--- | :--- |
| X-Cleartax-Auth-Token | Header | String | Mandatory. The auth token generated from ClearTax user id and password. **For testing/sandbox environment this parameter is not required**. |
| gstin | Header | String | GSTIN number for the user |
| owner\_id | Header | String | Owner\_id of the user |

#### Query Param

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">template</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Optional.Accepted values include: TEMPLATE1, TEMPLATE2, TEMPLATE3, TEMPLATE4</p>
        <p>Default: TEMPLATE1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Optional.Accepted values include: PDF, ZIP</p>
        <p>Default: PDF</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">printFor</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Optional.Accepted values include: CUSTOMER, SUPPLIER, TRANSPORTER, CONSIGNOR</p>
        <p>Default: CUSTOMER</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">supplyOf</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Optional.Accepted values include: GOODS, SERVICES</p>
        <p>Default: GOODS</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">irns</td>
      <td style="text-align:left">List</td>
      <td style="text-align:left">Required. List of IRNs generated. Multiple accepted</td>
    </tr>
    <tr>
      <td style="text-align:left">transaction_ids</td>
      <td style="text-align:left">List</td>
      <td style="text-align:left">Optional. List of transaction ids.</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
The `content-type` of the response will be  `application/pdf`.
{% endhint %}

{% file src="../../../.gitbook/assets/response \(1\).pdf" caption="Sample response" %}

