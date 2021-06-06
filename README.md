# Checksum for Memory
A high level state machine with 16x8-bit memory that can be implemented in a Basys3 FPGA. Can compute the checksum of the current data, display a word at a given address and display the count of the words. The register file is initialized with the following data
````
Register File := {8'h0f, 8'h0e, 8'h0d, 8'h0c,
                8'h0b, 8'h0a, 8'h09, 8'h08,
                8'h07, 8'h06, 8'h05, 8'h04,
                8'h03, 8'h02, 8'h01, 8'h00} // RF[i] := i, for i ranging from 0 to f
````

## But, what is a checksum?
Checksum is the 2's complement of sum of all words in the memory. 2's complement of a number is 1 more than the inverse of itself.

## Display
The machine has three modes of displaying. It either displays a word from the memory, the checksum or the count of the words.
### Word Display
This is the default display. When the machine is initialized, it will display the word at the 0th index. Current word that is displayed can be changed with right and left push buttons. The sevent segment display will show both the index and the value of the word. For instance, the word 0x07 at index 5 would be displayed as
````
5-07
````
### Checksum
When compute button is pressed, after the computation is complete, the checksum will be displayed. If the checksum is computed as 0x88 for instance the following will be displayed for ten seconds, then default display will continue where it left off:
````
C=88
````
### Count
When count button is pressed, number of words in the memory, that is already computed in checksum computation, will be displayed. If the count is computed as 16, 0x10, for instance, the following will be displayed for ten seconds, then default display will continue where it left off:
````
c=10
````
## Push Buttons
- Center
  - Writes the word specified in the switches in the specified index to the register file
- Left
  - Shows the previous word in the memory by decrementing the index
- Right
  - Shows the next word in the memory by incrementing the index
- Up
  - Computes and displays the checksum
- Bottom
  - Displays the number of words

## Switches
- The switches SW<sub>15:8</sub> is used for the value of the external data, the value of the word to be written
- The switches SW<sub>3:0</sub> is used for the address of the data to be written
## Design

### Computing Checksum

#### HLSM Diagram
![Checksum HLSM diagram](https://github.com/zubeyir-bodur/Checksum/blob/master/img/model%20hlsm%204.png)
#### Reduced FSM Diagram
<img src="https://github.com/zubeyir-bodur/Checksum/blob/master/img/controller%20fsm.jpg" alt="Checksum FSM diagram" width="640" height="800">

### Main Module HLSM Diagram
![Main HLSM Diagram](https://github.com/zubeyir-bodur/Checksum/blob/master/img/view%20logic%20hlsm.jpg)

### Block Diagrams

#### Computing Checksum - Inputs and Outputs
![IO](https://github.com/zubeyir-bodur/Checksum/blob/master/img/I-O.jpg)

#### Computing Checksum - Datapath
![Datapath](https://github.com/zubeyir-bodur/Checksum/blob/master/img/datapath.jpg)

The [report](https://github.com/zubeyir-bodur/Checksum/blob/master/Report.pdf) may not be helpful, as it is outdated and long.


