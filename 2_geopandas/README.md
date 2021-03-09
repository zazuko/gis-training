# Exercise 2

In this section we will focus on how to create geometries in Geopandas, how to re-project data and do some basic
geometric calculations.

The Exercise 2 continues the process what we started, i.e. creating geometric objects and putting them into a map.
Here our aim is to plot a London Underground network. The data is available in `data/London/metro_routes.csv` and `data/London/metro_stations.csv`.

## Sections

 - [Problem 1: Points to map](#problem-1-points-to-map)
 - [Problem 2: Lines to map](#problem-2-lines-to-map)
 - [Problem 3: Split data by line](#problem-3-split-data-by-line)
 - [Problem 4: Split data by line](#problem-3-split-data-by-line)

## Problem 1: Points to map

Plot all stations of London Underground on a map.

**Steps**
- Read the `data/London/metro_stations.csv` into memory using geopandas. Store those in `segments` dataframe
- Define the coordinate reference system as [WGS84](https://epsg.io/4326). Hint: use `.set_crs()` function
- Transform `segments` dataframe in such a way, that one row corresponds to one station. Store the results in `stations` dataframe.
- Create shapely Point object for each station in `stations` dataframe. Store them in `geometry` column.
- Create a simple map of the stations using `.plot()` -funtion in Python.

## Problem 2: Lines to map

Plot all lines of London Underground on a map.

**Steps**
- Create LineString representation for each metro segment. Store them in `geometry` column in `segments` dataframe.
- Create a simple map of lines using `.plot()` funtion
- Create a joint map of lines, and stations.

# Problem 3: Split data by line

Group data together for each metro line. Plot each line and its stations with different color.

**Steps**
- Group lines data:
    - Group the `segments` by line.
    - For each group, create one MultiLineString. It should aggregate all the geometries in a group.
    - Store the results (line number and new geometry) in `lines` dataframe.
    - Save your results to `underground_lines.shp`
- Group stations data:
    - Implement similar approach on `stations` dataframe. What geometry will you use?
    - Save your results to `underground_stations.shp`
- Visualize your results
    - Load `data/London/metro_routes.csv` into memory
    - Create a `colormap` dictionnary. The keys should correspond to `line`, and values to `colour`
    - Plot all lines, and stations on the same map. For each line, apply the colour from `colormap`

# Problem 4:

Find the answers to the following questions:

 - What is the average segment length in meters?
 - What is the shortest line in meters?
 - What is the longest line in meters?
 - Where does the longest line go? Plot it.

 **Remember to reproject your data!** To calculate the anseres, you will need to use the projected coordinate system.
 Which one would you choose for UK?