# Cyclocomputer-CC-PA100W-weak-signal-and-clone-possible
### STEM project, to learn and practices.  One of customers is telling the dissatisfaction, what, why & how.  
  
It is one day project, the target, a "fancy" product with new name to us - "Cyclocompetuer". User told that malfuction intermittent as no blinking of counting during biking. To complete & writting the report of project has more than weeks and slowly, not a single day event because no urgent.  

Verify the case and used what learned for STEM project.  
  
1) RF signal transmission and reception, mimic RPM singal without real biking, nor uses the original RPM transimitter.  
2) PWM and smaller brush motor speeding control, to mimic the biking to produce RPM signal; ADC for set point;  
3) Coding technique for simple scalling & filtering, i.e. ADC range 0-1023, mapping to speed setting 0-63; ADC result filteried, more immunity to noise, steady ADC reading;  

### Odometer & RF signal for RPM
According to user, a brand named product, few years aged model, https://www.cateye.com/files/manual_dl/9/965/CC-PA100W_HP_TC_v2-1.pdf. It is a 19 KHZ transmitter with a reed relay, wheeling per revolution detected, sent two pluses via RF singal to odotometer. FCC ID https://fcc.report/FCC-ID/ON5SPDSENSORA, designed in year 2005.  

### Theory
Operation, rolling magnet trigger the reed relay, RF signal generator pulsing ASK (Amplitude Shift Keying) signal to odometer, it was said 70cm aprat in maximum, test result, this unit pair was no better than 45cm apart otherwise no singal. On the other hands, 99.9km/h is max, over plusing, no RPM counting was capable; low end 3.3km/h was able to display; Counting event against time, odometer could be used to display many functions of time related, for example speed, trip distant, ect.  
  
  
### Journey of the practices  
build the test rig, clone the RF signal, try to mimic RF single, confirmed RF 19KHZ ASK signal

build the "wheeling" jig, trigger original RF transimitter, mimic real biking. Rotating of two magnets, mimic the wheeling sucessufuly, 5V power and PWM control to the motor, it is easy and govenered slow RPM. Starting low PWM is not possible as load and friction, PWM ratio of 40/255 to 63/255 seems the best fit for the case and the specific small motor. One transistor is good enough, 2N3904 or MJE800, both tested as works well, general NPN would be fine;


### code and hints
These code build with Arduino IDE, under laying is actual avr-gcc, some mix of pure C and/or Arduino C++.

### Filtering and easy 8 bit MCU (AVR or Arduino Nano / Uno)  
Many online tutorial was telling to sum as many as possible sample from ADC, kicks out max/min, find the average, some sort of similar to MOVING AVERAGE method. It was ok and works, but what is the point to count so many and averaging. There is trick could be used, uses RC filter in hardware before feeds input to ADC, one resistor and one capacitor (integrator) will do the job, usually 10K/0.01uF. One advance trick is using software to build such RC filtering, simple, fast & better than hardware RC filter, code snippet following, FILTER_SHIFT is RC constant, the greater number the longer response time and vise versa. I did not invented this but learned from those someone who was working for NASA & Appollo, it is fun of learning and finally understood the beauty of code / algorithm design.
```  
   uint16_t s = analogRead(A5); // speed setting  
   
   FILTER_SHIFT =2;  
   integrator = integrator - (integrator >> FILTER_SHIFT) + s;  
   s = integrator >> FILTER_SHIFT;  

```  



### conclusion
the smaller brush motor and open-loop control, easy for wheeling and testing
