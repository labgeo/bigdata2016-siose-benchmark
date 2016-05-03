### Should EU Land Use and Land Cover data be managed with a NoSQL document store?
##### A benchmark of an implementation of the Spanish Land Use Database (SIOSE) using the PostgreSQL binary JSON data type
  
<small>José Tomás Navarro    {<i class="fa fa-envelope"></i> jt.navarro@ua.es,  <i class="fa fa-github"></i> @quommit}</small>  
<small>Benito Zaragozí    {<i class="fa fa-envelope"></i> benito.zaragozi@ua.es,  <i class="fa fa-github"></i> @benizar}</small>  
<small>Alfredo Ramón    {<i class="fa fa-envelope"></i>  alfredo.ramon@ua.es}</small>  
<small>Nuria Valcárcel    {<i class="fa fa-envelope"></i>  nvalcarcel@fomento.es}</small>  
![ign](http://labgeo.github.io/bigdata2016-siose-benchmark/img/iig-ign.jpg)
<small>Wessex Institute International Conference on Big Data, Alicante, 3-5 May 2016</small>

Note:
My name is J.T. Navarro and I presently work as a research fellow for the University of Alicante Geomatics Lab at the Geography Institute. I am here to present a recent computational experiment on land-use and land-cover document stores. For this particular experiment we designed and run a benchmark of an implementation of SIOSE, which is the acronym of the Spanish Land-Use Database, using the Postgre-Sequel binary Jayson data type.



### Contents
-  Land Use and Land Cover EU joint initiatives
-  Benchmarking the Spanish Land Use Database (SIOSE): relational vs document store
-  Conducting a reproducible computational experiment: a DevOps approach
-  Benchmark results
-  Potential of land use document stores

Note:
We are in our way to assemble a research group with interests in applying innovative database technology to land-use geographical databases. In practice, we seek to empower the usability of these databases so that professionals coming from different backgrounds are able to fully exploit them, no matter their level of GIS expertise. In this preliminary research on land-use and land-cover document stores, we attempted to scope the European Union joint efforts in building a common framework for land-use information systems, and focused on SIOSE as one product of this endeavour. As a starting point, we decided to benchmark SIOSE using a document-oriented implementation against the reference implementation, whose physical model is relational. The computational experiment was devised with reproducibility in mind so that SIOSE administrators could replicate and extend tests using container-based virtualisation. Early benchmark results were obtained using Postgre- Sequel for both, relational and document-oriented implementations. From these results we concluded that document stores show some strengths which can boost massive land-use data visualisation and analysis.



### Land Use and Land Cover (LU/LC)
![lulc](http://labgeo.github.io/bigdata2016-siose-benchmark/img/lulc.png)

Note:
When we define the land-cover on a particular area we depict landscape according to some structural and biophysical properties of elements seen on surface such as spatial distribution, vegetation or buildings. In contrast, land-use relates to manpower pressure on landscape, resource explotation and social or economic function. For instance, here we can see a somewhat uniform area for which land-cover may be defined as a farming mosaic landscape of citrus crops and pastures. On the other hand, as far as land-use is concerned, there is evidence of irrigated lands.



### EU Land Monitoring activity
![eu-land-monitoring](http://labgeo.github.io/bigdata2016-siose-benchmark/img/eu-land-monitoring.png)

Note:
Land use change is an indicator of environmental problems such as over-exploitation, biodiversity loss or climate change. Land-use monitoring is, therefore, a key aspect throughout European Union long-term environmental policies. Copernicus, the European Spatial Agency earth observation programme, serves as the general framework for several projects and inventories recorded at regional, state and european levels. To date, and given the lack of compulsory regulation, the Harmonised European Land Monitoring or HELM project, stands out as the strongest coordination effort among European Union members. The HELM project determined how state and regional land-related data should be aggregated into pan-European data systems, such as Corine Land Cover and Eurostat Land Use and Cover Area Frame Survey. Corine Land Cover makes up the target reference classification system for land-use map data gathered by states, which may internally use their own land-use categorisation scheme. This is the case of LISA in Austria or SIOSE in Spain, to name a few. In order to reconcile approaches and contributions from different state agencies there is an ongoing proposal for a common land-use data model by the EAGLE group at the European Environment Agency. The EAGLE concept integrates and extends two technical guidelines laid out by the European Comission INSPIRE directive, namely land-use and land-cover data specifications.



### SIOSE Object Oriented Data Model
![siose-uml](http://labgeo.github.io/bigdata2016-siose-benchmark/img/siose-uml.png)

Note:
I will focus now on SIOSE as the target land use database of this benchmark. SIOSE is coordinated by the National Geographical Institute in colaboration with public agencies in charge of preparing official cartography for each of the 19 spanish autonomous regions. SIOSE defines an object oriented data model instead of a fixed classification system. Therefore, SIOSE is in line with INSPIRE data specifications and the EAGLE concept, while also ensuring compatibility with Corine Land Cover. The mapping elements in SIOSE are two-dimensional vector polygons with minimum area ranging between five thousand and twenty thousand square metres. Polygons may be categorised according to multiple criteria using photographic and satellite image interpretation. So, in practice, there are simple cover and composite cover polygons. Within the latter, a particular spatial distribution is identified, and each component cover is assigned its area percentage value. A cover may in turn have child covers and also have attributes, some of which belong to the realm of land-use.



### SIOSE Physical Model
![siose-mf2](http://labgeo.github.io/bigdata2016-siose-benchmark/img/siose-mf2.png)

Note:
SIOSE is downloadable as a set of relational database files, namely GIS shapefiles for polygons and Microsoft JET MDB files for cover values. As to year 2005 inventory, which is our target database, roughly two and a half million polygons and more than 10 million cover values were recorded. Thus, GIS users are provided with suitable data for their desktops out-of-the-box. However, usability is affected by the need to join polygon geometries with the values table, which, in turn, implements composite covers by means of adjacency lists. Although an extensive guide on how to solve common use cases is provided, non-expert database users may encounter this physical model unsuitable to fulfill their research goals by leveraging their skills.



### Transform into document store
![siose-docstore](http://labgeo.github.io/bigdata2016-siose-benchmark/img/siose-docstore.png)

Note:
Transforming the former SIOSE physical model into a Postgre Sequel document store which supports spatial search basically meant keeping the vector polygons table plus an additional binary Jayson field where land-cover values were stored as documents. With regard to composite covers, the Jayson document translates the original adjacency list as nested elements in the document tree.



### Research goals
-  Run two equivalent sets of massive bounding box queries on twin PostgreSQL instances
  -  Reference instance: SIOSE relational model
  -  Benchmark instance: SIOSE document store based on binary JSON (JSONB)
-  Get response time and throughput
-  Results must be comparable: same spatial access method throughout the experiment
-  Elucidate query qualifications for which JSONB is more performant

Note:
The benchmark essentially involved a performace test where predefined bounding box search queries were run on the SIOSE relational model and compared with their counterparts on a document-oriented model using Postgre Sequel binary Jayson data type. Grids with varying spatial resolution were generated and used as iterative scenarios. Twin Postgres Sequel instances were launched, one for each model. By constraining ourselves to a common database system we pursued fully comparable response time and throughput values, since the same query processor and spatial access method, that is to say an R-Tree index, will be used throughout the experiment. Finally, we expected to check out those query qualification categories for which a document store should be considered with regard to performance.



### Experimental setup
![devops](http://labgeo.github.io/bigdata2016-siose-benchmark/img/devops.png)

Note:
In order for this experiment to be replicated, we adopted a development operations approach. A data loader bash script was prepared to get a Postgre Sequel database dump of the full SIOSE 2005 dataset using the Geospatial Data Access Library. A binary Docker image was also built based on the official Postgre Sequel 9.5 image and expanded to compile and install PostGIS 2.1 geospatial extension. We wrote an additional bash script to further automate deployment, so that, given the dump file and the Docker image, a Postgre Sequel Docker container could be launched and a raw SIOSE database restored on a Docker volume. The benchmark was run using two identical containers and tests were, therefore, executed in two isolated environments: one container for querying the relational model, and another one for the document store. All operations run in the database server were provided as simple Sequel scripts, including grid generation, schema and data normalisation, conversion to binary Jayson and the queries which made up this benchmark. Each query plan was recorded into a log table upon execution, so that response times could be later aggregated and compared.



### Neat reproducibility
  
```
$ docker run -d -e POSTGRES_PASSWORD=postgres labgeo/pg_siose_bench
$ psql -h localhost -p 5432 -d siose2005 -U postgres
siose2005=# CREATE EXTENSION pg_siose_bench;
```  
  
A single image in Docker Hub to get:  
**PostgreSQL server** + **SIOSE 2005 database** + **benchmark sources packaged in one PostgreSQL extension**

Note:
As of today, we went one step further to make the computational experiment easily reproducible to any researcher. There is a publicly available image in Docker Hub which gets built automatically and allows users to launch Postgre Sequel containers that already provide the SIOSE 2005 geographical database and all benchmark sources packaged as a Postgre Sequel extension. This means the whole benchmark environment may be reproduced by simply executing the docker run command.



### Test suite
<small>LU/LC Condition</small> | <small>Query ID</small> | <small>Description</small>
------------------------------ | ----------------------- | --------------------------
<small>cover equals</small>                                  | <small>coniferous</small>       | <small>Select polygons with coniferous cover.</small>
<small>cover equals AND area greater than</small>            | <small>large_coniferous</small> | <small>Select polygons with coniferous coverage greater than 10,000 m².</small>
<small>attribute equals OR attribute equals</small>          | <small>reforested</small>       | <small>Select polygons with forest coverage originating from plantation or agricultural abandonment.</small>
<small>cover equals AND parent(cover) equals</small>         | <small>scattered_urb</small>    | <small>Select polygons with scattered urbanisation coverage.</small>
<small>IF cover equals THEN sum(area)</small>                | <small>area_coniferous</small>  | <small>Sum all areas of coniferous plantations.</small>
<small>IF cover equals THEN reclass(area_percentage)</small> | <small>reclass</small>          | <small>Reclassify all polygons into 4 density class categories based on conifer percentage (0-25%, 25-50%, 50-75% and 75-100%). Discard polygons with no coniferous cover.</small>  
  
**Bounding box search configuration**  
  
<small>Grid levels of detail </small> | <small>Total grid cells</small> | <small>Iterations per cell</small>
------------------------------------- | ------------------------------- | ----------------------------------
<small>10k 25k 50k 100k 200k 500k 1M</small> | <small>56,557</small> | <small>4</small>

Note:
As to the test suite, a set of six bounding box search queries were prepared. The featured qualifiers were polygon selection by cover or attribute, area aggregation by cover and, finally, polygon reclassification by cover area percentage. The focus was set on forest covers since we were after common queries in environmental and risk management studies. With regard to the predefined grids, the tessellation function provides graticule scenarios overlapping Spain's mainland and islands at seven resolutions, ranging from 5 to 500 kilometres wide on a standard sixteen nineth desktop screen.



### Benchmark results
![charts](http://labgeo.github.io/bigdata2016-siose-benchmark/img/charts.png)

Note:
Let's have a look at benchmark results. Comparative line charts plot average response times by query and grid, while throughput boxplots show average polygons per millisecond grouped by query. The simple query by cover, which, in our case, selects polygons where coniferous forests exist, rendered better response times on the document-oriented model. So did the scattered urbanisation query, which is slightly more complex since it runs a cover in cover qualifier, that is to say, evaluates a parent and child relationship. These queries achieved best average throughput and biggest gains with regard to their counterparts in the relational model, as seen on the corresponding boxplots. The reclassification query also performs better on the binary Jayson store, although execution time gains tend to decrease at lower levels of detail. As to land-use attribute and area aggregation queries, differences are less significant. In contrast, the query by cover and attribute, which selects polygons where coniferous forests greater than 10,000 square metres exist, runs progressively slower at smaller scales on the document store, thus rendering better overall performance on the relational model.

