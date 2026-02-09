# Stadtteil mapping for Baustellen-Vorschau

This notebook maps Karlsruhe Baustellen-Vorschau geodata (Point, LineString, MultiLineString, Polygon, MultiPolygon) to Stadtteile polygons. The core idea is to load raw CSVs, build GeoDataFrames with geometries, then spatially join each geometry type to the Stadtteile map so each feature is tagged with `Stadtteil` and `Stadtteil_Nummer`.

## Structure

- `src/add_stadtteil_baustellen_vorschau_divided.ipynb`
  - Loads raw CSVs from `data/mobidata/raw/csv_files/`
  - Loads Stadtteile polygons from `data/map/Stadtteile_SHP/Stadtviertel_Karlsruhe.shp`
  - Converts geometry columns to Shapely objects
  - Applies `gpd.sjoin(..., predicate="intersects")` for each geometry type
  - Produces:
    - `gdf_Point_stadtteil`
    - `gdf_LineString_stadtteil`
    - `gdf_MultiLineString_stadtteil`
    - `gdf_Polygon_stadtteil`
    - `gdf_MultiPolygon_stadtteil`

## Key functions

- `gpd.GeoDataFrame(...)` for constructing geodataframes
- `shapely.geometry.shape(...)` to parse geometry from stored coordinates
- `gpd.sjoin(left, right, how="left", predicate="intersects")` to attach Stadtteil attributes

## How to use

1. Ensure the raw CSV files exist in `data/mobidata/raw/csv_files/` and the Stadtteile shapefile exists in `data/map/Stadtteile_SHP/`.
2. Open and run `src/add_stadtteil_baustellen_vorschau_divided.ipynb` from top to bottom.
3. Inspect the `*_stadtteil` outputs or export them as needed.

## Function documentation

- GeoPandas spatial join (`sjoin`) docs:

```text
https://geopandas.org/en/stable/docs/reference/api/geopandas.sjoin.html
```
