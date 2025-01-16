# winogradcnn-mpc

## Installation
Follow [EzPC](https://github.com/mpc-msri/EzPC/tree/master) to install the docker of CryptFlow2

## File Prepration
1. In the path of `EzPC/Athos/Networks`, copy the folder of SqueezeNetCIFAR10 and name the new folder as WinogradConv
2. Follow the instruction of setup to prepare the basic files
3. Put the file of WinogradConv_41_sci_OT0.cpp into `EzPC/Athos/Networks/WinogradConv` where involves the Winograd convolution kernel

## Compilation
1. Put the file of CompileCPP.py into the path of `EzPC/Athos` which is modified from CompileSampleNetworks.py to enable seperately compile the c++ file
2. In the path of `EzPC/Athos/Networks/`, set the file of sample_network.config as follows:
```config
{
  "network_name":"WinogradConv",
  "target":"SCI",
  "backend": "OT",
  "run_in_tmux": false 
}
```
