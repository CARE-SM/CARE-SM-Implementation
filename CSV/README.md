## CSV Documentation

This workflow is specifically designed to process CSV-formatted files containing a multitude of data elements. Each data element must follow a precise be precisely structured with column names and information disposition.

[YARRRML templates](/YARRRML/) utilize column name references to map and transform the data into a designated RDF structure. Therefore, it is crucial to correctly associate the data with the appropriate columns and datatypes to generate RDF-based CDE-oriented patient data.


Every data element defined by the European Joint Project - Rare Diseases and other use cases are described at this [documentation](/CSV/doc/) in which defines a set of sufficient columns to be represented.

## Exemplar CARE CSV data

You can also find an exemplar patient data table **before and after** using CARE-SM Toolkit implementation at [exemplar_data](/CSV/exemplar_data/) folder.

## CARE-SM Toolkit

Before running any RDF tranformation of our CSV data table. Some quality controls are required to make sure every data element is properly represented and described. Also, this step modifies the template CSV to add additional fields and automatically make certain translations that reduce the complexity and burden on the data provider.

To perform this particular and critical step, CARE-SM Toolkit is created. The primary transformation carried out includes:

* Adding every domain specific ontological term required to define every instances of the model, these terms are specific for every data element.

* Splitting the column labeled as `value` into distinct datatypes. This enables YARRRML to interpret each datatype differently, facilitating the subsequent processing.

* Conducting a sanity check on the date-based column names (as `date`, `stardate` and `enddate`) to ensure data consistency and validity.

* Eliminating any input rows that lack of the minimal required data to minimize the generation of incomplete RDF transformations.

* Creation of the column called `uniqid` that assigns a unique identifier to each observation. This prevents the RDF instances from overlapping with one another, ensuring their distinctiveness and integrity.

In conclusion, the implementation of the CARE Semantic Model for CSV data entails a meticulous and technically advanced workflow. By leveraging the power of the YARRRML templates and incorporating the critical curation step executed by the Hefesto toolkit, this implementation achieves robustness, accuracy, and reliability in generating RDF-based patient data.

For more information about CARE-SM Toolkit, please check the [Github repository](https://github.com/CARE-SM/CARE-SM-Toolkit).