# Easy-Link V2 - Handling Errors

## Overview
When handling data that traverses multiple systems, having accurate error messages that pin-point the true source of error is invaluable. This document intends to define what errors may occur while trying to submit an API request, as well as what course of action should be taken for each 'type' or error.

There are four primary groups of errors: improper payloads that will fail prior to receipt by the API, validation errors that occur after the API has received the payload but prior to being submitted to the WMS staging table, validation errors that occur after reaching the staging table but prior to being processed into the WMS, and finally, correctness errors that aren't caught by any automated systems and will result in improper material movement if not caught by a human check.

## Improper Payloads

Depending on the API being called there is a very specific format that the payload must conform to. These formats are detailed in the ***README_BuildingPayloads.md*** file.

The two most common errors in this category will occur in instance of an unrecognized field being sent, or a string being sent to a number field. These responses will be sent directly from Salesforce and will return as an array containing objects with fields *message* and *errorCode*. **Since these errors fail at deserialization before entering the API method, they cannot be handled by the API, and will be the responsibility of the sending party to handle and correct! No notification will be sent out!**

#### Unrecognized Field

In this example the field **Quantitay** is accidentally sent instead of **Quantity**.

```
[
    {
        "message": "No such column 'Quantitay' on object of type EasyLink_Payload_Line at [line:53, column:23]",
        "errorCode": "JSON_PARSER_ERROR"
    }
]
```

#### Improper Field Type

This may happen in the case of text being sent to a number field or an invalid date string being sent. In this example, the invalid date string was sent as **2017-05-30T-06:00:00X** rather than the proper value **2017-05-30T-06:00:00Z**.

```
[
    {
        "message": "Cannot deserialize instance of date from VALUE_STRING value 2017-05-30T-06:00:00X or request may be missing a required field at [line:11, column:55]",
        "errorCode": "JSON_PARSER_ERROR"
    }
]
```

## Invalid Payloads - Pre Staging

These errors occur when the payload is able to be de-serialized by Salesforce, however, there are fields with invalid data that can be caught with a preliminary check, prior to sending to the wms. The most common error of this type, is a missing required field. These responses will have the format of an object with fields *status*, and *message*. These errors will create an error case in the Chem-Star Portal. Errors of this type will require the full payload to be corrected and will be the responsibility of the sending party to handle and correct!**

#### Missing Required Field

In this example, the required field **From_Warehouse_Code__c**, was omitted from the sending payload.

```
{
    "status": "Error",
    "message": "Your request failed with the following error: Insert failed. First exception on row 0; first error: REQUIRED_FIELD_MISSING, Required fields are missing: [From_Warehouse_Code__c]: [From_Warehouse_Code__c]Class.OBO_Service_V1.handlePostNew: line 176, column 1\nClass.OBO_Service_V1.doPost: line 64, column 1"
}
```
#### Invalid Data

This example is specific to the Disposition Integration. In this example, the requested part number was not found in Rinchem WMS System. 

```
{
    "status": "GENERAL_ERROR"
    "message": "Sorry, we could not submit your request. We were not able to find part number 008906011",
}
```

You can find more details regarding error reseponses here. 

## Invalid Payloads - Post Staging

These errors occur when the payload passes all the smell tests and is sent over to the WMS staging table. If the payload makes it to this stage, a successful response will be returned by the API. Errors will occur when our Warehouse Management System tries to process the request. These errors will will create an error case in the Chem-Star Portal . **How users will be alerted of these errors, and how they will be handled, has yet to be set in stone.**

![img](file:///C:/Users/jdenning/Documents/Typora/Resources/ExampleApiError_PostStaging.PNG?lastModify=1509393627)

## Correctness Errors

These are errors that have no checks and manage to make it through the API, staging table, and into the WMS. All errors of this type should be scrutinized closely and a decision should be made as to whether or not the mistake should/could have been caught by our systems and how to minimize risk of the error in future.

![img](file:///C:/Users/jdenning/Documents/Typora/Resources/WhereIsMyPackage.PNG?lastModify=1509393627?lastModify=1509393627)
