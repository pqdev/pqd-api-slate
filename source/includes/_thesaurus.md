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
    <TotalHits>158</TotalHits>
    <ResultSet>
        <Entry>
            <ID product="medline2018_en" ord="14981">medline2018_en_14981</ID>
            <Head>Blood</Head>
            <Paths>
                <Path tn="A.15.145">
                    <Term ord="6944">Anatomy</Term>
                    <Term ord="49543">Hemic and Immune Systems</Term>
                </Path>
                <Path tn="A.12.207.152">
                    <Term ord="6944">Anatomy</Term>
                    <Term ord="42271">Fluids and Secretions</Term>
                    <Term ord="15269">Body Fluids</Term>
                </Path>
            </Paths>
            <BT>
                <Term ord="15269">Body Fluids</Term>
                <Term ord="49543">Hemic and Immune Systems</Term>
            </BT>
            <NT>
                <Term ord="14993" tn="A.15.145">Blood Cells</Term>
                <Term ord="41437" tn="A.12.207.152">Fetal Blood</Term>
                <Term ord="41437" tn="A.15.145">Fetal Blood</Term>
                <Term ord="84757" tn="A.15.145">Plasma</Term>
                <Term ord="84757" tn="A.12.207.152">Plasma</Term>
                <Term ord="98451" tn="A.15.145">Serum</Term>
                <Term ord="98451" tn="A.12.207.152">Serum</Term>
            </NT>
            <RT>
                <Term ord="49466">Hematopoiesis</Term>
            </RT>
            <SN>
                <Term ord="0">The body fluid that circulates in the vascular system (BLOOD VESSELS). Whole blood includes PLASMA and BLOOD CELLS.</Term>
            </SN>
            <AQ>
                <Term ord="86" product="medline2018_qualifiers_en" alt="DG">diagnostic imaging</Term>
                <Term ord="91" product="medline2018_qualifiers_en" alt="DE">drug effects</Term>
                <Term ord="148" product="medline2018_qualifiers_en" alt="IM">immunology</Term>
                <Term ord="177" product="medline2018_qualifiers_en" alt="ME">metabolism</Term>
                <Term ord="181" product="medline2018_qualifiers_en" alt="MI">microbiology</Term>
                <Term ord="205" product="medline2018_qualifiers_en" alt="PS">parasitology</Term>
                <Term ord="244" product="medline2018_qualifiers_en" alt="RE">radiation effects</Term>
                <Term ord="303" product="medline2018_qualifiers_en" alt="VI">virology</Term>
            </AQ>
            <DATE>
                <Term ord="0">1999</Term>
            </DATE>
            <NOTE>
                <Term ord="0">Annotation: general only as a substance: prefer / blood with higher animals, substances & diseases: Manual 19.7+, 19.8.10; not for hemodynamics: Manual 23.28, 23.29; reinfusion = BLOOD TRANSFUSION, AUTOLOGOUS; venous blood: coordinate BLOOD + VEINS or specific vein but do not index here for routine blood samples; arterial blood: coordinate BLOOD + ARTERIES or specific artery but only if the arterial aspect is significant; "blood picture" = probably BLOOD CELLS or BLOOD CELL COUNT; "blood clot": physiol clot or clotting = BLOOD COAGULATION, pathologic clot or clotting = THROMBOSIS or EMBOLISM</Term>
            </NOTE>
            <EXPLODE>14981 15269 42271 49543 6944 A A.12 A.12.207 A.12.207.152 A.15 A.15.145</EXPLODE>
        </Entry>
        <Entry>
            <ID product="medline2018_en" ord="14982">medline2018_en_14982</ID>
            <Head>Blood Alcohol Concentration</Head>
            <USE>
                <Term ord="14983">Blood Alcohol Content</Term>
            </USE>
            <EXPLODE>14982 </EXPLODE>
        </Entry>
    </ResultSet>
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

## Obtain specific thesaurus term

> Response

```xml
<Entry>
    <ID product="medline2018_en" ord="6944">medline2018_en_6944</ID>
    <Head>Anatomy</Head>
    <Paths>
        <Path tn="A"/>
    </Paths>
    <BT>
        <Term ord="0">thesaurus_root</Term>
    </BT>
    <NT>
        <Term ord="7533" tn="A">Animal Structures</Term>
        <Term ord="12318" tn="A">Bacterial Structures</Term>
        <Term ord="15292" tn="A">Body Regions</Term>
        <Term ord="19015" tn="A">Cardiovascular System</Term>
        <Term ord="20759" tn="A">Cells</Term>
        <Term ord="32412" tn="A">Digestive System</Term>
        <Term ord="36491" tn="A">Embryonic Structures</Term>
        <Term ord="37010" tn="A">Endocrine System</Term>
        <Term ord="42271" tn="A">Fluids and Secretions</Term>
        <Term ord="43580" tn="A">Fungal Structures</Term>
        <Term ord="49543" tn="A">Hemic and Immune Systems</Term>
        <Term ord="56860" tn="A">Integumentary System</Term>
        <Term ord="70831" tn="A">Musculoskeletal System</Term>
        <Term ord="73417" tn="A">Nervous System</Term>
        <Term ord="84706" tn="A">Plant Structures</Term>
        <Term ord="94082" tn="A">Respiratory System</Term>
        <Term ord="97969" tn="A">Sense Organs</Term>
        <Term ord="102929" tn="A">Stomatognathic System</Term>
        <Term ord="108235" tn="A">Tissues</Term>
        <Term ord="112530" tn="A">Urogenital System</Term>
        <Term ord="114296" tn="A">Viral Structures</Term>
    </NT>
    <EXPLODE>6944 A </EXPLODE>
</Entry>
```

Obtain an thesaurus term entry by matching its head term exactly.

### HTTP Request

`GET /thesaurus/{thesaurusName}/term/{query}`

### URL (template) Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
thesaurusName | - | Yes | A thesaurus name as discovered through the /thesaurus/fordatabases/{databaselist} endpoint.
query | - | Yes | The exact name of a thesaurus head term.
