# Serious-BDDs
The Project is in two parts, both focused on network repair applications, since these exercise a lot of the power of a good BDD package. We will write and exercise kbdd scripts to complete this Project.

# Part 1: Network Gate Repair
Consider this logic network:

   ![](https://github.com/3a3del/Serious-BDDs/blob/main/First%20Part%20Design.jpeg)     

We are showing just the carry chain (from carry-in “cin” to carry-out “cout”) for a 4 bit adder, this is a more sophisticated architecture called a carry-bypass adder. We believe the highlighted gate labeled “?” has been implemented incorrectly. Our job is repair this network and tell the proper gate.
# How to this
  1. Build a “correct” version of the circuit. This means you just need an ordinary 4 bit adder with a carry-in and a carry-out from the high-order bit. You can 
     recall that kbdd has an adder primitive built in. (Hint: it looks like this: adder 4 cout_gold sum[3..0] a[3..0] b[3..0] cin).
  2. Replace the “?” gate with a multiplexor, to emulate the gate we need to find. Note that we are working to repair a 4-input gate, with inputs q1,q2,q3,q4.So, we need a 
     16:1 mux, since any truth table for this gate is a function of 4 variables, so it has 24 rows you need to solve for.
  3. Set up the BDD-based gate repair: replace the gate with the mux; EXNOR the correct circuit with this incorrect circuit with the mux inserted; quantify away the right 
     variables; satisfy this result.

      ![](https://github.com/3a3del/Serious-BDDs/blob/main/temp.jpeg)     

  
  
  
  
  
  
  
  
  
                                                                                                                                                                                                                                                                                                                                                                   
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
