# Easy-Link V2 Reference - Fields

#### Table Of Contents

> [Overview](#overview)
>
> [Header Fields](#header-fields)
> > [Record Fields](#record-fields)<br/>
> > [General Fields](#general-fields)<br/>
> > [Contact Fields](#contact-fields)<br/>
> > [Freight Fields](#freight-fields)<br/>
> > [Ship To Fields](#ship-to-fields)<br/>
> > [Ship From Fields](#ship-from-fields)<br/>
> > [Customer Fields](#customer-fields)<br/>
> > [GET Only Fields](#get-only-fields)<br/>
>
> [Line Item Fields](#line-item-fields)
> > [Record Fields](#record-fields-line)<br/>
> > [General Fields](#general-fields-line)<br/>
> > [Product Number Fields](#product-number-fields-line)<br/>

## Overview

To ensure ease of use for all our integrating customers, we have created a set of generic fields with a consistent and intuitive naming structure, to collect your data. To simplify the process of both sending and receiving the payload, we have opted to use the same payload for both Inbound and Outbound requests. 

The available fields are listed below in the given tables. They are separated into related groups in order to make their meaning and relationship more apparent. Items that aren't entirely self apparent are given descriptions in subsequent text. If you have any issues understanding what data you might need to map into a specific field, please don't hesitate to ask your Rinchem contact.

The ***Format*** column shows the data type that will be accepted by the API.

> **Text(X)** signifies that any ascii character string with *X* characters or less will be accepted.
>
> **Integer(X)** signifies that any whole numerical value with *X* digits or less will be accepted.
>
> **Date** signifies that any date in the format of '**yyyy-mm-dd**' will be accepted.
>
> **Boolean** signifies that either 'true' or 'false' should be provided.
>
> **Picklist** signifies that this is not a free-form field and certain Rinchem approved values must be provided. Look to the description text to find more information about the acceptable values.

The ***Inbound*** and ***Outbound*** columns show the availability of the field for the desired request type. 
> '**+**' signifies that the field is available for use, but not required. 
>
> '**\***' signifies that the field is both available and required. 
>
> '**x**' signifies that the field is not available and will be ignored by the API.
>
> ---
> 
> '**w**' signifies that the field gets passed through to our Warehouse Management System (WMS). On *GET* requests, these fields will have an additional field returned with the value currently in our WMS system. These additional fields will be distinguished by the prefix **WMS_** followed by the standard field name.  

## Header Fields

### Record Fields

| Inbound | Outbound | Disposition | Field Name          | Format    | Example   |
| ------- | -------- | ----------- | ------------------- | --------- | --------- |
| + w     | + w      | +           | Record_Name         | Text(25)  | IMP000015 |
| +       | +        | +           | Record_ExternalName | Text(120) | 1234EXA   |

The **Record_Name** is a Salesforce generated value that will be returned upon successful order creation. It may be stored and used to reference the order for any *patch* or *get* requests, however, **should not be included in any *POST* requests**.

The **Record_ExternalName** on the other hand is a user created unique id/name. It may be passed in on *POST* requests, and may be used to reference the order for any *PATCH* or *GET* requests. The *Record_ExternalName* must be unique amongst all orders amongst all Chem-Star users. If a *post* request is sent with a non-unique value, the order will be discarded and an error response will be sent.

### General Fields

| Inbound | Outbound | Disposition | Field Name                 | Format    | Example        |
| ------- | -------- | ----------- | -------------------------- | --------- | -------------- |
| * w     | \* w     | + w         | OwnerCode                  | Picklist  | RIN            |
| \* w    | \* w     | + w         | SupplierCode               | Picklist  | RIN            |
| x       | \* w     | x           | DesiredDeliveryDate        | Date      | 2018-10-22     |
| \* w    | x        | x           | EstimatedShipDate          | Date      | 2018-10-22     |
| + w     | + w      | +           | PurchaseOrderNumber        | Text(50)  | PO1234         |
| + w     | + w      | x           | AdditionalOrderNumber      | Text(50)  | ADDITIONAL1234 |
| +       | +        | x           | AdditionalShipmentComments | Text(255) |                |
| +       | +        | x           | CustomerField1             | Text(255) |                |
| +       | +        | x           | CustomerField2             | Text(255) |                |
| +       | +        | x           | CustomerField3             | Text(255) |                |

The **OwnerCode** specifies the owner of the material at the time the request is sent. If ownership changes after sending, a *PATCH Update* request should be sent. The **SupplierCode** specifies who distributes or manufactures the material. Both *OwnerCode* and *SupplierCode* must match specific values in Rinchem's system. Please ask your Rinchem contact for a list of relevant owner and supplier codes to use.

The **DesiredDeliverDate** describes when you would like the material to arrive at your facility; it should **only be used for Outbound Orders**. 
The **EstimatedShipDate** similarly describes when you expect the material to leave your facility; it should **only be used for Inbound Orders**.

The **PurchaseOrderNumber** is the purchase order number that pertains to the request. It will travel with the material on the BOL. The *PurchaseOrderNumber* may also be provided at the line item level if necessary. 
The **AdditionalOrderNumber** may be used to store any secondary order numbers that you would like associated with the request. It will live entirely in *Chem-Star* and will not be passed on to our WMS or appear on any forms.

**AdditionalShipmentComments** and **CustomerField**s may be used for any header level information that you would like stored that we haven't provided a specific field for.  They live entirely in *Chem-Star* and will not be passed on to our WMS or appear on any forms.

### Contact Fields

| Inbound | Outbound | Disposition | Field Name                 | Format   | Example                                             |
| ------- | -------- | ----------- | -------------------------- | -------- | --------------------------------------------------- |
| +       | +        | x           | Requester_Email            | Text(70) | [requester@email.com](mailto:requester@email.com)   |
| +       | +        | x           | Requester_Phone            | Text(70) | 1-555-123-4567                                      |
| +       | +        | x           | SecondaryContact_FirstName | Text(70) | John                                                |
| +       | +        | x           | SecondaryContact_LastName  | Text(70) | Doe                                                 |
| +       | +        | x           | SecondaryContact_Company   | Text(70) | EXAMPLE CO                                          |
| +       | +        | x           | SecondaryContact_Phone     | Text(70) | 1-555-123-4567                                      |
| +       | +        | x           | SecondaryContact_Email     | Text(70) | [john.doe@example.com](mailto:john.doe@example.com) |

The **Requester** and **SecondaryContact** fields are entirely optional. They simply provide Rinchem with contacts to reach out to if there happens to be an issue with the order. There is no guarantee that they will be notified of the order or any order updates. These fields live entirely in *Chem-Star* and will not be passed to our WMS or appear on any forms.
The **Requester** fields should be used to describe the person sending the request payload. If these fields are left blank, the values will be populated with information pulled from your *Chem-Star* profile. 
The **SecondaryContact** fields should be used to describe anybody else of concern, this may potentially be an approver, a facility engineer, or perhaps somebody that you are submitting the order on behalf of. 

### Freight Fields

| Inbound | Outbound | Disposition | Field Name                            | Format    | Example  |
| ------- | -------- | ----------- | ------------------------------------- | --------- | -------- |
| * w     | * w      | x           | Freight_CarrierService                | Picklist  | RINCHEM  |
| +       | +        | x           | Freight_CarrierService_TrackingNumber | Text(100) | abc12345 |
| +       | +        | x           | Freight_CarrierService_AccountNumber  | Text(100) | 12345abc |

The **Freight_CarrierService** specifies the company that will be transporting your material. You will need to use Rinchem specific values for this field, please ask see the ***REF_PicklistValues.md*** file for a list of relevant carrier service codes. **Freight_CarrierService_AccountNumber** specifies the account number that you have open with the specified *Freight_CarrierService*.
**Freight_CarrierService_TrackingNumber** specifies any tracking number that has bee provided by the specified *Freight_CarrierService*.

| Inbound | Outbound | Disposition | Field Name                | Format   | Example            |
| ------- | -------- | ----------- | ------------------------- | -------- | ------------------ |
| *       | * w      | x           | Freight_BillTo_Type       | Picklist | Recipient          |
| +       | + w      | x           | Freight_BillTo_Name       | Text(40) | John Doe           |
| +       | + w      | x           | Freight_BillTo_Company    | Text(40) | EXAMPLE CO         |
| +       | + w      | x           | Freight_BillTo_Street1    | Text(30) | 123 Example Street |
| +       | + w      | x           | Freight_BillTo_Street2    | Text(30) |                    |
| +       | + w      | x           | Freight_BillTo_Street3    | Text(30) |                    |
| +       | + w      | x           | Freight_BillTo_City       | Text(20) | Albuquerque        |
| +       | + w      | x           | Freight_BillTo_State      | Text(20) | NM                 |
| +       | + w      | x           | Freight_BillTo_PostalCode | Text(10) | 87109              |
| +       | + w      | x           | Freight_BillTo_Country    | Text(20) | USA                |

**Freight_BillTo_Type** is a picklist that will accept 1 of the 3 following values:

> ***Requester*** - indicates that you, the person sending the payload, is responsible for payments. 
> ***Recipient*** - indicates that the *ShipTo* recipient will be responsible for the payment. 
> ***Third Party*** - indicates that an outside party, described in the subsequent *Freight_BillTo* address fields, will be responsible for payment.

The remaining **Freight_BillTo** fields are only applicable if ***Third Party*** has been selected.

| Inbound | Outbound | Disposition | Field Name                             | Format   | Example       |
| ------- | -------- | ----------- | -------------------------------------- | -------- | ------------- |
| *       | *        | x           | Freight_IsInternationalShipment        | Boolean  | TRUE          |
| +       | +        | x           | Freight_International_ImporterOfRecord | Text(40) | EXAMPLE OWNER |
| +       | +        | x           | Freight_MethodOfTransport              | Picklist | Domestic      |

**Freight_IsInternationalShipment** lets us know if the shipment will be crossing any international borders. 

**Freight_InternationalShipment_ImporterOfRecord** then tells us who will be responsible for the material once it reaches customs. It is only applicable if the request is for an international shipment

**Freight_MethodOfTransport** specifies how the material will be transported. The field is available for both domestic and international shipments, though it's primary purpose is to specify whether an international shipment will be sent by *OCEAN* or *AIR*. Domestic shipments currently may only specify *GROUND* or leave it blank.

### Ship To Fields

| Inbound | Outbound | Disposition | Field Name           | Format   | Example            |
| ------- | -------- | ----------- | -------------------- | -------- | ------------------ |
| * w     | x        | x           | ShipTo_WarehouseCode | Picklist | 16                 |
| x       | * w      | x           | ShipTo_Name          | Text(40) | John Doe           |
| x       | + w      | x           | ShipTo_Company       | Text(40) | EXAMPLE CO         |
| x       | * w      | x           | ShipTo_Street1       | Text(40) | 123 Example Street |
| x       | + w      | x           | ShipTo_Street2       | Text(40) |                    |
| x       | + w      | x           | ShipTo_Street3       | Text(40) |                    |
| x       | * w      | x           | ShipTo_City          | Text(20) | Albuquerque        |
| x       | * w      | x           | ShipTo_State         | Text(20) | NM                 |
| x       | * w      | x           | ShipTo_PostalCode    | Text(10) | 87109              |
| x       | * w      | x           | ShipTo_Country       | Text(20) | USA                |

The **ShipTo** fields let us know the final destination for your requested material. 

The **ShipTo_WarehouseCode** should only be used in the case of an **Inbound** request and must use a Rinchem recognized warehouse code, please see the ***REF_PicklistValues.md*** file for a list of relevant warehouse codes.  

The other **ShipTo** fields should only be used in the case of an **Outbound** request.

### Ship From Fields

| Inbound | Outbound | Disposition | Field Name             | Format   | Example            |
| ------- | -------- | ----------- | ---------------------- | -------- | ------------------ |
| x       | * w      | x           | ShipFrom_WarehouseCode | Picklist | 11                 |
| *       | x        | x           | ShipFrom_Name          | Text(40) | John Doe           |
| +       | x        | x           | ShipFrom_Company       | Text(40) | EXAMPLE CO         |
| +       | x        | x           | ShipFrom_Street1       | Text(40) | 123 Example Street |
| +       | x        | x           | ShipFrom_Street2       | Text(40) |                    |
| +       | x        | x           | ShipFrom_Street3       | Text(40) |                    |
| +       | x        | x           | ShipFrom_City          | Text(20) | Albuquerque        |
| +       | x        | x           | ShipFrom_State         | Text(20) | NM                 |
| * w     | x        | x           | ShipFrom_PostalCode    | Text(10) | 87109              |
| +       | x        | x           | ShipFrom_Country       | Text(20) | USA                |

The **ShipFrom** fields let us know the material's origin of shipment. 

The **ShipTo_WarehouseCode** should only be used in the case of an **Outbound** request and must use a Rinchem recognized warehouse code, please see the ***REF_PicklistValues.md*** file for a list of relevant warehouse codes.  

The other **ShipFrom** fields should only be used in the case of a F2W request.

### Customer Fields
| Inbound | Outbound | Disposition | Field Name                       | Format        | Example         |
| ------- | -------- | ----------- | -------------------------------- | ------------- | --------------- |
| x       | x        | +           | Customer_AvailableHoldCodes      | List(String)  | ["OH"]          |
| x       | x        | +           | Customer_ModifyLotsWithHoldCodes | List(String)  | ["OK"]          |
| x       | x        | +           | Customer_ReturnRecord            | Boolean       | true            |

The **Customer** fields holds information that is specific to the customer. This is information that will be used to help process disposition requests. 

The **Customer_AvailableHoldCodes** field contains all the hold codes that could possibly be used as a hold code status in the request. The intention of this field to hold all the hold codes that are available for use. For example, sending OH means that you can only change the hold code status to OH.

The **Customer_ModifyLotsWithHoldCodes** field is a way to specifiy which lots can be modified based on the hold code status of each line item. For example, if any of the line items in the requested lot have a hold code other than OK, then this lot becomes unmodifiable else if it has all line items with the status OK then it will successfully modify the lots.   

The **Customer_ReturnRecord** field if set true will return record values. 

### GET Only Fields

These are fields that reflect how the order has been processed in the Rinchem system and cannot be sent/modified by integrators.

| Inbound | Outbound | Disposition | Field Name              | Format    | Example                                                      |
| ------- | -------- | ----------- | ----------------------- | --------- | ------------------------------------------------------------ |
| +       | +        | x           | Record_Status           | Picklist  | SUBMITTED                                                    |
| +       | +        | x           | Record_Message          | Text(255) | Your record has passed initial validation and has been submitted to our warehouse management system. |
| + w     | + w      | x           | Record_CreatedDate      | Date/Time | 2018-07-25T22:58:03.000Z                                     |
| + w     | + w      | x           | Record_LastModifiedDate | Date/Time | 2018-07-25T23:23:14.000Z                                     |

The **Record_Status** and **Record_Message** fields describe the status of the request within Rinchem's system. Please see the ***REF_PicklistValues.md*** file for all available statuses and their meaning.

## Line Item Fields

### Record Fields (line)

| Inbound | Outbound | Disposition | Field Name              | Format     | Example  |
| ------- | -------- | ----------- | ----------------------- | ---------- | -------- |
| + w     | + w      | +           | RecordLine_Number       | Integer(5) | 1        |
| +       | +        | +           | RecordLine_ExternalName | Text(255)  | EXAMPLE1 |

The **RecordLine_Number** and **RecordLine_ExternalName** are fields that allow you to reference the line item in *PATCH* and *GET* calls. Each value must be unique to the order, meaning two lines can't both have a *Record_LineNumber* of '1'. If this occurs, the payload will be discarded and an error will be returned. *RecordLine_Number* should be used for integer values only! *RecordLine_ExternalName* may be any character string.

### General Fields (line)

| Inbound | Outbound | Disposition | Field Name          | Format      | Example |
| ------- | -------- | ----------- | ------------------- | ----------- | ------- |
| * w     | * w      | +           | Quantity            | Integer(12) | 6       |
| * w     | * w      | * w         | LotNumber           | Text(20)    | 12345   |
| +       | x        | +           | SerialNumber        | Text(50)    | 54321   |
| * w     | * w      | +           | UnitOfMeasure       | Picklist    | BOTTLE  |
| +       | +        | +           | PurchaseOrderNumber | Text(10)    | PO1234  |
| +       | + w      | +           | AdditionalComments  | Text(50)    |         |
| +       | +        | x           | LineCustomerField1  | Text(255)   |         |
| +       | +        | x           | LineCustomerField2  | Text(255)   |         |
| +       | +        | x           | LineCustomerField3  | Text(255)   |         |

**LotNumber** tells us which lot we will be picking/receiving for this request. 

**UnitOfMeasure** tells us what unit of measure the *Quantity* field is referencing; this must match what is set up in our product table and must be a Rinchem recognized value. Please see the ***REF_PicklistValues.md*** file for a list of available units.  

**PurchaseOrderNumber** tells us what purchase order number applies specifically to this line of material. It should only be provided if it differs from the header level PurchaseOrderNumber.

**AdditionalComments** and **LineCustomerField**s are used to store any additional information pertaining to this line of material that we didn't explicitly provide a field for. They currently live exclusively on Salesforce and will not appear on any forms.

### Product Number Fields (line)

| Inbound | Outbound | Disposition | Field Name                 | Format   | Example       |
| ------- | -------- | ----------- | -------------------------- | -------- | ------------- |
| + w     | + w      | x           | Product_RinchemPartNumber  | Text(25) | 12345_EXAMPLE |
| +       | +        | +           | Product_OwnerPartNumber    | Text(25) | OWN1234       |
| +       | +        | +           | Product_SupplierPartNumber | Text(25) | SUP1234       |

The **ProductNumber** fields specify the part number of the product that is being shipped. Any, and at least one, of the three must be sent in. If any of the three are found, the other two will be populated based on our alias table. If none of them are found, an error case will be created and manual intervention will be required.

### Hold Code and Attribute Fields (line)

| Inbound | Outbound | Disposition | Field Name                 | Format   | Example            |
| ------- | -------- | ----------- | -------------------------- | -------- | ------------------ |
| + w     | + w      | * w         | HoldCode                   | Picklist | VH                 |
| +       | +        | +           | HoldCode_Reason            | Text(25) | Needs verification |
| + w     | + w      | + w         | Attributes_Destination     | Text(30) | D12                |
| + w     | + w      | + w         | Attributes_Process         | Text(30) | 1272               |
| + w     | + w      | + w         | Attributes_Other           | Text(30) | IO,PQ              |
| + w     | + w      | + w         | Attributes_ComponentStatus | Text(30) | NT                 |
| + w     | + w      | + w         | Attributes_OwnerStatus     | Text(30) | CO                 |

The **HoldCode** and **Attributes** fields let us know what state the material is in when it is received.

The **HoldCode** field lets us know the hold code that is associated with the order. For example, sending VH, would let us know that the material is on vendor hold. The **HoldCode_Reason** field would then be used to let us know why. The **Attributes** fields on the other hand are allocations applied to the material. 

Both **HoldCode** and **Attributes** must use Rinchem accepted values. Please see the ***REF_PicklistValues.md*** file for a list of available hold codes and attributes.
