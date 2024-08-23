# Grove - EC & PH Sensor Kit with Particle Photons

This the sensor we are going to build in this exercise.

```{figure} /_static/0207task07/027task7_1.jpg
:width: 50%
```

This guide is based on these materials:
- Grove - EC Sensor Kit
    - <a href="https://wiki.seeedstudio.com/Grove-EC-Sensor-kit/" target="_blank">source 1</a>

- Grove - PH Sensor Kit (E-201C-Blue)
    - <a href="https://wiki.seeedstudio.com/Grove-PH-Sensor-kit/" target="_blank">source 2</a>

We will need the following hardwares:
- A Particle Argon (Can be bought <a href="https://store.particle.io/products/argon" target="_blank">here</a>)
- USB Data Cable
- Grove - EC Sensor Kit (Can be bought <a href="https://www.seeedstudio.com/Grove-EC-Sensor-Kit-DJS-1C-Black-p-4576.html" target="_blank">here</a>)
- Grove - PH Sensor Kit (E-201C-Blue) (Can be bought <a href="https://www.seeedstudio.com/Grove-PH-Sensor-Kit-E-201C-Blue-p-4577.html" target="_blank">here</a>)
- Grove Shield FeatherWing for Particle Mesh and all Feathers (Can be bought <a href="https://www.adafruit.com/product/4309" target="_blank">here</a>)
- Jumper Wires x 4 (Can be bought <a href="https://www.adafruit.com/product/1956" target="_blank">here</a>)
- Breadboard (Can be bought <a href="https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img" target="_blank">here</a>)
- Soldering Kit (Can be bought <a href="https://www.amazon.com/Soldering-Iron-Kit-Temperature-Desoldering/dp/B073VDX4B7/ref=sr_1_1_sspa?crid=3TI8MUBYG9QXZ&dchild=1&keywords=soldering+kit&qid=1615313665&s=industrial&sprefix=soldering%2Cindustrial%2C166&sr=1-1-spons&psc=1&smid=A1XLBTH0MIQMMO&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFHUTdTSUtLUkdESUQmZW5jcnlwdGVkSWQ9QTAzODE3MjcyS0REVDQ5U1JLSVk4JmVuY3J5cHRlZEFkSWQ9QTAxMjYzMDYxOTk2N0ZMSjdVUVI2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==" target="_blank">here</a>)
- Laptop or Computer

1. Connect the Argon, Grove shield, Grove - EC Sensor and Grove - PH Sensor as shown. The EC sensor to the A0 connector and the PH Sensor to the A2 connector.
    </Br><Br/>
      ```{figure} /_static/0207task07/027task7_2.jpg
      :width: 100%
      ```

2. Refer to {doc}`../030/0318subtask18` to register the Argon Device with our Particle account.

3. Flash the script **'STAPI_1_PH_1_EC'** to the Argon. Fill in the mandatory parameters accordingly. You can choose to leave the optional parameters to their default values.
    ```
    =============================================================================================
    !!! MANDATORY PARAMETERS
    =============================================================================================
    String thingDesc = "water quality of greenhouse"; //DESCRIBE THE DEPLOYMENT
    int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
    =============================================================================================
    OPTIONAL PARAMETERS
    (this parameters only works when it is the first time registration of the device)
    (if the device is already registered, these options are ignored)
    =============================================================================================
    //Description of the location
    String foiName = "na"; //THE LOCATION NAME
    String foiDesc = "na";
    //Define the geometry of the location. Geometry types from geojson is accepted. Refer to https://tools.ietf.org/html/rfc7946 for geometry types.
    String locType = "Point";
    String enType = "application/vnd.geo+json";
    //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
    float coordx = 0.0; //lon/x
    float coordy = 0.0; //lat/y
    float coordz = 0.0; //elv/z
    ```
4. Refer to  {doc}`../030/0319subtask19` to visualize the data on Grafana.

5. Calibrate the sensors according to the guide.
    - <a href="https://wiki.seeedstudio.com/Grove-EC-Sensor-kit/" target="_blank">For the EC sensor </a>
    - <a href="https://wiki.seeedstudio.com/Grove-PH-Sensor-kit/" target="_blank">For the PH sensor </a>
