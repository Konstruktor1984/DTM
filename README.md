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

## Umwandlung json zu geojson
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

## Code zur Auswahl der gewinnenden Partei in Attributtabelle
case
 
when  "ungarn_wahlen_2026_Tisza_Stimmen" >  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Tisza'

when  "ungarn_wahlen_2026_Tisza_Stimmen" <  "ungarn_wahlen_2026_Fidesz_Stimmen" THEN 'Fidesz'

else 'Unentschieden'

end
