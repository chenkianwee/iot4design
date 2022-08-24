# Register Particle Device

1. Register and setup your Particle device with our chaos lab particle account (You can do it with your own Particle account too). For login information to the Chaos account please approach members of the lab. Follow the instruction [here](https://setup.particle.io/).
    </Br><Br/>
    a. Sometimes, you might have some problem with registering. Doing a factory reset on the Argon might be useful. [Instructions to doing a factory reset](https://community.particle.io/t/how-to-do-a-factory-reset/2579). A summary is provided here.

    ```
    1) Begin holding the MODE button down.
    2) While holding the MODE button down, tap the RESET button briefly.
    3) After 3 seconds the core will begin blinking yellow, KEEP HOLDING the MODE button.
    4) After 10 seconds the core will begin blinking white.
    When this happens the factory reset process has begun. Let go of the MODE button.
    ```
    - It is possible to register the device using the command line on your laptop too. First connect the Particle device to your laptop with a data cable. Download the Particle Cli [here](https://docs.particle.io/tutorials/developer-tools/cli/).
    - Once installed go to the terminal, make sure the device is in listening mode (blinking blue). Type in the following command to get the device id.
    ```
    particle identify
    ```
    - After you have gotten the device id, type in the following. You will be prompted to input the ssid and password of the wifi network you want to connect to.
    ```
    particle serial wifi
    ```
    - once connected go to the particle web ide. Under the device column, go to the very bottom and click on add device. Key in the device id and you can claim the device. Make sure the device is breathing cyan (connected to internet).
3. Once your device is registered, go to the [particle web console](https://console.particle.io/devices). Check if the device is on the list.
    ```{figure} /_static/02subtask01/particle_console.png
    :width: 100%
    :name: particle_console

    We have named our Argon HYDRO_ARG001.
    ```
4. Go to the [Web IDE](https://build.particle.io/build/new). Go to the Devices tab, star the device that you have registered.
    ```{figure} /_static/02subtask01/web_ide.png
    :width: 100%
    :name: web_ide

    Star Argon HYDRO_ARG001, so we can flash to the device.
    ```
5. Click on the code option on the left side bar. In the search bar for 'My apps' search for 'STAPI'. You will see a series of STAPIXX_XXX scripts.
    ```{figure} /_static/02subtask01/web_ide2.png
    :width: 100%
    :name: web_ide2

    STAPIxx series of scripts
    ```
6. For a general description of the integration of Particle with our database (FROST-Server) refer to [here](https://chenkianwee.github.io/masa3db/docs/040/042particle.html).
