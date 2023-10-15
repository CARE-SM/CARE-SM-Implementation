# CARE Semantic Model Implementation
**Repository dedicated to explore workflows for CARE-SM implementation**

<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM_logo.png"width="200" height="200"> 
<p align="center" > </p> 

<hr>

* [Quick start](#quick-start)
* [EJP proposed implementation](#ejp-rd-proposed-implementation)
    * [FAIR-in-a-box](#fair-in-a-box-solution)
    * [Standalone implementation](#standalone-implementation)

<hr>

# Quick start
To jump directly to the "just tell me what I have to do to make this work", please [follow this link](https://github.com/ejp-rd-vp/FiaB/tree/main/CDE%20Version2%20Models%20FiaB).

If you want to understand more deeply what you are doing, read on!

# EJP-RD proposed implementation

[CARE Semantic Model](https://github.com/CARE-SM/CARE-Semantic-Model) defines a set of clinical data elements used in the healthcare domain of knowledge. However, it doesn't specify a mechanism for bringing these to life. 

The proposed implementation workflow consumes CSV tables as the primary data source. Each row within these tables represents an individual module or data element. The required information for generating each module is defined within a set of columns. For instance, the diagnosis module requires several distinct columns, including those for patient identifier, diagnosis date, and the IRI used for disease definition. Every individual module is concatenated within at a common CSV file. A predefined set of common column names is used to reference each specific clinical entry.

These columns are referenced in a template, which defines the structure of the resulting RDF shape. These templates are formulated in [YARRRML](https://rml.io/yarrrml/spec/), a versatile templating language capable of defining the RDF structure and uses  the column names to referes the CSV data and create a complete RDF representation. For the European Joint Project for Rare Diseases (EJPRD) we propose an implementation pipeline that can be described as follows:


<p align="center"> 
	<img src="/EJP_CARESM_workflow.png"> 
<p align="center" ><b>Figure 1: EJP-RD CARE-SM implementation </b></p>


First, CSV data table is created, following a common template spanning all types of patient data. Each row is an observation, and depending on the type of observation different columns of the template must be filled (as its explained above). The required columns are defined by an [data element glossary](/CSV/doc/), explaining which columns are required to be filled and a datatype description. Alongside this standard CSV template is a [YARRRML template](/YARRRML/) that defines the final RDF shape based on the CARE semantic model. This YARRRML template is provided.

In the full EJP implementation, sitting between this common CSV and the YARRRML, is an additional step that modifies the template CSV to add additional fields and automatically make certain translations that reduce the complexity and burden on the data provider.  This translation is executed by a component called [CARE-SM Toolkit](https://github.com/CARE-SM/CARE-SM-Toolkit) (_note: it is not necessary to understand the functionality of this component to fully take advantage of the EJP pipeline!_) It is this final, much richer CSV file that is used by the YARRRML to do the final RDF transformation. 

## FAIR-in-a-box solution

This whole pipeline have been implemented using [FAIR-in-a-box software (FiaB)](https://github.com/ejp-rd-vp/FiaB). Please visit [this page](https://github.com/ejp-rd-vp/FiaB/tree/main/CDE%20Version2%20Models%20FiaB) to know more about this details and how to use it.

## Standalone implementation

From those who are not interested in using FAIR-in-a-box or interested in exploring every step in the workflow locally. You have the option to perform RDF transformations locally, without relying on the FAIR-in-a-box toolkit. To support this process, we have developed Docker compose images that cover the entire transformation pipeline. ([Figure 1]())

1) **YARRRML and CSV preparation:**

First, use our YARRRML template or create your own. You might use our [YARRRML template builder](https://github.com/pabloalarconm/EMbuilder). Save the template as {TAGNAME}_yarrrml.yaml and place it in the ./data folder, for example, "height_yarrrml.yaml".

In the same ./data folder, create a CSV file with the required headings for your desired transformation, you might use the following guidelines provided in the [accompanying documentation](/CSV/doc/). Save the file as {TAGNAME}.csv, e.g., "height.csv". 

The {TAGNAME} serves as a coordinating identifier among various components during the automation steps and must precisely match the "tag" portion of the template name.

2) **Folder distribution:**
```bash
.
./data/
./data/{TAGNAME}.csv  # Input CSV file,  TAGNAME explained above
./data/{TAGNAME}_yarrrml.yaml # YARRRML template, TAGNAME explained above
./data/triples/  # Output RDF data ends up here, this folder will be automatically created.
./docker-compose.yaml # Docker image that will execute the transformation (see step 3 below)
```

3) **RDF transformation execution:**

You can use Docker compose to run the services:

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

Once this services are running, call in your local browser this link: http://127.0.0.1:4567/{TAGNAME} (where {TAGNAME} is the data/template tag name, as in the examples above, like "height"). RDF file should be created a `./data/triples` folder.
