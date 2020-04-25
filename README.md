﻿# DataValidateFix
A torch plugin which fix several data validate issue for SpaceEngineers server.

The SpaceEngineers server NOT validate some important two-way sync variable received from client.

For example, open the file located in `SpaceEngineers\Content\Data\CubeBlocks\CubeBlocks_Automation.sbc`(XML) and search for text `MyObjectBuilder_SensorBlockDefinition`.

Modify `MaxRange` of this BlockDefinition then save it.

Use this modified client to connect to dedicated server, you will find that you can set `LeftExtend`, `RightExtend` and other options in SensorBlock UI to very large value.

Those data NOT ONLY display on client, server actually accept them.

Use ProgramBlock to get data from SensorBlock with [`Sandbox.ModAPI.Ingame.IMySensorBlock.DetectedEntities`](https://github.com/malware-dev/MDK-SE/wiki/Sandbox.ModAPI.Ingame.IMySensorBlock.DetectedEntities).

Player can get as many grids' position as he want by increase the `MaxRange` in XML.

# Feature
This plugin add extra validate logic in server to void the problem above.

Current fixed:
* MySensorBlock(LeftExtend, RightExtend, BottomExtend, TopExtend, BackExtend, FrontExtend)
* MyWarhead(Countdown)
* MyLargeTurretBase(ShootingRange)
* MyOreDetector(Range)
* MyMechanicalConnectionBlockBase(SafetyDetach)
* MyPistonBase(MaxVelocity, MaxLimit, MinLimit, MaxImpulseAxis, MaxImpulseNonAxis)
* MyMotorStator(Torque, BrakingTorque, TargetVelocity)

# TODO
* Projector
* Antenna
* SafeZone
* Sound
* Light

# Note
The game will automatically correct the wrong data when loading world. If the player created illegal data, Those data will be cleared after the server restarts(to nearest legal value). No more step need to be done, just install this plugin and restart server.

# License
Apache 2.0