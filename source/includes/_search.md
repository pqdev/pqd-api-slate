# Search

The search endpoint allows searching for content on the ProQuest Dialog platform by specifying an MQL query.  The search API supports multiple search options and same MQL syntax supported on the Dialog platform.  Each doc in a search response contains a Link field to the full document in XML format.

## Get search results

> Search response:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<searchResponse>
    <searchId>jjt06vm1-egdcl1</searchId>
    <result docsFound="3104">
        <doc>
            <field name="ID">
                <value>596697054</value>
            </field>
            <field name="Title">
                <value>Benzoate stimulates glutamate release from perfused rat liver</value>
            </field>
            <field name="Database">
                <value>MEDLINE®; 1946-1989</value>
            </field>
            <field name="Link">
                <value>https://api-dialog.proquest.com/v1/content/jjt06vm1-egdcl1_596697054.xml</value>
            </field>
        </doc>
        <doc>
            <field name="ID">
                <value>596624243</value>
            </field>
            <field name="Title">
                <value>Competition for antigen presentation in living cells involves exchange of peptides bound by class II MHC molecules</value>
            </field>
            <field name="Database">
                <value>MEDLINE®; 1946-1989</value>
            </field>
            <field name="Link">
                <value>https://api-dialog.proquest.com/v1/content/jjt06vm1-egdcl1_596624243.xml</value>
            </field>
        </doc>
    </result>
</searchResponse>
```

Search for content on ProQuest Dialog.

### HTTP Request

`GET /search`

### Query Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
q | - | Yes | An MQL query used to perform a search.
db | - | Yes | A comma delimited list of database codes to search (medlineprof,embase).  Your account must have authorization to use any database codes specified.
count | 20 | No | The number of documents to return in a single request.  We only support scrolling 4000 documents into search results (count + offset <= 4000).
offset | 0 | No | The number of documents to skip before returning search results.  This facilitates paging through search results without returning a large list of documents at a time. 
s1 | - | No | Should contain the MQL query for a set reference.  Any set references can be included as query parameters (s1, s2, s231, etc).

<aside class="success">
Remember — GET requests must still contain a correct Authorization header.
</aside>
