# CARE-SM Implementaion -- CSV Documentation

<br>

* [Step by Step](#step-by-step)
* [Data element glossary](#data-element-glossary)

---

## Step by step

1) Create your CSV file

    In order to create a functional CSV file for your patient data for implementing CARE-SM. A set of column names are required to be populated in a CSV file. We recommend first to create an empty CSV file with all these column names on it. The required column names are:

    * `model`: Tagname used by CARE-SM toolkit to recognize which data element is being represented.
    * `pid`: patient identifier, represents the personal identifier of the patient.
    * `value`: Numerical or Lexical data value of this data entry.
    * `value_datatype`: XSD data type of the `value` column name.
    * `valueIRI`: IRI-based value of this data entry.
    * `process_type`: IRI-based ontological class that describes the patient procedure.
    * `unit_type`: IRI-based ontological class that describes the unit of `value` measurement.
    * `input_type`: IRI-based ontological class that describes the input of the patient procedure.
    * `target_type`:IRI-based ontological class that describes the target of the patient procedure.
    * `frequency_type`: IRI-based ontological class that describes the frequency of `value` presence.
    * `frequency_value`: Numerical value associated with the `frequency_type`
    * `agent_id`: GUID used to describe any agent that participates in the data entry
    * `route_type`: IRI-based ontological class that describes the route of administration
    * `startdate`: the start date of the observation process
    * `enddate`: the end date of the observation process
    * `age`: the age of the patient at time of observation
    * `comments` : free-text comments
    * `context_id`: a method for grouping observations together (explained elsewhere... one day!)

    Very few of this column names are present at all (or most) of the cases, but **its mandatory all columns to exist in the CSV file**. No need to know precisely the meaning of every one of them. Each data element requires a subset of these columns to be filled, and the rest are 'null'.


    This is an example of an empty CSV file with the proper columns names:

    ```csv
    model,pid,context_id,value,age,value_datatype,valueIRI,process_type,unit_type,input_type,target_type,frequency_type,frequency_value,agent_id,route_type,startdate,enddate,comments
    ,,,,,,,,,,,,,,,,,

    ```

2) Rename the CSV file as `preCARE.csv`. CARE-SM will recognize the name as the proper tagname and perform the quality control on it using `CARE-SM Toolkit`. This is why its mandatory to create a single file because this is the one file its going to be executed.

    

3) Populate your patient data elements

    Every data element requires a concrete set of column names to be populated. This is because not every clinical entry contains the same type of information.(e.g. a laboratory measurement needs to specify the targeting molecule to analyze, but a diagnosis assessment doesn't require defining any target). 

    <br>
    This is a glossary of every data requirement documentation:

    - Demographic personal information:

        * [Birthdate](#birthdate) - patient date of birth
        * [Sex](#sex) -  patient sex at birth
        * [Body measurement](#body-measurement) - patient physical measurement of the body. 

    - Participation status:
        * [Status](#participation-status) - patient alive or dead status
        * [Deathdate](#deathdate) -  patient date of death

    - Medical history:
        * [First confirmed visit](#first-confirmed-visit) - patient first contact with specialized center
        * [Symptoms onset](#symptoms-onset) - patient signs/symptoms onset

    - Conditions and medical findings:
        * [Diagnosis](#diagnosis) - patient disease diagnosis
        * [Symptoms and phenotype assessment](#symptoms-or-signs) - patient date of signs/symptoms and its onset
        * [Genetic information](#genetic-information) - genetic diagnosis retained by the specialized center
        * [Disability](#disability) - patient disability score
        * [Laboratory Measurement](#laboratory-measurement) - patient laboratory measurements.
        * [Medical imaging](#medical-imaging) - any patient medical imaging data.

    - Research availability and consent:
        * [Biobank](#biobank) - availability of subject's samples in a biobank
        * [Consent](#consent-for-being-contacted) - consent given by a subject

    - Treatment-related interventions:
        * [Medication](#medications) - patient medications based on a prescription.
        * [Medical intervention](#medical-intervention) - any component presented in treatment and therapy/surgery procedures.

    - Clinical trials:
        * [Clinical Trials](#clinical-trials) - patient participation in clinical trials.

    <br>
    This is an example of functional `preCARE.csv` file that can be used with CARE-SM Toolkit,  both for `FAIR-in-a-box` software or Standalone implementation:

    ```csv
    model,pid,context_id,value,age,value_datatype,valueIRI,process_type,unit_type,input_type,target_type,frequency_type,frequency_value,agent_id,route_type,startdate,enddate,comments
    Diagnosis,30056,,,,,http://www.orpha.net/ORDO/Orphanet_93552,,,,,,,,,2006-01-19,,

    ```

    Find more complete exemplar cases at [`exemplar_data`](/CSV/exemplar_data/) folder.

## Data Element Glossary

Here you can find the list of data elements and the columns required to be defined. Those that are optional, feel free to add them. If not, leave them empty.



### Birthdate:

- **pid**: Patient unique identifier 
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: ISO 8601 formatted date (not date time)
- **model**: Birthdate
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- **comments**: Human readable comments of any kind related to this procedure.

### Birthyear:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: Year of birth defined as YYYY.
- **model**: Birthyear
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.  
- **comments**: Human readable comments of any kind related to this procedure.

### Deathdate:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: ISO 8601 formatted date of death (not date time), or age in which the patient died.
- **value_datatype**: XSD datatype that defines `value` column type.
    - xsd:date in case you added date.
    - xsd:integer in case you added age.
- **model**: Deathdate
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **comments**: Human readable comments of any kind related to this procedure.

### First Confirmed Visit:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: ISO 8601 formatted date of first confirmed visit (not date time) or age in case you added the age of the first confirmed visit.
- **value_datatype**: XSD datatype that defines `value` column type.
    - xsd:date in case you added date.
    - xsd:integer in case you added age.
- **model**: First_visit
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **comments**: Human readable comments of any kind related to this procedure.


### Symptoms onset:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **model**: Symptom_onset
- **value**: ISO 8601 formatted date of symptom onset (not date time) or age in case you added the age of symptom onset. This value represents the onset perceived by the patient, as a difference of the clinical encounter, defined as `startdate`.
- **value_datatype**: XSD datatype that defines `value` column type.
    - xsd:date in case you added date.
    - xsd:integer in case you added age.
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **comments**: Human readable comments of any kind related to this procedure.

### Sex:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: one of the following: 
    * http://purl.obolibrary.org/obo/NCIT_C16576 (Female) ; 
    * http://purl.obolibrary.org/obo/NCIT_C20197 (Male); 
    * http://purl.obolibrary.org/obo/NCIT_C124294 (Undetermined) ; 
    * http://purl.obolibrary.org/obo/NCIT_C17998 (Unknown, use this for foetal undetermined) 
- **model**: Sex
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **comments**: Human readable comments of any kind related to this procedure.

### Participation status:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: one of the following: 
    * http://semanticscience.org/resource/SIO_010059 (dead)
    * http://semanticscience.org/resource/SIO_010058 (alive)
    * http://purl.obolibrary.org/obo/NCIT_C70740 (lost to follow-up)
    * http://purl.obolibrary.org/obo/NCIT_C124784 (refused to participate)
- **model**: Status
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation was taken, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Symptoms or signs:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: IRI that defines clinical symptom or sign: For example Human Phenotype ontology (HPO) term represented with a full URL such as http://purl.obolibrary.org/obo/HP_0001251
- **model**: Symptom
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when the patient started to perceive the symptoms.
- **comments**: Human readable comments of any kind related to this procedure.

### Diagnosis:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
- **model**: Diagnosis
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation was taken, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Genetic information:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: Genetic code constructed by appending the HGVS/HGNC/OMIM code, e.g. https://www.omim.org/entry/310200
- **value**: *(OPTIONAL)*  Human readable label that defines the genetic identifier. Example: HNGC:489
- **model**: Genetic
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation was taken, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Consent for being contacted:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: Some label describing consent outcome
- **value_datatype**: XSD data type that defines `value` column type, for this case is xsd:string by default
- **model**: Consent_contacted
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Consent for Data (Re)Use Permission:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **value**: Some label describing consent outcome
- **value_datatype**: XSD data type that defines `value` column type, for this case is xsd:string by default
- **model**: Consent_used
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Biobank:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **agent_id**: Biobank Identifier as https://directory.bbmri-eric.eu/{biobank id}
- **value_datatype**: XSD data type that defines `value` column type, for this case is xsd:string by default
- **model**: Biobank
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`. 
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


### Disability:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **process_type**: Some child of http://purl.obolibrary.org/obo/NCIT_C20993 (research or clinical assessment tool)
- **value_datatype**: XSD datatype that defines `value` column type, for this case is xsd:float by default, but depending on your score's datatype, it could be different.
- **value**: the numeric score of the output from the test
- **model**: Disability
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted enddate of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation ocurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


### Body measurement:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **valueIRI**: Child of Personal Attribute: http://purl.obolibrary.org/obo/NCIT_C19332
- **value**: Resulting value from this observation
- **value_datatype**: XSD datatype that defines `value` column type, for this case is xsd:float by default, but depending on your score's datatype, it could be different.
- **unit_type**: Child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- **model**: Body_measurement
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted enddate of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation ocurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Laboratory measurement:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **input_type**: Material input represented as Child of Anatomic, Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (ex: obo:Urine)
- **value**: Resulting value from this analysis
- **value_datatype**: XSD data type that defines `value` column type, for this case is xsd:float by default, but depending on your score's datatype, it could be different.
- **target_type**: Compound being measured in the sample. Child of Drug, Food, Chemical or Biomedical Material http://purl.obolibrary.org/obo/NCIT_C1908 (ex: obo:Creatinine http://purl.obolibrary.org/obo/NCIT_C399)
- **unit_type**: Child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- **model**: Lab_measurement
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


### Medical imaging:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **process_type**: child of Imaging technique http://purl.obolibrary.org/obo/NCIT_C17369  (example: obo:Digital X-Ray http://purl.obolibrary.org/obo/NCIT_C18001)
- **target_type**: Child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (ex: obo:Palmar Region http://purl.obolibrary.org/obo/NCIT_C33252)
- **valueIRI**: Preferably a URI-based GUID of the file (must be a GUID system compatible with RDF Resource identifiers)
- **model**: Imaging
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.

### Medications:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **route_type**: Child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (example: obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
- **value**: Dose value prescribe to the patient
- **value_datatype**: XSD datatype that defines `value` column type, for this case is xsd:float by default, but depending on your score's datatype, it could be different.
- **unit_type**: Child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- **frequency_type**: Child of obo:Temporal Qualifier http://purl.obolibrary.org/obo/NCIT_C21514 (ex: obo:Per Day)
- **frequency_value**: Frequency value prescribe to the patient
- **agent_id**: ATC URI-code for drugs components. (example: https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- **model**: Medications
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


### Medical intervention:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **process_type**: Child of Intervention or Procedure http://purl.obolibrary.org/obo/NCIT_C25218 (ex: obo:Tumor Resection http://purl.obolibrary.org/obo/NCIT_C164212)
- **target_type**:  *(RECOMMENDED)* Child of Anatomic Structure, System, or Substance
- **agent_id**: *(IN CASE OF ANY)* ATC URI-code for drugs components. (example: https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- **route_type**: *(IN CASE OF ANY)* Child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (example: obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
or obo:Material (example: obo: Tumor Tissue http://purl.obolibrary.org/obo/NCIT_C18009)
- **model**: Intervention
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


### Clinical trials:

- **pid**: Patient unique identifier
- **context_id**: *(OPTIONAL)* Contextual identifier in case you want to relate several data elements under a common context (ex: certain diagnosis/phenotype relationship or some elements under same visit occurrence)
- **agent_id**: GUID for this medical center where this clinical trial is taking place.
- **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630- **model**: Clinical_trial
- **startdate**: *(OPTIONAL)* ISO 8601 formatted start date of observation
- **enddate**: *(OPTIONAL)* ISO 8601 formatted end date of observation in case it is different from `startdate`.
- **age**: *(OPTIONAL)* Patient age when this observation occurred, this age information can be both an addition or an alternative for start/end date information.
- **comments**: Human readable comments of any kind related to this procedure.


