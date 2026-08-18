# DTM
# EP01 Dasymmetrische Chloroplethenkarten
<img width="10523" height="7440" alt="DTM_EP01_Thorben Flick" src="https://github.com/user-attachments/assets/2385e742-db06-4a96-841d-596e1d2b79f1" />

## Umsetzung der Methode 
## Vor- und Nachteile der Methode

# EP02
<img width="3368" height="2380" alt="Kirschblüten-1" src="https://github.com/user-attachments/assets/bbe1d4f0-1b73-4d82-93cb-ff7d57a8189a" />

## Umsetzung der Methode
## Vor- und Nachteile der Methode

# EP03 Punktrasterkarten


# EP04 value-by-alpha-mapping

## Umsetzung der Methode
Umwandlung json zu geojson
```
import json

# 1. Datei laden (Stelle sicher, dass oevk.json im gleichen Ordner liegt)
with open('oevk.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

geojson = {
    "type": "FeatureCollection",
    "features": []
}

for item in data:
    # Koordinaten-String säubern und in Liste von Floats umwandeln
    # Wichtig: In der Quelle ist es "Lat Lon", GeoJSON braucht "Lon Lat"
    raw_coords = item['poligon'].split(',')
    clean_coords = []
    for pair in raw_coords:
        lat, lon = pair.strip().split(' ')
        clean_coords.append([float(lon), float(lat)])

    # Erstes Element am Ende wiederholen, um Polygon zu schließen
    if clean_coords[0] != clean_coords[-1]:
        clean_coords.append(clean_coords[0])

    feature = {
        "type": "Feature",
        "properties": {
            "maz": item['maz'],
            "evk": item['evk'],
            "centrum": item['centrum']
        },
        "geometry": {
            "type": "Polygon",
            "coordinates": [clean_coords]
        }
    }
    geojson['features'].append(feature)

# 2. Als echte GeoJSON speichern
with open('ungarn_wahlbezirke.geojson', 'w', encoding='utf-8') as f:
    json.dump(geojson, f)

print("Fertig! Die Datei 'ungarn_wahlbezirke.geojson' wurde erstellt.")
```

Code zur Auswahl der gewinnenden Partei in Attributtabelle
```
case
 
when  "ungarn_wahlen_2026_Tisza_Stimmen" >  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Tisza'

when  "ungarn_wahlen_2026_Tisza_Stimmen" <  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Fidesz'

else 'Unentschieden'

end
```
win_value berechnen mit max Funktion (max Tidasz, Fidesz)

win_rel berechnen mit win value / wahlberechtigte

win_advantage berechnen mit abs (abs (tidasz-fidesz)/(tidasz+fidesz+mh)*100

value by alpha variieren (nach Vorsprung)
```
set_color_part( 
 'black',
 'alpha',
 scale_linear("win_advantage",
 1,45,
 0,200)
 )
```

## Vor- und Nachteile der Methode

## 1. Karte wie LV, 2. Karte nur Stimmanteil Fidesz 3. Karte nur Stimmmanteil Tidasz

# EP05 Ursprung-Ziel Karten
<img width="4210" height="2975" alt="Hyperglobe BHT Studenten-1" src="https://github.com/user-attachments/assets/34db0a52-4975-44e8-8cc6-091c92564aa0" />

## Umsetzung der Methode
## Vor- und Nachteile der Methode

# EP06 Digitales Höhenmodell in QGIS 
<img width="5847" height="8270" alt="DeutschlandLegoMap-1" src="https://github.com/user-attachments/assets/977bc9ce-e3a0-46ac-92ca-5fbff8fc7c5e" />

## Umsetzung der Methode
## Vor- und Nachteile der Metho

# EP07 Animation in QGIS
<img width="1012" height="639" alt="Geminiden2022-12-14" src="https://github.com/user-attachments/assets/bec81828-10f9-41ae-a3c9-7b1b0546a9db" />
Dargestellt ist der Geminiden-Meteorschauer am 14.12.2022-15.12.2022 während seines Peaks über dem Vereinigten Königreich und Irland. 

## Umsetzung der Methode

meteoshowers.org
https://tammojan.github.io/meteormap/
Umwandlung Zeitformat in ISO Format -> colab
Geometriegenerator LatLonBeg - LatLonEnd
Interpolierte Linie
Dynamische Zeitsteuerung
Export als Bilderstapel
GIF Erstellung mit Python -> colab

## Vor- und Nachteile der Methode

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



## 3D Darstellung von Norderney
<img width="2116" height="820" alt="Screenshot 2026-08-18 2018459" src="https://github.com/user-attachments/assets/dafc144e-7373-4f84-a016-4c2bf004b6f4" />

prozess:
<img width="1848" height="959" alt="Screenshot 2026-08-18 195944" src="https://github.com/user-attachments/assets/550914ff-f1bb-43e7-9f36-de7c4ae8b34f" />
 welliges Gelände, untenansicht
 <img width="2457" height="1213" alt="Screenshot 2026-08-18 200039" src="https://github.com/user-attachments/assets/c41bfc05-d713-4908-85bd-fbcd8abaa597" />

Mosaik aus vier GeoTif DGM1 Kacheln als DGM für die 3D Ansicht
<img width="2553" height="1150" alt="Screenshot 2026-08-18 200833" src="https://github.com/user-attachments/assets/b0d594c1-29bd-4acc-a03b-060a51928f6c" />
Ergebnis:
<img width="2363" height="1156" alt="Screenshot 2026-08-18 201233" src="https://github.com/user-attachments/assets/67f9b214-659f-4714-a229-b1a5df738aa7" />

Anpassung mit Farbe durch regelbasierte Symbolisierung
<img width="2514" height="1307" alt="Screenshot 2026-08-18 201933" src="https://github.com/user-attachments/assets/0b134204-b5cd-4e99-b6eb-5cce430ca7db" />






