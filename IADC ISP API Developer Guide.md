# IADC ISP Public API
Welcome to the IADC Incident Statistics Program (ISP) public API documentation. The IADC ISP public API can
be used to perform many of the functions possible through the web portal. This API can be used to create
new monthly reports, update the hours worked per operation category, add new SIRs, and more. 

The base of the URL for this API is **https://isp.iadc.org/publicapi**. The URI for any HTTP request sent to the API should be 
this address followed by the path for a specific endpoint.

Use the links below to get started using the API.
* For an introduction to using the API and the documentation, view the [Quick Start](#quick-start) portion 
  of this documentation.

* For a list of all endpoints, visit the [API Overview](#overview).

* For information on authentication and API keys, read the [Authentication](#authentication) portion of 
  this documentation.
  
* For information on how to interpret JSON response bodies, read [JSON Data Object Structure].

Last updated: 9/28/2023

## Table of Contents
* [Introduction](#iadc-isp-public-api)
* [Quick Start](#quick-start)
* [Overview](#overview)
* [Authentication](#authentication)
* [JSON Data Object Structure](#json-data-object-structure)
* [Lookup Values](#lookup-values)
* [Endpoints](#endpoints)

## Quick Start
In this section, we will cover all the basics you need to get started using the IADC ISP public API.
First, read about how to generate and use an API key. Then cover how to find the values you need to
make your HTTP request. Finally, we'll show an example call to the API and provide links to further 
documentation.

---

### Generate or Retrieve an API Key
If you have not used the IADC ISP public API before, you may need to generate an API key. If you have, you
will need to retrieve it. Only company administrators can generate and retrieve API keys. If you are not an
adminsitrator, contact your company's admin and ask them to generate or retrieve the key for you. 

As a comapny administrator, start by logging in to your IADC ISP account. Then navigate to the API key
page by clicking Company Admin > API Keys. 

If you already have an API key, you can copy it here. If you do not already have an API key, select 'Generate
API Key' and one will be generated for you. Once your API key appears, you can copy it.

Find more information about API key generation and retrieval here: [Authentication](#authentication).

---
### Build Your HTTP Request
Once you have an API key, you can begin constructing your HTTP request. 

First, you must determine what action you wish to take. A full list of all endpoints can be found at the
[API Overview](#overview).

Once you have decided on an endpoint, find the values you will need for your request. Start by visiting 
your endpoint's portion of this documentation. Either look for your endpoint in [Endpoints](#endpoints) or 
use the [API Overview](#overview) to link you to the correct section. Once there, locate the following:

1. Request Method and Path
    * Always required.
    * May include route or query paramters, explained below.
    * The root URI for the API is **isp.iadc.org/publicapi**
        * The URI you should use in your request is the root URI followed by the path specified for the endpoint
        you wish to hit.
2. Route and Query Parameters
    * These parameters are required for some endpoints but not needed for others. 
    * More information about accepted parameter values can be found at [Lookup Values](#lookup-values)
    or by using the [Lookups Endpoints](#lookups).
3. Body
    * Some endpoints require a body, some do not accept requests with a body, and some have an optional body.
    * If your request will include a body, ensure it is in the format specified by the endpoint's documentation.
4. Headers
    * All endpoints require the request to have an authentication header, usually the X-Api-Key header.
        * This header's value should be the API key from the first portion of this quick start guide.
        * If you are unable to set custom HTTP headers, read [Using an API Key](#using-an-api-key) for other options. 
        * For more information about API keys, visit the [Authentication](#authentication) portion of this
        documentation.
    * Check that your endpoint does not require any other headers.

With all of these values, we can now craft and send an HTTP request and receive a response. Visit the section
of this documentation covering your endpoint for information about server responses.

---

### Example
Let's consider an example. For this quick start example, we will retrieve a list of companies we have access
to. We do this by using the [Get All Companies](#get-all-companies) endpoint. 

Using the [Get All Companies](#get-all-companies) endpoint documentation, we can quickly determine our needed
values.

1. Request Method and Path
    * GET
    * /Companies
    * URI: **isp.iadc.org/publicapi/Companies**
2. Route and Query Parameters
    * No parameters
3. Body
    * No body
4. Headers
    * X-Api-Key
        * We'll use the following sample key: isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae
    * No other headers

Using these values, we construct our HTTP request:

> GET&emsp;&emsp;isp.iadc.org/publicapi/Companies   
> X-Api-Key: "isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae"


The response from this request is a status code of 200 and a JSON list of companies we have access to, as shown
below:   

> 200&emsp;&emsp; OK   
> [   
> &emsp;{   
> &emsp;&emsp;"participantCompanyID": 123,   
> &emsp;&emsp;"participantCompanyName": "Example Drilling Co.",   
> &emsp;&emsp;"role": "ParticipantCompanyAdmin",   
> &emsp;&emsp;"userID": 2   
> &emsp;},    
> &emsp;{   
> &emsp;&emsp;"participantCompanyID": 321,   
> &emsp;&emsp;"participantCompanyName": "Notreal Drilling",   
> &emsp;&emsp;"role": "ParticipantCompanyUser",   
> &emsp;&emsp;"userID": 2   
> &emsp;}    
> ] 

Where to go from here:

* For more information about the endpoint used in this example, read [Get All Companies](#get-all-companies).

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* For information on authentication and API keys, read the [Authentication](#authentication) portion of 
  this documentation.

* [Return to Table of Contents](#table-of-contents)

---

## Overview
The following is a list of all endpoints. Click each endpoint to find more information about it.

### Companies
[**Get All Companies**](#get-all-companies) - 
Returns all companies that the API key owner is allowed to access, along with the owner's roles for each company.

### Monthly Reports

[**Get All Monthly Reports**](#get-all-monthly-reports) - 
Returns a list of all monthly reports for the specified company.

[**Get a Specific Monthly Report**](#get-a-specific-monthly-report) - 
Returns a single monthly report according to the reportID provided.

[**Add a New Monthly Report**](#add-a-new-monthly-report) - 
Adds a new monthly report according to the companyID and reportMonth.

[**Submit an Existing Monthly Report**](#submit-an-existing-monthly-report) - 
Validates report for submission and then changes status of report to submitted.

[**Delete Monthly Report**](#delete-monthly-report) - 
Deletes the monthly report specified by the companyID and reportMonth.

### Operation Categories

[**Get Hours for an Operation Category**](#get-hours-for-an-operation-category) - 
Returns the hours worked for the specified operation category.

[**Create or Update an Operation Category**](#create-or-update-an-operation-category) - 
Either updates the hours worked for an already existing operation category or creates a new operation 
category and then updates the hours worked.

### SIRs

[**Get a Specific SIR**](#get-a-specific-sir) - 
Returns the SIR specified by the sirID.

[**Create New SIR**](#create-new-sir) - 
Creates a new SIR for the provided month, operation category, and incident statistic type. SIR is updated to 
include information from the body of the request, if provided.

[**Update SIR**](#update-sir) - 
Updates the specified SIR with the information included in the body of the request.

[**Delete SIR**](#delete-sir) - 
Deletes the SIR specified by the sirID. 

### Lookups

[**Get Incident Questions and Answers**](#get-incident-questions-and-answers) - 
Returns all incident questions that must be answered for each SIR. Also provides the valid answer options for 
each question.

[**Get Operation Categories**](#get-operation-categories) - 
Returns all possible valid operation category values. 

[**Get Incident Statistic Types**](#get-incident-statistic-types) - 
Returns all valid incident statistic type values. 

<!--
[**Get Countries**](#get-countries) - 
Returns all possible valid country values.-->


Where to go from here:

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* For an overview of API keys and authentication, visit the [Authentication](#authentication) portion of this documentation.

* For information on how to interpret JSON response bodies, read [JSON Data Object Structure](#json-data-object-structure).

* [Return to Table of Contents](#table-of-contents)
---


## Authentication
API keys are the authentication and authorization scheme used for the IADC ISP public API. When a user
wants to use the public API, they first must generate or retrieve an API key using the web portal. Then they can 
make calls to the public API with their API key value in the X-Api-Key header for the request. This key will be 
used to authenticate the user making the request and then to authorize any action taken as a result of the 
endpoint being called. 

In the sections below, learn more about API key generation and use.

---

### Permissions
In order to generate an API key, a user must be a company administrator. If you are not an admin, contact the 
administrator for your company and ask them to generate or retrieve an API key for you. 

To check if you are an administrator, 
log in to the IADC ISP platform using your credentials. If prompted, select the company you believe you are an
administrator of. Once you have logged in, navigate to the homepage. On the left hand side you will find your
account information summary, including your status as a user or as a company admin.

As an admin, proceed to API key generation.

---

### API Key Generation
Once you have confirmed you are logged in to the IADC ISP portal as a company administrator, do the following to generate
or retrieve an API key.

1. From the IADC ISP portal, navigate to the API Keys page.
    * Click on the admin link in the menu on the left hand side of the screen
    * Then click API Keys
2. Generate an API key. Skip this step if you have already generated one.
    * On the API Keys page, click 'Generate API Key'
    * If you have already generated an API key, the generate button will not appear and you can move to the 
    next step
3. Copy the API key.
    * Once your API key has been generated, you can copy it from the API Keys page

The API key you have generated and copied can now be used to access the public API. 

**Note:** This API key will give any
request made with it the same permissions as your administrator account. Be sure to treat this key with the 
same level of security as your username and password. 

---

### Using an API Key
After generating and retrieving an API key, it can be used to access the IADC ISP public API. There are two ways
to use your API key: by providing the API key as the value for a X-Api-Key header or by using basic authentication
and providing the API key as either the username or password. In this section, we will detail both methods.

---

**X-Api-Key Header**   
The easiest way to use the API key is by including a X-Api-Key header on any HTTP requests to the API. For the 
value of the header, provide your API key. 

For example, if our API key is **isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae**, our HTTP request should have a X-Api-Key
header value as follows:   
&emsp;&emsp;**X-Api-Key: 'isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae'**

---

**Authentication Header**   
Though the X-Api-Key header is very straightforward, you may not be able to include it if you are using a tool 
that does not allow you to add custom headers. In this case, you can use basic authentication with the Authorization
header to submit your API key.

When using the Authorization header, some changes must be made to your API key before it can be submitted with your 
request.
1. Start by creating a credentials token
    1. For cases with a username and password, the token starts with a string as follows:   
&emsp;&emsp;**'username:password'** 
    2. Since we are submitting just one value, the API key will take the place of the username and the password will
    be left blank:   
&emsp;&emsp;**'apiKey:'**
    3. Then, the string is encoded with Base64. The result is the credentials token.
2. Next, the keyword 'Basic ' is prepended to the string:    
&emsp;&emsp;**'Basic \<credentials token\>'**
2. Finally, The whole string can be submitted as the value for the Authorization header   
&emsp;&emsp;**Authorization: 'Basic \<credentials token\>'**

For example, suppose our API key is **isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae**. To use it in the Authorization header
we would follow the steps:
1. Create credentials token   
    1. Construct the string    
&emsp;&emsp;**'isp_TUbabklXnNS8-h7bIs12SxnYd5K9mnLZae:'**
    2. Encode with Base64   
&emsp;&emsp;**'aXNwX1RVYmFia2xYbk5TOC1oN2JJczEyU3huWWQ1SzltbkxaYWU6'**
2. Prepend the Basic keyword   
&emsp;&emsp;**'Basic aXNwX1RVYmFia2xYbk5TOC1oN2JJczEyU3huWWQ1SzltbkxaYWU6'**
3. Use as the value for the Authorization header   
&emsp;&emsp;**Authorization: 'Basic aXNwX1RVYmFia2xYbk5TOC1oN2JJczEyU3huWWQ1SzltbkxaYWU6'**

---

**API Key Processing**   
When you make a request, the API first checks for a X-Api-Key header. If your request does not have one, then the 
API will look at the Authentication header and try to retrieve your API key. 

Once your API key has been retrieved, it will be used to authenticate your identity. This is similar to using a
username and password to log in to the web portal. Keep in mind that the account used to generate the API key 
is the identity that will be recognized.

Once authenticated, your identity will be used to authorize access to certain companies and reports. 

Where to go from here:

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* [Return to Table of Contents](#table-of-contents)
---

## JSON Data Object Structure 
In the API, JSON is used to transmit data in the bodies of requests and responses. 

When using the API, a user may need to submit data in the body of their HTTP request. To be understood by the API,
this data must be a JSON object with the expected attributes or keys. A user also needs to understand any JSON 
objects they may receive in the body of a HTTP response. 

In this portion of the documentation, we cover the expected JSON structure of data objects within the API. 

**Requests**    
Before submitting a request with a JSON object in the body, be sure to read the documentation for the endpoint you 
are calling. This way, you will ensure your object is properly formatted and contains only attributes that the endpoint
is expecting. 

**Responses**  
Some endpoints return JSON objects in the body of the reponse. Read the endpoint's documentation and the following
documentation on different object types for help understnading your response.

Below is an outline of the overall structure of monthly reports in the API. Click on each item in the
structure to find more information about the JSON structure of that object.

* [Monthly Report](#monthly-report)  
    * Operation Categories    
        * [Operation Category 1](#operation-category)    
        * [Operation Category 2](#operation-category)     
        * [...]   
        * [Operation Category N](#operation-category)     
            * Incident Types   
                * [Incident Statistic Type 1](#incident-statistic-type)   
                * [Incident Statistic Type 2](#incident-statistic-type)   
                * [...]   
                * [Incident Statistic Type N](#incident-statistic-type)  
                    * Supplemental Incident Reports  
                        * [Supplemental Incident Report 1](#supplemental-incident-report)   
                        * [Supplemental Incident Report 2](#supplemental-incident-report)   
                        * [...]   
                        * [Supplemental Incident Report N](#supplemental-incident-report)   
                            * Answers   
                                * [Answer 1](#answer)   
                                * [Answer 2](#answer)   
                                * [...]   
                                * [Answer N](#answer) 


&emsp;[Return to Table of Contents](#table-of-contents)   

---

### Monthly Report
The monthly report object consists of many fields that record all of the information pertaining to
any monthly report. This includes the company, the date, operation categories, and more.

**Fields/Attributes:**
* companyReportID - ID of the report.
* companyID - ID of the company that the report belongs to.
* reportStatusID & reportStatus - Representation of whether the report is submitted or not.
    * 10 - Draft
    * 20 - Submitted
* reportYear & reportMonth - Together represent the date of the report.
* comments - Any comments associated with the report.
* createdBy ID, Name, and UTC - Information about the creation of the report.
    * Who created it
    * When was it created
* lastUpdateBy ID, Name, and UTC - Information about the last update of the report.
    * Who updated it
    * When was it updated
* operationCategories - An array of [Operation Category](#operation-category) objects. Each object represents one
operation category for this monthly report.

**JSON:**    
&emsp;&emsp;{                                  
&emsp;&emsp;&emsp;"companyReportID": 24814,    
&emsp;&emsp;&emsp;"companyID": 786,            
&emsp;&emsp;&emsp;"reportStatusID": 10,        
&emsp;&emsp;&emsp;"reportStatus": "Draft",     
&emsp;&emsp;&emsp;"reportYear": 2023,          
&emsp;&emsp;&emsp;"reportMonth": 9,            
&emsp;&emsp;&emsp;"comments": "",              
&emsp;&emsp;&emsp;"createdByID": null,         
&emsp;&emsp;&emsp;"createdByName": null,       
&emsp;&emsp;&emsp;"createdTimeUTC": null,      
&emsp;&emsp;&emsp;"lastUpdateByID": null,      
&emsp;&emsp;&emsp;"lastUpdateByName": null,    
&emsp;&emsp;&emsp;"lastUpdateTimeUTC": null,   
&emsp;&emsp;&emsp;"operationCategories": [    
&emsp;&emsp;&emsp;&emsp;&emsp;array of [Operation Category](#operation-category) objects    
&emsp;&emsp;&emsp;]   
&emsp;&emsp;}   


&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overall Object Structure](#json-data-object-structure)

---

### Operation Category
Each operation category that a monthly report has is represented by an operation category object.
The operation categories record the number of hours worked for each category as well as any SIRs.

**Fields/Attributes:**
* operationCategoryID & operationCategory - Represent the operation category type. Read more about how the operation
categories are represented at [Operation Categories](#operation-categories).
* hoursWorked - integer value representing the number of hours worked for that operation category.
* incidentTypes - An array of [Incident Statistic Type](#incident-statistic-type) objects, each with some number of SIRs. 
    * The SIRs for each operation category are sorted by statistic type. 
    * This array represents the sorted SIRs. 
    * Each object in the array is a single category or statistic type of incident.

**JSON:**   
&emsp;&emsp;{                                                               
&emsp;&emsp;&emsp;"operationCategoryID": 1,                                 
&emsp;&emsp;&emsp;"operationCategory": "US - Land",                         
&emsp;&emsp;&emsp;"hoursWorked": 0,                                         
&emsp;&emsp;&emsp;"incidentTypes": [                                        
&emsp;&emsp;&emsp;&emsp;&emsp;array of [Incident Statistic Type](#incident-statistic-type) objects    
&emsp;&emsp;&emsp;]                                                         
&emsp;&emsp;}   


&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overall Object Structure](#json-data-object-structure)

---

### Incident Statistic Type
The incident statistic type objects each represent one of the statistic types that an incident can 
be. Each operation category has a list of incident statistic types that in turn have a list of SIRs
for that category and type. In this way, the SIRs for any operation category are sorted by statistic
type.

**Fields/Attributes:**
* incidentStatistic TypeID, Type, and Abbreviation - Representation of the statistic type of the 
incident. Read more about how the types are represented at [Incident Statistic Types](#incident-statistic-types).   
* quantity - The number of incidents reported of this statistic type for this operation category and 
month.
* supplementalIncidentReports - An array of [Supplemental Incident Report (SIR)](#supplemental-incident-report) 
objects. Each item in the array is one SIR that has been created.

**JSON:**                                                                             
&emsp;&emsp;{                                                                     
&emsp;&emsp;&emsp;"incidentStatisticTypeID": 1,                                   
&emsp;&emsp;&emsp;"incidentStatisticType": "Medical Treatment",                 
&emsp;&emsp;&emsp;"incidentStatisticAbbreviation": "MTO",                         
&emsp;&emsp;&emsp;"quantity": 5,                                                  
&emsp;&emsp;&emsp;"supplementalIncidentReports": [                                
&emsp;&emsp;&emsp;&emsp;&emsp;array of [Supplemental Incident Report](#supplemental-incident-report) objects     
&emsp;&emsp;&emsp;]                                                               
&emsp;&emsp;}   


&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overall Object Structure](#json-data-object-structure)

---


### Supplemental Incident Report
Each incident is reported to IADC through a Supplemental Incident Report (SIR). The SIR contains
all the information about the incident, including the operation category, incident statistic type,
and the answers to [Incident Questions](#incident-questions-and-answers).

**Fields/Attributes:**
* sirid - ID of the SIR.
* operationCategoryID - ID of the operation category type. Read more about how the operation
categories are represented at [Operation Categories](#operation-categories).
* incidentStatisticTypeID - ID of the statistic type of the incident. Read more about how the types are 
represented at [Incident Statistic Types](#incident-statistic-types).  
* incidentDayNotReported - Boolean value representing whether the day the incident occured was reported
or not.
    * true - incident day was **NOT** reported
    * false - incident say **WAS** reported
* incidentDate - Date value. Meaning changes based on incidentDayNotReported value.
    * incidentDayNotReported = true - incidentDate is set to the first of the month
    * incidentDayNotReported = false - incidentDate is set to the date of the incident
* isSIF - Boolean representation of if the incident is a serious injury or fatality(SIF) or not.
* sifComments - Optional comments about the SIF status.
* rigNameNumber - Optional string representation of the rigNameNumber.
* answers - An array of [Answer](#answer) objects. Each object in the array represents an answer to one of 
the SIR [Incident Questions](#incident-questions-and-answers). This array may have no answers, a subset of the 
required answers, or all of the required answers.

**JSON:**                                                                      
&emsp;&emsp;{                                                              
&emsp;&emsp;&emsp;"sirid": 61130,                                          
&emsp;&emsp;&emsp;"operationCategoryID": 1,                                
&emsp;&emsp;&emsp;"incidentStatisticTypeID": 2,                            
&emsp;&emsp;&emsp;"incidentDayNotReported": false,                         
&emsp;&emsp;&emsp;"incidentDate": "2023-08-15T00:00:00",                   
&emsp;&emsp;&emsp;"isSIF": null,                                           
&emsp;&emsp;&emsp;"sifComments": "Optional comment about SIF status",      
&emsp;&emsp;&emsp;"rigNameNumber": "Optional rigNameNumber string",        
&emsp;&emsp;&emsp;"answers": [                                             
&emsp;&emsp;&emsp;&emsp;&emsp;array of [Answer](#answer) objects                    
&emsp;&emsp;&emsp;]                                                        
&emsp;&emsp;} 


&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overall Object Structure](#json-data-object-structure)

---


### Answer
An answer is a response to one of the SIR [Incident Questions](#incident-questions-and-answers).
Each answer has a question and an option. The optionID for an answer must be a valid response for
the question represented by the questionID. Before an SIR can be submitted, it must have answers 
for all the required questions. Find more information about required questions as well as how questions
and answers are represented at [Incident Questions](#incident-questions-and-answers).

**Fields/Attributes:**
* questionID - ID of the question being answered.
* optionID & optionText - Representation of the option chosen as the answer to the question.

**JSON:**                                                         
&emsp;&emsp;{                                                  
&emsp;&emsp;&emsp;"questionID": 6,                             
&emsp;&emsp;&emsp;"optionID": 102,                             
&emsp;&emsp;&emsp;"optionText": "Material Handling Manual"     
&emsp;&emsp;}   


&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overall Object Structure](#json-data-object-structure)

---

## Lookup Values
This section will cover lookup values. Some values used for the IADC ISP are given ID values that make
them easier to store. For example, the questions that must be answered for each SIR each have a question ID. 

A user may need to look up the options for a particular field and their corresponding IDs in order to submit a 
request to the API. A user may also need to decipher the IDs returned to them from a request. This section of 
the IADC ISP API documentation lists and details the fields and options where IDs are used to represent longer
values.

### Incident Questions and Answers
In order for a SIR to be considered complete, it must have a valid answer for each of the required SIR questions. 

The required questions are represented by a questionID. Possible answers are represented by an optionID.

Both required questions and valid answers for each question can be retrieved by using the 
[**Get Incident Questions and Answers**](#get-incident-questions-and-answers) endpoint. 

A call to the endpoint will return a list of required questions. Each question will have a questionID and a 
description of the question. Each question will also have a list of options that are valid answers to the question.
These options will have an optionID and a description of the option.

---
### Operation Categories
Each monthly report has a set of operation categories, each with a number of hours worked. Each of these operation
categories are represented by an operationCategoryID.

These operationCategoryIDs and their associated values can be retrieved by using the [**Get Operation 
Categories**](#get-operation-categories) endpoint.

A call to this endpoint returns a list of operation categories, each with an operationCategoryID and a description.

---
### Incident Statistic Types
Each SIR has an incident stistic type represented by an incidentStatisticTypeID.

These incident statistic types can be retrieved using the [Get Incident Statistic Types](#get-incident-statistic-types)
API endpoint.

A call to this endpoint returns a list of incident statistic types, each with an incidentStatisticTypeID, a name, 
and an abbreviation.


Where to go from here:

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* For an overview of API keys and authentication, visit the [Authentication](#authentication) portion of this documentation.

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* [Return to Table of Contents](#table-of-contents)
---

## Endpoints
### Company
#### Get All Companies
Returns all companies that the API key owner is allowed to access, along with their roles for each company.

**Method and Path** - GET /Companies

**URL** - https://isp.iadc.org/publicapi/Companies

**Route Parameters** - None

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: JSON array of companies
        * Each object in the array represents a company
        * Each company has:
            * participantCompanyID - ID of the company
            * participantCompanyName - Name of the company
            * role - role or access level for the user
            * userID - ID of the user
    * Example response body:   
        [   
            &emsp;{   
            &emsp;&emsp;"participantCompanyID": 123,   
            &emsp;&emsp;"participantCompanyName": "Example Drilling Co.",   
            &emsp;&emsp;"role": "ParticipantCompanyAdmin",   
            &emsp;&emsp;"userID": 2   
            &emsp;},    
            &emsp;{   
            &emsp;&emsp;"participantCompanyID": 321,   
            &emsp;&emsp;"participantCompanyName": "Notreal Drilling",   
            &emsp;&emsp;"role": "ParticipantCompanyUser",   
            &emsp;&emsp;"userID": 2   
            &emsp;}    
        ] 

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve participant company access list.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### Monthly Reports

#### Get All Monthly Reports
Returns a list of all monthly reports for the specified company.

Note: Ensure the account associated with the API key you use has read accesss for the specified company.

**Method and Path** - GET /Company/*companyID*/Report

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report

**Route Parameters**   
* *companyID* - ID value of the company you want to retrieve monthly reports for
    * Can be found using the [Get All Companies](#get-all-companies) endpoint

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**
* 200: Ok
    * Body: JSON array of monthly reports
        * Read [Monthly Report](#monthly-report) for more information about JSON formatted monthly reports.
        <!--* For an example response body, visit the Swagger documentation.-->

* 400: Bad Request - Missing/invalid values
    * No reports exist for this company.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to this
    company.
    

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Get a Specific Monthly Report
Returns a single monthly report according to the reportID provided in the route.

Note: Ensure the account associated with the API key you use has read accesss for the specified company.

**Method and Path** - GET /Company/*companyID*/Report/*reportID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportID*

**Route Parameters**   
* *companyID* - ID value of the company that owns the report you want to retrieve
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportID* - ID of the monthly report you would like to access
    * Can be found using the [Get All Monthly Reports](#get-all-monthly-reports) endpoint.

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**
* 200: Ok
    * Body: JSON monthly report.
        * Read [Monthly Report](#monthly-report) for more information about JSON formatted monthly reports.
        <!-- * For an example response body, visit the Swagger documentation. -->

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve report.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to this
    company.
    * Report does not belong to the companyID specified in the request.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Add a New Monthly Report
initializes a new monthly report according to the companyID and reportMonth.

This endpoint generates a new monthly report outline that has some default operation categories but is largely blank.
After creation, you can view the report with its default values by using the reportID from the body of the 
reponse and the [Get a Specific Monthly Report](#get-specific-monthly-report) endpoint.

To add or update values, use the following endpoints:
* [Create or Update an Operation Category](#create-or-update-an-operation-category) to update the hours worked for
  a new or already existing operation category.
* [Create New SIR](#create-new-sir) to add SIRs to your monthly report

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - POST /Company/*companyID*/Report/*reportMonth*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*

**Route Parameters**   
* *companyID* - ID value of the company you want to add a monthly report to
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the new monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: *reportID* of the newly created monthly report
    * Example response body:   
    &emsp;12456

* 400: Bad Request - Missing/invalid values
    * Failed to create monthly report.
    * Date provided is invalid.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Submit an Existing Monthly Report
Validates report for submission and then changes status of report to submitted.

In order to submit a monthly report:
* All operation categories with corresponding SIRs must have a non-zero hours worked value. 
* All SIRs must have a valid answer for each incident question.
    * Read the [Incident Questions and Answers](#incident-questions-and-answers) section for more information.

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - PUT /Company/*companyID*/Report/*reportMonth*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*

**Route Parameters**   
* *companyID* - ID value of the company that owns the monthly report you want to submit
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the new monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**   
* 200: Ok
    * Body: *reportID* of the submitted monthly report
    * Example response body:
    &emsp;12456

* 400: Bad Request - Missing/invalid values
    * Failed to update report status.
    * Date provided is invalid.
    * No monthly report exists for the provided company and date.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Delete Monthly Report
Deletes the monthly report specified by the companyID and reportMonth.

Deleting a monthly report also deletes any operation categories, hours worked, and SIRs associated with that
report.

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - DELETE /Company/*companyID*/Report/*reportMonth*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*

**Route Parameters**   
* *companyID* - ID value of the company you want to retrieve reports for
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the new monthly report in 'MMYYYY' format 
    * Date must be a current or past month of the currently active year.

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**    
* 200: Ok
    * Body: Empty

* 400: Bad Request - Missing/invalid values
    * Failed to delete report.
    * No monthly report exists with that ID.
    * Date provided is invalid.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company. 
    
&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### Operation Category Endpoints

#### Get Hours for an Operation Category 
Returns the hours worked for the specified operation category.

Note: Ensure the account associated with the API key you use has read accesss for the specified company.

**Method and Path** - GET /Company/*companyID*/Report/*reportMonth*/OpCategoy/*operationCategoryID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*/OpCategoy/*operationCategoryID*

**Route Parameters**    
* *companyID* - ID value of the company you want to retrieve reports for
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the new monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.
* *operationCategoryID* - ID corresponding to the requested operation category hours
    * Can be found using the [Get Operation Categories](#get-operation-categories) endpoint or in the 
    [Operation Categories](#operation-categories) portion of this documentation

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**    
* 200: Ok
    * Body: *hoursWorked*, an integer value representing the number of hours worked for that operation category
    * Example response body:
    &emsp;500

* 400: Bad Request - Missing/invalid values
    * Invalid date.
    * No operation reported for this combination of company, month, and operation category.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have read access 
    for this company.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Create or Update an Operation Category
Either updates the hours worked for an already existing operation category or creates a new operation 
category and then updates the hours worked.

1. First, if a monthly report for the specified company and month does not already exist, it is created.
2. Then, if the specified operation category does not already exist for the monthly report, the operation 
category is created.
3. Finally, the hours worked for the specified operation category is set to the integer value provided.
    * Note: This call does **NOT** *add* the provided hours worked value to the existing value. Instead, the 
    existing value is *overwritten* or *replaced* by the provided value.

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - POST /Company/*companyID*/Report/*reportMonth*/OpCategory/*operationCategoryID*/*hoursWorked*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*/OpCategory/*operationCategoryID*/*hoursWorked*

**Route Parameters**    
* *companyID* - ID value of the company you want to create or update the operation categories of
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.
* *operationCategoryID* - ID of the operation category you want to create or update
    * Can be found using the [Get Operation Categories](#get-operation-categories) endpoint or in the 
    [Operation Categories](#operation-categories) portion of this documentation
* *hoursWorked* - integer representation of the number of hours worked

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses** 
* 200: Ok
    * Body: Empty
    * Use [Get Hours for an Operation Category](#get-hours-for-an-operation-category) to view or confirm
    reported hours worked.

* 400: Bad Request - Missing/invalid values
    * Failed to create or update operation category hours.
    * Invalid date.
    * Operation category created but failed to set or update hours worked.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company.  

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### SIRs

#### Get a Specific SIR
Returns the SIR specified by the sirID in the route.

Note: Ensure the account associated with the API key you use has read accesss for the specified company.

**Method and Path** - GET /Company/*companyID*/Report/SIR/*sirID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/SIR/*sirID*

**Route Parameters**   
* *companyID* - ID value of the company that the requested SIR belongs to
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *sirID* - ID of the SIR you wish to retrieve
    * Can be found using the [Get All Monthly Reports](#get-all-monthly-reports) endpoint

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.
     
**Responses**   
* 200: Ok
    * Body: JSON formatted SIR
        * Read [Supplemental Incident Report](#supplemental-incident-report) for more information about JSON formatted SIRs.
       <!-- * For an example response body, visit the Swagger documentation. -->

* 400: Bad Request - Missing/invalid values
    * No SIR exists with this ID.
    * No SIR exists with this ID in this company.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have read access 
    for this company. 

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Create New SIR
Creates a new SIR for the provided month, operation category, and incident statistic type. SIR is updated to 
include information from the body of the request, if provided.

1. First, if a monthly report for the specified company and month does not already exist, it is created.
2. Then, if the specified operation category does not already exist for the monthly report, the operation 
category is created.
3. Next, a SIR is created with the specified incident statistic type.
4. Finally, if a body is provided with the request, the SIR is updated to include the information provided in
    the body.
    
Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - POST /Company/*companyID*/Report/*reportMonth*/OpCategory/*operationCategoryID*/SIR/*incidentStatisticTypeID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*/OpCategory/*operationCategoryID*/SIR/*incidentStatisticTypeID*

**Route Parameters**    
* *companyID* - ID value of the company you want to create a new SIR for
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.
* *operationCategoryID* - ID of the operation category you want to create or update
    * Can be found using the [Get Operation Categories](#get-operation-categories) endpoint or in the 
    [Operation Categories](#operation-categories) portion of this documentation
* *incidentStatisticTypeID* - ID of the incident statistic type of the SIR
    * Can be found using the [Get Incident Statistic Types](#get-incident-statistic-types) endpoint 
    * Read more in the [Incident Statistic Types](#incident-statistic-types) portion of this documentation

**Query Parameters** - None

**Body** - Optional
* JSON object representing SIR information
    * If the request has a correctly-formatted body, the SIR that is created is updated with the values provided
    in the body.
    * If the request does not have a body or the body is incorrectly formatted, the SIR is still created but it
    is not updated with the values from the body.
    * When submitting SIR information in the body of the request, only include attributes for the values you would 
    like to update.
* Formatting for JSON object
    * Read [Supplemental Incident Report](#supplemental-incident-report) for an overview of all fields/attributes for a JSON formatted SIR.
    * Only some SIR attributes can be updated by including them in the body of a request.
    * List of possible attributes to include:
        * incidentDate - optional, the date that the incident occurred, must be the same month and year provided in
        the route
        * isSIF - optional, boolean value 
        * rigNameNumber - optional, string 
        * comments - optional, string containing any comments
        * answers - optional, array of objects representing incident questions and their answers
            * Can provide all required answers, a subset of the required answers, or no answers at all
            * Each answer should have these attributes:
                * questionID - required for each answer provided, number representing the question being answered
                * optionID - required for each answer provided, number representing the answer to the question
            * For more information about questions and answers, read here: [Incident Questions and Answers](#incident-questions-and-answers)
    * Attributes not on this list will be ignored or may cause errors when included in the JSON object 
* Example request body:    
&emsp;{   
&emsp;&emsp;"incidentDate": "2022-08-15",                
&emsp;&emsp;"isSIF": "true",                               
&emsp;&emsp;"rigNameNumber": "rigNameNumber string",     
&emsp;&emsp;"comments": "comment string",                
&emsp;&emsp;"answers": [                                 
&emsp;&emsp;&emsp;{                                          
&emsp;&emsp;&emsp;  &emsp;"questionID": 2,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 10                           
&emsp;&emsp;&emsp;},&emsp;                                         
&emsp;&emsp;&emsp;{ &emsp;                                         
&emsp;&emsp;&emsp;  &emsp;"questionID": 5,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 69                           
&emsp;&emsp;&emsp;},&emsp;                                         
&emsp;&emsp;&emsp;{ &emsp;                                         
&emsp;&emsp;&emsp;  &emsp;"questionID": 6,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 102                          
&emsp;&emsp;&emsp;}                                          
&emsp;&emsp;]                                            
&emsp;}                                                  


**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**  
* 201: Ok
    * Body: JSON formatted SIR
        * Read [Supplemental Incident Report](#supplemental-incident-report) for more information about JSON formatted SIRs.
       <!-- * For an example response body, visit the Swagger documentation.-->

* 400: Bad Request - Missing/invalid values
    * Failed to create SIR.
    * Invalid date.
        * SIR Created. Failed to update with SIR fields provided in body of request.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company.  

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Update SIR
Updates the specified SIR with the information included in the body of the request.

Note: The company, month, operation category, and incident statistic type cannot be changed for existing SIRs.
If one of these values needs to be edited, please delete the existing SIR and then create a new one with the 
correct values.

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - PUT /Company/*companyID*/Report/*reportMonth*/SIR/*sirID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/*reportMonth*/SIR/*sirID*

**Route Parameters**    
* *companyID* - ID value of the company who owns the SIR you want to update
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *reportMonth* - Month of the monthly report in 'MMYYYY' format
    * Date must be a current or past month of the currently active year.
* *sirID* - ID of the SIR you want to update
    * Can be found using the [Get All Monthly Reports](#get-all-monthly-reports) endpoint

**Query Parameters** - None

**Body** - Required, JSON formatted SIR
* JSON object representing SIR information
    * When submitting SIR information in the body of the request, only include attributes for the values you would 
    like to update.
* Formatting for JSON object
    * Read [Supplemental Incident Report](#supplemental-incident-report) for an overview of all fields/attributes for a JSON formatted SIR.
    * Only some SIR attributes can be updated by including them in the body of a request.
    * List of possible attributes to include:
        * incidentDate - optional, the date that the incident occurred, must be the same month and year provided in
        the route
        * isSIF - optional, boolean value 
        * rigNameNumber - optional, string 
        * comments - optional, string containing any comments
        * answers - optional, array of objects representing incident questions and their answers
            * Can provide all required answers, a subset of the required answers, or no answers at all
            * Each answer should have these attributes:
                * questionID - required for each answer provided, number representing the question being answered
                * optionID - required for each answer provided, number representing the answer to the question
            * For more information about questions and answers, read here: [Incident Questions and Answers](#incident-questions-and-answers)
    * Attributes not on this list will be ignored or may cause errors when included in the JSON object 
* Example request body:    
&emsp;{   
&emsp;&emsp;"incidentDate": "2022-08-15",                
&emsp;&emsp;"isSIF": "true",                               
&emsp;&emsp;"rigNameNumber": "rigNameNumber string",     
&emsp;&emsp;"comments": "comment string",                
&emsp;&emsp;"answers": [                                 
&emsp;&emsp;&emsp;{                                          
&emsp;&emsp;&emsp;  &emsp;"questionID": 2,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 10                           
&emsp;&emsp;&emsp;},&emsp;                                         
&emsp;&emsp;&emsp;{ &emsp;                                         
&emsp;&emsp;&emsp;  &emsp;"questionID": 5,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 69                           
&emsp;&emsp;&emsp;},&emsp;                                         
&emsp;&emsp;&emsp;{ &emsp;                                         
&emsp;&emsp;&emsp;  &emsp;"questionID": 6,                         
&emsp;&emsp;&emsp;  &emsp;"optionID": 102                          
&emsp;&emsp;&emsp;}                                          
&emsp;&emsp;]                                            
&emsp;}  

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**  
* 201: Ok
    * Body: JSON formatted SIR
        * Read [Supplemental Incident Report](#supplemental-incident-report) for more information about JSON formatted SIRs.
       <!-- * For an example response body, visit the Swagger documentation.-->

* 400: Bad Request - Missing/invalid values
    * Failed to update SIR.
    * No SIR exists with this ID.
    * No SIR exists with this ID in this company.
    * Invalid date.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company.   
    
&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Delete SIR
Deletes the SIR specified in the route. 

Note: Ensure the account associated with the API key you use has edit accesss for the specified company.

**Method and Path** - DELETE /Company/*companyID*/Report/SIR/*sirID*

**URL** - https://isp.iadc.org/publicapi/Company/*companyID*/Report/SIR/*sirID*

**Route Parameters**   
* *companyID* - ID value of the company who owns the SIR you want to delete
    * Can be found using the [Get All Companies](#get-all-companies) endpoint
* *sirID* - ID of the SIR you want to delete
    * Can be found using the [Get All Monthly Reports](#get-all-monthly-reports) endpoint

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**    
* 200: Ok
    * Body: Empty

* 400: Bad Request - Missing/invalid values
    * Failed to delete SIR.
    * No SIR exists with this ID.
    * No SIR exists with this ID in this company.
    * Invalid date.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have edit access 
    for this company. 

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### Lookups

#### Get Incident Questions and Answers
Returns all incident questions that must be answered for each SIR. Also provides the valid answer options for 
each question.

**Method and Path** - GET /Report/SIR/IncidentQuestions

**URL** - https://isp.iadc.org/publicapi/Report/SIR/IncidentQuestions

**Route Parameters**  - None

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**   
* 200: Ok
    * Body: List of all required incident questions, each with a questionID, a question, and a list of valid
    options. Each option in the list has an optionID and an optionText field. 
        * Find more information at [Incident Questions and Answers](#incident-questions-and-answers)
    * Example response body:   
&emsp;[                                                                                                   
&emsp;&emsp;{                                                                                             
&emsp;&emsp;&emsp;"questionID": 2,                                                                        
&emsp;&emsp;&emsp;"question": "Occupation Type",                                                                          
&emsp;&emsp;&emsp;"options": [                                                                            
&emsp;&emsp;&emsp;&emsp;{                                                                                 
&emsp;&emsp;&emsp;&emsp;&emsp;"optionID": 9,                                                              
&emsp;&emsp;&emsp;&emsp;&emsp;"optionText": "Roustabout (Lease Hand)"                                                                 
&emsp;&emsp;&emsp;&emsp;},                                                                                
&emsp;&emsp;&emsp;&emsp;{                                                                                 
&emsp;&emsp;&emsp;&emsp;&emsp;"optionID": 10,                                                             
&emsp;&emsp;&emsp;&emsp;&emsp;"optionText": "Floorman"                                                             
&emsp;&emsp;&emsp;&emsp;}                                                                                 
&emsp;&emsp;&emsp;]                                                                                       
&emsp;&emsp;},                                                                                            
&emsp;&emsp;{                                                                                             
&emsp;&emsp;&emsp;"questionID": 3,                                                                        
&emsp;&emsp;&emsp;"question": "Body Parts",                                                                           
&emsp;&emsp;&emsp;"options": [                                                                            
&emsp;&emsp;&emsp;&emsp;{                                                                                 
&emsp;&emsp;&emsp;&emsp;&emsp;"optionID": 31,                                                             
&emsp;&emsp;&emsp;&emsp;&emsp;"optionText": "Eyes (eyelid)"                                                               
&emsp;&emsp;&emsp;&emsp;},                                                                                
&emsp;&emsp;&emsp;&emsp;{                                                                                 
&emsp;&emsp;&emsp;&emsp;&emsp;"optionID": 32,                                                             
&emsp;&emsp;&emsp;&emsp;&emsp;"optionText": "Head (face, nose, mouth, chin, jaw, teeth, eyebrow)"                                                             
&emsp;&emsp;&emsp;&emsp;},                                                                                
&emsp;&emsp;&emsp;&emsp;{                                                                                 
&emsp;&emsp;&emsp;&emsp;&emsp;"optionID": 33,                                                             
&emsp;&emsp;&emsp;&emsp;&emsp;"optionText": "Back"                                                               
&emsp;&emsp;&emsp;&emsp;}                                                                                 
&emsp;&emsp;&emsp;]                                                                                       
&emsp;&emsp;}                                                                                             
&emsp;]                                                                                                   

* 400: Bad Request - Failed to retrieve incident questions and options

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.
    
&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Get Operation Categories
Returns all possible valid operation category values. 

**Method and Path** - GET /Report/OperationCategories

**URL** - https://isp.iadc.org/publicapi/Report/OperationCategories

**Route Parameters**  - None

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**    
* 200: Ok
    * Body: List of possible operation categories, each with an operationCategoryID and an operationCategoryName.
        * Find more information at [Operation Categories](#operation-categories)
    * Example response body:

&emsp;[                                                           
&emsp;&emsp;{                                                     
&emsp;&emsp;  &emsp;"operationCategoryID": 1,                     
&emsp;&emsp;  &emsp;"operationCategoryName": "US - Land"                               
&emsp;&emsp;},&emsp;                                              
&emsp;&emsp;{ &emsp;                                              
&emsp;&emsp;  &emsp;"operationCategoryID": 2,                     
&emsp;&emsp;  &emsp;"operationCategoryName": "US - Water"                                 
&emsp;&emsp;},&emsp;                                              
&emsp;&emsp;{ &emsp;                                              
&emsp;&emsp;  &emsp;"operationCategoryID": 3,                     
&emsp;&emsp;  &emsp;"operationCategoryName": "Canada - Land"                                 
&emsp;&emsp;}                                                     
&emsp;]                                                           

* 400: Bad Request - Failed to retrieve operation category options.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Get Incident Statistic Types
Returns all valid incident statistic type values. 

**Method and Path** - GET /Report/IncidentStatisticTypes

**URL** - https://isp.iadc.org/publicapi/Report/IncidentStatisticTypes

**Route Parameters**  - None

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**    
* 200: Ok
    * Body: List of possible incident statistic types, each with an incidentStatisticTypeID, an 
    incidentStatisticTypeName, and an abbreviation.
        * Find more information at [Incident Statistic Types](#incident-statistic-types)
    * Example response body:
&emsp;[                                                                  
&emsp;&emsp;{                                                            
&emsp;&emsp;  &emsp;"incidentStatisticTypeID": 1,                        
&emsp;&emsp;  &emsp;"incidentStatisticTypeName": "Medical Treatment",    
&emsp;&emsp;  &emsp;"abbreviation": "MTO"                                
&emsp;&emsp;},&emsp;                                                     
&emsp;&emsp;{ &emsp;                                                     
&emsp;&emsp;  &emsp;"incidentStatisticTypeID": 2,                        
&emsp;&emsp;  &emsp;"incidentStatisticTypeName": "Restricted Work",      
&emsp;&emsp;  &emsp;"abbreviation": "RWC"                                
&emsp;&emsp;},&emsp;                                                     
&emsp;&emsp;{ &emsp;                                                     
&emsp;&emsp;  &emsp;"incidentStatisticTypeID": 3,                        
&emsp;&emsp;  &emsp;"incidentStatisticTypeName": "Lost Time Incident",   
&emsp;&emsp;  &emsp;"abbreviation": "LTI"                                
&emsp;&emsp;},&emsp;                                                     
&emsp;&emsp;{ &emsp;                                                     
&emsp;&emsp;  &emsp;"incidentStatisticTypeID": 4,                        
&emsp;&emsp;  &emsp;"incidentStatisticTypeName": "Fatality",             
&emsp;&emsp;  &emsp;"abbreviation": "FTL"                                
&emsp;&emsp;}                                                            
&emsp;]

* 400: Bad Request - Failed to retrieve incident statistic type options.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---

Last updated: 9/28/2023
