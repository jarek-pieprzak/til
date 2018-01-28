# Timing Events
JavaScript gives us the option of calling functions with a certain delay.
       
We have two options:
   
        setTimeout(function, miliseconds)
        setInterval(function, miliseconds)
  
## setTimeout

The setTimeout method as the first argument takes the callback function to be called and the second delay time in milliseconds.

## setInterval

The setInterval method works similarly to setTimeout, with the difference that it executes the code cyclically.
The method returns an identifier that can be stored and used to stop the timer using the clearInterval method.
