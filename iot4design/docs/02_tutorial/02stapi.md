# Chaos Database Tutorial 1 - Sensorthings API data model
1. The UML diagram of the sensorthings data model is shown below. The API consist of 9 objects, in the figure below there are only 8 objects as it is not depicting the multidatastream object. The multidatastream object is very similar to the datastream object.
    ```{figure} /_static/0210task10_1/0210task101_1.png
    :width: 100%
    OGC Sensorthings API standard working group, CC BY-SA 4.0 <https://creativecommons.org/licenses/by-sa/4.0>, via Wikimedia Commons
    ```
2. To put this data model in context, we will instantiate the model with a typical setup in our lab as shown in the figure below.
    ```{figure} /_static/0210task10_1/0210task101_3.png
    :width: 100%
    OGC Sensorthings API standard working group, CC BY-SA 4.0 <https://creativecommons.org/licenses/by-sa/4.0>, via Wikimedia Commons
    ```
3. You can access the database by going to <a href="https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0" target="_blank">https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0</a>. We are using the FROST-Server sensorthings api implementation. If you are using Firefox browser. The page will be rendered as follows. You can click on the links to access the objects.
    ```{figure} /_static/0210task10_1/0210task101_4.png
    :width: 100%
    ```
4. If you are using a Chrome-based browser, the page is rendered in its raw format and you won't be able to click on the links. Please install the JSONview extension to be able to view the json in your chrome browser. Install it <a href="https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en" target="_blank">here</a>  
    ```{figure} /_static/0210task10_1/0210task101_5.png
    :width: 100%
    ```
5. You can explore how the sensorthings api objects are linked to each other with the browser interface. Click on the url under "Things" object. You will be directed to a page listing the first 100 Things registered on the database.
    ```{figure} /_static/0210task10_1/0210task101_6.png
    :width: 100%
    ```
    - Zooming into the the first Thing on the list we can see that each thing has a series of attributes like : description, id, name, properties, location, multidatastream, historical location, datastreams, tasking capabilities.
        ```{figure} /_static/0210task10_1/0210task101_7.png
        :width: 100%
        ```
    - We can click on the location URL. You will be directed to the Location object linked to the this Thing. You can see that this Thing is located in the Arch Lab. The location is further specified with its GPS location in Lat Lon.
        ```{figure} /_static/0210task10_1/0210task101_8.png
        :width: 100%
        ```
    - Next click on the Multidatastreams URL. You will be directed to the Multidatastream objects associated with this Thing. In this case, this Thing has no multidatastreams.
        ```{figure} /_static/0210task10_1/0210task101_9.png
        :width: 100%
        ```
    - Next click on the HistoricalLocation URL. You will be directed to the HistoricalLocation objects associated with this Thing. In this case, this Thing has only 1 historical location, which is its current location. We have not change its location before.
        ```{figure} /_static/0210task10_1/0210task101_10.png
        :width: 100%
        ```
    - Next click on the Datastreams URL. You will be directed to the Datastreams objects associated with this Thing. In this case, this Thing has 5 datastreams.
        ```{figure} /_static/0210task10_1/0210task101_11.png
        :width: 100%
        ```
    - Zooming into the the first datastream named "CHAOS_PH045_manifold1_return_cold", we can see the meta data of the datastream. What it is observing , the unit of measurement etc. If you clicked on the Sensor URL you can see the sensors that is acquiring the data. It is a thermistor, you can further explore the datasheet of the sensor if you click on the url to its metadata.
        ```{figure} /_static/0210task10_1/0210task101_12.png
        :width: 100%
        ```
    - Going back to the datastream page. You can further explore what is the datastream observing by clicking on the observedproperty url. In this case, the thermistor is returning a temperature reading.
        ```{figure} /_static/0210task10_1/0210task101_13.png
        :width: 100%
        ```
6. Now that you have an idea of the data model of the sensorthings api. We will move on to the next exercise to write some filter api to search for sensors.
