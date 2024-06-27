# Chaos Database Tutorial 2 - REST-based Sensorthings API
You can refer to <a href="https://developers.sensorup.com/docs/#sensorthingsAPISensing" target="_blank">this webpage</a> for the full Sensorthings API documentation.

1. If you know the id of the Thing you can do a GET request on the browser and get the data. Input the following url into your browser. The request will return the specified Thing with the id=1.
    ```
    https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Things(1)
    ```
2. Now let's post a new Thing to the database using the in-built http tool of FROST-Server. Go to <a href="https://andlchaos300l.princeton.edu:8080/FROST-Server/" target="_blank">https://andlchaos300l.princeton.edu:8080/FROST-Server/</a>. Input the following JSON string into the text box under the HTTP Tool. Make sure to set the action to POST with the drop down list and the 'To URL' is set to 'v1.0/Things' as shown in the figure below. You will be prompted for username and password.
    ```
    {
      "name": "Temperature Monitoring System",
      "description": "Sensor system monitoring area temperature",
      "properties": {
        "Deployment Condition": "Deployed in a third floor balcony",
        "Case Used": "Radiation shield"
      }
    }
    ```
    ```{figure} /_static/0210task10_2/0210task102_1.png
    :width: 100%
    ```
    - Once you click on execute you will get a Done message at the bottom. You can see the new Thing you have created and its Id. We can look at it by using the return url with your browser.
    ```{figure} /_static/0210task10_2/0210task102_2.png
    :width: 100%
    ```
    - Enter the URL into the browser and you can see the newly created Thing.
    ```{figure} /_static/0210task10_2/0210task102_3.png
    :width: 100%
    ```
3. Now I can change the description of the Thing by specifying the change with the following String. Change the action to Patch and the url to 'v1.0/Things(110)'. Click Execute.
    ```
    {
      "description": "I am changing the description"
    }
    ```
    ```{figure} /_static/0210task10_2/0210task102_4.png
    :width: 100%
    ```
    - We can go check if the description is changed by making a get request of the Thing with its id.
    ```{figure} /_static/0210task10_2/0210task102_5.png
    :width: 100%
    ```
4. We can query this Thing with a GET request and the filter statement as follows. The query is asking for a Thing with the name 'Temperature Monitoring System' and description 'I am changing the description'.
    ```
    https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Things?$filter=name eq 'Temperature Monitoring System' and description eq 'I am changing the description'
    ```
    ```{figure} /_static/0210task10_2/0210task102_6.png
    :width: 100%
    ```
5. Now we can delete this dummy thing that we have created with the following. Change the action to Delete and the url to 'v1.0/Things($id of the created thing)'
    ```{figure} /_static/0210task10_2/0210task102_7.png
    :width: 100%
    ```
6. For a full set of API please refer to <a href="https://developers.sensorup.com/docs/#sensorthingsAPISensing" target="_blank">this webpage</a>.

7. Now that we have an idea of how the REST API works. We can move on to posting data with real sensors and microcontroller.
