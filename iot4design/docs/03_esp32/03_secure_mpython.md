# Securing Passwords and codes - Micropython

## Most convenient but lease secure
1. Easiest and most convenient, but least secure. Encrypt your password and compile it into .mpy file. The password will be encrypted into bytecode. The password won't be human readable. However, it is possible to reverse engineer the .mpy files and obtain the password.

    - <a href="https://forum.micropython.org/viewtopic.php?f=16&t=6726&p=38315&hilit=ucryptolib.aes#p38315" target="_blank">Encrpyt your password with the ucryptolib library</a>
      ```
      import ucryptolib
      enc = ucryptolib.aes(b'1234567890123456', 1)
      data = 'input plaintext'
      data_bytes = data.encode()
      enc_val = enc.encrypt(data_bytes + b'\x00' * ((16 - (len(data_bytes) % 16)) % 16))
      print(enc_val)
      >>> b'\xfe!F\x87?\xdb\x19\x18\xcdM\x83\x9b\xaa\x02\xa9\x04'
      ```

    - Use the encrypted password and your 16 digit key in your script. So your passwords are not stored as human readable plain text on your device.
      ```
      dec = ucryptolib.aes(b'1234567890123456', 1)
      dec_val = dec.decrypt(b'\xfe!F\x87?\xdb\x19\x18\xcdM\x83\x9b\xaa\x02\xa9\x04')
      print(dec_val)
      >>> b'input plaintext\x00'
      ```
2. Download mpy-cross library. The mpy-cross library will compile your script into bytecodes. Thus making it harder to obtain your password.
    ```
    $ pip install mpy-cross
    ```
    - You can compile your codes with the following command.
      ```
      $ python -m mpy_cross directory\scd30\connect_wifi.py -march=xtensawin -X emit=bytecode

      # then upload the mpy file into the device
      $ ampy -p COMx put directory\scd30\connect_wifi.mpy
      ```

## Quite secure storing the passwords in RTC memory (untested)
Quite secure, but it will be very inconvenient as once the chip lose power, you will have to have physical access to the chip to restart. Store the password in memory. Once the board is restarted, all passwords are lost.
- <a href="https://forum.micropython.org/viewtopic.php?t=7013" target="_blank">Full discussion</a>.
```
import machine
rtc = machine.RTC()
rtc.memory(b'hello')
```
## Quite secure using wifimanager library (untested)
Using wifimanager library.
- <a href="https://randomnerdtutorials.com/micropython-wi-fi-manager-esp32-esp8266/" target="_blank">Tutorials here</a>.

## Most secure with secure boot and flash encryption (untested)
Highest level of security, enable secure boot and flash encrpytion. Precompile and Freeze the python module and bundle it with the firmware. Require the most amount of effort with compiling and freezing modules.
- <a href="https://forum.micropython.org/viewtopic.php?t=4510" target="_blank">https://forum.micropython.org/viewtopic.php?t=4510</a>

- <a href="https://limitedresults.com/2019/11/pwn-the-esp32-forever-flash-encryption-and-sec-boot-keys-extraction/" target="_blank">https://limitedresults.com/2019/11/pwn-the-esp32-forever-flash-encryption-and-sec-boot-keys-extraction/</a>

- <a href="https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html" target="_blank">https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html</a>

- <a href="https://iotworkers.com/board-development/esp32-the-secure-boot.html" target="_blank">https://iotworkers.com/board-development/esp32-the-secure-boot.html</a>

- <a href="https://docs.espressif.com/projects/esp-idf/en/latest/esp32/security/secure-boot-v1.html#secure-boot-reflashable" target="_blank">https://docs.espressif.com/projects/esp-idf/en/latest/esp32/security/secure-boot-v1.html#secure-boot-reflashable</a>

### For Pycom boards
Can use these instructions for references
- <a href="https://docs.pycom.io/advance/frozen/" target="_blank">https://docs.pycom.io/advance/frozen/</a>
- <a href="https://docs.pycom.io/advance/encryption/" target="_blank">https://docs.pycom.io/advance/encryption/</a>
