# CARE Semantic Model Implementation
**Repository dedicated to explore workflows for CARE-SM implementation**

<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM_logo.png"width="200" height="200"> 
<p align="center" > </p> 

<hr>

* [Quick start](#quick-start)
* [Implementation workflows](#implementation-workflows)
    * [FAIR-in-a-box software](#fair-in-a-box-software)
    * [Standalone implementation](#standalone-implementation)
* [Exemplar data](#exemplar-csv-templates)
* [CARE-SM Toolkit](#care-sm-toolkit)

<hr>

# Quick start
To jump directly to the "just tell me what I have to do to make this work" using FAIR-in-a-box software, please [follow this link](https://github.com/ejp-rd-vp/FiaB/blob/main/CARE-SM_FiaB/README.md).

If you want to understand more deeply what you are doing, read on!

# Implementation workflows

[CARE Semantic Model](https://github.com/CARE-SM/CARE-Semantic-Model) defines a set of clinical data elements used in the healthcare domain of knowledge. However, it doesn't specify a mechanism for bringing these to life. 

The proposed implementation workflows (both EJPRD and Standalone) consumes CSV tables as the primary data source. Each row within these tables represents an individual module or data element. The required information for generating each module is defined within a set of columns. For instance, the diagnosis module requires several distinct columns, including those for patient identifier, diagnosis date, and the IRI used for disease definition. Every individual module is concatenated within a common CSV file. A predefined set of common column names is used to reference each specific clinical entry.

These columns are referenced in a template, which defines the structure of the resulting RDF shape. These templates are formulated in [YARRRML](https://rml.io/yarrrml/spec/), a versatile templating language capable of defining the RDF structure and uses the column names to reference the CSV data and create a complete RDF representation.


From the [European Joint Project on Rare Diseases (EJP-RD)](https://www.ejprarediseases.org/) initiative, a set of technologies and softwares have been created, capable of consuming data tables into RDF data representation. [FAIR-in-a-box](https://github.com/ejp-rd-vp/FiaB) has implemented a whole pipeline for patient-based data using CARE-SM. Same technologies can be used outside FAIR-in-a-box software in a standalone implementation.


## FAIR-in-a-box software

FAIR-in-a-box solution is explained out of this repository, please [follow this link](https://github.com/ejp-rd-vp/FiaB)

## Standalone implementation

From those who are not interested in using FAIR-in-a-box or interested in exploring every step in the workflow locally. You have the option to perform RDF transformations locally, without relying on the FAIR-in-a-box solution. To support this process, we have developed Docker compose images that cover the entire transformation pipeline. The standalone implementation can be described as follows:


<p align="center"> 
	<img src="/CARE-SM_workflow.png"> 
<p align="center" ><b>Figure 1: Standalone CARE-SM implementation </b></p>

1) **CSV template creation:** First, a CSV data template is created. This template is defined by a [data element glossary](), explaining which columns are required to be filled in every data element. Each row is an observation, and depending on the type of observation different columns of the template must be filled (as explained above). Rename your CSV file as `preCARE.csv`.

2) **Quality control**: After creating this CSV template with the patient data on it, this CSV template needs to be adapted to YARRRML template before performing RDF transformation. This modification add additional fields and automatically make certain translations that reduce the complexity and burden on the data provider. This translation is executed by a component called [CARE-SM Toolkit](#care-sm-toolkit). CARE-SM Toolkit will transform your `preCARE.csv` to the curated CSV template called `CARE.csv` (green box from [Figure 1]()). It is this final, much richer CSV file that is used by the YARRRML to do the final RDF transformation.

3) **YARRRML template**: Alongside this standard CSV template, a YARRRML template defines the final RDF shape based on the CARE semantic model. This YARRRML template is provided [here](#standalone-implementation) at this repository. This YARRRML templates was created by using [EMbuilder YARRRML template builder](https://github.com/pabloalarconm/EMbuilder)


5) **Folder distribution:**
```bash
.
./data/
./data/CARE.csv  # CSV data file, explained above
./data/YARRRML_yarrrml.yaml # YARRRML template, explained above
./data/triples/  # Output RDF data ends up here, this folder will be automatically created.
./docker-compose.yaml # Docker image that will execute the transformation (step below)
```

5) **RDF transformation execution:**

You can use Docker compose to run the services (red box from [Figure 1](#standalone-implementation))

```yaml
version: "3"
services:
  yarrml-rdfizer:
    image: markw/yarrrml-rml-ejp:0.0.2
    container_name: yarrrml-rdfizer
    environment:
      # (nquads (default), trig, trix, jsonld, hdt, turtle)
      - SERIALIZATION=nquads
    ports:
      - "4567:4567"
    volumes:
      - ./data:/mnt/data
```

Once this services are running, call in your local browser this link: http://127.0.0.1:4567/CARE
The RDF file should be created at ./data/triples` folder.

## Exemplar CSV templates

You can also find an exemplar patient data table **before and after** using CARE-SM Toolkit implementation at [exemplar_data](/CSV/exemplar_data/README.md) folder.

## CARE-SM Toolkit

Before running any RDF transformation of our CSV data table. Some quality controls are required to make sure every data element is properly represented and described. Also, this step modifies the template CSV to add additional fields and automatically make certain translations that reduce the complexity and burden on the data provider.

To perform this particular and critical step, CARE-SM Toolkit is created. The primary transformation carried out includes:

* Adding every domain specific ontological term required to define every instance of the model, these terms are specific for every data element.

* Splitting the column labeled as `value` into distinct data types. This enables YARRRML to interpret each data type differently, facilitating the subsequent processing.

* Conducting a sanity check on the date-based column names (as `date`, `startdate` and `enddate`) to ensure data consistency and validity.

* Eliminating any input rows that lack the minimal required data to minimize the generation of incomplete RDF transformations.

* Creation of the column called `uniqid` that assigns a unique identifier to each observation. This prevents the RDF instances from overlapping with one another, ensuring their distinctiveness and integrity.

In conclusion, the implementation of the CARE Semantic Model for CSV data entails a meticulous and technically advanced workflow. By leveraging the power of the YARRRML templates and incorporating the critical curation step executed by the Hefesto toolkit, this implementation achieves robustness, accuracy, and reliability in generating RDF-based patient data.

For more information about CARE-SM Toolkit, please check the [Github repository](https://github.com/CARE-SM/CARE-SM-Toolkit).

