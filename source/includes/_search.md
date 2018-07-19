# Search

The search endpoint allows searching for content on the ProQuest Dialog platform by specifying an MQL query.  The search API supports multiple search options and the same MQL syntax supported on the Dialog platform.  Each doc in a search response contains a Link field to the full document in XML format.

## GET search results

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
sortOrder | pubDateDescending | No | The sort order to use in the results returned.  pubDateDescending - in descending order by publication date.  pubDateAscending - in ascending order by publication date.  relevance - in order of relevance to the query.
s1 | - | No | Should contain the MQL query for a set reference.  Any set references can be included as query parameters (s1, s2, s231, etc).
includeDuplicates | false | No | Specify whether or not to include duplicate documents in the results returned. (true/false)
includeLemmatization | false | No | Specify whether to automatically search terms with the same lemmatized stem (read|reads|reading). (true/false)
includeUsUkSpellingVariants | false | No | Specify whether to automatically search for US/UK spelling variations of the terms used in the query. (true/false)

<aside class="success">
Remember — GET requests must still contain a correct Authorization header.
</aside>

## POST search results

> Request body:

```xml
<?xml version="1.0" encoding="utf-8"?>
<searchRequest>
    <search>
        <query>ti(test) or s1</query>
        <databases>
            <database>medlineprof</database>
            <database>embase</database>
        </databases>
        <set id="1">
            <query>mesh.#("ammonium chloride")</query>
            <databases>
                <database>medlineprof</medlineprof>
            </databases>
        </set>
        <options>
            <includeLemmatization>true</includeLemmatization>
            <includeUsUkSpellingVariants>true</includeUsUkSpellingVariants>
            <includeDuplicates>true</includeDuplicates>
        </options>
    </search>
    <count>5</count>
    <offset>20</offset>
    <sortOrder>pubDateAscending</sortOrder>
</searchRequest>
```

The preferred method for accessing the search API is to make a POST request.  This bypasses the maximum URL length imposed by some servers and browsers allowing for longer queries to be used.

### HTTP Request

`POST /search`

### Schema: searchRequest

Element | Default | Required | Description
------- | ------- | -------- | -----------
search | - | Yes | The structured search for which results will be returned.
count | 20 | No | The number of documents to return in a single request.  We only support scrolling 4000 documents into search results (count + offset <= 4000)
offset | 0 | No | The number of documents to skip before returning search results.  This facilitates paging through search results without returning a large list of documents at a time.
sortOrder | pubDateDescending | No | The sort order to use in the results returned.  pubDateDescending - in descending order by publication date.  pubDateAscending - in ascending order by publication date.  relevance - in order of relevance to the query.

### Schema: search
Element | Default | Required | Description
------- | ------- | -------- | -----------
query | - | Yes | An MQL query used to perform a search.
databases | - | Yes | A non-zero list of database elements each one containing a database code (medlineprof/embase).  The top level list of databases must include all databases used in any search sets.
set | - | No | Any number of set elements can be included in the after the databases element.  This allows for the inclusion of an unlimited number of search sets. 
options | - | No | A collection of search options that modify the number of documents returned by the search.

### Schema: set

Attribute | Required | Description
--------- | -------- | -----------
id | Yes | The numeric reference for the set.  So, if your query is: test and s1, then you should have a set element with an id of 1.

Element | Required | Description
------- | -------- | -----------
query | Yes | An MQL query used for this set.
databases | No | If included, a non-zero list of database elements each one containing a database code.  This filters the databases used for this set in the query.

### Schema: options

Element | Default | Required | Description
------- | ------- | -------- | -----------
includeLemmatization | false | No | Specify whether to automatically search terms with the same lemmatized stem (read|reads|reading). (true/false)
includeUsUkSpellingVariants | false | No | Specify whether to automatically search for US/UK spelling variations of the terms used in the query. (true/false)
includeDuplicates | false | No | Specify whether or not to include duplicate documents in the results returned. (true/false)
