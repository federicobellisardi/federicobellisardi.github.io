---
title: "How to Get UNIBO Cartography from OSM"
description: >-
  A step-by-step guide to extracting and processing cartography data for the University of Bologna using OpenStreetMap (OSM) tools and Physycom utilities.
author: fbellisardi
date: 2025-04-11 08:00:00 +0100
categories: [Blogging, Tutorial]
tags: [cartography, OSM, tools, GIS]
pin: false
---

# How to Get UNIBO Cartography from OSM

This guide provides detailed instructions for extracting and processing cartography data from OpenStreetMap (OSM) for the University of Bologna (UNIBO). The process involves using various tools, including `osmtools`, `cartography-data`, and `minimocas-tools`, to generate and clean cartography files.

---

## Prerequisites

Before starting, ensure you have the following installed on your system:

- **osmtools**: A set of tools for processing OSM data.
- **cartography-data**: A repository containing tools for converting OSM data.
- **minimocas-tools**: A repository for editing and cleaning cartography files.

---

## Steps to Extract and Process Cartography Data

### 1. Download OSM Cartography

1. Visit the [OSM cartography](https://download.openstreetmap.fr/extracts/europe/italy/) website.
2. Download the **osm.pbf** file containing the OSM cartography for your area of interest.

---

### 2. Install `osmtools`

Install `osmtools` using the following command:

```bash
sudo apt install osmtools
```

---

### 3. Extract a Boundary Box from OSM

Identify the boundary box of interest and run the following command to extract it:

```bash
osmconvert file.osm.pbf -b="lon_min, lat_min, lon_max, lat_max" -o=output_name.osm
```

Replace `lon_min`, `lat_min`, `lon_max`, and `lat_max` with the coordinates of your area of interest.

---

### 4. Convert OSM Data Using `cartography-data`

1. Clone the [cartography-data](https://github.com/physycom/cartography-data) repository:
   ```bash
   git clone https://github.com/physycom/cartography-data.git
   ```
2. Run the `cartconv_osm` executable on a configuration JSON file:
   ```bash
   $WORKSPACE/cartography-data/build_release/cartconv_osm /path_to_conf/config.json
   ```
3. Use a JSON file with the following structure:
   ```json
   {
     "osm_data" : "path_to_OSM_file.osm",
     "out_base" : "output_name",
     "bbox"     :
     {
       "lat_max" : 45.3055084,
       "lat_min" : 43.8698767,
       "lon_max" : 12.7978165,
       "lon_min" : 9.0652115
     }
   }
   ```

This operation generates **.pnt** and **.pro** files that need to be cleaned.

---

### 5. Create an `.edit` File

Create a file with the `.edit` extension using the following structure:

```json
{
  "file_pro"          : "path_to_pro.pro",
  "file_pnt"          : "path_to_pnt.pnt",
  "cartout_basename"  : "path_to_file.edit",
  "explore_node"      : [0],
  "enable_merge_subgraph" : true,
  "enable_remove_degree2" : true,
  "enable_attach_nodes"   : true
}
```

---

### 6. Edit the Cartography Using `minimocas-tools`

1. Clone the [minimocas-tools](https://github.com/physycom/minimocas-tools) repository:
   ```bash
   git clone https://github.com/physycom/minimocas-tools.git
   ```
2. Run the `miniedit` executable on the `.edit` file:
   ```bash
   $WORKSPACE/minimocas-tools/bin/miniedit /path_to_edit/path_to_file.edit
   ```

This operation generates the following files:

- **.edit.pnt**
- **.edit.pro**
- **.edit.test**

---

### 7. Clean the `.edit.test` File

Run `miniedit` on the `.edit.test` file:

```bash
$WORKSPACE/minimocas-tools/bin/miniedit /path_to_edit/path_to_file.edit.test
```

Use a JSON configuration file with the following structure:

```json
{
  "file_pnt"          : "/path_to_pnt/*.edit.pnt",
  "file_pro"          : "/path_to_pnt/*.edit.pro",
  "verbose"           : false,
  "enable_histo"      : false,
  "enable_gui"        : true,
  "enable_bp"         : false,
  "enable_geojson"    : true,
  "enable_explore"    : false,
  "bp_matrix"         : false,
  "state_grid_cell_m" : 1000
}
```

---

### 8. Generate Simplified Cartography Files

Repeat the process to generate the following simplified cartography files:

- **carto_edit.pro**
- **carto_edit.pnt**
- **carto_edit.test**

---

### 9. Verify the Cleaned Cartography

Run `minitest` on the `.test` configuration files to verify the cleaned cartography:

```bash
$WORKSPACE/minimocas-tools/bin/minitest /path_to_edit/path_to_file.edit.test
$WORKSPACE/minimocas-tools/bin/minitest /path_to_edit/path_to_file.carto_edit.test
```

---

## Conclusion

By following these steps, you can extract, process, and clean cartography data from OSM for use in various applications. Ensure that all tools and dependencies are correctly installed before starting the process.