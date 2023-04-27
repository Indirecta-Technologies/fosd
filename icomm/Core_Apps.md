<h1 align="center">
  <img alt="cgapp logo" src="https://raw.githubusercontent.com/Indirecta-Technologies/branding/main/logos/indirecta_logo_medium500_withPill.png" width="350px"/><br/>
  iComm
</h1>
<p align="center">
  <a href="https://github.com/Indirecta-Technologies/branding">Branding</a> •
  <a href="https://github.com/Indirecta-Technologies/RFCs">RFCs</a> •
  <a href="https://github.com/Indirecta-Technologies/dob">DOB</a> •
  <a href="https://github.com/Indirecta-Technologies/indirectaSEA">iSEA</a> •
  <a href="https://github.com/Indirecta-Technologies/pcsi">pCsi</a> •
  <a href="https://github.com/Indirecta-Technologies/rtech-archive">rtech-archive</a> •
  <a href="https://github.com/Indirecta-Technologies/openlift">openlift</a> •
  <a href="https://github.com/Indirecta-Technologies/Rufus">Rufus</a>
</p>

# 💡 General Idea
Indirecta ships each iComm or communicator device with roughly 5 default applications, these applications are called core apps, similiar to GNOME Desktop Environment's Core and Circle apps.  
This article aims to describe best all the core applications.  
More complex core applications like the Radiocomm app can have their own article.

# 🛰️ Radiocomm `Radio`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/radiocomm_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/radiocomm_2.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/radiocomm_3.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/radiocomm_4.png" width="200px"/>

>Radio-like encrypted messaging app made with ❤️ by Indirecta  
>Allows the user to change frequency up/down 1/.5 MHz, messages are sent in different MessagingService topics depending on frequency, and encrypted with frequency and a key derived from an optional secret using [Indirecta's public encryption algorithm](https://github.com/Indirecta-Technologies/indirectaSEA)  

- Use mouse scroll wheel to scroll, if not available (disabled by group/developer), use the `UP` and `DOWN` iComm Keys  
- When the app is launched, an extension of the status bar (macro title) featuring PTT/Mic status and current frequency
- For developers or advanced users, the custom iSEA String Key option in the freq. menu can be toggled using `LFN`; there is also a debug menu featuring experimental data that can be toggled using `RFN`
- As string encryption is also used on messages without custom keys using their frequency, the Roblox filter cannot be implemented, and we are not responsible for inadequate usage of this application among common game players and not experienced staff. We have implemented a setting in both the Client and Server scripts (both must be either false or true) allowing game developers to disable all encryption options and techniques.
- Since the PTT/Microphone message capture technique uses Roblox's .Chatted event, when sending a message using Radiocomm, it will also be shown in Roblox chat. That is why we suggest game developers who use Radiocomm to remove chat history, allowing only bubble chat (your messages will still be seen if you're close, but it's also realistic this way)

# 🧭 Compass `Compass`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/compass_1.png" width="200px"/>

>Basic application displaying current camera orientation using `Camera.CoordinateFrame.LookVector`   
>Displays camera orientation in 3 ways, using labels for each heading, a label for the orientation in degrees, and a compass arrow.

# 🗺️ Map `Map`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/map_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/map_2.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/map_3.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/map_4.png" width="200px"/>

>Map application made with ❤️ by Indirecta  
>Loads 500 instances at a time to prevent crashes, calculates time took from 1 lag spike to the other (experimental)  
>Displays map in 3 modes, one display a blue player indicator with a compass indicator, the other rotating the map directly dependign on the compass orientation, and the last freezing the camera (for now, intended to be a free arrow navigation mode); the modes are toggled using `LFN`  
>Also allows for waypoints to be added to the map (in the module configuration, or by editing existing ones using FOSDebug), and loads all of the current server's players' position using colored indicators
>Displays in the bottom left of the screen an indicator depicting the width of the map shown in real world units.

# 🔦 Torch/Flashlight `Torch`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/flashlight_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/flashlight_2.png" width="200px"/>

>Core application with tool flashlight peripheral integration  
>Allows 5 different flashlight on-off intervals, 5 flashlight brightness levels (brightness-range tradeoff configurations) and an emergency SOS interval  
>As iComm developers may develop directly with the iComm firmware (GUI) directly in StarterGui, without it being linked to any hardware (tool that toggles GUI), the Torch app displays a warning screen when it detects that there isn't any iComm tool or flashlight linked as a peripheral to use



# 📈 Sensors `AtmosData`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_2.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_3.png" width="200px"/>

>Application displaying in a scrollable list all auto-updating iComm Sensor Updates.  
>Occasionally displays readings using colored progress bars, graphs, and custom units.

- Use mouse scroll wheel to scroll, if not available (disabled by group/developer), use the `UP` and `DOWN` iComm Keys  
- When the app is launched, an extension of the status bar featuring ping connectivity bars and a favorite measurement is added, that is configurable through the application module configuration

# 🐞 Indirecta Free Open Source Device Debug Kit `FOSDebug`
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/fosdebug_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/fosdebug_2.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/fosdebug_3.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/fosdebug_4.png" width="200px"/>

>Application displaying in a scrollable list all loaded applications, it is heavily in development, and not user friendly as it was designed as a developer kit accessory only.  
>It allows developers to select applications, and edit live module data such as sensor configuration, app name, icon, soft keys, etc. without interrupting the playtest

- The user is greeted with a red on black selection menu. Use the `UP` and `DOWN` iComm Keys to scroll and `OK` to choose.  The only choice available on the current version is the Applications debug menu. 
- After selecting the Applications menu, the user can scroll using the previous keys or the mouse scroll wheel, and select an application.
- After selecting an application, the user will be able to edit live module "self" data such as AppInfo, Configuration strings and booleans.



## ⚠️ License

The iComm and any other proprietary related devices by Indirecta are released under the GNU GPL v3 license.
