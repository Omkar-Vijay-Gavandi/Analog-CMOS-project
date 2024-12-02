# Analog-CMOS-project

## LDO Design

In this project we have designed an LDO subject to different conditions. For this design we are designing the LDO for both externally and internally compensated LDO. We have considered different technology nodes for the same. For the below figure we are considering 45nm technology node. The technology node file is attached [here](https://github.com/Omkar-Vijay-Gavandi/Analog-CMOS-project/blob/main/Spice%20files/45nm_HP.txt). Our aim is to design the LDO for a max and a min load condition.

I have designed the following schematic

## Schematic

![image](https://github.com/user-attachments/assets/5ce8b229-9fde-489d-9ea2-97845d9a9552)

For the below schematic we have three cases wherein we have to find the open loop PSRR, Closed loop PSRR and the loop gain of the circuit. The formula for the closed loop PSRR is given below.

![image](https://github.com/user-attachments/assets/74732307-9d95-4bd0-9c3a-439d7e7c2d72)

Thus in order to simulate this circuit we have made three schematics in LTSpice to calculate the three conditions. We have made a simulation artifact for the same and from that we can find the above mentioned parameters.

# Heavy Load ( 10ma )

## Case 1:- Loop gain analysis:-

#### Schematic

![image](https://github.com/user-attachments/assets/73df3602-6764-4e8e-a6de-a64607ee085a)

#### Explanation of the artifact used:-

In order to calculate the loop gain we have given a RC circuit in the feedback loop alongwith a AC source with amplitude 1 ( as we want to maintain a voltage of 1V ) at the output. At the same time we also need to bias the circuit and provide a dc voltage to the gate of the nmos in the differential amplifier and for this we are giving the RC circuit which will prevent the flow of dc current to ground but will send any AC signal at the output to ground at high frequency. Also the drop across the resistor will be very less as we have given a very high resistance with very negligible current ( since current going into the gate of the mosfet is zero). Thus we will bias the circuit and also calculate the loop gain.

#### Output log file:-

![image](https://github.com/user-attachments/assets/c9ab2a3a-f744-4f13-99e3-927b20009abc)

From the above file we can verify that all the devices are in saturation as follows:-

M1:- PMOS 
    Vsd = 0.651
    Vsg = 0.651
    Vtp = 0.489
    Vsg - vtp = 0.162
    since vsd > 0.162 the device is in saturation
    

M2:-  PMOS
      Vsd = 0.64
     Vsg = 0.651
     vtp = 0.489
    Vsg - vtp = 0.162
    since vsd > 0.162 the device is in saturation

M3:- PMOS
     Vsd = 0.367
     Vsg = 0.64
     vtp = 0.481
    Vsg - vtp = 0.159
    since vsd > 0.159 the device is in saturation

M4:-  NMOS
     Vds = 0.734
     Vgs = 0.734
     vtn = 0.4
    Vgs - vtn = 0.162
    since vds > 0.162 the device is in saturation

M5:- NMOS
     Vds = 0.368
     Vgs = 0.609
     vtn = 0.468
    Vgs - vtn = 0.141
    since vds > 0.141 the device is in saturation

M6:- NMOS
     Vds = 0.358
     Vgs = 0.609
     vtn = 0.468
    Vgs - vtn = 0.141
    since vds > 0.141 the device is in saturation

M7:- NMOS
     Vds = 0.391
     Vgs = 0.734
     vtn = 0.468
    Vgs - vtn = 0.266
    since vds > 0.266 the device is in saturation

M8:- NMOS
     Vds = 1.03
     Vgs = 0.734
     vtn = 0.466
    Vgs - vtn = 0.268
    since vds > 0.268 the device is in saturation


# Transistor Operating Regions Table

This document provides a table summarizing the operating regions of several transistors based on their parameters.

## Table:

| **Transistor** | **Type** | **Vds (V)** | **Vgs/Vsg (V)** | **Vt (V)** | **Vgs/Vsg - Vt (V)** | **Operating Region**   |
|----------------|----------|-------------|------------------|------------|-----------------------|------------------------|
| M1            | PMOS     | 0.651       | 0.651           | 0.489      | 0.162                | Saturation             |
| M2            | PMOS     | 0.64        | 0.651           | 0.489      | 0.162                | Saturation             |
| M3            | PMOS     | 0.367       | 0.64            | 0.481      | 0.159                | Saturation             |
| M4            | NMOS     | 0.734       | 0.734           | 0.4        | 0.334                | Saturation             |
| M5            | NMOS     | 0.368       | 0.609           | 0.468      | 0.141                | Saturation             |
| M6            | NMOS     | 0.358       | 0.609           | 0.468      | 0.141                | Saturation             |
| M7            | NMOS     | 0.391       | 0.734           | 0.468      | 0.266                | Saturation             |
| M8            | NMOS     | 1.03        | 0.734           | 0.466      | 0.268                | Saturation             |



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

#### Output on LTSpice

![image](https://github.com/user-attachments/assets/85b464f6-d450-43b8-a251-6bcd33e5667f)

#### Python plots

![image](https://github.com/user-attachments/assets/102533ba-24b7-4ca6-8a21-0296292e25e1)

![image](https://github.com/user-attachments/assets/ea9f2dfd-6f89-4fc3-b8b6-5530e594ce18)


## Hand Calculations vs Simulation Results

### For Passfet,

### Hand Calculation:- 

ro = 242 ohms
gm = 0.1A/V
Wp1 (first pole location) = 4.14k
gmro = 24.18

Simulation Results from Spice Error Log:-

ro = 1/gds = 207.42 ohms
gm = 0.0978
Wp1 ( first pole location) = 4.132k
gmro = 20.289

## Hand Calculation vs Simulation Results

| Parameter               | Hand Calculation | Simulation Result | % Difference      |
|-------------------------|------------------|-------------------|-------------------|
| **ro (Ω)**             | 242.00          | 207.42            | 14.32%           |
| **gm (A/V)**           | 0.1000          | 0.0978            | 2.20%            |
| **Wp1 (Hz)**           | 4.14k           | 4.132k             |            |
| **gmro**               | 24.18           | 20.289            | 16.08%           |


# For light load ( 2 ma )

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

#### Spice Output Log

![image](https://github.com/user-attachments/assets/10f2193c-3a87-4006-971b-fdaf4c401b62)

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


## Transient Analysis

I have given a pulse at the load with a rise time and fall time of 1u. Also the period of the pulse is 10m with a 50% duty cycle. From the below figure we can understand that the output is able to settle within the specified range of time. We are not able to observe any overshoot or undershoot in the output. 

#### Schematic:-

![image](https://github.com/user-attachments/assets/8f3895a3-2f67-4477-b945-ec36c37772cc)

#### Ltspice Output:-

![image](https://github.com/user-attachments/assets/4ba6f9ee-f344-43fb-8105-7759defef3cf)

#### Python Plots:-

![image](https://github.com/user-attachments/assets/3799cae8-0856-47f7-a9da-690c2110d4f2)

![image](https://github.com/user-attachments/assets/23dc06a2-a85d-4a55-8f00-3f49f5f70a8d)


## Stability analysis

### For heavy load we get the following curve 

![image](https://github.com/user-attachments/assets/159b4262-fbd9-4e14-ae1b-79680f8f7f9b)

The python plots for the same is as follows:-

![image](https://github.com/user-attachments/assets/181a108d-53f2-46c1-9a15-e0a237ec5b98)

### For light load we get the following curve

![image](https://github.com/user-attachments/assets/c7a3ff2f-fe9c-485c-933c-daddf8d3138d)

The pyton plots are as follows:-

![image](https://github.com/user-attachments/assets/e48c82f1-f800-4617-8118-c13b432e4f86)

From the above analysis we can see that we can see that the unity gain bandwiddth is closer to the second pole for the heavy load case than the light load case. From the phase margin also we can observe that we observe a lesser phase margin of 76 degrees for the heavy load case than that of the light load case. From this analysis we can say that when we apply light load we get a more stable system.


## Effect of VDD on the output voltage

#### Schematic

![image](https://github.com/user-attachments/assets/5de1f3fb-e9a0-4dd2-8652-8cee7d2ea588)

#### Output plots

![image](https://github.com/user-attachments/assets/97a7bbb7-3222-4a28-8568-148f42457671)

From the plots we can see that we are getting regulation after 1.2 till 1.4v. After this voltage we are still getting 1v output but we can't comment on the circuit since the device has a nominal voltage of 1v and the vds across the mosfets might go above 1v so the device can breakdown.


