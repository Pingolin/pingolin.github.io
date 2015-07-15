# lignesdevie
Tests d'une carto des services et équipements autour des gares d'Île-de-France.
L'idée part d'un besoin de trouver si des piscines existaient le long d'un trajet de RER C.
Le projet se base aussi sur la cartographie OpenStreetMap des gares de Transilien dont [le référentiel a été partagé sur le wiki OSM](http://wiki.openstreetmap.org/wiki/FR:Railway_stations).

## To Do :
- Ajouter des contrôles dynamiques : slider pour la distance, choix des lignes, liste d'équipements et services,...
- Ajouter le tracé en couleur des autres lignes que C (export geojson)
- Améliorer l'appel Overpass (très long actuellement)

Après quelques tests avec des bbox, j'ai choisi de faire une seule fois l'appel pour chacun des calques.

La requêtes est sous la forme :

    {{geocodeArea:Île-de-France}}->.searchArea;
    rel["line:SNCF"="C"](area.searchArea);
    node(around:800)[sport=swimming](area.searchArea);
    out body qt;
    rel["line:SNCF"~"C"](area.searchArea);
    way(around:800)[sport=swimming](area.searchArea);
    out center qt;
