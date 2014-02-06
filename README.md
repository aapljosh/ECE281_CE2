ECE281_CE2
==========

Sabin's Computer Exercise 2

## Decoder
A decoder is a device which takes in binary inputs and returns the information into unique, separate outputs.  In CE 2, we will program a simple decoder using both the structural and behavioral architectural designs.

## Schematic of a Decoder
![alt text](https://raw2.github.com/sabinpark/ECE281_CE2/master/Decoder%20Schematic.png "Decoder Schematic")

## Structural Decoder
The first decoder that was made was using structural architecture.  This means that the decoder consisted of various components that were put together using VHDL.  Three VHDL modules were created: *inverter*, *and3*, *Decoder_Structural*.  As it sounds, the *inverter* takes an input and outputs the inverse of the input.  *and3* takes in three inputs and outputs the AND of the three.  Finally, *Decoder_Structural* is used to combine the other two modules in such a way to program a functional decoder.

Under the *architecture* part of the *Decoder_Structural* module, the *inverter* and the *and3* modules were declared so that these components may be used to program the decoder.  As shown below, *inverter* and *and3* have the appropriate number and types of inputs and outputs.  The intermediary signals, *I0_NOT* and *I1_NOT* are declared here as well.

```vhdl
	COMPONENT inverter
	PORT(
		I : IN std_logic;
		O : OUT std_logic);
	END COMPONENT;
	
	COMPONENT and3
	PORT(
		I0 : IN std_logic;
		I1 : IN std_logic;
		I2 : IN std_logic;
		O : OUT std_logic);
	END COMPONENT;
	
	SIGNAL I0_NOT, I1_NOT : std_logic;
```

Following the schematic, the decoder module was programmed to use the appropriate components and signals for the decoder.  Below is an example of the connection for the Y3_and3 component:

```vhdl
	Y3_and3: and3 PORT MAP(
		I0 => I0,
		I1 => I1,
		I2 => EN,
		O => Y3);
```

After completing the connections for all of the components in the circuit, the next step was to test the module using a test bench.  NOTE: it was interesting that after creating a gate, a vhdl representing that gate was automatically created under the *Decoder_Structural* module.

## Test Bench for Structural Decoder
For this test bench, all of code pertaining to clocks were commented out.  Along with the inputs (I0, I1, and EN) and outputs (Y0, Y1, Y2, and Y3), a counter signal (count) was also created to be used in the stimulus process.  *count* was initialized to a value of *000*, and would go through all eight of the input combinations.  Thus, in the UUT (Unit Under Test), count(0) was set to I0, count(1) as I1, and count(3) as EN.  The outputs were kept the same.

A *for-loop* was used to test the eight input combinations.  Starting with *000*, the simulation would read through the three inputs and print out the corresponding output values.  Immediately after printing the results in the console, the simulation displayed the waveform of the inputs and outputs.  After every iteration, *count* was incremented by *001*.  This was made possible by using the unsigned.all library.  

## Structural Decoder Results
![alt text](https://raw2.github.com/sabinpark/ECE281_CE2/master/Decoder_Structural%20Simulation%20Results.PNG "Structural Decoder Results")

These results may be compared with the table above or the waveform below.

## Structural Decoder Waveform
![alt text](https://raw2.github.com/sabinpark/ECE281_CE2/master/Decoder_Structural%20Simulation%20Waveform.PNG "Structural Decoder Waveform")

The three inputs, I0, I1, and EN are represented by the count signal.
