# Guida pratica a DCAT-AP_IT e all'alimentazione del catalogo nazionale ``dati.gov.it``

Questo progetto rappresenta la guida pratica offerta da ``dati.gov.it`` per l'accreditamento, l'alimentazione dello stesso secondo le due diverse modalità previste, e per l'adeguamento delle Pubbliche Amministrazioni al profilo nazionale di metadatazione DCAT-AP_IT, così come raccomandato nelle [linee guida per la valorizzazione del patrimonio informativo pubblico (anno 2016)](http://www.dati.gov.it/sites/default/files/LG2016_0.pdf).
Per dettagli sulla semantica degli elementi si invita a consultare anche l'[ontologia OWL](http://dati.gov.it/onto/dcatapit) del profilo DCAT-AP_IT.
La presente guida pratica fornisce una descrizione degli elementi principali del profilo con le relative proprietà. Per ciascun elemento e proprietà, al fine di facilitare le amministrazioni nella predisposizione dei metadati per abilitare la modalità di alimentazione del catalogo detta harvesting, sono forniti esempi di uso nelle seguenti serializzazioni RDF: JSON-LD, RDF/XML, RDF/Turtle. 

**Licenza:**
CC-BY 4.0 (Creative Commons Attribution).

## Indice
* [Alimentare il catalogo nazionale dei dati](#alimentare-il-catalogo-nazionale-dei-dati)
  * [Modalità di alimentazione](#modalità-di-alimentazione)
* [Guida pratica a DCAT-AP_IT](#guida-pratica-a-dcat-ap_it)
  * [Come definire un soggetto/organizzazione in DCAT-AP_IT](#come-definire-un-soggetto-o-organizzazione-in-dcat-ap_it)
    * [dcatapit:Agent](#definizione-di-dcatapitagent)
    * [Elementi obbligatori che descrivono un Soggetto o Organizzazione](#elementi-obbligatori-che-descrivono-un-soggetto-o-organizzazione)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-in-json-ld-rdfxml-rdfturtle)
  * [Come definire un catalogo in DCAT-AP_IT](#come-definire-un-catalogo-di-dati-in-dcat-ap_it)
    * [dcatapit:Catalog](#definizione-di-dcatapitcatalog)
    * [Esempi di uso di dcatapit:Catalog in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitcatalog-in-json-ld-rdfxml-rdfturtle)
    * [Elementi obbligatori](#elementi-obbligatori)
      * [Titolo del catalogo](#1-titolo-del-catalogo-dcttitle)
      * [Descrizione del catalogo](#2-descrizione-del-catalogo-dctdescription)
      * [Editore del catalogo](#3-editore-del-catalogo-dctpublisher)
      * [Data di ultima modifica del catalogo](#4-data-di-ultima-modifica-del-catalogo-dctmodified)
      * [Dataset del catalogo](#5-dataset-del-catalogo-dcatdataset)
    * [Elementi raccomandati](#elementi-raccomandati)
      * [Home page del catalogo](#1-home-page-del-catalogo-foafhomepage)
      * [Lingua del catalogo](#2-lingua-del-catalogo-dctlanguage)
      * [Data di rilascio del catalogo](#3-data-di-rilascio-del-catalogo-dctissued)
      * [Temi del catalogo](#4-temi-del-catalogo-dcatthemetaxonomy)
  * [Come definire un dataset in DCAT-AP_IT](#come-definire-un-dataset-in-dcat-ap_it)
    * [dcatapit:Dataset](#definizione-di-dcatapitdataset)
    * [Esempi di uso di dcatapit:Dataset in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitdataset-in-json-ld-rdfxml-rdfturtle)
    * [Elementi obbligatori](#elementi-obbligatori-1)
      * [Identificativo del dataset](#1-identificativo-del-dataset-dctidentifier)
      * [Titolo del dataset](#2-titolo-del-dataset-dcttitle)
      * [Descrizione del dataset](#3-descrizione-del-dataset-dctdescription)
      * [Data di ultima modifica del dataset](#4-data-di-ultima-modifica-del-dataset-dctmodified)
      * [Temi del dataset](#5-temi-del-dataset-dcattheme)
      * [Titolare del dataset](#6-titolare-del-dataset-dctrightsholder)
      * [Frequenza di aggiornamento del dataset](#7-frequenza-di-aggiornamento-del-dataset-dctaccrualperiodicity)
      * [Distribuzione del dataset](#8-distribuzione-del-dataset-dcatdistribution)
    * [Elementi raccomandati](#elementi-obbligatori-1)
      * [Sottotema del dataset](#1-sottotema-del-dataset-dctsubject)
      * [Punto di contatto del dataset](#2-punto-di-contatto-del-dataset-dcatcontactpoint)
      * [Editore del dataset](#3-editore-del-dataset-dctpublisher)
    * [Elementi opzionali](#elementi-opzionali)
      * [Autore del dataset](#1-autore-del-dataset-dctcreator)
      * [Versione del dataset](#2-versione-del-dataset-owlversioninfo)
      * [Data di rilascio del dataset](#3-data-di-rilascio-del-dataset-dctissued)
      * [Pagina di accesso del dataset](#4-pagina-di-accesso-del-dataset-dcatlandingpage)
  * [Come definire la distribuzione del Dataset in DCAT-AP_IT](#come-definire-la-distribuzione-del-dataset-in-dcat-ap_it)
    * [dcatapit:Distribution](#definizione-di-dcatapitdistribution)
    * [Esempi di uso di dcatapit:Distribution in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitdistribution-in-json-ld-rdfxml-rdfturtle)
  * [Come definire il punto di contatto del Dataset in DCAT-AP_IT](#come-definire-il-punto-di-contatto-del-dataset-in-dcat-ap_it)
    * [dcatapit:Organization](#descrizione-di-dcatapitdescrizione)
    * [Elementi obbligatori che descrivono il Punto di Contatto](#elementi-obbligatori-che-descrivono-il-punto-di-contatto)
  * [Come definire la copertura temporale del Dataset in DCAT-AP_IT](#come-definire-la-copertura-temporale-del-dataset-in-dcat-ap_it)
  * [Come definire la copertura spaziale del Dataset in DCAT-AP_IT](#come-definire-la-copertura-spaziale-del-dataset-in-dcat-ap_it)
  * [Come definire lo standard del Dataset in DCAT-AP_IT](#come-definire-il-punto-di-contatto-del-dataset-in-dcat-ap_it)
  * [Come definire un identificativo alternativo del Dataset in DCAT-AP_IT](#come-definire-un-identificativo-alternativo-del-dataset-in-dcat-ap_it)
  * [Come mappare i temi di DCAT-AP_IT](#come-mappare-i-temi-di-dcat-ap_it)

   
## Alimentare il catalogo nazionale dei dati 
Questa sezione illustra le modalità di alimentazione del catalogo nazionale dei dati.

### Modalità di alimentazione 
Esistono due modalità di alimentazione:

1. *editor*: applicazione Web integrata nel catalogo per l'acquisizione e l'aggiornamento guidato dei metadati. L'editor alimenta automaticamente il catalogo in modo da garantire la conformità al profilo DCAT-AP_IT. Tale modalità è consigliata in presenza di pochi dataset che hanno anche una frequenza di aggiornamento ampia. Per usufruirne, l'utente accede all'area privata di ``dati.gov.it`` selezionando *Login* dal menu in alto a destra, previo accreditamento presso la piattaforma;
2. *harvesting*: funzionalità offerta dal catalogo per l'acquisizione e l'aggiornamento periodico dei metadati. L'uso di tale funzionalità richiede che l'amministrazione comunichi, una volta effettuato il login e solo la prima volta, l'URL del catalogo e selezioni la modalità per l'harvesting (e.g., RDF, CKAN, CSW). Sarà lo stesso catalogo nazionale che si occuperà successivamente di raccogliere periodicamente i metadati che descrivono i dati. Tale modalità è consigliata in presenza di un numero elevato di dataset, soggetti anche a frequenti aggiornamenti. 

## Guida pratica a DCAT-AP_IT
Nelle seguenti sezioni, per ciascun elemento (classe e proprietà) del profilo di metadatazione DCAT-AP_IT saranno fornite istruzioni per l'uso ed esempi pratici di definizione dei metadati in JSON-LD, RDF/XML e RDF/Turtle.

### Come definire un Soggetto o Organizzazione in DCAT-AP_IT
Un soggetto/organizzazione è definito mediante la specifica della classe _Agente_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dcatapit:Agent``

<table>
<tr>
<td align="left">URI</td>
<td align="left">dcatapit:Agent</td>
</tr>
<tr>
<td align="left">Sottoclasse</td>
<td align="left">foaf:Agent</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">Un soggetto (organizzazione) che gioca un certo ruolo sul catalogo e sui dataset del catalogo.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">1</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Obbligatorio</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://www.dati.gov.it/onto/dcatapit#Agent</td>
</tr>
</table>

#### Elementi obbligatori che descrivono un Soggetto o Organizzazione

1) **_IDENTIFICATIVO del SOGGETTO_**: ``dct:identifier``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1 </td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L'identificativo del soggetto (organizzazione)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/identifier</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Nel caso di pubbliche amministrazioni, l'identificativo è rappresentato dal codice IPA (Indice della Pubblica Amministrazione). Per organizzazioni private, l'identiticativo è rappresentato dalla partita IVA. Si consiglia di far riferimento all'organizzazione e non a singoli uffici. 
 <br />Esempio: "agid" oppure "r_lazio".</td>
  </tr>
</table>

2) **_NOME del SOGGETTO_**: ``foaf:name``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1 </td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il nome del soggetto (organizzazione) </td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://xmlns.com/foaf/0.1/name</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Specificare il nome ufficiale della pubblica amministrazione così come riportato nell'Indice della Pubblica Amministrazione. Nel caso di oganizzazione privata, specificare il nome ufficiale della stessa così come riportato nel Registro Imprese.
 <br />Esempio: "Agenzia per l'Italia Digitale".</td>
  </tr>
</table>

#### Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
{
      "@id": "http://dati.gov.it/resource/Amministrazione/agid",
      "@type": [
        "foaf:Agent",
        "http://dati.gov.it/onto/dcatapit#\"Agent"
      ],
      "dcterms:identifier": "agid",
      "foaf:name": {
        "@language": "it",
        "@value": "Agenzia per l'Italia Digitale"
      }
    },
    
```
> ``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Amministrazione/agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Amministrazione/agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#&quot;Agent"/>
        <rdf:type rdf:resource="&foaf;Agent"/>
        <dct:identifier>agid</dct:identifier>
        <foaf:name xml:lang="it">Agenzia per l'Italia Digitale</foaf:name>
    </rdf:Description>
```
> ``RDF/TURTLE``

```Turtle
   <http://dati.gov.it/resource/Amministrazione/agid>
	 a               dcatapit:Agent , foaf:Agent ;
	 dct:identifier  "agid" ;
	 foaf:name       "Agenzia per l'Italia Digitale" .
```

### Come definire un catalogo di dati in DCAT-AP_IT
Un catalogo è definito mediante la classe _Catalogo_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dcatapit:Catalog``

<table>
    <tr>
        <td align="left">URI</td>
        <td align="left">dcatapit:Catalog</td>
    </tr>
     <tr>
        <td align="left">Sottoclasse</td>
        <td align="left">dcat:Catalog</td>
    </tr>
    <tr>
        <td align="left">Descrizione</td>
        <td align="left">Il catalogo che contiene i dati (aperti e non) pubblicato da un'amministrazione.</td>
    </tr>
    <tr>
        <td align="left">Cardinalità</td>
        <td align="left">1</td>
    </tr>
    <tr>
        <td align="left">Stato</td>
        <td align="left">Obbligatorio</td>
    </tr>
     <tr>
        <td align="left">Riferimento</td>
        <td align="left">http://www.dati.gov.it/onto/dcatapit#Catalog</td>
    </tr>
</table>


#### Esempi di uso di dcatapit:Catalog in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
{
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "dcat:dataset": [
        {
          "@id": "http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid"
        },
        {
          "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid"
        }
      ],
      "dcat:themeTaxonomy": {
        "@id": "http://publications.europa.eu/resource/authority/data-theme"
      },
      "dcterms:description": {
        "@language": "it",
        "@value": "Il catalogo dei dati aperti della pubblica amministrazione italiana"
      },
      "dcterms:issued": {
        "@type": "xsd:date",
        "@value": "2012-01-15"
      },
      "dcterms:language": {
        "@id": "http://publications.europa.eu/resource/authority/language/ITA"
      },
      "dcterms:modified": {
        "@type": "xsd:date",
        "@value": "2016-03-20"
      },
      "dcterms:publisher": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      "dcterms:title": {
        "@language": "it",
        "@value": "Catalogo SPCData"
      },
      "foaf:homepage": {
        "@id": "http://spcdata.digitpa.gov.it/index.html"
      }
    },
```
>``RDF/XML``

```XML
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#Catalog"/>
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:modified rdf:datatype="&xsd;date">2016-03-20</dct:modified>
        <dct:issued rdf:datatype="&xsd;date">2012-01-15</dct:issued>
        <dct:title xml:lang="it">Catalogo SPCData</dct:title>
        <dct:description xml:lang="it">Il catalogo dei dati aperti della pubblica amministrazione italiana</dct:description>
        <dct:publisher rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        <dcat:dataset rdf:resource="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid"/>
        <dcat:dataset rdf:resource="http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid"/>
        <dct:language rdf:resource="http://publications.europa.eu/resource/authority/language/ITA"/>
        <dcat:themeTaxonomy rdf:resource="http://publications.europa.eu/resource/authority/data-theme"/>
        <foaf:homepage rdf:resource="http://spcdata.digitpa.gov.it/index.html"/>
    </rdf:Description>
```
>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 						dcatapit:Catalog , dcat:Catalog ;
	dct:title				"Catalogo Dati.gov.it"@it ;
	dct:description 		"Il catalogo dei dati aperti della pubblica amministrazione italiana"@it ;
	dct:modified			"2016-03-20"^^xsd:date ;
	dct:issued				"2012-01-15"^^xsd:date ;
	dct:publisher  			<http://dati.gov.it/resource/Amministrazione/agid> ;
	dct:language			<http://publications.europa.eu/resource/authority/language/ITA> ;
	dcat:dataset    		<http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid> ;
	dcat:dataset    		<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid> ;
	foaf:homepage   		<http://spcdata.digitpa.gov.it/index.html> ;
	dcat:themeTaxonomy  	<http://publications.europa.eu/resource/authority/data-theme> .
```


#### Elementi obbligatori
##### 1) **_TITOLO del CATALOGO:_** ``dct:title``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N (può esistere più di un'istanza in diverse lingue della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il titolo del Catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di inserire un testo semplice e corto. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il catalogo sia parte di un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso.</b> <br />Esempio: "Catalogo dei dati aperti dell'AgID (Agenzia per l'Italia Digitale)" oppure "Catalogo delle banche dati della Regione Lazio".</td>
  </tr>
</table>

##### Esempi di uso di ``dct:title`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "dcterms:title": {
        "@language": "it",
        "@value": "Catalogo SPCData"
      },
      "dcterms:title": {
        "@language": "en",
        "@value": "SPCData Catalog"
      },
      
    altri elementi per specificere il catalogo
```

>``RDF/XML``

```XML
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#Catalog"/>
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:title xml:lang="it">Catalogo SPCData</dct:title>
        <dct:title xml:lang="en">SPCData Catalog</dct:title>
        [altri elementi per specificare il catalogo]
    </rdf:Description>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 						dcatapit:Catalog , dcat:Catalog ;
	dct:title				"Catalogo Dati.gov.it"@it , "SPCData Catalog"@en ;
  
  [altri elementi per specificare il catalogo] .
	
```

##### 2) **_DESCRIZIONE del CATALOGO:_** ``dct:description``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N (può esistere più di un'istanza in diverse lingue della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La descrizione del Catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/description</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di fornire una breve descrizione delle caratteristiche principali del catalogo. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il catalogo. Si ricorda che nessun tag HTML è consentito.</b> <br />Esempio: "Il catalogo contiene i dati aperti dell'Agenzia per l'Italia Digitale, in particolare, i dati aperti dell'Indice della Pubblica Amministrazione (IPA) e dei contratti del Sistema Pubblico di Connettività (SPC) relativi alle gare del 2007".</td>
  </tr>
</table>

##### Esempi di uso di ``dct:description`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "dcterms:description": {
        "@language": "it",
        "@value": "Il catalogo dei dati aperti della pubblica amministrazione italiana"
      },
      
     altri elementi per specificare il catalogo
```

>``RDF/XML``

```XML
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#Catalog"/>
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:description xml:lang="it">Il catalogo dei dati aperti della pubblica amministrazione italiana</dct:description>
        [altri elementi per specificare il catalogo]
    </rdf:Description>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 						dcatapit:Catalog , dcat:Catalog ;
	dct:description 		"Il catalogo dei dati aperti della pubblica amministrazione italiana"@it ;
	[altri elementi per specificare il catalogo] .
```

##### 3) **_EDITORE del CATALOGO:_** ``dct:publisher``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L'editore del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalog</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">Dataset</a>dcatapit:Agent (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/publisher</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Un'organizzazione (o pubblica amministrazione) responsabile di rendere disponibile (pubblicare) il catalogo. <b> Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#soggetto-esempi-JSONLD-RDFXML-RDFTURTLE">esempi riportati sull'uso della classe Agente</a></td>
  </tr>
</table>

##### Esempi di uso di ``dct:publisher`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
       "dcterms:publisher": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      
      altri elementi che descrivono il catalogo
      
   
      "@id": "http://dati.gov.it/resource/Amministrazione/agid",
      "@type": [
        "foaf:Agent",
        "http://dati.gov.it/onto/dcatapit#\"Agent"
      ],
      "dcterms:identifier": "agid",
      "foaf:name": {
        "@language": "it",
        "@value": "Agenzia per l'Italia Digitale"
      }
 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Catalog rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:publisher rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        [altri elementi del catalogo]
    </dcatapit:Catalog>
    
 <!-- http://dati.gov.it/resource/Amministrazione/agid -->
    <dcatapit:Agent rdf:about="http://dati.gov.it/resource/Amministrazione/agid">
        <rdf:type rdf:resource="&foaf;Agent"/>
        <dct:identifier>agid</dct:identifier>
        <foaf:name xml:lang="it">Agenzia per l'Italia Digitale</foaf:name>
    </dcatapit:Agent>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 		dcatapit:Catalog , dcat:Catalog ;
	dct:publisher  	<http://dati.gov.it/resource/Amministrazione/agid> ;
	[altri elementi del catalogo] .
 
 <http://dati.gov.it/resource/Amministrazione/agid>
	a 		dcatapit:Agent , foaf:Agent ;
	dct:identifier  "agid" ;
	foaf:name       "Agenzia per l'Italia Digitale" .
```


##### 4) **_DATA di ULTIMA MODIFICA del CATALOGO:_** ``dct:modified``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di ultima modifica del Catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/modified</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">La data di ultima modifica del catalogo. E' la data in cui si verificano operazioni di modifica del catalogo o dei dataset (es. l’inserimento di un nuovo dataset nel catalogo, la modifica dei metadati del catalogo o di uno dei dataset in esso inclusi) </td>
  </tr>
</table>

##### Esempi di uso di ``dct:modified`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
        "dcterms:modified": {
        "@type": "xsd:date",
        "@value": "2016-03-20"
      },
      
      altri elementi del catalogo

 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Catalog rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:modified rdf:datatype="&xsd;date">2016-03-20</dct:modified>
        [altri elementi del catalogo]
    </dcatapit:Catalog>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 		dcatapit:Catalog , dcat:Catalog ;
	dct:modified	"2016-03-20"^^xsd:date ;
	[altri elementi del catalogo] .
```


##### 5) **_DATASET del CATALOGO:_** ``dcat:dataset``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">E' una proprietà che lega un oggetto (dominio) <a href="#catalogo">Catalogo</a> all'oggetto (codominio) Dataset ed è utilizzata per elencare la lista di dataset presenti nel catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#dataset</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare tante proprietà quanti sono i dataset presenti nel catalogo</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:dataset`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "dcat:dataset": [
        {
          "@id": "http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid"
        },
        {
          "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid"
        }
      ],
      
      altri elementi del catalogo

 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Catalog rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dcat:dataset rdf:resource="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid"/>
        <dcat:dataset rdf:resource="http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid"/>
        [altri elementi del catalogo]
    </dcatapit:Catalog>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 		dcatapit:Catalog , dcat:Catalog ;
	dcat:dataset    <http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid> ;
	dcat:dataset    <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid> ;
	[altri elementi del catalogo] .
```

#### Elementi raccomandati

##### 1) **_HOME PAGE del CATALOGO:_** ``foaf:homepage``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L'home page del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#catalogo">Catalogo</a> a un oggetto (codominio) di tipo foaf:Document (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://xmlns.com/foaf/0.1/homepage</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di indicare l’URL di una pagina web attiva che funge da pagina principale (home page) del catalogo. Si consiglia di indicare l’indirizzo completo, comprensivo anche di protocollo (es. http://).</b> <br />Esempio: "http://spcdata.digitpa.gov.it/index.html".</td>
  </tr>
</table>

##### Esempi di uso di ``foaf:homepage`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "foaf:homepage": {
        "@id": "http://spcdata.digitpa.gov.it/index.html"
      }
      
    altri elementi del catalogo
```

>``RDF/XML``

```XML
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#Catalog"/>
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <foaf:homepage rdf:resource="http://spcdata.digitpa.gov.it/index.html"/>
        [altri elementi del catalogo]
    </rdf:Description>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 	        dcatapit:Catalog , dcat:Catalog ;
	foaf:homepage	<http://spcdata.digitpa.gov.it/index.html>  ;
  
  [altri elementi del catalogo] .
	
```

##### 2) **_LINGUA del CATALOGO:_** ``dct:language``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (possono esistere più istanze della proprietà per ciascuna lingua del catalogo)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La lingua del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#catalogo">Catalogo</a> a un oggetto (codominio) di tipo dct:LinguisticSystem (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/language</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Scegliere una o più lingue utilizzate nel catalogo. <b>La scelta della lingua è regolata dall'uso obbligatorio del <a href="http://publications.europa.eu/mdr/resource/authority/language/skos/languages-skos.rdf">vocabolario definito a livello Europeo sulle lingue.</a></b></td>
  </tr>
</table>

##### Esempi di uso di ``dct:language`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
      "dcterms:language": {
        "@id": "http://publications.europa.eu/resource/authority/language/ITA"
      },
      
    altri elementi del catalogo
```

>``RDF/XML``

```XML
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->

    <rdf:Description rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="http://dati.gov.it/onto/dcatapit#Catalog"/>
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:language rdf:resource="http://publications.europa.eu/resource/authority/language/ITA"/>
        [altri elementi del catalogo]
    </rdf:Description>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 	        dcatapit:Catalog , dcat:Catalog ;
	dct:language	<http://publications.europa.eu/resource/authority/language/ITA> ;
  
  [altri elementi del catalogo] .
	
```

##### 3) **_DATA di RILASCIO del CATALOGO:_** ``dct:issued``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandata</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di rilascio del Catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/issued</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">La data di rilascio del catalogo. E' la data in cui il catalogo è reso disponibile. </td>
  </tr>
</table>

##### Esempi di uso di ``dct:issued`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
        "dcterms:issued": {
        "@type": "xsd:date",
        "@value": "2016-03-20"
      },
      
      altri elementi del catalogo

 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Catalog rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dct:issued rdf:datatype="&xsd;date">2016-03-20</dct:issued>
        [altri elementi del catalogo]
    </dcatapit:Catalog>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 		dcatapit:Catalog , dcat:Catalog ;
	dct:issued	"2016-03-20"^^xsd:date ;
	[altri elementi del catalogo] .
```

##### 4) **_TEMI del CATALOGO:_** ``dcat:themeTaxonomy``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandata</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Tema del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#catalogo">Catalogo</a> a un oggetto (codominio) di tipo skos:Concept (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#themeTaxonomy</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare un sistema di organizzazione della conoscenza (KOS) usato per classificare i dataset del Catalogo. Il valore da utilizzare per questa proprietà è l’URI dei vocabolari utilizzati (<b>non gli URI dei concetti presenti nel vocabolario</b>). Nel caso del vocabolario Data Theme da utilizzare obbligatoriamente per indicare i temi relativi ai Dataset, usare questo URI http://publications.europa.eu/resource/authority/data-theme come valore della proprietà.</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:themeTaxonomy`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid",
      "@type": [
        "dcat:Catalog",
        "http://dati.gov.it/onto/dcatapit#\"Catalog"
      ],
        "dcat:themeTaxonomy": {
        "@id": "http://publications.europa.eu/resource/authority/data-theme"
      },
      
      altri elementi del catalogo

 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Catalog rdf:about="http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid">
        <rdf:type rdf:resource="&dcat;Catalog"/>
        <dcat:themeTaxonomy rdf:resource="http://publications.europa.eu/resource/authority/data-theme" />
        [altri elementi del catalogo]
    </dcatapit:Catalog>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Catalogp/datigov_agid>
	a 			dcatapit:Catalog , dcat:Catalog ;
	dcat:themeTaxonomy	<http://publications.europa.eu/resource/authority/data-theme> ;
	[altri elementi del catalogo] .
```

### Come definire un dataset in DCAT-AP_IT
Un dataset è definito mediante la classe _Dataset_ identificata univocamente da un URI (Uniform Resource Identifier).


#### Definizione di ``dcatapit:Dataset``

<table>
    <tr>
        <td align="left">URI</td>
        <td align="left">dcatapit:Dataset</td>
    </tr>
     <tr>
        <td align="left">Sottoclasse</td>
        <td align="left">dcat:Dataset</td>
    </tr>
    <tr>
        <td align="left">Descrizione</td>
        <td align="left">Il dataset da descrivere.</td>
    </tr>
    <tr>
        <td align="left">Cardinalità</td>
        <td align="left">1</td>
    </tr>
    <tr>
        <td align="left">Stato</td>
        <td align="left">Obbligatorio</td>
    </tr>
     <tr>
        <td align="left">Riferimento</td>
        <td align="left">http://www.dati.gov.it/onto/dcatapit#Dataset</td>
    </tr>
</table>

#### Esempi di uso di dcatapit:Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
 {
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcat:contactPoint": {
        "@id": "http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA"
      },
      "dcat:distribution": {
        "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti-N3"
      },
      "dcat:keyword": [
        "Contratto pubblico",
        "SPC",
        "Acquisizione"
      ],
      "dcat:theme": {
        "@id": "http://publications.europa.eu/resource/authority/data-theme/ECON"
      },
      "dcterms:accrualPeriodicity": {
        "@id": "http://publications.europa.eu/resource/authority/frequency/NEVER"
      },
      "dcterms:creator": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      "dcterms:description": {
        "@language": "it",
        "@value": "Il dataset LOD che contiene i contratti SPC del Lotto 1 (2007)"
      },
      "dcterms:identifier": "agid:D.301",
      "dcterms:modified": {
        "@type": "xsd:date",
        "@value": "2015-05-25"
      },
      "dcterms:publisher": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      "dcterms:rightsHolder": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      "dcterms:spatial": {
        "@id": "http://www.geonames.org/3169070"
      },
      "dcterms:subject": [
        {
          "@id": "http://eurovoc.europa.eu/3193"
        },
        {
          "@id": "http://eurovoc.europa.eu/1810"
        }
      ],
      "dcterms:temporal": {
        "@id": "http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC"
      },
      "dcterms:title": {
        "@language": "it",
        "@value": "Contratti del Sistema Pubblico di Connettività (SPC)"
      }
    },

```
>``RDF/XML``

```XML
  <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->

    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:modified rdf:datatype="&xsd;date">2015-05-25</dct:modified>
        <dct:identifier>agid:D.301</dct:identifier>
        <dcat:keyword>Acquisizione</dcat:keyword>
		<dcat:keyword>SPC</dcat:keyword>
        <dcat:keyword>Contratto pubblico</dcat:keyword>
        <dct:title xml:lang="it">Contratti del Sistema Pubblico di Connettività (SPC)</dct:title>
        <dct:description xml:lang="it">Il dataset contiene i contratti SPC del Lotto 1 (2007)</dct:description>
        <dct:publisher rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        <dct:creator rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        <dct:rightsHolder rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        <dcat:distribution rdf:resource="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3"/>
        <dcat:contactPoint rdf:resource="http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA"/>
        <dct:temporal rdf:resource="http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/3193"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/1810"/>
        <dcat:theme rdf:resource="http://publications.europa.eu/resource/authority/data-theme/ECON"/>
        <dct:accrualPeriodicity rdf:resource="http://publications.europa.eu/resource/authority/frequency/NEVER"/>
        <dct:spatial rdf:resource="http://www.geonames.org/3169070"/>
    </dcatapit:Dataset>
    
```
>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a				dcatapit:Dataset , dcat:Dataset ;
	dct:identifier			"agid:D.301" ;
	dct:title 			"Contratti del Sistema Pubblico di Connettività (SPC)"@it ;
	dct:description 		"Il dataset contiene i contratti SPC del Lotto 1 (2007)"@it ;
	dcat:theme 			<http://publications.europa.eu/resource/authority/data-theme/ECON> ; 
	dct:subject		 	<http://eurovoc.europa.eu/3193> , <http://eurovoc.europa.eu/1810>;
	dct:modified			"2015-05-25"^^xsd:date ;
	dcat:keyword 			"Acquisizione" , "Contratto pubblico" , "SPC" ;
	dct:rightsHolder		<http://dati.gov.it/resource/Amministrazione/agid> ;
	dct:creator 			<http://dati.gov.it/resource/Amministrazione/agid> ;
	dct:publisher 			<http://dati.gov.it/resource/Amministrazione/agid> ;
	dcat:distribution 		<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3> ;
	dct:accrualPeriodicity 		<http://publications.europa.eu/resource/authority/frequency/NEVER> ;
	dcat:contactPoint	 	<http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA> ;
	dct:spatial 			<http://www.geonames.org/3169070> ; 
	dct:temporal 			<http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC> .
```

#### Elementi obbligatori
##### 1) **_IDENTIFICATIVO del DATASET:_** ``dct:identifier``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L'identificativo univoco del Dataset assegnato dal catalogo nazionale</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/identifier</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">L'identificativo univoco del dataset è assegnato dal catalogo nazionale ed è costituito da codiceIPA:D.numeroProgressivo<br />Esempio:agid:D.1</td>
  </tr>
</table>

##### Esempi di uso di ``dct:identifier`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:identifier": "agid:D.301",
      
      altri elementi del catalogo

 ```

>``RDF/XML``

```XML
  <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->

    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
	<dct:identifier>agid:D.1</dct:identifier>
        [altri elementi per specificare il dataset] 
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
   a			dcatapit:Dataset , dcat:Dataset ;
   dct:identifier 	"agid:D.1" ;

   [altri elementi per specificare il dataset] .
	
```

##### 2) **_TITOLO del DATASET:_** ``dct:title``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il titolo del Dataset</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di inserire un testo semplice e corto. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il dataset sia legato a un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso. Si può evitare di inserire nel titolo del Dataset la distribuzione dello stesso (e.g., si può evitare di scrivere un titolo come "Luoghi ed eventi della cultura in LOD")</b> <br />Esempi di titoli di dataset: "Contratti del Sistema Pubblico di Connettività (SPC)" oppure "Luoghi ed eventi della cultura".</td>
  </tr>
</table>

##### Esempi di uso di ``dct:title`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:title": {
        "@language": "it",
        "@value": "Contratti del Sistema Pubblico di Connettività (SPC)"
      },
      
      altri elementi del catalogo

 ```

>``RDF/XML``

```XML
  <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->

    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
	<dct:title xml:lang="it">Contratti del Sistema Pubblico di Connettività (SPC)</dct:title>
        [altri elementi per specificare il dataset] 
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
   a		dcatapit:Dataset , dcat:Dataset ;
   dct:title 	"Contratti del Sistema Pubblico di Connettività (SPC)"@it ;

   [altri elementi per specificare il dataset] .
	
```

##### 3) **_DESCRIZIONE del DATASET:_** ``dct:description``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La descrizione del Dataset che indica cosa contiene il dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/description</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di fornire una breve descrizione dei contenuti principali del dataset. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il contenuto del dataset. Ove possibile, si possono descrivere gli oggetti principali contenuti nel dataset. Si ricorda che nessun tag HTML è consentito.</b> <br />Esempi: "Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) relativi al Lotto 1 dell'anno 2007." oppure "Il dataset contiene i dati relativi ai luoghi della cultura (e.g., musei, biblioteche, siti archeologici, ecc.) e i relativi eventi culturali che si tengono nei luoghi. Informazioni sugli orari di apertura per i luoghi e i relativi eventi sono incluse nel dataset".</td>
  </tr>
</table>

##### Esempi di uso di ``dct:description`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:description": {
        "@language": "it",
        "@value": "Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) 
	           relativi al Lotto 1 dell'anno 2007"
      },
      
     altri elementi per specificare il catalogo
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:description xml:lang="it">Il dataset contiene i dati sui contratti del 
				       Sistema Pubblico di Connettività (SPC) relativi al Lotto 1 dell'anno 2007.</dct:description>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dct:description	"Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) 
			 relativi al Lotto 1 dell'anno 2007."

	[altri elementi per specificare il catalogo] .
	
```

##### 4) **_DATA DI ULTIMA MODIFICA del DATASET:_** ``dct:modified``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di ultima modifica del Dataset</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/modified</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di usare il formato ISO 8601, i.e., yyyy-mm-dd</b></td>
  </tr>
</table>

##### Esempi di uso di ``dct:modified`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:modified": {
        "@type": "xsd:date",
        "@value": "2015-05-25"
      },
      
     altri elementi per specificare il catalogo
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:modified rdf:datatype="&xsd;date">2015-05-25</dct:modified>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dct:modified	"2015-05-25"^^xsd:date ;

	[altri elementi per specificare il catalogo] .
	
```

##### 5) **_TEMI del DATASET:_** ``dcat:theme``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">I temi attraverso cui classificare il Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un o più oggetto (codominio) di tipo skos:Concept (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#theme</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Il metadato assume come valore un URI (NON una stringa con l'URL del tema) che <b>deve essere necessariamente</b> uno di quelli definiti nel seguente vocabolario Europeo sui Temi per i dati: http://publications.europa.eu/mdr/resource/authority/data-theme/skos/data-theme-skos.rdf. Esempio: se il tema è Agricoltura, Pesca e Politiche Forestali e Alimentari il valore di questa proprietà è necessariamente http://publications.europa.eu/resource/authority/data-theme/AGRI. Si veda a tal proposito la sezione <a href="#come-mappare-i-temi-di-dcatapit">Come mappare i temi di DCAT-AP_IT</a> </td>
  </tr>
</table>

##### Esempi di uso di ``dcat:theme`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      {
       "@id": "http://publications.europa.eu/resource/authority/data-theme/ECON",
       "@type": "skos:Concept",
       "skos:prefLabel": {
         "@language": "it",
         "@value": "Economia e Finanze"
      }
    },

     altri elementi per specificare il catalogo
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
       	<dcat:theme rdf:resource="http://publications.europa.eu/resource/authority/data-theme/ECON"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
   Opzionalmente si può anche specificare 
   <!-- http://publications.europa.eu/resource/authority/data-theme/ECON -->

    <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/data-theme/ECON">
        <skos:prefLabel xml:lang="it">Economia e Finanze</skos:prefLabel>
    </skos:Concept>

```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dcat:theme      <http://publications.europa.eu/resource/authority/data-theme/ECON> ;

	[altri elementi per specificare il catalogo] .

  Opzionalmente si può anche specificare 
  
  <http://publications.europa.eu/resource/authority/data-theme/ECON>
	a 		skos:Concept ;
	skos:prefLabel 	"Economia e Finanze"@it .
	
```

##### 6) **_TITOLARE del DATASET:_** ``dct:rightsHolder``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il titolare del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">dcatapit:Agent</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/rightsHolder</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Il metadato assume come valore un URI (NON una stringa). Esso rappresenta un’organizzazione (o pubblica amministrazione) responsabile della gestione complessiva del dataset in virtù dei propri compiti istituzionali. <b>Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#soggetto-esempi-JSONLD-RDFXML-RDFTURTLE">esempi riportati sull'uso della classe Agente</a>
   </td>
 </tr>
</table>

##### Esempi di uso di ``dct:rightsHolder`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
       "dcterms:rightsHolder": {
        "@id": "http://dati.gov.it/resource/Amministraione/agid"
      },
      altri elementi per specificare il catalogo
      
      Dove l'Organizzazione http://dati.gov.it/resource/Amministraione/agid è definita come:
      
      "@id": "http://dati.gov.it/resource/Amministrazione/agid",
      "@type": [
        "foaf:Agent",
        "http://dati.gov.it/onto/dcatapit#\"Agent"
      ],
      "dcterms:identifier": "agid",
      "foaf:name": {
        "@language": "it",
        "@value": "Agenzia per l'Italia Digitale"
      }
    },
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:rightsHolder rdf:resource="http://dati.gov.it/resource/Amministraione/agid"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
   Dove l'organizzazione 
   <!-- http://dati.gov.it/resource/Amministrazione/agid --> è definita come:
   
    <dcatapit:Agent rdf:about="http://dati.gov.it/resource/Amministrazione/agid">
        <rdf:type rdf:resource="&foaf;Agent"/>
        <dct:identifier>agid</dct:identifier>
        <foaf:name xml:lang="it">Agenzia per l'Italia Digitale</foaf:name>
    </dcatapit:Agent>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		  dcatapit:Dataset , dcat:Dataset ;
	dct:rightsHolder  <http://dati.gov.it/resource/Amministraione/agid> ;

	[altri elementi per specificare il catalogo] .

  Dove l'organizzazione <http://dati.gov.it/resource/Amministraione/agid> è definita come
  
  <http://dati.gov.it/resource/Amministrazione/agid>
  a 			dcatapit:Agent , foaf:Agent ;
  dct:identifier  	"agid" ;
  foaf:name		"Agenzia per l'Italia Digitale" .
	
```

##### 7) **_FREQUENZA di AGGIORNAMENTO del DATASET:_** ``dct:accrualPeriodicity``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La frequenza di aggiornamento del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo skos:Concept (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/accrualPeriodicity</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">La frequenza con cui il dataset viene aggiornato <b>assume necessariamente</b> uno dei valori definiti nel seguente vocabolario Europeo sulle frequenze: http://publications.europa.eu/mdr/resource/authority/frequency/skos/frequencies-skos.rdf. Esempio: se il dataset si aggiorna ogni trimestre il valore da indicare è http://publications.europa.eu/resource/authority/frequency/QUARTERLY. Nel caso la frequenza di aggiornamento non sia disponibile è possibile indicare una frequenza sconosciuta utilizzando il seguente URI: http://publications.europa.eu/resource/authority/frequency/UNKNOWN</td>
  </tr>
</table>

##### Esempi di uso di ``dct:accrualPeriodicity`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
        "dcterms:accrualPeriodicity": {
        "@id": "http://publications.europa.eu/resource/authority/frequency/ANNUAL_2"
      },

      altri elementi per specificare il catalogo
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:accrualPeriodicity rdf:resource="http://publications.europa.eu/resource/authority/frequency/ANNUAL_2"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		         dcatapit:Dataset , dcat:Dataset ;
	dct:accrualPeriodicity   <http://publications.europa.eu/resource/authority/frequency/ANNUAL_2> ;

	[altri elementi per specificare il catalogo] .
	
```

##### 8) **_DISTRIBUZIONE del DATASET:_** ``dcat:distribution``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N nel caso di dati aperti, 0..N negli altri casi</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio nel caso di dati aperti, Opzionale negli altri casi</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La distribuzione del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitdistribution">Distributione</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#distribution</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Una distribuzione è una forma attraverso cui il dataset è disponibile. Ogni dataset può essere disponibile in diverse forme, come per esempio diversi formati o differenti endpoint (e.g., SPARQL endpoint). Nel caso di serie temporali o spaziali o viste di un dataset, queste sono descritte mediante le distribuzioni. Per esempio, nel caso di un dataset suddiviso per regioni, le suddivisioni rappresentano distribuzioni di un dataset più ampio che include tutti i dati del territorio nazionale. <br /> Si veda <a href="#definizione-di-dcatapitdistribution">Come definire una distribuzione</a>.</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:distribution`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
       dcat:distribution": {
        "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti-N3"
      }, 

      altri elementi per specificare il catalogo
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dcat:distribution rdf:resource="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		         dcatapit:Dataset , dcat:Dataset ;
	dcat:distribution 		<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3> ;

	[altri elementi per specificare il catalogo] .
	
```

#### Elementi raccomandati

##### 1) **_SOTTOTEMA del DATASET:_** ``dct:subject``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La sottocategoria in cui può  essere  classificato  il  Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un o più oggetti (codominio) di tipo skos:Concept (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/subject</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">In corrispondenza del <a href="#come-mappare-i-temi-di-dcat-ap_it">tema scelto</a>, si può specificare una o più categorie per dettagliare le parole chiave specifiche in cui il dataset può essere classificato.</td>
  </tr>
</table>

##### Esempi di uso di ``dct:subject`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
       "dcterms:subject": [
        {
          "@id": "http://eurovoc.europa.eu/3193"
        },
        {
          "@id": "http://eurovoc.europa.eu/1810"
        }
      ],

```
>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/3193"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/1810"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		         dcatapit:Dataset , dcat:Dataset ;
	dct:subject		 <http://eurovoc.europa.eu/3193> , <http://eurovoc.europa.eu/1810> ;
	[altri elementi per specificare il catalogo] .
	
```
##### 2) **_PUNTO di CONTATTO del DATASET:_** ``dcat:contactPoint``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il Punto di contatto del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un o più oggetti (codominio) di tipo <a href="#definizione-di-dcatcontactpoint">Punto di Contatto</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#contactPoint</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Utilizzare questa proprietà per specificare le informazioni di contatto usate per inviare osservazioni, richieste di informazioni e commenti sul Dataset. <b>E' bene non confondere questo metadato con l'organizzazione titolare o editore o creatore del dataset. Il punto di contatto è usato tipicamente per specificare i riferimenti di un ufficio dell'organizzazione che può fornire informazioni sul dataset. Si veda la sezione <a href="#definizione-di-dcatcontactpoint">Come definire un Punto di Contatto.</a></b></td>
  </tr>
</table>

##### Esempi di uso di ``dcat:contactPoint`` in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcat:contactPoint": {
        "@id": "http://dati.gov.it/resource/PuntoContatto/contactPoint"
      },

      altri elementi per specificare il catalogo
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dcat:contactPoint rdf:resource="http://dati.gov.it/resource/PuntoContatto/contactPoint"/>
        [altri elementi per specificare il catalogo]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		    dcatapit:Dataset , dcat:Dataset ;
	cdat:contactPoint   <http://dati.gov.it/resource/PuntoContatto/contactPoint> ;
	[altri elementi per specificare il catalogo] .
	
```

##### 3) **_EDITORE del DATASET:_** ``dct:publisher``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L'editore del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">dcatapit:Agent</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/publisher</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Un'organizzazione (o pubblica amministrazione) responsabile di rendere disponibile (pubblicare) il dataset. <b> Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#esempi-di-uso-in-json-ld-rdfxml-rdfturtle">esempi riportati sull'uso della classe Agente.</a></td>
  </tr>
</table>

##### Esempi di uso di ``dct:publisher`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
       "dcterms:publisher": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      
      altri elementi che descrivono il catalogo
      
   
      "@id": "http://dati.gov.it/resource/Amministrazione/agid",
      "@type": [
        "foaf:Agent",
        "http://dati.gov.it/onto/dcatapit#\"Agent"
      ],
      "dcterms:identifier": "agid",
      "foaf:name": {
        "@language": "it",
        "@value": "Agenzia per l'Italia Digitale"
      }
 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Catalogo/SPCDataCatalog_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:publisher rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        [altri elementi del catalogo]
    </dcatapit:Dataset>
    
 <!-- http://dati.gov.it/resource/Amministrazione/agid -->
    <dcatapit:Agent rdf:about="http://dati.gov.it/resource/Amministrazione/agid">
        <rdf:type rdf:resource="&foaf;Agent"/>
        <dct:identifier>agid</dct:identifier>
        <foaf:name xml:lang="it">Agenzia per l'Italia Digitale</foaf:name>
    </dcatapit:Agent>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dct:publisher  	<http://dati.gov.it/resource/Amministrazione/agid> ;
	[altri elementi del catalogo] .
 
 <http://dati.gov.it/resource/Amministrazione/agid>
	a 		dcatapit:Agent , foaf:Agent ;
	dct:identifier  "agid" ;
	foaf:name       "Agenzia per l'Italia Digitale" .
```



#### Come mappare i temi di DCAT-AP_IT
I temi in cui i dataset sono classificati si basano sull'uso del vocabolario controllato come indicato nella sezione ["Temi del Dataset dcat:theme"(#5-temi-del-dataset-dcattheme). Sulla base della [valutazione dei diversi temi per i dati discussa nell'ambito del gruppo Europeo](https://joinup.ec.europa.eu/asset/dcat_application_profile/document/review-dcat-ap-draft-proposal-list-categorization-data), la tabella seguente offre un possibile mapping di domini applicativi rispetto ai temi richiesti dal profilo Europeo DCAT-AP, e quindi dall'estensione italiana DCAT-AP_IT.

<table>
    <tr>
    	<td align="left"><b>Tema e relativo URI di riferimento da utilizzare</b></td>
	<td align="left"><b>Descrizione</b></td>
    </tr>
    <tr>
        <td align="left">Agricoltura, pesca, silvicoltura e prodotti alimentari, http://publications.europa.eu/resource/authority/data-theme/AGRI</td>
        <td align="left">Rientra tutto ciò che riguarda il settore agricoltura, pesca, politiche forestali e alimentari</td>
    </tr>
    <tr>
        <td align="left">Economia e Finanze, http://publications.europa.eu/resource/authority/data-theme/ECON </td>
        <td align="left">Rientra tutto ciò che riguarda la tassazione, l'industria, il manifatturiero, il bilancio dello stato, la crescita economica, il commercio</td>
    </tr>
    <tr>
        <td align="left">Istruzione, cultura e sport, http://publications.europa.eu/resource/authority/data-theme/EDUC</td>
        <td align="left">Rientra tutto ciò che riguarda la cultura, il turismo, l'istruzione e le attività sportive</td>
    </tr>
    <tr>
        <td align="left">Energia, http://publications.europa.eu/resource/authority/data-theme/ENER</td>
        <td align="left">Rientra tutto ciò che concerne il settore dell'energia e dell'estrazione mineraria</td>
    </tr>
    <tr>
        <td align="left">Ambiente, http://publications.europa.eu/resource/authority/data-theme/ENVI</td>
        <td align="left">Rientra tutto ciò che riguarda l'ambiente (rifiuti, consumo del suolo, oceani, ecc.) e il clima/meteo</td>
    </tr>
    <tr>
        <td align="left">Governo e settore pubblico, http://publications.europa.eu/resource/authority/data-theme/GOVE</td>
        <td align="left">Rientra tutto ciò che riguarda le politiche di governo, gli affari istituzionali, la trasparenza del settore pubblico</td>
    </tr>
    <tr>
        <td align="left">Salute, http://publications.europa.eu/resource/authority/data-theme/HEAL</td>
        <td align="left">Rientra tutto ciò che concerne le attività sulla salute e tutto ciò che riguarda gli animali</td>
    </tr>
    <tr>
        <td align="left">Tematiche internazionali, http://publications.europa.eu/resource/authority/data-theme/INTR</td>
        <td align="left">Rientra tutto ciò che concerne le relazioni internazionali, la cooperazione internazionale, i diritti umanitari, le organizzazioni internazionali e gli affari esteri</td>
    </tr>
    <tr>
        <td align="left">Giustizia, sistema giuridico e sicurezza pubblica, http://publications.europa.eu/resource/authority/data-theme/JUST</td>
        <td align="left">Rientra tutto ciò che riguarda le frodi, i crimini, la giustizia, le norme. Rientra anche tutto ciò che riguarda la difesa e gli aspetti legati alle attività del ministero dell'interno</td>
    </tr>	
    <tr>
        <td align="left">Regioni e città, http://publications.europa.eu/resource/authority/data-theme/REGI</td>
        <td align="left">Rientra tutto ciò che riguarda le strade urbane e i numeri civici. Il tema ha una forte sovrapposizione con ambiente perché potrebbe anche contenere tutto ciò che concerne la geografia del territorio (e.g., montagne, laghi, fiumi, ecc.)</td>
    </tr>
    <tr>
        <td align="left">Popolazione e società, http://publications.europa.eu/resource/authority/data-theme/SOCI</td>
        <td align="left">Rientra tutto ciò che concerne lo sviluppo della società, le condizioni della società, la cittadinanza, la demografia, il welfare</td>
    </tr>
    <tr>
        <td align="left">Scienza e tecnologia, http://publications.europa.eu/resource/authority/data-theme/TECH</td>
        <td align="left">Rientra tutto ciò che riguarda la ricerca, l'innovazione, la tecnologia, la banda larga e ultralarga, la psicologia, lo spazio</td>
    </tr>
    <tr>
        <td align="left">Trasporti, http://publications.europa.eu/resource/authority/data-theme/TRAN</td>
        <td align="left">Rientra tutto ciò che riguarda i trasporti e le relative infrastrutture, la mobilità</td>
    </tr>
</table>
