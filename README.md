# Rinchem Easy-Link API Integration 

#### Table Of Contents

> [Overview](#overview)
>
> [README Files](#readme-files)
> > [README_Authenticating](#readme_authenticatingmd)<br/>
> > [README_BuildingPayloads](#readme_buildingpayloadsmd)<br/>
> > [README_SendingRequests](#readme_sendingrequestsmd)<br/>
> > [README_HandlingErrors](#readme_handlingerrorsmd)<br/>
>
> [REF Files](#ref-files)
> > [REF_PostmanWalkthrough](#ref_postmanwalkthroughmd)<br/>
> > [REF_AllFields](#ref_allfieldsmd)<br/>
> > [REF_PayloadExamples](#ref_payloadexamplesmd)<br/>
> > [REF_PicklistValues](#ref_picklistvaluesmd)<br/>
> > [REF_ErrorResponses](#ref_errorresponsesmd)<br/>

## Overview

Rinchem is committed to making the API integration process straightforward, reliable, and transparent. Over time, we will build a robust platform that will allow you to submit orders, review your history, and generate reports. Initially our API platform will be available for **Inbound Order** and **Outbound Order** requests.

> The **Inbound** request will encompass both material *Returns* **and** *Advanced Shipping Notices*. Anything leaving your facility and arriving at a Rinchem warehouse would be considered an inbound order.
>
> The **Outbound** request will encompass any request for material to leave a Rinchem warehouse and arrive at your facility.

There are four major steps in connecting to our API: 

1. ***Authenticating Your Credentials***
2. ***Building Your Payload*** 
3. ***Sending Your Request***
4. ***Handling Errors***

Each of these steps are described briefly below. They each also have there own dedicated **README** file in order to help break up the information for you. Along with the individual README files, there are also a few ***REF*** files to aid your path to integration.

Though each file is standalone and they can be read out of order, we do recommend you read the entirety of this file first, then read through ***README_Authenticating***, ***README_BuildingPayloads***, and ***README_SendingRequests***; in that order. We also highly recommend you follow along with the ***REF_PostmanWalkthrough*** prior to starting.



## README Files

### [README_Authenticating.md](README_Authenticating.md)

The first step in connecting to our API is proving to *Chem-Star* that you are the user that you claim to be. This is done by passing your user credentials to a generic *Salesforce API* that will then pass back an ***instance_url*** and and ***access_token*** that can then be used to access the *EasyLink API*.

This file walks you through setting up the authentication call and explains how to handle the response(s) you may receive.

### [README_BuildingPayloads.md](README_BuildingPayloads.md)

The second step in connecting to our API is going to be converting your data into a payload that our system can understand.  

This file is going to explain the payload structure as well as discuss some design considerations to think about before you start building.

### [README_SendingRequests.md](README_SendingRequests.md)

The third step in connecting to our API is going to be combining the credentials you received from the *Authenticating* phase and the payload that you built during the *BuildingPayloads* phase into one request that you can send Rinchem for processing. 

This file is going to explain how to set up the request depending on whether you want to send a new payload, update a prior payload, cancel a payload, or retrieve existing orders. It is also going to explain the successful responses that you can expect to see after sending the request..

### [README_HandlingErrors.md](README_HandlingErrors.md)

The final step in connecting to the Easy-Link API is going to be handling the response when things don't quite go as plan. There are four types of errors that can occur while the payload is traversing our system. 

This file is going to explain the format for each type of error response. It is also going to explain the separation of due diligence between an error that must be corrected by the requester, versus an error that may need to be corrected by Rinchem.

## REF Files

### [REF_PostmanWalkthrough.md](REF_PostmanWalkthrough.md)

*Postman* is a Google Chrome WebApp that allows you to manually create and send HTTP requests. 

This resource walks you through manually calling the *Salesforce Authentication API* with *Postman*. It then shows how to use the authentication response to build a new request that will call the *Easy-Link API*. It is a pretty quick activity and really helps to understand the steps required in integration.

### [REF_AllFields.md](REF_AllFields.md)

As you get to going building your payloads, this resource will help you know: what fields you can map to, what fields we require you to map to, and how we are going to interpret each field that you send us.

### [REF_PayloadExamples.md](REF_PayloadExamples.md)

This file is going to show you some examples with the the format that you need for your payloads. It has a minimum payload example and a full payload example for both F2W and W2F requests.

### [REF_PicklistValues.md](REF_PicklistValues.md)

Some fields that you map to are going to require specific values. This means they are not freeform and you may have to use some sort of alias table to convert your values into one of our accepted values. This file is going to list out all values that we will accept for each of our 'Picklist' fields.

### [REF_ErrorResponses.md](REF_ErrorResponses.md)

You may get into some trouble understanding the error responses you may get back from sending requests. This file contains a compiled list of error responses with an explanation on why the error occured during your requests. 
