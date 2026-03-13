# **1-TOPS** proposed architecture   

<img width="641" height="473" alt="image" src="https://github.com/user-attachments/assets/5beb36e6-c54a-464f-b28a-0277047e891b" />

--------

# 8 BIT SAR-ADC (**ADC Analog Peripheral**)
------

A Successive Approximation Register Analog-to-Digital Converter (SAR ADC) is a type of ADC architecture that converts an analog input signal into a digital output through a binary search process. It offers a balance of speed, accuracy, and power efficiency, making it widely used in mixed-signal and embedded systems.    

The main fundamental building blocks of a SAR-ADC are :         
**1. Sample & Hold circuit**      
**2. DAC**     
**3. Comparator**     
**4. SAR logic (Successive Aproximation register)**   

*P-1 : Conventional Architecture* 

![Untitled design](https://github.com/user-attachments/assets/8c9f3bce-6127-4628-af94-13b20ed0af2f)

*p-2 : Monotonic Switching Architecture*

- Brief Working of SAR ADC    
   1. The Capacitor network serves as both S/H circuit and a reference DAC capacitor array.      
   2. **Sampling the Input** : The analog input voltage is first sampled and held by a sample-and-hold circuit so it remains constant during the conversion process.    
   3. **Initial Guess (MSB Test)** : The SAR logic sets the most significant bit (MSB) to 1 and all other bits to 0. This digital code is sent to the DAC.
   4. **DAC Generates Comparison Voltage** : The Digital-to-Analog Converter converts this digital code into an analog voltage.
   5. **Comparison** : A Analog Comparator compares ***Vin*** and ***Vdac***.  
      - If ***Vin > Vdac*** -> keep that bit as 1.    
      - If ***Vin < Vdac*** -> keep that bit as 0.     
   6. **Binary Search Process** : This process continues bit-by-bit from MSB to LSB, each time refining the approximation.
   7. **Final Digital Output** : After N clock cycles for an N-bit ADC, the SAR register contains the final digital representation of ***Vin***.

- **Conventional Switching Architecture**
  - no. of unit cap -> 2^N -> 256
  - Total cap -> 2N + 2 -> 18
  - Total switches -> 4N+10 -> 42
  - Large switchingg energy : Large capacitors causes large energy consumption.
    - The average switching energy for 8 bit ≈ 339.34 CV²_ref

$$E_{avg,conv} = \sum_{i=1}^{n} 2^{n+1-2i}(2^i - 1)CV_{ref}^2$$

  - Bidirectionl switching
    - Vreff -> GND
    - GND -> Vreff
  - High switch counts : Each cap needs switches for three state : Vin, Vreff, GND


- **Monotonic Switching Architecture**
  - no. of unit cap -> 2^(N-1) -> 128
  - Total cap -> 2N -> 16
  - Total switches -> 4N -> 32
  - Less switching energy : average switching energy for 8 bit ≈ 63.5 CV²_ref

$$E_{avg,mono} = \sum_{i=1}^{n-1} 2^{n-2-i} CV_{ref}^2$$

  - Unidirectional switching : Vreff -> GND
  - Each cap needs switvhes for two state : Vreff, GND

---------------------

## Monotonic Switching Architecture

- Two identical capacitor arrays  
   - Top array -> connected to comparator positive (+)  
   - Bottom array -> connected to comparator negative (–)
     
- Each array has:   
   - Binary weighted capacitors :       

$$
C_i = 2C_{i+1}
$$


   - A fully differential comparator
   - SAR logic controlling switches S1p…S8p and S1n…S8n
​
-----
## Individual Block :

### **1. Capacitor DAC**

   <img width="1021" height="580" alt="image" src="https://github.com/user-attachments/assets/cc039a85-4fa5-4a51-a109-b76faa38e8ba" />

- The Capacitor network serves as both S/H circuit and a reference DAC capacitor array. 

- **Phase 1 : Sampling phase**
  - Top array bottom plates -> Vip
  - Bottom array bottom plates -> Vin
  - Top plates -> Vcm
  - So both arrays sample the input.

  - The voltage stored on capacitors :
    
$$
Q_{initial} = C(V_{cm} - V_{ip})
$$

$$
Q_{initial} = C(V_{cm} - V_{in})
$$

Each side stores equal charge.
  - Since it's differential:

$$
V_{d} = V_{ip} - V_{in}
$$

  - If input is:

$$
V_{ip} = V_{cm} + \frac{V_{diff}}{2}
$$

$$
V_{in} = V_{cm} - \frac{V_{diff}}{2}
$$

- **Phase 2 — Conversion Phase :**
  - Input is disconnected.
  - Top node becomes floating.
  - Total charge must remain constant.
