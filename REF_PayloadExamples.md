## Payload Samples (for *Post* requests)

#### Table of Contents

> [Minimum Inbound Payload](#minimum-inbound-payload)<br/>
> [Minimum Outbound Payload](#minimum-outbound-payload)<br/>
> [Minimum Disposition Payload](#minimum-disposition-payload)<br/>
> [Full Inbound Payload](#full-inbound-payload)<br/>
> [Full Outbound Payload](#full-outbound-payload)<br/>
> [Full Disposition Payload](#full-disposition-payload)<br/>
> [Full Generic Payload](#full-generic-payload)<br/>



## Minimum Inbound Payload

```json
{
    "OwnerCode" : "OWN",
    "SupplierCode" : "SUP",
    "EstimatedShipDate" : "2018-10-22",
    "PurchaseOrderNumber" : "A12345",
    "Freight_CarrierService" : "RINCHEM",
    "Freight_BillTo_Type" : "Requester",
    "Freight_BillTo_Name" : "John Doe",
    "Freight_IsInternationalShipment" : false,
    "ShipTo_WarehouseCode" : "11",
    "ShipFrom_Name" : "John Doe",
    "ShipFrom_Street1" : "123 Example Street",
    "ShipFrom_City" : "Albuquerque",
    "ShipFrom_State" : "NM",
    "ShipFrom_PostalCode" : "87109",
    "ShipFrom_Country" : "USA",

    "LineItems" : 
    [
        {
            "RecordLine_Number" : 1,
            "Product_OwnerPartNumber" : "OWN1234",
            "LotNumber" : "12345",
            "Quantity" : 5,
            "UnitOfMeasure" : "BOTTLE" 
        }
    ]
}
```

## Minimum Outbound Payload

```json
{
    "OwnerCode" : "OWN",
    "SupplierCode" : "SUP",
    "DesiredDeliveryDate" : "2018-10-22",
    "PurchaseOrderNumber" : "A12345",
    "Freight_CarrierService" : "RINCHEM",
    "Freight_BillTo_Type" : "Requester",
    "Freight_BillTo_Name" : "John Doe",
    "Freight_IsInternationalShipment" : false,
    "ShipFrom_WarehouseCode" : "11",
    "ShipTo_Name" : "John Doe",
    "ShipTo_Street1" : "123 Example Street",
    "ShipTo_City" : "Albuquerque",
    "ShipTo_State" : "NM",
    "ShipTo_PostalCode" : "87109",
    "ShipTo_Country" : "USA",

    "LineItems" : 
    [
        {
            "RecordLine_Number" : 1,
            "Product_OwnerPartNumber" : "OWN1234",
            "LotNumber" : "12345",
            "Quantity" : 5,
            "UnitOfMeasure" : "BOTTLE" 
        }
    ]
}
```

## Minimum Disposition Payload

```json
{
    "Customer_AvailableHoldCodes": ["OH"],
    "Customer_ModifyLotsWithHoldCodes": ["OK"],
    "Customer_ReturnRecord": true,

    "LineItems" : 
    [
        {
            "Product_OwnerPartNumber" : "00186390",
            "LotNumber" : "0000250390",
	    "HoldCode" : "OH"
        }
    ]
}
```

## Full Inbound Payload

```json
{
    "Record_ExternalName" : "EXA_INBOUND_10001",
    "OwnerCode" : "OWN",
    "SupplierCode" : "SUP",
    "EstimatedShipDate" : "2018-10-22",
    "PurchaseOrderNumber" : "PO1234",
    "AdditionalOrderNumber" : "ADDITIONAL1234",
    "AdditionalShipmentComments" : "This is a test payload",
    "Requester_Email" : "requester@email.com",
    "Requester_Phone" : "1-555-123-4567",
    "SecondaryContact_FirstName" : "John",
    "SecondaryContact_LastName" : "Doe",
    "SecondaryContact_Company" : "EXAMPLE CO",
    "SecondaryContact_Phone" : "1-555-765-4321",
    "SecondaryContact_Email" : "john.doe@example.com",
    "Freight_CarrierService" : "RINCHEM",
    "Freight_CarrierService_AccountNumber" : "abc12345",
    "Freight_CarrierService_TrackingNumber" : "54321abc",
    "Freight_BillTo_Type" : "Requester",
    "Freight_BillTo_Name" : "John Doe",
    "Freight_BillTo_Company" : "EXAMPLE CO",
    "Freight_BillTo_Street1" : "123 Example St",
    "Freight_BillTo_Street2" : "",
    "Freight_BillTo_Street3" : "",
    "Freight_BillTo_City" : "Albuquerque",
    "Freight_BillTo_State" : "NM",
    "Freight_BillTo_PostalCode" : "87109",
    "Freight_BillTo_Country" : "USA",
    "Freight_IsInternationalShipment" : false,
    "Freight_InternationalShipment_ImporterOfRecord" : "",
    "Freight_MethodOfTransport" : "Domestic",
    "ShipTo_WarehouseCode" : "11",
    "ShipFrom_Name" : "John Doe",
    "ShipFrom_Company" : "EXAMPLE CO",
    "ShipFrom_Street1" : "123 Example Street",
    "ShipFrom_Street2" : "",
    "ShipFrom_Street3" : "",
    "ShipFrom_City" : "Albuquerque",
    "ShipFrom_State" : "NM",
    "ShipFrom_PostalCode" : "87109",
    "ShipFrom_Country" : "USA",

    "LineItems" : 
    [
        {
            "RecordLine_Number" : 1,
            "Product_OwnerPartNumber" : "OWN1234",
            "Product_SupplierPartNumber" : "SUP1234",
            "Product_RinchemPartNumber" : "1234_EXAMPLE",
            "Quantity" : 5,
            "LotNumber" : "12345A",
            "SerialNumber" : "54321A",
            "UnitOfMeasure" : "BOTTLE",
            "PurchaseOrderNumber" : "PO1234",
            "AdditionalComments" : "This is a test line.",
            "Status" : "VH",
            "Status_Reason" : "Needs verification",
            "Attributes_Destination" : "D12",
            "Attributes_Process" : "1272",
            "Attributes_Other" : "IO,PQ",
            "Attributes_ComponentStatus" : "NT"
        }
    ]
}
```

## Full Outbound Payload

```json
{
    "Record_ExternalName" : "EXA_OUTBOUND_10001",
    "OwnerCode" : "OWN",
    "SupplierCode" : "SUP",
    "DesiredDeliveryDate" : "2018-10-22",
    "PurchaseOrderNumber" : "PO1234",
    "AdditionalOrderNumber" : "ADDITIONAL1234",
    "AdditionalShipmentComments" : "This is a test payload",
    "Requester_Email" : "requester@email.com",
    "Requester_Phone" : "1-555-123-4567",
    "SecondaryContact_FirstName" : "John",
    "SecondaryContact_LastName" : "Doe",
    "SecondaryContact_Company" : "EXAMPLE CO",
    "SecondaryContact_Phone" : "1-555-765-4321",
    "SecondaryContact_Email" : "john.doe@example.com",
    "Freight_CarrierService" : "RINCHEM",
    "Freight_CarrierService_AccountNumber" : "abc12345",
    "Freight_CarrierService_TrackingNumber" : "54321abc",
    "Freight_BillTo_Type" : "Requester",
    "Freight_BillTo_Name" : "John Doe",
    "Freight_BillTo_Company" : "EXAMPLE CO",
    "Freight_BillTo_Street1" : "123 Example St",
    "Freight_BillTo_Street2" : "",
    "Freight_BillTo_Street3" : "",
    "Freight_BillTo_City" : "Albuquerque",
    "Freight_BillTo_State" : "NM",
    "Freight_BillTo_PostalCode" : "87109",
    "Freight_BillTo_Country" : "USA",
    "Freight_IsInternationalShipment" : false,
    "Freight_InternationalShipment_ImporterOfRecord" : "",
    "Freight_MethodOfTransport" : "Domestic",
    "ShipFrom_WarehouseCode" : "11",
    "ShipTo_Name" : "John Doe",
    "ShipTo_Company" : "EXAMPLE CO",
    "ShipTo_Street1" : "123 Example Street",
    "ShipTo_Street2" : "",
    "ShipTo_Street3" : "",
    "ShipTo_City" : "Albuquerque",
    "ShipTo_State" : "NM",
    "ShipTo_PostalCode" : "87109",
    "ShipTo_Country" : "USA",

    "LineItems" : 
    [
        {
            "RecordLine_Number" : 1,
            "Product_OwnerPartNumber" : "OWN1234",
            "Product_SupplierPartNumber" : "SUP1234",
            "Product_RinchemPartNumber" : "1234_EXAMPLE",
            "Quantity" : 5,
            "LotNumber" : "12345A",
            "UnitOfMeasure" : "BOTTLE",
            "PurchaseOrderNumber" : "PO1234",
            "AdditionalComments" : "This is a test line."
        }
    ]
}
```

## Full Disposition Payload

```json
{
    "OwnerCode" : "OWN",
    "SupplierCode" : "",
    "Customer_AvailableHoldCodes": ["OH"],
    "Customer_ModifyLotsWithHoldCodes": ["OK"],
    "Customer_ReturnRecord": true,

    "LineItems" : 
    [
        {
            "Product_OwnerPartNumber" : "00186390",
            "LotNumber" : "0000250390",
      	    "HoldCode" : "OH"
        }
    ]
}
```


## Full Generic Payload

```json
{
    "Record_ExternalName" : "",
    "OwnerCode" : "",
    "SupplierCode" : "",
    "EstimatedShipDate" : "",
    "DesiredDeliveryDate" : "",
    "PurchaseOrderNumber" : "",
    "AdditionalOrderNumber" : "",
    "AdditionalShipmentComments" : "",
    "Requester_Email" : "",
    "Requester_Phone" : "",
    "SecondaryContact_FirstName" : "",
    "SecondaryContact_LastName" : "",
    "SecondaryContact_Company" : "",
    "SecondaryContact_Phone" : "",
    "SecondaryContact_Email" : "",
    "Freight_CarrierService" : "",
    "Freight_CarrierService_AccountNumber" : "",
    "Freight_CarrierService_TrackingNumber" : "",
    "Freight_BillTo_Type" : "",
    "Freight_BillTo_Name" : "",
    "Freight_BillTo_Company" : "",
    "Freight_BillTo_Street1" : "",
    "Freight_BillTo_Street2" : "",
    "Freight_BillTo_Street3" : "",
    "Freight_BillTo_City" : "",
    "Freight_BillTo_State" : "",
    "Freight_BillTo_PostalCode" : "",
    "Freight_BillTo_Country" : "",
    "Freight_IsInternationalShipment" : "",
    "Freight_InternationalShipment_ImporterOfRecord" : "",
    "Freight_MethodOfTransport" : "",
    "ShipFrom_WarehouseCode" : "",
    "ShipTo_WarehouseCode" : "",
    "ShipFrom_Name" : "",
    "ShipFrom_Company" : "",
    "ShipFrom_Street1" : "",
    "ShipFrom_Street2" : "",
    "ShipFrom_Street3" : "",
    "ShipFrom_City" : "",
    "ShipFrom_State" : "",
    "ShipFrom_PostalCode" : "",
    "ShipFrom_Country" : "",
    "ShipTo_Name" : "",
    "ShipTo_Company" : "",
    "ShipTo_Street1" : "",
    "ShipTo_Street2" : "",
    "ShipTo_Street3" : "",
    "ShipTo_City" : "",
    "ShipTo_State" : "",
    "ShipTo_PostalCode" : "",
    "ShipTo_Country" : "",

    "LineItems" : 
    [
        {
            "RecordLine_Number" : ,
            "Product_OwnerPartNumber" : "",
            "Product_SupplierPartNumber" : "",
            "Product_RinchemPartNumber" : "",
            "Quantity" : ,
            "LotNumber" : "",
            "SerialNumber" : "",
            "UnitOfMeasure" : "",
            "PurchaseOrderNumber" : "",
            "AdditionalComments" : "",
            "Status" : "",
            "Status_Reason" : "",
            "Attributes_Destination" : "",
            "Attributes_Process" : "",
            "Attributes_Other" : "",
            "Attributes_ComponentStatus" : ""
        }
    ]
}
```
