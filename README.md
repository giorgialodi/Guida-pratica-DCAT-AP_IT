# Guida pratica a DCAT-AP_IT e all'alimentazione del catalogo nazionale ``dati.gov.it``

Questo progetto rappresenta la guida pratica offerta da ``dati.gov.it`` per l'accreditamento, l'alimentazione dello stesso secondo le due diverse modalità previste, e per l'adeguamento delle Pubbliche Amministrazioni al profilo nazionale di metadatazione DCAT-AP_IT, così come raccomandato nelle [linee guida per la valorizzazione del patrimonio informativo pubblico (anno 2016)](http://www.dati.gov.it/sites/default/files/LG2016_0.pdf).
Per dettagli sulla semantica degli elementi si invita a consultare anche l'[ontologia OWL](http://dati.gov.it/onto/dcatapit) del profilo DCAT-AP_IT.
La presente guida pratica fornisce una descrizione degli elementi principali del profilo con le relative proprietà. Per ciascun elemento e proprietà, al fine di facilitare le amministrazioni nella predisposizione dei metadati per abilitare la modalità di alimentazione del catalogo detta harvesting, sono forniti esempi di uso nelle seguenti serializzazioni RDF: JSON-LD, RDF/XML, RDF/Turtle. 

**Licenza:**
CC-BY 4.0 (Creative Commons Attribution).

##Indice
* [Alimentare il catalogo nazionale ``dati.gov.it``](#modalita-inserimento-metadati-catalogo)
  * [Procedura di accreditamento](#accreditamento)
  * [Modalità di alimentazione](#modalita-alimentazione)
* [Guida pratica a DCAT-AP_IT](#dcatapit)
  * [Come definire un soggetto/organizzazione in DCAT-AP_IT](#soggetto)
    * [dcatapit:Agent](#agent)
    * [Elementi obbligatori che descrivono un Soggetto/Organizzazione in DCAT-AP_IT](#elementi-obbligatori-soggetto)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#soggetto-esempi-JSONLD-RDFXML-RDFTURTLE)
  * [Come definire un catalogo in DCAT-AP_IT](#catalogo)
    * [dcatapit:Catalog](#catalog)
    * [Esempi di uso in JSON-LD, RDF/XML, RDF/Turtle](#catalogo-esempi-JSONLD-RDFXML-RDFTURTLE)
    * [Elementi obbligatori che descrivono un Catalogo in DCAT-AP_IT](#elementi-obbligatori-catalogo)
      * [Titolo del catalogo](#dcttitle-JSONLD-RDFXML-RDFTURTLE)
      * [Descrizione del catalogo](#dctdescription-JSONLD-RDFXML-RDFTURTLE)
      * [Editore del catalogo](#dctpublisher-JSONLD-RDFXML-RDFTURTLE)
      * [Data di ultima modifica del catalogo](#dctmodified-JSONLD-RDFXML-RDFTURTLE)
      * [Dataset del catalogo](#dcatdataset-JSONLD-RDFXML-RDFTURTLE)
    * [Elementi raccomandati che descrivono un Catalogo in DCAT-AP_IT](#elementi-raccomandati-catalogo)
      * [Home page del catalogo](#foafhomepage-JSONLD-RDFXML-RDFTURTLE)
      * [Lingua del catalogo](#dctlanguage-JSONLD-RDFXML-RDFTURTLE)
      * [Data di rilascio del catalogo](#dctissued-JSONLD-RDFXML-RDFTURTLE)
  
<a name="modalita-inserimento-metadati-catalogo" />
##Alimentare il catalogo nazionale ``dati.gov.it``
Per poter alimentare il catalogo nazionale è necessario accreditarsi presso il catalogo stesso. 
<a name="accreditamento" />
####Procedura di accreditamento
La procedura di accreditamento al momento disponibile prevede l'esecuzione dei seguenti passi:

1. l'utente dell'amministrazione accede alla [piattaforma di test](http://93.63.32.55);
2. l'utente dell'amministrazione avvia la registrazione selezionando la voce *Registrati* nel menu in alto a destra;
3. nella pagina Web seguente, l'utente inserisce nel box in fondo alla pagina il codice IPA, i.e., codice della propria amministrazione come assegnato dall'Indice della Pubblica Amministrazione (IPA). Il codice IPA è reperibile attraverso [il catalogo IPA;](http://www.indicepa.gov.it). L'utente preme "avanti";
4. il sistema presenta all'utente uno o più nomi di cosiddetti referenti IPA, ovvero di responsabili, all'interno dell'amministrazione, del corretto e tempestivo aggiornamento dei dati dell'IPA. L'utente seleziona un referente IPA dalla lista e preme "avanti";
5. l'utente è invitato a completare la registrazione inserendo l'*email* istituzionale, lo *username* da utilizzare per i successivi accessi e il *Nome e Cognome*. L'utente preme "invia";
6. il sistema provvede a inoltrare una richiesta di accreditamento. Al momento la richiesta è inviata agli amministratori del sistema ``dati.gov.it`` e non al referente selezionato. L'invio al referente IPA sarà abilitato solo in una fase successiva;
8. l'utente riceverà una email all’indirizzo indicato al suddetto passo 5. con il seguente testo “*Ti ringraziamo per la registrazione su dati.gov.it - i dati aperti della pubblica amministrazione. La tua richiesta di account è in attesa di approvazione. Una volta approvata, riceverai un'altra e-mail con le informazioni necessarie per effettuare il primo accesso, impostare la password ed altri dettagli.*”;
9. a seguito dell’approvazione da parte degli amministrazioni di ``dati.gov.it``, l'utente riceverà una seconda email con un link; cliccando sul link dell'email, l'utente è indirizzato all'applicazione che gli consente di inserire la password da utilizzare per i successivi accessi.

L'Agenzia per l'Italia Digitale sta valutando anche l'implementazione di una seconda modalità di accreditamento a ``dati.gov.it``che non contempla l'uso dei dati dell'IPA. In particolare, analogamente ad altri sistemi dell'Agenzia, si sta valutando l'accreditamento mediante 
un *modulo firmato* digitalmente da inviare via Posta Elettronica Certificata (PEC) ad AgID. 

Una volta ottenute le credenziali per l'accesso, l'utente può iniziare a documentare i propri dataset scegliendo attraverso [due modalità previste](#modalita-alimentazione).

<a name="modalita-alimentazione" />
####Modalità di alimentazione del catalogo 
Esistono due modalità di alimentazione:

1. *editor*: applicazione Web integrata nel catalogo per l'acquisizione e l'aggiornamento guidato dei metadati. L'editor alimenta automaticamente il catalogo in modo da garantire la conformità al profilo DCAT-AP_IT. Tale modalità è consigliata in presenza di pochi dataset che hanno anche una frequenza di aggiornamento ampia. Per usufruirne, l'utente accede all'area privata di ``dati.gov.it`` selezionando *Login* dal menu in alto a destra. Una volta effettuato il login, l'utente può accedere al web editor selezionando la voce di menu *Aggiungi dataset*. Per poter visualizzare l’elenco dei dataset descritti si può selezionare la voce *I miei dataset* in alto a destra. Ogni dataset può essere eventualmente modificato (attraverso l'operazione *Modifica*) o eliminato (attraverso l'operazione *Elimina*);
2. *harvesting*: funzionalità offerta dal catalogo per l'acquisizione e l'aggiornamento periodico dei metadati. L'uso di tale funzionalità richiede che l'amministrazione comunichi, una volta effettuato il login e solo la prima volta, l'URL dove poter acquisire tutti i dataset. Sarà lo stesso catalogo nazionale che si occuperà successivamente di raccogliere periodicamente i metadati che descrivono i dati. Tale modalità è consigliata in presenza di un numero elevato di dataset, soggetti anche a frequenti aggiornamenti. 

<a name="dcatapit" />
##Guida a DCAT-AP_IT
Nelle seguenti sezioni, per ciascun elemento (classe e proprietà) del profilo di metadatazione DCAT-AP_IT saranno fornite istruzioni per l'uso ed esempi pratici di definizione dei metadati in JSON-LD, RDF/XML e RDF/Turtle.
<a name="soggetto" />
###Come definire un Soggetto/Organizzazione in DCAT-AP_IT
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

<a name="elementi-obbligatori-soggetto" />
####Elementi obbligatori che descrivono un Soggetto/Organizzazione in DCAT-AP_IT

<br />
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

<br />
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
<a name="elementi-obbligatori-catalogo" />
####Elementi obbligatori che descrivono un Catalogo in DCAT-AP_IT

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
    <td align="left">http://purl.org/dc/terms/title</td>
  </tr>
  <tr>
    <td align="left">Uso</td>
    <td align="left"><b>Si raccomanda di inserire un testo semplice e corto. Si raccomanda di non utilizzare acronimi o abbreviazioni incomprensibili. Se si vogliono utilizzare comunque gli acronimi, riportare anche il nome esteso. Nel caso il catalogo sia parte di un progetto più ampio, si consiglia di indicare, tra parentesi, il nome del progetto alla fine del titolo stesso.</b> <br />Esempio: "Catalogo dei dati aperti dell'AgID (Agenzia per l'Italia Digitale)" oppure "Catalogo delle banche dati della Regione Lazio".</td>
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
    <td align="left"><b>Si raccomanda di fornire una breve descrizione delle caratteristiche principali del catalogo. Evitare di utilizzare un linguaggio ricco di riferimenti normativi. Utilizzare invece un linguaggio semplice che possa aiutare qualsiasi utente a identificare il catalogo. Si ricorda che nessun tag HTML è consentito.</b> <br />Esempio: "Il catalogo contiene i dati aperti dell'Agenzia per l'Italia Digitale, in particolare, i dati aperti dell'Indice della Pubblica Amministrazione (IPA) e dei contratti del Sistema Pubblico di Connettività (SPC) relativi alle gare del 2007".</td>
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
##### Esempi di uso di ``dct:publisher`` in JSON-LD, RDF/XML e RDF/Turtle
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

<a name="dctmodified-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:modified`` in JSON-LD, RDF/XML e RDF/Turtle
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
####Elementi raccomandati che descrivono un Catalogo in DCAT-AP_IT

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

<a name="foafhomepage-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``foaf:homepage`` in JSON-LD, RDF/XML e RDF/Turtle
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

<a name="dctlanguage-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:language`` in JSON-LD, RDF/XML e RDF/Turtle
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

<a name="dctissued-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:issued`` in JSON-LD, RDF/XML e RDF/Turtle
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
    <td align="left">ndicare un sistema di organizzazione della conoscenza (KOS) usato per classificare i dataset del Catalogo. Il valore da utilizzare per questa proprietà è l’URI dei vocabolari utilizzati (non gli URI dei concetti presenti nel vocabolario). Nel caso del vocabolario Data Theme da utilizzare obbligatoriamente per indicare i temi relativi ai Dataset, usare questo URI http://publications.europa.eu/resource/authority/data-theme come valore della proprietà.</td>
  </tr>
</table>

<a name="dctissued-JSONLD-RDFXML-RDFTURTLE" />
##### Esempi di uso di ``dct:issued`` in JSON-LD, RDF/XML e RDF/Turtle
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




