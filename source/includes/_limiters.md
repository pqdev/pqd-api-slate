# Limiters

The limiters endpoint allows for the discovery of available limiters for databases.  It further facilitates determining search limiter values and constructing a search based on limiter values.

## Discover limiters

> Response:

```xml
<limiters>
    <limiter name="Abstract" type="simple">
        <label lang="en">Abstract Included</label>
        <option name="Yes">
            <mql>abany(yes)</mql>
        </option>
    </limiter>
    <limiter name="Humans" type="simple">
        <label lang="en">Humans</label>
        <option name="Yes">
            <mql>human(yes)</mql>
        </option>
    </limiter>
    <limiter name="Animals" type="simple">
        <label lang="en">Animals</label>
        <option name="Yes">
            <mql>animal(yes)</mql>
        </option>
    </limiter>
    <limiter name="EmbaseClinicalTrials" type="simple">
        <label lang="en">Clinical Trials</label>
        <option name="Yes">
            <mql>(EMB.EXACT.EXPLODE("CLINICAL TRIAL") OR EMB.EXACT.EXPLODE("CLINICAL TRIAL (TOPIC)") OR EMB("CLINICAL TRIAL*")) OR (dtype("CLINICAL TRIAL*" or "CONTROLLED CLINICAL TRIAL" or "MULTICENTER STUDY" or "RANDOMIZED CONTROLLED TRIAL" or "EQUIVALENCE TRIAL") or mesh.EXACT.EXPLODE("Clinical Trials as Topic"))</mql>
        </option>
    </limiter>
    <limiter name="PublicationDate" type="date">
        <label lang="en">Publication Date</label>
        <mnemonic>pd</mnemonic>
    </limiter>
    <limiter name="embSubject" type="field">
        <label lang="en">Emtree Subject</label>
        <mnemonic>emb</mnemonic>
    </limiter>
    <limiter name="casRegistryNumber" type="field">
        <label lang="en">CAS Registry Number</label>
        <mnemonic>rn</mnemonic>
    </limiter>
    <limiter name="EmbaseDocumentStatus" type="complex">
        <label lang="en">Embase Document Status</label>
        <option name="ArticleInPress">
            <label lang="en">Article in Press</label>
            <mql>dstat.exact("Article in Press")</mql>
        </option>
        <option name="InProcess">
            <label lang="en">In Process</label>
            <mql>dstat.exact("In Process")</mql>
        </option>
        <option name="Embase">
            <label lang="en">Embase</label>
            <mql>dstat.exact("Embase")</mql>
        </option>
        <option name="MEDLINE">
            <label lang="en">MEDLINE</label>
            <mql>dstat.exact("MEDLINE")</mql>
        </option>
    </limiter>
    <limiter name="AgeGroupEmbase" type="complex">
        <label lang="en">Age Group</label>
        <option name="Adult">
            <label lang="en">Adult</label>
            <mql>emb.exact("adult")</mql>
            <option name="Aged">
                <label lang="en">Aged</label>
                <mql>emb.exact("aged")</mql>
                <option name="AgedHospitalPatient">
                    <label lang="en">Aged Hospital Patient</label>
                    <mql>emb.exact("aged hospital patient")</mql>
                </option>
                <option name="InstitutionalizedElderly">
                    <label lang="en">Institutionalized Elderly</label>
                    <mql>emb.exact("institutionalized elderly")</mql>
                </option>
                <option name="VeryElderly">
                    <label lang="en">Very Elderly</label>
                    <mql>emb.exact("very elderly")</mql>
                </option>
            </option>
            <option name="InstitutionalizedAdult">
                <label lang="en">Institutionalized Adult</label>
                <mql>emb.exact("institutionalized adult")</mql>
            </option>
            <option name="MiddleAged">
                <label lang="en">Middle Aged</label>
                <mql>emb.exact("middle aged")</mql>
            </option>
            <option name="YoungAdult">
                <label lang="en">Young Adult</label>
                <mql>emb.exact("young adult")</mql>
            </option>
        </option>
        <option name="Juvenile">
            <label lang="en">Juvenile</label>
            <mql>emb.exact("juvenile")</mql>
            <option name="Adolescent">
                <label lang="en">Adolescent</label>
                <mql>emb.exact("adolescent")</mql>
            </option>
            <option name="Child">
                <label lang="en">Child</label>
                <mql>emb.exact("child")</mql>
            </option>
        </option>
        <option name="Embryo">
            <label lang="en">Embryo</label>
            <mql>emb.exact("embryo")</mql>
        </option>
    </limiter>
</limiters>
```

Discover available limiters for a database or a set of databases.

### HTTP Request

`GET /limiter/fordatabases/{databaseList}`

### URL (template) Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
databaseList | - | Yes | A comma delimited list of database codes (medlineprof/embase).

<aside class="success">
Remember — GET requests must still contain a correct Authorization header.
</aside>

### Schema: limiter

Attribute | Required | Description
--------- | -------- | -----------
name | Yes | The unique name (identifier) of the limiter.
type | Yes | The generic type of limiter.  This can help clients to decide how to handle the specific limiter details.

Element | Required | Description
------- | -------- | -----------
label | No | Zero or more label elements naming the limiter in various languages.
mnemonic | No | What mnemonic to use to search this limiter.
option | No | Zero or more option elements describing the various options for this limiter.

### Schema: label


### Schema: option
