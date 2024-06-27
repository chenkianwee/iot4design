# IoT for Design
This is a manual that provide information on how to build your own Internet of Things (IoT) devices. 
# Pre-requisite
## Backend Database and REST API
All of the tutorials in this e-book assume that you already setup a database backend setup that has a REST API. I am using the Yun2Infinity open-source software stack. You can either setup an instance on your local computer (you can only access the server on your local network) or set it up on a cloud instance like the aws ec2 instance. Follow the <a href="https://chenkianwee.github.io/yun2infinity/docs/030/031deploy.html" target="_blank">tutorial</a> to setup the backend.

## Equipment
- Jumper Wires x 4 (can be bought [here](https://www.adafruit.com/product/1956))
- PH 2.0mm Male & Female JST Connector Kit, more permanent wire connection (can be bought [here](https://www.amazon.com/Keszoox-Connector-Pre-Crimped-Housing-Connector%EF%BC%8810/dp/B09SX4W8Q6/ref=sr_1_1_sspa?crid=1LPD117TNLZKY&dib=eyJ2IjoiMSJ9.8w5jZBmC9jLa61wHzO6ZqngH8tE04_-idppruckAj0hydpHmsYKqEuDxLCtgQScwyzL3F3ZV4nnaqtj3JOn16mAOs4w88TfvB4TJoMyjCpuYLE4mIbe8OZOLriSuI6nqZUlYNqdBbXKlDliMW5vPYbcGDPMqnEfUhuhZaxIdV5Q3Px0xATKK1WMebCrPG9LTy0T8L5WN440aJYiQEq08d082QYU7bVPXLVkBaDESBrbMvJAaddcq2A7tJEPJx1EhTYZ-lS0mzTyxkJjt5cMBAh5E9TRMsve4Vxx0n7l-DLE.qH3KnTaOvKnw8QvYRXdzfiBFe-c_y7iDNq_BrZlZ4vQ&dib_tag=se&keywords=PH+2.0mm+JST+Connector&qid=1709700585&s=hi&sprefix=ph+2.0mm+jst+connector+%2Ctools%2C74&sr=1-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1))
- Breadboard (can be bought [here](https://www.amazon.com/dp/B07DL13RZH/ref=redir_mobile_desktop?_encoding=UTF8&aaxitk=Ha8lI6PHb2sFCtkeyNViLQ&hsa_cr_id=4991273630901&pd_rd_plhdr=t&pd_rd_r=e429b428-9c18-43cc-bdb2-24937613797e&pd_rd_w=SmgRr&pd_rd_wg=zw5Ku&ref_=sbx_be_s_sparkle_mcd_asin_0_img))
- Solderable Breadboard (can be bought [here](https://www.adafruit.com/product/571))
- Soldering Kit (can be bought [here](https://www.amazon.com/dp/B09HXD4L14/ref=sspa_dk_detail_3?pd_rd_i=B09HXD4L14&pd_rd_w=qlXev&content-id=amzn1.sym.d81b167d-1f9e-48b6-87d8-8aa5e473ea8c&pf_rd_p=d81b167d-1f9e-48b6-87d8-8aa5e473ea8c&pf_rd_r=AGW0CW28JTSQJGBDCRZW&pd_rd_wg=VrIRT&pd_rd_r=ca1243df-3184-40bc-bb39-de15791137f7&s=industrial&sp_csd=d2lkZ2V0TmFtZT1zcF9kZXRhaWxfdGhlbWF0aWM&th=1))
- Solid core hookup wires (can be bought [here](https://www.amazon.com/TUOFENG-Hookup-Wires-6-Different-Colored/dp/B07TX6BX47/ref=pd_ci_mcx_di_int_sccai_cn_d_sccl_4_3/138-9205715-1450825?pd_rd_w=sJ5XL&content-id=amzn1.sym.751acc83-5c05-42d0-a15e-303622651e1e&pf_rd_p=751acc83-5c05-42d0-a15e-303622651e1e&pf_rd_r=GZR050VFQTHW63GXXANJ&pd_rd_wg=RLbwJ&pd_rd_r=0e526a56-53f7-43b6-a669-075baf18359e&pd_rd_i=B07TX6BX47&th=1))

### Particle.io
The tutorials on Particle.io devices will work on all Argon, Boron and Photon1. It has not been tested on Photon2 (https://store.particle.io/collections/all-products?filter.p.product_type=Development%20Boards).

### ESP32
The tutorials on ESP32 will work on HUZZAH32 from Adafruit (https://www.adafruit.com/product/3405).

## Resources
- Making http request on the Particle.io devices locally: (https://randomnerdtutorials.com/esp32-http-get-post-arduino/)
- Making https request on ESP32: (https://randomnerdtutorials.com/esp32-https-requests/)
- OTA for ESP32: https://randomnerdtutorials.com/esp32-ota-over-the-air-vs-code/
- ESP32 deep sleep: https://randomnerdtutorials.com/esp32-timer-wake-up-deep-sleep/
