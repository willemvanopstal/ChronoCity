## Demo
A functional online demo can be found at: www.chronocity.net
_(29-6-2017)_  

Before executing a change detection, make sure the service is running by browsing to www.chronocity.net:12839/test  

## Demo video  
A demo video can be found at: https://www.youtube.com/watch?v=lqZBHaU7G08

# ChronoCity Installation

__Installation__  

1. Install a (local) webserver. E.g. Apache Tomcat
2. Install all Python dependencies (see next section)
3. Download this entire repositery as .zip
4. Extract the zip into your webserver-webapps directory. Make sure the paths look like: <code>webapps/OPCM/chronocity-engine/..</code> and <code>webapps/OPCM/chronocity-viewer/..</code>
5. Download the AHN datasets in potree-structure here: https://wvanopstal.stackstorage.com/s/n4FTmxSEaJ6avrp
6. Extract the two folders <code>AHN2</code> and <code>AHN3</code> and put them both under <code>chronocity-viewer/pointclouds/</code>
7. Download the pre-processed difference-layers here: https://wvanopstal.stackstorage.com/s/qEvkj1lgwUksYEK
8. Extract <code>AHN2-AHN3</code>, <code>AHN3-AHN2</code> and <code>Clips</code>
9. Put both <code>AHN2-AHN3</code>, <code>AHN3-AHN2</code> under <code>chronocity-viewer/pointclouds/</code>. (next to AHN2 and AHN3)
10. Download and extract the <code>Clips</code> folder here: https://wvanopstal.stackstorage.com/s/DhTwM4Fm6Di5yWw
11. Put the contents in <code>Clips</code> under <code>chronocity-engine/Clips</code>. It should now contain 4 files.
12. Get a LAStools license-file (.txt) and save it under <code>chronocity-engine/Tools/LAS_tools</code>
13. The ChronoCity-viewer is ready to view. You can access it through your webserver and browse to <code>domain:port/OPCM/</code>

__Python Dependencies__  

For the server-side running correctly, you should also make sure you have the following dependencies installed on your Python interpreter;
- fiona
- laspy
- flask
- copy
- os
- json
- multiprocessing
- time
- shutil
- shapely

__Setup__

1. In <code>/OPCM/chronocity-engine/server_service.py</code> at the bottom you should replace the two paths <code> serv_path</code> and <code>potree_path</code> with the path to the two installations folders like below. Be aware of the double '\\' ! The server listens to port _12839_ by default, but you can specify it yourself if needed.


        port = 12839
        serv_path = "C:\\geo1007\\apache-tomcat-8.5.14\\webapps\\OPCM\\chronocity-engine\\"
        potree_path = "C:\\geo1007\\apache-tomcat-8.5.14\\webapps\\OPCM\\chronocity-viewer\\"

2. Run the <code>server_service.py</code> to start the server. You can test if it is running correctly by browsing to <code>localhost:12839/test</code> in your browser. It will return the message _ACTIVE_ if it is running.

3. The viewer runs on port _8080_ by default and relies on the default value for the server-side. If you have changed the default port, you should edit <code>OPCM/chronocity-viewer/build/potree/potree.js</code> and search for _localhost:_. Replace the entries with your custom ports.

__Console controls__  

All important interactions can be done within the GUI. There are also some other usefull command for more control. You can use these in your browser's webconsole;

    getActivePC();                     # returns a list of the visible pointclouds [AHN2, AHN3, AHN23, AHN32]
    checkLayers(bool,bool,bool,bool)   # sets the visibility for all layers (AHN2, AHN3, AHN23, AHN32)
    toggleAHN()                        # toggles the view between AHN2 and AHN3
    saveAsImage()                      # saves the current view as a .png image (prompt)
    viewer.setPointSizing('Adaptive')   # sets dynamic point sizing; points on foregrond appear bigger
    viewer.setPointSizing('Attenuated') # sets dynamic point sizing; point on foregrond appear smaller
    viewer.setPointSizing('Fixed')      # sets static point sizing; default
    
# ChronoCity Usage 

The application is built to be as intuitive as possible, hopefully you can get along with it right away. If not, this section will guide you through some main functionalities.

## Overview  

The application can be divided in three main parts: the viewport, sidebar and overview-map. The viewport is where the actual data is shown and where you should use your mouse or arrow-keys to navigate around. The sidebar is where you can find all settings and information. The sidebar is hidden by default, you can show it by clicking the menu-icon on the top-left. Below the menu-icon is the map-toggle. By clicking this, the overview-map is shown on which you can see the current orientation of the camera.  

## Sidebar  

The side bar is split up in two sections; the upper part with blue icons contains the general settings and information. The lower part indicated with orange icons contains all available modules in which you can use different tools and analyses. We'll go over the various options very briefly below;

## Navigation  

The navigation panel shows information about the camera position in the coordinates of the loaded dataset. Under 'Controls' you can use different types of navigation-modes (left three icons). For the different effects, select one and use the buttons on the mouse to et acquinted with the different options. The four icons on the right gives you some quick options to view the entire dataset in the viewport, or flies to an orthogonal view.  

## Display settings 

Within the display panel you'll have control over the visual appearance of the points in the viewport. The three options speak for themself, but it has to be noted the 'Point Budget' has great influence on the computers' performance. If you experience any troubles while loading points lower this amount and you'll be fine. The colouring section gives you control over the colors of the points. There are a few options available to color them along their information, or just geometries.  

## Data

Within the data panel you can currently toggle between two different datasets, AHN2 and AHN3. If the dataset is classified according to the ASPRS LAS format, you can also choose which classes you'd like to see or not. This has effect on both datasets.  

## Measurement tools  

This panel contains some basic measurement tools like distance, angles, volumes and profiles. On clicking an icon, you should hover your pointer over the viewport to specify the characteristics. The results-section shows you information on the measurement and you can also delete them one-by-one again. There's also the option to delete all available measurements by clicking the red 'x'.  

## Change Detection  

The change detection panel guides you through the analyses. You can also check the already processed areas by enabling 'Show changes'. You can also specify a region of interest yourself. After clicking 'Run analysis', the algorithm will proces the data in the background. You can just go on with exploring and will be automatically redirected to the region of interest after completion. When the changes are shown, you can also specify which data you'd like to see. Best combinations are New Points + t1 and Removed Points + t2.  

## Download and Export  

In this experimental module you can save an image of the current viewport as .png. This is experimental and is not yet supported by all browsers. Work in progress! You can also download the original data tiles, but needs some more work in this stage. If you really want to download the tiles, go to the overview-map and press the small 'D'-button.  

## Share your view   

In this module you can generate a shareable link which you can send to your friends. The process is straightforward, you just need to press the button and copy the link.  

## Search and Go  

This experimental module can be used for quickly navigating through your data. Suggestions are not yet implemented, so keep it simple like clear postal codes. While streetnames can be used in various cities, it is not yet known to which one you'll be sent!
