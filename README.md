# EV Simulation
Created from a starter repo for the Capstone project in the [Udacity C++ Nanodegree Program](https://www.udacity.com/course/c-plus-plus-nanodegree--nd213).

## Udacity Blurb
The Capstone Project gives you a chance to integrate what you've learned throughout this program. This project will become an important part of your portfolio to share with current and future colleagues and employers.
In this project, you can build your own C++ application starting with this repo, following the principles you have learned throughout this Nanodegree Program. This project will demonstrate that you can independently create applications using a wide range of C++ features.

## My take on the Captone Project
I decided this project should be to create something that expands on what I do daily.
For this to be the case I have listed a few key focus points:
* Automotive based
* Cutting edge modern and future technology
* Vehicle modification
* ECU calibration
* Tuning

## Description of EV Simulation
EV Simulation is a combination of my daily work, mixed with the future of my industry. As an automotive diagnostic director and well established vehicle tuner I have taken note that the automotive industry is moving away from internal combustion and towards electrified vehicles and hybrids.
Being a field in which I have a profound knowledge it seemed like a good choice for the Capstone Project.
This project creates a massively simplified electric vehicle motor through the creation of an object of type Calibration (calibration meaning specification of motor operating parameters and sensor calibration).
It then drives this electric motor through a simple simulated course and reports the time from start to finish.

It does this not once, but with several different motor calibrations all being driven through several different simulated scenarios to find the best motor calibration overall under several usage conditions.

## Assumptions
* EV motor runs at constant rpms for each sector.
* If zero speed is reached during testing then test fails.
* If test end is reached then the test is considered a success.
* Torque effort required to maintain constant velocity simulates various inclines that vehicle may climb.
* Torque output beyond required effort creates acceleration and below required effort creates deceleration.

## Order of execution
1. Vector of motors is created and loaded with calibration files of type .map found within folder ./datafiles.
2. Vector of simulations is created and loaded with simulation files of type .sim found within folder ./datafiles.
3. Simulation 1 shared_ptr. Simulation 1 method started as thread for each motor calibration
4. Wait for simulation 1 to end then write results to terminal for each calibration.
5. Best calibration for this sim stored in vector.
6. Next simulation starts (loop through all sims displaying result on terminal and storing best in vector).
7. Count number of wins by each calibration.
8. Write to terminal best overall calibration based on which came out top of the most simulations.

## Dependencies for Running Locally
* cmake >= 3.7
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build / Run Instructions
1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./EVSim`
5. Either input file locations and extensions or allow defaults - extra datafiles2 folder to test user input

## Source Files - Found within src folder
* main.cpp - `main method. Loads calibrations and simulations. Launches simulation. Organises results to display them to terminal`
* AnalogSensor.cpp - `Creates analog sensor object. Can be a voltage between specified min and max. Specifically used for throttle position in this sim`
* Calibration.cpp - `To build a sim motor. This file creates the class Calibration. Calibration relies on the AnalogSensor.cpp and datafile .map to create an object that resembles an electric vehicle motor with tps and "3D" torque map`
* Simulation.cpp - `Creates a simulation environment of class Simulation. Loads sim data and contains methods to run simulation. Returns time vehicle would have taken to complete course`
* SortResults.cpp - `Contains functions specific to sorting the results and to return the best results`
* Result.h - `Creates a struct Result. This is used to hold the results in varying ways throughout the program, including std::vector<Result> etc`

## Data Files - Found within datafiles folder
* Pay attention to how the data files are created as they are read line by line. The `Key` of each line can be named anything, but I suggest the name remains the same for continuity and easy visual representation of data that follows.
* Data in files is blank space seperated. For example TPS 0.4 4.7 is ready by the code as variables KEY >> Min >> Max.
* If in doubt don't modify these data files as no checking is done for correct data on each line.
* Don't introduce extra lines including blank space lines into these files.

## Rubric Points Used
* Loops, Functions, I/O   `For loops and while loops throughout, plus the project is well organised into functions and methods`

* Reads data from a file  `main.cpp L19-30 contains a function to return the path to specified files.`
                          `Calibration.cpp reads data from file L131-178`
                          `Simulation.cpp reads data from file L18-51`

* Accept user input       `Main.cpp L47 - 74 - Asks user to input file paths and extensions`

* Uses OOP techniques     `Examples throughout`

* Classes use appropriate access specifiers `Calibration.h, Simulation.h and AnalogSensor.h - examples throughout`

* Initialization lists    `Classes Calibration, Simulation and AnalogSensor use initialization lists`

* Abstract implementation details from interfaces `Examples throughout`

* Encapsulate behaviour   `Easily seen in examples of Simulation.cpp and Calibration.cpp. SortResults.cpp although not a class, encapsulates all sorting functions into one file`

* Pass by reference       `Several places but one example is Calibration.cpp L16 & L23`

* Smart Pointers          `Main.cpp L83, 84, 90, 96 - Examples through Simulation.cpp also`

* Multithreading          `std::async used in main.cpp L111`

* Promise / Future        `main.cpp L107 vector of futures - results using .get() on L115`

* Mutex                   `Mutex used in Simulation.cpp L69, 71, 77, 79 and other locations to give sole access to terminal output so as not to get muddled output from multiple threads`
