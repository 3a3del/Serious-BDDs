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
     
# Results
Variables: d14 d13 d12 d11 d10 d9 d8 d7 d6 d5 d4 d3 d2 d1 d0 : 000000000000000

That's mean we can remove the gate entirely and replace it with a constant “0”;  this is logically a correct repair, but it makes the adder slow, and is not the best solution. 

# Part 2: Unknown Inversion Find-and-Repair
A common error in a large logic network is an incorrect inversion: on some internal wire, there is error that can be corrected by adding exactly one invertor to this wire 
in the network. But, we do not know where the error is. It turns out we can still use a BDD to solve this new, seemingly more difficult problem. We can find the wrong wire and then invert it to repair things.
 
  
  
  
  
  
  
  
  
                                                                                                                                                                                                                                                                                                                                                                   
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
