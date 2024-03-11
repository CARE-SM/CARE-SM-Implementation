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
    * `activity`: IRI-based ontological class that describes the patient's specific description related to the clinical procedure.
    * `unit`: IRI-based ontological class that describes the unit of `value` measurement.
    * `input`: IRI-based ontological class that describes the input of the patient procedure.
    * `target`:IRI-based ontological class that describes the target of the patient procedure.
    * `protocol_id`: IRI-based identifier that is used the define the protocol identifier.
    * `frequency_type`: IRI-based ontological class that describes the frequency of `value` presence.
    * `frequency_value`: Numerical value associated with the `frequency_type`
    * `agent`: GUID used to describe any agent that participates in the data entry
    * `startdate`: the start date of the observation process
    * `enddate`: the end date of the observation process
    * `age`: the age of the patient at time of observation
    * `comments` : free-text comments
    * `event_id`: a method for grouping observations together (explained elsewhere... one day!)

    Very few of this column names are present at all (or most) of the cases, but **it's not mandatory to provide all columns that exists in the CSV file, but it's forbidden to use other columns that the named above**. Each data element requires a subset of these columns to be filled, and the rest are 'null'.

    This is an example of an empty CSV file with the proper columns names:

    ```csv
    model,pid,event_id,value,age,value_datatype,valueIRI,activity,unit,input,target,protocol_id,frequency_type,frequency_value,agent,startdate,enddate,comments
    ,,,,,,,,,,,,,,,,,

    ```

2) Rename the CSV file as `preCARE.csv`. CARE-SM will recognize the name as the proper tagname and perform the quality control on it using `CARE-SM Toolkit`. This is why it's mandatory to create a single file because this is the one file it's going to be executed.

    

3) Populate your patient data elements

    Every data element requires a concrete set of column names to be populated. This is because not every clinical entry contains the same type of information.(e.g. a laboratory measurement needs to specify the targeting molecule to analyze, but a diagnosis assessment doesn't require defining any target). 

    <br>
    This is a glossary of every data requirement documentation:

    * Medical history and participation status:
        * [Birthdate](#birthdate) - Patient date of birth.
        * [Birthyear](#birthyear) - Year in which a person was born.
        * [Deathdate](#deathdate) -  Patient date of death.
        * [First confirmed visit](#first-confirmed-visit) - Patient first contact with specialized center.
        * [Participation status](#participation-status) - Patient healthcare participation status.
        * [Symptoms onset](#symptom-onset) - Patient signs/symptoms onset.

    * Demographic and questionnaire/PROMs representations:
        * [Sex](#sex) -  Patient sex at birth.
        * [Education level](#education) - Patient scholar level code measured by ISCED.
        * [Disability](#disability) - Patient disability score/assessment.
        * [Questionnaire](#questionnaire) - Generic questionnaire representation for any clinical question/PROM.

    * Conditions and findings assesments:
        * [Diagnosis](#diagnosis) - Patient disease diagnosis.
        * [Symptom/phenotype assessment](#symptoms-signs-or-phenotype-assessment) -  Patient symptom/phenotype assessment.

    * Clinical and molecular measurements:
        * [Laboratory measurement](#laboratory-measurement) - Patient laboratory measurements.
        * [Body measurement](#body-measurement) - Patient physical measurement of the body. 
        * [Medical imaging](#medical-imaging) -  Patient medical imaging data.
        * [Genetic variant](#genetic-sequence-variant) -  Genetic variant assessment.
        * [Zygosity](#genetic-variant-zygosity) -  Zygosity of a certain genetic variant.
        * [Protein variant](#protein-sequence-variant) -  Protein variant assessment.
        * [Aminoacid location](#protein-aminoacid-position) -  Position of a aminoacid in a certain protein chain.

    * Treatment-related assesments:
        * [Medication](#medication) - Patient drug administration based on a prescription.
        * [Surgical intervention](#surgery) -  Therapeutical interventation related to a surgerical procedure.

    * Research sample availability and consent:
        * [Biobank](#biobank) - availability of subject's samples in a biobank.
        * [Consent](#consent-for-being-contacted-for-research) -  consent given by a subject.

    * Clinical trials:
        * [Clinical trial](#clinical-trial) -  patient participation in clinical trial.

    <br>
    This is an example of functional `preCARE.csv` file that can be used with CARE-SM Toolkit,  both for `FAIR-in-a-box` software or Standalone implementation:

    ```csv
    model,pid,event_id,value,age,value_datatype,valueIRI,activity,unit,input,target,intensity,protocol_id,frequency_type,frequency_value,agent,route,startdate,enddate,comments
    Diagnosis,30056,,,,,http://www.orpha.net/ORDO/Orphanet_93552,,,,,,,,,,,2006-01-19,,

    ```

    Find more complete exemplar cases at [`exemplar_data`](/CSV/exemplar_data/README.md) folder.

## Data Element Glossary

#### **Legend:**

- ![](https://placehold.co/15x15/808080/808080.png) This column is **UNUSED** for this case.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) This column is filled in **IN CASE OF ANY**.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) This column colored is **REQUIRED** for this case.

Here you can find the list of data elements and the columns required to be defined. Those that are optional, feel free to add them. If not, leave them empty.

### Birthdate:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Birthdate
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: patient unique identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: ISO 8601 formatted date (not date time)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation, could be the same of the `value`
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/808080/808080.png) **age**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same visit occurrence event.

### Birthyear:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Birthdate
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: patient unique identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: The year in which a person was born. E.g. 1984
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/808080/808080.png) **startdate**:
- ![](https://placehold.co/15x15/808080/808080.png) **enddate**:
- ![](https://placehold.co/15x15/808080/808080.png) **age**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same visit occurrence event.

### Deathdate:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Deathdate
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: ISO 8601 formatted date of death (not date time)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation, could be the same of the `value`
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: Besides its named as "Deathdate", accepts "Age of Death" using this `age` column. Patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.


### First Confirmed Visit:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: First_visit
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: ISO 8601 formatted date of first confirmed visit (not date time). Its required to add at least one the following: `value` and/or `age` column (preferably `value`)
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation, could be the same of the `value`
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information. It's required to add at least one the following: `value` and/or `age` column (preferably `value`). Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Sex:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Sex
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: human readable label, e.g. Female
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: one of the following: 
    * http://purl.obolibrary.org/obo/NCIT_C16576 (Female) ; 
    * http://purl.obolibrary.org/obo/NCIT_C20197 (Male); 
    * http://purl.obolibrary.org/obo/NCIT_C124294 (Undetermined) ; 
    * http://purl.obolibrary.org/obo/NCIT_C17998 (Unknown, use this for foetal undetermined) 
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/808080/808080.png) **age**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.


### Participation status:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Status
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: any human readable response, e.g. Lost of follow-up
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: one of the following: 
    * http://semanticscience.org/resource/SIO_010059 (dead)
    * http://semanticscience.org/resource/SIO_010058 (alive)
    * http://purl.obolibrary.org/obo/NCIT_C70740 (lost to follow-up)
    * http://purl.obolibrary.org/obo/NCIT_C124784 (refused to participate)
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same visit occurrence event.

### Education:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Education
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: International Standard Classification of Education score. E.g. 7
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**: 
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**: 
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Symptoms, signs or phenotype assessment:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Symptom
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical phenotypic symptom or sign: For example Human Phenotype ontology (HPO) term represented with a full URL such as http://purl.obolibrary.org/obo/HP_0001251
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Diagnosis:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Diagnosis
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **value**: Human readable label of the diagnosed condition.
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
- ![](https://placehold.co/15x15/808080/808080.png)  **activity**:
- ![](https://placehold.co/15x15/808080/808080.png)  **unit**:
- ![](https://placehold.co/15x15/808080/808080.png)  **input**:
- ![](https://placehold.co/15x15/808080/808080.png)  **target**:
- ![](https://placehold.co/15x15/808080/808080.png)  **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Genetic sequence variant:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Genotype
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: human readable label that defines the genetic identifier. E.g. NM-004006.2:c.4375C>T p.(Arg1459*)
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: gene variant code constructed by appending the HGVS annotation, e.g. https://www.ncbi.nlm.nih.gov/clinvar/RCV000008537
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **activity**: Specific method in form of an ontological class that describe the process, e.g. NCIT:Microarray Analysis: http://purl.obolibrary.org/obo/NCIT_C18477
- ![](https://placehold.co/15x15/808080/808080.png)  **unit**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **input**: Anatomical structure where the sample was extracted. Recommended a child of NCIT:Biospecimen or NCIT:Anatomic Structure, System, or Substance, e.g. NCIT:Blood Sample: http://purl.obolibrary.org/obo/NCIT_C17610
- ![](https://placehold.co/15x15/808080/808080.png)  **target**:
- ![](https://placehold.co/15x15/808080/808080.png)  **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Genetic variant zygosity:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Zygosity
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: human readable label that defines zygosity. E.g. Homozygosity
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: One the following:
    - NCIT:Homozygosity: http://purl.obolibrary.org/obo/NCIT_C45826
    - NCIT:Hemizygosity: http://purl.obolibrary.org/obo/NCIT_C64346
    - NCIT:Heterozygosity: http://purl.obolibrary.org/obo/NCIT_C45825
    - NCIT:Nullizygosity: http://purl.obolibrary.org/obo/NCIT_C148063
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **activity**: Specific method in form of an ontological class that describe the process, e.g. NCIT:Microarray Analysis: http://purl.obolibrary.org/obo/NCIT_C18477
- ![](https://placehold.co/15x15/808080/808080.png)  **unit**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **input**: Anatomical structure where the sample was extracted. Recommended a child of NCIT:Biospecimen or NCIT:Anatomic Structure, System, or Substance, e.g. NCIT:Blood Sample: http://purl.obolibrary.org/obo/NCIT_C17610
- ![](https://placehold.co/15x15/808080/808080.png)  **target**:
- ![](https://placehold.co/15x15/808080/808080.png)  **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Protein sequence variant:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Protein
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: human readable label that defines the protein identifier. Example: GRCh38/hg38 7p22.3-q36.3(chr7:54185-159282390)x1
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **valueIRI**: protein variant code constructed by appending the HGVS/UniProt code, e.g. https://www.ncbi.nlm.nih.gov/clinvar/variation/146075/
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **activity**: Specific method in form of an ontological class that describe the process, e.g. NCIT:Protein Sequencing: http://purl.obolibrary.org/obo/NCIT_C18883
- ![](https://placehold.co/15x15/808080/808080.png)  **unit**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png)  **input**: Anatomical structure where the sample was extracted. Recommended a child of NCIT:Biospecimen or NCIT:Anatomic Structure, System, or Substance, e.g. NCIT:Blood Sample: http://purl.obolibrary.org/obo/NCIT_C17610
- ![](https://placehold.co/15x15/808080/808080.png)  **target**:
- ![](https://placehold.co/15x15/808080/808080.png)  **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Protein aminoacid position:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Aminoacid
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: Non-decimal numeric value that defines the position of the aminoacid. E.g. 13 
- ![](https://placehold.co/15x15/808080/808080.png)  **value_datatype**: 
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**: protein code constructed by appending the Uniprot code. E.g. https://www.uniprot.org/uniprotkb/Q8WWM7
- ![](https://placehold.co/15x15/808080/808080.png)  **activity**:
- ![](https://placehold.co/15x15/808080/808080.png)  **unit**:
- ![](https://placehold.co/15x15/808080/808080.png)  **input**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png)  **target**: CHEBI ontological term for the specific amino acid measured. E.g. http://purl.obolibrary.org/obo/CHEBI_15356
- ![](https://placehold.co/15x15/808080/808080.png)  **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png)  **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png)  **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Consent for being contacted for research:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Consent_contacted
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: some label describing consent outcome
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Consent for data (re)use permission:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Consent_used
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **value**: some label describing consent outcome
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Biobank:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Biobank
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **input**: Tissue/sample collected during the sampling process. E.g. Cerebrospinal Fluid http://purl.obolibrary.org/obo/NCIT_C12692
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **agent**: Biobank Identifier, e.g. https://directory.bbmri-eric.eu/biobankid
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Symptom Onset:

**This data element can be queried (for counting anonymized patient information) by Beacon API created for CARE-SM, for more information, click [here](https://github.com/CARE-SM/beaconAPI4CARESM)**

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Symptoms_omset
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: Age or date of ocurrence (It's not the same this temporal information than the one described as `startdate`/`enddate`/`age` for the time when this observation was registered) 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:date` for date or `xsd:integer`
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**: 
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **target**: URI based ontological term that defines symptom/phenotype measured, in case of any. E.g. HP ontological term for the symptom.
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Disability:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Disability
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: Score/value of the test output.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` por a decimal score.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **activity**: URL that defines the specific clinical questionnaire. Some examples are presented. E.g. http://purl.obolibrary.org/obo/NCIT_C107391  for Edmonton symptom disability assessment .
- ![](https://placehold.co/15x15/808080/808080.png) **unit**: 
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Questionnaire:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Questionnaire
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: Score/value of the test output.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` por a decimal score.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **activity**: URL that defines the specific clinical question defined in the questionnaire or PROM.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **unit**: IRI based unit of measuement ontological term, in case of any.
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**: 
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/808080/808080.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of this data elements under the same visit occurrence event.


### Body measurement:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Body_measurement
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: resulting value from this observation
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: child of Personal Attribute: http://purl.obolibrary.org/obo/NCIT_C19332
- ![](https://placehold.co/15x15/808080/808080.png) **activity**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **protocol_id**: URL reference to a protocol, e.g. https://protocols.io deposit or any identifier that describes the specific properties of this clinical procedure. E.g. https://www.protocols.io/view/hplc-sample-prep-4r3l25ew4l1y/v1
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Laboratory measurement:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Lab_measurement
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value**: resulting value from this analysis.
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**: 
- ![](https://placehold.co/15x15/808080/808080.png) **activity**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **input**: material input represented as Child of Anatomic, Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g: obo:Urine)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **target**: compound being measured in the sample. Child of Drug, Food, Chemical or Biomedical Material http://purl.obolibrary.org/obo/NCIT_C1908 (e.g. obo:Creatinine http://purl.obolibrary.org/obo/NCIT_C399)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **protocol_id**: URL reference to a protocol, e.g. https://protocols.io deposit or any identifier that describes the specific properties of this clinical procedure. E.g. https://www.protocols.io/view/hplc-sample-prep-4r3l25ew4l1y/v1
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Medical imaging:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Imaging
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: 
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: medical imagine GUID of the file (must be a GUID system compatible with RDF Resource identifiers)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **activity**: child of Imaging technique http://purl.obolibrary.org/obo/NCIT_C17369  (e.g. obo:Digital X-Ray http://purl.obolibrary.org/obo/NCIT_C18001)
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **target**: child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 (e.g. obo:Palmar Region http://purl.obolibrary.org/obo/NCIT_C33252)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **protocol_id**: URL reference to a protocol, e.g. https://protocols.io deposit or any identifier that describes the specific properties of this clinical procedure. E.g. https://www.protocols.io/view/anatomical-variations-and-dimensions-of-the-poplit-3byl4qqk8vo5
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/808080/808080.png) **agent**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Medication:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Medication
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: dose value prescribed to the patient
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: XSD datatype that defines `value` column type, e.g. `xsd:float` or `xsd:integer` for numerical values.
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**: 
- ![](https://placehold.co/15x15/808080/808080.png) **activity**: child of Route of Administration http://purl.obolibrary.org/obo/NCIT_C38114 (e.g. obo:Sublingual Route of Administration http://purl.obolibrary.org/obo/NCIT_C38300 )
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **unit**: child of UO:unit http://purl.obolibrary.org/obo/UO_0000000
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**: 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **protocol_id**: URL reference to a protocol, e.g. https://protocols.io deposit or any identifier that describes the specific properties of this clinical procedure. E.g. https://www.protocols.io/view/hplc-sample-prep-4r3l25ew4l1y/v1
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **frequency_type**: child of obo:Temporal Qualifier http://purl.obolibrary.org/obo/NCIT_C21514 (e.g. obo:Per Day)
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **frequency_value**: frequency value prescribe to the patient
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **agent**: ATC URI-code for drugs components. (e.g. <https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Surgery:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Surgery
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**: 
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**:
- ![](https://placehold.co/15x15/808080/808080.png) **valueIRI**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **activity**: child of Intervention or Procedure http://purl.obolibrary.org/obo/NCIT_C25218 (ex: obo:Tumor Resection http://purl.obolibrary.org/obo/NCIT_C164212)
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **target**: child of Anatomic Structure, System, or Substance http://purl.obolibrary.org/obo/NCIT_C12219 
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **protocol_id**: URL reference to a protocol, e.g. https://protocols.io deposit or any identifier that describes the specific properties of this clinical procedure. E.g. https://www.protocols.io/view/hplc-sample-prep-4r3l25ew4l1y/v1
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **agent**: If any, ATC URI-code for drugs components. (example: <https://www.whocc.no/atc_ddd_index/?code=A07EA01)
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `value`/`startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.

### Clinical trial:

- ![](https://placehold.co/15x15/1589F0/1589F0.png) **model**: Clinical_trial
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **pid**: individual identifier, in the form of a patient identifier.
- ![](https://placehold.co/15x15/808080/808080.png) **value**:
- ![](https://placehold.co/15x15/808080/808080.png) **value_datatype**: 
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **valueIRI**: IRI that defines clinical condition as disease or disorder: Orphanet disease ontology (ORDO) represented with a full URL such as http://www.orpha.net/ORDO/Orphanet_199630
- ![](https://placehold.co/15x15/808080/808080.png) **activity**:
- ![](https://placehold.co/15x15/808080/808080.png) **unit**:
- ![](https://placehold.co/15x15/808080/808080.png) **input**:
- ![](https://placehold.co/15x15/808080/808080.png) **target**:
- ![](https://placehold.co/15x15/808080/808080.png) **protocol_id**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_type**:
- ![](https://placehold.co/15x15/808080/808080.png) **frequency_value**:
- ![](https://placehold.co/15x15/1589F0/1589F0.png) **agent**: GUID for this medical center where this clinical trial is taking place.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **startdate**: ISO 8601 formatted start date of observation
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **enddate**: ISO 8601 formatted enddate of observation in case it is different from `startdate`.  
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **age**: patient age when this observation was taken, this age information can be both an addition or an alternative for `startdate`/`enddate` information. Its units are fractional years, so it accepts any decimal figure for age. E.g. 33.75 years.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **comments**: human readable comments of any kind related to this procedure.
- ![](https://placehold.co/15x15/fb9902/fb9902.png) **event_id**: contextual identifier (formatted as `integer`) used for relating several of these data elements under the same visit occurrence event.