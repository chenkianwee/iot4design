# Micropython on HUZZAH32

Overview of the <a href="https://learn.adafruit.com/adafruit-huzzah32-esp32-feather" target="_blank">HUZZAH32 board from Adafruit</a>. This exercise is based on a series of other tutorials available online.
- <a href="https://how2electronics.com/esp32-micropython-upycraft-getting-started/" target="_blank">Micropython with uPyCraft instructions</a>.
- <a href="https://github.com/pvanallen/esp32-getstarted" target="_blank">HUZZAH32 with Micropython getting started guide</a>.
- <a href="https://circuitdigest.com/microcontroller-projects/how-to-program-esp32-in-micropython-using-thonny-ide" target="_blank">Micropython with Thonny IDE</a>.
- <a href="https://learn.adafruit.com/micropython-basics-esp8266-webrepl/access-webrepl" target="_blank">Enabling Micropython webrepl</a>

This exercise assumes you are familiar with programming with Python and Anaconda.

1. Download and install the driver necessary to read and write from HUZZAH32 <a href="https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers" target="_blank">here</a>. In this exercise, I am using a Windows machine. However, the steps should work for the other OSes.
    - Connect the HUZZAH32 board to your computer. Go to Device Manager. You should be able to see under Ports (COM & LPT) - Silicon Labs CP210x USB to UART Brigdge (COMx). Remember the COM number 'COM4' in my case.
      ```{figure} /_static/02subtask02/comport.PNG
      :width: 50%
      :name: comport
      ```
2. Download the <a href="https://micropython.org/resources/firmware/esp32-20210623-v1.16.bin" target="_blank">Micropython</a> firmware.

3. Install <a href="https://docs.conda.io/en/latest/miniconda.html" target="_blank">miniconda</a>. For instructions on how to use conda refer to <a href="https://docs.conda.io/projects/conda/en/latest/user-guide/index.html" target="_blank">this</a>.
    - Create an environment call micropython.
        ```
        $ conda create --name micropython python=3.9
        ```
    - Once created activate the environment and we will be working in this environment.
        ```
        $ conda activate micropython
        ```

4. Install the esptool.py tool with the following command in the micropython environment.
    ```
    $ pip install esptool
    ```
5. Install the ampy library with the following command.
    ```
    $ pip install adafruit-ampy
    ```
6. Type in this command to erase and flash the micropython onto the HUZZAH32 board. Remember the COM number of your HUZZAH32 board. Specify the directory of where you downloaded your Micropython firmware.
    ```
    $ esptool --chip esp32 --port COMx erase_flash
    $ esptool --chip esp32 --port COMx --baud 460800 write_flash -z 0x1000 <micropython_firmware>.bin
    ```
7. With Micropython install on your board. We can write some codes with the Thonny IDE. Download the Thonny IDE <a href="https://thonny.org/" target="_blank">here</a>.

8. In Thonny go to Tools -> Options -> Interpreter. In the 'Which interpreter or device should Thonny use for running your code?', choose Micropython (ESP32). In the 'Port or WebREPL', choose the COM your HUZZAH32 board is connected to.
    ```{figure} /_static/02subtask02/thonny.PNG
    :width: 100%
    ```
    - Once chosen, the shell will show it is connected to the Micropython on the HUZZAH32.
      ```{figure} /_static/02subtask02/thonny2.PNG
      :width: 100%
      ```
9. Connect to an existing WiFi network and enable webrepl interface. This will allow you to access the device through a local network.
    - Write a script and upload it onto the board to connect to the internet. Go to File -> New. Copy and paste the codes onto the script. Connect to an existing wifi network with the following script.
      ```
      def connect():
          import network
          import time
          ssid = b'your ssid name'
          pw = b'your password'

          station = network.WLAN(network.STA_IF)
          if station.isconnected() == False:
              print('connecting to network...')
              station.active(True)
              # wifi_networks = station.scan()
              # status = station.status()
              station.connect(ssid, pw)
              print('still connecting ...')
              while station.isconnected() == False:
                  time.sleep(3)

              print('connected!')
              print(station.ifconfig())
          else:
              print('already connected')
              print(station.ifconfig())

      connect()
      ```

10. Go to File -> Save as ... -> Micropython device. Save the script as main.py. The boot.py and main.py are executed at each startup of the board.
    ```{figure} /_static/02subtask02/thonny3.PNG
    :width: 100%
    ```

11. Press the reset button on HUZZAH32. If your credentials for your Wifi network is correct, you will see the successful connection message.
    ```{figure} /_static/02subtask02/thonny4.PNG
    :width: 100%
    ```

12. To enable webrepl, open the boot.py file.
    - At the shell of the Thonny IDE, type in:
      ```
      import webrepl_setup
      ```
      ```{figure} /_static/02subtask02/thonny5.PNG
      :width: 100%
      ```
    - Check the boot.py file these two lines of code will be uncommented.
      ```
      import WebREPL
      webrepl.start()
      ```
    - First disconnect your HUZZAH from Thonny IDE. Now go to the <a href="http://http://micropython.org/webrepl/" target="_blank">micropython webrepl</a>. In **step 10**, when you are connected a list of ip address is printed out. In my case the HUZZAH32 is connected on the 192.168.1.243 ip address. On the top left corner, key in:
      ```
      ws://192.168.1.243:8266
      ```
      You will be prompted to enter the password you entered when setting up the webrepl. If successful you will be able to control the HUZZAH board as shown below. Remember to disconnect your board from the Thonny IDE. If not you will not be able to type in any commands in the webrepl.

      ```{figure} /_static/02subtask02/webrepl.PNG
      :width: 100%
      ```

13. Next we will write a blink.py script and upload it onto the board to blink the LED on HUZZAH32. Go to File -> New. Copy and paste the codes onto the script. Save the file as main.py as in step 9.
    ```
    import machine
    import time

    #setup
    led = machine.Pin(13, machine.Pin.OUT) # LED on the board

    #loop
    while True:
      if led.value() == 0:
        led.value(1)
      else:
        led.value(0)
      time.sleep(0.5)
    ```

14. Press the reset button on HUZZAH32. You will be able to see the LED blinks.
