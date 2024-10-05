# EL ANÁLISIS DEL GENOMA Y DEL PAN-PROTEOMA EN BIFIDOBACTERIAS HUMANAS REVELA FRONTERAS DISCRETAS PARA LA DEMARCACIÓN DE ESPECIES Y LA DIVERGENCIA FUNCIONAL EN FAMILIAS CAZy
Aida Vaquero-Rey(1,2), Antonio Bahilo-Gómez(2), Alfonso Benítez-Páez(1,2)

1. Unidad de Investigación en Microbiota, Nutrición y Salud. Instituto de Agroquímica y Tecnología de Alimentos (IATA-CSIC). Paterna-Valencia, España.
2. Laboratorio de Interacciones Huésped-Microbio en la Salud Metabólica. Centro de Investigación Príncipe Felipe (CIPF). Valencia, España.

Motivación del trabajo:
Las especies de Bifidobacterium son uno de los habitantes más predominantes del intestino humano en los primeros años de vida, y están estrechamente relacionadas con el metabolismo de los carbohidratos de la dieta derivados del huésped. Las especies de Bifidobacterium están altamente especializadas y adaptadas al nicho ecológico del intestino humano; sin embargo, no se conocen bien las bases moleculares de dicha adaptación. El objetivo general del presente trabajo fue realizar un análisis de todo el genoma de las especies de Bifidobacterium derivadas exclusivamente de humanos, identificar genes codificantes, estudiar familias de proteínas compartidas en todo el género e identificar señales de divergencia funcional asociadas al panproteoma y al metabolismo de los carbohidratos.

Aproximación: 
Se utilizó un total de 822 genomas recogidos de la base de datos BV-BRC anotados como de origen Bifidobacterium. Se establecieron múltiples pasos para retener genomas de alta calidad descartando errores taxonómicos y reteniendo genomas sin señal de contaminación. Durante toda la evaluación se realizaron evaluaciones basadas en ANI para la demarcación de especies, predicciones de genes codificantes, agrupación de proteínas y alineaciones de secuencias múltiples. La anotación funcional fue asistida utilizando la base de datos de genes ortólogos (COG), y se exploró la divergencia funcional en el panproteoma expandido, particularmente en las familias CAZy.

Resultados: 
Bifidobacterium longum fue la especie más representada en el conjunto de datos explorado. El control de calidad de la información y la integridad del genoma permitió excluir veinticuatro genomas del estudio, y se reunificaron treinta especies basándose en los discretos valores de ANI intraespecíficos obtenidos. Además, el análisis de calidad identificó quince genomas contaminados, que se eliminaron para los análisis posteriores. Tras la agrupación iterativa de genes codificantes (a nivel de aminoácidos), la modelización matemática sugirió que el 85% de identidad de secuencia era el mejor umbral para explicar la diversidad del proteoma central. Con este umbral, se contabilizaron 101 familias de proteínas para conformar el panproteoma de Bifidobacterium, en el que la traducción, la estructura y la biogénesis ribosómica eran las funciones más representadas. El pan-proteoma ampliado se exploró más a fondo al 50% de identidad de secuencia, aumentando así el pan-proteoma a 463 familias, donde se identificaron siete familias distintas relacionadas con el metabolismo de los carbohidratos (CAZy) presentes en todas las bifidobacterias humanas. A partir del panproteoma ampliado y de las familias CAZy se recuperó una fuerte señal de divergencia funcional de tipo II, información fundamental para comprender el predominio de especie a especie en el intestino humano y la especialización en el metabolismo de los carbohidratos.

Conclusiones:  
Las evaluaciones actuales de todo el genoma para explorar las funciones y la divergencia genética exigen genomas de alta calidad. La evaluación de la calidad en nuestro pipeline apoya firmemente los resultados obtenidos en relación con la demarcación de especies, la categorización funcional y la divergencia funcional de las especies de Bifidobacterium. Las comparaciones realizadas a nivel de nucleótidos y proteínas permitieron desvelar rasgos asociados a las especies, fundamentales para comprender la ecología y las preferencias de nicho de estos taxones bacterianos. En conjunto, el establecimiento y la caracterización del proteoma central de Bifidobacterium permitirán futuros estudios de divergencia funcional para explicar las adaptaciones entre especies y las ventajas competitivas de nicho en estos simbiontes humanos de relevancia para nuestra salud.



# METODOLOGÍA - FLUJO DE TRABAJO EN LINUX
## GUNC

Es un paquete de Python utilizado para la detección de contaminación y quimerismo en los genomas procarióticos. Conlsutar página de documentación para su instalación (https://grp-bork.embl-community.io/gunc/index.html)

#### Requisitos previos:

* Descarga de la base de datos proGenomes 2.1 (ocupa 13 GB)
* Instalar la versión 2.0.4 de Diamond (no admite otras versiones)
* Instalar Prodigal 

#### Input:

Se utilizó como inputs genomas ensamblados en metagenoma con extensión .fna (archivo tipo FASTA)

#### Código:

```bash
$ gunc run -r gunc_db_progenomes2.1.dmnd -d ~/Downloads/archivos_fna -e .fna -o ~/Downloads/resultados_fna --detailed_output
```

#### Explicación de las opciones utilizadas para GUNC:
* -r : base de datos proGenomes 2.1 para que la herramienta Diamond la tome de referencia para el mapeo de las secuencias 
* -d : directorio donde se encuentra los archivos FASTA 
* -e : para indicar el tipo de archivo FASTA (en este caso .fna), ya que sino por defecto interpreta que son archivos .fa
* -o : el directorio donde se desean alamacenar los resultados generados
* --detailed_output : resultados del output para cada nivel taxonómico

#### Output:
 
Los outputs que se generaron tras analizar las 824 secuencias fueron:

* Una carpeta llamada diamond_output (un archivo para cada secuencia).  
* Una carpeta llamada gene_calls (donde genera los archivos .faa obtenidos de Prodigal). En esta carpeta también se genera un archivo .json con el conteo de los genes.
* Una carpeta llamada  gunc_output (donde genera 1 archivo .tsv por cada secuencia .fna que se introduce de input. Estos archivos tsv recogen el output detallado para cada nivel taxonómico).
* Un archivo llamado GUNC.progenomes_2.1.maxCSS_level.tsv, donde se recoge la información de las variables que utiliza para clasificación de la contaminación de las secuencias.


## PRODIGAL (versión 2.6.3)

Es un programa de código abierto para la predicción de genes codificantes. Consultar el siguiente github para su instalación (https://github.com/hyattpd/Prodigal)

#### Input:

Se utilizaron los genomas filtrados con extenión .fna (Consutar memoria de TFM y código en R para más información). 

#### Código:

* Se crea un archivo "Bourne shell" (sh) y se le conceden todos los permisos

```bash
$ touch bucle_prodigal.sh
$ gedit bucle_prodigal.sh
$ chmod -R 777 bucle_prodigal.sh
```

* Se ejecuta el bucle para predecir los genes codificantes mediante PRODIGAL

```bash
./bucle_prodigal.sh
```

* Contenido del bucle en bash  "bucle_prodigal.sh":

```bash
#!/bin/bash

#Directorio donde se encuentran los archivos con extensión .fna

directorio="/home/aida/Downloads/input_PRODIGAL"

#Bucle para predecir los genes codificantes mediante PRODIGAL

for i in "$directorio"/*.fna; do

#Código de PRODIGAL

prodigal -i $i -o $i.gff -a $i.faa -d $i.fa

echo "nombre archivo: $i"

done
```

* Se mueven los outputs generados a las carpetas deseadas

```bash
$ mv *.fa ~/Downloads/output_PRODIGAL/fa
$ mv *.faa ~/Downloads/output_PRODIGAL/faa
$ mv *.gff ~/Downloads/output_PRODIGAL/gff
```

#### Explicación de las opciones utilizadas para PRODIGAL:

* -i : input en fotmato FASTA.
* -o : especificación del output (en este caso se especifica que se generen archivos con extensión .gff y .faa
* -d : escribir secuencias de nucleótidos de genes, indicando la extensión .fa

#### Output:

Se obtienen los outputs especificados en el código:
* Archivos con extensión .faa
* Archivos con extensión .fa
* Archivos con extensión .gff


## CD-HIT (versión 4.8.1)

Es un prorgrama de código abierto utilizado para el agrupamiento de proteínas que cumplen con un umbral de identidad especifico. Consultar el siguiente github para su instalación (https://github.com/weizhongli/cdhit)

#### Input:

* Secuencias con formato FASTA (.faa) en un archivo comprimido .taz.gz


#### Código:

```bash
$ tar -czvf faa.tar.gz /home/aida/Downloads/CD-HIT/input_CD-HIT/faa/*.faa

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_95 -c 0.95 -n 5 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_90 -c 0.9 -n 5 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_85 -c 0.85 -n 5 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_80 -c 0.8 -n 5 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_75 -c 0.75 -n 5 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_70 -c 0.7 -n 4 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_65 -c 0.65 -n 4 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_60 -c 0.6 -n 4 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_55 -c 0.55 -n 3 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_50 -c 0.5 -n 3 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_45 -c 0.45 -n 2 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0

$ ~/Downloads/CD-HIT/output_CD-HIT$ cd-hit -i /home/aida/Downloads/CD-HIT/input_CD-HIT/faa.tar.gz -o db_40 -c 0.4 -n 2 -g 1 -G 0 -aS 0.9 -aL 0.9 -d 0 -p 1 -M 0
```

#### Explicación de las opciones utilizadas para CD-HIT:

* -i : input donde se encuentran los ficheros
* -o : para indicar el nombre de preferencia del output
* -c : umbral de identidad de secuencia (se calcula como número de aminoácidos o bases idénticas en la alineación dividido por la longitud total de la secuencia más corta)
* -n : longitud de las "palabras cortas" (CD-HIT utiliza "palabras cortas para confirmar si la similitud es superior o inferior al umbral de identidad establecido)
* -g : se establece 1 para que CD-HIT agrupe la secuencia en el cluster más similar que cumpla el umbral (modo preciso pero lento)
* -G : se establece en 0 porque se utiliza la identidad de secuencia local, calculada como número de aminoácidos o bases idénticos en la alineación dividido por la longitud de la alineación
* -aS : cobertura del alineamiento para la secuencia más corta. Se fija en 0.9 para que alineamiento cubra el 90% de la secuencia
* -aL : cobertura del alineamiento para la secuencia más larga. Se fija en 0.9 para que alineamiento cubra el 90% de la secuencia
* -d : longitud de la descripción del archivo .clstr. Se establece 0 para obtener la máxima descripción por el programa
* -p : se establece en 1 para que se indique el solapamiento de alineación en el archivo .clstr
* -M : se define el límite de memoria del programa en MB. Se establece 0 para que sea ilimitada

#### Output:
* Archivo FASTA con las secuencias representativas de cada cluster
* Archivo de texto con extensión .clstr donde se recogen todos los clusters

#### Recopilación de los clusters de interés con la función make_multi_seq de CD-HIT:

* Conceder todos los permisos de forma recursiva a la carpeta donde se encuentren los archivos FASTA (.faa). En este caso, la carpeta se nombró "faa".

```bash
$ chmod -R 777 faa
```

* Compilar todas las secuencias en un solo archivo

```bash
$ cat *.faa > Bifido.faa
```

* Ejecutar make_multi_seq.pl

```bash
$ make_multi_seq ~/Downloads/CD-HIT/input_CD-HIT/Bifido.faa ~/Downloads/CD-HIT/output_CD-HIT/db_50.clstr multi-seq-analysis_50 748
$ make_multi_seq ~/Downloads/CD-HIT/input_CD-HIT/Bifido.faa ~/Downloads/CD-HIT/output_CD-HIT/db_85.clstr multi-seq-analysis_85 748
```

#### Explicación de las opciones utilizadas para la función make_multi_seq de CD-HIT:

* ~/Downloads/CD-HIT/input_CD-HIT/Bifido.faa : se indica el directorio donde se encuentran los archivos faa compilados
* ~/Downloads/CD-HIT/output_CD-HIT/db_50.clstr: se indica el directorio donde se encuentra el archivo .clstr de interés
* multi-seq-analysis_50 : se indica el nombre de preferencia para guardar el output generado
* 748 : en este caso se disponían de un total de 787 genomas, y era de interés recuperar los clusters con un número de secuencias superior al 95%, es decir, superior a 748 secuencias/cluster

#### Output:

* Archivos pertenecientes a cada número de cluster conteniendo el número de secuencias según el criterio establecido (los archivos se generan sin extensión) 


## MUSCLE v3.8.1551

Programa de código abierto para la realización de alineamientos múltiples de secuencias (MSA). Consultar la siguientepáguina de información sobre la herramienta (http://www.drive5.com/muscle/)

#### Instalación:

```bash
$ wget https://drive5.com/muscle/downloads3.8.31/muscle3.8.31_i86linux64.tar.gz
$ gunzip muscle3.8.31_i86linux64.tar.gz
$ tar -xf muscle3.8.31_i86linux64.tar
$ chmod +x muscle3.8.31_i86linux6
$ sudo apt-get install muscle
```

#### Input:

Se utilizó el output generado por el algoritmo  make_multi_seq


#### Código:

* Dado que los ficheros que genera de output make_multi_seq se generan sin extensión, en primer lugar, es necesario hacer es añadirle la extensión .faa

```bash
$ rename 's/$/.faa/' *
```

* Se crea un bucle en bash, se conceden permisos y se ejecuta

```bash
$ touch bucle_muscle.sh
$ gedit bucle_muscle.sh
$ chmod -R 777 bucle_muscle.sh
$ ./bucle_muscle.sh
```

#### Ejemplo del bucle realizado en bash para el umbral de identidad 85
(se llevó a cabo el mismo proceso para el umbral de identidad 50)

```bash
#!/bin/bash

#Directorio donde se encuentran los archivos con extensión .faa 

directorio="/home/aida/Downloads/MUSCLE/input/multi-seq-analysis_85"

#Bucle para realizar alineamiento múltiple de secuencias con MUSCLE 

for i in "$directorio"/*.faa; do
    muscle -in "$i" -out "${i%.faa}_aligned.faa"
done
```

* Se mueven los outputs a un nuevo directorio

```bash
~/Downloads/MUSCLE/input/multi-seq-analysis_50$ mv *aligned.faa ~/Downloads/MUSCLE/output/output_50
~/Downloads/MUSCLE/input/multi-seq-analysis_85$ mv *aligned.faa ~/Downloads/MUSCLE/output/output_85
```

#### Explicación de las opciones utilizadas para MUSCLE:

* -in: input en formato FASTA (en este caso .faa)
* -out : output (en este caso, se nombran como "_aligned" con extensión .faa)

#### Output:
 
Se obtienen archivos FASTA (.faa)


## HMMER v3.3.2

Consultar la siguiente página de información sobre la herramienta (http://hmmer.org/)

#### Instalación:

```bash
$ wget http://eddylab.org/software/hmmer/hmmer-3.4.tar.gz
$ tar xf hmmer-3.4.tar.gz
$ cd hmmer-3.4
$ ./configure --prefix=/your/install/path
$ make
$ sudo apt install hmmer
```

#### Se generan perfiles de HMM con el algorimto hmmbuild de HHMER3

* Input:
Archivos .faa que se obtienen del alineamiento múltiple de secuencias con MUSCLE

* Se crea un bucle en bash, se ejecuta y se mueven los outputs a otro directorio (aunque se muestre el umbral de identidad de 85 de ejemplo, se llevó a cabo el mismo proceso para el umbral de identidad de 50)

```bash
$ touch bucle_hmmbuild.sh
$ gedit bucle_hmmbuild.sh
$ chmod -R 777 bucle_hmmbuild.sh
$ ./bucle_hmmbuild.sh
~/Downloads/HMMER3/Identidad_85/output_hmmbuild$ mv /home/aida/Downloads/MUSCLE/output/output_85/*.hmm .

```

* Contenido del bucle en bash "bucle_hmmbuild.sh" (ejemplo para el umbral de identidad de 85)

```bash
#!/bin/bash

#Directorio donde se encuentran los archivos con extensión .faa alineados previamente con MUSCLE

directorio="/home/aida/Downloads/MUSCLE/output/output_85"

#Bucle para realizar HMM 

for i in "$directorio"/*_aligned.faa; do
    hmmbuild "${i%_aligned.faa}.hmm" "$i"
done
```

#### Explicación de las opciones utilizadas para hmmbuild

* "${i%_aligned.faa}.hmm": se indica que se generen archivos con extensión .hmm para cada uno de los archivos input 
* "$i": input 

#### Output:
 
Se obtienen los perfiles de HMM (arhivos con extensión .hmm)


#### Obtención de las secuencias consenso con el algoritmo hmmemit de HMMER3

* Input:
Output generado por el algoritmo hmmbuild (archivos .hmm)

* Se crea un bucle en bash, se ejecuta y se mueven los outputs a otro directorio (aunque se muestre el umbral de identidad de 85 de ejemplo, se llevó a cabo el mismo proceso para el umbral de identidad de 50)

```bash
$ touch bucle_hmmemit.sh
$ gedit bucle_hmmemit.sh
$ chmod -R 777 bucle_hmmemit.sh
$ ./bucle_hmmemit.sh
~/Downloads/HMMER3/Identidad_85/output_hmmemit$ mv /home/aida/Downloads/HMMER3/Identidad_85/output_hmmbuild/*consenso.faa .

```

* Contenido del bucle en bash "bucle_hmmemit.sh" (ejemplo para el umbral de identidad de 85)

```bash
#!/bin/bash

#Directorio donde se encuentran los perfiles de HMM

directorio="/home/aida/Downloads/HMMER3/Identidad_85/output_hmmbuild"

#Bucle para establecer una secuencia consenso a partir de los perfiles HMM

for i in "$directorio"/*.hmm; do
    hmmemit -c "$i" > "${i%.hmm}_consenso.faa"
done
```

#### Explicación de las opciones utilizadas para hmmemit 

* -c : para emitir una secuencia de consenso de regla mayoritaria simple
* "$i": input

#### Output:

Archivos FASTA (.faa) con la secuencia consenso 


## eggNOG-mapper v2

Servidor web para la anotación funcional de secuencias (http://eggnog-mapper.embl.de/). Consultar la siguiente páguina de información (https://github.com/eggnogdb/eggnog-mapper/wiki/).

#### Requisitos previos antes de cargar la secuencias en el servidor web

* Es necesario compilar y comprimir los archivos FASTA 

```bash
$ cat *.faa > Bifido_consenso_85.faa
$ gzip -k Bifido_consenso_85.faa
```
