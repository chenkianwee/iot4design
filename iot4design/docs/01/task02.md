# Sensirion SCD30 CO2 Sensors with HUZZAH32

This the sensor we are going to build in this exercise.

```{figure} /_static/01task02/scd30_d1.jpg
:width: 100%
```
We will need the following hardwares:
- HUZZAH32 (Can be bought [here](https://www.adafruit.com/product/3591))
- USB Data Cable
- A SCD30 Sensor (Can be bought [here](https://www.digikey.com/en/products/detail/sensirion-ag/SCD30/8445334))
- Jumper Wires x 4 (Can be bought [here](https://www.adafruit.com/product/1956))
- Breadboard (Can be bought [here](https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img))
- Soldering Kit (Can be bought [here](https://www.amazon.com/Soldering-Iron-Kit-Temperature-Desoldering/dp/B073VDX4B7/ref=sr_1_1_sspa?crid=3TI8MUBYG9QXZ&dchild=1&keywords=soldering+kit&qid=1615313665&s=industrial&sprefix=soldering%2Cindustrial%2C166&sr=1-1-spons&psc=1&smid=A1XLBTH0MIQMMO&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFHUTdTSUtLUkdESUQmZW5jcnlwdGVkSWQ9QTAzODE3MjcyS0REVDQ5U1JLSVk4JmVuY3J5cHRlZEFkSWQ9QTAxMjYzMDYxOTk2N0ZMSjdVUVI2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==))
- Laptop

1. Solder the header to your SCD30. Follow similar soldering instructions [here](https://learn.adafruit.com/adafruit-sht31-d-temperature-and-humidity-sensor-breakout/assembly).
</Br><Br/>

2. Connect the HUZZAH32 and SCD30 onto the breadboard as shown in the previous figure. Wire up the Argon and the sensor as follows:
    </Br><Br/>
    - Connect the USB pin of the HUZZAH32 to VIN of the SCD30 sensor.
      ```{figure} /_static/01task02/scd30_d2.jpg
      :width: 50%
      ```

    - Connect the Ground (GND) pin of HUZZAH32 to GND of SCD30 sensor.
      ```{figure} /_static/01task02/scd30_d3.jpg
      :width: 50%
      ```

    - Connect the HUZZAH32 SCL pin to SCL of the SCD30 sensor.
      ```{figure} /_static/01task02/scd30_d4.jpg
      :width: 50%
      ```

    - Connect the HUZZAH32 SDA pin to SDA of the SCD30 sensor.
      ```{figure} /_static/01task02/scd30_d5.jpg
      :width: 50%
      ```
3. Refer to  **Step 1 to 11** of {doc}`../02/subtask02` to setup the HUZZAH32 with Micropython.

4. Download the scd30 scripts from <a href="https://github.com/chaos-laboratory/huzzah32scd30/archive/refs/heads/main.zip" target="_blank">here</a>. Unzip the file.

5. Upload all the scripts in the scd30 folder onto the HUZZAH32 board.
    - Use the ampy library to upload files to the board.
      ```
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\boot.py
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\main.py
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\reg_stapi.py
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\connect_wifi.py
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\webrepl_cfg.py
      $ ampy -p COMx put directory\huzzah32scd30-main\scd30\scd30.py
      ```
6. Once uploaded you can use Thonny to view and edit the script.
    - Fill in the mandatory parameters in the  main.py script.
      ```{figure} /_static/01task02/view.png
      :width: 100%
      ```
7. Open the connect_wifi.py script. Encrypt your ssid and wifi password following the instruction in **Most convenient but lease secure** section of {doc}`../02/subtask03`. Enter your encrypted password and the 16 digit key into the script.
    ```{figure} /_static/01task02/key.png
    :width: 100%
    ```
8. Open the webrepl_cfg.py script. Enter your encrypted password and the 16 digit key into the script.

9. Open the reg_stapi.py script.
    - First fill in the empty url variable in all of the functions. This is the url you are retrieving and posting your sensor results. For chaos_lab you can either post your data to
      ```
      https://andlchaos300l.princeton.edu:8080/FROST-Server/v1.0/
      or
      http://chaosbox.princeton.edu:8080/FROST-Server/v1.0/
      ```
    - Next, posting data to the database requires user and password authorization. You have to first convert your username and password to base64 encoding. We will be using the Python base64 library. Run this script in a Python environment.
      ```
      import base64
      encoded = base64.b64encode(b'user:password')
      print(encoded)
      >>> b'dXNlcjpwYXNzd29yZA=='
      ```
    -  Encrypt your base64 username password following the instruction in **Most convenient but lease secure** section of {doc}`../02/subtask03`. Enter your encrypted base64 username and password and the 16 digit key into the script.
        -  The enc_val variable is at line 8
        -  enter the 16 digit key value in all the functions, line 48, 83, 128.

10. Save all your scripts. Reset the HUZZAH32 and check the Grafana visualization. Look for the Thing and Datastream created in this exercise.

11. Once everything is working. Compile the scripts with passwords into mpy files and upload them onto the device. Following the instruction in **Most convenient but lease secure** section of {doc}`../02/subtask03`.

12. Check again to make sure the device are running as expected.
