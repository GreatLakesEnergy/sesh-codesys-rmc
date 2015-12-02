# sesh-codesys-rmc
This is an RMC unit designed to work on the WAGO PFC200 series plc. Code is written in codesys V2. 
Be aware that this code is quite specific in nature but does touch on many characteristics of using a PFC-200.
It is intended to store data from PV systems in a MYSQL database

#PLC Configuration
This code is designed to work with the following configuration.

![sample system diagram ](https://raw.githubusercontent.com/GreatLakesEnergy/sesh-diagrams/master/wago_config.PNG "sesh system diagram")

You will need to modufy the codesys project to reflect your own ocnfiguration in the PLC configuration tab in Codesys.


#Code Configuration

You'll need to modify certain variables for the code to work accordingly. THe following code can be found in "Global Variables" under "resources" tab

```
(* MYSQL configs *)
gc_sHost : STRING := 'your_Database_url';  (*'application.dyndns.info';*)
gc_uiPort : UINT := 3306;
gc_sUser : STRING := 'your_Database_user';
gc_sPwd : STRING := 'your_Database_password';
gc_sDB : STRING := 'your_database';   	(* Optional - Name of database instance to connect to *)
gc_sTable:STRING := 'your_db_table' ;
```
	
Logging interval is configured by the following paramter. Though keep in mind that this is also attributed to your cycle speed in which the task is running.
	

	(* Logging constants*)
  gc_LogInterval             :TIME := T#1s;
  gc_iTotalParams		:INT := 18;


The PFC200 is equiped with a relay firing module designed to start or stop a generator. The variables below identify the thresholds that will trigger this functionality

	(* generator constants*)
	gc_DCVoltageGenSetON :REAL := 23; (*make this a bit higher tha load shedding time*)
	gc_DCVoltageGenSetOFF :REAL := 26; (*make this estimate soc %80*)

	(*how many cycles do we wait before we trigger the genset need to calculate based no cycletime *gc_DCGenCycleCount = total_seconds  *)
	gc_DCGenCycleCount       :INT := 40;

	
#Running
Make sure the your 750-8202 is powered up with a 24v power supply
	
A diagram of the PFC 200 setup can be found here.
	
![wago system diagram ](https://raw.githubusercontent.com/GreatLakesEnergy/sesh-diagrams/master/wago_image_setup.jpg "wago system diagram")

	
	
	
