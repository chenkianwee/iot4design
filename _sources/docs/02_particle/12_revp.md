# Modern Device Wind Sensor Rev P with Particle Argon
This the sensor we are going to build in this exercise.

```{figure} /_static/0215task15/img1.jpg
:width: 50%
```
We will need the following hardwares:
- A Particle Photon, it will work with Argon too (Can be bought <a href="https://store.particle.io/collections/gen-3/products/argon" target="_blank">here</a>)
- USB Data Cable
- Wind Sensor Rev.P (Can be bought <a href="https://moderndevice.com/product/wind-sensor-rev-p/" target="_blank">here</a>)
- Jumper Wires x 4 (Can be bought <a href="https://www.adafruit.com/product/1956" target="_blank">here</a>)
- Breadboard (Can be bought <a href="https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img" target="_blank">here</a>)
- 12V Power Adapter (Can be bought <a href="https://www.adafruit.com/product/798" target="_blank">here</a>)
- Female DC Power Adapter (Can be bought <a href="https://www.adafruit.com/product/368" target="_blank">here</a>)
- Soldering Kit (Can be bought <a href="https://www.amazon.com/Soldering-Iron-Kit-Temperature-Desoldering/dp/B073VDX4B7/ref=sr_1_1_sspa?crid=3TI8MUBYG9QXZ&dchild=1&keywords=soldering+kit&qid=1615313665&s=industrial&sprefix=soldering%2Cindustrial%2C166&sr=1-1-spons&psc=1&smid=A1XLBTH0MIQMMO&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFHUTdTSUtLUkdESUQmZW5jcnlwdGVkSWQ9QTAzODE3MjcyS0REVDQ5U1JLSVk4JmVuY3J5cHRlZEFkSWQ9QTAxMjYzMDYxOTk2N0ZMSjdVUVI2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==" target="_blank">here</a>)
- Laptop or Computer

1. Connect the Argon, Wind Sensor and 12V power onto the breadboard as shown in the figures.
    </Br><Br/>
    - Connect the Wind Sensor Rev P as follows
      ```
      Wind Sensor <---> Argon/ Power Adapter  
      GND <----------------> Argon (GND)
                   |
                   |-----------> Power Adapter (-)
      +9-12V <-----------------> Power Adapter (+)
      OUT <----------------> Argon (A0)
      TMP <----------------> Argon (A1)
      ```
2. Refer to {doc}`../030/0318subtask18` to register the Argon Device with our Particle account.

3. Flash the script **'STAPI_1_WIND_REVP'** to the Argon. Fill in the mandatory parameters accordingly. You can choose to leave the optional parameters to their default values.
    ```
    =============================================================================================
    !!! MANDATORY PARAMETERS
    =============================================================================================
    const int OutPin  = A0;   // wind sensor analog pin  hooked up to Wind P sensor "OUT" pin
    const int TempPin = A1;   // temp sesnsor analog pin hooked up to Wind P sensor "TMP" pin
    String thingDesc = "windrev-p"; //DESCRIBE THE DEPLOYMENT
    int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
    =============================================================================================
    OPTIONAL PARAMETERS
    (this parameters only works when it is the first time registration of the device)
    (if the device is already registered, these options are ignored)
    =============================================================================================
    //Description of the location
    String foiName = "na"; //THE LOCATION NAME
    String foiDesc = "na";
    String locType = "Point";
    String enType = "application/vnd.geo+json";
    //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
    float coordx = 0.0; //lon/x
    float coordy = 0.0; //lat/y
    float coordz = 0.0; //elv/z
    ```
4. Refer to  {doc}`../030/0319subtask19` to visualize the data on Grafana.
