# degauss/pepr_drivetime

> DeGAUSS container that calculates driving distance to care center for PEPR multi-site study

## Geomarker Data

### Drive Time Isochrones (`drive_time`)

This container uses isochrones to assign drive time to care center for each participant address.  Drive time isochrones are concentric polygons, in which each point inside a polygon has the same drive time to the care center. Below is an example of drive time isochrones around Cincinnati Children's Hospital Medical Center.

![](figs/cchmc_isochrones_fig.png)

For each care center, drive times are assigned in 6-minute intervals.  Locations farther than 1 hour away will be assigned a drive time of "> 60".

Drive time isochrones were obtained from [openroute service](https://maps.openrouteservice.org/reach?n1=38.393339&n2=-95.339355&n3=5&b=0&i=0&j1=30&j2=15&k1=en-US&k2=km).

### Distance (`distance`)

This container also calculates "as the crow flies" distance (meters) from care center for each participant address. The distance does not take into account driving routes, but rather provides an overall metric for how far a participant lives from their care center.

## Using

DeGAUSS arguments specific to this container:

- `file_name`: name of a CSV file in the current working directory with columns named `lat` and `lon`
- `site`: abbreviation for care center for which you would like to obtain drive time and distance; must be from the list below

| **Name** |  **Abbreviation** |
|--------------------|-------------------|
Children's Hospital of Philadelphia | `chop` 
Riley Hospital for Children, Indiana University | `riley`
Seattle Children's Hospital | `seattle`
Children's Mercy Hospital | `mercy`
Emory University | `emory`
Johns Hopkins University | `jhu`
Cleveland Clinic | `cc`
Levine Children's | `levine`
St. Louis Children's Hospital | `stl`
Oregon Health and Science University | `ohsu`
University of Michigan Health System | `umich`
Children's Hospital of Alabama | `al`
Cincinnati Children's Hospital Medical Center | `cchmc`
Nationwide Children's Hospital | `nat`
University of California, Los Angeles | `ucla`
Boston Children's Hospital | `bch`
Medical College of Wisconsin | `mcw`
St. Jude's Children's Hospital | `stj`
Martha Eliot Health Center | `mehc`
Ann & Lurie Children's / Northwestern | `nwu`
Lurie Children's Center in Northbrook | `lccn`
Lurie Children's Center in Lincoln Park | `lcclp`
Lurie Children's Center in Uptown | `lccu`
Dr. Lio's and Dr. Aggarwal's Clinics | `lac`
Recruited from Eczema Expo 2018 | `expo`

Example calls (that will work with example file included in repository):

**MacOS**

```
docker run --rm -v "$PWD":/tmp degauss/pepr_drivetime:0.6 my_address_file_geocoded.csv cchmc
```

**Microsoft Windows**

```
docker run --rm -v "%cd%":/tmp degauss/pepr_drivetime:0.6 my_address_file_geocoded.csv cchmc
```

In the above example call, replace `my_address_file_geocoded.csv` with the name of your geocoded csv file and `cchmc` with the abbreviation for the care center to be used for drive time and distance calculations.

Some progress messages will be printed and when complete, the program will save the output as the same name as the input file name, but with `pepr_drivetime` and the care center abbreviation appended, e.g. `my_address_file_geocoded_pepr_drivetime_cchmc.csv`

## DeGAUSS Details

For detailed documentation on DeGAUSS, including general usage and installation, please see the [DeGAUSS](https://degauss.org) website.
