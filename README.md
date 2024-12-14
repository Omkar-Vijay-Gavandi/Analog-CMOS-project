# Analog-CMOS-project

## LDO Design

In this project we have designed an LDO subject to different conditions. For this design we are designing the LDO for both externally and internally compensated conditions. We have considered different technology nodes for the same. For the below figure we are considering 45nm technology node. The technology node file is attached [here](https://github.com/Omkar-Vijay-Gavandi/Analog-CMOS-project/blob/main/Spice%20files/45nm_HP.txt). Our aim is to design the LDO for a max and a min load condition.

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

![image](https://github.com/user-attachments/assets/3252ba88-5d11-443f-b0ca-002f75fb9b61)


#### Phase margin

![image](https://github.com/user-attachments/assets/56499ec5-458f-4eaa-a9de-39557e758819)

The phase margin is **77.10**


The output voltage ( Loop gain ) comes out to be close to **58.3db** . The formula for loop gain is Adiff * Apass where Adiff is differential amplifier gain and Apass is the passfet gain.


## Case 2:- Open Loop PSRR calculation

#### Schematic

![image](https://github.com/user-attachments/assets/144239d4-726a-4754-bffd-38615734f837)

#### Explanation of the artifact

In order to calculate the open loop PSRR we need to send an AC signal from the source which in our case is VDD. Here we are giving an AC 1 signal in the source. This signal is given to the source of the passfet and the source of pmos in the diffamp. We will ideally want very bad PSRR in the diffamp as we want the OTA output to have all the AC noise such that Vsg of pmos = 0 ( small signal analysis ). Thus all the noise will get rejected and we will get a noise free dc voltage at the output of the LDO. Here in order to calculate the open loop PSRR we have a RC circuit to bias the circuit. You can see AC 0 in the circuit indicating that there is an **open loop in the circuit** . From here we have calculated the open loop PSRR in the circuit. Since there is no feedback in the circuit we can thus say that there will be noise at the output and thus the rejection will be very poor.

#### Output on LTSpice

![image](https://github.com/user-attachments/assets/7ff05626-2961-4a15-9ead-2e394e6466d7)

#### Python plots

![image](https://github.com/user-attachments/assets/08850f7c-92a8-4e6b-90d9-646895e38fcd)

![image](https://github.com/user-attachments/assets/f73109a2-fc91-46fb-829a-8064fa6d8c59)


#### Note:- Always observe the Vota output in volts because it will give you the insight into what AC voltage is coming into the gate of the passfet. It should be close to VDD. If it becomes close to 

## Case 3:- Closed Loop PSRR Calculation

#### Schematic

![image](https://github.com/user-attachments/assets/cac4217d-e203-4a21-9b5d-b2f444a84736)

#### Explanation of the artifact
In this case we can see that we have given a AC source in the voltage source VDD. We want to see the negative feedback in the circuit due to which we will get the output voltage cancelled out (small signal analysis). Here we should observe a high PSRR according to our specifications ( 60db) which tells us that our sizing is perfect. For this circuit we have given a feedback from the output terminal to the input of the diffamp which indicated the feedback path.

#### Output on LTSpice

![image](https://github.com/user-attachments/assets/85b464f6-d450-43b8-a251-6bcd33e5667f)

#### Python plots

![image](https://github.com/user-attachments/assets/f80b76ae-2a9f-47ef-ac13-14aef3a384e4)

![image](https://github.com/user-attachments/assets/17a0280b-618a-4c1b-bc49-6d23df5f6d3f)


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
| **Wp1 (Hz)**           | 4.14k           | 4.132k             |  0.19%          |
| **gmro**               | 24.18           | 20.289            | 16.08%           |

### For Differential Amplifier,

Adiff = 1000 / 24.18 = 41.35

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


# For light load ( 2 ma )

## Case 1:- Loop gain analysis:-

#### Schematic

![image](https://github.com/user-attachments/assets/eff568e3-e7bb-4538-91d5-c4276706db6e)

#### LTSpice output

![image](https://github.com/user-attachments/assets/fa53ad2d-7eae-4504-831e-e8bab6847c9d)

#### Python plots

![image](https://github.com/user-attachments/assets/505904f5-ff1f-4b4e-8f94-ecd7c245b1f6)


#### Phase margin

![image](https://github.com/user-attachments/assets/0e024eaf-2ae5-425e-a9af-8279b341b041)

The phase margin obtained is 84.74 degrees. This value is more than that of the value obtained for heavy load. Thus proving the point that for light load we get a better phase margin as the 1st pole and the 2nd pole are far apart.

#### Spice Output Log

![image](https://github.com/user-attachments/assets/10f2193c-3a87-4006-971b-fdaf4c401b62)


# Transistor Operating Regions Table

This document provides a table summarizing the operating regions of several transistors based on their parameters.

## Table:

| *Transistor* | *Type* | *Vds (V)* | *Vgs/Vsg (V)* | *Vt (V)* | *Vgs/Vsg - Vt (V)* | *Operating Region*   |
|----------------|----------|-------------|------------------|------------|-----------------------|------------------------|
| M1            | PMOS     | 0.652       | 0.652           | 0.489      | 0.163                | Saturation             |
| M2            | PMOS     | 0.522        | 0.652           | 0.490      | 0.162                | Saturation             |
| M3            | PMOS     | 0.364       | 0.522           | 0.481      | 0.041               | Saturation             |
| M4            | NMOS     | 0.734       | 0.734           | 0.467        | 0.267                | Saturation             |
| M5            | NMOS     | 0.485       | 0.607           | 0.468      | 0.139                | Saturation             |
| M6            | NMOS     | 0.355       | 0.609           | 0.468      | 0.141                | Saturation             |
| M7            | NMOS     | 0.393       | 0.734           | 0.468      | 0.266                | Saturation             |
| M8            | NMOS     | 1.04        | 0.734           | 0.466      | 0.268                | Saturation             |

## Case 2:- Open Loop PSRR calculation

#### Schematic

![image](https://github.com/user-attachments/assets/55a79a24-c9bf-4878-ab65-ad170099e1b9)

#### LTSpice Plots

![image](https://github.com/user-attachments/assets/c2672015-6bce-4010-87f6-5b4910b89391)

#### Python plots

![image](https://github.com/user-attachments/assets/083f0a4f-4094-4d63-bcb5-c5dac644556b)

![image](https://github.com/user-attachments/assets/b2193462-47ac-44f3-96fb-5378b04153e7)


## Case 3:- Closed loop PSRR calculation

### Schematic

![image](https://github.com/user-attachments/assets/2a040b24-c4f3-4cd3-90fb-ae7f01303585)


#### LTSpice Output:-

![image](https://github.com/user-attachments/assets/49fbebe0-9b72-4279-9a39-b4aaa8a98029)

#### Python plots

![image](https://github.com/user-attachments/assets/f560a3dc-0765-49d1-a1f4-0a3ea5b642da)

![image](https://github.com/user-attachments/assets/2f2d0a33-3308-4c55-964f-cfaf8f8b99f0)




## Transient Analysis

I have given a pulse at the load with a rise time and fall time of 1u. Also the period of the pulse is 10m with a 50% duty cycle. From the below figure we can understand that the output is able to settle within the specified range of time. We are not able to observe any overshoot or undershoot in the output. 

#### Schematic:-

![image](https://github.com/user-attachments/assets/8f3895a3-2f67-4477-b945-ec36c37772cc)

#### Ltspice Output:-

![image](https://github.com/user-attachments/assets/4ba6f9ee-f344-43fb-8105-7759defef3cf)

#### Python Plots:-

![image](https://github.com/user-attachments/assets/79c4088a-7ad2-4762-8411-288539ce16d0)

![image](https://github.com/user-attachments/assets/07b3dfa5-d862-40ab-8bb7-0e25857b8380)


## Stability analysis

### For heavy load we get the following curve 

![image](https://github.com/user-attachments/assets/77033727-1fd7-4d1d-b11b-4e0c789f1d04)

The python plots for the same is as follows:-

![image](https://github.com/user-attachments/assets/6c110f9a-c617-47b1-92fa-f5ee751562d0)

### For light load we get the following curve

![image](https://github.com/user-attachments/assets/7544b974-61c2-4d03-a631-5a44713d8bdd)

The python plots are as follows:-

![image](https://github.com/user-attachments/assets/c6e6c015-d850-408a-b522-4d5a5869aa6c)


From the above analysis we can see that we can see that the unity gain bandwiddth is closer to the second pole for the heavy load case than the light load case. From the phase margin also we can observe that we observe a lesser phase margin of 76 degrees for the heavy load case than that of the light load case. From this analysis we can say that when we apply light load we get a more stable system.


## Effect of VDD on the output voltage

#### Schematic

![image](https://github.com/user-attachments/assets/5de1f3fb-e9a0-4dd2-8652-8cee7d2ea588)

#### Output plots

![image](https://github.com/user-attachments/assets/ea7a701e-b33f-455e-b51c-d05d3234685d)

From the plots we can see that we are getting regulation after 1.2 till 1.4v. After this voltage we are still getting 1v output but we can't comment on the circuit since the device has a nominal voltage of 1v and the vds across the mosfets might go above 1v so the device can breakdown.

# Area vs gm/Id plot

This document summarizes the area calculations for different gm/Id values. The table below lists the areas of individual transistors (passfet, PMOS diffamp FET, NMOS diffamp FET, and current mirror FET) as well as the overall area for each gm/Id value.

## Table: Transistor Area for Different gm/Id Values

| **gm/Id** | **Passfet Area (μm²)** | **PMOS Diffamp FET Area (μm²)** | **NMOS Diffamp FET Area (μm²)** | **Current Mirror FET Area (μm²)** | **Overall Area (μm²)** |
|-----------|-------------------------|----------------------------------|----------------------------------|-----------------------------------|-------------------------|
| 10        | 12.08                  | 0.297                           | 0.1124                          | 0.9085                           | 13.3979                |
| 12        | 17.82                  | 0.445                           | 0.1156                          | 1.36                             | 19.781                 |
| 15        | 32.46                  | 0.544                           | 0.215                           | 2.55                             | 35.769                 |

## Notes

- The **gm/Id** values represent the ratio of transconductance (gm) to drain current (Id).
- The **Overall Area** is the sum of all individual transistor areas.
- These calculations are useful for evaluating the area trade-offs associated with different gm/Id values during circuit design.
- From the above table we can observe that as the gm/Id value increases the overall area of the design increases. This area is primarily dominated by the passfet who has the most area in the circuit given that its width is the most , it being a PMOS .
- We can observe that the area increases but the device is going in the subthreshold region as the overdrive voltage decreases. The Vgs is also decreasing assuming that the threshold voltage remains the same. Based on this we can say that the source voltage required to drive the LDO will decrease and also the bias currents required to bias the mosfets will reduce and thus we require less power to drive the entire circuit. 


![image](https://github.com/user-attachments/assets/f8cf3615-fc30-45e7-8f7e-bf3024644f29)

## Comparitive analysis between 180nm technology node and 45nm technology node for NMOS

| Parameter         | 180nm Technology Node | 45nm Technology Node |
|--------------------|-----------------------|-----------------------|
| **gmro**          | 20                    | 6.721                |
| **Id/W** (μA/μm)  | 28                    | 154.324              |
| **fT** (Hz)       | 1.6e10                | 18.93e10             |

For gmro we know that as that as length decreases ro decreases so the value of gmro decreases. Also ro is the dominant factor in gmro so overall gmro decreases.
For Id/w, if length decreases Id increases so overall Id/w increases which can be obesrved from the values.
For ft , if length decreases , gm increases , so overall ft increases which can be obserevd from the above table.




# Analog_ic_design_project

# Internally Compensated LDO

## Low Load(2ma)

### Case-1: Loop gain analysis:-

#### Schematic

![Screenshot 2024-12-03 215715](https://github.com/user-attachments/assets/fee7a096-3ef0-4455-93e6-fe4644fbe93d)


#### Output log file:-

![image](https://github.com/user-attachments/assets/fe15a521-710d-4b12-8d1d-5b0adb58d749)


# Transistor Operating Regions Table

This document provides a table summarizing the operating regions of several transistors based on their parameters.

## Table:

| *Transistor* | *Type* | *Vds (V)* | *Vgs/Vsg (V)* | *Vt (V)* | *Vgs/Vsg - Vt (V)* | *Operating Region*   |
|----------------|----------|-------------|------------------|------------|-----------------------|------------------------|
| M1            | PMOS     | 0.652       | 0.652           | 0.489      | 0.163                | Saturation             |
| M2            | PMOS     | 0.522       | 0.652           | 0.490      | 0.162                | Saturation             |
| M3            | PMOS     | 0.364       | 0.522            | 0.481      | 0.041                | Saturation             |
| M4            | NMOS     | 0.734       | 0.734           | 0.467        | 0.267                | Saturation             |
| M5            | NMOS     | 0.485       | 0.607           | 0.468      | 0.139                | Saturation             |
| M6            | NMOS     | 0.355       | 0.609           | 0.468      | 0.141                | Saturation             |
| M7            | NMOS     | 0.393       | 0.734           | 0.468      | 0.266                | Saturation             |
| M8            | NMOS     | 1.04        | 0.734           | 0.466      | 0.268                | Saturation             |


### Output on Python:-

![image](https://github.com/user-attachments/assets/59d290cc-2641-4349-8903-37ea35e7dffb)


### Phase margin

![Screenshot 2024-12-03 215638](https://github.com/user-attachments/assets/d2b6bc1d-3ad0-491b-87d3-3b8aa7483429)

![image](https://github.com/user-attachments/assets/0f7718d1-bc83-4664-bb2b-c2f7f40e0524)


## Case 2:- Open Loop PSRR calculation

### Schematic

![image](https://github.com/user-attachments/assets/db534bfc-6962-404b-a3ac-95dc34842b4c)


### Explanation of the artifact

### Python plots

![image](https://github.com/user-attachments/assets/65a99641-081f-4fbe-b99e-5cc4720080f9)

![image](https://github.com/user-attachments/assets/f0a9fc51-7fd4-4456-a346-604a08474d6b)


## Case 3:- Closed Loop PSRR Calculation

### Schematic

![image](https://github.com/user-attachments/assets/3af5bdd6-786e-43df-8d68-c779ad49a757)

### Python plots

![image](https://github.com/user-attachments/assets/7111e192-8b1f-4fe8-a14a-c59e2d573780)

![image](https://github.com/user-attachments/assets/1c13e55c-8e20-4695-824a-4bc81c249095)


### Hand Calculations vs Simulation Results


# For heavy load ( 10 ma )

## Case 1:- Loop gain analysis:-

### Schematic

![Screenshot 2024-12-03 215850](https://github.com/user-attachments/assets/ef1ab793-0dc1-4552-bfd4-999130da643c)


### Python plots

![image](https://github.com/user-attachments/assets/9da2dfa9-82bd-4dce-8acd-4f49614c0e35)


### Phase margin

![Screenshot 2024-12-03 215830](https://github.com/user-attachments/assets/b3944f33-0b71-4fd6-9b2e-25f150c0f6ff)

![image](https://github.com/user-attachments/assets/09339e57-e322-4c21-baa9-23e7887c8d74)



### Spice Output Log

![image](https://github.com/user-attachments/assets/9d00a5a7-42af-46dc-b791-85d6535928f8)


# Transistor Operating Regions Table

This document provides a table summarizing the operating regions of several transistors based on their parameters.

## Table:

| *Transistor* | *Type* | *Vds (V)* | *Vgs/Vsg (V)* | *Vt (V)* | *Vgs/Vsg - Vt (V)* | *Operating Region*   |
|----------------|----------|-------------|------------------|------------|-----------------------|------------------------|
| M1            | PMOS     | 0.651       | 0.651           | 0.489      | 0.162                | Saturation             |
| M2            | PMOS     | 0.64        | 0.651           | 0.489      | 0.162                | Saturation             |
| M3            | PMOS     | 0.367       | 0.64            | 0.481      | 0.159                | Saturation             |
| M4            | NMOS     | 0.734       | 0.734           | 0.467        | 0.267                | Saturation             |
| M5            | NMOS     | 0.368       | 0.609           | 0.468      | 0.141                | Saturation             |
| M6            | NMOS     | 0.358       | 0.609           | 0.468      | 0.141                | Saturation             |
| M7            | NMOS     | 0.391       | 0.734           | 0.468      | 0.266                | Saturation             |
| M8            | NMOS     | 1.03        | 0.734           | 0.466      | 0.268                | Saturation             |



## Case 2:- Open Loop PSRR calculation

### Schematic

![image](https://github.com/user-attachments/assets/ec1025c3-24ea-4bee-8f06-04e198f5c7e2)


### Python plots

![image](https://github.com/user-attachments/assets/504467fc-6ca2-4249-8103-2219dfb7a064)

![image](https://github.com/user-attachments/assets/d33f07f4-caf3-4425-8186-4f86177b9a49)



## Case 3:- Closed loop PSRR calculation

### Schematic

![image](https://github.com/user-attachments/assets/112705cf-8831-4b34-a88a-96ed6861a41c)

### Python plots

![image](https://github.com/user-attachments/assets/68666a96-e34d-401e-a840-8b471203acb7)

![image](https://github.com/user-attachments/assets/e4cf3612-c7a5-471b-a242-97848e7a7737)

## Transient Analysis

### Schematic

![image](https://github.com/user-attachments/assets/14acb753-7ff5-4fcf-8249-fbacf9a5a891)

### Python Plots:-

![image](https://github.com/user-attachments/assets/f2118e8d-c02e-45b9-8217-fff5728f80dd)

![image](https://github.com/user-attachments/assets/a3a94d7c-8979-40eb-8559-1e3a8762c1ec)
