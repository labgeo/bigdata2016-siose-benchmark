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
