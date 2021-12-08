---
includes:
- errors
---

![Campaign api](images/favico) ***ViziBit***
# Campaign API integration

# Introduction

> Following examples will use **authorization as query parameter**.

In order to use requests from this documentation, it is necessary to configure an environment defined with parameters such as gateway host and authorization key.

Here's an example of API structure for an endpoint:

### HTTP Request

`GET {{GATEWAYHOST}}/v/1/campaign`

In order to test requests in a test environment, you can find demonstrational gateway host in the table below. The required authorization key must be requested from Vizibit company. Once given, the authorization key should be written in a header with or without **Bearer** key word or as a **query** parameter (authorization_key) in the testing request.

### Query Parameters

Parameter | Value
--------- | -----------
**GATEWAYHOST** | https://campaigns-test.signator.hr
**authorization_key** | Your authorization key. Add in a header of request or as **query** parameter.


# Campaign API Calls

![Campaign api](images/Campaign_diagram.png)

## Get Campaigns

> If successful the above command returns JSON structured like this:

```json
{
  "page": 1,
  "perPage": 12,
  "pages": 4,
  "total": 37,
  "count": 12,
  "type": "Campaign",
  "results": [
    {
      "Id": "Campaign_example_id",
      "StartedAt": 1636636239,
      "ValidUntil": 1639228239,
      "Name": "New campaign",
      "TransferTemplate": {
        "EN": {
          "Subject": "Email subject",
          "Content": "Text sent in email"
        },
        "DE": {
          "Subject": "...",
          "Content": "..."
        },
        "IT": {
          "Subject": "...",
          "Content": "..."
        },
        "FR": {
          "Subject": "...",
          "Content": "..."
        }
      },
      "Status": "PENDING",
      "Participants": [
          {
            "Id": "Participant_example_id_1",
            "CampaignId": "Campaign_example_id",
            "Status": "CREATED",
            "TransferLanguage": "EN",
            "TransferType": "EMAIL",
            "TransferIdentifier": "example@vizibit.eu",
            "ParticipantData": {
              "mobilePhone": "example@vizibit.eu"
            },
            "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_1&language=EN"
          }
      ],
      "ParticipantDataRequiredKeys": [],
      "DeliveryAddresses": ["example@vizibit.eu"]
    }
  ]
}
    
```

This endpoint retrieves all campaigns requested by parameters in query.

### HTTP Request

`GET {{GATEWAYHOST}}/v/1/campaign`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.
page | 1 | Page number whose campaigns will be returned.
perPage | 12 | Maximal number of campaigns returned in each page.



## Get a Specific Campaign

> If successful the above command returns JSON structured like this:

```json
{
  "Id": "Campaign_example_id",
  "StartedAt": 1634821121,
  "ValidUntil": 1637413121,
  "Name": "Test campaign",
  "TransferTemplate": {
    "EN": {
      "Subject": "Email subject",
      "Content": "Text sent in email"
    },
    "DE": {
      "Subject": "...",
      "Content": "..."
    },
    "IT": {
      "Subject": "...",
      "Content": "..."
    },
    "FR": {
      "Subject": "...",
      "Content": "..."
    }
  },
  "Status": "DRAFT",
  "Participants": [
    {
      "Id": "Participant_example_id_1",
      "CampaignId": "Campaign_example_id",
      "Status": "CREATED",
      "TransferLanguage": "EN",
      "TransferType": "EMAIL",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "example@vizibit.eu"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_1&language=EN"
    },
    {
      "Id": "Participant_example_id_2",
      "CampaignId": "Campaign_example_id",
      "Status": "CREATED",
      "TransferLanguage": "EN",
      "TransferType": "SMS",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "+29910236548"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_2&language=EN"
    }
  ],
  "ParticipantDataRequiredKeys": [],
  "DeliveryAddresses": ["example@vizibit.eu"]
}
```

This endpoint retrieves a specific campaign.

`GET {{GATEWAYHOST}}/v/1/campaign/{id}`

### Route Values
Parameter | Default | Description
--------- | ------- | -----------
id |  | Id of the campaign requested in call.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.

## Create Campaign

> JSON body request example:

```json
{
  "name": "Test campaign",
  "transferTemplate": {
    "EN": {
      "Subject":"Campaign Test Subject",
      "Content":"Campaign Test Content"
    }
  },
  "Participants": [
    {
      "Status": "CREATED",
      "TransferLanguage": "EN",
      "TransferType": "EMAIL",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "example@vizibit.eu"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_1&language=EN"
    },
    {
      "Status": "CREATED",
      "TransferLanguage": "EN",
      "TransferType": "SMS",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "+29910236548"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_2&language=EN"
    }],
  "status": "DRAFT"
}
```

> If successful the above command returns JSON structured like this:

```json
{
  "Id": "Campaign_example_id",
  "StartedAt": 1638798772,
  "ValidUntil": 1641390772,
  "Name": "Test campaign",
  "TransferTemplate": {
    "EN": {
      "Subject":"Campaign Test Subject",
      "Content":"Campaign Test Content"
    }
  },
  "Status": "DRAFT",
  "Participants": [
      {
        "Id": "Participant_example_id_1",
        "CampaignId": "Campaign_example_id",
        "Status": "CREATED",
        "TransferLanguage": "EN",
        "TransferType": "EMAIL",
        "TransferIdentifier": "example@vizibit.eu",
        "ParticipantData": {
          "mobilePhone": "example@vizibit.eu"
        },
        "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_1&language=EN"
      },
      {
        "Id": "Participant_example_id_2",
        "CampaignId": "Campaign_example_id",
        "Status": "CREATED",
        "TransferLanguage": "EN",
        "TransferType": "SMS",
        "TransferIdentifier": "example@vizibit.eu",
        "ParticipantData": {
          "mobilePhone": "+29910236548"
        },
        "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_2&language=EN"
      }
  ],
  "ParticipantDataRequiredKeys": [],
  "DeliveryAddresses": []
}
```

This endpoint creates new campaign filled with required parameters filled in requests body.

In section "Body input" bolded body values are required. 

### HTTP Request

`POST {{GATEWAYHOST}}/v/1/campaign`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.

### Body input

- **name** - Campaign name
- **transferTemplate** - JSON object with language codes(ISO 639-1) as key and values as objects:
    - **Subject** - Email subject
    - **Content** - Text contained in email
- **Participants** - Array of object with following parameters:
    - **TransferLanguage** - Language code(ISO 639-1) of subject and content send in email, default: EN
    - **TransferIdentifier** - Participants email
    - **TransferType** - Defines means of transmission for otp, currently implemented EMAIL and SMS
    - **ParticipantData** - Object containing data about participant
      - **mobilePhone** - Text of mobile phone number for SMS ie. email where participant gets otp
                    - Means of transmission defined in TransferType
    
    - **status** - <code>DRAFT</code> or <code>PENDING</code>:
      - </code>DRAFT</code> - user can still change campaign
      - <code>PENDING</code> - user can't change campaign because emails to participants to fill are already been sent
      - other statuses can't be defined at creation of campaign, only when created
- ParticipantDataRequiredKeys - Array of ParticipantData fields expected to be in request
- DeliveryAddresses - Email addresses where campaign changes are sent 


## Update Campaign

> JSON body request example:

```json
{
  "status": "PENDING"
}
```

> If successful the above command returns JSON structured like this:

```json
{
  "Id": "Campaign_example_id",
  "StartedAt": 1638798772,
  "ValidUntil": 1641390772,
  "Name": "Test campaign",
  "TransferTemplate": {
    "EN": {
      "Subject":"Campaign Test Subject",
      "Content":"Campaign Test Content"
    }
  },
  "Status": "PENDING",
  "Participants": [
    {
      "Id": "Participant_example_id_1",
      "CampaignId": "Campaign_example_id",
      "Status": "SEND",
      "TransferLanguage": "EN",
      "TransferType": "EMAIL",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "example@vizibit.eu"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_1&language=EN"
    },
    {
      "Id": "Participant_example_id_2",
      "CampaignId": "Campaign_example_id",
      "Status": "SEND",
      "TransferLanguage": "EN",
      "TransferType": "SMS",
      "TransferIdentifier": "example@vizibit.eu",
      "ParticipantData": {
        "mobilePhone": "+29910236548"
      },
      "EntityLink": "{{GATEWAYHOST}}/residence?cid=Campaign_example_id&pid=Participant_example_id_2&language=EN"
    }
  ],
  "ParticipantDataRequiredKeys": [],
  "DeliveryAddresses": []
}
```

Main purpose of this endpoint is to allow user to change campaigns **STATUS**.

Except changing status it can change other campaign parameters, but only in campaigns which **STATUS** is **<code>DRAFT</code>**.
It can change one or more parameters included in campaign.


### HTTP Request

`PUT {{GATEWAYHOST}}/v/1/campaign/{id}`

### Route Values
Parameter | Default | Description
--------- | ------- | -----------
id |  | Id of the campaign requested in call.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.

### Body input

- name - Campaign name
- transferTemplate - JSON object with language key and objects:
  - Subject - Email subject
  - Content - Text contained in email
    
  - status - <code>DRAFT</code>, <code>PENDING</code>, <code>ERROR</code>, <code>FINISHED</code>, <code>DELETED</code>, <code>ARCHIVED</code>, <code>TERMINATED</code>:
    - <code>DRAFT</code> - user can still change campaign
       - can change to <code>DRAFT</code>, <code>PENDING</code>, <code>DELETED</code>, <code>ERROR</code>
    - <code>PENDING</code> - user can't change campaign because emails are sent to participants
       - can change to <code>PENDING</code>, <code>ERROR</code>, <code>DELETED</code>, <code>ARCHIVED</code>, <code>FINISHED</code>, <code>TERMINATED</code>
    - <code>ERROR</code> - error accrued - final state
    - <code>FINISHED</code> - every participant filled form or the duration of the campaign has finished or campaign creator changed status
       - can change to <code>FINISHED</code>, <code>DELETED</code>, <code>ARCHIVED</code>
    - <code>ARCHIVED</code> - admin changed campaign status so it is visible only when asked for

![Campaign state machine](images/Campaign_state_machine.png)


## Update Campaign Participant

> JSON body request example:

```json
{
  "status": "COMPLETED"
}
```
> If successfully completed response is **204 No Content**

Purpose of this endpoint is to update participant **STATUS**, but only in campaigns which **STATUS** is **PENDING**

### HTTP Request

`PUT {{GATEWAYHOST}}/v/1/campaign/{id}/participant/{participant_id}`

### Route Values
Parameter | Default | Description
--------- | ------- | -----------
id |  | Id of the campaign requested in call.
participant_id | | Id of participant requested to update.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.

### Body input

 - status - new participant status
    - <code>CREATED</code> - when campaign status is still draft, can change to <code>CREATED</code> and <code>SENT</code>
    - <code>SENT</code> - when campaign admin starts campaign ie. campaign status switched to <code>PENDING</code>
        - emails are sent to participants 
        - can change to <code>READ</code>
    - <code>READ</code> - campaign participant opened link received in email, can open multiple times
        - can change to <code>READ</code>, <code>COMPLETED</code>, <code>ERROR</code>
    - <code>COMPLETED</code> - participant filled form, final state
    - <code>ERROR</code> - error occured, final state
  

![Participant state machine](images/Participant_state_machine.png)

## Get report for Campaigns

> If successfully completed returns filtered report with campaigns in requested file type.

This endpoint retrieves report about campaigns requested by parameters in query.

### HTTP Request

`GET {{GATEWAYHOST}}/v/1/campaign/report/{report_type}`

### Route Values
Parameter | Default | Description
--------- | ------- | -----------
report_type |  | Type of report, CSV or XLSX.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.
page | 1 | Page number whose campaigns will be returned.
perPage | 12 | Maximal number of campaigns returned in each page.


## Get report for Campaign Participants

> If successfully completed returns filtered report with campaign participants in requested file type.

This endpoint retrieves report about campaign participants.

### HTTP Request

`GET {{GATEWAYHOST}}/v/1/campaign/{id:guid}/report/{report_type}`

### Route Values
Parameter | Default | Description
--------- | ------- | -----------
report_type |  | Type of report, CSV or XLSX.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
**authorization_key** |  | Indicates the user and his authorities.


---



