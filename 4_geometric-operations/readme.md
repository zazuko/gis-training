# Exercise 4

This module we will practice how to do geometric operations in Geopandas. We will also cover data aggregation, and classification.

## Problem 1: How many people live close to a train station?

In this exercise we will be working with population data in Zürich area. The area is split into grid, with equidistant lines draw every 100m. As a result, each grid call has 100x100m. Population statistics are reported for each grid cell. The cells that are not reported are unpopulated.

The raw data, alongside with its description, is available [here](https://www.bfs.admin.ch/bfs/en/home/services/geostat/swiss-federal-statistics-geodata/population-buildings-dwellings-persons/population-housholds-from-2010.assetdetail.3543467.html). The coordinates on population grid are defined in [LV95](https://epsg.io/2056) format.

The city borders are available [here as linked data](https://ld.geo.admin.ch/boundaries/municipality/261).

The goal of this exercise is to find out how many people live within 2km from a train station.

**Steps**
- Load the population grid from `data/Zurich/population.shp`
- Load city borders from `data/Zurich/border.geojson`
- Align CRS on both dataframes. Let's use [LV95](https://epsg.io/2056) format throughout the exercise.
- Crop the population grid to include only the cells within the city borders.
- Find the coordinates for all train stations in Zurich area:
   ```
   train_stations = [
      "Bahnhof Wiedikon",
      "Bahnhof Wipkingen",
      "Bahnhof Wollishofen",
      "Bahnhof Altstetten",
      "Bahnhof Enge",
      "Bahnhof Zürich Flughafen",
      "Bahnhof Oerlikon",
      "Bahnhof Stadelhofen",
      "Bahnhof Affoltern",
      "Bahnhof Tiefenbrunnen",
      "Bahnhof Zürich HB"
   ]
   ```
   *Hint* Geocoding algorithms perform better if you define object type, city, and contry. Therefore *Bahnhof Wiedikon, Zurich, Switzerland* will work better than simply "Bahnhof Wiedikon".
- Visualize your results on a city map. Remove any train stations outside of city borders.
- Define 2km [`buffer`](https://geopandas.org/docs/user_guide/geometric_manipulations.html#GeoSeries.buffer) around each train station. Save the station names, and buffer polygons in `buffered_stations` dataframe.
- Find the population grid cells where:
   - inhabitants can access a train station within 2km
   - inhabitants have to travel more than 2km to a train station

Plot both areas. How many people live in each of them?
## Problem 2: How many people live close to multiple train stations? (optional)

By now we know how many people live close to some train station. But how many have the luxury of living inear to two, three, or more train stations?

Let's find out how many people can access 0, 1, 2, 3 etc. train stations within 2km.

**Steps**
- For each population cell, calculate number of `stations_nearby`

   *Hints*:
   - Join population, and buffer dataframes using spatial join.
   - Be careful with population cells that are outside any buffer! Set their `stations_nearby` count to 0.

   Save your results in `accessibility` dataframe. It should include:
   * `ID`: population cell ID
   * `pop_total`: population value
   * `geometry`: population cell polygon
   * `stations_nearby`: number of stations within 2km from population cell

- Aggregate the `accessibility` results per `stations_nearby`.
- Count number of inhabitants within each accessibility zone
- Plot `accessibility` areas. Classify them using `stations_nearby` column.
- Plot `buffered_stations`. Do your results make sense?
- Save your results to `accessibility.shp` file