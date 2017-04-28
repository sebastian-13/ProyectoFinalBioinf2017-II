#Avance_2 trabajo final.md

**Combosch DJ, Vollmer SV (2015). Data from: Trans-Pacific RAD-Seq population genomics confirms introgressive hybridization in Eastern Pacific Pocillopora corals. http://dx.doi.org/10.5061/dryad.436h0**


*En primera instancia, respondiendo al comentario de Alicia creo que es importante el hacer un ensamble a partir de un genoma de referencia aunque pertenezca al equipo oyamel porque como nunca he manejado datos ni softwares de nueva generación quiero meterme con calma y paulatinamente en estos temas y deseo aplicar los programas y las ideas de clase.*

*En segunda instancia en respuesta a Azalea si voy a intentar hacer análisis de firmas de selección además de los resultados de selección.*

*En tercera instancia cambié los datos por unos datos de unos corales porque los genomas no son tan grandes y ya tengo varios individuos y dos genomas de referencia*

_________________

###Análisis a trabajar en el proyecto

Con base en la información obtenida a partir de los archivos archivos de tres especies del género Pocillopora se plantea analizar entre los genomas de *P. damicornis*, *P. eydouxi* y *P. elegans*. 


####Querido diario luego de una charla con la Dra Mastretta he logrado tener unas ideas más claras en especial luego de revisar un par de manuales y leer papers. La idea global está en hacer un ensamble utilizando datos de las especies propuestas inicialmente. Soy conciente de que en el presente deseo trabajar con datos de transcritos pero por lo pronto quiero aplicar varios de los conceptos tratados en clases en datos genómicos.

______________


**Los papers revisados en este rato son:**

>_1-_ Wagner K., Keller I., Wittwer S., Selz O., Mwaiko S., Greuter., Sivasundar A., y Seehausen O. 2013. Genome-wide RAD sequence data provide unprecedented resolution of species boundaries relationship in the Lake Victoria cichlid adaptive radiation. Molecular Ecology 22, 787-798. 

>*Analisis:* La idea es aplicar la metodología de genómica poblacional usando secuenciación de nueva generación (NGS). Los datos se utilizan para inferir relaciones filogenéticas entre especies en Cíclidos que se encuentran hubicados en el Lago Victoria que presentan gran variación entre especies. Los patrones generalmente se atribuyen a una radiación temprana. Finalmente se determina la presencia de monofilia entre los grupos genéticos utilizados  y se discute de la importancia de NGS para resolver problemas filogenéticos


>_2-_ Combosch D., Vollmer S. 2015. Trans-Pacific RAD-Seq population genomics confirms introgressive hybridization in Eastern Pacific Pocillopora corals. Molecular Phylogenetics and Evoltion. 

>*Análisis:* A causa de la discrepancia en la taxonomia basada en la morfología en los corales del género Polliopora y que se sugiere introgreción genética y posterior hibridización entre especies. Por lo mismo se hace un análisis de RADseq entre y dentro de las poblaciones de tres especies. Finalmente se observa que los  patrones de introgresión genética han generado  linages polifiléticos dentro del género.


>_3-_ Abdelkrim P., Gey V., France SC, Boisselier MC and S Samadi. 2014. Use of RAD sequencing for delimiting species. Heredity 1-10. 

>*Análisis:* Dentro del paper sugieren a RAD-tag como un método prominente para los estudios evolutivos en todo el genoma y de esta forma en el momento de delimitar especies, un modelo claro para hacerlo son los corales porque pocos marcadores molecules han funcionado. Se utilizan RAD mitocondrial a partir de dos análisis pipelines (con Stacks y PyRAD). La delimitación de especies es soportada en los clados, además de ello se encuentra que la divergencia genética se correlaciona con la estructura 


>_4-_ Davey J., Cezard K., Fuentes-Utrilla P., Eland C., Gharbi K. y Blaxter M. L. 2013. Special features of RAD Sequencing data: implications for genotyping. Molecular Ecology. 22, 3151-3164.  

>*Análisis:* Restriction site-associated DNA Sequencing (RAD-Seq) es un método común para detectar SNP y genotipificarlos. Esta metodología produce un conteo estocástico y requiere de análisis de sencibilidad. En el paper se muestran formas de errar en el genotipeo también en sitios de restricción heterocigotos. Ellos exploran los diferentes análisis


>_5-_ Richards P., Liu M., Lowe N., Davey J., Blaxter M., y Davison A. 2013. RAD-Seq derived markers flank the shell colour and banding loci of the Cepaea nemoralis supergene. Molecular Ecology.

>*Análisis:* Son clásicos los estudios con base en la coloración y los patrones de bandeo en la concha, lo cual se ha interpretado como un caracter blanco de la selección natural. Siendo que la variación fenotípica en el bandeo se debe a "super genes" que ya se han descrito y se encuentran ligados. Con base en esto se realizaron cruzas con la idea de determinar genotipos de las descendencias por medio de marcadores RADseq

__________________ 


*Se está haciendo una revisión del manual: Manejo y análisis de datos de secuenciación masiva de ADN.* 


**En el artículo base manejan los datos RAD-seq de ocho invididuos que se encuentran separados individualmente, lo anterior evita la necesidad de hacer un multiplexeo de datos**

**La calidad de cada uno de los archivos en formato FASQ (xxx.fq) se revisa en el software FASQC**

**Remover bases mal identificadas en FASTXtools o Trimmomatic** 

**Se va a hacer un mapeo de lecturas con el software BWA utilizando como base de los dos genomas de referencias encontrados en la base de datos NCBI los cuales pertenecen a las especies Pseudodiploria strigosa y Orbicella faveolata.  **

*Ya he descargado y me encuentro estudiando el manual de Stacks que es el software que utilizaré para alinear*

*Por lo pronto ya me encuentro realizando la lectura de los manuales de bwa, samstools y vcftools o bcftool con la idea de manipular bien los diferentes comandos y seguir realizando los análisis del proyecto de la clase*  






