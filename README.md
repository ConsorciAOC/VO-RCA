# VO-RCA

## 1- Introducció
Aquest document detalla la missatgeria associada al servei de consulta del Registre Central d’Assegurats de CatSalut (en endavant RCA). Per poder realitzar la integració cal conèixer prèviament la següent documentació:
* Document d’Especificació de missatgeria pel consum de productes de la plataforma PCI del Consorci AOC. 

## 2- Transmissions de dades disponibles
Les dades disponibles a través del servei són les que es presenten a continuació: 
* Emissor: Servei Català de la Salut

| Producte | Modalitat | Descripció |
|---|---|---|
| RCA | RCA_CONSULTA | Consulta d’assegurats per CIP, dades identificatives o per document identificador al RCA. |
| RCA | RCA_VERIFICACIO | Validació d'assegurats per CIP al RCA |

Totes les consultes del producte tenen disponible la versió imprimible del resultat de la consulta en format PDF. Per més detalls adreceu-vos a l’apartat Extensions de missatgeria del document de missatgeria genèrica.

## 3- Missatgeria dels serveis
Aquest servei permet consultar i verificar la identitat de menors. Per aquesta identificació, el servei consulta el RCA que emmagatzema les dades personals per a la gestió de les targetes sanitàries individuals (TSI).

![Tarjeta TSI](https://github.com/ConsorciAOC/VO-RCA/blob/main/images/3%20Missatgeria%20dels%20serveis.png)

La TSI és el document que permet als ciutadans l’accés als centres, als serveis i a les prestacions del sistema sanitari públic. A més a més, la TSI facilita la identificació de forma ràpida i correcta a través del Codi d’Identificació Personal (CIP) que està imprès a la primera línia. El CIP és el conjunt de regles (expressades amb nombres i lletres) que de forma individual i unívoca permet identificar a cada persona assegurada del CatSalut.
El CIP sanitari està compost de 14 dígits:
<table align = "center">
  <tbody>
    <tr>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
      <td>S</td>
      <td>Y</td>
      <td>Y</td>
      <td>M</td>
      <td>M</td>
      <td>D</td>
      <td>D</td>
      <td>R</td>
      <td>R</td>
      <td>T</td>
    </tr>
  </tbody>
</table>

* AA: dos primeres lletres del primer cognom
* BB: dos primeres lletres del segon cognom
* S: sexe (dígit)
* YY: any de naixement
* MM: mes de naixement
* DD: dia de naixement
* RR: dos dígits de control
* T: un dígit de control

Cal tenir en compte que:

* Un ciutadà pot tenir més d'un CIP.
* Únicament un CIP pot estar actiu per ciutadà.
* Tots els CIP associats a un individu estant enregistrats al RCA encara que no estiguin actius.

### 3.1 Consulta d’assegurats (RCA_CONSULTA)
Aquesta modalitat permet consultar les dades d’un assegurat a partir del CIP, de les dades personals o del document identificador.

#### 3.1.1 Petició – dades específiques 

| Element | Descripció |
|---|---|
| /peticioConsultaAssegurat/codiIdentificacioPersonal | Bloc de dades per informar les dades d’identificació personal del titular.  |
| //codiIdentificacioPersonal/CIP | CIP |
| /peticioConsultaAssegurat/dadesPersonals | Bloc de dades per informar les dades personals del titular. |
| //dadesPersonals/nom | Nom. |
| //dadesPersonals/primerCognom | Primer cognom. |
| //dadesPersonals/segonCognom | Obligatori si el titular té segon cognom. En cas de no tenir-ne (p.e.estranger) no s’ha d’informar. |
| //dadesPersonals/dataNaixement | Format DDMMYYYY. |
| /dadesPersonals/sexe | Sexe (0: home 1: dona). |
| /peticioConsultaAssegurat/documentIdentificador | Bloc de dades per informar el document identificador del titular. |
| //documentIdentificador/tipusDocumentacio | Tipus de documentació: DNI / NIF, Passaport, Targeta de residència comunitària, Permís de residència i treball, Documents varis i NIE |
| //documentIdentificador/documentacio  | Documentació. |

![dades específiques](https://github.com/ConsorciAOC/VO-RCA/blob/main/images/3.1.1%20Petici%C3%B3%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

#### 3.1.2 Resposta – dades específiques
De l’schema associat a la resposta especifica, el servei informa les dades que es detallen a continuació.

![Resposta dades específiques](https://github.com/ConsorciAOC/VO-RCA/blob/main/images/3.1.2%20Resposta%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

| Element | Descripció |
|---|---|
| /respostaConsultaAssegurat/peticioConsultaAssegurat | Bloc de dades de la consulta (vegeu apartat anterior). |
| /respostaConsultaAssegurat/resposta | Bloc de dades corresponent a la resposta. |
| //resposta/CIPVigent | CIP actiu de l’assegurat. |
| //resposta/situacioAssegurat | Situació de l’assegurat: alta, defunció, trasllat i fusió |
| //resposta/adreca/nomLocalitat | Nom de localitat. |
| //resposta/adreca/codiLocalitat | Codi de localitat (INE). |
| //resposta/adreca/districtePostal | Districte postal. |
| //resposta/adreca/nomVia | Nom de la via. |
| //resposta/adreca/numeroViaInicial | Número de via. |
| //resposta/adreca/numeroViaFinal | Número de via. |
| //resposta/adreca/tipusVia | Codi de tipus de via (vegeu apartat 3.1.2.2). |
| //resposta/adreca/indicadorBis | Indicador BIS. |
| //resposta/adreca/pis | Pis. |
| //resposta/adreca/porta | Porta. |
| //resposta/adreca/escala | Escala. |
| //resposta/adreca/quilometre  | Quilometre. |
| //resposta/dadesPersonals/nom | Nom. |
| //resposta/dadesPersonals/primerCognom | Primer cognom. |
| //resposta/dadesPersonals/segonCognom | Segon cognom. |
| //resposta/dadesPersonals/sexe | Sexe (0: home 1: dona). |
| //resposta/documentIdentificador/tipusDocumentacio | Tipus de documentació: DNI / NIF, Passaport, Targeta de residència comunitària, Permís de residència i treball, Documents varis i NIE |
| //resposta/documentIdentificador/documentacio | Documentació. |
| //resposta/dadesCobertura/codiNivellCobertura | **1:** COB. SANITÀRIA GENERAL FARM. GRAT., **3:** COBERTURA SANITÀRIA GENERAL, **4:** COB. SANIT. GRAL. EXCEPTE FARMÀCIA, **7:** E. COL. COB. COMUNA FARM. GRAT., **8:** E. COL. COB. COMUNA, **9:** PROGRAMES INTERÈS SANITARI DS, **11:** COB.SANITÀRIA PAMEM FARMÀCIA GRATUITA i **12:** COB.SANITÀRIA PAMEM FARMÀCIA PARCIAL |
| //resposta/dadesCobertura/descripcioNivellCobertura | Descripció nivell de cobertura. |
| //resultat/codiResultat | Codi de resultat de l’operació de consulta (vegeu apartat 3.1.2.1). |
| //resultat/descripcio | Descripció. |

##### 3.1.2.1 Codis de resultat
* 0: El ciutadà consta al Registre Central d'assegurats.
* 1: El ciutadà NO consta al Registre Central d'assegurats.
* 2: Múltiples respostes trobades amb els criteris de cerca introduïts. Milloreu la cerca.
* 0502: Error realitzant la consulta.

##### 3.1.2.2 Tipus de via
Codi|Descripció
:-----:|:-----:
AV|AVINGUDA
BL|BLOCS
BR|BARRI
BX|BAIXADA
CM|CAMI
CN|CANN
CO|CARRERÓ
CR|CARRERÓ
CS|COSTA
CT|CARRETERA
DA|DAVALLADA
DI|DISSEMINAT
DR|DRECERA
ES|ESCALES
GL|GLORIETA
GR|GRUPS
GV|GRAN VIA
JA|JARDI
LL|LLOC
MO|MOLL
MS|MASS
PA|PAS
PC|PLACETA
PD|PARTIDA
PG|PASSATGE
PI|PASSADIS
PJ|PUJADA
PL|PLAÇA
PO|POLIGON
PR|PARC
PS|PASSEIG
PT|PONT
PY|PLATJA
RB|RAMBLA

### 3.2 Verificació d’assegurats (RCA_VERIFICACIO)
Aquesta modalitat permet verifcar les dades d’un assegurat.

#### 3.2.1 Petició – dades específiques
Element|Descripció
-----|-----
/peticioVerificacioAssegurat/CIP| CIP.
/peticioVerificacioAssegurat/primerCognom| Primer cognom. 

![Resposta dades específiques](https://github.com/ConsorciAOC/VO-RCA/blob/main/images/3.2.1%20Petici%C3%B3%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

#### 3.2.2 Resposta – dades específiques
De l’schema associat a la resposta especifica, el servei informa les dades que es detallen a continuació.

Element|Descripció
-----|-----
/respostaVerificacioAssegurat/ peticioVerificacioAssegurat|Bloc de dades de la consulta (vegeu apartat anterior).
/respostaVerificacioAssegurat/resposta|Bloc de dades corresponent a la resposta.
//resposta/CIPVigent|CIP actiu de l’assegurat.
//resposta/situacioAssegurat |Situació de l’assegurat: A: alta, D: defunció, T: trasllat, F: fusió
//resultat/codiResultat|Codi de resultat de l’operació de consulta: 0: El ciutadà consta al Registre Central d'assegurats, 1: El ciutadà NO consta al Registre Central d'assegurats, 0502: Error realitzant la consulta.
//resultat/descripcio|Descripció del resultat.

![Resposta dades específiques](https://github.com/ConsorciAOC/VO-RCA/blob/main/images/3.2.2%20Resposta%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

## 4 Joc de proves
Podeu demanar el joc de proves del servei proporcionat per l’emissor final, vàlid per a l’entorn de preproducció, a l’adreça **suport.integracio@aoc.cat**. 
