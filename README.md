```
DTM SoSe 26 Thorben Flick
```
# EP01 (Dasymetrische) Chloroplethenkarten

<img width="10523" height="7440" alt="DTM_EP01_Thorben Flick" src="https://github.com/user-attachments/assets/2385e742-db06-4a96-841d-596e1d2b79f1" />

## Umsetzung der Methode 
Auf drei verschiedene Arten sollte die Bevölkerungsverteilung Berlins dargestellt werden. Dabei wurden... 

**...(1) absolute Bevölkerungszahlen auf die lebensweltlich orientierten Räume (LOR) aggreggiert**

Die absoluten Bevölkerungszahlen stammen vom *Amt für Statistik Berlin-Brandenburg*. Sie wurden auf die LOR-Shapefile der *Senatsverwaltung Berlin* gerechnet.
Große LOR-Planungsräume mit hoher Bevölkerungsanzahl (aufgrund ihrer größeren Fläche) treten visuell stärker hervor und suggerieren eine höhe Bevölkerungsdichte. Kleine, dicht besiedelte LOR-Planungsräume rücken in den Hintergrund. Es liegt eine Verzerrung durch die Größe der Verwaltungseinheit vor.

**...(2) relative Bevölkerungsdichten in $Einwohnern/km^2$ auf die LOR aggregiert**

Diese Darstellung gibt ein besseres Bild über die tatsächliche Bevölkerungsdichte in den Verwaltungseinheiten. Die Flächenverzerrung ist verschwunden, insbesondere im Südwesten, Norden und Südosten der Stadt.

> Chloroplethenkarten:
>
>Gebiete werden im Verhältnis zur Verteilungsdichte des thematischen Objektes eingefärbt, gepunktet, schattiert oder schraffiert.
In den Karten (1) und (2) sind Planungsräume (LOR) im Verhältnis zur absoluten und relativen Bevölkerungsverteilung
(thematisches Objekt) eingefärbt.

**...(3) relative Bevölkerungsdichten in $Einwohnern/km^2$ auf die tatsächlichen Wohngebiete aggregiert**

Die Shapefile der tatsächlichen Wohngebiete stammt aus dem *Informationssystem Stadt und Umwelt 5 (ISU5)* der Senatsverwaltung Berlin und lassen sich über *WebMapService (WMS)* direkt in QGIS aufrufen. Im Datensatz vorhanden sind bereits Bevölkerungszahlen zu jedem Block. Nach Auflösen der ursprünglichen Shapefile auf Wohngebiete- und Mischnutzungsblocks konnten die Gebiete entsprechend eingefärbt werden. 
<img width="2237" height="358" alt="image" src="https://github.com/user-attachments/assets/de9d51df-134c-4dd8-985b-7a65f7e5e62a" />


> Dasymetrische Chloroplethenkarten:
> 
>Im dasymetrischen Prozess werden die administrativen Einheiten in kleinere, mehr Karten relevante Einheiten (tatsächliche Wohngebiete), aufgespalten. Das Ziel ist die Modellierung einer genaueren räumlichen Verteilung von Populationen als es bei der Choroplethenkarte möglich ist und deren Darstellung in Karten. (verändert aus: https://de-academic.com/dic.nsf/dewiki/304884)


## Modifiable-Areal-Unit-Problem (MAUP)
Die dreifache Darstellung verdeutlicht das MAUP-Problem: 
Punktbasierte Erhebungen werden auf Räume/Verwaltungseinheiten/Zonen aggregiert. Entstehende Statistikwerte werden durch die Form und Größe der Aggregationsräume beeinflusst. Die Wahl der Aggregationsräume sollte immer berücksichtigt werden. 
<p align="center">
   <img width="40%" height="auto" alt="image" src="https://github.com/user-attachments/assets/74d28850-b015-4cbe-8546-1fb3fb5ae2e0" />
</p>

(aus: https://en.wikipedia.org/wiki/Modifiable_areal_unit_problem)

# EP02 Gitterchloroplethenkarten

<img width="3368" height="2380" alt="Kirschblüten-1" src="https://github.com/user-attachments/assets/bbe1d4f0-1b73-4d82-93cb-ff7d57a8189a" />

## Umsetzung der Methode
Der Baumbestand Berlins wurde über einen *WebFeatureService (WFS)* der Senatsverwaltung Berlin abgerufen und die Kirschbäume aus dem Datensatz extrahiert. Über das Shapefile von Berlin ist ein Hexagongitter mit 500 m x 500 m Hexagonen zugeschnitten worden.

<img width="1599" height="1069" alt="image" src="https://github.com/user-attachments/assets/344293d3-1532-49fd-9d70-e8681a106926" />

Auf jedes Hexagon wurde die Anzahl an Punkten (Kirschbäume) aggregiert und nach absoluter Anzahl eingefärbt. 
> Gitterchloroplethenkarten
>
> Im Gegensatz zu den Chloroplethenkarten ist der Raum nicht in administrative Grenzen sondern in ein Raster gleich großer Raster- bzw. Gitterzellen (hier: Hexagone) geteilt. Jede Rasterzelle erhält eine bestimmte Farbe / Farbintensität, welche sich nach dem Wert des thematischen Objektes (Anzahl der Kirschbäume im Hexagon) richtet. Die Bezugsfläche ist eine regelmäßige geometrische Fläche.
## Vor- und Nachteile der Methode
Gitterchloroplethenkarten verringern das MAUP-Problem der Chloroplethenkarten. Außerdem ist ein Zeitreihenvergleich (z.B. Bestandsaufnahmen alle 10 Jahre) einfacher möglich, da sich das geometrische Gitter im Gegensatz zu Verwaltungseinheiten nicht ändern kann. Probleme treten auf, wenn Cluster durch "unglückliche" Platzierung des Gitters zerschnitten werden. Außerdem beeinflusst die Wahl der Gitterzellengröße massiv das Ergebnis. Hier bietet es sich an, verschiedene Größen zu vergleichen. 
# EP03 Punktrasterkarten

<img width="3507" height="2480" alt="punktrasterlayout" src="https://github.com/user-attachments/assets/f9a2fb7f-f0f2-47bc-b56e-304017cf5508" />

Als Variante sollte das Ergebnis ebenfalls als Punktrasterkarte dargestellt werden. Das Hexagongitter verliert seine Form, während die Aggregationsart (500x500 m Hexagone) die selbe bleibt. Alleinig die Symbolisierung auf Karte wird verändert. Dies kann die Lesbarkeit erhöhen. 
# EP04 value-by-alpha-mapping

<img width="4960" height="3507" alt="UngarnWahlen3fach" src="https://github.com/user-attachments/assets/b64942b1-2936-491f-a4c7-93b86a50a4a0" />
Die Wahlkreise als .json-Dateien und die Stimmenverteilungen als .csv-Dateien der Parlamentswahlen in Ungarn 2026 stammen vom der Website des National Election Office Ungarns. Auf einem A3-Layout sollten drei verschiedene Karten dargestellt werden:

(1) Wahlkreis-Sieger nach Farbton und Stimmenvorsprung (%) gegenüber der zweitplatzierten Partei nach Transparenz

(2) Stimmenanteil der Partei "Tisza" von der Anzahl der Wahlberechtigten eines jedem Wahlkreises

(3) Stimmenanteil der Partei "Fidesz" von der Anzahl der Wahlberechtigten eines jedem Wahlkreises

## Umsetzung der Methode

Zuerst wurde die .json-Datei der Wahlkreise in Google Colab zu einer QGIS konformen .geojson umgewandelt. Die Wahldaten wurden durch den Feldrechner in QGIS um die benötigten Werte ergänzt. 
Wahlkreissieger nach Stimmen in einer Spalte darstellen:

```
case
 
when  "ungarn_wahlen_2026_Tisza_Stimmen" >  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Tisza'

when  "ungarn_wahlen_2026_Tisza_Stimmen" <  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Fidesz'

else 'Unentschieden'

end
```

Stimmenzahl des Wahlkreissiegers (win_value) in einer Spalte darstellen:

```
max("ungarn_wahlen_2026_Tisza_Stimmen", "ungarn_wahlen_2026_Fidesz_Stimmen")
```

Den relativen Stimmenanteil des Wahlkreissiegers (win_rel) in einer Spalte darstellen:

```
win value / "ungarn_wahlen_2026_Wahlberechtigte"
```

Stimmenvorsprung: 

```
abs (abs ("ungarn_wahlen_2026_Tisza_Stimmen"-"ungarn_wahlen_2026_Fidesz_Stimmen") / ("ungarn_wahlen_2026_Tisza_Stimmen"+"ungarn_wahlen_2026_Fidesz_Stimmen"+"ungarn_wahlen_2026_mh_Stimmen")*100
```

value by alpha variieren (nach Stimmenvorsprung) (regelbasierte Symbolisierung)

```
set_color_part( 
 'black',
 'alpha',
 scale_linear("win_advantage",
 1,45,
 0,200)
 )
```

Auf die nach Wahlkreissieger eingefärbten Wahlkreise wird eine schwarze Fläche gelegt, welche in der Transparenz je nach Höhe des Stimmenvorsprungs variiert. 

>  Value-by-alpha Karten:
>
> stellen zwei Variablen (bivariat) gleichzeitig dar, indem zwei visuelle Eigenschaften (Farbton und Transparenz)
miteinander kombiniert werden. "Alpha" bezeichnet in der Computergrafik den Wert der Transparenz einer Farbe, es werden also Werte (hier: Stimmenvorsprung) durch den Alpha-Wert / Transparenz abgebildet. Ziel dieser Darstellung ist Kombination zweier Kartendarstellung in eine, die Reduktion einer visuellen Überforderung (irrelevante Daten treten in den Hintergrund) und die Darstellung einer räumlichen Verteilung ("Hochburgen"). 

## Erkenntnisse 
Zu erkennen ist, das Tisza in den Städten Hochburgen an Wählern besitzt, während in den ländlicheren Gebieten der Vorsprung zu der zweitplatzierten Partei (Fidesz) geringer ist. 

# EP05 Ursprung-Ziel Karten

<img width="4210" height="2975" alt="Hyperglobe BHT Studenten-1" src="https://github.com/user-attachments/assets/34db0a52-4975-44e8-8cc6-091c92564aa0" />

## Umsetzung der Methode
Die Shapefiles der Kontinente, Ozeane und Länder stammen von naturalearthdata.org und die Daten der Austauschstudenten von der BHT Referat Auslandsangelegenheiten. Für die Darstellung einer Ursprung-Ziel Karte sollte der Globus auf Berlin zentriert werden. 

Definition einer eigenen Projektion, zentriert auf Berlin
```
+proj=ortho +lat_0=52.52 +lon_0=13.40 +x_0=0 +y_0=0 +a=6371000 +b=6371000 +units=m +no_defs
```
Für die Globusdarstellung wurde ein Punkt auf Berlin zentriert und mit dem Geometriegenerator ein Buffer mit der Länge des Erdradius gezeichnet. Die Shapeburst-Füllung gibt eine 3D-Wirkung.

```
buffer(make_point(0, 0), 6371000)
```

Ausgehend vom Punkt der BHT sind mit dem Geometriegenerator Linien zu den Austauschuniversitäten gezeichnet worden. Je nach Stärke (Anzahl der Studenten) ist die Linie rötlicher eingefärbt

```
make_line(make_point(13.33, 52.54), $geometry)
```

## Vor- und Nachteile der Methode
Die Karte gibt einen schnellen Überblick über die Austauschstudenten der BHT in der Welt. Allerdings ist der Überblick nur für Europa, Afrika, Westasien und Nordamerika zielführend. Sämtliche andere Länder liegen sehr stark verzerrt am Rand des Globus oder sind kaum sichtbar. Da die Darstellung eines Hyperglobes die 3D-Ansicht simuliert, ist eine echte 3D-Animation für eine Ursprung-Ziel Karte naheliegender. Für den Zweck einer 2D-Darstellung ist es trotzdem ausreichend. 

# EP06 Digitales Höhenmodell in QGIS 

<img width="9921" height="7015" alt="BerlinLegoMapModern" src="https://github.com/user-attachments/assets/023c528d-f965-4a26-b485-027a25cf05b6" />

In der Lehrveranstaltung sollte ein digitales Geländemodell im Lego Stil von Berlin erstellt werden. Deutlich zu erkennen ist das Urstromtal, die Ausläufer der Havel nordwestlich von Grunewald und Erhebungen wie der Teufelsberg in Charlottenburg.

<p align="center">
   <img width="60%" height="auto" alt="DeutschlandLegoMapModern" src="https://github.com/user-attachments/assets/2b845ec0-ca33-4e35-bdc7-221b4087b368" />
<p>

## Umsetzung der Methode
Grundlage ist ein digitales Höhenmodell (DGM) Deutschlands als .geotiff-Datei. Das Rasterbild besteht aus Grauwerten, welche je nach Höhe variieren. Auf die Shapefile Deutschlands wurde ein Gitter (Quadrate) zugeschnitten. Der Rasterlayer des DGM und der Polygonvektorlayer des Gitters wurden mit der *Zonenstatistik* verrechnet. Auf jede Zelle des Polygonvektorlayers wird der durchschnittliche Höhenwert berechnet und abgespeichert. Die Zellen mit den Durchschnittswerten wurden entsprechend symbolisiert und im Legostil gestylt.

Wichtig ist bei der Darstellung von Höhenmodellen die sinnvolle Klassifizierung der Symbolisierung. Unterschiedliche Klassifizierungen können die Sichtbarkeit von Gebirgen, Täler und Höhenunterschieden verringern oder verbessern. Die obig dargestellten digitalen Höhenmodelle sind nach Jenks klassifiziert, da hier die Sichtbarkeit von Geländeformen am besten war. 

# EP07 Animation in QGIS

<img width="1012" height="639" alt="Geminiden2022-12-14" src="https://github.com/user-attachments/assets/bec81828-10f9-41ae-a3c9-7b1b0546a9db" />

Dargestellt ist der Geminiden-Meteorschauer am 14.12.2022-15.12.2022 während seines Höhepunktes über dem Vereinigten Königreich und Irland. 

## Umsetzung der Methode

Auf meteoshowers.org konnte sollte ein Meteorschauer herausgesucht werden. Der Datensatz stammt aus: https://tammojan.github.io/meteormap/. Die Daten bestehen aus einer Start- und Endkoordinate des jeweiligen Meteors sowie einem Zeitstempel, wann dieser aufgenommen wurde. Zuerst musste allerdings das Zeitformat in ein ISO Format umgewandelt werden, um in QGIS die dynamische Zeitsteuerung zu aktivieren.
> ISO 8601 (Zeitformat)
> 
> YYYY-MM-DDThh:mm:ss.f (f = dezimale Bruchteile, in der Regel von Sekunden)
> 
> z.B. 2025-08-12T19:55:21.565

In der Symbolisierung wurde mit dem Geometriegenerator zwischen den Koordinaten "LatLonBeg" und "LatLonEnd" für jeden Meteor eine interpolierte Linie gezeichnet, welche mit einem Farbverlaufshader den Schweif simuliert. Die Basemap ist in einem dunklen Grau und Schwarz gehalten, um die Nachtfarben darzustellen. In der dynamischen Zeitsteuerung wurde der Zeitraum des Höhepunktes mit dem zeitlichen Intervall von einer Minute als Bilderstapel exportiert. Die Umwandlung in ein GIF erfolgte wieder in Colab.

## Vor- und Nachteile der Methode
Gerade bei animierten Darstellungen sind interaktive Elemente wichtig. Eine Möglichkeit den Meteorschauer zu verlangsamen, zu verschnellern oder zu vergrößern / verkleinern verbessert die Nutzerfreundlichkeit der Darstellung. 

# EP08 Mesh-Daten

![](https://github.com/Konstruktor1984/DTM/blob/85bc6b75220bbe5899620f0d8dbdf57a7458f936/Orkan%20Kyrill.gif)

Grundlage sind die Wetterdaten (als .grib) des Copernicus-Programms (EU) aus dem "Climate Data Store" vom 16.01.2007 00:00 bis 21.01.2007 16:00. Die vorhandenen Winddaten (Geschwindigkeit und Richtung) sollten in QGIS im Stile eines Künstlers visualisiert werden.

## Umsetzung der Methode
Die .grib Daten wurden in QGIS eingepflegt und die Stromlinienform passend eingestellt. Als Basislayer dient eine ESRI Satellite Map. Ich habe mich für die Gestaltung nach Vincent van Gogh entschieden. Basis dafür war das Bild "Sternennacht" aus Blau, Gelb und Weißtönen. Dazu wurde die ESRI Basiskarte nachtblau eingefärbt, sodass die topographischen Merkmale Europas nur noch schemenhaft zu erkennen sind. Die Stromlinien der Windvektoren sind durch einen Farbverlaufsshader von nachtblau (niedrige Windgeschwindigkeit) über ockergelb (mittlere Windgeschwindigkeit) bis cremeweiß (hohe Windgeschwindigkeit) nach Geschwindigkeit (0-18 m/s) eingefärbt. Damit repräsentieren sie die vorherrschenden Farbtöne des Bildes "Sternennacht". Ich habe mich gegen einen Mischmodus bzw. dem Mischen des Wind- und Basiskartenlayers entschieden, da eine farbgetreue Abbildung nicht möglich und keine ästhetische Verbesserung zu erwarten war. 
Mit einem zeitlichen Intervall von einer Stunde pro Bild wurde ein Bilderstapel exportiert, als GIF zusammengeführt und für den github-Upload komprimiert. Die nachträgliche Kompression hat den Nebeneffekten von "ausgefransten" Linien, welche der Malerei auf Leinwand nahe kommen. 
## Vor- und Nachteile der Methode
Die Darstellung gibt einen schnellen, groben Überblick über die Windlage über Europa im Zeitabschnitt. Außerdem ist sie gut geeignet für ästhetische Darstellungen (nach Künstlern oder wie in der Lehrveranstaltung). Sie eignet sich schlecht für eine genaue Lokalisation von Orten (Maßstab zu klein) und ist limitiert durch den maximalen Detailgrad (Stromliniendicke und Maßstab bei Export) Benutzerfreundlicher wäre eine interaktive Karte mit Zoomleveln und dynamisch angepassten Stromliniendicken, welche eine feinere Beobachtung der Wetterlage ermöglichen. Zustäzlich sind kleinere Zeitintervalle und ein Panel mit Start/Stopp, Zeitachse und "fast forward" Button vom Vorteil bei der Betrachtung dynamischer Karten. 

# EP09 3D-Gebäudemodelle

## 2,5D Darstellung der Oldenburger Innenstadt

<img width="3368" height="2380" alt="oldenburg2_5d-1" src="https://github.com/user-attachments/assets/3885b3ce-c709-4103-97fd-fd2e26338c1f" />

Die Daten stammen von LGLN Niedersachsen und zeigen die Oldenburger Innenstadt. Für die Darstellung mussten zwei Kacheln (LOD2....) wie in der Karte dargestellt, genutzt werden. Auffällig ist das Fehlen von Polygonen öffentlicher Gebäude wie die Lambertikirche inmitten der Innenstadt oder das Bahnhofsgebäude im Nordosten. Da das Land Niedersachsen keine Sondermodelle anbietet (möglich wäre eine zu komplexe Dachstruktur bei Kirchen), werden die Modelle entweder durch die Randlage in der Kachel unvollständig und somit nicht darstellbar oder fehlen aus anderen Gründen. 

> 2,5 D
> 
> Die Höhenwerte werden lediglich als Attribute eines 2D modellierten Objektes gespeichert. Dies ist zum Bespiel bei DGM der Fall. Senkrechte Wände, Tunnel oder Überstände lassen sich nicht darstellen, weil hier mehrere Punkte verschiedener Höhen übereinanderliegen. Gleichzeitig benötigen 2,5D Darstellungen dadurch weniger Prozessorleistung zur Darstellung.

## 3D Darstellung von Norderney

<img width="2116" height="820" alt="Screenshot 2026-08-18 2018459" src="https://github.com/user-attachments/assets/dafc144e-7373-4f84-a016-4c2bf004b6f4" />

Für die 3D-Ansicht von Norderney wurden vier Kacheln LOD2 Objekten genutzt. Als Basemap dient eine stylisierte Karte von Esri. 

*Prozess:*
<img width="1848" height="959" alt="Screenshot 2026-08-18 195944" src="https://github.com/user-attachments/assets/550914ff-f1bb-43e7-9f36-de7c4ae8b34f" />

*Problem: Nicht alle Gebäude liegen auch nach Anpassung eines Versatzes korrekt auf dem Gelände.*
Norderney besitzt welliges Gelände, wie in der Untenansicht sichtbar wird.

<img width="2457" height="1213" alt="Screenshot 2026-08-18 200039" src="https://github.com/user-attachments/assets/c41bfc05-d713-4908-85bd-fbcd8abaa597" />

Es besteht die Möglichkeit das Gelände mit einem Modell zu hinterlegen.
Für die Anpassung des 3D-Geländes wurde das DGM1 (Digitales Geländemodell mit einer Rasterbreite von 1 m) des Landesamtes für Geoinformation und Landesvermessung Niedersachsen genutzt. Auf OpenGeoDataNI wird es in 1x1km Kacheln zum Download bereitgestellt.

*Bildung eines Mosaiks aus vier .geoTiff DGM1 Kacheln als Rasterlayer für die 3D Ansicht:*
<img width="2553" height="1150" alt="Screenshot 2026-08-18 200833" src="https://github.com/user-attachments/assets/b0d594c1-29bd-4acc-a03b-060a51928f6c" />

Wie z.B. beim Turm sichtbar wird, liegen die Gebäude nun besser im Gelände.
<img width="2363" height="1156" alt="Screenshot 2026-08-18 201233" src="https://github.com/user-attachments/assets/67f9b214-659f-4714-a229-b1a5df738aa7" />

*Anpassung mit Farbe durch regelbasierte Symbolisierung:*
<img width="2514" height="1307" alt="Screenshot 2026-08-18 201933" src="https://github.com/user-attachments/assets/0b134204-b5cd-4e99-b6eb-5cce430ca7db" />






