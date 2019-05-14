# ANIMA
This README file is going to take you through all the steps needed in order to create your own version of the plant-based synthesiser project, ANIMA
## Step 1 - All the right tools
Before advancing any further with this project, it is important that you have all the tools you will need to successfully create your own working version of Anima. You will need the following items before you go any further:
- 1x Arduino board
- 1x Breadboard
- 1x Capacitive sensor
- 3x Male to male solderless breadboard jumper cables
- 1x 1MΩ Resistor
- 1x Plant (preferrably one that has leaves with a relatively large surface area)
- 1x USB Printer cable with A to B ends
- Arduino software, which can be downloaded here: https://www.arduino.cc/en/Main/Software
- Pure data software, which can be downloaded here: https://puredata.info/downloads
-- Please note the version of Pure Data used in ANIMA is pd Vanilla, however, when using vanilla you may have to install some externals in order to get the patch to run correctly. A guide to help you figure out how to install externals can be found here: https://puredata.info/docs/faq/how-do-i-install-externals-and-help-files
## Step 2 - Setting up the Arduino
The arduino board should be set up as shown in figure 1, figure 2 and figure 3. There are no charged ends within this circuit so the send and receive cable can run in either position (https://www.youtube.com/watch?v=stejKa03tdw). The purpose of the capacitive sensor pad is to pick up any changes in the electric potential within the plants leaf (https://www.bareconductive.com/make/what-is-capacitive-sensing/), however any conductive object can be used in place of these pads (e.g. conductive paste, crocodile clip, etc.)

Figure 1: Image showing how the Arduino board and breadboard should look in your own version of ANIMA
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224538.jpg "Arduino and breadboard")

Figure 2: Image showing the way in which the jumper cables were added to the Arduino board in order to carry a signal from the capacitive sensor.
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224559.jpg "Arduino close-up")

Figure 3: Image showing how the breadboard should look when creating your own version of ANIMA. _Remember: There are no charged ends within this circuit, so this is just an example of how you can set it up, if yours differs slightly, it shouldn't have any effect on the data your circuit collects_.
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224614.jpg "Breadboard close-up")

Figure 4: A print-screen showing the circuit diagram that was used as a guide when putting the hardware components of ANIMA together. 
![alt text](https://github.com/antoniawork2813/Anima/blob/master/circuit.png "Anima circuit")
### Step 2a
a.	After you have set your board up correctly and the arduino software has been installed on your computer, please install the following code:
    
```
#include <CapacitiveSensor.h>

CapacitiveSensor   cs_2_4 = CapacitiveSensor(2,4);        // 10M resistor between pins 4 & 2, pin 2 is sensor pin, add a wire and or foil if desired

void setup()                    
{
   Serial.begin(57600);
}

void loop()                    
{
    long start = millis();
    long total1 =  cs_2_4.capacitiveSensor(30);


    Serial.print(millis() - start);        // check on performance in milliseconds
    Serial.print("\t");                    // tab character for debug windown spacing

    Serial.println(total1);
    
    delay(1000);                             // arbitrary delay to limit data to serial port 
}
```
As I wasn’t particularly familiar with Arduino or the coding language its software uses, I thought the best option to create an effective working demo of Anima, would be to use the code created by https://www.youtube.com/watch?v=stejKa03tdw. I knew it worked and served the exact purpose that was needed for my computer to be able to read the data being picked up by the Arduino.
- It should be mentioned that for the code above to work effectively, you will need to install the CapSense library into your computational device. The CapSense library can be found by following this link: https://playground.arduino.cc/Main/CapacitiveSensor/.
- Once the file has been downloaded and unzipped it needs to be installed in Arduino/hardware/libraries/ (https://playground.arduino.cc/Main/CapacitiveSensor/). _The Arduino file should be located where your operating system stores its program files_.

Once the code has been copied into the Arduino editing window, the next step is to connect the arduino board to the computer using the USB printer cable, mentioned in step one. After this is done and the Arduino board lights up (demonstrating that is working), upload the code in the Arduino editing window to the board. Provided the software has been setup correctly and the comport in the code matches the one assigned within the program; the code should successfully upload to the board.

**The reason I decided to use an Arduino for this project as opposed to an already complete unit like the _MIDI sprout_ was primarily to do with cost. The components to make my own plant-based synthesisers were collectively a lot less expensive than pre-made commercial models, such as the _MIDI sprout_, which retails for about $300.**
## Step 3 - Getting Pure Data and Arduino to communicate with each other
