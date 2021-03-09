# Exercise-1: Working with Geometric Objects

*Credit*
[Vuokko Heikinheimo, Henrikki Tenkanen](https://automating-gis-processes.github.io/)

We will practice how to create geometric objects using Shapely module and how to find out different useful attributes from those geometries.
We will also use Pandas to read data from a file.

## Sections

 - [Problem 1: Creating basic geometries](#problem-1-creating-basic-geometries)
 - [Problem 2: Attributes of geometries](#problem-2-attributes-of-geometries)
 - [Problem 3: Reading coordinates from a file and creating a geometries](#problem-3-Reading-coordinates-from-a-file-and-creating-a-geometries-(optional))

## Problem 1: Creating basic geometries

Write your codes into a single `create_geometries.py` -file and upload the script to your personal GitHub branch.

1. Create a function called `createPointGeom()` that has two parameters (x_coord, y_coord). Function should create a shapely Point geometry object and return that.
Demonstrate the usage of the function by creating Point -objects with the function.

2. Create a function called `createLineGeom()` that takes a list of Shapely Point objects as parameter and returns a
LineString object of those input points. Function should first check that the input list really contains Shapely Point(s).
Demonstrate the usage of the function by creating LineString -objects with the function.

3. Create a function called `createPolyGeom()` that takes a list of coordinate tuples **OR** a list of Shapely Point objects and returns a Polygon object of the input data. Both ways of passing the data to the function should be working.
Make sure you can pass the data for both exterior (required), and interior ring (optional).

Test your function with the following parameters:

```
exterior = [(0.7116692108637522, 0.7111061228019184),
 (0.5080310431525847, 0.922855404602472),
 (0.10495858060349925, 1.032189541996318),
 (-0.374764701370009, 0.9391994778121242),
 (-0.6724519439208715, 0.7414477759474434),
 (-0.8915613009360314, 0.44326589552388707),
 (-0.9951704640914677, 0.03573412832368477),
 (-0.7354800494393435, -0.6764712313313701),
 (-0.4511288800308735, -0.8905982588492805),
 (-0.05187728606671324, -0.9984728234571857),
 (0.38929165762045026, -0.9019367539827067),
 (0.7393667707249828, -0.6748412987256568),
 (0.0, 0.0),
 (0.7116692108637522, 0.7111061228019184)]

interior = [(0.30000000000000004, 0.7),
 (0.27943615696959956, 0.6392554778938779),
 (0.2466077775397787, 0.6115256247673796),
 (0.20517258568582375, 0.6001338678163471),
 (0.1627821997184475, 0.6071838627058717),
 (0.12726462860667803, 0.6313737240681419),
 (0.10056852582767012, 0.6893519042116772),
 (0.10528037242218496, 0.7320654354643753),
 (0.1274835929992999, 0.7688576118937391),
 (0.18390851956161536, 0.7986968300266076),
 (0.22681632878439417, 0.7963373474335227),
 (0.26477210802560597, 0.7761877550654909),
 (0.2907667637479727, 0.7419689718568337),
 (0.30000000000000004, 0.7)]
```

## Problem 2: Attributes of geometries

1. Create a function called `getCentroid()` that takes any kind of Shapely's geometric -object as input and returns a centroid of that geometry. Demonstrate the usage of the function.

2. Create a function called `getArea()` that takes a Shapely's Polygon -object as input and returns the area of that geometry. Demonstrate the usage of the function.

3. Create a function called `getLength()` takes either a Shapely's LineString or Polygon -object as input. Function should check the type of the input and returns the length of
the line if input is LineString and length of the exterior ring if input is Polygon. If something else is passed to the function,
it should tell the user --> `"Error: LineString or Polygon geometries required!"`.  Demonstrate the usage of the function.

## Problem 3: Reading coordinates from a file and creating a geometries (optional)

One of the "classical" problems in GIS is the situation where you have a set of coordinates in a file and you need to get them into a map (or into a GIS-software). Python is a really handy tool to solve this problem as with Python it is basically possible to read data from any kind of input datafile (such as csv-, txt-, excel-, or gpx-files (gps data) or from different databases).
So far, I haven't faced any kind of data or file that would be impossible to read with Python.

Thus, let's see how we can read data from a file and create Point -objects from them that can be saved e.g. as a new Shapefile (we will learn this in the next module).
Our dataset **[travelTimes_Helsinki.txt](data/travelTimes_Helsinki.txt)** consist of
travel times between specific locations in Helsinki Region. The first four rows of our data looks like this:

```
   from_id;to_id;fromid_toid;route_number;at;from_x;from_y;to_x;to_y;total_route_time;route_time;route_distance;route_total_lines
   5861326;5785640;5861326_5785640;1;08:10;24.9704379;60.3119173;24.8560344;60.399940599999994;125.0;99.0;22917.6;2.0
   5861326;5785641;5861326_5785641;1;08:10;24.9704379;60.3119173;24.8605682;60.4000135;123.0;102.0;23123.5;2.0
   5861326;5785642;5861326_5785642;1;08:10;24.9704379;60.3119173;24.865102;60.4000863;125.0;103.0;23241.3;2.0
```

Thus, we have many columns of data, but the few important ones are:

| Column | Description |
|--------|-------------|
| from_x | x-coordinate of the **origin** location (longitude) |
| from_y | y-coordinate of the **origin** location (latitude) |
| to_x   | x-coordinate of the **destination** location (longitude)|
| to_y   | y-coordinate of the **destination** location (latitude) |
| total_route_time | Travel time with public transportation at the route |

### Tasks

1. Save the [travelTimes_Helsinki.txt](data/travelTimes_Helsinki.txt) into your computer.
2. Read 4 columns, i.e. 'from_x', 'from_y', 'to_x', 'to_y' from the data into Python using Pandas.
3. Create two lists called `orig_points` and `dest_points`
4. Iterate over the rows of your DataFrame and add Shapely Point -objects into the orig_points -list and dest_point -list representing the origin locations and destination locations accordingly.
5. Iterate over the origin and destination lists and create a Shapely LineString -object between the origin and destination point
6. Find out what is the average (Euclidian) distance of all the origin-destination LineStrings that we just created, and print it out.
