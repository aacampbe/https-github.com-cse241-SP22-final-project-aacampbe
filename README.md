# CSE 241 Final Project Report by Adrian Campbell
## Introduction
  A finite-state machine is a model that represents the conditions of one or more states (the current values of various variables that can change) in a system.  One type of a finite-state machine is a Moore machine in which the current output values are determined by the current states. An example of a Moore machine is a traffic light simulation in which the traffic light signals are determined by the current state of various sensors and this simulation can be implemented using D-FlipFlops. The main goal of this simulation would be to demonstrate state pattern and how applications of state pattern can play into real life. 
## Design Problem
  The simulation will need to output two traffic signals from two roads the country road and the highway and each traffic signal could either be red or green which in the context of the simulation will be represented as 0 and 1 and in order to do that the state of the sensors which will be represented as the inputs will change from time to time in order to get the corresponding traffic signals. Each of the following sensors: the weather sensor (responsible for telling if it is snowing or not), the sensor enabler (responsible for being the overall sensor and in activation with the counting sensor), and the counting sensor (responsible for telling how many vehicles are passing through an intersection) have different behavior and from that behavior the traffic signals can be found. One behavior is when the sensor enabler is off and or the counting sensor is off then the country road traffic signal is red. Also, another behavior is if the weather sensor is on then the sensor enabler and the counting sensor will be off as well otherwise the counting sensor and sensor enabler will always be on. Lastly, the traffic signals for both of the roads cannot both be red.
## Design Development
  State Diagram:
  ![State Diagram](IMG-0421.svg)

  State Assignments:
    A=000
    B=001
    C=010
    D=011
    E=100
    F=101
    G=110
    H=111
  State Table:
  ![State Table](State-Table.svg)
  
  Transition Table:
  ![Transition Table](Transition-Table.svg)
   
  Transition Equations:


  
## Bill of Materials

- D-Flip Flops
- Resistors
- MyDAQ
- Wires
- Not IC


## Physical Implementation and Testing
  Eight test cases that would be needed to test this system is would be for each of the inputs in the test cases the inputs for each respective test case would be 000,001,010,011,100,101,110, and 111 in.  Also, for each of the test cases none of the outputs can both be 0 and for the first two test cases the outputs are 0 and 1 and for the next two test cases the outputs are 1 and 0. Next, for the rest of the test cases the outputs are both 0.  The first two test cases are trying to check that the country road’s traffic light is off and the highway’s traffic light is on due to the fact that the country road’s light will always be off if the overall sensor is off. In addition, the next two cases are trying to check if any of the traffic lights are on if the overall sensor and or counting sensor is on. To add on, the last four test cases is trying to test if the input that is associated with the weather sensor is 0 then the outputs will be 0s and the state variables will equal 1,0, and 0 as this is trying to verify that the traffic lights will be off when the weather sensor is on and that the counting sensor and overall sensor is off. One essential case to check to make sure it is working correctly is if throughout the system the outputs are never both 1 and if that is the case then the system needs to be revamped. Lastly, another important case to make sure the system is working probably is if every time the weather sensor input is 1 or on then the country road output will always be 0 or off and if that is not the case then change it to make sure that criteria is met as it one of the most straight forward criteria and if that condition is not met then the implementation of the other criteria would be made much more difficult.
  
## SystemVerilog Implementation
// Adrian Campbell
//inputs:WS,SE,CS,and clk
//outputs:CR and Hi
module traffic(WS,SE,CS,clk,CR,Hi);
	input WS,SE,CS,clk;
	output reg CR,Hi;  
	//internal variables
	reg ps,ns;
	parameter 			  A=3'b000,B=3'b001,C=3'b010,D=3'b011,E=3'b100,F=3'b101,G=3'b110,H=3'b111;
	//next state calculations
	always@(WS or SE or CS)
		case(ps)
			A: if (WS==0 && SE==0 && CS==0) ns = D; 
   			else if (WS==0 && SE==0 && CS==1)ns=D;
   			else if (WS==0 && SE==1 && CS==0)ns=D;
  		 	else if (WS==0 && SE==1 && CS==1)ns=D;
   		 	else if (WS==1 && SE==0 && CS==0)ns=E;
   		 	else if (WS==1 && SE==0 && CS==1)ns=E;
         	else if (WS==1 && SE==1 && CS==0)ns=E;
         	else if (WS==1 && SE==1 && CS==1)ns=E;
		 	B:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
     		C:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
      		D:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
      		E:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
      		F:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
      		G:if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
      		H: if (WS==0 && SE==0 && CS==0) ns = D; 
   	   		else if (WS==0 && SE==0 && CS==1)ns=D;
       		else if (WS==0 && SE==1 && CS==0)ns=D;
       		else if (WS==0 && SE==1 && CS==1)ns=D;
       		else if (WS==1 && SE==0 && CS==0)ns=E;
       		else if (WS==1 && SE==0 && CS==1)ns=E;
       		else if (WS==1 && SE==1 && CS==0)ns=E;
		endcase
  	//update the outputs
	always@(ps)
		case(ps)
			E:begin 
         	 CR <= 1;
      	 	 Hi<= 0;
         end
         default:begin
           		   CR <= 0;
      			   Hi<=0;
         		 end
	endcase
  	//update for clock
	always@(posedge clk)
		ps<=ns;
endmodule
## SystemVerilog Test Bench
// Adrian Campbell
module traffic_tb;
  reg WS_tb, SE_tb, CS_tb, clk_tb;
  wire CR_tb,Hi_tb;
  traffic in1(.WS(WS_tb),.SE(SE_tb),.CS(CS_tb),.clk(clk_tb),.CR(CR_tb),.Hi(Hi_tb)); 
  initial
  	  begin
       WS_tb=0;
       SE_tb=0;
       CS_tb=0;
       clk_tb=0;
  end
  
 always
   begin
   #10 clk_tb=!clk_tb;
   end
  
 always
   begin
   #10 WS_tb=0;
       SE_tb=0;
       CS_tb=0;
   end
  
 always
   begin
   #10 WS_tb=0;
   #10 SE_tb=1;
   #10 CS_tb=0;
   end
  
 always
   begin
   #10 WS_tb=0;
   #10 SE_tb=1;
   #10 CS_tb=1;
   end
  
 always
   begin
   #10 WS_tb=1;
   #10 SE_tb=0;
   #10 CS_tb=0;
   end
 
 always
   begin
   #10 WS_tb=1;
   #10 SE_tb=0;
   #10 CS_tb=1;
   end
  
  always
    begin
   #10 WS_tb=1;
   #10 SE_tb=1;
   #10 CS_tb=0;
    end
  
   always
     begin
   #10 WS_tb=1;
   #10 SE_tb=1;
   #10 CS_tb=1;
     end
 
 initial
    begin
      $dumpfile("traffic.vcd");
      $dumpvars;
    end
  initial
    begin
      $display("------------ Results ------------");
      $display("WS\t SE\t CS\t clk\t\t F \G\tH");
      $monitor("%d\t%d\t\t%d\t\t%d\t\t%d%d\t\t\t\t%d",
              WS_tb,SE_tb,CS_tb,clk_tb,CR_tb,Hi_tb);
    end
  initial
    #400 $finish;
endmodule
## Analysis
  Based on the log file of inputs/outputs the correct approach would be to look through the waveform to see if all the outputs and input values are correct and all the variables are named accordingly in the waveform. For example, WS, SE, CS, CR, clck and Hi are in the waveform and the different 0s and 1s are in there and if not fix the testbench or maybe it is a problem with the function that is being called in the testbench so fix that function accordingly. Also, in the waveform the right approach would be to see if it is resetting and updating in the appropriate time frame as defined in the testbench and if not then the testbench needs to be fixed. In addition, if the inputs and outputs are not in the right data types then it would be more likely be a problem associated with the function that is being called from the test bench and not the test bench itself. Lastly, from the video recordings of the intersection if the traffic light on either road has the wrong color signals based on the state of the signals then it would be crucial to fix it immediately or redesign the system as some malfunctions in the sensors and the traffic lights could be hazardous in the grand scheme such as if the country road and highway traffic lights at any point both have green lights then the system is completely wrong as this is one of the most basic requirements needed in the system and if this benchmark fails then most likely the other benchmarks will fail or are not completely met as well.
## Conclusion
   In conclusion, the simulation of traffic lights using D-Flip Flops demonstrates the concept of Moore finite state machines very clearly. From this simulation a better understanding of state pattern from the change of various inputs was made and the usage of tools such as System Verilog and the problem-solving process of designing the simulation on the breadboard through state diagrams, transition tables, and state tables was also made. This simulation helped give a much larger insight into state pattern and how state pattern can be incorporated into the everyday world.

This project was designed and implemented by Adrian Campbell in
Spring 2022 for CSE241 at the University at Buffalo. Content in this
repository is not to be reproduced or utilized without written
authorization from the instructor, Dr. Winikus (jwinikus@buffalo.edu). 


