# Error feedback

All errors return the HTTP status code 400, unless an unforeseen situation has occurred. In that case HTTP status code is 500.

All errors are returned as **JSON**.

List of possible errors on Campaign interface

Error Code | Meaning
---------- | -------
22000 | "Field 'campaignId' missing from request"
22001 | "Field 'participantId' missing from request"
22002 | "Field 'otp' missing from request"
22003 | "No participant with requested 'campaignId' and 'participanId'"
22004 | "Field 'FormData' missing from request"
22005 | "Campaign not found"
22006 | "Campaign participant not found"
22007 | "Unable to update campaign"
22008 | "Created campaign can only be DRAFT or PENDING"
22009 | "Cannot change campaign status from 'PENDING' to 'DRAFT'"
22010 | "Cannot change campaign participant status from 'READ' to 'SENT'"
22011 | "Cannot update non PENDING campaign"
22012 | "Cannot add users with email: example@vizibit.eu"
22013 | "Participant: 'participant_1', missing some of required data keys: 'mobilePhone'"
22014 | "Request body must be defined"
22015 | "Needed at least one participant to start campaign"
22016 | "Participant language not implemented in transfer template"
22017 | "Missing information about entity"
22018 | "Needed at least one transfer template"
22019 | "Participant has already filled the campaign."
22020 | "Participant mobile phone is not defined"
22021 | "Campaign has not yet started"
22022 | "Campaign has finished"
22023 | "Not existing report type."
22024 | "Missing properties for column names."

In case of an error, the processing is interrupted and the error response is returned to the caller.
