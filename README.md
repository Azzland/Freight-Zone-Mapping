# Freight-Zone-Mapping

# Objective

Create a PDF of each of the freight zones in the Greater Perth Region for the company I work for as a freight dockhand, using QGIS and PyQGIS. 

# Equipment/Software

- QGIS 3.14
- Python 3.8

# Process

I completed an Udemy short course titled Automated GIS Workflows with PyQGIS (Packt Publishing) in 2018. I am utilising and building on the skills used from this course and my current Python skills to create a program that automates the process of creating shapefiles and PDF maps of for each freight zone and the localities within them. 
A geojson file containing all the suburb boundaries in Western Australia was downloaded from www.data.gov.au. In QGIS I selected all the suburb polygons in and around the Greater Perth, Northam, Toodyay, York and Mandurah areas. I copied and pasted them into a new shapefile and saved it. I downloaded a shapefile for all water bodies in Western Australia. I identified and selected the polygons containing the estuaries of the Swan River, Canning River, Peel Inlet and the Harvey Estuary. These were copied and pasted into a new layer, and saved as a new shapefile. The boundaries of the suburbs were clipped using the estuary layer to remove any suburb boundaries overlapping the water body boundaries. 

There are a few suburbs that are located in multiple zones so the suburb polygons had to be split manually and accordingly, using an Open Street Maps basemap as reference for accurately tracing the split lines. The polygon containing West Perth was split along the Mitchell and Farmer Freeways as the area to the north (renamed as West Perth North) is in a different zone. The boundary for Perth City was split along the railway line in similar fashion (a polygon called Perth North created). The part of Midland containing Clayton Street was split off from the Midland polygon. Osborne Park was split into three to create a polygon bounding all the businesses along Scarborough Beach Road, as this is part of a different zone. The new shapefile was saved and used as the input suburb shapefile for the program. 

The following modules were imported
    • QtGui (from qgis.PyQt)
    • math
    • os

The following functions were created
    • checkspellings(wordtocheck, WordList)
    • addfilestomap(suburbs)
    • modifysuburblayer(suburb_layer, zone_details, output_folder)
    • createmapshapefiles(output_folder, zone_names, suburbs_with_zone_attribute)
    • createmaps(canvas, output_folder, zone_boundary, suburbs_within_zone , zone_names, label_attribute, all_suburbs_by_zone)

The class ClickBox(QWidget) was created for the program GUI. 

The function addfilestomap adds the input layer and the Open Street Map basemap to the canvas and returns the details opf the suburb layer for editing in the modifysuburblayer function. In this function using a text file showing the list of all freight zones with the list of localities underneath each freight zone the suburb layer is editied to add a new attribute to store the zone names for each suburb feature and remove any uneccesary attributes and saves the layer as a new layer which is used to create the shapefiles for each freight zone using function createmapshapefiles. Here for each freight zone a shapefile showing the zone bnoundaries and a shapefile showing all the boundaries for each locality in the zone are created. These shapefiles are used for creating the maps in the function createmaps which takes in details of all freight zones and the suburbs within them as well as the column position of the suburb names to be labelled in the attribute table for the suburb layer crerated from modifysuburblayer. Createmaps saves a PDF file for each freightzone map showing the outer zone boundary and suburb boundaries and labels within the freight zone, formatted according to commands within the function. The map scales and frame shape, size and orientation (landscape or portrait) vary according to the size and shape of the freight zone.

The ClickBox contains the GUI the user can use in QGIS when running the code. It requests for the suburb shapefile, the textfile containing the list of all freight zones along with the list of suburbs within each freight zone and the output folder to store all output shapefiles and PDF maps. 

More is detailed in the Documentation. 
