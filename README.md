# NGSPICE SIMULATION HELP 

## INSTALLATION 
1.On Debian like distros execute following 
```
sudo apt-get install ngspice 

```
## File Format 
We recommend the following file format .
``` 
First line should be name and roll no and ckt description.
**comments begin with astericks
**extention of files should be .cir or .spice 

**parameter 


**circuit 



**sim command 


.end 
```

## USAGE 
1.
```
$ ngspice yourCircuit.cir 
```

## DEVICES 
Here's a brief reference of the SPICE devices and statements. Parameters enclosed by braces { } are 
required, while, those in brackets [ ] are optional. Parameters followed by an asterisk { }* should 
be repeated as necessary 

1. .C device - Capacitor. 
	C{name} {+node} {-node} [{model}] {value} [IC={initial}] 
	Examples: 
	CLOAD  15  0  20pF
	CFDBK   3 33  CMOD 10pF IC=1.5v 

2. .D device - Diode. 
	D{name} {+node} {-node} {model}  [area]
	Examples: 
	DCLAMP  14  0  DMOD 

3. .I device - Current Source. 
	I{name} {+node} {-node} [[DC] {value}] [AC {mag} [{phase}]]
	Examples: 
	IBIAS  13  0  2.3mA 
	IAC    2   3  AC .001 
	IPULSE 1   0  PULSE(-1mA 1mA 2ns 2ns 2ns 50ns 100ns) 
	I3    26  77  AC 1 SIN(.002 .002 1.5MEG)

4. .L device - Inductor.  
	L{name} {+node} {-node} [model] {value} [IC={initial}]  
	Examples: 
	LLOAD  15  0   20mH 
	L2      1  2   .2e-6 
	LSENSE  5 12   2uH IC=2mA

5. .R device - Resistor.  
	R{name}  {+node} {-node} [{model}] {value}  
	Examples: 
	RLOAD  15  0  2k 

6. .V device - Voltage Source.  
	V{name} {+node} {-node} [[DC] {value}] [AC {mag} [{phase}]] 
	Examples: 
	VBIAS  13  0  2.3mV 
	VAC    2   3  AC .001 
	VPULSE 1   0 PULSE(-1mV 1mV 2ns 2ns 2ns 50ns 100ns) 
	V3    26  77  AC 1 SIN(.002 .002 1.5MEG)

7. .X device - Subcircuit Call.  
	X{name} [{node}]* {subcircuit name} 
	Examples: 
	X12  100 101  200 201  DIFFAMP 

## INPUT SOURCES 

1. .PULSE
	PULSE( {v1} {v2} {tdelay} {trise} {tfall} {width} {period} 

2. .PIECE WISE LINEAR
	PWL( {time1} {v1} {time2} {v2} ... {time3} {v3} )

3. .SINE WAVE
	SIN( {voffset} {vpeak} {freq} {tdelay} {damp_factor} {phase} )

## STATEMENTS 

1. .AC - AC Analysis.  
	.AC [LIN][OCT][DEC] {points} {start} {end}  
	Examples: 
	.AC  LIN  101  10Hz  200Hz 
	.AC  DEC   20  1MEG 100MEG

2. .DC - DC Analysis.
	.DC [LIN] {varname}  {start} {end} {incr}
	.DC [OCT][DEC] {varname} {start} {end} {points} 
	Examples: 
	.DC  VIN  -.25  .25  .05 
	.DC  LIN I2 5mA -2mA 0.1mA  VCE 10V 15V 1V

3. .IC - Initial Transient Conditions.  
	.IC { {vnode} = {value} }*  
	Examples: 
	.IC  V(2)=3.4  V(102)=0

4. .SUBCKT - Subcircuit Definition.  
	.SUBCKT {name} [{node}*] 
	Examples: 
	.SUBCKT  OPAMP 1 2 101 102 

5. .TRAN - Transient Analysis.  
	.TRAN {print step value} {final time} [{start_time_for_save}]  
	Examples: 
	.TRAN 5NS 100NS
 
