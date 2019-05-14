# ANIMA
This README file is going to take you through all the steps needed in order to create your own version of the plant-based synthesiser project, ANIMA
## Step One - All the right tools
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
## Step two - Setting up the Arduino
The arduino board should be set up as shown in figure 1 and figure 2. There are no charged ends within this circuit so the send and receive cable can run in either position (https://www.youtube.com/watch?v=stejKa03tdw). The purpose of the capacitive sensor pad is to pick up any changes in the electric potential within the plants leaf (https://www.bareconductive.com/make/what-is-capacitive-sensing/), however any conductive object can be used in place of these pads (e.g. conductive paste, crocodile clip, etc.)
