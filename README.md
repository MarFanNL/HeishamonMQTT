# HeishamonMQTT
Simple plugin to manage Heishamon through MQTT


This [Domoticz](https://www.domoticz.com/) plugin is able to read and to control the Panasonic using the [Heishamon](https://github.com/IgorYbema/HeishaMon) module.

# Prerequisites
To use Plugins in Domoticz please read : https://www.domoticz.com/wiki/Using_Python_plugins

# Installation

1. Create a folder [HeishamonMQTT] in the plugin folder of domoticz
2. Restart domoticz
3. Add in the Hardware the Heishamon MQTT plug in.
4. All devices are created, add them from the devices

# Update :

1. place the (new) mqtt.py and plugin.py in the HeishamonMQTT folder (overwrite the old-files)
2. In Hardware, select the HeishamonMQTT plugin and click on Update 
   !!! Do NOT click on delete, all the devices will also be removed then !!!
3. Add new devices when needed


# Current status commands:
```
SetHeatpump			Set heatpump on or off	0=off, 1=on					tested	
SetHolidayMode			Set holiday mode on or off	0=off, 1=on				not tested
SetQuietMode			Set quiet mode level	0, 1, 2 or 3					tested	
SetPowerfulMode			Set powerful mode run time in minutes	0=off, 1=30, 2=60 or 3=90	tested	
SetZ1HeatRequestTemperature	Set Z1 heat shift or direct heat temperature	-5 to 5 or 20 to max	tested
SetZ1CoolRequestTemperature	Set Z1 cool shift or direct cool temperature	-5 to 5 or 20 to max	not tested
SetZ2HeatRequestTemperature	Set Z2 heat shift or direct heat temperature	-5 to 5 or 20 to max	not tested
SetZ2CoolRequestTemperature	Set Z2 cool shift or direct cool temperature	-5 to 5 or 20 to max	not tested
SetOperationMode		Sets operating mode	0=Heat only, 1=Cool only, 2=Auto, 3=DHW only
				, 4=Heat+DHW, 5=Cool+DHW, 6=Auto+DHW					not tested	
SetForceDHW			Forces DHW (Operating mode should be firstly set to one with DWH mode (3,4,5 or 6) to be effective. Please look at SET9 )	0, 1	not tested	
SetDHWTemp			Set DHW target temperature	40 - 75					not tested
SetForceDefrost			Forces defrost routine	0, 1						not tested	
SetForceSterilization		Forces DHW sterilization routine	0, 1				not tested	
SetZones                        Set zones to active  0 = zone 1 active, 1 = zone2 active, 2 = zone1 and zone2 active  tested                      
```

# ToDo:
- Check ForceDHW for correct operation mode
- Add influxDB support
- SetPump / SetPumpSpeed / SetCurves / SetFloorHeatDelta / SetFloorCoolDelta / SetDWHHeatDelta

# Common problems:
If you don't see the heishamon values in domoticz after enabling the plugin there are a few things you should check:
- Is heishamon receiving values from heatpump? (see heishamon webpage)
- Is heishamon correctly sending messages to mqtt broker? (see message in mqtt broker, for example with MQTT explorer)
- Is domoticz plugin correctly configured to point to the mqtt broker?
- Is 'allow new devices' enabled in domoticz?
- Do you have the most recent version of Heishamon firmware? (at least v1.0 is needed for plugin version 0.1.8 and up)


# History
```
Version 0.1.1 -> First version
Version 0.1.2 -> Added COP devices and Error (Text)

Version 0.1.3 ->
		- Round Set...RequestTemperature and SetDHWTemp 
		- check Set...RequestTemperature to be in range -5 to 5 and 20 to max (max is user variable maxTemp, default=50)
		- Check SetDHWTemp to be in range 40 to 75
		- Force_DHW_State only on/off (no unknown anymore)
Version 0.1.4 -> Fix: Switch only publish On (1) not Off (0) in MQTT
Version 0.1.5 -> Implemented S0 Support (2 devices)
Version 0.1.6 -> No change
Version 0.1.7 -> Use MQTT for S0 (panasonic_heat_pump/s0/Watt/x)
Version 0.1.8 -> Allow mqtt base topic to be set 
Version 0.1.9 -> Heishamon v1.0 + Zone (for older version of Heishamon take 0.1.8) 
Version 0.2.0 -> 
		- Change Error from Text to Alert
		- Add Heat Pump Model
		- Add Pump Duty		- 
Version 0.2.0 -> 
		- Added WattHourTotal to S0 (General,kWh)
		- Added Defrost Counter
		- Detect old Heishamon Firmware
		- Code cleanup
		

```
