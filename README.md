# PyQGIS Tutorial

This tutorial serves as an introduction to both QGIS and the use of Python scripting within the QGIS platform. It was developed as a final project for IDCE 30274 Computer Programming for GIS taught by Professor Shadrock Roberts at Clark University in Fall 2020. Questions, comments, and suggestions should be directed to Jess Strzempko either at JeStrzempko@clarku.edu or JessStrzempko@gmail.com. Her GitHub profile can be found [here](https://github.com/jstrzempko). 

### Objectives

* To introduce users to the use of Python scripting in QGIS
* To promote the use of open source software through a demonstration of its capabilities
* To explore the ACLED US Crisis Monitor dataset

### Data

Data for this tutorial is sourced from [ACLED](acleddata.com), the Armed Conflict Location & Event Data Project. ACLED is a registered non-profit organization with 501(c)(3) status operating in the United States that compiles spatial and attribute data on worldwide crises. These include political violence, civil and communal conflicts, violence against civilians, remote violence, rioting, and protesting. ACLED has [teams of research analysts](https://acleddata.com/about-acled/) that collect, analyze, and map events in these regions: Africa, East Asia, South Asia, Southeast Asia, the Middle East, Central Asia and the Caucasus, Latin America and the Caribbean, and Southeastern and Eastern Europe and the Balkans. 

In addition to location data, disaggregated information on the dates, actors, fatalities, and types of conflict is gathered and verified through media outlets. Decisionmaking and documentation behind the methodology can be found [here](https://acleddata.com/resources/methodology/). This tutorial will specifically be using data from the [US Crisis Monitor](https://acleddata.com/special-projects/us-crisis-monitor/), a new project begun by ACLED in 2020 in response to increased domestic civil unrest following the murder of [George Floyd](https://en.wikipedia.org/wiki/George_Floyd) by Minneapolis police. In collaboration with the Bridging Divides Initiative (BDI) at Princeton University, ACLED launched the US Crisis Monitor to support and empower local communities through access to real-time evidence of demonstrations, protesting and violence. Nowadays, Americans are faced with an insidious combination of [white supremacist extremism](https://www.theguardian.com/australia-news/audio/2020/nov/03/us-election-2020-trump-and-the-rise-of-white-supremacist-extremism) and [political partisanship](https://www.cbsnews.com/news/second-stimulus-check-status-update-2020-11-24/) exacerbated by a global pandemic and fascist president. The US data ACLED gathers and shares aims to provide communities with useful information on risks, conflict hotspots, and resources needed to keep community members safe and healthy. 

Both the data and analysis performed by ACLED is free for use, which is why we will be employing it in this tutorial. The outputs are merely educational and exploratory and should not be treated as academically rigorous results. Use of ACLED data for research should involve a [critical examination of the quality and methodology](https://journals.sagepub.com/doi/abs/10.1177/0010836711434463) behind the data collection and analysis, with an eye toward biased findings and reliance on media sources. Comments and questions about the ACLED dataset should be directed toward admin@acleddata.com. 

![](images/download_acled.PNG)

Data should be downloaded from [the US Crisis Monitor site](https://acleddata.com/special-projects/us-crisis-monitor/). It should then be opened in Excel and saved as a CSV UTF-8 (Comma Delimited) (`.csv`) file for ease of use with QGIS (and other software). Should problems arise, a back-up version of the `.csv` file is provided in the data folder within this repository. 

## Tutorial Steps

### Downloading QGIS 

QGIS can be downloaded for free from the [QGIS website](download.qgis.org). This tutorial will explain some points of confusion surrounding the process, but assumes users have previous experience downloading programs to their personal computers. QGIS can be downloaded for Windows, MacOS X, Linux, BDS, and Android. This tutorial will focus on a Windows downloads. Assistance with other operating systems can be found on the [QGIS Installers page](https://qgis.org/en/site/forusers/alldownloads.html). 

![](images/download_qgis.PNG)

The first question that arises when downloading QGIS is - what is OSGeo4W? A [nice and quick explanation](https://gis.stackexchange.com/questions/164976/what-is-osgeo4w) of OSGeo and OSGeo4W can be found by StackExchange user HeikkiVesanto. To paraphrase, OSGeo, [The Open Source Geospatial Foundation](https://www.osgeo.org/) supports open source GIS projects like QGIS, GeoServer, and OpenLayers, offering legitimacy and quality assurance. OSGeo4W is a Windows installer for Open Source GIS projects. It keeps track of the dependencies (reliance of one piece of software on another) of Open Source GIS packages, ensuring that one install of programs like Python, GDAL, or GRASS can be shared among softwares. It also maintains software versions so you can easily upgrade programs. 

I would recommend downloading using OSGeo4W if you intend to perform further GIS/programming work on your personal computer. Having dependencies already installed can be incredibly useful in the future and save time and energy (and prevent frustration). However, if you feel that your foray into Open Source GIS will be limited, I would suggest downloading using the QGIS Standalone Installer. Choice of 32 vs 64 bit depends on [what processor](https://www.techsoup.org/Support/articles-and-how-tos/do-i-need-the-32bit-or-64bit) your personal computer has. I would recommend downloading the 64-bit since most modern personal computers have 64-bit processors, but if you are concerned you should check. 

**<p align="center"> After downloading OSGeo4W from the above website, open the OSGeo4W Net Release Setup Program and you should see the below screen. Select Advanced Install then Next. </p>**

![](images/osgeo4w_setup.PNG)

**<p align="center"> We will be downloading from the internet, so ensure you have a strong wifi connection before performing the below steps. Choose Install from Internet then Next. </p>**

![](images/osgeo4w_setup2.PNG)

**<p align="center"> Choose the Installation Directory. I typically leave the Root Directory as the default and opt to add an icon on both my Desktop and Start Menu. </p>**

![](images/osgeo4w_setup3.PNG)

**<p align="center"> Select Local Package Directory. Again, leaving this as the default option is a good decision. </p>**

![](images/osgeo4w_setup4.PNG)

**<p align="center"> Select your Internet Connection type. Most often, this will be Direct Connection. </p>**

![](images/osgeo4w_setup5.PNG)

**<p align="center"> Choose a download site. I generally select one of the OSGeo ones. </p>**

![](images/osgeo4w_setup6.PNG)

**<p align="center"> Here, you will select the packages to install. As you can see in the below screenshot, I have version 3.12.3-1 of QGIS already installed, but can update to 3.16.0-1 by hitting Skip next to the Package name to change the action performed. Do this for qgis: QGIS Desktop. Don't worry about dependencies right now and ddon’t blindly do a full install of available packages. Select Next. </p>**

![](images/osgeo4w_setup7.PNG)

**<p align="center"> Here are the dependencies! OSGeo4W will resolve them for you by installing them at the same time. If these components are not installed, your QGIS copy will be rendered unusable. Ensure the box to install them is selected at the bottom of the page. </p>**

![](images/osgeo4w_setup8.PNG)

**<p align="center"> Now, when you go to your start menu and type QGIS you should see the QGIS 3 App! Select it to get started. </p>**

![](images/qgis_startmennu.PNG)

### PyQGIS

Once you have opened QGIS, explore the menu and buttons. The user interface is very similar to that of ArcMap. If you would like to get familiar with the software and explore its capabilities, I suggest following along with [another tutorial](https://www.youtube.com/watch?v=kCnNWyl9qSE&vl=en). Open the Python Console by either clicking the toolbar button, as is shown in the screenshot below, or by going to Plugins > Python Console in the top ribbon. 

![](images/qgis_pythonconsole.PNG)

Similar to the way `import arcpy` is run automatically when the Python console is opened in ArcMap, the following statements are executed in the QGIS Python console as an initial default.  

```
from qgis.core import *
import qgis.utils
```

**Setting Path Name**

![](file_location.PNG)

![](show_editor.PNG)

Console vs. Editor

Open the USA_2020_Nov21.csv file you have downloaded from the US Crisis Monitor site, take note of the LONGITUDE and LATITUDE fields
os.getcwd()
to get the current working directory

how to construct:

example

path1 = "file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?type=csv&xField=LONGITUDE&yField=LATITUDE&crs=EPSG:3857"
path2 = "file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?delimiter=,&xField=LONGITUDE&yField=LATITUDE&crs=EPSG:3857"
path3 = "file:///{}/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?delimiter={}&xField={}&yField={}".format(os.getcwd(), ",", "LONGITUDE", "LATITUDE")

path = "file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?delimiter=,&xField=LONGITUDE&yField=LATITUDE"

path = "file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?delimiter=,&xField=LONGITUDE&yField=LATITUDE&crs=EPSG:3857"

Open the USA_2020_Nov21.csv file you have downloaded from the US Crisis Monitor site, take note of the LONGITUDE and LATITUDE fields

Layer > Add Layer > Add Delimited Text Layer
File name: USA_2020_Nov21
File format: CSV
Leave everything else as default

Right click > Properties
Information
Information from Provider
Right click path > Copy Link Location
Go to file location in computer (where you have saved it), right click Properties
Location will give the file path starting from the drive that you can copy and use in the next exercise

for example, mine would be 
path = "file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?type=csv&xField=LONGITUDE&yField=LATITUDE&crs=EPSG:3857
file:// is needed before the path to the csv file we want

EPSG3857 The most common CRS for online maps, used by almost all free and commercial tile providers. Uses Spherical Mercator projection.

Source
file:///C:/Users/jas36/Documents/Clark/Year%205/Comp_Prog/Class_Materials/Final/USA_2020_Nov21.csv?type=csv&maxFields=10000&detectTypes=yes&xField=LONGITUDE&yField=LATITUDE&crs=EPSG:3857&spatialIndex=no&subsetIndex=no&watchFile=no

CSV or other delimited text files — to open a file with a semicolon as a delimiter, with field “x” for X coordinate and field “y” for Y coordinate you would use something like this:

uri = "file://{}/testdata/delimited_xy.csv?delimiter={}&xField={}&yField={}".format(os.getcwd(), ";", "x", "y")
vlayer = QgsVectorLayer(uri, "layer name you like", "delimitedtext")
QgsProject.instance().addMapLayer(vlayer)

uri = "elevp.csv?delimiter=%s&xField=%s&yField=%s&elevField=%s" % (";","x","y","elev")

Every time QGIS starts, the user’s Python home directory
    Linux: .local/share/QGIS/QGIS3
    Windows: AppData\Roaming\QGIS\QGIS3
    macOS: Library/Application Support/QGIS/QGIS3

from qgis.core import 

```
# get the path to the shapefile e.g. /home/project/data/ports.shp
path_to_airports_layer = "testdata/airports.shp"

# The format is:
# vlayer = QgsVectorLayer(data_source, layer_name, provider_name)

vlayer = QgsVectorLayer(path_to_airports_layer, "Airports layer", "ogr")
if not vlayer.isValid():
    print("Layer failed to load!")
else:
    QgsProject.instance().addMapLayer(vlayer)
```

### Credits

[PyQGIS 101](https://anitagraser.com/pyqgis-101-introduction-to-qgis-python-programming-for-non-programmers/)
