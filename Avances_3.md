#Avances 3
=====================

Querido diario en esta ocación decidí organizar las cosas por partes para tener las ideas claras en mi cabeza. En segunda instancia  acompañado de cada uno de los items que viene a continuación hay un archivo tipo [README](https://github.com/sebastian-13/ProyectoFinalBioinf2017-II/blob/master/README.md) para darle orden consistencia al presente proyecto bioinformático 

1. INTRODUCCIÓN
--------------------

Actualmente existe una discrepancia en la clasificación entre diferentes estudios de taxonomía y sistemática filogenética en diferentes especies de corales debido a que se plantean diferentes eventos de hibridización ([Willis et al., 2006](http://www.annualreviews.org/doi/full/10.1146/annurev.ecolsys.37.091305.110136)). 

La familia *Scleractinidae* es un buen modelo para explorar los procesos de hibridación entre diferentes miembros del grupo debido a que se encuentra ampliamente distribuido a lo largo del oceano Índico y Pacífico ([Vollmer y Pallumbi, 2002](http://science.sciencemag.org/content/296/5575/2023.long)). 

Con base en lo anterior,  se plantea hacer un estudio de genómica de poblaciones particularmente en ciertas especies del género _Pocillopora_ el cual incluye especies que se encuentran en la región marítima del Pacífico Tropical del Este y en el Oceano Pacífico Central y Este. Los datos fueron extraidos del estudio de [Combosch et al. (2015)] (http://www.sciencedirect.com/science/article/pii/S1055790315000858), quienes obtuvieron los datos mediante una extracción y análisis por un método de RNA-Seq. 

Por otro lado, uno de los objetivos de este proyecto bioinformático es poner en práctica los diferentes softwares estudiados en el curso de *Bioinformática* con el transcurso del semestre. De la misma forma darle un sentido lógico a los diferentes calculos obtenidos. Finalmente, exponer de forma clara la forma como se debe presentar un proyecto bioinformático.

2. INFORMACIÓN BÁSICA
-------------------------

El presente proyecto bioinformático contiene los *scripts*, *inputs*, *outputs*, *gráficas* y *archivos suplementarios* que se fueron desarrollando a lo largo de un proyecto bioinformático de genómica de poblaciones. Siendo así, se va a presentar los directorios donde se encuentran los archivos, cada uno de los pasos realizados en el proceso y las posibles herramientas que facilitaron el desarrollo de este.

- El directorio de trabajo `Proyecto_Bioinformatica/bin` contiene los scripts que contienen las funciones particulares para cada uno de los softwares utilizados para el análisis de los datos.

- El directorio de trabajo `Proyecto_Bioinformatica/data` contiene los archivos de entrada y salidas de cada uno de los programas computacionales.

- El directorio de trabajo `Proyecto_Bioinformatica/figures` contiene cada una de las gráficas de R.

- El directorio de trabajo `Proyecto_Bioinformatica/data/secuencias` contiene las secuencias originales trabajadas en el proyecto y el artículo original del estudio que también se puede descargar en el siguiente link [Combosch DJ, Vollmer SV (2015). Data from: Trans-Pacific RAD-Seq population genomics confirms introgressive hybridization in Eastern Pacific Pocillopora corals. http://dx.doi.org/10.5061/dryad.436h0](http://datadryad.org/resource/doi:10.5061/dryad.436h0)

Las herramientas computacionales empleadas se encuentran libres en linea y se pueden descargar en los siguientes links: 
[bwa](http://bio-bwa.sourceforge.net),
[Fastools](http://compbio.ufl.edu/software/fastools/),
[Stacks](http://catchenlab.life.illinois.edu/stacks/),
[PGD Spider](http://www.cmpg.unibe.ch/software/PGDSpider/),
[Admixture](https://www.genetics.ucla.edu/software/admixture/download.html),
[FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
[FigTree](http://tree.bio.ed.ac.),
[PhyMl](http://www.atgc-montpellier.fr/phyml/)

3. Análisis de Calidad
------------------------

Este segmento ya se había desarrollado para el avance dos del proyecto de Bioinformática de igual forma las gráficas serán expuestas para el final.

4. Alineamiento sobre un genoma de referencia 
-----------------------------------------
De los programas existentes para alinear secuencias (NGS) contra una referencia dada, **BWA** y **Bowtie2** son quizás, los mayormente utilizados. La idea basicamente es el alineamiento (mapeo) de secuencias cortas sobre un *genoma de referencia* que preferiblemente se encuentre geneticamente relacionado. Luego de el alineamiento la secuencia cumple con las caracteristicas de un archivo tipo *SAM* con el cual trabajamos nuestras preguntas de SNPs (polimorfismos de un aolos nucleótido), de transcriptómica (RNA Seq) o de re-secuenciación. 

Los mapeos se pueden hacer en una infinidad de programas a saber; *Bowtie*, *Bowtie2*, *SMALT*, *MAQ*, *BWA*, *SOAP2*, *SHRIMP*, etc. Y la selección del programa depende de una evaluación sobre:
>Tipo de datos
>Tiempo de procesamiento
>Recursos (hadware) que consume
>Sensibilidad
>Otros...

**BWA (Burrows-Wheeler Aligment Tool)**

Es un software para hacer alineamientos de secuencias de poca divergencia. Consta principalmente de tres algoritmos: sampe/samse, BWASW y MEM, siendo MEM el recomendado para "queries" de alta-cañidad y se utiliza para reads de /0-100bp.

*Comandos*

Utilizando la secuencia de referencia: `GCF_000222465.1_Adig_1.1_genomic.fna` y los fastq de secuencias: `PdamT1P_Pst1.fq`, `PdamT3P1GC_Pst1.fq`, `PdamT3P2GP_Pst1.fq`, `PdamT1P_Pst1.fq`, `PdamT5TU_Pst1.fq`, `PeleT1P_Pst1.fq` y `PeydT1P_Pst1.fq`.

```
# Dentro de la carpeta /bin/ crear un directorio donde trabajar:
$ mkdir bwa
$ cd bwa

# Donde descargaras el genoma de referencia 
$ curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&rettype=fasta&id=NW_015441057.1" > GCF_002042975.1_ofav_dov_v1_genomic.fna

# Puedes ver el nombre lo puedes ver con
$ grep ">" GCF_002042975.1_ofav_dov_v1_genomic.fna

# Y puedes contar el número de nucleotidos
$ grep -v ">" *.fna | wc -m

# Y moveras las secuencias 
$ mv ../bwa/PdamT1P_Pst1.fq 
$ mv ../bwa/PdamT3P1GC_Pst1.fq 
$ mv ../bwa/PdamT3P2GP_Pst1.fq 
$ mv ../bwa/PdamT1P_Pst1.fq 
$ mv ../bwa/PdamT5TU_Pst1.fq 
$ mv ../bwa/PeleT1P_Pst1.fq  
$ mv ../bwa/PeydT1P_Pst1.fq

# NOTA IMPORTANTE: Me tengo que asegurar que en esa carpeta se encuentren los programas **bwa** y **samtools**.

# Construir un indice de referencia 

$ ./bwa index GCF_000222465.1_Adig_1.1_genomic.fna
## Y así corre :)  "[bwa_index] Pack FASTA..." 

# Crear una carpeta para hacer el siguiente análisis STACKS

$ mkdir ../stacks

# Alinear utilizando la opción MEM y comprimir nuestro archivo de alineamiento BAM en la carpeta creada en el último paso

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PdamT1P_Pst1.fq | samtools view -hbS > PdamT1P_Pst1.bam
$ mv PdamT1P_Pst1.bam ../stacks/

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PdamT3P1GC_Pst1.fq | samtools view -hbS > PdamT3P1GC_Pst1.bam
$ mv PdamT3P1GC_Pst1.bam ../stacks/

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PdamT3P2GP_Pst1.fq | samtools view -hbS > PdamT3P2GP_Pst1.bam
$ mv PdamT3P2GP_Pst1.bam ../stacks/

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PdamT5JA_Pst1.fq | samtools view -hbS > PdamT5JA_Pst1.bam
$ mv PdamT5JA_Pst1.bam ../stacks/

$./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PdamT5TU_Pst1.fq | samtools view -hbS > PdamT5TU_Pst1.bam
$ mv PdamT5TU_Pst1.bam ../stacks/

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PeleT1P_Pst1.fq | samtools view -hbS > PeleT1P_Pst1.bam
$ mv PeleT1P_Pst1.bam ../stacks/

$ ./bwa mem -t 1 -M GCF_000222465.1_Adig_1.1_genomic.fna PeydT1P_Pst1.fq | samtools view -hbS > PeydT1P_Pst1.bam
$ mv PeydT1P_Pst1.bam ../stacks/

## Y así corre :)
"[M::bwa_idx_load_from_disk] read 0 ALT contigs
[M::process] read 212766 sequences (10000002 bp)...
[M::process] read 212766 sequences (10000002 bp)...
[M::mem_process_seqs] Processed 212766 reads in 11.967 CPU sec, 13.073 real sec
[M::process] read 212766 sequences (10000002 bp)..."

# Crear una carpeta para los outputs
$ mkdir Genoma _de_Referencia 

# Mover los archivos del genoma de referencia y comprimir la carpeta
$ mv GCF_000222465.1_Adig_1.1_genomic.fna.sa Genoma_de_Referencia
$ mv GCF_000222465.1_Adig_1.1_genomic.fna.amb Genoma_de_Referencia
$ mv GCF_000222465.1_Adig_1.1_genomic.fna.ann Genoma_de_Referencia
$ mv GCF_000222465.1_Adig_1.1_genomic.fna.pac Genoma_de_Referencia
$ mv GCF_000222465.1_Adig_1.1_genomic.fna.bwt Genoma_de_Referencia

$ tar -zcvf Genoma_de_Referencia.tar.gz Genoma_de_Referencia
$ rm -R Genoma_de_Referencia
```


5. Stacks *Un dolor necesario*
----------------------------

El softwares Stack un un programa representativo en la utilización de datos de secuenciación de nueva generación. Es un programa que funciona con secuencias de reas generados por la plataforma *Illumina*. El programa fue desarrollado para datos desarrollados con enzimas de restricción RAD-Seq para el desarrollo de *mapas genómicos*, *genómica de poblaciones* y *filogeografía*.

Stacks funciona con "Core", "Raw Reads" y "Execution control" representativos con diferentes tipos de análisis. Para el caso del alineamiento con un genoma de referencia utilizamos el "pipeline" de Control de Ejecución [ref_mar.pl] (http://catchenlab.life.illinois.edu/stacks/comp/ref_map.php)
  

**Ref_map de Stacks:** Es un programa que trabaja con diferentes componentes individuales y es utilizado para procesar datos resoltado del alineamiento con genoma de referencia en formatos *SAM* o *BAM*. Puede funcionar con los sub. Es un programa que desarrolla diferentes tipos de análisis como pstacks, cstacks, sstacks, population, etc, haciendo funciones como mapeo genético, crear un catálogo de todos los loci a través de la población, y en mi caso de interes hacer el llamado de los polimorfismos.

**populationes de Stacks:** Es un programa analizado para la estimacion de estadisticos genetico-poblacionales como la *heterocigosidad esperada* y *observada*, el *π*, el *Fst* y el *número de haplotipos*. El programa también exporta una gran variedad de outputs que pueden ser utilizados por muchos softwares. 

*Comandos*

```
# Los datos de mi interes se encuentran en /data/stacks/

# Ir a la carpeta de trabajo donde tiene que encontrarse el Execution control *ref_map.pl*, el Core *populations* y los archivos PeleTiP_Pst1.bam, Pey,dT1P_Pst1.bam, PdamT3P2GP_Pst1.bam, PdamT1P_Pst1.bam, PdamT5JA_Pst1.bam
$ cd data/stacks

#Crear una carpeta donde meteras un archivo .txt donde tendras asignadas tus poblaciones
$ mkdir treestudy_popmap
### El archivo interno se verá así
head treestudy_popmap/popmap1.txt
"PeydT1P_Pst1	1
PeleT1P_Pst1	3
PdamT5TU_Pst1	2
PdamT3P1GC_Pst1	2
PdamT5JA_Pst1	2
PdamT1P_Pst1	2"

#Crear una carpeta donde meteras los archivos BAM
$ mkdir proyecto
# Mover los archivos a esa carpeta
mv PeleT1P_Pst1.bam proyecto/
mv PeydT1P_Pst1.bam	proyecto/
mv PeleT1P_Pst1.bam	proyecto/
mv PdamT5TU_Pst1.bam proyecto/	
mv PdamT3P1GC_Pst1.bam	proyecto/	
mv PdamT5JA_Pst1.bam proyecto/	
mv PdamT1P_Pst1.bam	proyecto/

# Crear una carpeta para tener los outputs
mkdir refmap

# CORRER EL REF_MAP
ref_map.pl -m 3 -b 1 -o ./refmap -O ./treestudy_popmap/popmap1.txt --samples ./proyecto -S 
./treestudy_popmap/popmap1.txt --samples ./proyecto -S 

Así corre :) 
"Parsed population map: 7 files in 3 populations and 1 group.
Found 7 sample file(s).
Identifying unique stacks; file   1 of   7 [PeydT1P_Pst1]
  /usr/local/bin/pstacks -t bam -f ./proyecto/PeydT1P_Pst1.bam -o ./refmap -i 1 -m 3  2>&1"

# Correr el POPULATION
$ populations -P ./refmap -b 1 -M ./treestudy_popmap/popmap1.txt --vcf -t 3

Así corre :)
# populations parameters selected:
Fst kernel smoothing: off
Bootstrap resampling: off
Percent samples limit per population: 0
Locus Population limit: 1
Minimum stack depth: 0
Log liklihood filtering: off; threshold: 0
Minor allele frequency cutoff: 0
Maximum observed heterozygosity cutoff: 1
Applying Fst correction: none.

# Cambiar el nombre al formato output "vcf" (Que es uno de los más importantes para el análisis)

$ mv ./refmap/batch_1.vcf ./refmap/Bioinformatica.vcf

# En la carpeta /data/ descargas el programa vcftools que tiene 6 parpetas: bin/, cpp/, examples/, lib/, perl, y website/ y el programa se encuentra en bin/.

# Finalmente, moverme el archivo .vcf al archivo /vcftools/bin/
mv ./refmap/Bioinformatica.vcf ../../vcftools/bin/

# Prepararme para el siguiente análisis
$ ./refmap/Bioinformatica.vcf ../vcftools/bin/
```

6. VCFtools 
----------------------------
Es un programa que genera una herramienta sencilla de trabajo con un suite de funciones para explicar la variación genética compleja y maneja especialmente el formato **vcf**. Es muy utilizado para:

- Filtros específicos
- Comparar carpetas
- Calcular la varicación
- Hacer conversión de formatos
- Hacer validación y unir carpetas
- Crear intersección entre y subset de variantes

*Comandos*

```
# Inicialmente me muevo a la carpeta donde se encuentra el programa VCFtools

cd ../vcftools/bin/

# Hacer estimados genetico poblacionales

## Escribe un comando que muestre ¿Cuántos individuos y variantes (SNPs) tiene el archivo?
$ ./vcftools --vcf Bioinformatica.vcf

Así corre -> "VCFtools - v0.1.13
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
--vcf Bioinformatica.vcf

After filtering, kept 7 out of 7 Individuals
After filtering, kept 1285 out of a possible 1285 Sites
Run Time = 0.00 seconds"


## Escribe un comando que calcule la frecuencia de cada alelo para todos los individuos dentro del archivo y guarde el resultado en un archivo llamado Bioinformática_allelefreq.
$ ./vcftools --vcf Bioinformatica.vcf --freq --out Bioinformatica_allelefreq

## Escribe un comando que muester ¿Cuántos sitios del archivo no tienen missing data?
$ ./vcftools --vcf Bioinformatica.vcf --max-missing 1.0
"After filtering, kept 7 out of 7 Individuals
After filtering, kept 462 out of a possible 1285 Sites
Run Time = 0.00 seconds"

## Escribe un comando que calcule la frecuencia de cada alelo para todos los individuos pero *sólo* para los sitios sin missing data y guarde el resultado en un archivo llamado Bioinformatica_allelefreqnoNA
$ ./vcftools --vcf Bioinformatica.vcf --freq --max-missing 1.0 --out Bioinformatica_allelefreqnoNA

## Escribe un comando que muestre ¿Cuántos sitios tienen una frecuencia del alelo menor <=0.05
$ ./vcftools --vcf Bioinformatica.vcf --max-maf 0.05
"After filtering, kept 7 out of 7 Individuals
After filtering, kept 0 out of a possible 1285 Sites
No data left for analysis!
Run Time = 0.00 seconds"
###Todos los sitios tienen una frecuencia mayor


## Escribe un comando para calcular la heterocigosidad de cada individuo y guardarla en un archivo llamado BioinformaticaHet
$ ./vcftools --vcf Bioinformatica.vcf --het --out BioinformaticaHet

## Calcula la diversidad nucleotídica por sitio y guarda los resultados en un archivo llamado 
$ ./vcftools --vcf Bioinformatica.vcf --site-pi --out Bioinformatica_Pi

## Calcula la proporción de Transición/Transversión para los SNPs y guardarlo en un archivo
$ ./vcftools --vcf Bioinformatica.vcf --TsTv-by-count --out TsTv.cvs

## Calcula el número de variantes entre cada individuo de frecuencia específica
$ ./vcftools --vcf Bioinformatica.vcf --indv-freq-burden

```
7. "Un elefante se columpiaba sobre la tela de una araña": PGDSpider un software para jugar con los input
------------------------------------------

PGDSpider es un programa amigable para hacer conversión de formatos entre diferentes tipos de formatos se utilizan en programas de *genética de poblaciones* y *genómica*. Este lo caracteriza que acepta un amplio rango de datos (e.i. DNA, RNA, NGS, microsatélites, SNP, RFLP, AFLP o distancias genéticas) y es bastante común en los análisis que tienen que ver con información de *next-generation sequencing* (NGS) 

Este fue el primer programa que no se maniobró por línea de comandos o scripts pero fue utilizado basicamente con el input `Bioinformatica.vcf` para generar los intput: `phylogenia_bioinformatica.phy` que será el archivo a correr con el software *PhyML* para hacer un análisis de _Máxima Verosimilitud_ y el archivo `Proyecto_Bioinformatica_BS` que es el formato que acepta el software *BayeScan*, para hacer el análisis de _Selección_.

Los archivos se encuentran en

**1-)**. El input de PhyMl está en data/PhymL/
**2-)**. El input de BayeScan está en data/bayescan/

8. ATGC: PhyML 
--------------------
PhyML es un software filogenético que se basa en el princiio de La **maximum-likelihood (ML)** a partir de ciertos algoritmos (i.e. Nearest Neighbor Interchangues, NNI que parte de una topología RAZONABLE inicial). La ML es un análisis sugerido para realizar a partir de un amplio set de datos a partir de un *modelo de evolución molecular*, también es importante para hacer un cálculo del soporte interno de las ramas de la filogenia y el más clásico es el _bootstrap no paramétrico_. 

*Comandos*

```
Proceso
input de PhyMl está en data/PhymL/

# El programa se corrió en la plataforma virtual de Guindon et al., 2010 de  ATGC: PhyML 3.0: new algorithms, methods and utilities en [http://www.atgc-montpellier.fr/phyml/]

# Los output se descargaron en la carpeta data/PhyML

# Para ver el árbol obtenido 
$ more PhyML/phylogenia_bioinformatica_phy_phyml_tree.txt 

(PdamT5JA_P:0.04865447,PdamT5TU_P:0.01737179,((PdamT3P1GC:0.04414354,PdamT3P2GP:0.02241088)999:0.07679141,(PeleT1P_Ps:0.01673541,(PeydT1P_Ps:0.03241796,PdamT1P_Ps:0.00000001)865:0.01264615)1000:0.12902947)998:0.09207680);

# Finalmente, la filogenia fue graficada utilizando el software PhyML 

```

8. Admixture y la ancestría
-----------------------

El software *ADMIXTURE* es un programa para realizar la estimación de **ancestría** basada en un modelo para genotipos de SNPs, donde se supone que los individuos no se encuentran relacionados. Particularmente es un programa que corre con los inputs binarios obtenidos de PLINK (.bed) o EIGENSTRAT (.geno).

Para hacer el análisis necesitamos definir una cantidad de pozas génicas (_K_) que definen las poblaciones ancestrales.

*Comandos*

```
# Nota: Es fundamental tener en una carpeta dentro de data/ instalado Plink/ y en otra Admixture/

# Me muevo a la ubicación del Bioinformatica.vcf
cd data/vcftools/

# moverme el archivo .vcf al archivo data/plink/
./vcftools/Bioinformatica.vcf ../Plink/

# Prepararme para análisis con Plink
$ cd ../Plink/

# Hacer la conversión de formatos
./plink --vcf Bioinformatica.vcf --double-id --allow-extra-chr 0 --make-bed --out Proyecto_Bioinformatica_bed

# moverme el archivo .bed al archivo data/Admixture/
./Plink/Proyecto_Bioinformatica.vcf ../Admixture/

# Prepararme para análisis con Admixture
$ cd ../Admixture/

#Correr ADMIXTURE
## Elegir la K
$ grep -h CV log*.out > Proyecto_Bioinformatica_CV.txt

###k=7
$ for K in 1 2 3 4 5 6 7; do  ./admixture --cv=7 Proyecto_Bioinformatica.bed $K | tee log${K}.out; done
	
Así corre :D

"****                   ADMIXTURE Version 1.3.0                  ****
****                    Copyright 2008-2015                     ****
****           David Alexander, Suyash Shringarpure,            ****
****                John  Novembre, Ken Lange                   ****
****                                                            ****
****                 Please cite our paper!                     ****
****   Information at www.genetics.ucla.edu/software/admixture  ****

Cross-validation will be performed.  Folds=7.
Random seed: 43
Point estimation method: Block relaxation algorithm
Convergence acceleration algorithm: QuasiNewton, 3 secant conditions
Point estimation will terminate when objective function delta < 0.0001
Estimation of standard errors disabled; will compute point estimates only.
Size of G: 7x1285

# Para chismosear el K más probable
$ more Proyecto_Bioinformatica_CV.txt 
CV error (K=1): 2.30965
CV error (K=2): 1.72706
CV error (K=3): 1.59410
CV error (K=4): 1.63952
CV error (K=5): 1.34310
CV error (K=6): 0.70847
CV error (K=7): 0.11794
```

9. Marcas de Selección: BayeScan 
-------------------------
 **BAYESCAN** es un software especializado en la identificación de loci candidatos bajo el proceso de _Selección Natural_ a partir de nuestros datos genéticos, utilizando las diferencias entre las frecuencias alélicas entre poblaciones. El cual se basa en un modelo multinomial de Dirichlet donde se va estimando Fst permanentemente.
 
 *Comandos*

```
# moverme el Proyecto_Bioinformatica_BS al archivo data/bayescan/source/Proyecto_Bioinformatica_BS

$ cd ../PDGSpider
$ mv ./Proyecto_Bioinformatica_BS ../bayescan/source

# Prepararme para análisis con BayeScan
$ cd ../bayescan/source

# Correr BayeScan
$ ./bayescan2 -snp bayescan_BioinformaticaR -threads 10 -n 5000 -thin 10 -nbp 20 -pr_odds 10 -pilot 5000 -burn 50000 -out_freq

Y así corre :)
"Pilot runs...
1% 2% 3% 4% 5% 6% 7% 8% 9% 10% 11% 12% 13% 14% 15% 16% 17% 18% 19% 20% 21% 22% 23% 24% 25% 26% 27% 28..."

```

10. Qué Falta?
----------------------

**1-)** Las gráficas resultado del análisis con Bayescan y Admixture ya fueron graficadas con ggplot de R pero aún no se han editado del todo.

**2-)** Terminar el análisis de componentes principales con SNPRelate y graficarlo

**3-)** Discutir los resultados de forma concisa y ordenada.
