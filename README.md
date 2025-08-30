
# Application 1
## Name: Vy Nguyen UCFID:5490419

### Project Links: - [Wokwi Simulation](https://wokwi.com/projects/440568718488538113) 

**Q1. Vary Priorities: Change the print task’s priority to 2 (higher than blink’s 1). With such short tasks and delays, you may not notice a big difference, but in principle the print task would preempt the blink task if it were ready. Given both tasks spend most time sleeping, the effect is minimal. In later projects with CPU-bound tasks, priority will matter more. Does anything happen to the LED if you increase the delay within the print task? What if you increase the number of characters printed?**

I pumped up the delay to 50000ms and increased the number of characters but nothing happened. This means for blink task to be affected, my delay has to be nigger and the character increase can be more.

**Q2. Increase Load: Remove the vTaskDelay in the print task (making it a tight loop printing continuously). Be careful – this will flood the console. But it illustrates a point: if one task never yields, it can starve the other. In this case, the LED might stop blinking on schedule because the print task hogs the CPU. This is a starvation scenario, leading into Project 2. If you try this, reset it back after observing a few lines, to avoid crashing your serial output. Describe the behavior you observed.**

As expected the print task was dominated, kept printing while the LED stayed on and no blinking.

**Q3. Thematic Customization: If you chose the space context, perhaps change the printed message to “Telemetry OK” or similar. In healthcare, print a pseudo heart rate. In security, print sensor status.  Assume you were a developer of one of these applications - might there be some considerations that you would want to take into consideration in how verbose (or not) you want your messages to be? Additionally, explain why this system benefits from having correct functionality at predictable times.**

My approach is healthcare. I wouldn't want my system to be verbose. For example a vitals monitor should only print the name and measurement of what it is measuring, we do not have to explain anything, that would be a healthcare worker job. If we have a heart rate mornitor something like "Heart rate: ..." is enough, the healthcare workers will intepret that number and giving the course of action and we want them to make it fast and accurate so being verbose is not a good choice. Correct functionality at predictable times in healthcare domain is crucial since it can help saving people life if a sudden change happened and we can't show what vitals are bot good on the monitor in times, the healthcare workers would not know what to do.

**Q4. Identify/Verify the period of each task; you can try to do this via the simulator, or perhaps by printing data to the console, or connect the outputs to the logic analyzer.**

a. Describe how you measure the periods:
I used "pdTICKS_TO_MS (xTaskGetTickCount());" to capture the current_time, then use the formula "period=current-previous", the update the "previous_time= current_time". So in the next loop the current_time will have a new value and the previous_time will take on the old current_time value. Note: both current_time and previous_time is initialized at 0.
b. LED blink task period:
Should be 500ms in total (250ms on, 250ms off). In my code I calculated the period of LED ON and LED OFF seperately so on the display console will show LED ON 250ms and LED 250ms.
c. Print task period:
shoulb be 10000ms using the same logic.

**Q5. Did our system tasks meet the timing requirements?**

The timing requirement was met.
How do you know?
By prinyting out period and time stamp. 
How did you verify it?
Compare with the counter on wokwi.

**Q6. If the LED task had been written in a single-loop with the print (see baseline super-loop code), you might have seen the LED timing disturbed by printing (especially if printing took variable time).**

Did you try running the code?
Yes, I did.
Can you cause the LED to miss it's timing requirements?
If yes, how?
If no, what did you try?
Because super loop is sequential, increase the delay in printing task will add up to the time until next LED blink.

**Q7. Do you agree or disagree: By using multitasking, we were able to achieve timing determinism for the LED blink. Why or why not?**

I disagree, because using multitasking we are relying on the system task scheduling. Timing determinism is more about event driven or hardware interupt.
