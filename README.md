HC-SR04 Test Project 

Using this NUCLEO Dev-board: https://www.st.com/en/evaluation-tools/nucleo-f401re.html, and STM32CubeIDE 
Using this ultrasonic sensor: https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf

This repo contains libraries that I've made for Timers, and other functionalities, which can be seen here if you want to test them out and see how to set it up if you're having issues: https://github.com/nmanhas2/LIBRARIES_STM32F401

This project is specifically for the HC-SR04 ultrasonic sensor for ranging purposes. It uses the input capture functionality for the timer TIM2 within the F401RE MCU, SYSTICK timer for a delay, UART2 for transmitting the measured distance, and interrupts for detecting rising and falling edge to determine the pulse width based on the input capture count. 

The first step to begin measuring distance is to bring the trigger pin high for a minimum of 10uS, then bringing it low, with at least a 60mS delay in between turning it high again: 

![image](https://github.com/nmanhas2/HC-SR04_STM32F401RE/assets/113201793/8f7b562a-1393-4e28-a907-64e329d08960)

In response to this, an 8 burst ultrasound signal comes from the echo pin at 40KHz:

![image](https://github.com/nmanhas2/HC-SR04_STM32F401RE/assets/113201793/4344db6a-5407-48d4-9c76-ec5aa3ea6529)

Then finally, an echo pulse outputs from the echo pin with a width corresponding to the distance by using the given formula:

![image](https://github.com/nmanhas2/HC-SR04_STM32F401RE/assets/113201793/51372eed-fd42-414e-bb44-47178335eb6f)

![image](https://github.com/nmanhas2/HC-SR04_STM32F401RE/assets/113201793/7ed24e1b-84c4-4dc2-8747-a90ed8242005)

Within the code, I've setup a state machine that runs through this process using PA1 as an input capture for the echo pin, and PA0 as an output pin for the trigger pin.


