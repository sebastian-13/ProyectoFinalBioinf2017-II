##README
-------------

Este proyecto bioinformático contiene los scripts para el desarrollo de un proyecto bioinformático de genómica de poblaciones. Se presentan los scripts de los programas *bwa*, *fastools*, *ref_map* y *populations* de *Stacks*, *Tassel*,  *Plink*, *PhyML*, *PGDSpider*, *Admixture*, *BayeScan*. Además de ello se emplearon *FASTQC*, *Figtree* y *R* para hacer tareas extras explicadas más adelante. 

Este proyecto fue hecho como trabajo final de Bioinformática y los programas empleados se encuentran de acceso libre en la red y se pueden descargar en los siguientes links:

Descargar en las páginas web de los siguientes programas 
[bwa](http://bio-bwa.sourceforge.net),
[Fastools](http://compbio.ufl.edu/software/fastools/),
[Stacks](http://catchenlab.life.illinois.edu/stacks/),
[PGD Spider](http://www.cmpg.unibe.ch/software/PGDSpider/),
[Admixture](https://www.genetics.ucla.edu/software/admixture/download.html),
[FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
[FigTree](http://tree.bio.ed.ac.uk/software/figtree/),
[R](https://www.r-project.org),
[BayeScan](http://cmpg.unibe.ch/software/BayeScan/download.html),
[Plink](https://www.cog-genomics.org/plink2),
[Tassel](http://www.maizegenetics.net/tassel).

Directorios y archivos
---------------------------

El directorio de trabajo `Proyecto_Bioinformatica/bin` contiene los scripts que tienen las funciones específicas para cada uno de los softwares utilizados para el análisis de los datos.

El directorio de trabajo `Proyecto_Bioinformatica/data` contiene los archivos de entrada y salidas de cada uno de los programas computacionales.

El directorio de trabajo `Proyecto_Bioinformatica/figures` contiene cada una de las gráficas de R.

El directorio de trabajo `Proyecto_Bioinformatica/docs` contiene las secuencias originales trabajadas en el proyecto y el artículo original que también se puede descargar en el siguiente link [Combosch DJ, Vollmer SV (2015). Data from: Trans-Pacific RAD-Seq population genomics confirms introgressive hybridization in Eastern Pacific Pocillopora corals. http://dx.doi.org/10.5061/dryad.436h0](http://datadryad.org/resource/doi:10.5061/dryad.436h0)

Softwares y sus funciones
--------------------------

**Formatos .fq(1):** El análisis de la calidad de las secuencias se evaluó mediante el programa FASTQC (PeleTiP_Pst1.fq, PeydT1P_Pst1.fq, PdamT3P2GP_Pst1.fq, PdamT1P_Pst1.fq, PdamT5JA_Pst1.fq).

**Formatos .fq(2):** Las secuencias son alineadas con el software *bwa*, sobre un genoma de referencia (**CF_000222465.1_Adig_1.1_genomic.fna**) utilizando el algoritmo MEM que es utilizado para reads de 70-1000bp.

**Ref_map de Stacks:** Agarra los formatos alineados con base al genoma de referencia que exportó *bwa* es decir: `PeleTiP_Pst1.bam`, `PeydT1P_Pst1.bam`, `PdamT3P2GP_Pst1.bam`, `PdamT1P_Pst1.bam`, `PdamT5JA_Pst1.bam` para hacer un llamado de SNPs.

**Populations de Stacks:** Toma todos los outputs que arrojó el `ref_map` de `Stacks` es decir aquellos que se encuentran dentro de la carpeta `data/Stacks/refmap/`  y los asocia para hacer estimados *genetico poblaciones* (Particularmente los Fst's). De la misma manera genera el formato `.vcf` disponible para muchos análisis posteriores

**Bioinformatica.vcf(1):** En el programa ejecutable **VCFTools** se hizo un estimado de la variación genética, un filtrado de los datos que acepta el ouput `.vcf` de *populations* de *Stacks* 

**Bioinformatica.vcf(2):** En el programa **R** será utilizado para la realización de un _Análisis de Componentes Principales_ que posteriormente va a ser graficado en el mismo.

**Proyecto_Bioinformatica.vcf(3):** Se metió en el programa **PDGSpider** que es un programa para hacer conversión de formatos entre diferentes tipos de formatos se utilizó para generar el output `Proyecto_Bioinformatica_BS` que es el formato que acepta *BayeScan* y el formato `phylogenia_bioinformatica.phy` con el que se estimará una topología de Máxima Verosimilitud con el software **PhyML**.

**phylogenia_bioinformatica.phy:** Fue subido a la base de datos de **ATCG: PhyML** donde puedes hacer corridas de Máxima Verosimilitud de forma masiva dejándole implícito el modelo evolutivo y la opción de hacer un bootstraps no paramétrico para darle poder estadístico al análisis [link] (http://www.atgc-montpellier.fr/phyml/).

**Bioinformatica.vcf(4):** En el caso del softare **Plink** fue utilizado para la determinación de _estadísticos sumario_ para el estudio de la diferenciación entre muestras. Además, se exportó el formafo `Proyecto_Bioinformatica.bed` que es el input para el software **Admixture**. 

**Proyecto_Bioinformatica.bed:** Se realizó una corrida en **Admixture** que es un software especializado en la estimación de ancestría. Con el cual se encontró que `K=7` explica la distribución de la varianza genética de los individuos. El output `Proyecto_Bioinformatica_bed.7.Q` fue graficado en **R**.

**Proyecto_Bioinformatica_BS:** El objetivo del BayeScan es identificar en nuestros datos genéticos loci candidatos bajo _selección natural_, con base en las diferencias en las frecuencias aléícas entre poblaciones. *BayeScan* fue corrido bajo un modelo de evolución molecular neutral con 5000 iteraciones. Finalmente, las salidas fueron graficadas en R.