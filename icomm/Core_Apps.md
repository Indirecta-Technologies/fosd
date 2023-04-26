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
Indirecta ships each iComm or communicator device with 4 default applications, these applications are called core apps, similiar to GNOME Desktop Environment's Core and Circle apps.  
This article aims to describe best all the core applications.  
More complex core applications like the Radiocomm app can have their own article.

# 📈 Sensors `AtmosData`

Application displaying in a scrollable list all auto-updating iComm Sensor Updates. Occasionally displays readings using colored progress bars, graphs, and custom units.

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



## ⚠️ License

The iComm and any other proprietary related devices by Indirecta are released under the GNU GPL v3 license.
