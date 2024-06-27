# Sparkfun Air Velocity FS3000
This the sensor we are going to build in this exercise.
- https://learn.sparkfun.com/tutorials/air-velocity-sensor-breakout---fs3000-hookup-guide#example-code

We will need the following hardwares:
- A Particle Argon(Can be bought <a href="https://store.particle.io/collections/gen-3/products/argon" target="_blank">here</a>)
- USB Data Cable
- Air Velocity Sensor(Can be bought <a href="https://www.sparkfun.com/products/18377?_gl=1*32djx7*_ga*MTE4MzI1MDYyOC4xNzA3ODU3NDU1*_ga_T369JS7J9N*MTcwOTU4MTcxMi4yLjEuMTcwOTU4MjU0MC4yMi4wLjA.&_ga=2.148034871.1493328372.1709581713-1183250628.1707857455" target="_blank">here</a>)
- Jumper Wires (Can be bought <a href="https://www.adafruit.com/product/1956" target="_blank">here</a>)
- Breadboard (Can be bought <a href="https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img" target="_blank">here</a>)
- Soldering Kit (Can be bought <a href="https://www.amazon.com/Soldering-Iron-Kit-Temperature-Desoldering/dp/B073VDX4B7/ref=sr_1_1_sspa?crid=3TI8MUBYG9QXZ&dchild=1&keywords=soldering+kit&qid=1615313665&s=industrial&sprefix=soldering%2Cindustrial%2C166&sr=1-1-spons&psc=1&smid=A1XLBTH0MIQMMO&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFHUTdTSUtLUkdESUQmZW5jcnlwdGVkSWQ9QTAzODE3MjcyS0REVDQ5U1JLSVk4JmVuY3J5cHRlZEFkSWQ9QTAxMjYzMDYxOTk2N0ZMSjdVUVI2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==" target="_blank">here</a>)
- Laptop or Computer

1. Connect the Particle device and air velocity sensor onto the breadboard as shown in the figures.
    </Br><Br/>
    - Connect the ADC as follows.
      ```
      Air Velocity <---> Argon/Photon
      GND <------------> GND
      3.3V <-----------> 3.3V
      SDA <------------> SDA/D0
      SCL <------------> SCL/D1    
      ```
2. Refer to {doc}`../030/0318subtask18` to register the Argon Device with our Particle account.

3. Flash the script **'STAPI_1_AIR_VEL_FS3000'** to the Particle device. Fill in the mandatory parameters accordingly. You can choose to leave the optional parameters to their default values.
      ```
      =============================
      !!! MANDATORY PARAMETERS
      ===========================
      String thingDesc = "heatflux measurement and air temperature and humidity"; //DESCRIBE THE DEPLOYMENT
      int sample_rate = 10 * 1000; // how often you want device to publish where the number in front of a thousand is the seconds you want
      #define ADS1220_CS_PIN    D5 // chip select pin
      #define ADS1220_DRDY_PIN  D6 // data ready pin
      float scalib = 1.23; //microvolt per w/m2
      *=============================================================================================================================================
      OPTIONAL PARAMETERS (if the device is already registered, these options are ignored)
      =============================================================================================================================================*/
      //Description of the location
      String foiName = "na"; //THE LOCATION NAME
      String foiDesc = "na";
      String locType = "Point"; //Define the geometry of the location. Refer to https://tools.ietf.org/html/rfc7946 for geometry types.
      String enType = "application/vnd.geo+json";
      //Define the location of the thing. If location is not impt, use [0,0,0] the null island position.
      float coordx = 0.0; //lon/x
      float coordy = 0.0; //lat/y
      float coordz = 0.0; //elv/z
      ```
4. Refer to {doc}`../030/0319subtask19` to visualize the data on Grafana.
