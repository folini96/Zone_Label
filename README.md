# Zone Label User Guide

Zone Label is a QGIS 3 plugin that can be used to manually label and describe rectangular areas using an overlay layer. Each area can also be split in other 4 equal areas. 

## Installation
The plugin can be installed from the official plugin repository of QGIS and does not require the installation of any additional library.
Once the plugin is installed, it should be visible both in the UI and in the Plugins section drop down window. In case the plugin is not visible, go to the View section, search for Toolbars, and check ZoneLabel.

## Area selection
The selected area can be either a new empty area, or an existing area with classification. To select the area, check the right option, fill the parameters, and click the "Select area" button. Once the area is created, it will be visible in the map canvas, and the buttons for labelling will be active. 
Any error in the selection of the area is notified to the user using the QGIS message bar.
It is not advised to modify the map CRS once the area has been selected, since this could cause problems with some CRS combinations. 
If a new area is selected while another area is in use, the plugin will ask the user to confirm before overwriting the old area with the new one.

### New area
The area of interest is selected using the center coordinates (in the correct CRS) and the extension of the area in kilometers. Each box must be filled to select an area, and the extension max limits are 99999km x 99999km. In the case that one of the side is smaller than 400 meters, a non-blocking warning will be shown to the user. The Coordinate Reference System of the area is the same as the current CRS of the canvas map, and only CRS with a Meter unit measure are accepted. 

### Load area
To load a previously saved area in the plugin, select the file (in vector format gpk, geojson, shp, ecc...) containing the classification from the file explorer. In this section it is possible to load only files created using this plugin. Even though there are multiple checks to identify wrong files, to avoid any error it is advised to not try loading any other file.
All the modifications applied after loading an area will **not** be applied to the original file.

## Area labelling
For the labelling, three different modes are available: Split, Accept, and Reject. A mode is activated by clicking the correspondent button, and the active mode is visible in the UI, and in the map canvas with different mouse cursors. A mode is active until the button is clicked again, a different plugin mode is selected, or a mouse mode is selected in the QGIS UI (such as Pan Map, Zoom, Select Features, ...). Once a mode is active, all the map clicks in the area of interest will perform the selected action. With the Split mode, the area will split instantly in 4 equal parts, while with Accept and Reject, a description for the area is asked to the user. The description for each area is limited to 254 characters, due to limitations of the Shapefile format. if an area after a splitting will have at least a side shorter than 400 meters, the user is notified with a non-blocking warning.
All the modifications can be reversed using the "Undo action" button. The undo is available for the last 5 actions performed.

## Save layer
To save a classification of an area, select a name for the new layer and click the "Save Layer" button. The new layer will be added to the layer list in the QGIS UI. The layer is only saved in memory and must be exported as a file before closing QGIS to avoid losing it. It is possible to continue modifying the area after saving a layer, and all the modifications will not be applied to the saved layers. 

### Export the layer styling
When a layer is exported to a file, its styling (e.g. colors and borders) is not automatically saved with it. To save the styling as well, follow this steps:
Right click on the layer -> Export -> Save as QGIS Layer Style File -> Save the file with the same name as the exported layer file and in the same folder. 
With this method, if the layer will be opened in QGIS, it will have the same style as in the plugin.
This is not necessary to maintain the style when loading the layer back in the plugin, as the style is applied automatically. 
