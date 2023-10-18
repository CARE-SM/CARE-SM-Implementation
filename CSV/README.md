# CARE-SM Implementation -- CSV Documentation

<br>

* [Step by Step](#step-by-step)
* [Data element glossary](#data-element-glossary)

---

## Step by step

1) Create your CSV file

    In order to create a functional CSV file for your patient data for implementing CARE-SM. A set of column names are required to be populated in a CSV file. We recommend first to create an empty CSV file with all these column names on it. The required column names are:

    * `model`: Tagname used by CARE-SM toolkit to recognize which data element is being represented.
    * `pid`: individual identifier, in the form of a patient identifier.
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
    * `event_id`: a method for grouping observations together (explained elsewhere... one day!)

    Very few of this column names are present at all (or most) of the cases, but **its mandatory all columns to exist in the CSV file**. No need to know precisely the meaning of every one of them. Each data element requires a subset of these columns to be filled, and the rest are 'null'.


    This is an example of an empty CSV file with the proper columns names:

    ```csv
    model,pid,event_id,value,age,value_datatype,valueIRI,process_type,unit_type,input_type,target_type,frequency_type,frequency_value,agent_id,route_type,startdate,enddate,comments
    ,,,,,,,,,,,,,,,,,

    ```

2) Rename the CSV file as `preCARE.csv`. CARE-SM will recognize the name as the proper tagname and perform the quality control on it using `CARE-SM Toolkit`. This is why it's mandatory to create a single file because this is the one file it's going to be executed.

    

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
    model,pid,event_id,value,age,value_datatype,valueIRI,process_type,unit_type,input_type,target_type,frequency_type,frequency_value,agent_id,route_type,startdate,enddate,comments
    Diagnosis,30056,,,,,http://www.orpha.net/ORDO/Orphanet_93552,,,,,,,,,2006-01-19,,

    ```

    Find more complete exemplar cases at [`exemplar_data`](/CSV/exemplar_data/README.md) folder.

## Data Element Glossary

Here you can find the list of data elements and the columns required to be defined. Those that are optional, feel free to add them. If not, leave them empty.


#### **Legend:**
Those columns colored as <span style="color: grey"> GREY means UNUSED </b></span> for this case.
Those columns colored as <span style="color: orange"> <b> ORANGE means IN CASE OF ANY </b></span> .
Those columns colored as <span style="color: blue"> <b> BLUE means REQUIRED </b></span> column to fill in.


### Birthdate:

* <span style="color: blue"> <b> model </b></span> : Birthdate
* <span style="color: blue"> <b> pid </b></span> : patient unique identifier.
* <span style="color: blue"> <b> value </b></span> : ISO 8601 formatted date (not date time)
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: grey"> age </b></span> : Year of birth defined as YYYY.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Birthyear:

* <span style="color: blue"> <b> model </b></span> : Birthyear
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : year of birth defined as YYYY.
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: grey"> age </b></span> : 
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Deathdate:


* <span style="color: blue"> <b> model </b></span> : Deathdate
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : ISO 8601 formatted date of death (not date time)
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### First Confirmed Visit:

* <span style="color: blue"> <b> model </b></span> : First_visit
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : ISO 8601 formatted date of first confirmed visit (not date time)
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Symptoms onset:


* <span style="color: blue"> <b> model </b></span> : Symptom_onset
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> :  ISO 8601 formatted date of symptom onset (not date time). This value represents the onset **perceived** by the patient, as a difference of the clinical observation, defined as `startdate`.
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: grey"> age </b></span> : patient age when this observation was *perceived* by the patient, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Sex:

* <span style="color: blue"> <b> model </b></span> : Sex
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: orange"> value </b></span> : human readable label, e.g. Female
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : one of the following: 
    * http://purl.obolibrary.org/obo/NCIT_C16576 (Female) ; 
    * http://purl.obolibrary.org/obo/NCIT_C20197 (Male); 
    * http://purl.obolibrary.org/obo/NCIT_C124294 (Undetermined) ; 
    * http://purl.obolibrary.org/obo/NCIT_C17998 (Unknown, use this for foetal undetermined) 
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: grey"> age </b></span> :
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Participation status:

* <span style="color: blue"> <b> model </b></span> : Status
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: orange"> value </b></span> : any human readable response, e.g. Lost of follow-up
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : one of the following: 
    * http://semanticscience.org/resource/SIO_010059 (dead)
    * http://semanticscience.org/resource/SIO_010058 (alive)
    * http://purl.obolibrary.org/obo/NCIT_C70740 (lost to follow-up)
    * http://purl.obolibrary.org/obo/NCIT_C124784 (refused to participate)
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Symptoms, signs or phenotype assessment:

* <span style="color: blue"> <b> model </b></span> : Symptom
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> :
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : IRI that defines clinical phenotypic symptom or sign: For example Human Phenotype ontology (HPO) term represented with a full URL such as http://purl.obolibrary.org/obo/HP_0001251
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Diagnosis:

* <span style="color: blue"> <b> model </b></span> : Diagnosis
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> :
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Genetic information:

* <span style="color: blue"> <b> model </b></span> : Genetic
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: orange"> <b> value </b></span> : human readable label that defines the genetic identifier. Example: HNGC:489
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : genetic code constructed by appending the HGVS/HGNC/OMIM code, e.g. https://www.omim.org/entry/310200
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Consent for being contacted for research:

* <span style="color: blue"> <b> model </b></span> : Consent_contacted
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: orange"> <b> value </b></span> : some label describing consent outcome
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Consent for data (re)use permission:

* <span style="color: blue"> <b> model </b></span> : Consent_used
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: orange"> <b> value </b></span> : some label describing consent outcome
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Biobank:

* <span style="color: blue"> <b> model </b></span> : Biobank
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> :
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: blue"> <b> agent_id </b></span> : Biobank Identifier as https://directory.bbmri-eric.eu/{biobank id}
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Disability:

* <span style="color: blue"> <b> model </b></span> : Disability
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : numeric score/value of the test output.
* <span style="color: blue"> <b> value_datatype </b></span> : XSD datatype that defines `value` column type, e.g. `xsd:float` por a decimal score.
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: blue"> <b> process_type </b></span> : child of http://purl.obolibrary.org/obo/NCIT_C20993 (research or clinical assessment tool)
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Body measurement:

* <span style="color: blue"> <b> model </b></span> : Body_measurement
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : resulting value from this observation
* <span style="color: blue"> <b> value_datatype </b></span> : XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
* <span style="color: blue"> <b> valueIRI </b></span> : child of Personal Attribute: http://purl.obolibrary.org/obo/NCIT_C19332
* <span style="color: grey"> process_type </b></span> : 
* <span style="color: blue"> <b> unit_type </b></span> : child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> : 
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Laboratory measurement:

* <span style="color: blue"> <b> model </b></span> : Lab_measurement
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: blue"> <b> value </b></span> : resulting value from this analysis.
* <span style="color: blue"> <b> value_datatype </b></span> : XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
* <span style="color: grey"> valueIRI </b></span> : 
* <span style="color: grey"> process_type </b></span> : 
* <span style="color: blue"> <b> unit_type </b></span> : child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
* <span style="color: blue"> <b> input_type </b></span> : material input represented as Child of Anatomic, Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g: obo:Urine)
* <span style="color: blue"> <b> target_type </b></span> : compound being measured in the sample. Child of Drug, Food, Chemical or Biomedical Material http://purl.obolibrary.org/obo/NCIT_C1908 (e.g. obo:Creatinine http://purl.obolibrary.org/obo/NCIT_C399)
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> : 
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medical imaging:

* <span style="color: blue"> <b> model </b></span> : Imaging
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> : 
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : medical imagine GUID of the file (must be a GUID system compatible with RDF Resource identifiers)
* <span style="color: blue"> <b> process_type </b></span> : child of Imaging technique http://purl.obolibrary.org/obo/NCIT_C17369  (e.g. obo:Digital X-Ray http://purl.obolibrary.org/obo/NCIT_C18001)
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: blue"> <b> target_type </b></span> : child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g. obo:Palmar Region http://purl.obolibrary.org/obo/NCIT_C33252)
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: grey"> agent_id </b></span> :
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medications:

* <span style="color: blue"> <b> model </b></span> : Medication
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> : dose value prescribed to the patient
* <span style="color: grey"> value_datatype </b></span> : XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
* <span style="color: grey"> valueIRI </b></span> : 
* <span style="color: grey"> process_type </b></span> : 
* <span style="color: blue"> <b> unit_type </b></span> : child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> : 
* <span style="color: blue"> <b> frequency_type </b></span> : child of obo:Temporal Qualifier http://purl.obolibrary.org/obo/NCIT_C21514 (e.g. obo:Per Day)
* <span style="color: blue"> <b> frequency_value </b></span> : frequency value prescribe to the patient
* <span style="color: blue"> <b> agent_id </b></span> : ATC URI-code for drugs components. (e.g. https://www.whocc.no/atc_ddd_index/?code=A07EA01)
* <span style="color: blue"> <b> route_type </b></span> : child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (e.g. obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medical intervention:

* <span style="color: blue"> <b> model </b></span> : Intervention
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> : 
* <span style="color: grey"> value_datatype </b></span> :
* <span style="color: grey"> valueIRI </b></span> :
* <span style="color: blue"> <b> process_type </b></span> : Child of Intervention or Procedure http://purl.obolibrary.org/obo/NCIT_C25218 (ex: obo:Tumor Resection http://purl.obolibrary.org/obo/NCIT_C164212)
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: orange"> <b> target_type </b></span> : Child of Anatomic Structure, System, or Substance
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: orange"> <b> agent_id </b></span> : If any, ATC URI-code for drugs components. (example: https://www.whocc.no/atc_ddd_index/?code=A07EA01)
* <span style="color: orange"> <b> route_type </b></span> : In case of any, Child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (example: obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Clinical trials:

* <span style="color: blue"> <b> model </b></span> : Clinical_trial
* <span style="color: blue"> <b> pid </b></span> : individual identifier, in form of a patient identifier.
* <span style="color: grey"> value </b></span> :
* <span style="color: grey"> value_datatype </b></span> : 
* <span style="color: blue"> <b> valueIRI </b></span> : IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
* <span style="color: grey"> process_type </b></span> :
* <span style="color: grey"> unit_type </b></span> :
* <span style="color: grey"> input_type </b></span> :
* <span style="color: grey"> target_type </b></span> :
* <span style="color: grey"> frequency_type </b></span> :
* <span style="color: grey"> frequency_value </b></span> :
* <span style="color: blue"> <b> agent_id </b></span> : GUID for this medical center where this clinical trial is taking place.
* <span style="color: grey"> route_type </b></span> :
* <span style="color: orange"> <b> startdate </b></span> : ISO 8601 formatted start date of observation
* <span style="color: orange"> <b> enddate </b></span> : ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
* <span style="color: orange"> <b> age </b></span> : patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
* <span style="color: orange"> <b> comments </b></span> : human readable comments of any kind related to this procedure.
* <span style="color: orange"> <b> event_id </b></span> : contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


