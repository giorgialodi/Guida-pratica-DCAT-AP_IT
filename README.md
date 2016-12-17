# Guida pratica a DCAT-AP_IT
## Profilo italiano di metadazione per la descrizione di dati presenti in cataloghi (DCAT-AP_IT)

Questo progetto rappresenta la guida pratica offerta dal portale ``dati.gov.it`` per l'adeguamento da parte delle Pubbliche Amministrazioni al profilo nazionale di metadatazione DCAT-AP_IT così come raccomandato nell'ambito delle linee guida per la valorizzazione del patrimonio informativo pubblico (anno 2016).
Per dettagli sulla semantica degli elementi si invita a consultare la [relativa specifica DCAT-AP_IT 1.0](http://www.dati.gov.it/sites/default/files/DCAT-AP_IT_v10.pdf) disponibile anche come [ontologia OWL.](http://dati.gov.it/onto/dcatapit)

**Licenza:**
CC-BY 4.0 (Creative Commons Attribution).

##Indice
* [Come definire un soggetto/organizzazione in DCAT-AP_IT](#soggetto)
  * [dcatapit:Agent](#agent)
  * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#soggetto-esempi-JSONLD-RDFXML-RDFTURTLE)
* [Come definire un catalogo in DCAT-AP_IT](#catalogo)
  * [dcatapit:Catalog](#catalog)
  * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#catalogo-esempi-JSONLD-RDFXML-RDFTURTLE)
  * [Elementi che descrivono un catalogo](#elementi-catalogo)
    * [dct:title](#dcttitle-JSONLD-RDFXML-RDFTURTLE)
    * [dct:description](#dctdescription-JSONLD-RDFXML-RDFTURTLE)
    * [dct:publisher](#dctpublisher-JSONLD-RDFXML-RDFTURTLE)
  
  

<a name="soggetto" />
###Come definire un soggetto/organizzazione in DCAT-AP_IT
Un soggetto/organizzazione è definito mediante la specifica della classe _Agente_ identificata univocamente da un URI (Uniform Resource Identifier).
<a name="agent" /> 
####Definizione di ``dcatapit:Agent``
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

<a name="soggetto-esempi-JSONLD-RDFXML-RDFTURTLE" />
####Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle
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

<a name="catalogo" />
###Come definire un catalogo di dati in DCAT-AP_IT
Un catalogo è definito mediante la classe _Catalogo_ identificata univocamente da un URI (Uniform Resource Identifier).
<a name="catalog" />
#### Definitione di ``dcatapit:Catalog``

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

<a name="catalogo-esempi-JSONLD-RDFXML-RDFTURTLE" />
####Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle
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
<a name="elementi-catalogo" />
####Elementi che contribuiscono a descrivere un Catalogo in DCAT-AP_IT
Un catalogo è descritto da alcuni elementi **obbligatori**:

<br />
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
    <td align="left">hhttp://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di inserire un testo semplice e corto. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il catalogo sia parte di un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso.</b> <br />Esempio: "Catalogo dei dati aperti dell'AgID (Agenzia per l'Italia Digitale)" oppure "Catalogo delle banche dati  della Regione Lazio".</td>
  </tr>
</table>

<a name="dcttitle-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:title`` in JSON-LD, RDF/XML e RDF/Turtle
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
    <td align="left"><b>Si raccomanda di inserire una breve illustrazione delle  caratteristiche principali del catalogo. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il catalogo. Si ricorda che: nessun tag HTML è consentito.</b> <br />Esempio: "Il catalogo contiene i dati aperti dell'Agenzia per l'Italia Digitale, in particolare, i dati aperti dell'Indice della Pubblica Amministrazione (IPA)" e dei contratti del Sistema Pubblico di Connettività (SPC) relativi alle gare del 2007.</td>
  </tr>
</table>

<a name="dctdescription-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:description`` in JSON-LD, RDF/XML e RDF/Turtle
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

<a name="dctpublisher-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:description`` in JSON-LD, RDF/XML e RDF/Turtle
>``JSON-LD``

```JSON

