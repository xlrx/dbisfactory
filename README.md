# DBISfactory Documentation

The code at ```/plc``` can be used to control a Fischertechnik Factory (Art.-Nr. 536634_sim)
consisting of a High Rack, a Vacuum Gripper, a Furnance, and a Sorting Line.

## Hardware list

For this project, you need:
- FischerTechnik Factory Simulation 24V (536634_sim)
- Berghof EC2250
- CodeSys SP5
- a so-called Berghof 'target license' to be able to transfer the PLC data from Codesys to the Berghof
- additional DIO 16/16 Extension board for the EC2250
- a self-made motor encoder board (see below)
- 24 volt stable power supply
- a lot of wires
- and space :-)

## Getting started

- read the Bachelor Thesis from Manuel Göster, acts as manual
- build the motor encoder board (see below)
- connect the factory with the PLC according to the wiring (see io-layout-mapping.pdf in this repository)
- connect the PLC with a computer
- install CodeSys and the PLC target
- transfer the code from this repository (/plc) to the PLC
- start the program

Connect to the factory via REST (optional):
- install the OPC/UA extension in CodeSys
- start the OPC/UA server on the PLC
- download and start the REST service (see https://github.com/xlrx/dbisfactory-opcua-connector)
- API docs are available here: https://github.com/xlrx/dbisfactory-apidocu

## /plc Notes

*.project = CodeSys project file
*.xml = OpenPLC export of the code

The application was build with CodeSys V3.5 SP10, a Berghof EC2250 0.8S PLC and a Berghof DIO 16/16 Extension board.
You have to import a CodeSys Target ("Driver" for your PLC) in order to be able to upload and debug on your PLC type.
Additionally, you have to map the I/O port layout (see io-layout-mapping.pdf) of your PLC to the application structure 
(see Settings of Application). Note, that the hardware switch is implemented as emergency switch to immediately stop 
application execution.

IMPORTANT: you need to build five encoder boards in order to correctly communicate with the Fischertechnik stepping motors
(see folder "motor-encoder-boards").

In general, the program supports three running modes:
- SINGLE (one workpiece is "produced" at a time)
- MULTI (parallel processing, all stations may "produce" one or more workpieces at a time)
- SORT (re-sort the High Rack according to the settings)

The "task controller" of the application can be started with the supplied visualization ("visu") by clicking the only button.

## /motor-encoder-boards Notes

The DBIS factory consists of "normal" motors and "encoder" motors, that are controlled via encoded steps.
When the motor is running, stepping signals are generated and provided to the PLC. 
The number of stepping signals is much higher from the motors than the maximum allowed number of processable steps by the PLC.
Therefore, we need encoder signals that divide the number of signals. 


## Further Information

Project Website: https://www.uni-ulm.de/in/iui-dbis/forschung/laufende-projekte/dbisfactory/
Fischertechnik Circuit Layout: https://content.ugfischer.com/cbfiles/fischer/Zulassungen/ft/536634-Fabrik_Simulation_24V.pdf
Fischertechnik Technical Documentation: https://content.ugfischer.com/cbfiles/fischer/Zulassungen/ft/536634-Factory-simulation-24V-extended-description.pdf

## Documentation

Please see the Bachelor Thesis of Manuel Goester: http://dbis.eprints.uni-ulm.de/1576/

## License

The application is licensed under MIT, always provide the copyright notice.