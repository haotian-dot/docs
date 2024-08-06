---
sidebar_position: 2
---

# File Preparation

After creating a Record, upload Bag / Mcap format files and other necessary files for playback.
Note: For detailed steps on creating a Record and uploading files, refer to [Upload Files](../4-record/2-upload-files.md).

## Managing File Media Types

For data lacking map and static TF information:
1. Copy the bag file containing such information into the corresponding Record and set it as a Static Bag (only using map and coordinate data during playback without playing the file).
2. Manually import map and coordinate files.
3. Extract map and static coordinates from the Record file.

### Setting a Static Bag

1. Upload the static bag containing this information.
    
![viz-2-1-Eng](../img/viz-2-1-Eng.png)

2. Click the **Actions** button on the right side of the Record and select **Set File Media Type** in the popup.
    
![viz-2-2-Eng](../img/viz-2-2-Eng.png)

3. Set the media type of the Bag file to **Static Bag** and click **Confirm** to complete the modification.
   
![viz-2-3-Eng](../img/viz-2-3-Eng.png)

### Manually Importing Static Map and Coordinate Files

#### Static Map

1. Upload the map file to the Record and click the **More** button on the right side of the Record.
   
![viz-2-4-Eng](../img/viz-2-4-Eng.png)
 
2. Click the **Actions** button on the right side of the Record file and select **Set File Media Type** in the popup.
   
![viz-2-5-Eng](../img/viz-2-5-Eng.png)
 
3. Set the media type of the file to **Map** and click **Confirm** to complete the modification.
   
![viz-2-6-Eng](../img/viz-2-6-Eng.png)

#### Static Coordinates

1. Upload the static coordinate file to the Record.
   
![viz-2-7-Eng](../img/viz-2-7-Eng.png)
 
2. Click the **Actions** button on the right side of the Record file and select **Set File Media Type** in the popup.
   
![viz-2-8-Eng](../img/viz-2-8-Eng.png)
 
3. Set the media type of the file to **Static TF** and click **Confirm** to complete the modification.
    
![viz-2-9-Eng](../img/viz-2-9-Eng.png)

### Extracting Map and Coordinates from Record Files

1. Find the Record that can be extracted from the Record list.
   
![viz-2-10-Eng](../img/viz-2-10-Eng.png)
 
2. Click the **Actions** button on the right side of the Record file and select **Extract Map** and **Extract Dynamic Coordinates** in the popup.
    
![viz-2-11-Eng](../img/viz-2-11-Eng.png)
 
3. After selecting, click **Invocations** to check the status of the action invocation.
   
![viz-2-12-Eng](../img/viz-2-12-Eng.png)
 
4. After the action is successfully invoked, return to the Record details page to view the generated map and coordinate files, completing the extraction.
    
![viz-2-13-Eng](../img/viz-2-13-Eng.png)

