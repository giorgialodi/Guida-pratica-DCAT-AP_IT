# Guida pratica a DCAT-AP_IT e all'alimentazione del catalogo nazionale dei dati

Questo progetto rappresenta la guida pratica per l'alimentazione del catalogo dei dati (attualmente ``dati.gov.it``) secondo le due diverse modalità previste, e per l'adeguamento delle Pubbliche Amministrazioni al profilo nazionale di metadatazione DCAT-AP_IT, così come raccomandato nelle [linee guida per la valorizzazione del patrimonio informativo pubblico (anno 2016)](http://www.dati.gov.it/sites/default/files/LG2016_0.pdf).
<br/>Per dettagli sulla semantica degli elementi si invita a consultare anche l'[ontologia OWL](http://dati.gov.it/onto/dcatapit) del profilo DCAT-AP_IT.
<br />La presente guida pratica fornisce una descrizione degli elementi principali del profilo con le relative proprietà. Per ciascun elemento e proprietà, al fine di facilitare le amministrazioni nella predisposizione dei metadati per abilitare la modalità di alimentazione del catalogo detta harvesting, sono forniti esempi di uso nelle seguenti serializzazioni RDF: JSON-LD, RDF/XML, RDF/Turtle. 

**Licenza:**
CC-BY 4.0 (Creative Commons Attribution).

## Indice
* [Alimentare il catalogo nazionale dei dati](#alimentare-il-catalogo-nazionale-dei-dati)
  * [Modalità di alimentazione](#modalità-di-alimentazione)
* [Guida pratica a DCAT-AP_IT](#guida-pratica-a-dcat-ap_it)
  * [Come definire un Catalogo in DCAT-AP_IT](#come-definire-un-catalogo-di-dati-in-dcat-ap_it)
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
  * [Come definire un Dataset in DCAT-AP_IT](#come-definire-un-dataset-in-dcat-ap_it)
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
    * [Elementi raccomandati](#elementi-raccomandati-1)
      * [Sottotema del dataset](#1-sottotema-del-dataset-dctsubject)
      * [Punto di contatto del dataset](#2-punto-di-contatto-del-dataset-dcatcontactpoint)
      * [Editore del dataset](#3-editore-del-dataset-dctpublisher)
    * [Elementi opzionali](#elementi-opzionali)
      * [Autore del dataset](#1-autore-del-dataset-dctcreator)
      * [Versione del dataset](#2-versione-del-dataset-owlversioninfo)
      * [Data di rilascio del dataset](#3-data-di-rilascio-del-dataset-dctissued)
      * [Pagina di accesso del dataset](#4-pagina-di-accesso-del-dataset-dcatlandingpage)
      * [Lingua del dataset](#5-lingua-del-dataset-dctlanguage)
      * [Parole chiave del dataset](#6-parole-chiave-del-dataset-dcatkeyword)
      * [Dataset correlato](#7-dataset-correlato-isversionof)
      * [Estensione temporale del dataset](#8-estensione-temporale-del-dataset-dcttemporal)
      * [Copertura geografica del dataset](#9-copertura-geografica-del-dataset-dctspatial)
      * [Conformità del dataset](#10-conformita-del-dataset-dctconformsto)
      * [Altro identificativo del dataset](#11-altro-identificativo-del-dataset-admsidentifier)
  * [Come definire una Distribuzione del Dataset in DCAT-AP_IT](#come-definire-una-distribuzione-del-dataset-in-dcat-ap_it)
    * [dcatapit:Distribution](#definizione-di-dcatapitdistribution)
    * [Esempi di uso di dcatapit:Distribution in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitdistribution-in-json-ld-rdfxml-rdfturtle)
    * [Elementi obbligatori](#elementi-obbligatori-2)
      * [Formato della distribuzione](#1-formato-della-distribuzione-dctformat)
      * [URL di accesso](#2-url-di-accesso-dcataccessurl)
      * [Licenza](#3-licenza-dctlicense)
    * [Elementi raccomandati](#elementi-raccomandati-2)
      * [Descrizione della distribuzione](#1-descrizione-della-distribuzione-dctdescription)
    * [Elementi opzionali](#elementi-opzionali-1)
      * [Titolo della distribuzione](#1-titolo-della-distribuzione-dcttitle)
      * [URL di download](#2-url-di-download-dcatdownloadurl)
      * [Ultima modifica della distribuzione](#3-ultima-modifica-della-distribuzione-dctmodified)
      * [Dimensione in byte](#4-dimensione-in-byte-dcatbytesize)
  * [Come definire un soggetto/organizzazione in DCAT-AP_IT](#come-definire-un-soggetto-o-organizzazione-in-dcat-ap_it)
    * [dcatapit:Agent](#definizione-di-dcatapitagent)
    * [Elementi obbligatori che descrivono un Soggetto o Organizzazione](#elementi-obbligatori-che-descrivono-un-soggetto-o-organizzazione)
    * [Esempi di uso di dcatapit:Agent in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle)
  * [Come definire la Licenza in DCAT-AP_IT](#come-definire-la-licenza-in-dcat-ap_it)
    * [dcatapit:LicenseDocument](#definizione-di-dcatapitlicensedocument)
    * [Elementi raccomandati che descrivono la licenza](#elementi-raccomandati-che-descrivono-la-licenza)
    * [Elementi opzionali che descrivono la licenza](#elementi-opzionali-che-descrivono-la-licenza)
    * [Esempi di uso di dcatapit:LicenseDocument in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitlicensedocument-in-json-ld-rdfxml-rdfturtle)
  * [Come definire il punto di contatto del Dataset in DCAT-AP_IT](#come-definire-il-punto-di-contatto-del-dataset-in-dcat-ap_it)
    * [dcatapit:Organization](#definizione-di-dcatapitorganization)
    * [Elementi obbligatori che descrivono il punto di contatto](#elementi-obbligatori-che-descrivono-il-punto-di-contatto)
    * [Elementi ozionali che descrivono il punto di contatto](#elementi-opzionali-che-descrivono-il-punto-di-contatto)
    * [Esempi di uso di dcatapit:Organization in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitorganization-in-json-ld-rdfxml-rdfturtle)  
  * [Come definire la copertura temporale del Dataset in DCAT-AP_IT](#come-definire-la-copertura-temporale-del-dataset-in-dcat-ap_it)
    * [dct:PeriodOfTime](#definizione-di-dctperiodoftime)
    * [Elementi obbligatori che descrivono il periodo di tempo](#elementi-obbligatori-che-descrivono-il-periodo-di-tempo)
    * [Elementi opzionali che descrivono il periodo di tempo](#elementi-opzionali-che-descrivono-il-periodo-di-tempo)
    * [Esempi di uso di dct:PeriodOfTime in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dctperiodoftime-in-json-ld-rdfxml-rdfturtle)
  * [Come definire la copertura geografica del Dataset in DCAT-AP_IT](#come-definire-la-copertura-geografica-del-dataset-in-dcat-ap_it)
    * [dct:Location](#definizione-di-dctlocation)
    * [Elementi opzionali che descrivono la copertura geografica](#elementi-opzionali-che-descrivono-la-copertura-geografica)
    * [Elementi che descrivono la geometria della copertura geografica](#elementi-che-descrivono-la-geometria-della-copertura-geografica)
    * [Esempi di uso di dct:Location e locn:Geometry in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dctlocation-e-locngeometry-in-json-ld-rdfxml-rdfturtle)
  * [Come definire lo standard del Dataset in DCAT-AP_IT](#come-definire-lo-standard-del-dataset-in-dcat-ap_it)
    * [dctapit:Standard](#definizione-di-dcatapitstandard)
    * [Elementi obbligatori che descrivono lo standard](#elementi-obbligatori-che-descrivono-lo-standard)
    * [Elementi opzionali che descrivono lo standard](#elementi-opzionali-che-descrivono-lo-standard)
    * [Esempi di uso di dcatapit:Standard in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-dcatapitstandard-in-json-ld-rdfxml-rdfturtle)
  * [Come definire un identificativo alternativo del Dataset in DCAT-AP_IT](#come-definire-un-identificativo-alternativo-del-dataset-in-dcat-ap_it)
    * [adms:Identifier](#definizione-di-admsidentifier)
    * [Elementi raccomandati che descrivono altro identificativo del dataset](#elementi-raccomandati-che-descrivono-altro-identificativo-del-dataset)
    * [Esempi di uso di adms:Identifier in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-di-admsidentifier-in-json-ld-rdfxml-rdfturtle)
  * [Come mappare i temi di DCAT-AP_IT](#come-mappare-i-temi-di-dcat-ap_it)
  * [Riepilogo dei vocabolari controllati da utilizzare](#riepilogo-dei-vocabolari-controllati-da-utilizzare)
  * [Alcuni errori comuni](#alcuni-errori-comuni)

   
## Alimentare il catalogo nazionale dei dati 
Questa sezione illustra le modalità di alimentazione del catalogo nazionale dei dati.

### Modalità di alimentazione 
Esistono due modalità di alimentazione:

1. *editor*: applicazione Web integrata nel catalogo per l'acquisizione e l'aggiornamento guidato dei metadati. L'editor alimenta automaticamente il catalogo in modo da garantire la conformità al profilo DCAT-AP_IT. Tale modalità è consigliata in presenza di pochi dataset che hanno anche una frequenza di aggiornamento ampia. Al momento la funzionalità non è ancora attiva. Si prevede tuttavia la possibilità per l'utente di accedere all'area privata del catalogo dei dati selezionando *Login* dal menu in alto a destra, previo accreditamento presso la piattaforma;
2. *harvesting*: funzionalità offerta dal catalogo per l'acquisizione e l'aggiornamento periodico dei metadati. L'uso di tale funzionalità richiede che l'amministrazione comunichi, solo la prima volta, l'URL del catalogo e indichi la modalità di harvesting (e.g., RDF (DCAT-AP_IT), CKAN, CSW). Sarà lo stesso catalogo nazionale che si occuperà successivamente di raccogliere periodicamente i metadati che descrivono i dati. Tale modalità è consigliata in presenza di un numero elevato di dataset, soggetti anche a frequenti aggiornamenti. 

## Guida pratica a DCAT-AP_IT
Nelle seguenti sezioni, per ciascun elemento (classe e proprietà) del profilo di metadatazione DCAT-AP_IT saranno fornite istruzioni per l'uso ed esempi pratici di definizione dei metadati in JSON-LD, RDF/XML e RDF/Turtle. Il profilo complessivo è illustrato nella seguente figura. 

![DCAT-AP_IT UML Diagram](DCAT-AP_IT_UML.png)

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
	a 				dcatapit:Catalog , dcat:Catalog ;
	dct:title			"Catalogo Dati.gov.it"@it ;
	dct:description 		"Il catalogo dei dati aperti della pubblica amministrazione italiana"@it ;
	dct:modified			"2016-03-20"^^xsd:date ;
	dct:issued			"2012-01-15"^^xsd:date ;
	dct:publisher  			<http://dati.gov.it/resource/Amministrazione/agid> ;
	dct:language			<http://publications.europa.eu/resource/authority/language/ITA> ;
	dcat:dataset    		<http://dati.gov.it/resource/Dataset/LinkedOpenIPA20_agid> ;
	dcat:dataset    		<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid> ;
	foaf:homepage   		<http://spcdata.digitpa.gov.it/index.html> ;
	dcat:themeTaxonomy  	        <http://publications.europa.eu/resource/authority/data-theme> .
```


#### Elementi obbligatori
##### 1) **_TITOLO del CATALOGO:_** ``dct:title``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1..N (può esistere più di un'istanza in diverse lingue, della stessa proprietà)</td>
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
    <td align="left">Si raccomanda di inserire un testo <b>semplice e corto</b>. Si raccomanda di <b>non utilizzare acronimi o abbreviazioni incomprensibili</b>. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il catalogo sia parte di un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso.<br />Esempio: "Catalogo dei dati aperti dell'AgID (Agenzia per l'Italia Digitale)" oppure "Catalogo delle banche dati della Regione Lazio".</td>
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
	a 		dcatapit:Catalog , dcat:Catalog ;
	dct:title	"Catalogo Dati.gov.it"@it , "SPCData Catalog"@en ;
  
  [altri elementi per specificare il catalogo] .
	
```

##### 2) **_DESCRIZIONE del CATALOGO:_** ``dct:description``

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
    <td align="left">La descrizione del Catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/description</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Si raccomanda di fornire una breve descrizione delle caratteristiche principali del catalogo. <b>Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il catalogo.</b> Si ricorda che nessun tag HTML è consentito. <br />Esempio: "Il catalogo contiene i dati aperti dell'Agenzia per l'Italia Digitale, in particolare, i dati aperti dell'Indice della Pubblica Amministrazione (IPA) e dei contratti del Sistema Pubblico di Connettività (SPC) relativi alle gare del 2007".</td>
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
	a 		  dcatapit:Catalog , dcat:Catalog ;
	dct:description   "Il catalogo dei dati aperti della pubblica amministrazione italiana"@it ;
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
    <td align="left">L'editore del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalog</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">Agent</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/publisher</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Un'organizzazione (o pubblica amministrazione) responsabile di rendere disponibile (pubblicare) il catalogo. <b> Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle">esempi riportati sull'uso della classe Agente</a></td>
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
      
      Dove l'amministrazione è definita come:
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
    
 Dove l'amministrazione è definita come:   
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
 
 Dove l'amministrazione è definita come:
 
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
    <td align="left">La data di ultima modifica del catalogo. E' la data in cui si verificano operazioni di modifica del catalogo (es. l’inserimento di un nuovo dataset nel catalogo, la modifica dei metadati del catalogo o di uno dei dataset in esso inclusi) </td>
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
    <td align="left">E' una proprietà che lega un oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalog(Catalogo)</a> all'oggetto (codominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> ed è utilizzata per elencare la lista di dataset presenti nel catalogo</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#dataset</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare tante proprietà dcat:dataset quanti sono i dataset presenti nel catalogo</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:dataset`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
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
    <td align="left">L'home page del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalog(Catalogo)</a> a un oggetto (codominio) di tipo foaf:Document (specificato mediante un URI- Uniform Resource Identifier)</td>
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
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La lingua del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalog(Catalogo)</a> a un oggetto (codominio) di tipo dct:LinguisticSystem (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/language</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare una o più lingue utilizzate nel catalogo. <b>La scelta della lingua è regolata dall'uso obbligatorio del <a href="http://publications.europa.eu/mdr/resource/authority/language/skos/languages-skos.rdf">vocabolario definito a livello Europeo sulle lingue.</a></b></td>
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
    <td align="left">E' la data in cui il catalogo è reso disponibile. </td>
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
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Tema del Catalogo. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitcatalog">Catalogo</a> a un oggetto (codominio) di tipo skos:Concept (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#themeTaxonomy</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare un sistema di organizzazione della conoscenza (KOS) usato per classificare i dataset del Catalogo. Il valore da utilizzare per questa proprietà è l’URI dei vocabolari utilizzati (<b>non gli URI dei concetti presenti nel vocabolario</b>). Nel caso del vocabolario Data Theme da utilizzare obbligatoriamente per indicare i temi relativi ai Dataset, usare questo URI http://publications.europa.eu/resource/authority/data-theme come valore di questa proprietà.</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:themeTaxonomy`` per il Catalogo in JSON-LD, RDF/XML, RDF/Turtle
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
        <td align="left">1..N</td>
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
      
      altri elementi del dataset

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
    <td align="left">Si raccomanda di inserire un testo <b>semplice e corto</b>. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il dataset sia legato a un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso. Si può evitare di inserire nel titolo del Dataset la distribuzione dello stesso (e.g., si può evitare di scrivere un titolo come "Luoghi ed eventi della cultura in LOD"). <br />Esempi di titoli di dataset: "Contratti del Sistema Pubblico di Connettività (SPC)" oppure "Luoghi ed eventi della cultura".</td>
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
      
      altri elementi del dataset

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
    <td align="left"><b>Si raccomanda di fornire una breve descrizione dei contenuti principali del dataset. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il contenuto del dataset. Ove possibile, si possono fornire indicazioni sulla struttura dei dati che compongono il dataset. Si ricorda che nessun tag HTML è consentito.</b> <br />Esempi: "Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) relativi al Lotto 1 dell'anno 2007." oppure "Il dataset contiene i dati relativi ai luoghi della cultura (e.g., musei, biblioteche, siti archeologici, ecc.) e i relativi eventi culturali che si tengono nei luoghi. Informazioni sugli orari di apertura per i luoghi e i relativi eventi sono incluse nel dataset".</td>
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
      
     altri elementi per specificare il dataset
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:description xml:lang="it">Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) relativi al Lotto 1 dell'anno 2007.</dct:description>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dct:description	"Il dataset contiene i dati sui contratti del Sistema Pubblico di Connettività (SPC) 
			 relativi al Lotto 1 dell'anno 2007."

	[altri elementi per specificare il dataset] .
	
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
    <td align="left">Si raccomanda di usare il formato ISO 8601, i.e., yyyy-mm-dd</td>
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
      
     altri elementi per specificare il dataset
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:modified rdf:datatype="&xsd;date">2015-05-25</dct:modified>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		dcatapit:Dataset , dcat:Dataset ;
	dct:modified	"2015-05-25"^^xsd:date ;

	[altri elementi per specificare il dataset] .
	
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
    <td align="left">Il metadato assume come valore un URI (NON una stringa con l'URL del tema) che <b>deve essere necessariamente</b> uno tra quelli definiti nel <a href="http://publications.europa.eu/mdr/resource/authority/data-theme/skos/data-theme-skos.rdf">vocabolario Europeo sui Temi per i dati</a>. Esempio: se il tema è Agricoltura, Pesca e Politiche Forestali e Alimentari il valore di questa proprietà è necessariamente http://publications.europa.eu/resource/authority/data-theme/AGRI. Si veda a tal proposito la sezione <a href="#come-mappare-i-temi-di-dcat-ap_it">Come mappare i temi di DCAT-AP_IT</a> </td>
  </tr>
</table>

##### Esempi di uso di ``dcat:theme`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
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

     altri elementi per specificare il dataset
     
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
       	<dcat:theme rdf:resource="http://publications.europa.eu/resource/authority/data-theme/ECON"/>
        [altri elementi per specificare il dataset]
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

	[altri elementi per specificare il dataset] .

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
    <td align="left">Il titolare del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">Agent(Soggetto)</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/rightsHolder</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Il metadato assume come valore un URI (NON una stringa). Esso rappresenta un’organizzazione (o pubblica amministrazione) responsabile della gestione complessiva del dataset in virtù dei propri compiti istituzionali. <b>Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle">esempi riportati sull'uso della classe Agente</a>
   </td>
 </tr>
</table>

##### Esempi di uso di ``dct:rightsHolder`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
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
      altri elementi per specificare il dataset
      
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
        [altri elementi per specificare il dataset]
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

	[altri elementi per specificare il dataset] .

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
    <td align="left">La frequenza di aggiornamento del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo dct:Frequency (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/accrualPeriodicity</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">La frequenza con cui il dataset viene aggiornato <b>assume necessariamente</b> uno dei valori definiti nel <a href="http://publications.europa.eu/mdr/resource/authority/frequency/skos/frequencies-skos.rdf">vocabolario Europeo sulle frequenze.</a> Esempio: se il dataset si aggiorna ogni trimestre il valore da indicare è http://publications.europa.eu/resource/authority/frequency/QUARTERLY. Nel caso la frequenza di aggiornamento non sia disponibile è possibile indicare una frequenza sconosciuta utilizzando il seguente URI: http://publications.europa.eu/resource/authority/frequency/UNKNOWN</td>
  </tr>
</table>

##### Esempi di uso di ``dct:accrualPeriodicity`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
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

      altri elementi per specificare il dataset
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:accrualPeriodicity rdf:resource="http://publications.europa.eu/resource/authority/frequency/ANNUAL_2"/>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		         dcatapit:Dataset , dcat:Dataset ;
	dct:accrualPeriodicity   <http://publications.europa.eu/resource/authority/frequency/ANNUAL_2> ;

	[altri elementi per specificare il dataset] .
	
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
    <td align="left">La distribuzione del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitdistribution">Distribuzione</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#distribution</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Una distribuzione è una forma attraverso cui il dataset è disponibile. Ogni dataset può essere disponibile in diverse forme, come per esempio diversi formati o differenti endpoint (e.g., SPARQL endpoint). Nel caso di serie temporali o spaziali o viste di un dataset, queste sono descritte mediante le distribuzioni. Per esempio, nel caso di un dataset suddiviso per regioni, le suddivisioni rappresentano distribuzioni di un dataset più ampio che include tutti i dati del territorio nazionale. <br /> Si veda <a href="#definizione-di-dcatapitdistribution">Come definire una distribuzione</a> per maggiori dettagli.</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:distribution`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
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

      altri elementi per specificare il dataset
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dcat:distribution rdf:resource="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3"/>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		        dcatapit:Dataset , dcat:Dataset ;
	dcat:distribution 	<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3> ;

	[altri elementi per specificare il dataset] .
	
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
    <td align="left">In corrispondenza del <a href="#come-mappare-i-temi-di-dcat-ap_it">tema scelto</a>, si possono specificare più categorie per indicare parole chiave specifiche con cui il dataset può essere ulteriormente classificato.</td>
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
      altri elementi del dataset
```
>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/3193"/>
        <dct:subject rdf:resource="http://eurovoc.europa.eu/1810"/>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		         dcatapit:Dataset , dcat:Dataset ;
	dct:subject		 <http://eurovoc.europa.eu/3193> , <http://eurovoc.europa.eu/1810> ;
	[altri elementi per specificare il dataset] .
	
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
    <td align="left">Il Punto di contatto del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo <a href="#definizione-di-dcatapitorganization">Punto di Contatto</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/dcat#contactPoint</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Utilizzare questa proprietà per specificare le informazioni di contatto usate per inviare osservazioni, richieste di informazioni e commenti sul Dataset. <b>E' bene non confondere questo metadato con l'organizzazione titolare o editore o creatore del dataset. Il punto di contatto è usato tipicamente per specificare i riferimenti di un ufficio dell'organizzazione che può fornire informazioni sul dataset. Si veda la sezione <a href="#come-definire-il-punto-di-contatto-del-dataset-in-dcat-ap_it">Come definire un Punto di Contatto.</a></b></td>
  </tr>
</table>

##### Esempi di uso di ``dcat:contactPoint`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcat:contactPoint": {
        "@id": "http://dati.gov.it/resource/PuntoContatto/contactPointContrattiSPC"
      },

      altri elementi per specificare il dataset
      
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
   <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dcat:contactPoint rdf:resource="http://dati.gov.it/resource/PuntoContatto/contactPointContrattiSPC"/>
        [altri elementi per specificare il dataset]
   </dcatapit:Dataset>
   
```

>``RDF/Turtle``

```Turtle
   <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		    dcatapit:Dataset , dcat:Dataset ;
	dcat:contactPoint   <http://dati.gov.it/resource/PuntoContatto/contactPointContrattiSPC> ;
	[altri elementi per specificare il dataset] .
	
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
    <td align="left">L'editore del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitagent">Agent (Soggetto)</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/publisher</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Un'organizzazione (o pubblica amministrazione) responsabile di rendere disponibile (pubblicare) il dataset. <b> Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle">esempi riportati sull'uso della classe Agent.</a></td>
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
      
      altri elementi che descrivono il dataset
      
      Dove l'organizzazione editore è definita come:
      
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
 
 <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:publisher rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
 
 Dove l'organizzazione editore è descritta come:
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
	[altri elementi del dataset] .
 
 Dove l'organizzazione editore è definita come:
 <http://dati.gov.it/resource/Amministrazione/agid>
	a 		dcatapit:Agent , foaf:Agent ;
	dct:identifier  "agid" ;
	foaf:name       "Agenzia per l'Italia Digitale" .
```
#### Elementi opzionali

##### 1) **_AUTORE del DATASET:_** ``dct:creator``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il creatore del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo <a href="#definizione-di-dcatapitagent">Agent (Soggetto)</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/creator</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Un'organizzazione (o pubblica amministrazione) che ha materialmente prodotto il dataset. <b> Si raccomanda di evitare l'inserimento di nomi di singole persone.</b><br />Si vedano gli <a href="#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle">esempi riportati sull'uso della classe Agent.</a></td>
  </tr>
</table>

##### Esempi di uso di ``dct:creator`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
       "dcterms:creator": {
        "@id": "http://dati.gov.it/resource/Amministrazione/agid"
      },
      
      altri elementi che descrivono il dataset
      
      Dove l'amministrazione creatore è specificata come:
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
 
  <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:creator rdf:resource="http://dati.gov.it/resource/Amministrazione/agid"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
 
 Dove l'amministrazione creatore è specificata come:
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
	dct:creator  	<http://dati.gov.it/resource/Amministrazione/agid> ;
	[altri elementi del dataset] .
 
 Dove l'amministrazione creatore è specificata come:
 <http://dati.gov.it/resource/Amministrazione/agid>
	a 		dcatapit:Agent , foaf:Agent ;
	dct:identifier  "agid" ;
	foaf:name       "Agenzia per l'Italia Digitale" .
```

##### 2) **_VERSIONE del DATASET:_** ``owl:versionInfo``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La versione del Dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2002/07/owl#versionInfo</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Utilizzato per specificare il numero della versione o altre indicazioni della versione del dataset. <b>Per indicare il numero della versione, è fortemente raccomandato l’utilizzo di numeri separati dal “.”.</b> Esempi: 0.7, 1.2.3, 1.10</td>
  </tr>
</table>

##### Esempi di uso di ``owl:versionInfo`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
        "owl:versionInfo": "2.0"
     },
      
      altri elementi che descrivono il dataset
      
 ```
 >``RDF/XML``
 
 ```XML
 
 <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <owl:versionInfo>2.0</owl:versionInfo>
        [altri elementi del dataset]
    </dcatapit:Dataset>
    
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a		 dcatapit:Dataset , dcat:Dataset ;
	owl:versionInfo	 "2.0" ;
	[altri elementi del dataset] .

```

##### 3) **_DATA di RILASCIO del DATASET:_** ``dct:issued``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di rilascio del Dataset</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/issued</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">E' la data in cui il dataset è reso disponibile.</td>
  </tr>
</table>

##### Esempi di uso di ``dct:issued`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD`

```JSON
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
        "dcterms:issued": {
        "@type": "xsd:date",
        "@value": "2012-01-15"
      },
      
      altri elementi del dataset

 ```
 >``RDF/XML``
 
 ```XML
 
    <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:issued rdf:datatype="&xsd;date">2012-01-15</dct:issued>
        [altri elementi del dataset]
    </dcatapit:Dataset>
 ```
 >``RDF/Turtle``
 
 ```Turtle
 <http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		dcatapit:Dataset , dcat:Dataset ;
	dct:issued	"2012-01-15"^^xsd:date ;
	[altri elementi del dataset] .
 ```
 
##### 4) **_PAGINA DI ACCESSO del DATASET:_** ``dcat:landingPage``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La pagina di accesso o landing page del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un oggetto (codominio) di tipo foaf:Document (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#landingPage</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Si raccomanda di utilizzare l’URL della pagina web che fornisce l’accesso al dataset o alla sua distribuzione o ad altre informazioni aggiuntive. La pagina di accesso è quella di origine del fornitore del dato. Non è valido l’URL di una pagina web riferibile a un sito fornito da una terza parte, come nel caso di un aggregatore.</td>
  </tr>
</table>

##### Esempi di uso di ``dcat:landingPage`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
        "dcat:landingPage": {
      	"@id": "http://spcdata.digitpa.gov.it/dataLotto1.html"
      },
      
      altri elementi del dataset

```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dcat:landingPage rdf:resource="http://spcdata.digitpa.gov.it/dataLotto1.html />
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dcat:landingPage <http://spcdata.digitpa.gov.it/dataLotto1.html> ; 
	[altri elementi del dataset] .
	
```
 ##### 5) **_LINGUA del DATASET:_** ``dct:language``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La lingua del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo dct:LinguisticSystem (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/language</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicaare una o più lingue utilizzate nel dataset. <b>La scelta della lingua è regolata dall'uso obbligatorio del <a href="http://publications.europa.eu/mdr/resource/authority/language/skos/languages-skos.rdf">vocabolario definito a livello Europeo sulle lingue.</a></b></td>
  </tr>
</table>

##### Esempi di uso di ``dct:language`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

       "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:language": {
        "@id": "http://publications.europa.eu/resource/authority/language/ITA"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:language rdf:resource="http://publications.europa.eu/resource/authority/language/ITA"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dct:language	<http://publications.europa.eu/resource/authority/language/ITA> ;
  
  [altri elementi del dataset] .
	
```
 
 ##### 6) **_PAROLE CHIAVE del DATASET:_** ``dcat:keyword``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La parole chiave associate al Dataset</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#keyword</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">inserire una o più parole chiave che consentono di identificare l'oggetto principale del dataset. Se si è scelto di inserire un tema più specifico per il dataset (soggetto o sotto tema)  assicurarsi che le parole chiave siano allineate ai temi e sotto temi usati, derivanti dai relativi vocabolari controllati.<br /><b> Si ricorda che nella definizione delle parole chiave non sono ammessi alcuni caratteri come la virgola, l'apostrofo, la "/" e altri caratteri non alfanumerici. Pertanto NON sono ammesse parole chiave come "controllo della qualità dell'aria" oppure "cave dismesse, cave" oppure "legge 190/2012". In questi casi si suggerisce di sostituirle rispettivamente con "controllo qualità aria" ovvero togliendo testo superfluo, "cave dismesse" "cave" ovvero separando le diverse parole chiave, "legge 190-2012" ovvero inserendo un "-", ecc.</b></td>
  </tr>
</table>

##### Esempi di uso di ``dcat:keyword`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
  
      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
        "dcat:keyword": [
      	"Contratto pubblico",
        "SPC",
        "Acquisizione"
      ],
       
      altri elementi del dataset

```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
       	<dcat:keyword>Acquisizione</dcat:keyword>
	<dcat:keyword>SPC</dcat:keyword>
        <dcat:keyword>Contratto pubblico</dcat:keyword>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dcat:keyword 	 "Acquisizione" , "Contratto pubblico" , "SPC" ;
	[altri elementi del dataset] .
	
```
 
#### 7) **_DATASET CORRELATO:_** ``dct:isVersionOf``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Un Dataset correlato che è una versione, un’edizione o un adattamento del Dataset descritto. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo <a href="#definizione-di-dcatapitdataset">Dataset</a> (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/isVersionOf</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Utilizzare l'URI del dataset correlato, ovvero il riferimento a una versione, un’edizione, un adattamento del dataset descritto. Per esempio, se si vuole inserire una nuova versione 2.0 di un dataset già presente nel catalogo (con versione 1.0) si richiede di indicare il riferimento al dataset già incluso nel catalogo. <b>Si sconsiglia fortemente comunque di creare nuovi dataset per piccoli cambiamenti. E’ invece consigliato definire nuovi dataset solo in presenza di cambiamenti significativi rispetto a precedenti versioni (e.g., nuovi elementi inclusi, adattamenti significativi di alcuni elementi, ecc).</b></td>
  </tr>
</table>

##### Esempi di uso di ``dct:isVersionOf`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

       "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      ""dcterms:isVersionOf": {
        "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid01"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:isVersionOf rdf:resource="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid01"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dct:isVersionOf	<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid01> ;
  
  [altri elementi del dataset] .
	
```

#### 8) **_ESTENSIONE TEMPORALE del DATASET:_** ``dct:temporal``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Un periodo temporale coperto dal Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo <a href="#come-definire-la-copertura-temporale-del-dataset-in-dcat-ap_it">Periodo di Tempo</a> (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/temporal</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Questo metadato è utilizzato per rappresentare, per esempio, casi quali “il dataset sul censimento della popolazione residente del 2011” oppure “il dataset sulla spesa pubblica dal 2000 al 2015". Per l'uso pratico di questa proprietà <a href="#esempi-di-uso-di-dctperiodoftime-in-json-ld-rdfxml-rdfturtle">si vedano gli esempi d'uso per la copertura temporale del Dataset</a> </td>
  </tr>
</table>

##### Esempi di uso di ``dct:temporal`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:temporal": {
        "@id": "http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:temporal rdf:resource="http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dct:temporal	<http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC> ;
  
  [altri elementi del dataset] .
	
```
 
#### 9) **_COPERTURA GEOGRAFICA del DATASET:_** ``dct:spatial``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Un'area geografica coperta dal Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a uno o più oggetti (codominio) di tipo <a href="#come-definire-la-copertura-geografica-del-dataset-in-dcat-ap_it">Localizzazione</a> (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/spatial</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Per l'uso pratico di questa proprietà <a href="#esempi-di-uso-di-dctlocation-e-locngeometry-in-json-ld-rdfxml-rdfturtle">si vedano gli esempi d'uso per la copertura geografica del Dataset</a> </td>
  </tr>
</table>

##### Esempi di uso di ``dct:spatial`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:spatial": {
        "@id": "http://www.geonames.org/3169070"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:spatial rdf:resource="http://www.geonames.org/3169070"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dct:spatial	<http://www.geonames.org/3169070> ;
  
  [altri elementi del dataset] .
	
```
 
#### 10) **_CONFORMITA' del DATASET:_** ``dct:conformsTo``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Una regola implementativa o altra specifica (e.g., una norma) a cui il Dataset è conforme. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un o più oggetti (codominio) di tipo <a href="#come-definire-lo-standard-del-dataset-in-dcat-ap_it">Standard</a> (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/conformsTo</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Specificare uno o più standard riferibili al dataset. Si possono specificare sia standard tecnici (anche de-facto) come per esempio DCAT, ISO/IEC 25012, CSW, ecc., sia riferimenti normativi (e.g., Decreto legislativo n.82/2005 - Codice dell’Amministrazione Digitale). Per l'uso pratico di questa proprietà <a href="#esempi-di-uso-di-dcatapitstandard-in-json-ld-rdfxml-rdfturtle">si vedano gli esempi d'uso per lo Standard del Dataset</a> </td>
  </tr>
</table>

##### Esempi di uso di ``dct:conformsTo`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "dcterms:conformsTo": {
        "@id": "http://dati.gov.it/resource/Standard/standard-org"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <dct:conformsTo rdf:resource="http://dati.gov.it/resource/Standard/standard-org"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	dct:conformsTo	<http://dati.gov.it/resource/Standard/standard-org> ;
  
  [altri elementi del dataset] .
	
```
 
#### 11) **_ALTRO IDENTIFICATIVO del DATASET:_** ``adms:identifier``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Un eventuale identificativo secondario del Dataset (e.g., DOI, ISBN, W3ID, ecc.). La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdataset">Dataset</a> a un o più oggetti (codominio) di tipo <a href="#definizione-di-admsidentifier">Altro Identificativo</a> (specificato mediante un URI- Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/adms#identifier</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Specificare uno o più identificativi secondari per il dataset. Per esempio, un identificativo secondario può essere un identificativo DOI (e.g., doi:10.10.1038/nphys1170) oppure un identificativo permanente per il Web W3ID (e.g., http://w3id.org/food) <b>oppure un identificativo stabile utilizzato in cataloghi locali</b>. Per l'uso pratico di questa proprietà <a href="#esempi-di-uso-di-admsidentifier-in-json-ld-rdfxml-rdfturtle">si vedano gli esempi d'uso per l'Identificativo Alternativo del Dataset</a></td>
  </tr>
</table>

##### Esempi di uso di ``adms:identifier`` per il Dataset in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Dataset/ContrattiSPC_agid",
      "@type": [
        "dcat:Dataset",
        "http://dati.gov.it/onto/dcatapit#\"Dataset"
      ],
      "adms:identifier": {
        "@id": "http://dati.gov.it/resource/Identifier/ContrattiSPC_agid_altroID"
      },
      
    altri elementi del dataset
```

>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Dataset/ContrattiSPC_agid -->
    <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
        <adms:identifier rdf:resource="http://dati.gov.it/resource/Identifier/ContrattiSPC_agid_altroID"/>
        [altri elementi del dataset]
    </dcatapit:Dataset>
```

>``RDF/Turtle``

```Turtle
 <<http://dati.gov.it/resource/Dataset/ContrattiSPC_agid>
	a 		 dcatapit:Dataset , dcat:Dataset ;
	adms:identifier	<http://dati.gov.it/resource/Identifier/ContrattiSPC_agid_altroID> ;
  
  [altri elementi del dataset] .
	
```
 
### Come definire una Distribuzione del Dataset in DCAT-AP_IT
Una distribuzione è definita mediante la classe _Distribution (Distribuzione)_ identificata univocamente da un URI (Uniform Resource Identifier).


#### Definizione di ``dcatapit:Distribution``

<table>
    <tr>
        <td align="left">URI</td>
        <td align="left">dcatapit:Distribution</td>
    </tr>
     <tr>
        <td align="left">Sottoclasse</td>
        <td align="left">dcat:Distribution</td>
    </tr>
    <tr>
        <td align="left">Descrizione</td>
        <td align="left">La distribuzione del dataset da descrivere.</td>
    </tr>
    <tr>
        <td align="left">Cardinalità</td>
        <td align="left">1..N (se in presenza di dati aperti)</td>
    </tr>
    <tr>
        <td align="left">Stato</td>
        <td align="left">Obbligatorio (se in presenza di dati aperti)</td>
    </tr>
     <tr>
        <td align="left">Riferimento</td>
        <td align="left">http://www.dati.gov.it/onto/dcatapit#Distribution</td>
    </tr>
</table>

#### Esempi di uso di dcatapit:Distribution in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
 {
      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
      "dcat:accessURL": {
        "@id": "http://spcdata.digitpa.gov.it:8899/sparql"
      },
      "dcat:downloadURL": {
        "@id": "http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt"
      },
      "dcterms:description": {
        "@language": "it",
        "@value": "Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"
      },
      "dcterms:format": {
        "@id": "http://publications.europa.eu/resource/authority/file-type/RDF"
      },
      "dcterms:license": {
        "@id": "http://creativecommons.org/licenses/by/4.0/"
      },
      "dcterms:title": "Distribuzione Turtle di LOD SPC Contratti"
 },


```
>``RDF/XML``

```XML
  <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->

    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dct:format rdf:resource="http://publications.europa.eu/resource/authority/file-type/RDF"/>
        <dct:title xml:lang="it">Distribuzione Turtle di LOD SPC Contratti</dct:title>
        <dct:description xml:lang="it">Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività</dct:description>
        <dct:license rdf:resource="http://creativecommons.org/licenses/by/4.0/"/>
        <dcat:downloadURL rdf:resource="http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt"/>
        <dcat:accessURL rdf:resource="http://spcdata.digitpa.gov.it:8899/sparql"/>
    </dcatapit:Distribution>
    
```
>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a			dcatapit:Distribution , dcat:Distribution ;
	dct:title		Distribuzione Turtle di LOD SPC Contratti"@it ;
	dct:description		"Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"@it ;
	dct:format 		<http://publications.europa.eu/resource/authority/file-type/RDF> ;
	dct:license 		<http://creativecommons.org/licenses/by/4.0/> ;
	dcat:downloadURL	<http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt> ;
	dcat:accessURL 		<http://spcdata.digitpa.gov.it:8899/sparql> .
```

#### Elementi obbligatori

##### 1) **_FORMATO della DISTRIBUZIONE:_** ``dct:format``

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
    <td align="left">Il formato della Distribuzione del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdistribution">Distribuzione(Distribution)</a> a un oggetto (codominio) di tipo dct:MediaTypeOrExtent (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/format</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Scegliere il formato in cui è reso disponibile il file relativo alla distribuzione descritta. Nel caso in cui il formato del file è di tipo “nidificato” (i.e. un file compresso, ad esempio nomefile.ttl.zip), allora indicare il formato originario del file compresso (nel caso dell’esempio, va indicato il formato ttl). <br /><b> Per specificare il formato si deve necessariamente utilizzare <a href="http://publications.europa.eu/mdr/resource/authority/file-type/skos/filetypes-skos.rdf">il vocabolario controllato definito a livello Europeo sui "File Type".</a> </b> 
   </td>
 </tr>
</table>

##### Esempi di uso di ``dct:format`` per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcterms:format": {
        "@id": "http://publications.europa.eu/resource/authority/file-type/RDF"
      },
      altri elementi per specificare la distribuzione
   
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dct:format rdf:resource="http://publications.europa.eu/resource/authority/file-type/RDF"/>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		  dcatapit:Distribution , dcat:Distribution ;
	dct:format 	  <http://publications.europa.eu/resource/authority/file-type/RDF> ;
	[altri elementi per specificare la distribuzione] .
```
 
##### 2) **_URL di ACCESSO:_** ``dcat:accessURL``

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
    <td align="left">Un URL tramite cui accedere alla Distribuzione del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdistribution">Distribuzione(Distribution)</a> a un oggetto (codominio) di tipo rdfs:Resource (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#accessURL</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Inserire l’URL di una pagina web tramite cui si possa accedere alla distribuzione. Essa può essere anche una pagina informativa che fornisce le indicazioni su come ottenere il dataset oppure l'URL di endpoint di accesso al dataset (e.g., SPARQL endpoint). Si consiglia di indicare l’indirizzo completo, comprensivo anche di protocollo (es. http://). <b> Si raccomanda di usare questa proprietà, e NON la proprietà <a href="#2-url-di-download-dcatdownloadurl">URL di download</a>, quando non è assolutamente una pagina di download o non si è sicuri che lo sia.</b></td>
 </tr>
</table>

##### Esempi di uso di ``dcat:accessURL``per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcat:accessURL": {
        "@id": "http://spcdata.digitpa.gov.it:8899/sparql"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dcat:accessURL rdf:resource="http://spcdata.digitpa.gov.it:8899/sparql"/>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		   dcatapit:Distribution , dcat:Distribution ;
	dcat:accessURL 	  <http://spcdata.digitpa.gov.it:8899/sparql> ;
	[altri elementi per specificare la distribuzione] .
```
 
##### 3) **_LICENZA:_** ``dct:license``

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
    <td align="left">La licenza con la quale è resa disponibile, per il riutilizzo, la Distribuzione del Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdistribution">Distribuzione(Distribution)</a> a un oggetto (codominio) di tipo <a href="#definizione-di-dcatapitlicensedocument">Licenza</a> (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/license</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Per un uso pratico del metadato licenza si veda <a href="#esempi-di-uso-di-dcatapitlicensedocument-in-json-ld-rdfxml-rdfturtle">Come definire la licenza.</a><br /><b> Si raccomanda tuttavia, in presenza di licenze creative commons, di riferirsi a quelle specificate in http://creativecommons.org come negli esempi sotto riportati.</b></td>
 </tr>
</table>

##### Esempi di uso di ``dct:license`` per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcterms:license": {
        "@id": "http://creativecommons.org/licenses/by/4.0/"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dct:license rdf:resource="http://creativecommons.org/licenses/by/4.0/"/>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		   dcatapit:Distribution , dcat:Distribution ;
	dct:license 	  <http://creativecommons.org/licenses/by/4.0/> ;
	[altri elementi per specificare la distribuzione] .
```
 
#### Elementi raccomandati

##### 1) **_DESCRIZIONE della DISTRIBUZIONE:_** ``dct:description``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Raccomandato</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La descrizione della Distribuzione del Dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/description</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Specificare una descrizione per la distribuzione, con una breve illustrazione delle sue caratteristiche principali. <b>Evitare di utilizzare un linguaggio ricco di riferimenti normativi</b>. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare la distribuzione. Si ricorda che nessun tag HTML è consentito,</td>
 </tr>
</table>

##### Esempi di uso di ``dct:description`` per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcterms:description": {
        "@language": "it",
        "@value": "Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
       <rdf:type rdf:resource="&dcat;Distribution"/>
       <dct:description xml:lang="it">Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività</dct:description>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		 dcatapit:Distribution , dcat:Distribution ;
	dct:description	 "Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"@it ;
	[altri elementi per specificare la distribuzione] .
```

#### Elementi opzionali

##### 1) **_TITOLO della DISTRIBUZIONE:_** ``dct:title``
 
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il titolo della Distribuzione del Dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Se disponibile o ritenuto opportuno, inserire un titolo della distribuzione. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso o fornire una loro spiegazione.</td>
 </tr>
</table>

##### Esempi di uso di ``dct:title`` per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcterms:description": {
        "@language": "it",
        "@value": "Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
       <rdf:type rdf:resource="&dcat;Distribution"/>
       <dct:description xml:lang="it">Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività</dct:description>
       [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		 dcatapit:Distribution , dcat:Distribution ;
	dct:description	 "Questa è la distribuzione N3 del dataset Linked Open Data relativo ai contratti del Sistema Pubblico di Connettività"@it ;
	[altri elementi per specificare la distribuzione] .
```


##### 2) **_URL di DOWNLOAD:_** ``dcat:downloadURL``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Un URL che rappresenta un link diretto al file scaricabile in un dato formato. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitdistribution">Distribuzione(Distribution)</a> a un oggetto (codominio) di tipo rdfs:Resource (specificato mediante un URI - Uniform Resource Identifier)</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#downloadURL</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare l’URL che fornisce il link diretto a un file scaricabile nel formato indicato per la distribuzione. Si consiglia di indicare l’indirizzo completo, comprensivo anche di protocollo (es. http://).</td>
 </tr>
</table>

##### Esempi di uso di ``dcat:downloadURL``per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcat:downloadURL": {
        "@id": "http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dcat:downloadURL rdf:resource="http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt"/>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		   dcatapit:Distribution , dcat:Distribution ;
	dcat:downloadURL   <http://spcdata.digitpa.gov.it/data/contrattiLotto1.nt> ;
	[altri elementi per specificare la distribuzione] .
```

##### 3) **_ULTIMA MODIFICA della DISTRIBUZIONE:_** ``dct:modified``
 
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di ultima modifica della Distribuzione del Dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/modified</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare la data di ultima modifica o di aggiornamento della distribuzione.</td>
 </tr>
</table>

##### Esempi di uso di ``dct:modified`` per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcterms:modified": {
        "@type": "xsd:date",
        "@value": "2015-05-25"
      },

      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
        <dct:modified rdf:datatype="&xsd;date">2015-05-25</dct:modified>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		 dcatapit:Distribution , dcat:Distribution ;
	dct:modified	"2015-05-25"^^xsd:date ;
	[altri elementi per specificare la distribuzione] .
```

##### 4) **_DIMENSIONE in BYTE:_** ``dcat:byteSize``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La dimensione in byte della distribuzione del dataset</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">https://www.w3.org/ns/dcat#byteSize</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare il valore della dimensione del file espresso in byte</td>
 </tr>
</table>

##### Esempi di uso di ``dcat:byteSize``per la Distribuzione in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON

      "@id": "http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"Distribution",
        "dcat:Distribution"
      ],
       "dcat:byteSize": {
        "@type": "xsd:float",
        "@value": "3000"
      },
      altri elementi per specificare la distribuzione
```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3 -->
    <dcatapit:Distribution rdf:about="http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3">
        <rdf:type rdf:resource="&dcat;Distribution"/>
       <dcat:byteSize rdf:datatype="&xsd;float">3000</dcat:byteSize>
        [altri elementi per specificare la distribuzione]
   </dcatapit:Distribution>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/Distribuzione/SPCContratti_agid-N3>
	a		   dcatapit:Distribution , dcat:Distribution ;
	dcat:byteSize	   "3000"^^xsd:float ;
	[altri elementi per specificare la distribuzione] .
```

### Come definire un Soggetto o Organizzazione in DCAT-AP_IT
Un soggetto/organizzazione è definito mediante la specifica della classe _Agente (Agent)_ identificata univocamente da un URI (Uniform Resource Identifier).

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
<td align="left">1..N</td>
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

##### 1) **_IDENTIFICATIVO del SOGGETTO_**: ``dct:identifier``

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

##### 2) **_NOME del SOGGETTO_**: ``foaf:name``
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

#### Esempi di uso di dcatapit:Agent in JSON-LD, RDF/XML, RDF/Turtle
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

### Come definire la licenza in DCAT-AP_IT
La licenza è definita mediante la specifica della classe _dcatapti:LicenseDocument_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dcatapit:LicenseDocument``

<table>
<tr>
<td align="left">URI</td>
<td align="left">dcatapit:LisenceDocument</td>
</tr>
<tr>
<td align="left">Sottoclasse</td>
<td align="left">dct:LicenseDocument</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">La licenza della distribuzione del dataset.</td>
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
<td align="left">http://www.dati.gov.it/onto/dcatapit#LicenseDocument</td>
</tr>
</table>


#### Elementi raccomandati che descrivono la Licenza
##### 1) **_TIPO della LICENZA_**: ``dct:type``
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
    <td align="left">Il tipo di licenza associata alla distribuzione del dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitlicensedocument">dcatapit:LicenseDocument</a> a un oggetto (codominio) di tipo skos:Concept (specificato mediante un URI - Uniform Resource Identifier).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/type</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare il tipo di licenza. Esempi: “pubblico dominio”, “richiesto pagamento diritti”. I valori da utilizzare per  questa  proprietà sono gli URI dei concetti del vocabolario <a href="http://purl.org/adms/licencetype/">“ADMS licence type vocabulary.”</a></td>
  </tr>
</table>


#### Elementi opzionali che descrivono la Licenza
##### 1) **_NOME della LICENZA:_** ``foaf:name``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (possono esistere più istanze di questa proprietà, una per ogni lingua</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il nome della licenza.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://xmlns.com/foaf/0.1/name</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare il nome della licenza associata alla distribuzione. Esempio: "CC_BY" oppure "Creative Commons Attribution (CC-BY)".</td>
  </tr>
</table>

##### 2) **_VERSIONE della LICENZA:_** ``owl:versionInfo``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La versione della licenza</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2002/07/owl#versionInfo</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare la versione della licenza. Esempio: "4.0" oppure "3.0"</td>
  </tr>
</table>

#### Esempi di uso di dcatapit:LicenseDocument in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
   {
      "@id": "http://creativecommons.org/licenses/by/4.0/",
      "@type": [
        "http://dati.gov.it/onto/dcatapit#\"LicenseDocument",
        "dcterms:LicenseDocument"
      ],
      "dcterms:type": {
        "@id": "http://purl.org/adms/licencetype/Attribution"
      },
      "foaf:name": "CC BY",
      "owl:versionInfo": "4.0"
    },

```

>``RDF/XML``

```XML

   <!-- http://creativecommons.org/licenses/by/4.0/ -->
    <dcatapit:LicenseDocument rdf:about="http://creativecommons.org/licenses/by/4.0/">
        <rdf:type rdf:resource="&dct;LicenseDocument"/>
        <dct:type rdf:resource="http://purl.org/adms/licencetype/Attribution"/>
        <owl:versionInfo>4.0</owl:versionInfo>
        <foaf:name>CC BY</foaf:name>
    </dcatapit:LicenseDocument>
   
```

>``RDF/Turtle``

```Turtle
<http://creativecommons.org/licenses/by/4.0/>
	a		 dcatapit:LicenseDocument , dct:LicenseDocument ;
	dct:type	 <http://purl.org/adms/licencetype/Attribution> ;
	foaf:name	 "CC BY" ;
	owl:versionInfo	 "4.0" .

```


### Come definire il Punto di Contatto del Dataset in DCAT-AP_IT
Il punto di contatto è definito mediante la specifica della classe _dcatapti:Organization_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dcatapit:Organization``

<table>
<tr>
<td align="left">URI</td>
<td align="left">dcatapit:Organization</td>
</tr>
<tr>
<td align="left">Sottoclasse</td>
<td align="left">vcard:Organization a sua volta sotto classe di vcard:Kind</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">Un ufficio/organizzazione che agisce come punto di contatto per il dataset.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">0..N</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Raccomandato</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://www.dati.gov.it/onto/dcatapit#Organization</td>
</tr>
</table>

#### Elementi obbligatori che descrivono il Punto di Contatto

##### 1) **_NOME del PUNTO di CONTATTO_**: ``vcard:fn``

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
    <td align="left">Il nome del contatto stabile per il dataset.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2006/vcard/ns#fn</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">E’ fortemente raccomandato indicare il nome di uno specifico ufficio (unità organizzativa) responsabile della raccolta delle richieste/commenti e della predisposizione delle relative risposte. Solo se non è possibile individuare il riferimento dell’ufficio, si può indicare l’organizzazione nel suo complesso. Sono da evitare comunque nomi di singole persone. Questo metadato deve essere specificato qualora si inseriscano informazioni di contatto per il dataset. Per esempio, per il dataset LOD dell’Indice della Pubblica amministrazione il nome dell’ufficio/organizzazione è “banche dati e open data".</td>
  </tr>
</table>

##### 2) **_EMAIL del PUNTO DI CONTATTO_**: ``vcard:hasEmail``
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
    <td align="left">L’indirizzo email del punto di contatto per il Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitorganization">dcatapit:Organization</a> a un oggetto (codominio) di tipo vcard:Email (specificato mediante un URI - Uniform Resource Identifier).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2006/vcard/ns#hasEmail</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare l’indirizzo email primario dell’ufficio (o gestito dall’ufficio) identificato come punto di contatto per il dataset. Se non è possibile identificare l’ufficio, si può inserire l’indirizzo email principale dell’organizzazione. Evitare in ogni caso di specificare indirizzi email di singole persone fisiche. Questo metadato deve essere specificato qualora si inseriscano informazioni di contatto per il dataset. Esempio: “mailto:info@dati.gov.it"</td>
  </tr>
</table>

#### Elementi opzionali che descrivono il Punto di Contatto

##### 1) **_TELEFONO del PUNTO di CONTATTO_**: ``vcard:hasTelephone``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il telefono del contatto stabile per il dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitorganization">dcatapit:Organization</a> a un oggetto (codominio) di tipo vcard:TelephoneType (specificato mediante un URI - Uniform Resource Identifier).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2006/vcard/ns#hasTelephone</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare il numero di telefono dell’ufficio (o gestito dall’ufficio) identificato come punto di contatto per il dataset. Se non è possibile identificare l’ufficio, si può indicare il numero di telefono del centralino dell’amministrazione. Evitare in ogni caso di specificare numeri di telefono di singole persone.</td>
  </tr>
</table>

##### 2) **_SITO del PUNTO DI CONTATTO_**: ``vcard:hasURL``
<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">L’La pagina di contatto per il Dataset. La proprietà lega l'oggetto (dominio) <a href="#definizione-di-dcatapitorganization">dcatapit:Organization</a> a un oggetto (codominio) di tipo owl:Thing (specificato mediante un URI - Uniform Resource Identifier).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2006/vcard/ns#hasURL</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Se esiste, inserire l’URL primario di una pagina di contatto o di un form di contatto. Evitare il più possibile di indicare l’URL dell’home page dell’organizzazione. Un esempio di possibile valore per questo metadato è il seguente “http://spcdata.digitpa.gov.it/contattaci.html  (NON dovrebbe essere per esempio “httpi://www.agid.gov.it”). Nel caso in cui si abbia la necessità di indicare ulteriori URL di interesse per la risorsa descritta, oltre a quello principale, si possono aggiungere più istanze della proprietà foaf:page.</td>
  </tr>
</table>

#### Esempi di uso di dcatapit:Organization in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
   {
     "@id": "http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA",
      "@type": [
        "vcard:Organization",
        "vcard:Kind",
        "http://dati.gov.it/onto/dcatapit#\"Organization"
      ],
      "vcard:fn": "banche dati e open data",
      "vcard:hasEmail": {
        "@id": "mailto:info@dati.gov.it"
      },
      "vcard:hasTelephone": {
        "@id": "_:N423506244f6e46028ea51a957fe407f3"
      },
      "vcard:hasURL": {
        "@id": "http://spcdata.digitpa.gov.it/contattaci.html"
      }
      {
       "@id": "_:N423506244f6e46028ea51a957fe407f3",
       "@type": "vcard:Voice",
       "vcard:value": "06123456"
       },
    },

```

>``RDF/XML``

```XML

   <!-- http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA -->
    <dcatapit:Organization rdf:about="http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA">
        <rdf:type rdf:resource="&vcard;Kind"/>
        <rdf:type rdf:resource="&vcard;Organization"/>
        <vcard:hasEmail rdf:resource="mailto:info@dati.gov.it"/>
        <vcard:fn>banche dati e open data</vcard:fn>
        <vcard:hasTelephone rdf:parseType="Resource">
         	<vcard:value>06123456</vcard:value>
         	<rdf:type rdf:resource="http://www.w3.org/2006/vcard/ns#Voice"/>
        </vcard:hasTelephone>
        <vcard:hasURL rdf:resource="http://spcdata.digitpa.gov.it/contattaci.html"/>
    </dcatapit:Organization>

   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/PuntoContatto/contactPointLODIPA>
	a				catapit:Organization , vcard:Organization, vcard:Kind ;
	vcard:fn			"banche dati e open data" ;
	vcard:hasEmail 			<mailto:info@dati.gov.it> ;
	vcard:hasTelephone		[ a vcard:Voice ; vcard:value "06123456" ] ;
	vcard:hasURL			<http://spcdata.digitpa.gov.it/contattaci.html> .
```

#### Come definire la copertura temporale del Dataset in DCAT-AP_IT
La copertura (o estensione) temporale del dataset è definita mediante la specifica della classe _PeriodOfTime (Periodo di Tempo)_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dct:PeriodOfTime``

<table>
<tr>
<td align="left">URI</td>
<td align="left">dct:PeriodOfTime</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">L'estensione temporale del dataset.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">0..N</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Opzionale</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://purl.org/dc/terms/PeriodOfTime</td>
</tr>
</table>

#### Elementi obbligatori che descrivono il Periodo di Tempo

##### 1) **_DATA INIZIO_**: ``dcatapit:startDate``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">1</td>
  </tr>
  <tr> 
    <td align="left">Sottoproprietà</td>
    <td align="left">schema:startDate</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Obbligatorio</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di inizio del Periodo di tempo (estensione temporale).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://dati.gov.it/onto/dcatapit#startDate</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Qualora si indichi una copertura temporale per il dataset è obbligatorio specificare almeno la data di inizio</td>
  </tr>
</table>

#### Elementi opzionali che descrivono il Periodo di Tempo

##### 1) **_DATA FINE_**: ``dcatapit:endDate``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Sottoproprietà</td>
    <td align="left">schema:endDate</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La data di fine del Periodo di tempo (estensione temporale).</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://dati.gov.it/onto/dcatapit#endDate</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare la data di fine del periodo temporale qualora il periodo temporale complessivo è ultimato. Nel caso di periodi temporali ancora aperti alla data corrente, si può evitare di specificare questo metadato. </td>
  </tr>
</table>

#### Esempi di uso di dct:PeriodOfTime in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
   {
      "@id": "http://dati.gov.it/resource/PeriodoTemporale/periodTimeLinkedOpenIPA",
      "@type": "dcterms:PeriodOfTime",
      "http://dati.gov.it/onto/dcatapit#\"startDate": {
        "@type": "xsd:date",
        "@value": "2016-01-01"
      }
    }

```

>``RDF/XML``

```XML

  <!-- http://dati.gov.it/resource/PeriodoTemporale/periodTimeLinkedOpenIPA -->
    <dct:PeriodOfTime rdf:about="http://dati.gov.it/resource/PeriodoTemporale/periodTimeLinkedOpenIPA">
        <dcatapit:startDate rdf:datatype="&xsd;date">2016-01-01</dcatapit:startDate>
    </dct:PeriodOfTime>
   
```

>``RDF/Turtle``

```Turtle
<http://dati.gov.it/resource/PeriodoTemporale/periodTimeContrattiSPC>
	a 			dct:PeriodOfTime ;
	dcatapit:startDate	"2007-01-01"^^xsd:date ;
	dcatapit:endDate	"2012-12-31"^^xsd:date .
```

### Come definire la copertura geografica del Dataset in DCAT-AP_IT
La copertura geografica del dataset è definita mediante la specifica della classe _Location (Localizzazione)_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dct:Location``
<table>
<tr>
<td align="left">URI</td>
<td align="left">dct:Location:</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">La copertura geografica del dataset.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">0..N</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Opzionale</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://purl.org/dc/terms/Location</td>
</tr>
</table>

#### Elementi opzionali che descrivono la copertura geografica

##### 1) **_NOME GEOGRAFICO_**: ``locn:geographicName``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Nome proprio associato all'oggetto spaziale.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/locn#geographicName"</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Da indicare solo se non è disponibile un identificativo geografico o non sono note le coordinate.</b></td>
  </tr>
</table>

##### 2) **_GEOMETRIA_**: ``loc:Geometry``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..1</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La Geometria dell'oggetto spaziale..</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/ns/locn#Geometry"</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Le proprietà  indicate,  nella  pratica,  possono  essere  specificate  attraverso  diverse  codifiche.  La
specifica <a href="https://joinup.ec.europa.eu/asset/dcat_application_profile/asset_release/geodcat-ap-v10">GeoDCAT-AP</a> prevede che debba essere utilizzata almeno una delle seguenti: GML o WKT.</td>
  </tr>
</table>

#### Elementi che descrivono la geometria della copertura geografica
I seguenti elementi sono obbligatori se la geometria dell'oggetto spaziale che descrive la copertura geografica del dataset viene specificata.

##### 1) **_CRS_**

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
    <td align="left">L’indicazione del sistema di riferimento spaziale in cui sono rappresentati i dati. Secondo quanto indicato in <a href="https://joinup.ec.europa.eu/asset/dcat_application_profile/asset_release/geodcat-ap-v10">GeoDCAT-AP</a>, nelle codifiche GML o WKT il CRS deve essere specificato come definito in GeoSPARQL.</td>
  </tr>
</table>

##### 2) **_COORDINATE_**

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
    <td align="left">Le coordinate dell’area geografica coperta dal Dataset.
</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Fornire le coordinate relative alla latitudine e longitudine, espresse nel sistema di riferimento WGS84, del riquadro di delimitazione (bounding box) dell’area geografica coperta dal dataset descritto. Se è stato già indicato un identificativo geografico come URI della classe <a href="#definizione-di-dctlocation">dct:Location</a>, le coordinate possono essere omesse.</td>
  </tr>
</table>

##### 3) **_TIPO DI GEOMETRIA_**

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
    <td align="left">Il tipo di geometria che caratterizza l’oggetto spaziale utilizzato per la localizzazione del Dataset (es., punto (point)). </td>
  </tr>
</table>

##### Esempi di uso di dct:Location e locn:Geometry in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
{
      "@id": "http://dati.gov.it/resource/CoperturaSpaziale/LocalizzazioneStudiMedici_r_liguri:D.658",
      "@type": "dcterms:Location",
      "locn:geometry": {
        "@type": "gsp:gmlLiteral",
        "@value": "<gml:Envelope srsName=\"http://www.opengis.net/def/EPSG/0/4326\"><gml:lowerCorner>7.48820862370018 43.5963597132668</gml:lowerCorner><gml:upperCorner>10.0879518636137 44.849579861466</gml:upperCorner></gml:Envelope>"
      }
    },
```
>``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/CoperturaSpaziale/LocalizzazioneLineaCosta -->
    <dct:Location rdf:about="http://dati.gov.it/resource/CoperturaSpaziale/LocalizzazioneLineaCosta_r_liguri:D.658">
        <locn:geometry rdf:datatype="&gsp;gmlLiteral">&lt;gml:Envelope srsName=&quot;http://www.opengis.net/def/EPSG/0/4326&quot;&gt;&lt;gml:lowerCorner&gt;7.48820862370018 43.5963597132668&lt;/gml:lowerCorner&gt;&lt;gml:upperCorner&gt;10.0879518636137 44.849579861466&lt;/gml:upperCorner&gt;&lt;/gml:Envelope&gt;</locn:geometry>
    </dct:Location>
```
>``RDF/Turtle``
```Turtle
<http://dati.gov.it/resource/CoperturaSpaziale/LocalizzazioneLineaCosta_r_liguri:D.658>
	a		dct:Location ;
	locn:geometry	"<gml:Envelope srsName=\"http://www.opengis.net/def/EPSG/0/4326\"><gml:lowerCorner>7.48820862370018 43.5963597132668</gml:lowerCorner><gml:upperCorner>10.0879518636137 44.849579861466</gml:upperCorner></gml:Envelope>"^^gsp:gmlLiteral .
	
```


### Come definire lo Standard del Dataset in DCAT-AP_IT
Uno standard è definito mediante la specifica della classe _Standard_ identificata univocamente da un URI (Uniform Resource Identifier).

#### Definizione di ``dcatapit:Standard``

<table>
<tr>
<td align="left">URI</td>
<td align="left">dcatapit:Standard</td>
</tr>
<tr>
<td align="left">Sottoclasse</td>
<td align="left">dct:Standard</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">Uno standard al quale il dataset è conforme.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">0..N</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Opzionale</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://www.dati.gov.it/onto/dcatapit#Standard</td>
</tr>
</table>

#### Elementi obbligatori che descrivono lo Standard

##### 1) **_IDENTIFICATIVO dello STANDARD_**: ``dct:identifier``

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
    <td align="left">L'identificativo dello standard.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/identifier</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Inserire l’URL di riferimento dello Standard. Nel caso di riferimenti normativi, includere il link permanente disponibile presso la gazzetta ufficiale (e.g., www.gazzettaufficiale.it/eli/id/2005/05/16/005G0104/sg). E’ obbligatorio specificare l’identificativo qualora si scelga di descrivere standard riferibili al dataset.</td>
  </tr>
</table>

#### Elementi opzionali che descrivono lo Standard

##### 1) **_TITOLO dello STANDARD_**: ``dct:title``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">Il titolo dello standard.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare un titolo dello standard comprensibile in quanto il metadato potrebbe essere utilizzato nella ricerca e nelle indicizzazioni (evitare acronimi, evitare codici non esaustivi).  Nel caso di riferimenti normativi, indicare per esempio la tipologia di norma il numero e l’anno e inserire il titolo ufficiale della norma.</td>
  </tr>
</table>

##### 2) **_DESCRIZIONE dello STANDARD_**: ``dct:description``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N (può esistere più di un'istanza, in diverse lingue, della stessa proprietà)</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">La descrizione dello standard.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://purl.org/dc/terms/description</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare una descrizione per lo standard. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare lo standard riferibile al dataset. Si ricorda che nessun tag HTML è consentito,</td>
  </tr>
</table>

##### 3) **_DOCUMENTAZIONE di RIFERIMENTO_**: ``dcatapit:referenceDocumentation``

<table>
  <tr> 
    <td align="left">Cardinalità</td>
    <td align="left">0..N</td>
  </tr>
  <tr> 
    <td align="left">Stato</td>
    <td align="left">Opzionale</td>
  </tr>
  <tr>
    <td align="left">Descrizione</td>
    <td align="left">URL attraverso i quali viene fornito l’accesso a documenti di dettaglio relativi allo Standard indicato.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.dati.gov.it/onto/dcatapit#referenceDocumentation</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left">Indicare uno o più URL della documentazione di riferimento relativa allo standard. Ad esempio, nel caso della raccomandazione DCAT, alcuni URL relativi alla documentazione di riferimento sono: https://www.w3.org/TR/vocab-dcat/ e https://www.w3.org/ns/dcat.rdf</td>
  </tr>
</table>

#### Esempi di uso di dcatapit:Standard in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
{
      "@id": "http://dati.gov.it/resource/Standard/standard-org",
      "@type": [
        "dcterms:Standard",
        "http://dati.gov.it/onto/dcatapit#\"Standard"
      ],
      "dcterms:description": {
        "@language": "en",
        "@value": "The ontology of the organizations"
      },
      "dcterms:title": {
        "@language": "en",
        "@value": "W3C Org organization ontology"
      },
      "http://dati.gov.it/onto/dcatapit#\"referenceDocumentation": [
        {
          "@type": "xsd:anyURI",
          "@value": "https://www.w3.org/TR/vocab-org/"
        },
        {
          "@type": "xsd:anyURI",
          "@value": "https://www.w3.org/ns/org.rdf"
        }
      ]
    },

    
```
> ``RDF/XML``

```XML
<!-- http://dati.gov.it/resource/Standard/standard-org -->
    <dcatapit:Standard rdf:about="http://dati.gov.it/resource/Standard/standard-org">
        <rdf:type rdf:resource="&dct;Standard"/>
        <dcatapit:referenceDocumentation rdf:datatype="&xsd;anyURI">https://www.w3.org/TR/vocab-org/</dcatapit:referenceDocumentation>
        <dcatapit:referenceDocumentation rdf:datatype="&xsd;anyURI">https://www.w3.org/ns/org.rdf</dcatapit:referenceDocumentation>
        <dct:title xml:lang="en">W3C Org organization ontology</dct:title>
        <dct:description xml:lang="en">The ontology of the organizations</dct:description>
    </dcatapit:Standard>

```
> ``RDF/TURTLE``

```Turtle
   <http://dati.gov.it/resource/Standard/standard-org>
	a				dcatapit:Standard , dct:Standard ;
	dct:title			"W3C Org organization ontology"@en ;
	dct:description			"The ontology of the organizations"@en ;
	dcatapit:referenceDocumentation "https://www.w3.org/ns/org.rdf"^^xsd:anyURI ;
	dcatapit:referenceDocumentation "https://www.w3.org/TR/vocab-org/"^^xsd:anyURI .
```


#### Come definire un identificativo alternativo del Dataset in DCAT-AP_IT
L'identificativo alternativo del dataset può essere specificato mediante la classe _adms:Identifier_ specificata mediante un URI (Uniform Resource Identifier)

#### Definizione di ``adms:Identifier``

<table>
<tr>
<td align="left">URI</td>
<td align="left">adms:Identifier</td>
</tr>
<tr>
<td align="left">Descrizione</td>
<td align="left">Un identificativo alternativo per il dataset.</td>
</tr>
<tr>
<td align="left">Cardinalità</td>
<td align="left">0..N</td>
</tr>
<tr>
<td align="left">Stato</td>
<td align="left">Opzionale</td>
</tr>
<tr>
<td align="left">Riferimento</td>
<td align="left">http://www.w3.org/ns/adms#Identifier</td>
</tr>
</table>

### Elementi raccomandati che descrivono altro identificativo del dataset
##### 1) **_NOTAZIONE_**: ``skos:notation``
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
    <td align="left">Descrizione</td>
    <td align="left">Un identificativo, nel contesto dello schema di identificazione, a cui fa riferimento il suo tipo.</td>
  </tr>
  <tr>
    <td align="left">Riferimento</td>
    <td align="left">http://www.w3.org/2004/02/skos/core#notation</td>
  </tr>
</table>

#### Esempi di uso di adms:Identifier in JSON-LD, RDF/XML, RDF/Turtle
>``JSON-LD``

```JSON
   {
      "@id": "http://dati.gov.it/resource/AltroIdentificativo/altroidentificativoDataset1",
      "@type": "adms:Identifier",
      "skos:notation": {
        "@value": "doi:10.1109/5.771073"
      }
    }

```

>``RDF/XML``

```XML

  <!-- http://dati.gov.it/resource/AltroIdentificativo/altroidentificativoDataset1 -->
    <adms:Identifier rdf:about="http://dati.gov.it/resource/AltroIdentificativo/altroidentificativoDataset1">
        <skos:notation>"doi:10.1109/5.771073"</skos:notation>
    </adms:Identifier>
   
```

>``RDF/Turtle``

```Turtle
<hhttp://dati.gov.it/resource/AltroIdentificativo/altroidentificativoDataset1>
	a 		adms:Identifier ;
	skos:notation	"doi:10.1109/5.771073" ;
```



#### Come mappare i temi di DCAT-AP_IT
I temi in cui i dataset sono classificati si basano sull'uso del vocabolario controllato come indicato nella sezione ["Temi del Dataset dcat:theme"](#5-temi-del-dataset-dcattheme). Sulla base della [valutazione dei diversi temi per i dati discussa nell'ambito del gruppo Europeo DCAT-AP](https://joinup.ec.europa.eu/asset/dcat_application_profile/document/review-dcat-ap-draft-proposal-list-categorization-data), la tabella seguente offre un possibile mapping di domini applicativi rispetto ai temi richiesti dal profilo DCAT-AP_IT.

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

### Riepilogo dei vocabolari controllati da utilizzare

<table>
    <tr>
    	<td align="left"><b>Oggetto</b></td>
	<td align="left"><b>Riferimento del vocabolario controllato</b></td>
    </tr>
    <tr>
        <td align="left">Lingua del Catalogo e del Dataset</td>
        <td align="left">http://publications.europa.eu/mdr/resource/authority/language/skos/languages-skos.rdf</td>
    </tr>
    <tr>
        <td align="left">Tema del Dataset</td>
        <td align="left">http://publications.europa.eu/mdr/resource/authority/data-theme/skos/data-theme-skos.rdf</td>
    </tr>
    <tr>
        <td align="left">Sottotema del Dataset</td>
        <td align="left">http://eurovoc.europa.eu/</td>
    </tr>
    <tr>
        <td align="left">Frenquenza di Aggiornamento del Dataset</td>
        <td align="left">http://publications.europa.eu/mdr/resource/authority/frequency/skos/frequencies-skos.rdf</td>
    </tr>
    <tr>
        <td align="left">Formato della Distribuzione</td>
        <td align="left">http://publications.europa.eu/mdr/resource/authority/file-type/skos/filetypes-skos.rdf</td>
    </tr>
    <tr>
        <td align="left">Tipo di Licenza della Distribuzione</td>
        <td align="left">http://purl.org/adms/licencetype</td>
    </tr>
    <tr>
        <td align="left">Identificativo della Localizzazione (copertura geografica) del Dataset</td>
        <td align="left">http://sws.geonames.org/</td>
    </tr>
</table>


### Alcuni errori comuni

**URI**. L'errore più diffuso riguarda la gestione degli URI. Si ricorda che oggetti di tipo diverso devono avere URI differenti. Per esempio, **NON** è corretto utilizzare lo stesso URI per definire <a href="#definizione-di-dcatapit:Agent">il soggetto o organizzazione </a> che ha un certo ruolo (titolare, editore, creatore) su un catalogo o dataset, e per definire <a href="#definizione-di-dcatapit:Organization">il punto di contatto del dataset</a>. I due concetti sono diversi e devono avere URI diversi. Ci si riferisca <a href="#esempi-di-uso-di-dcatapitagent-in-json-ld-rdfxml-rdfturtle">agli esempi di uso di Soggetto o Organizzazione</a> e di <a href="#esempi-di-uso-di-dcatapitorganization-in-json-ld-rdfxml-rdfturtle">Punto di Contatto</a> per maggiori dettagli.

**Differenza tra Literal(valore) e URI**. Molto spesso, soprattutto in presenza di dati serializzati in RDF/XML si tende a confondere il concetto di URI <http://....> con una stringa che all'interno contiene un URI "http://....". In quest'ultimo caso non si sta definendo un URI ma un valore (detto Literal nel contesto RDF). Per esempio:

il seguente codice **è** corretto:

```XML
 <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
       	<dcat:theme rdf:resource="http://publications.europa.eu/resource/authority/data-theme/ECON"/>
 ...
 </dcatapit:Dataset>

```
il seguente codice definirebbe il tema come una stringa che include un URI e **NON** è corretto rispetto alle specifiche riguardanti il tema del Dataset:
 
```XML
 <dcatapit:Dataset rdf:about="http://dati.gov.it/resource/Dataset/ContrattiSPC_agid">
        <rdf:type rdf:resource="&dcat;Dataset"/>
       	<dcat:theme>"http://publications.europa.eu/resource/authority/data-theme/ECON"</dcat:theme>
 ...
 </dcatapit:Dataset>
 ```
