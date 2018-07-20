# Errors

## Generic Errors

You may see any of the following HTTP error codes returned by the ProQuest Dialog API.

HTTP Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your bearer token is unspecified or invalid.
404 | Not Found -- The specified resource could not be found. Possibly an invalid thesaurus name or alert id.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

## Structured Errors

> Response

```xml
<error>
    <debugMessage>Problem encountered parsing query</debugMessage>
    <errorCode>5000</errorCode>
    <parameters>
        <param name="input">or </param>
        <param name="startIndex">5</param>
    </parameters>
</error>
```

An HTTP code of 400 (bad request) may contain either semantic or XML/structural errors.  For many semantic errors, the body of the response will contain a structured defining what is wrong in a way that could be programmatically reported back to a user more easily with some interpretation.

### Codes

Error Code | Meaning
---------- | -------
1000 | You may see this error code displayed when your bearer token is not valid.
1200 | The account identified by your bearer token does not have any active subscriptions and cannot be used.
5000 | Your MQL search could not be parsed.  Additional structured error parameters should identify the area of the query that could not be parsed.
5100 | Your MQL search contains an MQL operator that is not defined.  Additional structured error parameters should identify the area of the query that contains the invalid mnemonic operator.
5500 | You are attempting to scroll too far into the search results. We can only supprt returning the first 4000 documents of a search. offset + count <= 4000
6000 | There was an error interpreting your search.  Please check any additional structured error parameters.
6005 | There is a reference to set in the MQL query that is not supplied as a separate set in the search request.  Additional structured error parameters should identify the reference and its location.
6010 | Your MQL search contains a mnemonic that is not defined. The mnemonic and its location should be specified in the error parameters.
6015 | Your MQL search uses a mnemonic operator that is not compatible with the mnemonic on which it operates.  The operator and its location should be specified in the error parameters.
6020 | A mnemonic cannot be used in a given part of your MQL search.  The mnemonic and its location should be specified in the error parameters.
6025 | Proximity operaters (near/pre) cannot be used in a particular part of your search.  The location of the operator should be specified in the error parameters.
6100 | The given type of input cannot be used with a particular mnemonic.  Some mnemonics expect dates or numeric ranges.  The expected type of input and the mnemonic should be specified in the error parameters.
7100 | The top level database specification does not contain all of the databases used in the set references supplied.  Alternatively, you may be using a database code with the FDB mnemonic that is not part of your database selections.
7200 | You are using a database code that does not exist or is not part of your subscription.

### Schema: error

Element | Description
------- | -----------
debugMessage | A human readable hint to the problem.  This could be specific or generic.  It is not intended to fully identify the problem or be consumed by users.
errorCode | Numeric error code as listed above.
parameters | If present, a list of param elements that contain a name attribute and a value.  These describe any actual details of the semantic error.
