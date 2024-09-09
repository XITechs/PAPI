# PERfECT API

Xinyu Tian

> This is an introduction for the API of PERfECT system.

## See what's PERfECT

[PERfECT](https://pubs.acs.org/doi/abs/10.1021/acs.analchem.1c05210) The world's first coin-size ECT control system.

Electrical Chemical Transistor (ECT) is a special type of transistor that has a totally different work mechanism compared with traditional Si-based transistors. Essentially, this kind of transistor is playing more with ions but not electrons, which makes it more similar to a human neural (both sensing and computing) system.

PERfECT start from a project (2020) called 'Personalized Electrical Reader for Electrical Chemical Transistors' which aims to prototype the world's first characterization system specifically for ECT devices.

<!-- ![PERfECT F0](https://pubs-acs-org.eproxy.lib.hku.hk/cms/10.1021/acs.analchem.1c05210/asset/images/medium/ac1c05210_0001.gif) -->

## USB/Bluetooth Software Install
Developing this whole system cost lots of my time and effort but  I take pride in spreading it and serving our community. Unfortunately, due to some frustrating and boring reasons (hegemony in academic suck!! filled with jokers and thieves, rife with incompetence and dishonesty), I have had to restrict access to most of this API temporarily. Please always ask [ME](xinyutian0217@gmail.com)  if you want to use it, I'm still more than willing to assist with real research. Additionally, if  you have any suggestions for improving or finding a more sustainable and healthier way (including a commercial one) for this project, please do not hesitate to get in touch.


## Workflow for Basical Demos
1. Configure your measurement by command: `"Meas xxx"`
2. Run your measurement by command: `"Start"`
3. Say `"Seek truth from facts"` loudly 3 times and then you can see your facts.
4. Stop your measurement by command: `"Stop"`
5. Always stop your current measurement first if you want to reconfigure your next new measurement.

## Basical API
### Transistors
#### Transfer curve

<hr/>

`Transfer curve` indicates the change in Ids (i.e., doping level evolution of the channel) with Vgs. It can be used to extract secondary performance indicators of the OECTs such as the on/off ratio and the Gm at different Vgs values. For transfer characterization of OECTs, Vds is fixed at a constant value. Vgs is scanned normally between −1 and +1 V. In most cases, Vgs is set to less than ±1.23 V to avoid water hydrolysis.

##### [#]() Configuration for transfer curve: 

- **Meas 3 A B C D E F**


| Parameter        | Explain                                          | Unit | Range |
| ---------------- | ------------------------------------------------ | ---- | --------------- |
| 3        | Fixed for ECT transfer. | N/A   | N/A  |
| A       | The voltage applied to Drain and Source.    | mV   | -1000 to +1000  |
| B        | The V Gate at the BEGINNING of the transfer curve.  | mV   | -1000 to +1000 |
| C       |  The V Gate at the END of the transfer curve.   | mV   | -1000 to +1000  |
| D            | The V Gate sweep step during the transfer curve. | mV   | 1 to +1000  |
| E | The time interval of each V Gate sweep step during the transfer curve.  | mS  | 1 to 100000  |
| F       |  Hysteresis or not.  | N/A  | 1:sweep back. 0:single direction sweep. |

##### [#]() Data Output for transfer curve: 

- **Ids, Vds, Vgs**
- **X1,X2,X3**

| Parameter        | Explain           | Unit |
| ---------------- | ----------------- | ---- |
| X1      | The I measured from Drain and Source. | uA  |
| X2      | The V measured from Drain and Source. | mV  | 
| X3      | The V measured at the Gate.  | mV   |

```haskell
----Transistor Transfer----
Ids, Vds, Vgs
X1,X2,X3
X1,X2,X3
X1,X2,X3
...
```
##### [#]() Example for transfer curve: 
- **Setup:**

```haskell
Meas 3 -200 -500 500 10 5 1
```
> This command can achieve an ECT transfer (`hysteresis`) with `Vds=-0.2V`, `Vg from -0.5V t0 +0.5V`, `10 mV Vg step` with `5 ms interval` (speed = 10mV/5ms = `2 V/s`). 
- **Start:**

```haskell
Start
```
> This command can run this measurement. 

- **Output:**
```haskell
----Transistor Transfer----
Ids, Vds, Vgs
-0.000,-0.200,-0.503
-0.000,-0.199,-0.502
-0.253,-0.200,-0.500
-0.253,-0.200,-0.498
...
```

#### ECT I-T curve

<hr/>

`ECT I-T curve` indicates the change in Ids with constant Vds and Vgs. It is the most popular and sample characterization for ECT to do applications such as sensing and computing. 

##### [#]() Configuration for ECT I-T curve: 

- **Meas 1 A B**

| Parameter        | Explain     | Unit | Range |
| ---------------- | ------------| ---- | ------|
| 1  | Fixed for ECT I-T curve. | N/A   | N/A  |
| A   | The voltage applied to Drain and Source.    | mV   | -1000 to +1000  |
| B      |  The voltage applied to Gate .  | mV   | -1000 to +1000 |
##### [#]() Data Output for ECT I-T curve: 

- **Ids, Vds, Vgs**
- **X1,X2,X3**

| Parameter        | Explain           | Unit |
| ---------------- | ----------------- | ---- |
| X1      | The I measured from Drain and Source. | uA  |
| X2      | The V measured from Drain and Source. | mV  | 
| X3      | The V measured at the Gate.  | mV   |

```haskell
----Transistor I-T----
Ids, Vds, Vgs
X1,X2,X3
X1,X2,X3
X1,X2,X3
...
```
##### [#]() Example for ECT I-T curve: 
- **Setup:**

```haskell
Meas 1 -200 200
```
> This command can achieve an ECT I-T curvewith `Vds=-0.2V`, `Vg=0.2V`. 
- **Start:**

```haskell
Start
```
> This command can run this measurement. 

- **Output:**
```haskell
----Transistor Transfer----
Ids, Vds, Vgs
-0.000,-0.193,0.202
-0.000,-0.193,0.202
-0.000,-0.193,0.202
...
```
- **Stop:**

```haskell
Stop
```
> This command can stop this measurement. 
```haskell
----Transistor IT END----

Stop 0
...
```
