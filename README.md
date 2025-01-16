# winogradconv-mpc

## Installation
Follow the instructions of [EzPC](https://github.com/mpc-msri/EzPC/tree/master) to install the docker of CryptFlow2. Note that Tensorflow1.x is necessary for the program running.

## File Prepration
1. In the path of `EzPC/Athos/Networks`, copy the folder of SqueezeNetCIFAR10 and name the new folder as WinogradConv.
2. Follow the instruction of setup to prepare the basic files.
3. Put the file of WinogradConv_41_sci_OT0.cpp into `EzPC/Athos/Networks/WinogradConv` where involves the Winograd convolution kernel.
4. The testing dimensions can be modified as follows:
```cpp
int N = 1;  // batch size
int H = 16;  // height
int W = 16;  // width
int C = 32;  // input channels
int K = 64;  // output channels
```

## Compilation
1. Put the file of CompileCPP.py into the path of `EzPC/Athos` which is modified from CompileSampleNetworks.py to enable seperately compile the c++ file.
2. In the path of `EzPC/Athos/Networks/`, set the file of sample_network.config as follows:
```config
{
  "network_name":"WinogradConv",
  "target":"SCI",
  "backend": "OT",
  "run_in_tmux": false 
}
```
3. Use the commands below to compile the c++ file:
```bash
cd EzPC/Athos
python CompileCPP.py --config Networks/sample_network.config
```

Note that in CompileCPP.py, you can modify the bit width for the private inference (41-bit by default):
```python
if target == "SCI":
  bitlength = 41
```

After compilation, there will be an excutable file named WinogradConv_SCI_OT.out in the path of `EzPC/Athos/Networks/WinogradConv/`.

## Inference with 2PC
```bash
cd EzPC/Athos/Networks/WinogradConv
```

Terminal 1: initialize the server side:
```bash
/WinogradConv_SCI_OT.out r=1 < model_weights_scale_12.inp
```

Terminal 2: initialize the client side:
```bash
/WinogradConv_SCI_OT.out r=2 < model_input_scale_12.inp
```
