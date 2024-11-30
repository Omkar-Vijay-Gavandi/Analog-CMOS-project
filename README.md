# Analog-CMOS-project

## LDO Design

In this project we have designed an LDO subject to different conditions. For this design we are designing the LDO for both externally and internally compensated LDO. We have considered different technology nodes for the same. For the below figure we are considering 45nm technology node. The technology node file is attached [here](https://github.com/Omkar-Vijay-Gavandi/Analog-CMOS-project/blob/main/Spice%20files/45nm_HP.txt). Our aim is to design the LDO for a max and a min load condition. The design for

I have designed the following schematic

## Schematic

![image](https://github.com/user-attachments/assets/5ce8b229-9fde-489d-9ea2-97845d9a9552)

For the below schematic we have three cases wherein we have to find the open loop PSRR, Closed loop PSRR and the loop gain of the circuit. The formula for the closed loop PSRR is given below.

![image](https://github.com/user-attachments/assets/74732307-9d95-4bd0-9c3a-439d7e7c2d72)

Thus in order to simulate this circuit we have made three schematics in LTSpice to calculate the three conditions. We have made a simulation artifact for the same and from that we can find the above mentioned parameters.

## Case 1:- Loop gain analysis:-

#### Schematic

![image](https://github.com/user-attachments/assets/73df3602-6764-4e8e-a6de-a64607ee085a)

#### Explanation of the artifact used:-

In order to calculate the loop gain we have given a RC circuit in the feedback loop alongwith a AC source with amplitude 1 ( as we want to maintain a voltage of 1V ) at the output. At the same time we also need to bias the circuit and provide a dc voltage to the gate of the nmos in the differential amplifier and for this we are giving the RC circuit which will prevent the flow of dc current to ground but will send any AC signal at the output to ground at high frequency. Also the drop across the resistor will be very less as we have given a very high resistance with very negligible current ( since current going into the gate of the mosfet is zero). Thus we will bias the circuit and also calculate the loop gain.

#### Output log file:-

![image](https://github.com/user-attachments/assets/c9ab2a3a-f744-4f13-99e3-927b20009abc)


#### Output on LTSPICE:-

![image](https://github.com/user-attachments/assets/e3dc0547-675a-41e6-9ef8-05e527a62123)

#### Output on Python:-

![image](https://github.com/user-attachments/assets/7eac96a3-49b3-4560-86d8-618970a19647)

#### Phase margin

![image](https://github.com/user-attachments/assets/4b335ecc-917b-4c3f-9ba1-6eeb3d6fc36d)

The phase margin is **76.77**


The output voltage ( Loop gain ) comes out to be close to **58.3db** . The formula for loop gain is Adiff * Apass where Adiff is differential amplifier gain and Apass is the passfet gain.

## Case 2:- Open Loop PSRR calculation

#### Schematic

![image](https://github.com/user-attachments/assets/144239d4-726a-4754-bffd-38615734f837)

#### Explanation of the artifact

In order to calculate the open loop PSRR we need to send an AC signal from the source which in our case is VDD. Here we are giving an AC 1 signal in the source. This signal is given to the source of the passfet and the source of pmos in the diffamp. We will ideally want very bad PSRR in the diffamp as we want the OTA output to have all the AC noise such that Vsg of pmos = 0 ( small signal analysis ). Thus all the noise will get rejected and we will get a noise free dc voltage at the output of the LDO. Here in order to calculate the open loop PSRR we have a RC circuit to bias the circuit. You can see AC 0 in the circuit indicating that there is an **open loop in the circuit** . From here we have calculated the open loop PSRR in the circuit. Since there is no feedback in the circuit we can thus say that there will be noise at the output and thus the rejection will be very poor.

#### Output log file

![image](https://github.com/user-attachments/assets/e00ee07f-fca4-445c-9544-d940bc96e594)

#### Output on LTSpice

![image](https://github.com/user-attachments/assets/7ff05626-2961-4a15-9ead-2e394e6466d7)

#### Python plots

![image](https://github.com/user-attachments/assets/c1a644cd-d482-4e2f-9d2a-b314b360fade)

![image](https://github.com/user-attachments/assets/99e978fb-6fb9-4ad7-ae09-1cd126b99a28)



#### Note:- Always observe the Vota output in volts because it will give you the insight into what AC voltage is coming into the gate of the passfet. It should be close to VDD. If it becomes close to 

## Case 3:- Closed Loop PSRR Calculation

#### Schematic

![image](https://github.com/user-attachments/assets/cac4217d-e203-4a21-9b5d-b2f444a84736)

#### Explanation of the artifact
In this case we can see that we have given a AC source in the voltage source VDD. We want to see the negative feedback in the circuit due to which we will get the output voltage cancelled out (small signal analysis). Here we should observe a high PSRR according to our specifications ( 60db) which tells us that our sizing is perfect. For this circuit we have given a feedback from the output terminal to the input of the diffamp which indicated the feedback path.

#### Output log file

![image](https://github.com/user-attachments/assets/aa32f186-c528-4f10-9875-dac5cec5b9c0)

#### Output on LTSpice

![image](https://github.com/user-attachments/assets/85b464f6-d450-43b8-a251-6bcd33e5667f)

#### Python plots

![image](https://github.com/user-attachments/assets/102533ba-24b7-4ca6-8a21-0296292e25e1)

![image](https://github.com/user-attachments/assets/ea9f2dfd-6f89-4fc3-b8b6-5530e594ce18)



# For light load

## Case 1:- Loop gain analysis:-

#### Schematic

![image](https://github.com/user-attachments/assets/eff568e3-e7bb-4538-91d5-c4276706db6e)

#### LTSpice output

![image](https://github.com/user-attachments/assets/fa53ad2d-7eae-4504-831e-e8bab6847c9d)

#### Python plots

![image](https://github.com/user-attachments/assets/03488889-25c5-4a63-8cdc-b5d60af14562)

#### Phase margin

![image](https://github.com/user-attachments/assets/78ec7924-33c4-45e8-b4a0-455907abe2cd)

The phase margin obtained is 84.95 degrees. This value is more than that of the value obtained for heavy load. Thus proving the point that for light load we get a better phase margin as the 1st pole and the 2nd pole are far apart.


## Case 2:- Open Loop PSRR calculation

#### Schematic

![image](https://github.com/user-attachments/assets/55a79a24-c9bf-4878-ab65-ad170099e1b9)

#### LTSpice Plots

![image](https://github.com/user-attachments/assets/c2672015-6bce-4010-87f6-5b4910b89391)

#### Python plots

![image](https://github.com/user-attachments/assets/62b25429-89a9-49d6-bc9f-8dfd32d74622)

![image](https://github.com/user-attachments/assets/aa84d75e-e64f-488e-aa4a-16539c757983)

## Case 3:- Closed loop PSRR calculation

### Schematic

![image](https://github.com/user-attachments/assets/2a040b24-c4f3-4cd3-90fb-ae7f01303585)


#### LTSpice Output:-

![image](https://github.com/user-attachments/assets/49fbebe0-9b72-4279-9a39-b4aaa8a98029)

#### Python plots

![image](https://github.com/user-attachments/assets/be73a4cb-accb-47c9-9cfa-3c4084340091)

![image](https://github.com/user-attachments/assets/0c16b5b9-47d2-4aef-8c59-b9de1d316a25)























