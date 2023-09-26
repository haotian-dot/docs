---
sidebar_position: 4
---

# View and Configure Map Data

This section will introduce how to view and configure map topics.

## View/Hide Map Topic

### View/Hide Map Topic

### View the Information of a Specific Point's Corresponding Topic in the View

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-view-point-information.mp4" controls="controls" width="700" height="400"></video>

## Set Map Attributes

### Adjust Map Transparency

If the map is overlaid (map not shown), you can adjust the transparency of the topmost map. For instance, adjusting the transparency of the elevator map:

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-setting-map-transparency.mp4" controls="controls" width="700" height="400"></video>

### Adjust Map Boundaries

If the map doesn't display boundaries, you can turn off the move_base/global_costmap/costmap.

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-setting-map-boundary.mp4" controls="controls" width="700" height="400"></video>

## Import a Map

When the bag being played requires a map, you can import the machine's map files map.png and map.yaml to use this map on the visualization page.

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/import-map.mp4" controls="controls" width="700" height="400"></video>

### Extract a Map

coScene supports automatically extracting a map from a bag (containing a map topic) to use this map as shared data within the same project.

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/extract-map.mp4" controls="controls" width="700" height="400"></video>

### Copy a Map

When viewing a bag for issue analysis and requiring map data, you can copy map files from a record with an already extracted map to the current record.

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/copy-map.mp4" controls="controls" width="700" height="400"></video>

### Set Attributes of the Imported Map

Externally imported map topics are closed by default. They require attribute settings to display correctly in visualization.

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/setting-out-map.mp4" controls="controls" width="700" height="400"></video>

Based on the background color of the imported map, the following example parameters are recommended:

- For maps with a blue-white background:
  - Color mode: Gradient
  - Gradient: Left #0011ffff, Right #ffffffff
  - Value min: -20
  - Value max: 1
- For maps with a gray-black background:
  - Color mode: Gradient
  - Gradient: Left #e5e5e5ff, Right #000000ff
  - Value min: -2
  - Value max: 0
