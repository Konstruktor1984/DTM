# DTM
# EP01 Dasymmetrische Chloroplethenkarten
<img width="10523" height="7440" alt="DTM_EP01_Thorben Flick" src="https://github.com/user-attachments/assets/2385e742-db06-4a96-841d-596e1d2b79f1" />

## Vor- und Nachteile der Methode
## Umsetzung der Methode 

# EP02
<img width="3368" height="2380" alt="Kirschblüten-1" src="https://github.com/user-attachments/assets/bbe1d4f0-1b73-4d82-93cb-ff7d57a8189a" />


## Vor- und Nachteile der Methode
## Umsetzung der Methode
### Bild als 

# EP04 

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


## 1. Karte wie LV, 2. Karte nur Stimmanteil Fidesz 3. Karte nur Stimmmanteil Tidasz

# EP06 Digitales Höhenmodell in QGIS 
<img width="5847" height="8270" alt="DeutschlandLegoMap-1" src="https://github.com/user-attachments/assets/977bc9ce-e3a0-46ac-92ca-5fbff8fc7c5e" />


# EP07 Animation in QGIS
<img width="1012" height="639" alt="Geminiden2022-12-14" src="https://github.com/user-attachments/assets/bec81828-10f9-41ae-a3c9-7b1b0546a9db" />
Dargestellt ist der Geminiden-Meteorschauer am 14.12.2022-15.12.2022 während seines Peaks über dem Vereinigten Königreich und Irland. 

## Vor- und Nachteile der Methode
## Umsetzung der Methode 
meteoshowers.org
https://tammojan.github.io/meteormap/
Umwandlung Zeitformat in ISO Format -> colab
Geometriegenerator LatLonBeg - LatLonEnd
Interpolierte Linie
Dynamische Zeitsteuerung
Export als Bilderstapel
GIF Erstellung mit Python -> colab
<img width="3159" height="1997" alt="KartenausschnittGeminiden" src="https://github.com/user-attachments/assets/66ee1fa4-870f-4487-8f8b-8a843862afc9" />



