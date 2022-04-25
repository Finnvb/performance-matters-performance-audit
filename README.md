
# Walibi Performance Audit
Dit is een performance Audit voor de website van Walibi met behulp van Lighthouse. Met Lighthouse wordt er een score voor de performance gegenereerd en wordt er aangegeven wat je zou kunnen doen om die score te verbeteren. 




## ContentAudit
Ik heb de website van Walibi geanalyseerd. Walibi is een attractiepark gelegen in Flevoland. Op de website kun je onder andere tickets bestellen. 

- Testdatum: 25-4-2022
- website link: https://www.walibi.nl/nl

![afbeelding](https://user-images.githubusercontent.com/26089533/165131280-a382c5eb-1f2d-4faf-96fd-152056cef922.png)

![afbeelding](https://user-images.githubusercontent.com/26089533/165129977-0cef0be2-53b3-4853-9cef-c4aea0fe09b6.png)

### First Contentful Paint (FCP)
_Beschrijf de uitslag van de FCP van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._

De FCP geeft aan hoe lang het de browser duurt in seconden om het eerste stukje DOM content te renderen. 
* 0 - 1.8 sec (groen) snel
* 1.8 - 3 sec (oranje) middelmatig
* meer dan 3 sec (rood) traag

![afbeelding](https://user-images.githubusercontent.com/26089533/165137776-5688122b-0d31-4b47-8851-4ccc92004690.png)

Met een tijd van 0.6 sec. wordt het eerste stuk content snel geladen en gerendeerd. Dit kan nog sneller door het volgende toe te passen:
- **Eliminate render-blocking resources**

Er zijn bestanden die de "First paint" van de website blokkeren. Dit zijn twee CSS bestanden en een JS bestand. Een oplossing hiervoor is het gebruik van modules voor critical CSS en JS of om bepaalde assets asynchroon in te laden met Javascript.
- **Enable text compression**

Text-based bestanden kunnen worden gecomprimeerd om het totale aantal netwerkbytes van die bestanden te minimaliseren. Om dit te realiseren kun je gzip, deflate of brotli gebruiken.

<img width="450" src="https://user-images.githubusercontent.com/26089533/165138739-d7f91594-eb51-4a73-a887-9106584dac51.png" />

<img width="450" src="https://user-images.githubusercontent.com/26089533/165138803-7a448703-6171-4dc3-be3a-5233999544fc.png" />



### Time to Interactive (TTI)
_Beschrijf de uitslag van de TTI van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._
De TTI geeft aan hoe lang het duurt voordat de webpagina volledig interactief is voor de gebruiker.

Het duurt 3.2 seconden voordat de webpagina volledig interactief is voor de gebruiker. Dit geeft een oranje kleurcode aan en kan dus beter. Een manier om dit te verbeteren is om de execution time van Javascript te verminderen. Dit kan door onnodige Javascript code te verwijderen of om het op te splitsen. Nog een manier is om de workload op de main thread te minimaliseren.

![afbeelding](https://user-images.githubusercontent.com/26089533/165152352-e1fd945c-b721-4d02-a310-008e82735405.png)


### Speed Index
_Beschrijf de uitslag van de SI van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._

De Speed Index meet hoe snel de inhoud van de webpagina visueel wordt weergegeven tijdens het laden van de webpagina.
* 0–3.4 sec	(groen) snel
* 3.4 – 5.8 sec	(oranje) middelmatig
* meer dan 5.8 sec (rood) traag
Met een tijd van 1.3 sec wordt de inhoud van de webpagina snel visueel ingeladen. Goede oplossingen voor het verbeteren van de Speed Index zijn: de workload op de main thread verminderen, Javascript execution time te verminderen en om ervoor te zorgen dat tekst zichtbaar blijft tijdens het laden van webfonts.
Dat laatste kun je doen door gebruik te maken van de `font-display` property in CSS. Of door je fonts vooraf in te laden `<link rel="preload" as="font">`.

![afbeelding](https://user-images.githubusercontent.com/26089533/165154349-f8d0ad49-1268-456f-9cef-fcd0699ee8b3.png)


### Total Blocking Time (TBT)
_Beschrijf de uitslag van de TBT van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._

De TBT meet de totale tijd (in ms) dat een pagina niet reageert op gebruikersinvoer, zoals muisklikken, schermtikken of toetsenborddrukken. De totale tijd wordt berekend door het blokkerende deel van alle "Long Tasks" tussen FCP en TTI bij elkaar op te tellen. Als een taak langer dan 50 ms duurt is het een Long Task. De tijd daarna is het blokkerende deel. 
* 0 – 200 ms	(groen) snel
* 200 - 600 ms	(oranje) middelmatig
* meer dan 600 ms	(rood) traag
Met een tijd van 20 ms heeft de webpagina weinig TBT en reageert dus snel op gebruikersinvoer.

![afbeelding](https://user-images.githubusercontent.com/26089533/165157364-0423e559-2890-4a97-8a61-eae4288920d5.png)


### Largest Contentful Paint (LCP)
_Beschrijf de uitslag van de LCP van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._

De LCP meet hoelang het duurt voordat de grootste content element dat zichtbaar is in de viewport is gerendeerd op het scherm.

Met een tijd van 2.9 sec heeft de LCP een rode kleurcode. Dit is niet heel snel, hier kan dus nog wat tijd mee worden gewonnen. Een oplossing hiervoor is om onnodige Javascript bestanden te verwijderen. De walibi website gebruikt veel bestanden van derden die wellicht niet nodig zijn. En om het laden van die Javascript bestanden uit te stellen met `defer` totdat ze nodig zijn.

![afbeelding](https://user-images.githubusercontent.com/26089533/165159710-4e2cfd40-b778-4dd1-8482-d38baf16031e.png)


### Cumulative Layout Shift (CLS)
_Beschrijf de uitslag van de CLS van de test en toon de resultaten. Beschrijf wat kan worden verbeterd als de score minder dan 90 is._

De CLS meet de de beweging van zichtbare elementen binnen de viewport. Hoe hoger de CLS hoe vaker de gebruiker onverwachte lay-outverschuivingen van de webpagina ervaart. Dit kan heel irritant voor gebruikers zijn en er misschien voor zorgen dat je op een verkeerde link klikt. 
Met een score van 0.149 heeft de CLS een oranje kleurcode wat betekent dat er ruimte is voor verbetering. Voor een groene kleurcode moet je streven naar een score van 0.1 of lager.
Dit kun je bereiken door alle img elements een expliciete hoogte en breedte te geven. En om non-composited animations te vermijden.

![afbeelding](https://user-images.githubusercontent.com/26089533/165164844-c3848a68-4f92-47ea-af5c-34b8fbfd5094.png)


## Bronnen
- [Walibi](https://www.walibi.nl/nl)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)

## Licentie

![GNU GPL V3](https://www.gnu.org/graphics/gplv3-127x51.png)

This work is licensed under [GNU GPLv3](./LICENSE).
