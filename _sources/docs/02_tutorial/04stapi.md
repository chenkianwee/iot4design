# Posting to the FROST-Server (Sensorthings API database) using Particle.io Devices
In this tutorial we will go through the steps to write the codes for Particle-based sensor setup. We will be building a SHT31 sensor. The script can be reused as long as the setup is the same with the setup described here, a particle device with one connected SHT31 sensor. For this tutorial we will be needing these materials:
- A Particle Argon (Can be bought [here](https://store.particle.io/products/argon))
- USB Data Cable (Should come with your Particle Argon)
- A SHT31 Sensor (Can be bought [here](https://www.adafruit.com/product/2857))
- Jumper Wires x 4 (Can be bought [here](https://www.adafruit.com/product/1956))
- Breadboard (Can be bought [here](https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img))
- Soldering Kit (Can be bought [here](https://www.amazon.com/Soldering-Iron-Kit-Temperature-Desoldering/dp/B073VDX4B7/ref=sr_1_1_sspa?crid=3TI8MUBYG9QXZ&dchild=1&keywords=soldering+kit&qid=1615313665&s=industrial&sprefix=soldering%2Cindustrial%2C166&sr=1-1-spons&psc=1&smid=A1XLBTH0MIQMMO&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFHUTdTSUtLUkdESUQmZW5jcnlwdGVkSWQ9QTAzODE3MjcyS0REVDQ5U1JLSVk4JmVuY3J5cHRlZEFkSWQ9QTAxMjYzMDYxOTk2N0ZMSjdVUVI2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==))
- Laptop and Smart phone

1. Refer to {doc}`../030/0318subtask18` to register the Argon Device with our Particle account.

2. Wire up the sensor and the Argon as shown in the figure below. For step by step details on how to wire the sensors please refer to **Step 3** of {doc}`0201task01`.
    ```{figure} /_static/0201task01/sht31_6_labelled.jpg
    :width: 100%
    ```
3. Click on this link <a href="https://build.particle.io" target="_blank">build.particle.io</a>. Once you click on the link, you will be directed to the web ide and asked to create a new app. Name it as you wish. I have name it 'NEWAPP'. I will refer to it as 'NEWAPP' throughout this tutorial.
    ```{figure} /_static/0210task10_3/0210task10_3_1.png
    :width: 100%
    ```
4. Search for 'STAPI' at the search bar. You should be able to see the script 'STAPI_Template'.
    ```{figure} /_static/0210task10_3/0210task10_3_2.png
    :width: 100%
    ```
    - Select all (you can use the shortcut key Ctrl-A) and copy (Ctrl-C) the script to your 'NEWAPP'. We are going to use the template as the starting point for writing a new script that post data to our FROST-Server.
    ```{figure} /_static/0210task10_3/0210task10_3_3.png
    :width: 100%
    ```
5. Using the template, you will have make changes to the first 39 lines and lines 52-93 of the code. The first 39 lines of codes are as follows.
    ```
    ====================================================================================================================
    !!! MANDATORY PARAMETERS
    ====================================================================================================================
    String thingDesc = "template"; //DESCRIBE THE DEPLOYMENT
    int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
    ====================================================================================================================
    OPTIONAL PARAMETERS (if the device is already registered, these options are ignored)
    ====================================================================================================================
    //Description of the location
    String foiName = "na"; //THE LOCATION NAME
    String foiDesc = "na";//Define the geometry of the location. Refer to https://tools.ietf.org/html/rfc7946 for geometry types.
    String locType = "Point";
    String enType = "application/vnd.geo+json";
    //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
    float coordx = 0.0; //lon/x
    float coordy = 0.0; //lat/y
    float coordz = 0.0; //elv/z
    ====================================================================================================================
    SENSOR SPECIFIED SETTINGS & LIBRARIES - PLEASE MAKE CHANGES ACCORDING TO YOUR SENSORS
    ====================================================================================================================
    String pins = "i2c-co2sensor"; //describe the pins connection on the particle device
    const int nDs = 3; // how many sensors are attached to this particle device that is streaming single number result
    //Specify the Ids of the sensors that is attached to each datastream
    int dsSnrIds[nDs] = {5,5,5}; // Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Sensors to look at the sensor catalogue, if you can't find the sensors you need run STAPI04-RegisterSensors
    //Specify the Ids of the observation properties that is attached to each datastream
    int dsObsPropIds[nDs] = {5,1,3};// Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/ObservedProperties to look at the observed properties catalogue, if you can't find the observed properties you need run STAPI05-RegisterObservedProperties
    //descriptions of the datastream
    String dsDescs[nDs] = {"co2", "air temp", "rel humidity"};
    String dsObsTypes[nDs] = {"measurement", "measurement", "measurement"};
    //unit of measurement of the data
    String dsUomNames[nDs] = {"parts per million", "degree celsius", "%"}; //name of unit of measurement e.g. temperature, daylight
    String dsUomSyms[nDs] = {"ppm", "degC", "%"}; // the symbols of the unit of measurement e.g. C, lux
    String dsUomDefs[nDs] = {"number of particles per million particles","temperature", "percentage of humidity in the air"}; //visit "http://www.qudt.org/qudt/owl/1.0.0/unit/Instances.html" to get the definition
    ====================================================================================================================
    uint16_t carbonDioxide;
    float temperature;
    float rHumidity;
    //Specify the app that is flashed on the particle device
    String appName = "stapi01_template";
    ```
    - First we need to include the library necessary for SHT31 sensor. Click on the 'Libraries' icon. In the search bar, search for sht31. On the top of the list you will get 'adafruit-sht31'.
    ```{figure} /_static/0210task10_3/0210task10_3_4.png
    :width: 100%
    ```
    - Click on the 'adafruit-sht31' and include it in your code.
    ```{figure} /_static/0210task10_3/0210task10_3_5.png
    :width: 100%
    ```
    - Include it in your 'NEWAPP' code.
    ```{figure} /_static/0210task10_3/0210task10_3_6.png
    :width: 100%
    ```
    ```{figure} /_static/0210task10_3/0210task10_3_7.png
    :width: 100%
    ```
    - The library will be automatically included in your code.
    ```{figure} /_static/0210task10_3/0210task10_3_8.png
    :width: 100%
    ```
    - We will configure this code for our SHT31 sensor. First we change the mandatory parameters.Change the 'thingDesc' to describe your deployment. Change the 'sample_rate' to decide the intervals of acquisition.
    ```
    ====================================================================================================================
    !!! MANDATORY PARAMETERS
    ====================================================================================================================
    String thingDesc = "deployment of sht31 for tutorial"; //DESCRIBE THE DEPLOYMENT
    int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
    ```
    - We can make changes to the optional parameters. You can get the coordinate of the location by using google map. You can follow **step 3&4** of <a href="https://chenkianwee.github.io/gis4design/docs/030/0319task20.html?highlight=coordinate" target="_blank">this guide</a>.
    ```
    ====================================================================================================================
    OPTIONAL PARAMETERS (if the device is already registered, these options are ignored)
    ====================================================================================================================
    //Description of the location
    String foiName = "andlinger center chaos lab"; //THE LOCATION NAME
    String foiDesc = "this is the room where the tutorial is taking place";
    String locType = "Point"; //Define the geometry of the location. Refer to https://tools.ietf.org/html/rfc7946 for geometry types.
    String enType = "application/vnd.geo+json";
    //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
    float coordx = -74.65100728477384; //lon/x
    float coordy = 40.34965958241038; //lat/y
    float coordz = 0.0; //elv/z
    ```
    - Next we will fill in the sensor specified parameters.
    ```
    ====================================================================================================================
    SENSOR SPECIFIED SETTINGS & LIBRARIES - PLEASE MAKE CHANGES ACCORDING TO YOUR SENSORS
    ====================================================================================================================
    String pins = "i2c-sht31"; //describe the pins connection on the particle device
    const int nDs = 3; // how many sensors are attached to this particle device that is streaming single number result
    ```
    - For specifying the sensors and ObservedProperties we will go to the FROST-Server and find the sht31 sensor Id.
    ```
    //Specify the Ids of the sensors that is attached to each datastream
    int dsSnrIds[nDs] = {3,3,3}; // Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Sensors to look at the sensor catalogue, if you can't find the sensors you need run STAPI04-RegisterSensors
    //Specify the Ids of the observation properties that is attached to each datastream
    int dsObsPropIds[nDs] = {1,3,6};// Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/ObservedProperties to look at the observed properties catalogue, if you can't find the observed properties you need run STAPI05-RegisterObservedProperties
    ```
    - Go to <a href="https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Sensors" target="_blank">the sensor url</a>. Search for 'sht31' with the Ctrl-F command. We can see that the sht31 sensor has an ID of 3.
    ```{figure} /_static/0210task10_3/0210task10_3_9.png
    :width: 100%
    ```
    - Similarly for the observedproperties we will go to <a href="https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/ObservedProperties" target="_blank">the observedproperties url</a>. We have 3 datastreams that are measuring the temperature, relative humidity and absolute humidity respectively. We will use the Ctrl-F function to search for these properties. Their ID are 1, 3, 6 respectively.
    ```{figure} /_static/0210task10_3/0210task10_3_10.png
    :width: 100%
    ```
    - Next we need to fill in more information on the datastreams. The descriptions need to be the same order as the way you specify your observedproperties: air temp, relative humidity and absolute humidity.
    ```
    //descriptions of the datastream
    String dsDescs[nDs] = {"air temp", "rel humidity", "abs humidity"};
    String dsObsTypes[nDs] = {"measurement", "measurement", "measurement"};
    //unit of measurement of the data
    String dsUomNames[nDs] = {degree celsius", "percentage", "grams per kg"}; //name of unit of measurement e.g. temperature, daylight
    String dsUomSyms[nDs] = {"degC", "%", "g/kg"}; // the symbols of the unit of measurement e.g. C, lux
    String dsUomDefs[nDs] = {"temperature", "percentage of humidity in the air", "grams of moisture in the air"};
    ====================================================================================================================
    ```
    - Next we will include any extra codes that is required for running the SHT31 sensor. We have to first initialise the SHT31 library.
    ```
    Adafruit_SHT31 sht31 = Adafruit_SHT31();
    ```
    - Determine the data we are acquiring from the sensor. t (temperature), h (rel humidity) and g (absolute humidity).
    ```
    double t;
    double h;
    double g;
    ```
    - As the SHT31 only acquire the air temperature and the relative humidity. We wrote function to calculate the absolute humidty from these two data.
    ```
    //constants for calculating absolute humidity
    double EPSILON = 0.62198;  // ratio of molecular weights of water and dry air
    double P_ATM = 102595.8;   // current barometric pressure, Pa - UPDATE!!!! at time of experiment
    //fit to Magnus equation Psat = C1*exp(A1*t/(B1+t)) where t is in C, outputs Pa
    double A = 17.625; //from Alduchov and Eskridge, 1996
    double B = 243.04; // degrees C
    double C = 610.94; //Pa
    //helper function to compute absolute humidity
    double absolute_H(double tempC, double rh) {
        double Psat = C*exp(A*tempC/(B+tempC));
        double Pvap = rh/100*Psat;
        double ah = EPSILON*Pvap/(P_ATM-Pvap)*1000; //convert to g/kg
        return ah; //absolute humidity in g/kg
    }
    ```
    - Lastly, we specify the script name that will be flashed onto the particle device.
    ```
    //Specify the app that is flashed on the particle device
    String appName = "NEWAPP";
    ```
    - The complete code for first 39 lines are as follows.
    ```
    ============================================================================================
    !!! MANDATORY PARAMETERS
    ============================================================================================
    String thingDesc = "deployment of sht31 for tutorial"; //DESCRIBE THE DEPLOYMENT
    int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
    ============================================================================================
    OPTIONAL PARAMETERS (if the device is already registered, these options are ignored)
    ============================================================================================
    //Description of the location
    String foiName = "andlinger center chaos lab"; //THE LOCATION NAME
    String foiDesc = "this is the room where the tutorial is taking place";
    String locType = "Point"; //Define the geometry of the location. Refer to https://tools.ietf.org/html/rfc7946 for geometry types.
    String enType = "application/vnd.geo+json";
    //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
    float coordx = -74.65100728477384; //lon/x
    float coordy = 40.34965958241038; //lat/y
    float coordz = 0.0; //elv/z
    ============================================================================================
    SENSOR SPECIFIED SETTINGS & LIBRARIES - PLEASE MAKE CHANGES ACCORDING TO YOUR SENSORS
    ============================================================================================
    String pins = "i2c-sht31"; //describe the pins connection on the particle device
    const int nDs = 3; // how many sensors are attached to this particle device that is streaming single number result
    //Specify the Ids of the sensors that is attached to each datastream
    int dsSnrIds[nDs] = {3,3,3}; // Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/Sensors to look at the sensor catalogue, if you can't find the sensors you need run STAPI04-RegisterSensors
    //Specify the Ids of the observation properties that is attached to each datastream
    int dsObsPropIds[nDs] = {1,3,6};// Visit https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/ObservedProperties to look at the observed properties catalogue, if you can't find the observed properties you need run STAPI05-RegisterObservedProperties
    //descriptions of the datastream
    String dsDescs[nDs] = {"air temp", "rel humidity", "abs humidity"};
    String dsObsTypes[nDs] = {"measurement", "measurement", "measurement"};
    //unit of measurement of the data
    String dsUomNames[nDs] = {degree celsius", "percentage", "grams per kg"}; //name of unit of measurement e.g. temperature, daylight
    String dsUomSyms[nDs] = {"degC", "%", "g/kg"}; // the symbols of the unit of measurement e.g. C, lux
    String dsUomDefs[nDs] = {"temperature", "percentage of humidity in the air", "grams of moisture in the air"};
    ===========================================================================================
    Adafruit_SHT31 sht31 = Adafruit_SHT31();
    double t;
    double h;
    double g;
    //constants for calculating absolute humidity
    double EPSILON = 0.62198;  // ratio of molecular weights of water and dry air
    double P_ATM = 102595.8;   // current barometric pressure, Pa - UPDATE!!!! at time of experiment
    //fit to Magnus equation Psat = C1*exp(A1*t/(B1+t)) where t is in C, outputs Pa
    double A = 17.625; //from Alduchov and Eskridge, 1996
    double B = 243.04; // degrees C
    double C = 610.94; //Pa
    //helper function to compute absolute humidity
    double absolute_H(double tempC, double rh) {
        double Psat = C*exp(A*tempC/(B+tempC));
        double Pvap = rh/100*Psat;
        double ah = EPSILON*Pvap/(P_ATM-Pvap)*1000; //convert to g/kg
        return ah; //absolute humidity in g/kg
    }
    //Specify the app that is flashed on the particle device
    String appName = "NEWAPP";
    ```
6. With the Thing and Datastreams registered, we will move on to the setup and loop function of the particle device.
7. In the setup function. We have to add an extra line to start the SHT31 library.
    ```
    //start the sht31 library
    sht31.begin(0x44);
    ```
    - The code below is the completed setup function.
    ```
    void setup() {
        //start the sht31 library
        sht31.begin(0x44);
        //get the device name
        Particle.subscribe("particle/device/name", getDeviceName);
        Particle.publish("particle/device/name");
        //Set the Datastream Ids as variables
        Particle.variable("appName", appName);
        Particle.variable("datastreamId",dsIdString);
    }
    ```
8. In the loop function. You only need to fill in the scope within 'if (thingCnt == -2){}'. We will first change the datastream variables. We will change the datastream variables from dsId_co2, dsId_airTemp and dsId_relHumid to **dsId_airTemp, dsId_relHumid and dsId_absHumid**. We will also change the dsIdString with the right variable names as shown below.  
    ```
    int dsId_airTemp = dsIds[0];
    int dsId_relHumid = dsIds[1];
    int dsId_absHumid = dsIds[2];
    dsIdString = String::format("{ \"%s\" : \"%d\", \"%s\" : \"%d\", \"%s\" : \"%d\" }",
                                "dsId_airTemp",  dsId_airTemp, "dsId_relHumid", dsId_relHumid, "dsId_absHumid", dsId_absHumid);
    ```
    - Next we will change the codes below the '//get the reading from the sensor' comment. We will get the air temperature, relative humidity and absolute humidity with the following codes.
    ```
    //get the reading from the sensor
    t = double(sht31.readTemperature());
    h = double(sht31.readHumidity());
    float tF = (t* 9) /5 + 32;
    g = absolute_H(t,h);
    ```
    - Once we have the data from the sensors we have to publish them and trigger the 'postObservation' webhook by publishing with the event name 'postObservation'. The data is posted to the FROST-Server with the following code. In each post you have specify the time, the acquired data and the id of the datastream to post to. After each publish I have added in a 'delay(sample_rate/3)'. This is to give each publish some time to be publish and trigger the respective webhook. It is good practice to give some delay between publish statements.
    ```
    //post and publish the readings from the first sensor
    String postObsTemp = String::format(
    "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
    timeNow.c_str(), t, dsId_airTemp);
    Particle.publish("postObservation", postObsTemp, PRIVATE);
    delay(sample_rate/3);

    //post and publish the readings from the first sensor
    String postObsHumid = String::format(
    "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
    timeNow.c_str(), h, dsId_relHumid);
    Particle.publish("postObservation", postObsHumid, PRIVATE);
    delay(sample_rate/3);

    //post and publish the readings from the first sensor
    String postObsAbsHumid = String::format(
    "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
    timeNow.c_str(), g, dsId_absHumid);
    Particle.publish("postObservation", postObsAbsHumid, PRIVATE);

    delay(sample_rate/3);
    ```
    - the complete code of the setup and loop function codes are as follows.
    ```
    void setup() {
          //start the sht31 library
          sht31.begin(0x44);
          //get the device name
          Particle.subscribe("particle/device/name", getDeviceName);
          Particle.publish("particle/device/name");
          //Set the Datastream Ids as variables
          Particle.variable("appName", appName);
          Particle.variable("datastreamId",dsIdString);
      }
      void loop() {
          if (thingCnt == -2) {
              Particle.unsubscribe();
              //specify which datastream to post to
              int dsId_airTemp = dsIds[0];
              int dsId_relHumid = dsIds[1];
              int dsId_absHumid = dsIds[2];
              dsIdString = String::format("{ \"%s\" : \"%d\", \"%s\" : \"%d\", \"%s\" : \"%d\" }",
                                          "dsId_airTemp",  dsId_airTemp, "dsId_relHumid", dsId_relHumid, "dsId_absHumid", dsId_absHumid);
              //get the current time
              String timeNow = Time.format(Time.now(), TIME_FORMAT_ISO8601_FULL);

              t = double(sht31.readTemperature());
              h = double(sht31.readHumidity());
              g = absolute_H(t,h);

              //post and publish the readings from the first sensor
              String postObsTemp = String::format(
              "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
              timeNow.c_str(), t, dsId_airTemp);
              Particle.publish("postObservation", postObsTemp, PRIVATE);
              delay(sample_rate/3);

              //post and publish the readings from the first sensor
              String postObsHumid = String::format(
              "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
              timeNow.c_str(), h, dsId_relHumid);
              Particle.publish("postObservation", postObsHumid, PRIVATE);
              delay(sample_rate/3);

              //post and publish the readings from the first sensor
              String postObsAbsHumid = String::format(
              "{ \"time\" : \"%s\", \"result\": \"%f\", \"dsId\": \"%d\"}",
              timeNow.c_str(), g, dsId_absHumid);
              Particle.publish("postObservation", postObsAbsHumid, PRIVATE);

              delay(sample_rate/3);
          }
    ```
9. Once you have made the necessary changes to the template. Save the script (Ctrl+S or click on the save icon on the left sidebar). Click on the device tab and choose the device to flash to.
    ```{figure} /_static/0210task10_3/0210task10_3_11.png
    :width: 100%
    ```
10. You can first verify the code by clicking on the tick icon. If there are no mistakes you can flash it onto the device by clicking on the lightning icon.
    ```{figure} /_static/0210task10_3/0210task10_3_12.png
    :width: 100%
    ```
11. Go to the console page (<a href="https://console.particle.io/devices" target="_blank">https://console.particle.io/devices</a>). Click on the device that you flash the script on. If everything is successful, the sensor will be posting data according to the sample time.
    ```{figure} /_static/0210task10_3/0210task10_3_13.png
    :width: 100%
    ```
12. On the console page you can click on get variable to see what app is flashed to the device and also the datastream id it is posting to.
    ```{figure} /_static/0210task10_3/0210task10_3_14.png
    :width: 100%
    ```
13. Refer to  {doc}`../030/0319subtask19` to visualize the data on Grafana.

14. This script can be reused for the same setup **Particle device + 1 SHT31 sensor**. If you want to register a new entry with the same Particle device, you just need to change the deployment parameter. The script always looks for Thing with the same name, device uid and deployment. Only if the database has a thing with the same name, device uid and deployment, it will return the id of the Thing, if not found the script will register a new Thing entry.  
