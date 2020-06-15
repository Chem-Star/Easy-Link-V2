# EasyLink-API V2 - Error Responses

#### Table Of Contents

> [Disposition Error Responses](#disposition-error-responses)
> > [Admin Error](#admin-error)<br/>
> > [Payload Validation Error](#payload-validation-error)<br/>
> > [Data Availability Error](#data-availability-error)<br/>
>
> [Inbound Error Responses](#inbound-error-responses)<br/>
> [Outbound Error Responses](#outbound-error-responses)<br/>

## Disposition Error Responses

### Admin Error

The following error can be caused by an integration user not being set up properly to make Disposition requests. This type of error will need to be resolved by a Chem-star admin.   

```
{
    "message": "The integration user being used does not have a user type. Please contact your Chem-star Admin for support @{email address}.",
    "status": "DATA_VALIDATION_ERROR"
}
```

### Payload Validation Error

The following error can caused by an invalid payload request. This usually occurs when there are incorrect field mappings/definitions in the payload request. For example, if the above payload had the field **OwnerCode** written as OwnerCode1, the below response would be sent back. 

```
{
    "message": "There was an error while deserializing your request",
    "status": "DATA_VALIDATION_ERROR"
}
```

The following error can be caused by missing fields. Depending on the integration user that is used to send the request, the Dispostion integration currently requires the requester to send either an **Owner Code** or **Supplier Code** in the header fields. Part Number, Lot Number, and Hold Code is required on all Line Item fields. 

```
{
    "message": "Your request could not be completed due to missing fields: {missing fields}",
    "status": "DATA_VALIDATION_ERROR"
}
```

The following error can be caused by entering a Customer Code that is not associated with the Integration user that is being used for sending the request. A similar error will come back if an incorrect supplier code was passed in. If you do not know your customer code please contact your Chem-star admin.  

```
{
    "message": "The Owner Code that was provided does not match the Company Code on the Integration User. Please contact your Chem-star Admin for support @{email address}",
    "status": "DATA_VALIDATION_ERROR"
}
```

The following error can be caused by sending holdcodes in the **Customer_ModifyLotsWithHoldCodes** field that are not available to the Integration user that is sending the request. Integration users who are owners may not modify lots that have a status of Vendor Hold. Integration users who are suppliers may not modify lots that have a status of On Hold. This error is in place to strictly follow the Disposition process rules. 

```
{
    "message": "You cannot modify lots containing VH. Please remove this from the Customer_ModifyLotsWithHoldCodes list to proceed.",
    "status": "DATA_VALIDATION_ERROR"
}
```

### Data Availability Error

The following error can be caused by sending a Part Number that is not in Rinchem's WMS System. If you have belief that the Part Number
is indeed in Rinchem's system, please contact your Chem-star admin to further investigate. 

```
{
    "message": "Sorry, we could not submit your request. We were not able to find part number 501238944.",
    "status": "GENERAL_ERROR"
}
```

The following errors can occur if the requested lot combination is not available to be modified in Rinchem's WMS system. A reason for why this may occur is because a previous disposition request with the same inventory that is being requested is still being processed in the WMS system. Therefore, WMS cannot take in modifications to that inventory at this time.  

```
{
    "message": "Sorry, we could not submit your request due to the provided lot not being available. ",
    "status": "GENERAL_ERROR"
}
```

```
{
    "message": "Sorry, we could not submit your request due to the provided lot not being available. The unavailability is due to this lot containing line items with a status of OUTBOUND",
    "status": "GENERAL_ERROR"
}
```

To provide some background for this error, the field **Customer_ModifyLotsWithHoldCodes** is used to contains hold codes. Those hold codes are then used to identify which lots can be modified based on the hold codes provided. For example, if hold code status OK was held in the **Customer_ModifyLotsWithHoldCodes** field, then the integration will only succeed if the all the line items on the requested lot currently holds an OK status. The integration will fail and give back this error, if the requested inventory has line items that are not in OK status. 

```
{
    "message": "Sorry, we could not submit your request due to the provided lot not being available. The unavailability is due to this lot containing line items with the following hold codes: {Rinchem_HoldCode(s)}",
    "status": "GENERAL_ERROR"
}
```

To provide some background for this error, the field **Customer_AvailableHoldCodes** is used to contains hold codes. The purpose of the field **Customer_AvailableHoldCodes**, is to establish which hold code statuses are available to be used on the requested lots. For example, if the **Customer_AvailableHoldCodes** field contains hold code status OH, then the integration will only succeeded if the requested hold code status is OH. The integration will fail and give back this error, if the requested hold code is not in the Customer_AvailableHoldCodes list field. 

```
{
    "message": "Sorry, we could not submit your request. You cannot apply hold code {Requested_HoldCode} as New Status for this lot. ",
    "status": "GENERAL_ERROR"
}
```

## Inbound Error Responses

&ast;*To be written*&ast;

## Outbound Error Responses

&ast;*To be written*&ast;
