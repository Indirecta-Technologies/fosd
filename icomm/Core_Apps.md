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
Indirecta ships each iComm or communicator device with roughly 4 default applications, these applications are called core apps, similiar to GNOME Desktop Environment's Core and Circle apps.  
This article aims to describe best all the core applications.  
More complex core applications like the Radiocomm app can have their own article.

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

# 📈 Sensors `AtmosData`

<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_1.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_2.png" width="200px"/>
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/atmosdata_3.png" width="200px"/>

>Application displaying in a scrollable list all auto-updating iComm Sensor Updates.  
>Occasionally displays readings using colored progress bars, graphs, and custom units.

- Use mouse scroll wheel to scroll, if not available (disabled by group/developer), use the `UP` and `DOWN` iComm Keys  
- When the app is launched, an extension of the status bar featuring ping connectivity bars and a favorite measurement is added, that is configurable through the application module configuration



## ⚠️ License

The iComm and any other proprietary related devices by Indirecta are released under the GNU GPL v3 license.
