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

#### **Legend:**

- ![](https://placehold.co/15x15/808080/808080.png) This column is **UNUSED** for this case.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) This column is filled in **IN CASE OF ANY**.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) This column colored is **REQUIRED** for this case.



Here you can find the list of data elements and the columns required to be defined. Those that are optional, feel free to add them. If not, leave them empty.


### Birthdate:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Birthdate
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: patient unique identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: ISO 8601 formatted date (not date time)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/808080/808080.png) **age**: Year of birth defined as YYYY.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Birthyear:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Birthyear
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: year of birth defined as YYYY.
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/808080/808080.png) **age**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Deathdate:


- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Deathdate
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: ISO 8601 formatted date of death (not date time)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### First Confirmed Visit:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: First_visit
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: ISO 8601 formatted date of first confirmed visit (not date time). Its required to add at least one the following: `value` and/or `age` column (preferably `value`)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information. Its required to add at least one the following: `value` and/or `age` column (preferably `value`)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Symptoms onset:


- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Symptom_onset
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**:  ISO 8601 formatted date of symptom onset (not date time). This value represents the onset **perceived** by the patient, as a difference of the clinical observation, defined as `startdate`.
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was *perceived* by the patient, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Sex:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Sex
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: human readable label, e.g. Female
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: one of the following: 
    * http://purl.obolibrary.org/obo/NCIT_C16576 (Female) ; 
    * http://purl.obolibrary.org/obo/NCIT_C20197 (Male); 
    * http://purl.obolibrary.org/obo/NCIT_C124294 (Undetermined) ; 
    * http://purl.obolibrary.org/obo/NCIT_C17998 (Unknown, use this for foetal undetermined) 
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/808080/808080.png) **age**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Participation status:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Status
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: any human readable response, e.g. Lost of follow-up
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: one of the following: 
    * http://semanticscience.org/resource/SIO_010059 (dead)
    * http://semanticscience.org/resource/SIO_010058 (alive)
    * http://purl.obolibrary.org/obo/NCIT_C70740 (lost to follow-up)
    * http://purl.obolibrary.org/obo/NCIT_C124784 (refused to participate)
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Symptoms, signs or phenotype assessment:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Symptom
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical phenotypic symptom or sign: For example Human Phenotype ontology (HPO) term represented with a full URL such as http://purl.obolibrary.org/obo/HP_0001251
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Diagnosis:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Diagnosis
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **value**: Human readable label of the diagnosed condition.
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
- ![](https://placehold.co/15x15/808080/808080.png)  **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Genetic information:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Genetic
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: human readable label that defines the genetic identifier. Example: HNGC:489
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: genetic code constructed by appending the HGVS/HGNC/OMIM code, e.g. https://www.omim.org/entry/310200
- ![](https://placehold.co/15x15/808080/808080.png)  **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)


### Consent for being contacted for research:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Consent_contacted
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: some label describing consent outcome
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Consent for data (re)use permission:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Consent_used
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: some label describing consent outcome
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Biobank:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Biobank
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **agent_id**: Biobank Identifier as https://directory.bbmri-eric.eu/{biobank id}
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Disability:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Disability
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: numeric score/value of the test output.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` por a decimal score.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **process_type**: child of http://purl.obolibrary.org/obo/NCIT_C20993 (research or clinical assessment tool)
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Body measurement:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Body_measurement
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: resulting value from this observation
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: child of Personal Attribute: http://purl.obolibrary.org/obo/NCIT_C19332
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit_type**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**: 
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Laboratory measurement:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Lab_measurement
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: resulting value from this analysis.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**: 
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit_type**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **input_type**: material input represented as Child of Anatomic, Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g: obo:Urine)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **target_type**: compound being measured in the sample. Child of Drug, Food, Chemical or Biomedical Material http://purl.obolibrary.org/obo/NCIT_C1908 (e.g. obo:Creatinine http://purl.obolibrary.org/obo/NCIT_C399)
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**: 
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medical imaging:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Imaging
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: 
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: medical imagine GUID of the file (must be a GUID system compatible with RDF Resource identifiers)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **process_type**: child of Imaging technique http://purl.obolibrary.org/obo/NCIT_C17369  (e.g. obo:Digital X-Ray http://purl.obolibrary.org/obo/NCIT_C18001)
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **target_type**: child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g. obo:Palmar Region http://purl.obolibrary.org/obo/NCIT_C33252)
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medications:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Medication
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: dose value prescribed to the patient
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**: 
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit_type**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **frequency_type**: child of obo:Temporal Qualifier http://purl.obolibrary.org/obo/NCIT_C21514 (e.g. obo:Per Day)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **frequency_value**: frequency value prescribe to the patient
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **agent_id**: ATC URI-code for drugs components. (e.g. https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **route_type**: child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (e.g. obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Medical intervention:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Intervention
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: 
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **process_type**: child of Intervention or Procedure http://purl.obolibrary.org/obo/NCIT_C25218 (ex: obo:Tumor Resection http://purl.obolibrary.org/obo/NCIT_C164212)
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **target_type**: child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **agent_id**: If any, ATC URI-code for drugs components. (example: https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **route_type**: in case of any, Child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (example: obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)

### Clinical trials:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Clinical_trial
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
- ![](https://placehold.co/15x15/808080/808080.png) **process_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **input_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **target_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **agent_id**: GUID for this medical center where this clinical trial is taking place.
- ![](https://placehold.co/15x15/808080/808080.png) **route_type**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same event (e.g.: under same visit occurrence or under certain diagnosis/phenotype relationship)