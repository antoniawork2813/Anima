# ANIMA
This README file is going to take you through all the steps needed in order to create your own version of the plant-based synthesiser project, _ANIMA_
## Step 1 - All the right tools
Before advancing any further with this project, it is important that you have all the tools you will need to successfully create your own working version of _ANIMA_. You will need the following items before you go any further:
- 1x Arduino board
- 1x Breadboard
- 1x Capacitive sensor (_You may have to srip back the plastic covering on the end of wire, in order to expose the metal beneath. You should then be able to attach the jumper cable using any form of non-conductive cohesive. **Make sure the cohesive does not stop the two wires from physically connecting with each other**_) 
- 3x Male to male solderless breadboard jumper cables
- 1x 1MΩ Resistor
- 1x Plant (preferrably one that has leaves with a relatively large surface area)
- 1x USB Printer cable with A to B ends
- Arduino software, which can be downloaded here: https://www.arduino.cc/en/Main/Software
- Pure data software, which can be downloaded here: https://puredata.info/downloads
-- Please note the version of Pure Data used in _ANIMA_ is pd Vanilla, however, when using vanilla you may have to install some externals in order to get the patch to run correctly. A guide to help you figure out how to install externals can be found here: https://puredata.info/docs/faq/how-do-i-install-externals-and-help-files

**You should find two folders in this repository named _Setting up your circuit - Steps_ and _Setting up your circuit - Equipment_. In _Setting up your circuit - Equipment_ you should find images of each item you will need to build your circuit. In _Setting up your circuit - Steps_ you should find images illustrating how to physically set the circuit up**
## Step 2 - Setting up the Arduino
The arduino board should be set up as shown in figure 1, figure 2 and figure 3. There are no charged ends within this circuit so the send and receive cable can run in either position (https://www.youtube.com/watch?v=stejKa03tdw). The purpose of the capacitive sensor pad is to pick up any changes in the electric potential within the plants leaf (https://www.bareconductive.com/make/what-is-capacitive-sensing/), however any conductive object can be used in place of these pads (e.g. conductive paste, crocodile clip, etc.)

_Figure 1: Image showing how the Arduino board and breadboard should look in your own version of _ANIMA__
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224538.jpg "Arduino and breadboard")

_Figure 2: Image showing the way in which the jumper cables were added to the Arduino board in order to carry a signal from the capacitive sensor._
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224559.jpg "Arduino close-up")

_Figure 3: Image showing how the breadboard should look when creating your own version of _ANIMA__. _Remember: There are no charged ends within this circuit, so this is just an example of how you can set it up, if yours differs slightly, it shouldn't have any effect on the data your circuit collects_.
![alt text](https://github.com/antoniawork2813/Anima/blob/master/IMG_20190512_224614.jpg "Breadboard close-up")

_Figure 4: A print-screen showing the circuit diagram that was used as a guide when putting the hardware components of _ANIMA_ together_. 
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
As I wasn’t particularly familiar with Arduino or the coding language its software uses, I thought the best option to create an effective working demo of _ANIMA_, would be to use the code created by https://www.youtube.com/watch?v=stejKa03tdw. I knew it worked and served the exact purpose that was needed for my computer to be able to read the data being picked up by the Arduino.
- It should be mentioned that for the code above to work effectively, you will need to install the CapSense library into your computational device. The CapSense library can be found by following this link: https://playground.arduino.cc/Main/CapacitiveSensor/.
- Once the file has been downloaded and unzipped it needs to be installed in Arduino/hardware/libraries/ (https://playground.arduino.cc/Main/CapacitiveSensor/). _The Arduino file should be located where your operating system stores its program files_.

Once the code has been copied into the Arduino editing window, the next step is to connect the arduino board to the computer using the USB printer cable, mentioned in step one. After this is done and the Arduino board lights up (demonstrating that is working), upload the code in the Arduino editing window to the board. Provided the software has been setup correctly and the comport in the code matches the one assigned within the program; the code should successfully upload to the board.

**The reason I decided to use an Arduino for this project as opposed to an already complete unit like the _MIDI sprout_ was primarily to do with cost. The components to make my own plant-based synthesisers were collectively a lot less expensive than pre-made commercial models, such as the _MIDI sprout_, which retails for about $300.**
## Step 3 - Getting Pure Data and Arduino to communicate with each other
After the Arduino has been setup and the code uploads to the board, without any error messages, the next task is then getting the Arduino and Pure Data programs to communicate with each other. The best way of doing this is by using the Serial Print patch created by alexdrymonitis. 
Serial print “facilitate(s) the communication” between Pure Data and Arduino, making it much easier to work across both platforms. The serial print patch can be found here: https://github.com/alexdrymonitis/Arduino_Pd
_Once the file has been downloaded and unzipped, you will need to keep the pd patch you are using for this project, in the same folder as the unzipped files. Failure to do this may result in the [serial_print] object not functioning within your patch._
### Step 3a
In order to test that the system is functioning correctly, attach a [print] object to the left inlet of the [serial_print any] object. You should then be able to see some numbers begin to appear in the pure data command window. These numbers should vary depending on your proximity to the capacitive sensor pad. When you are close or touching it, the numbers should begin to increase and when you let go or move away from the pad the number should decrease.

**Serial Print was suggested as a useful and quick method of getting Arduino and Pure Data to communicate with each other. It would probably have been possible to achieve communication without the use of serial print but, once again, as I was not greatly familiar with Arduino, doing that may have proven to be a long and time consuming task that may have affected quality of the end product of this project. As I have frequently found with coding, most things that you could potentially need for a project have already been made by someone else. It can often be save a lot of time by using their code as a reference and perhaps making slight adjustments to better suit your own work.**
### Step 3b
As the data, from the Arduino board, comes into pure data, the desired numeric value is going to be prefixed by another number (typically 1, 2 and occasionally 3). This other number is not integral to _ANIMA_ and can interfere with the rest of the patch. In order to get pure data to ignore this value an [unpack f f] object needs to be connected to the left outlet of the [serial_print any] object. The [unpack f f] object separates the numerical values and stores them as floats. The first float will be output from the left outlet of the object and the second float, (the one that we need for this project), will be output from the right outlet. A number box can be added to that right outlet, just to ensure the right number is being output.
## Step 4 - Gestural control
### Step 4a - [moses] objects
An object named [moses 30] is attached to the outlet of the number box mentioned in **Step 3b**. Moses objects will compare incoming numbers to the control value specified, (in this case it would be 30). It then outputs the numbers from the left outlet if they are less than the control value and output the numbers from the right outlet if they’re greater than or equal to the control value.
The [moses] object was particularly useful as it allowed for the easy control of high volumes of random data coming in through the Arduino board, this data could then be easily directed to its intended location. 
In _figure 5_ located below, you can see that there are many [moses] objects attached to each other. These objects are attached via the right outlet to the left input. This means that as a value that is greater than or equal to the previous [moses] object comes into the new [moses] object, it will be compared to the control value of that object. This value will be output to the left if it is less than the control value and to the right if it’s greater than the control value. This [moses] object is then connected to another [moses] object and the process repeats until the chain is stopped. 
Every [moses] object has a number box attached to the left outlet. This allows for visual confirmation that the correct numerical data is being passed through the objects. The number box is then attached to a bang object that triggers every time the numerical value changes.

_Figure 5: Print-screen demonstrating how the [moses] objects have been utilised in this first section of the patch entitled Guitar_specdelay~-main_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/%5Bmoses%5D.png "[moses] chain 1")

**The number of [moses] objects may seem excessive; however, it was necessary in order to give _ANIMA_ the ability to control the sound via gestural actions. By including this many [moses] objects with increasing control values, the patch is able to detect how close a person is to the plant and how long they physically interact with the plant. 
The gestural control is one of the key elements of _ANIMA_ as it gives participants the opportunity to hear how quickly the plant reacts to their presence and to their touch, further proving and helping them understand that plants have some level of intelligence and are highly aware and responsive to their surroundings.**

There are 63 [moses] objects in the patch, which have all been sorted into groups of 3. The bang objects, attached to the number boxes of each individual [moses] object, are then attached to a [random] object. [random] objects output random integer values between 0 and the given control value.
_For example, the first [moses] object in the chain is connected to a [random 30] object, the control value in this instance is 30, so the object being output by this object will be between 0 and 30_. 

### Step 4b - [random] objects
Seven [random] objects have been used, as can be seen in _figure 6_. The purpose of these [random] objects is to randomly output an integer, (within the specified range), that will then trigger another set of [moses] objects. 
This second set of [moses] objects have been separated into 7 groups of 2 and each [random] object is connected to one of those groups of 2 (_see figure 6_). As the [random] object outputs an integer it will enter the [moses] chain and trigger one of the objects, depending on the value that has been output and the specified range of each [moses] object. 
A bang object has been added to the left outlet of each of these [moses] objects, as can be seen in _figure 6_. These bang objects have then been attached to the left input of 1 of 7 sub-patches in pd. This means that as the value output from the [random] object, triggers one of the [moses] objects in its chain (and subsequently the bang attached to the left output), it will trigger the content of the sub-patch it is attached to the left inlet of. 

_Figure 6: A print-screen showing how the [random] and [moses] objects are connected in order to randomly select and trigger different samples within the patch_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/%5Bmoses%5D2.png "[moses]2")


## Step 5 - Creating a sampler
When you open one of these sub-patches it should look like the one shown in _figure 7_. The content of these patches were based on the sampler patch created by cheetomoskeeto in a YouTube video, which can be found here: https://www.youtube.com/watch?v=boX0v54SqtU. If you follow the link you will find a full tutorial an explanation for each individual element within this sub-patch.  

_Figure 7: A print-screen image showing how the sampler in each subpatch should be set-up. The only feature that should differ between each sub-patch is the sample that is used and therefore the playback speed of that sample as well_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/Sub-patch.png "Sub-patch sampler")

**The audio samples that have been used for these patches can be found in the zip file named _ANIMA_. The reason that samples have been used, instead of the oscillators available in Pure Data, is because this patch was designed to sound as musical as possible and be somewhat ‘pleasant’ to listen to. It was felt that randomly triggering different oscillators and varying the frequencies of them, did not accomplish that, and instead created something that sounded too much like the stereotypical sound associated with a computer churning out a lot data (which can be heard in the _pieces for plants_ video { https://vimeo.com/63343503}). Using samples of notes within a musical scale was an easy and effective way of making the patch feel more musical, whilst still retaining the random and unpredictable nature of the data being output by the plant.**

The patch is largely the same as the one created in the video tutorial by cheetomoskeeto, however, a few minor additions have been added to make the patch better suit the project.
A [loadbang] object has been added to the bang object at the top of the patch, this was done to make sure that as soon as the patch is opened the samples are loaded and ready to be triggered. However, the samples automatically start playing as soon as they’re loaded so the same [loadbang] object was also added to the inlet of the message box that reads 0, which can be seen in _figure 7_. The 0 in the message box is attached to the inlet of the [phasor~] oscillator. By triggering the 0-message box a non-signal message is sent to the [phasor~] object in the patch, which stops the sample from playing. 
### Step 5a - Triggering the samples
Two [inlet] objects have also been created in this patch. The first [inlet] object is attached to another message box that contains the playback speed of the related sample. As the bang triggered by the [moses] object, mentioned in **Step 4b**, travels into the first inlet, (which will appear on the left of the sub-patch), it triggers this message box which then causes the sample to begin to play.
b.	The second [inlet] object is attached to the same 0 message box, as the [loadbang] object, so any command attached to the right inlet of the sub-patch will automatically stop the sample from playing. As can be seen in _figure 6_, the outlet of each bang object, (connected to a [moses] object), is connected to the left inlet of its assigned sub-patch **and** the right inlet of the other sub-patches. This means that as one of the samples is triggered, it automatically stops any other samples from playing at the same time. **This stops the system from overloading and causing issues in the overall signal being output from the patch**. Two [outlet] objects have also been added to each of these sub-patches, so the signal could be sent out as a stereo signal from both the left and right outlets.

**Each sub-patch is setup in the same way, the only thing that differs between each of them is the sample that is loaded into the patch. All the audio samples used in _ANIMA_ can be found in the folder named _CapacitiveSensorSketch_**.
## Step 6 - Adding effects
As the audio signal leaves the sub-patches, (from both the left and right outlets), it is then directed into two amplifiers ([*~ 1]*). The left outlet is attached to the left [*~ 1]* and the right outlet is attached to the right [*~ 1]*. These objects increase the output of the signal being sent through the system (_see figure 8_).
### Step 6a - [freeverb~]
Each [*~ 1]* object is attached to the left and right inlet, respectively, of a [freeverb~] object (_see figure 8_). [freeverb~] is a stereo reverb unit within pure data. This was added to the signal to give it some ambience and make it more interesting to listen to. Attached to the right inlet of the [freeverb~] object are three variable commands; wet, dry and roomsize. In the _figure 9_ you can see each variable is set up in the same way. They have a slider, (that has a range between 0 and 1), which is then attached to the inlet of a message box that features the variable name and a $1 value. This lets the [freeverb~] object know which variable is to be controlled, then the value of the slider replaces the $1 value in the message box.

_Figure 8: Print-screen showing the [freeverb~] object and its variable controls_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/%5Bfreeverb%5D.png "[freeverb~]")

### Step 6b - Guitar Specdelay~
The signal then travels from the left and right outlet of the [freeverb~] object and into an abstract named Guitar_specdelay~ (_see figure 9_). This abstract was originally part of a file downloaded from: https://guitarextended.wordpress.com/2012/02/07/spectral-delay-effect-for-guitar-with-pure-data/. 
Spectral delay pd patch was originally intended to be used as an effect for a guitar, however, it has been repurposed to be used in Anima. The patch adds reverb as well as a chorus-type delay effect that repeats and distributes the harmonics of the incoming signal all over the frequency spectrum (https://guitarextended.wordpress.com/2012/02/07/spectral-delay-effect-for-guitar-with-pure-data/.). This creates an interesting ambient effect that can be added on top of the already existing [freeverb~] object to make the samples being triggered sound even more atmospheric and ambient and a more interesting for the participant to listen to.

_Figure 9: Print-screen showing the Guitar_specdelay abstract that was used to add ambience to the samples being triggered_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/Guitar_specdelay~.png "Guitar_specdelay~")

## Step 7 - Output
The output of the Guitar_specdelay~, is then connected to two [*~]* objects, one that represents the left stereo input and one that represents the right stereo input. These act as amplifiers, giving the signal a final boost. The value that this signal will be amplified by is determined by the slider connected to the left input of each command box. These values will be between 0 and 0.5 as that is the range of the slider. 
Finally, the left and right amplifiers ([*~]*) are attached to the left and right input of a [dac~1 2] object. The 1 and 2 in the object box specifies that this signal should be in stereo (_see figure 9_).

## Bonus Step
In order to hear the audio being sent out by the patch, the DSP box in the command window of Pure Data will have to be switched on, which can be done manually. However, if you wish for this to automatically switch on when you open the patch then you should include the following in you patch (_see figure 10_)

_Figure 10: Print-screen image of the pure data command needed to automatically turn the DSP when the patch is opened_
![alt text](https://github.com/antoniawork2813/Anima/blob/master/DSP.png "DSP control")
# Demonstration
An explanation and demonstration of _AMINA_ has been created and can be found by following this link: https://youtu.be/7wf1yl4Ea4s
