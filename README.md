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

 # Idea
It is easiest to see the idea – which you need to work out – on a small design. Suppose we have this small section of a larger logic network, and we want to ask the simpler question: which one of these two wires is incorrectly inverted?

![](https://github.com/3a3del/Serious-BDDs/blob/main/t2.jpeg)
      
Then we modify the network as follows:
    - On each suspect wire, we insert a programmable inverter (PRI). A programmable inverter is a small piece of logic (2 inputs, 1 output) that has this function: if the 
      control input N=0, then out=in; if the control input N=1, then out=in’. In other words, the N signal negates the input, when N=1. 
        ![](https://github.com/3a3del/Serious-BDDs/blob/main/t3.jpeg)
        
We then build another piece of new logic that selects one of the programmable inverters, and sets its control signal Ni = 1. All the other programmable inverters are set to Nj=0. This selection logic takes a new set of inputs the select which one of the PRI control inputs to set to 1. Suppose you had 16 potential wires to check for an inversion error. Then this selection logic has log2(16) = 4 inputs, S3,S2,S1,S0, select one PRI to enable. For example, if 
S3,S2,S1,S0=1001, then we will set N9=1, and set all other Nj=0, for j9. Let’s call this version of the design, with the PRI’s and the selection logic, the “proposed repair” network. This is shown below
  
   ![](https://github.com/3a3del/Serious-BDDs/blob/main/t4.jpeg)
   
Just as with previous network repair methods, we need to have available some correct version of the logic. We connect the correct logic output, and our “proposed repair” version of the network, to an EXNOR gate. We want to solve for values of the selection inputs Sn-1…S2S1S0 so that the output Z of the EXNOR is always 1. We use quantification again, and get rid of all inputs other than the selection inputs.
   ![](https://github.com/3a3del/Serious-BDDs/blob/main/t1.jpeg)
   
This is the general “recipe” for finding and correcting an inversion error on a wire. It is helpful to consider a very small, concrete example, to work through the details you need to determine to complete this part.                    
  
  
  
  
  
                                                                                                                                                                                                                                                                                                                                                                   
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
