# Hard-Hat Detection using Nicla Vision on Edge Impulse

### Overview:
The Hard-Hat Detection project utilizes the powerful combination of Nicla Vision and Edge Impulse to create a robust and efficient system for identifying individuals wearing hard hats in real-time. This application is specifically designed to enhance safety and compliance in construction sites, industrial environments, and other hazardous locations where the use of protective headgear is essential.\
This dataset contains 852 images of classes ["HAT","HEAD"].
* 682 images (428 "HAT" labels, 412 "HEAD" labels) are used for training.
* 170 images (125 "HAT" labels, 95 "HEAD" labels) are used for testing.

### Project Objectives: 

The primary objective of this project is to develop an end-to-end solution that can accurately detect whether a person is wearing a hard hat or not. By leveraging Nicla Vision's hardware capabilities and the advanced machine learning capabilities of Edge Impulse, the system aims to provide real-time monitoring and alerting, helping mitigate potential risks and ensuring adherence to safety protocols.

### Key Features:
* Real-Time Hard-Hat detection: The system can process video streams in real-time, instantly indentigying individual wearing hard hats within the monitored area.
* Edge processing: By utilizing Edge Impulse's machine larning capabilities, the application can run efficiently on Nicla Vision's edge device, reducing the latency and eliminating the need for cloud-based processing.
* Customizable model: The machine learning model can be trained and fine-tuned according to specific project requirements, allowing easy adaptation to different hard hat designs, lighting conditions, and camera angles.
* User-friendly interface: The project includes a simple and intuitive user interface for easy setup, monitoring, and management of the hard-hat detection system.

## Getting Started:
To use this Hard-Hat Detection application on Nicla Vision and Edge Impulse, follow thse steps:

### Required Dependencies
* Edge Impulse CLI
* Arduino CLI

### [Installing Edge Impulse CLI](https://docs.edgeimpulse.com/docs/edge-impulse-cli/cli-installation#installation-windows)
1. Start by creating an [Edge Impulse account](https://studio.edgeimpulse.com/signup).

2. Install [Python 3](https://www.python.org).
3. Install [Node.js](https://nodejs.org/en) v14 or higher.
    * Remember to check the 'Automatically install the necessary tools. Note that this will also install Chocolatey. The script will pop-up in a new window after the installation completes' check-box in the installation wizard during the installation.
    * It will open a powershell window after the installation wizard of Node.js finishes and install all the necessary tools.
4. Finally open a new cmd terminal (as administrator) and install the edge impulse cli tools with this code
        
        npm install -g edge-impulse-cli --force

### [Installing Arduino CLI](https://arduino.github.io/arduino-cli/0.32/installation/#latest-release)
* Follow this 1 minute, detailed [instruction video](https://www.youtube.com/watch?v=1jMWsFER-Bc) to install Arduino CLI

Upon successful installation of Edge Impulse CLI and Arduino CLI, we are ready to proceed. However, prior to advancing, I would like to share some troubleshooting techniques that have helped me in resolving certain errors encountered during the installation of Edge Impulse CLI. To verify the correct installation of Edge Impulse CLI on your computer, execute the following code on the Windows command prompt:
        
        edge-impulse-daemon --clean
If everything is installed properly it should ask you to enter your login details of your edge impulse account. 

### Troubleshooting Edge Impulse CLI installation 
Download and install `Desktop development with C++` from this link: [Visual Studio](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community) and repeat the steps again.

## Connecting Nicla Vision to Edge Impulse (Windows)
1. Download the [latest edge impulse firmware](https://cdn.edgeimpulse.com/firmware/arduino-nicla-vision-firmware.zip) and extract the zip file.
2. Connect Arduino Nicla Vision to your PC with a micro-USB cable and press the reset button twice to enter the bootloader indicated by flashing green LED on Nicla Vision.
3. Open the file named `flash_windows.bat` from the unziped files, and let the flash script run, once it is finished blue LED should turn on in your Arduino Nicla Vision.
4. Then run this command on a new cmd prompt `edge-impulse-daemon` and log in to your edge impulse account. Then select the project you want Arduino Nicla Vision to connect. `edge-impulse-daemon --clean` can be run if you want to re-login to edge impulse or select a different project to connect your Nicla Vision.
5. Open your edge impulse project in your browser, you should be able to see Arduino Nicla vision in your Devices tab.
<p align = "center">
   <img src="https://user-images.githubusercontent.com/85072523/255311397-a5fd474e-b660-4cbf-986c-5d58e0cdcbe7.png" />
</p>

## Working on Project
### Data Collection
Under the Data Acquisition tab, upload the dataset in respective sets like training and testing which already have mentioned in the directories. The images are pre-labelled by me which are stored in bounding_boxes.labels and info.labels files.
<p align = "center">
   <img src="https://user-images.githubusercontent.com/85072523/255311474-da46e7bf-5608-49a6-a482-4724154bcd3d.png" />
</p> 

You are also welcomed to upload your custom images and go to the labelling queue to label your images.

### Impulse design 
* The following impulse design is used in this project.
<p align = "center">
   <img src="https://user-images.githubusercontent.com/85072523/255311507-2b9a12ea-ce50-43ae-8917-fbe9d6d79957.png" />
</p> 
* After saving the impulse, click on image tab and save the image parameters, click on generate features.

*Generated Features*
<p align = "center">
   <img src="https://user-images.githubusercontent.com/85072523/255311530-ee6ef900-9bc3-46cc-9da1-ae2e900e8564.png" />
</p>

### Model training

Selecting 60 epochs, 0.01 epochs with 20% validation set size for FOMO (Faster Objects, More Objects) MobileNetV2 0.35 model and training is done. The metrics are as follows.
<p align = "center">
   <img src="https://user-images.githubusercontent.com/85072523/255311547-8376f198-b106-4df8-89b1-9b98aee1b5bb.png" />
</p>

### Deployment
After getting satisfactory results in testing, the model is ready to be deployed. In the development options, Arduino Nicla Vision is selected and click on Build; a zip file will be downloaded.

Extract the zip, to find the `flash_windows.bat` file.

Connect the Nicla vision if not, to the pc and execute the bat file. Let it finish.

Now you can run the inference on the edge device by using 
`edge-impulse-run-impulse` command.

Run the following command to show the classification results with the live camera feed on your browser. This command will give you a web url which you can open to see the live calssification results.

        edge-impulse-run-impulse --debug

### Live classification

<div style="display: flex;">
  <div style="flex: 1;">
    <img src="https://user-images.githubusercontent.com/85072523/255311562-eb9ff985-e256-4895-b253-baeb8de446e9.png" alt="HAT">
  </div>
  <div style="flex: 1;">
    <img src="https://user-images.githubusercontent.com/85072523/255311572-2b40f2ca-d99d-468f-8ae9-6b0e9614f49d.png" alt="HEAD">
  </div>
</div>

### Author

This project is developed by **Kalavakuri Abhinay**.

### Data Source
https://www.kaggle.com/datasets/vodan37/yolo-helmethead , https://public.roboflow.com/object-detection/hard-hat-workers/2
