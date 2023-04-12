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
Our main inspiration came from GPS & Communication devices like the Garmin GPSMAP 66 and the Nokia 800 Tough, the Indirecta Communicator (or iComm) is an attempt to create one such device, that's open source, free for all and modular.
# ✏️ Design
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/design_illustr.png" width="450px"/>

- ###  `Decorative Antennas` 
  Respectively a short GPS Antenna and a long radio Antenna for decoration purposes  

- ###  `Colored Rubber Shell` 
  Protective rubber shell denoting purpose using accent color  

- ###  `Aspect Ratio` 
  Roughly 16:10 (status bar excluded)  

- ## Hardware Keys 
  `Shutdown` ON/OFF Power Toggle for device, turning the device on takes longer than turning it off  

- ## Software Keys (Keyboard)
  `LSK` `RSK` Respectively left and right soft keys, used in applications for zooming in and out (maps), turning volume up down, transposing octave (piano), and other misc. software purposes  

  `Menu` `Back` Respectively used to go back to the iComm apps menu and go back generally (semi-software defined function)  

  **D-PAD** `UP` `LEFT` `OK` `RIGHT` `DOWN` Used for map movement, or other misc. software purposes, OK generally used also as CSK (Center Soft Key, in the bottom bar menu with three options)
  
  `LFN` `RFN` Respectively left and right function keys, similiar in purpose to the software keys, generally reserved for high-level app purposes like changing map display mode, opening a debug menu, etc.

# 🧩 Modularity
A core idea of the iComm is that to use and require different modules for each scope, applications, and resources.  
Here's how iComm GUI is structured:  
<img alt="icomm design" src="https://raw.githubusercontent.com/Indirecta-Technologies/fosd/main/icomm/media/gui_struct.png" width="150px"/>
> - LocalScript `iComm`  
>> - **Module** `Keyboard` Handles all customizable "keys", unique to the iComm device, unifies all button .Activated events under one KeyPressEvent
>> - **Module** `Peripherals` Handles all customizable "peripherals" in it's own script, flashlight API, status led API, etc.
>> - **Module** `Screen` Handles all UI functions unique to the iComm (tweens, notifications, custom D-PAD scrolls, clock, etc.)  
>> - **Module** `Sensors` Very cool Sensors module, usually reused in various Indirecta devices, mentioned below in the README
>> - TextButton `AppTemplate` Irrelevant, used as button template in iComm App Menu
>> - **Configuration** `Apps` Folder containing all iComm app modules, each app has it's own structure depending on the ModuleScript template that will be discussed later in the document  

> - **Frame** `Anchor` Frame containing all device UI (screen, keyboard, deco, etc.)
> - **Frame** `ScreenSizeWarning` Independent frame used in Indirecta products to warn of screen resolutions that might alter normal device behavior

Do note that each module, application or script can have it's own configuration structure and config location
# 🌡️ Sensors
Indirecta ships each iComm or communicator device with a Sensors module. It uses various patched functions ranging from atmospheric data ([thank you PulsarNova!](https://create.roblox.com/marketplace/asset/4996116798)) to extended climate data derived from atmospheric data ([thank you ChatGPT!](https://chat.openai.com/)).  

Thanks to a wonderful idea and ChatGPT, Indirecta has been able to create a state-of-the-art sensor function for electromagnetic interference, that's essentialyl a value fluctuating depending on the number of parts in a range with scripts, and their distance to the player.  

We encourage iComm users to test this sensor in their game, and impose appropriate work safety and system configurations depending on sensor readings
<details>
  <summary>Magnetic Field Strength Algorithm</summary>
  
> ## Magnetic Field Strength 
> ### (**function** `DeviceRadiation` from **Module** `Sensors`)
> ```lua
> ["DeviceRadiation"] = function()
>		wait(.397)
>		-- Define a function that takes a position and a radius as inputs and returns the pollution level at that position
>		local function getPollutionLevel(position, radius)
>			-- Find all the parts within the radius of the given position
>			local parts = game.Workspace:FindPartsInRegion3(Region3.new(position - Vector3.new(radius, radius, radius), position + Vector3.new(radius, radius, radius)))
>
>			-- Initialize a counter for the number of parts with scripts
>			local numScripts = 0
>			local p3 = 0
>
>			local major_contributor = nil
>			local major_contribution = 0
>
>			-- Iterate over the parts and count the number with scripts attached to them
>			for _, part in pairs(parts) do
>				if part.Parent == workspace then continue end
>				if game:GetService("Players"):GetPlayerFromCharacter(part.Parent) then continue end
>
>				local distance = (part.Position - position).Magnitude+0.001
>				local function countScriptDescendants(part)
>					local numScripts = 0
>					local blacklist = {}
>					local currentPart = part
>					while currentPart.Parent ~= workspace do
>						for _, descendant in pairs(currentPart:GetDescendants()) do
>							if descendant:IsA("BaseScript") and descendant.Disabled == false and not table.find(blacklist, descendant) then
>								table.insert(blacklist, descendant)
>								numScripts = numScripts + 1
>							end
>						end
>						currentPart = currentPart.Parent
>					end
>					return numScripts
>				end
>
>				local numPartScripts = countScriptDescendants(part)
>
>				numScripts += numPartScripts
>
>				-- Calculate the contribution of the current part to p3
>				local contribution = numPartScripts / (2 * math.pi * distance)
>				if contribution > major_contribution then major_contributor = part.Parent.Name end
>				p3 += contribution
>
>			end
>
>			-- Calculate the pollution level as a function of the number of parts with scripts and the radius
>			local pollutionDensity = numScripts / (radius^2)
>			-- Round to micron
>			pollutionDensity = math.round(pollutionDensity / 0.000001 * 10) / 10
>
>			-- Calculate more accurate microTesla unit from weighted average (p2 is much higher than pollution density)
>			local microTeslaDensity = math.clamp((math.log(1+p3)) * 8, 0, math.huge) --15000000, needs a lot more tuning.
>
>			return microTeslaDensity, pollutionDensity
>		end
>
>		local tesla, density = getPollutionLevel(HumanoidRootPart.Position, 45)
>		if config["MagnetometerUnit"] == "Density" then
>			return string.format("%.2f µP/stud", density), (math.log(density) / 15) * 100
>		elseif config["MagnetometerUnit"] == "microTesla" then
>			return string.format("%.2f µT", tesla), (tesla + 100) / 2
>		elseif config["MagnetometerUnit"] == "milliGauss" then
>			return string.format("%.2f mG", tesla*10), (math.log(density) / 15) * 100
>		else return "-",50 end
>
>
>	end
> ```
</details>

# 🪩 Peripherals  
As described before, the iComm also features a Peripherals module, it currently has the following default peripherals:
> - **function** `:Led(Color3)` Changes status LED Peripheral color to first argument provided (must be a Color3 obj)
> - **function** `:Torch(On, Brightness)` Changes torch peripheral light enabled depending on first argument, range and brightness depending on the second argument; if no arguments are provided, the Torch LED will toggle Value with a default Brightness of `3`
# ⚗️ Use cases
Thanks to the iComm's modularity, we foresee endless possibilities.  
We suggest using the iComm in any RTECH-product based game, really, thanks to it's encrypted frequency Radio powering safe and secure staff communications,  
maps contributing to forest/deep game navigation,  
and incredible modularity empowering the game owner to customize the iComm to fit any use case, and create their own game-themed applications.



## ⚠️ License

The iComm and any other proprietary related devices by Indirecta are released under the GNU GPL v3 license.