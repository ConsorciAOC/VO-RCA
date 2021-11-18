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

**(INTRODUCIR IMAGEN)**

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
