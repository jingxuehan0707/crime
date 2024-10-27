# Crime Data Analysis
This project analyzes crime data for Chicago and Los Angeles, aggregating crime points by census tract and type of crime.

## Project Structure

```
.gitignore
chicago_census_tract/
    geo_export_2d3ffe6a-dd57-46d5-86e3-4f42a4df0e73.cpg
    geo_export_2d3ffe6a-dd57-46d5-86e3-4f42a4df0e73.dbf
    geo_export_2d3ffe6a-dd57-46d5-86e3-4f42a4df0e73.prj
    geo_export_2d3ffe6a-dd57-46d5-86e3-4f42a4df0e73.shp
    geo_export_2d3ffe6a-dd57-46d5-86e3-4f42a4df0e73.shx
crime_chicago.ipynb
crime_data/
    crime_chicago_2001_2024_by_tract_type.csv
    crime_chicago_2001_2024.csv
    ...
crime_demo.ipynb
crime_la.ipynb
la_census_tract/
    ...
```

## Notebooks

- **crime_chicago.ipynb**: Analyzes crime data for Chicago.
- **crime_la.ipynb**: Analyzes crime data for Los Angeles.
- **crime_demo.ipynb**: Demonstrates the analysis process.

## Data

- **chicago_census_tract/**: Contains shapefiles for Chicago census tracts. ([download link](https://geohub.lacity.org/datasets/la-city-2020-census-tracts-/explore))
- **crime_data/**: Contains CSV files with crime data for Chicago and Los Angeles.
- **la_census_tract/**: Contains shapefiles for Los Angeles census tracts. ([download link](https://data.cityofchicago.org/api/geospatial/5jrd-6zik?method=export&format=Shapefile))

## Usage

1. **Install Dependencies**:
    ```sh
    pip install pandas geopandas
    ```

2. **Run Notebooks**:
    Open and run the Jupyter notebooks (`crime_chicago.ipynb`, `crime_la.ipynb`) to perform the analysis.

## Functions

### aggregate_points

Aggregates crime points by census tract and type of crime.

```python
def aggregate_points(points_gdf, geometry_gdf):
    points_gdf = gpd.sjoin(points_gdf, geometry_gdf, how='inner', predicate='within')
    points_gdf = points_gdf.groupby(['geoid10', 'Primary Type']).size().reset_index(name='count')
    return points_gdf
```

## Results

The results are saved as CSV files in the `crime_data/` directory.

- `crime_chicago_2001_2024_by_tract_type.csv`
- `crime_la_2020_2024_by_tract_type.csv`

## License

This project is licensed under the MIT License.