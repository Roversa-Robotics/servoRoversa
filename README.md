# servoRoversa

Simple library for basic controls of Roversa using [codal-microbit-v2](https://github.com/lancaster-university/microbit-v2-samples) servo examples to control the Feetech FS90R continuous servo motors. This allows input values to be mapped onto the existing servo functions in the library. This can easily be modified to take any input and map its ranges onto the servo functions.

This assumes that your servo has a range of 700μs - 2300μs, neutral at 1500μs, and a frequency of 50Hz. Tune and test your motor before running all functions. All functions with parameters assume `function(left motor speed, right motor speed)` and will be in percentages up to 100. This also assumes that the left motor is on `MicroBit.io.P1` and the right motor is on `MicroBit.io.P2`. 

To use the library, add:
`#include "servoRoversa.h"`
to **main.cpp** to leverage the basic driving functions of Roversa.

For example in **main.cpp**:
```cpp
#include "MicroBit.h"
#include "servoRoversa.h"

MicroBit uBit;

main(){
    uBit.init();
    while(1){
        drive(100,100);      //drive forward at 100% speed
        uBit.sleep(1000);
        drive(-100,-100);    //drive backward at 100% speed
        uBit.sleep(1000);
        forward(100,100);    //forward at 100% speed
        uBit.sleep(1000);
        reverse(100,100);    //reverse at 100% speed
        uBit.sleep(1000);
        left(100,100);       //left turn at 100% speed
        uBit.sleep(1000);
        right(100,100);      //right turn at 100% speed
        uBit.sleep(1000);
        drive(50,50);        //drive forward at 50% speed
        uBit.sleep(1000);
        reverse(50,50);      //reverse at 50% speed
        uBit.sleep(1000);
    }
}
```

`drive(int,int);`

The drive function ranges from -100 to 100 percent to control direction and speed in each motor. The first parameter is the left motor speed/direction and the second is the right motor speed/direction. This allows you to move a motor forward and backward ranging all speeds. 100% moves each motor at full speed in the forward direction or left motor CCW and right motor CW. -100% moves each motor at full speed in the backwards direction or left motor CW and right motor CCW. 0 is neutral position.

`forward(int,int);`
`reverse(int,int);`
`left(int,int);`
`right(int,int);`

The forward, reverse, left, and right all range from 0-100 percent in the left and right motors. Directions are preset per function so you just need to give each motor a speed. Enter left motor then right motor in parameters.

`stop();`

The stop function writes the GPIO low to ensure that no signal is being sent to the motors.

`neutral();`

The neutral function sends a 0 analog signal or 1500μs pulse to each motor.
