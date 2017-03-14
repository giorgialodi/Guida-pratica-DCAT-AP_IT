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
    * [Elementi obbligatori che descrivono un Soggetto o Organizzazione in DCAT-AP_IT](#elementi-obbligatori-che-descrivono-un-soggetto-o-organizzazione-in-dcat-ap_it)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-in-json-ld-rdfxml-rdfturtle)
  * [Come definire un catalogo in DCAT-AP_IT](#come-definire-un-catalogo-di-dati-in-dcat-ap_it)
    * [dcatapit:Catalog](#definizione-di-dcatapitcatalog)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#esempi-di-uso-in-json-ld-rdfxml-rdfturtle-1)
    * [Elementi obbligatori](#elementi-obbligatori)
      * [Titolo del catalogo](#esempi-di-uso-di-dcttitle-per-il-catalogo-in-json-ld-rdfxml-rdfturtle)
      * [Descrizione del catalogo](#dctdescription-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Editore del catalogo](#dctpublisher-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Data di ultima modifica del catalogo](#dctmodified-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Dataset del catalogo](#dcatdataset-JSONLD-RDFXML-RDFTURTLE)
    * [Elementi raccomandati](#elementi-raccomandati-catalogo)
      * [Home page del catalogo](#foafhomepage-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Lingua del catalogo](#dctlanguage-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Data di rilascio del catalogo](#dctissued-catalogo-JSONLD-RDFXML-RDFTURTLE)
      * [Temi del catalogo](#dcatthemetaxonomy-JSONLD-RDFXML-RDFTURTLE)
  * [Come definire un dataset in DCAT-AP_IT](#dataset)
    * [dcatapit:Dataset](#dcatapitdataset)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#dataset-esempi-JSONLD-RDFXML-RDFTURTLE)
    * [Elementi obbligatori](#elementi-obbligatori-dataset)
      * [Identificativo del dataset](#dctidentifier-dataset-JSONLD-RDFXML-RDFTURTLE)
      * [Titolo del dataset](#dcttitle-dataset-JSONLD-RDFXML-RDFTURTLE)
      * [Descrizione del dataset](#dctdescription-dataset-JSONLD-RDFXML-RDFTURTLE)
      * [Data di ultima modifica del dataset](#dctmodified-dataset-JSONLD-RDFXML-RDFTURTLE)
  * [Come mappare i temi di DCAT-AP_IT](#temi)

   
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
<table align="left">
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

#### Elementi obbligatori che descrivono un Soggetto o Organizzazione in DCAT-AP_IT
1) **_IDENTIFICATIVO del SOGGETTO_**: ``dct:identifier``

<table align="left">
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
<table align="left">
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

<table align="left">
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


#### Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle
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
1) **_TITOLO del CATALOGO_**: ``dct:title``

<table align="left">
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


##### Esempi di uso di ``dct:title`` per il Catalogo in JSON-LD, RDF/XML RDF/Turtle
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
<br />
2) **_DESCRIZIONE del CATALOGO_**: ``dct:description``

<table align="left">
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

<a name="dctdescription-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:description`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
3) **_EDITORE del CATALOGO_**: ``dct:publisher``
<table align="left">
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
    <td align="left">L'editore del Catalogo</td>
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

<a name="dctpublisher-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:publisher`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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

<br />
4) **_DATA di ULTIMA MODIFICA del CATALOGO_**: ``dct:modified``
<table align="left">
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

<a name="dctmodified-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:modified`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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

<br />
5) **_DATASET del CATALOGO_**: ``dcat:dataset``
<table align="left">
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

<a name="dcatdataset-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dcat:dataset`` in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
<a name="elementi-raccomandati-catalogo" />
#### Elementi raccomandati

<br />
1) **_HOME PAGE del CATALOGO_**: ``foaf:homepage``

<table align="left">
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

<a name="foafhomepage-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``foaf:homepage`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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

<br />
2) **_LINGUA del CATALOGO_**: ``dct:language``

<table align="left">
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

<a name="dctlanguage-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:language`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
3) **_DATA di RILASCIO del CATALOGO_**: ``dct:issued``
<table align="left">
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

<a name="dctissued-catalogo-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:issued`` per il Catalogo in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
4) **_TEMI del CATALOGO_**: ``dcat:themeTaxonomy``
<table align="left">
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
    <td align="left">ndicare un sistema di organizzazione della conoscenza (KOS) usato per classificare i dataset del Catalogo. Il valore da utilizzare per questa proprietà è l’URI dei vocabolari utilizzati (<b>non gli URI dei concetti presenti nel vocabolario</b>). Nel caso del vocabolario Data Theme da utilizzare obbligatoriamente per indicare i temi relativi ai Dataset, usare questo URI http://publications.europa.eu/resource/authority/data-theme come valore della proprietà.</td>
  </tr>
</table>

<a name="dcatthemetaxonomy-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dcat:themeTaxonomy`` in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
<a name="dataset" />
### Come definire un dataset in DCAT-AP_IT
Un dataset è definito mediante la classe _Dataset_ identificata univocamente da un URI (Uniform Resource Identifier).

<a name="dcatapitdataset" />
#### Definizione di ``dcatapit:Dataset``

<table align="left">
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
<br />
<a name="dataset-esempi-JSONLD-RDFXML-RDFTURTLE" />
#### Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle
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
<br />
<a name="elementi-obbligatori-dataset" />
#### Elementi obbligatori
1) **_IDENTIFICATIVO del DATASET_**: ``dct:identifier``

<table align="left">
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

<a name="dctidentifier-dataset-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:identifier`` per il Dataset in JSON-LD, RDF/XML e RDF/Turtle
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

2) **_TITOLO del DATASET_**: ``dct:title``

<table align="left">
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

<a name="dcttitle-dataset-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:title`` per il Dataset in JSON-LD, RDF/XML e RDF/Turtle
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
<br />
3) **_DESCRIZIONE del DATASET_**: ``dct:description``

<table align="left">
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

<a name="dctdescription-dataset-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:description`` per il Dataset in JSON-LD, RDF/XML e RDF/Turtle
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

4) **_DATA DI ULTIMA MODIFICA del DATASET_**: ``dct:modified``

<table align="left">
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

<a name="dctmodified-dataset-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:modified`` per il Dataset in JSON-LD, RDF/XML e RDF/Turtle
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

<br />
<a name="temi" />
#### Come mappare i temi di DCAT-AP_IT
Sulla base della [valutazione dei diversi temi per i dati discussa nell'ambito del gruppo Europeo](https://joinup.ec.europa.eu/asset/dcat_application_profile/document/review-dcat-ap-draft-proposal-list-categorization-data), la tabella seguente offre un possibile mapping di domini applicativi rispetto ai temi richiesti dal profilo Europeo DCAT-AP, e quindi dall'estensione italiana DCAT-AP_IT.

<table align="left">
    <tr>
    	<td align="left"><b>Tema</b></td>
	<td align="left"><b>Descrizione</b></td>
    </tr>
    <tr>
        <td align="left">Agricoltura, pesca, silvicoltura e prodotti alimentari</td>
        <td align="left">Rientra tutto ciò che riguarda il settore agricoltura, pesca, politiche forestali e alimentari</td>
    </tr>
    <tr>
        <td align="left">Economia e Finanze</td>
        <td align="left">Rientra tutto ciò che riguarda la tassazione, l'industria, il manifatturiero, il bilancio dello stato, la crescita economica, il commercio</td>
    </tr>
    <tr>
        <td align="left">Istruzione, cultura e sport</td>
        <td align="left">Rientra tutto ciò che riguarda la cultura, il turismo, l'istruzione e le attività sportive</td>
    </tr>
    <tr>
        <td align="left">Energia</td>
        <td align="left">Rientra tutto ciò che concerne il settore dell'energia e dell'estrazione mineraria</td>
    </tr>
    <tr>
        <td align="left">Ambiente</td>
        <td align="left">Rientra tutto ciò che riguarda l'ambiente (rifiuti, consumo del suolo, oceani, ecc.) e il clima/meteo</td>
    </tr>
    <tr>
        <td align="left">Governo e settore pubblico</td>
        <td align="left">Rientra tutto ciò che riguarda le politiche di governo, gli affari istituzionali, la trasparenza del settore pubblico</td>
    </tr>
    <tr>
        <td align="left">Salute</td>
        <td align="left">Rientra tutto ciò che concerne le attività sulla salute e tutto ciò che riguarda gli animali</td>
    </tr>
    <tr>
        <td align="left">Tematiche internazionali</td>
        <td align="left">Rientra tutto ciò che concerne le relazioni internazionali, la cooperazione internazionale, i diritti umanitari, le organizzazioni internazionali e gli affari esteri</td>
    </tr>
    <tr>
        <td align="left">Giustizia, sistema giuridico e sicurezza pubblica</td>
        <td align="left">Rientra tutto ciò che riguarda le frodi, i crimini, la giustizia, le norme. Rientra anche tutto ciò che riguarda la difesa e gli aspetti legati alle attività del ministero dell'interno</td>
    </tr>	
    <tr>
        <td align="left">Regioni e città</td>
        <td align="left">Rientra tutto ciò che riguarda le strade urbane e i numeri civici. Il tema ha una forte sovrapposizione con ambiente perché potrebbe anche contenere tutto ciò che concerne la geografia del territorio (e.g., montagne, laghi, fiumi, ecc.)</td>
    </tr>
    <tr>
        <td align="left">Popolazione e società</td>
        <td align="left">Rientra tutto ciò che concerne lo sviluppo della società, le condizioni della società, la cittadinanza, la demografia, il welfare</td>
    </tr>
    <tr>
        <td align="left">Scienza e tecnologia</td>
        <td align="left">Rientra tutto ciò che riguarda la ricerca, l'innovazione, la tecnologia, la banda larga e ultralarga, la psicologia, lo spazio</td>
    </tr>
    <tr>
        <td align="left">Trasporti</td>
        <td align="left">Rientra tutto ciò che riguarda i trasporti e le relative infrastrutture, la mobilità</td>
    </tr>
</table>

