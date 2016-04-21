### Shoud EU Land Use and Land Cover data be managed with a NoSQL document store?
##### A benchmark of an implementation of the Spanish Land Use Database (SIOSE) using the PostgreSQL binary JSON data type
  
<small>José Tomás Navarro    {<i class="fa fa-envelope"></i> jt.navarro@ua.es,  <i class="fa fa-github"></i> @quommit}</small>  
<small>Benito Zaragozí    {<i class="fa fa-envelope"></i> benito.zaragozi@ua.es,  <i class="fa fa-github"></i> @benizar}</small>  
<small>Alfredo Ramón    {<i class="fa fa-envelope"></i>  alfredo.ramon@ua.es}</small>  
<small>Nuria Valcárcel    {<i class="fa fa-envelope"></i>  nvalcarcel@fomento.es}</small>  
![ign](http://labgeo.github.io/bigdata2016-siose-benchmark/img/iig-ign.jpg)
<small>Wessex Institute International Conference on Big Data, Alicante, 3-5 May 2016</small>



### Contents
-  Land Use and Land Cover EU joint initiatives
-  Benchmarking the Spanish Land Use Database (SIOSE): relational vs document store
-  Conducting a reproducible computational experiment: a DevOps approach
-  Benchmark results
-  Potential of land use document stores

Note:
We are in our way to assemble a research group with interests in applying innovative database technology to land use and land cover geographical databases in order to empower their usability by practitioners coming from different backgrounds. In this preliminary research on land use and land cover document stores we attempted to scope the European Union joint efforts in building a common framework for land use information systems and focused on SIOSE, the Spanish Land Use Database, as one product of this endeavour. As a starting point, we decided to benchmark SIOSE using a document-oriented implementation against the reference implementation, whose physical model is relational. The computational experiment was devised with reproducibility in mind so that SIOSE administrators could replicate and extend tests using container-based virtualization. Early  benchmark results were obtained using PostgreSQL for both, relational and document-oriented implementations. From these results we concluded that document stores show some strengths which can boost massive land use data visualisation and analysis.

