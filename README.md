# Pet feeder - Jetson nano project
This pet feeder uses the NVIDIA Jetson Nano Developer kit to monitor whether a (pet)bowl is empty or full. If empty it looses its Jetank gripper (which should be around a food-bag and then letting the food out) and when full it closes the grip again. 
 
## Requirements and Setup
Jetson Nano Developer Kit - with a recent JetBot SD card image (jetpack v 4.5 and jetbot v 0.4.3 was used in this project) 

Camera (CSI Camera recommended as some adjustments needs to be made for USB Camera)

Adding JETANK for grabber-functionality:

```bash
git clone https://github.com/waveshare/JETANK.git 
cd JETANK 
chmod +x install.py
chomd +x config.py
./install.sh
./config.sh
```
Further information can be found on https://www.waveshare.com/wiki/JETANK_AI_Kit

## Build & Run
### Option 1 - using already created model
Run *live-demo.ipynb*. This will use the model *model_trt.pth* that has been created through the steps below and with a dataset of 200+ pictures of both full and empty bowls. This will show the predictions in a window in the browser and the gripper will work live.

### Option 2 - train your own
For this option the following steps needs to be perform:
1. ***Collect data:*** run *collect-data.ipynb* to collect images of empty/full bowls
2. ***Train:*** run *train.ipynb* to train the neural network. Change the name of the model if you do not want to overwrite the current *model.pth*
3. ***Build TensorRT model:*** run *train.ipynb* using TensorRT to optimize the neural network model trained. Change the name of the model if you do not want to overrun the current *model-trt.pth*
4. ***Run:*** Same as above. Run *live-demo.ipynb* that will show the predictions in a window in the browser and the gripper will work live

## Features/Examples
### Measuring empty/full in probability
This the output in the browser window when running *live-demo.ipynb* with bowl-examples

![Probability of full/empty bowl](examples/gif-prob-bowl.gif)

### Food dispenser
As part of the project I attempted to set up an imporvised dispenser as can be seen in some of the examples. This mostly consisted of a bag hanging from a mic-stand, with a hole that the Jetson either could grip shut or open. In some of the other examples, food is being poured simply to demonstrate what the gripper does.

### Opening/Closing grip
This shows how the grabber opens or closes depending on how empty/full the bowl is (in this case the food is just dropping down as an example to fill the bowl)

![Grabber opening/closing](examples/gif-grabber.gif)

### Examples of live demo
This shows how the program works with a "bag-dispenser" on top of the grip that lets out food til the bowl is full (note: in this example the setting for full was very low to demonstrate it closing the bag)

![bowls full or empty](examples/gif-bag-bowl.gif)


