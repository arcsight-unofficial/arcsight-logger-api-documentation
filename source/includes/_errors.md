# HTTP Status Codes

The ArcSight Logger uses the following status codes:


HTTP Code | Meaning
---------- | -------
200 | Request was completed successfully.
204 | Request was completed successfully, though no content was returned.
400 | Your request format is incorrect or missing parameters.
401 | User does not have access or the sessionID is not correct.
404 | The ID of the search you are trying to retrieve was not found
500 | Internal Server error, for more information see the returned stacktrace