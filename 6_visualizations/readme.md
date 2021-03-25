# Exercise 6

**Credit**
Big thanks to Patrick Curran for the idea, and the data.

You will find the data in `MSC_ModelData_vectorized` folder. It consists of:
* `humidex.geojson` - Gridded Humidex Values
* `wind_speed.geojson` - Gridded Wind Speed (ht = 10 m) Values
* `clipbox.geojson` - Clip Box
* `land_PubStdZone_coarse_unproj.shp` - MSC Standard Forecast Zones
* `points.geojson` - random locations


Throughout the exercise, use following names for GeoDataFrames:
* `humidex_05.geojson` -> `humidex`
* `wind_speed_05.geojson` -> `wind`
* `WxO_Demo_Smaller_Extent.geojson` -> `clip_box`
* `land_PubStdZone_coarse_unproj.shp` -> `forecast_zones`
* `points.geojson` -> `locations`

## Problem 1: Create heatmap for humidex and wind speed

The goal of this problem is to create heatmap for humidex and wind speed with bokeh.

**Steps**
* Load `humidex` data
* Classify `humidex` values using a map classifier. Add a `class` column to your dataframes.
    *Experiment with different classifiers. Try finding one that best highlights the differences in data.*
* Create a dataframe with class numbers (`class` column), and corresponding geometries (`geometry` column). Make sure to aggregate your geometries.
Store the results in `humidex_classified` dataframe.
    *Hint*
    Let's say `humidex.at[0, "class"] = 3`. Then, the geometry at `humidex.at[0, "geometry"]` should cover all gridpoints that were assigned class number 3.
* Plot `humidex_classified` heatmap using bokeh
* Repeat all steps for `wind` data.


## Problem 2: Report precise values for selected locations

Thus far, we aggregated data into buckets. That's handy when trying to distinguish zones with higher, and lower values.
However, sometimes you will be interested in knowing a precise value at certain location. Let's now add the humidex and windspeed values for selected locations.

**Steps**
* Load `locations` data
* Load `clip_box` data
* Remove any `locations` outside of the `clip_box`
* For each location, find humidex and wind speed values. Store the values in `locations` dataframe.
* Add locations to the map from Problem 1.
* Use `HoverTool` to report the precise humidex and windspeed at the location.


## Problem 3: Analyze weather zones (optional)

Now, let's find weather forecast zones that had expected the most extreme humidex and windspeed values.

**Steps**
* Load `forecast_zones` data
* Clip the `forecast_zones` to the boundaries of `clip_box`
* Find the class number for the highest `humidex`. Store corresponding geometry as `highest_humidex_zone`
* For each `forecast_zone` find the area that overlaps with `highest_humidex_zone`.
Store this new geometry in `geom_humidex_high` column.
* Calculate the area of the forecast zones, and `geom_humidex_high`. Divide `geom_humidex_high` area by forecast zone area.
  Store the results in `ratio` column in `forecast_zones` dataframe.
* Visualize your results (`ratio` per `forecast_zone`) using bokeh.
* Calculate `min`, `max` and `median` humidex value in each forecast zone.
* Add this information to the map. Use `HoverTool`.
