# Under the Hood
So what is happening under the hood. The diagram illustrates the various mechanisms that are used. The particle device is connected to the particle.io cloud. We flash the code to the particle device through using the particle web ide. The code instructs the device to read data from the sensor, publish the result on particle.io cloud. The publish statement will trigger the respective webhooks and post the data to the FROST-Server. Once it is posted to the FROST-Server, we can pull data and visualise it with Grafana or any other visualisation software.
```{figure} /_static/0210task10_4/img1.png
:width: 100%
```
## Webhooks
For more information on the webhook integration. Refer to this entry <a href="https://chenkianwee.github.io/masa3db/docs/050/052webhooks.html" target="_blank">https://chenkianwee.github.io/masa3db/docs/050/052webhooks.html</a>
