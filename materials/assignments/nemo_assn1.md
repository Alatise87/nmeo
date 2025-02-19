Assignment 1, Spring 2022
================

# First assignment

The first class assignment consists of two exercises: one using Earth
Engine and the other using your AWS instance. It will be due on Friday
February 18th at midnight. Submission instructions for each will be
provided below.

## Earth Engine

Create a script named with you initials followed by `_nmeo_2022_assn`,
e.g. mine would be `lde_nmeo_2022_assn`.

-   Use this block of code to define the area of interest:

    ``` js
    var aoi = ee.Geometry.Polygon(
        [[[-0.3436329956054607, 9.48094283485201],
          [-0.3436329956054607, 9.334622294426413],
          [-0.18707781982421068, 9.334622294426413],
          [-0.18707781982421068, 9.48094283485201]]], null, false
    );
    ```

-   Load in the Landsat-8 TOA reflectance (“LANDSAT/LC08/C02/T1_TOA”)
    and Sentinel-2 surface reflectance (“COPERNICUS/S2_SR”) collections.
    We used TOA for Landsat because the surface reflectance collection
    only has 4 time points over this area.

-   Filter each collection by the location of the AOI and by for the
    period 2021-03-01 to 2021-12-31.

-   Use the cloud masking functions for each source of imagery to mask
    each collection, and crop them to the AOI.

-   Map an NDVI band onto each cloudmasked collection.

-   Create a smoothed NDVI time series for the AOI from each image
    collection. To do the smoothing, the following functions are
    required:

    -   `addTimeBand`
    -   `smoother`
    -   `reduceFits`

    And a separate smoother should be applied to each collection. When
    applying the smooth, use a 20 day window size

-   Create median composites of:

    -   The Sentinel-2 NDVI series
    -   The smoothed Sentinel-2 NDVI time series
    -   The Landsat-8 NDVI series
    -   The smoothed Landsat-8 NDVI time series

-   Then finally make some plots:

    -   Create a time series chart of the Landsat smoothed and original
        NDVI series for the AOI (Sentinel-2 has a lot of images, so we
        will not do that here).
    -   Use the `displayImage` function we developed to show the 30th
        images from the Sentinel collection and the 30th image from the
        Landsat collection. Use the correct `vizParams` for each to make
        a false color image, e.g. a `vizParams` for Sentinel 2 and one
        for Landsat 8. Set Band min and max values in the `vizParams`
        for each image collection to \[0.2, 0.2, 0.4\]. Use meaningful
        titles in the `vizParams`, e.g. “30th Sentinel 2 image”.
    -   Plot the median NDVI images for all four median images (S2 NDVI
        median; S2 smoothed NDVI median; L8 NDVI median; L8 smoothed
        NDVI median). Use a range of `{min: -0.5, max: 1}` to stretch
        the NDVI images, and also add meaningful titles,
        e.g. “Sentinel-2 median NDVI”.

### Reference code

The code we have already used in class provides the ingredients for how
to undertake this assignment, such as this
[one](https://code.earthengine.google.com/94a61ebc88710eb4becc30668152996b)
and this
[one](https://code.earthengine.google.com/cfe5da89d3e806d951848aea3d1ac953),
as well as your own homework.

### Materials to hand-in

Create a set of Google slides with Name written as
`firstname_lastname_nmeo_assn1` (replace firstname and lastname with
your names) Provide a link to your script in the slides, and images of
all the plots made in your notebook.

## AWS

In this exercise, you will re-use the notebook we used in class to
select another tile to subset. To do this, you can use the notebook in
the class repo, rather than the ones that we used in the last class. A
bit of prep is necessary. - Log into the AWS console and start your
instance. - `ssh` in to the instance. - Once in,
`cd /home/rstudio/projects` - Then run
`git clone https://github.com/agroimpacts/nmeo.git`. This will install
the class repository onto your instance. - Then run:

``` bash
cp nmeo/materials/code/notebooks/retile_images_on_cloud.ipynb notebooks/ 
```

    That will copy the notebook from the class repo to your notebooks folder. 

-   Then run `screen`, and once in the other screen `jupyter lab`.
    ctrl+a+d back to the original screen, and open up `jupyter lab`
    interface in a browser.
-   Navigate to the notebook you copied in the `jupyter lab` file
    browser, and rename it `<yourinitials>_nmeo_2022_assn`, where
    <yourinitials> is replaced with your actual initials.
-   Work through the notebook. Select tile 300 as the one to create a
    subset, and then work through the whole notebook.
-   Once done, go to the menu at the top of the interface, and select
    File > Download. That will download the notebook to your local
    computer.

### Materials to hand in

Send me the completed notebook.

## Assessment

This assignment will be assessed out of 50 points, with 35 assigned to
the Earth Engine section and 15 to the AWS section.

Points will be assigned as follows:

For Earth Engine:

| Assignment tasks | Points | Style of code & presentation       | Points |
|------------------|--------|------------------------------------|--------|
| 0-25% correct    | 10     | Messy & undocumented               | 2.5    |
| 25-50% correct   | 15     | Fairly messy, lightly documented   | 5      |
| 50-75% correct   | 20     | Somewhat tidy, somewhat documented | 7.5    |
| 75-100% correct  | 25     | Tidy, well-documented              | 10     |

For AWS:

Fully and correctly completed notebook is worth 15 points. Fully
complete entails:

-   Notebook template used as instructed: 2 pts
-   Correct tile processed: 2 pts
-   All plots rendered (tile grids and retiled images): 5 points
-   Retiled image transferred to AWS bucket: 5 points
-   Downloaded notebook submitted via Slack: 1 point
