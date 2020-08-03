# Cyclocomputer-CC-PA100W-weak-signal-and-clone-possible
STEM project, to learn and practices.  One of customers is telling the dissatisfaction, what, why & how.  
  
It is one day project, the target, a "fancy" product with new name to us - "Cyclocompetuer". User told that malfuction intermittent as no blinking of counting during biking. To complete & writting the report of project has more than weeks and slowly, not a single day event because no urgent.  

Verify the case and used what learned for STEM project.  
  
1) RF signal transmission and reception, mimic RPM singal without real biking, nor uses the original RPM transimitter.  
2) PWM and smaller brush motor speeding control, to mimic the biking to produce RPM signal; ADC for set point;  
3) Coding technique for simple scalling & filtering, i.e. ADC range 0-1023, mapping to speed setting 0-63; ADC result filteried, more immunity to noise, steady ADC reading;  

### odometer & RF signal for RPM
According to user, a brand named product, few years aged model, https://www.cateye.com/files/manual_dl/9/965/CC-PA100W_HP_TC_v2-1.pdf. It is a 19 KHZ transmitter with a reed relay, wheeling per revolution detected, sent two pluses via RF singal to odotometer.

### theory
Operation, rolling magnet trigger the reed relay, RF signal generator pulsing ASK (Amplitude Shift Keying) signal to odometer. Counting event against time, odometer could be used to display many function of time related, for example speed, trip distant, ect.
