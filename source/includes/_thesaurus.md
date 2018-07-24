# Thesaurus

The thesaurus endpoint allows for the discovery of available thesauri for databases.  It allows searching the content of a thesaurus for preferred terms, synonyms, and thesaurus notes.

## Discover thesauri

> Response:

```xml
<thesaurusList>
    <thesaurusName>medline2018_en</thesaurusName>
</thesaurusList>
```

Discover available thesauri for a database or a set of databases.

### HTTP Request

`GET /thesaurus/fordatabases/{databaselist}`

### URL (template) Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
databaselist | - | Yes | A comma delimited list of database codes (medlineprof/embase).

<aside class="success">
Remember — GET requests must still contain a correct Authorization header.
</aside>

## Search thesaurus terms

> Response:

```xml
<searchResponse>
    <totalHits>158</totalHits>
    <resultSet>
        <entry>
            <id product="medline2018_en" ord="14981">medline2018_en_14981</id>
            <head>Blood</head>
            <paths>
                <path tn="A.15.145">
                    <term ord="6944">Anatomy</term>
                    <term ord="49543">Hemic and Immune Systems</term>
                </path>
                <path tn="A.12.207.152">
                    <term ord="6944">Anatomy</term>
                    <term ord="42271">Fluids and Secretions</term>
                    <term ord="15269">Body Fluids</term>
                </path>
            </paths>
            <broader>
                <term ord="15269">Body Fluids</term>
                <term ord="49543">Hemic and Immune Systems</term>
            </broader>
            <narrower>
                <term ord="14993" tn="A.15.145">Blood Cells</term>
                <term ord="41437" tn="A.12.207.152">Fetal Blood</term>
                <term ord="41437" tn="A.15.145">Fetal Blood</term>
                <term ord="84757" tn="A.15.145">Plasma</term>
                <term ord="84757" tn="A.12.207.152">Plasma</term>
                <term ord="98451" tn="A.15.145">Serum</term>
                <term ord="98451" tn="A.12.207.152">Serum</term>
            </narrower>
            <related>
                <term ord="49466">Hematopoiesis</term>
            </related>
            <scopeNote>The body fluid that circulates in the vascular system (BLOOD VESSELS). Whole blood includes PLASMA and BLOOD CELLS.</scopeNote>
            <allowableQualifiers>
                <term ord="86" product="medline2018_qualifiers_en" alt="DG">diagnostic imaging</term>
                <term ord="91" product="medline2018_qualifiers_en" alt="DE">drug effects</term>
                <term ord="148" product="medline2018_qualifiers_en" alt="IM">immunology</term>
                <term ord="177" product="medline2018_qualifiers_en" alt="ME">metabolism</term>
                <term ord="181" product="medline2018_qualifiers_en" alt="MI">microbiology</term>
                <term ord="205" product="medline2018_qualifiers_en" alt="PS">parasitology</term>
                <term ord="244" product="medline2018_qualifiers_en" alt="RE">radiation effects</term>
                <term ord="303" product="medline2018_qualifiers_en" alt="VI">virology</term>
            </allowableQualifiers>
            <creationYear>1999</creationYear>
            <note>Annotation: general only as a substance: prefer / blood with higher animals, substances & diseases: Manual 19.7+, 19.8.10; not for hemodynamics: Manual 23.28, 23.29; reinfusion = BLOOD TRANSFUSION, AUTOLOGOUS; venous blood: coordinate BLOOD + VEINS or specific vein but do not index here for routine blood samples; arterial blood: coordinate BLOOD + ARTERIES or specific artery but only if the arterial aspect is significant; "blood picture" = probably BLOOD CELLS or BLOOD CELL COUNT; "blood clot": physiol clot or clotting = BLOOD COAGULATION, pathologic clot or clotting = THROMBOSIS or EMBOLISM</note>
        </entry>
        <entry>
            <id product="medline2018_en" ord="14982">medline2018_en_14982</id>
            <head>Blood Alcohol Concentration</head>
            <use>
                <term ord="14983">Blood Alcohol Content</term>
            </use>
        </entry>
    </resultSet>
</searchResponse>
```

Search for any thesaurus terms that match the provided query.

### HTTP Request

`GET /thesaurus/{thesaurusName}/beginswith/{query}`

`GET /thesaurus/{thesaurusName}/contains/{query}`

### URL (template) Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
thesaurusName | - | Yes | A thesaurus name as discovered through the /thesaurus/fordatabases/{databaselist} endpoint.
query | - | Yes | Description (need to figure out restrictions as well, special characters are likely not handled well)

### Query Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
offset | 0 | No | How many result terms to skip in the search response. This facilitates paging through thesaurus term search results.
count | 50? | No | How many result terms to include in the response.  The platform service limit is very high or unlimited, we should probably consider how many we want to allow.

### Schema: searchResponse

Element | Required | Description
------- | -------- | -----------
totalHits | Yes | The number of thesaurus terms that match the query.
resultSet | No | An element container for a number of thesaurus entries.

## Obtain specific thesaurus term

> Response

```xml
<entry>
    <id product="medline2018_en" ord="6944">medline2018_en_6944</id>
    <head>Anatomy</head>
    <paths>
        <path tn="A"/>
    </paths>
    <broader>
        <term ord="0">thesaurus_root</term>
    </broader>
    <narrower>
        <term ord="7533" tn="A">Animal Structures</term>
        <term ord="12318" tn="A">Bacterial Structures</term>
        <term ord="15292" tn="A">Body Regions</term>
        <term ord="19015" tn="A">Cardiovascular System</term>
        <term ord="20759" tn="A">Cells</term>
        <term ord="32412" tn="A">Digestive System</term>
        <term ord="36491" tn="A">Embryonic Structures</term>
        <term ord="37010" tn="A">Endocrine System</term>
        <term ord="42271" tn="A">Fluids and Secretions</term>
        <term ord="43580" tn="A">Fungal Structures</term>
        <term ord="49543" tn="A">Hemic and Immune Systems</term>
        <term ord="56860" tn="A">Integumentary System</term>
        <term ord="70831" tn="A">Musculoskeletal System</term>
        <term ord="73417" tn="A">Nervous System</term>
        <term ord="84706" tn="A">Plant Structures</term>
        <term ord="94082" tn="A">Respiratory System</term>
        <term ord="97969" tn="A">Sense Organs</term>
        <term ord="102929" tn="A">Stomatognathic System</term>
        <term ord="108235" tn="A">Tissues</term>
        <term ord="112530" tn="A">Urogenital System</term>
        <term ord="114296" tn="A">Viral Structures</term>
    </narrower>
</entry>
```

Obtain an thesaurus term entry by matching its head term exactly.

### HTTP Request

`GET /thesaurus/{thesaurusName}/term/{query}`

### URL (template) Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
thesaurusName | - | Yes | A thesaurus name as discovered through the /thesaurus/fordatabases/{databaselist} endpoint.
query | - | Yes | The exact name of a thesaurus head term.

### Schema: entry

Element | Required | Description
------- | -------- | -----------
id | Yes | An id element defining a compound unique identifier for the entry.
head | Yes | A label defining the complete head phrase for the entry. (Label type)
paths | No | A container element for multiple path elements.
broader | No | A container element listing zero or more broader thesaurus terms as term elements.
narrower | No | A container element listing zero or more narrower thesaurus terms as term elements.
related | No | A container element listing zero or more related thesaurus terms as term elements.
useFor | No | A container element listing zero or more thesaurus terms for which this entry should be used instead.
use | No | A container element listing zero or more thesaurus terms that should be used instead of the current entry.
scopeNote | No | Zero or more scopeNote elements compose the scope notes for a thesaurus entry.
historicalNote | No | Zero or more historicalNote elements compose the historical notes for a thesaurus entry.
classificationCode | No | Zero or more classificationCode elements define the classification codes for a thesaurus entry.
editorialCode | No | Zero or more editorialCode elements define the editorial codes for a thesaurus entry.
allowableQualifiers | No | A container element listing zero or more allowable qualifiers for a thesaurus entry.
creationYear | No | The year the thesaurus entry was created.
note | No | Zero or more note elements compose the notes for the thesaurus entry.

### Schema: head/term (Label type)

Attribute | Required | Description
--------- | -------- | -----------
ord | No | This contains the ordinal value for the linked term when present.
product | No | This is the thesaurus this term references when present.
alt | No | This stores the non-English or alternative value for the term when present.
tn | No | This stores the tree number in the thesaurus hierarchy for the term when present.

### Schema: path

Attribute | Required | Description
--------- | -------- | -----------
tn | No | This stores the tree number in the thesarus hierarchy for the path when present.

Element | Required | Description
------- | -------- | -----------
term | No | Zero or more term elements defining a transition of broader to narrower terms (or the reverse).
