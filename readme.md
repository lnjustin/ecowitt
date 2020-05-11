## Ecowitt WiFi Gateway
*Ecowitt WiFi Gateway driver for Hubitat Elevation*

### Features

- LAN comunication only, no cloud/weather service needed.
- One Hubitat device for each Ecowitt sensor for easy dashboard tiles and RM rules handling.
- On-the-fly Imperial <-> Metric conversion.
- Tile [HTML templates](#templates), which allows endless tiles customization, including displaying multiple attributes in a single tile. 

### Installation Instructions

#### Ecowitt WS View:

1.  Make sure all your sensors are properly registered:  

    <img src="https://i.imgur.com/YBOsGDg.png" width="300" height="600">  

2.  <span>Setup a local/customized weather service as follow (replacing hostname/IP with your own):  

    <img src="https://i.imgur.com/STF5v6d.png" width="300" height="600">

#### Hubitat: 

1.  If the Ecowitt Gateway has been setup correctly, every 5 minutes, you should see the following warning in the Hubitat system log:

    <img src="https://i.imgur.com/Q6w2S7W.png">
    
    That's because this driver has not been installed yet and the hub has nowhere to forward the data to.
    
2.  In "Drivers Code" add the Ecowitt [WiFi Gateway](https://raw.githubusercontent.com/mircolino/ecowitt/master/ecowitt_gateway.groovy) and [RF Sensor](https://raw.githubusercontent.com/mircolino/ecowitt/master/ecowitt_sensor.groovy) drivers:

    <img src="https://i.imgur.com/F66oitb.png">
    
3.  In "Devices" add a new "Ecowitt WiFi Gateway" virtual device and click "Save Device":

    <img src="https://i.imgur.com/3oPQpJ2.png">

4.  Enter the Gateway MAC address (in any legal form) and click "Save Preferences":

    <img src="https://i.imgur.com/YKYtm98.png">

5.  That should be all.
    The first time Hubitat receives data from the Gateway, the driver will automatically create child devices for all the present (and supported) sensors (depending on the frequency you setup your Gateway to POST, this may take a few minutes):
    
    <img src="https://i.imgur.com/Nad8ScL.png">

### <a name="templates"></a> HTML Template:

HTML templates are a powerful way to gang-up multiple Ecowitt sensor attributes in a single Hubitat dashboard tile with endless customization.
The following is a basic example of what you can achieve with a simple HTML template:

<img src="https://i.imgur.com/9Bd0jmh.png" width="160" height="130">

To use them:

1.  In "Hubitat -> Devices" select the Ecowitt sensor (not the gateway) you'd like to "templetize":
    
    <img src="https://i.imgur.com/nkSaORs.png">

2.  In "Preferences -> HTML Tile Template" enter your template (see below how to format them) and click "Save Preferences"

3.  Now, in any Hubitat dashboard, add a new tile, on the left select the Ecowitt sensor, in the center select "Attribute" and on the right select the "html" attribute:
    
    <img src="https://i.imgur.com/YxTja4A.png">   

    You can also remove the tile "html" title by entering the following in the dashboard CSS:

     ```
    #tile-0 .tile-secondary { visibility: hidden; }
    ```
   
#### HTML Template Format:

Templates are pure HTML code with embedded servlets, which are nothing but sensor attributes surrounded by a \$\{\} expression.
For example the following template is used to create the tile in the example above:
     
  ```
  <p>Temperature: ${temperature} �F</p><p>Humidity: ${humidity} %</p><p>Pressure: ${pressure} inHg</p>
  ```
Tips:

1. When you enter the template in the device preferences DO NOT surround it with quotation marks.
2. For each specific sensor template, ONLY use the attributes you see displayed on the upper-right corner of the sensor preferences.
3. For obvious reasons, in a template, NEVER use the expression **\$\{html}**. Or your hub will enter a wormhole and resurface in a parallel universe made only of antimatter ;-) 

***

### Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
