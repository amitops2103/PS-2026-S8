
# 8 BIT SAR-ADC
------
The main fundamental building blocks of a SAR-ADC are :         
        |___ **1. Sample & Hold circuit**      
        |___ **2. DAC**     
        |___ **3. Comparator**     
        |___ **4. SAR logic (Successive Aproximation register)**     

![Untitled design](https://github.com/user-attachments/assets/8c9f3bce-6127-4628-af94-13b20ed0af2f)

- Two identical capacitor arrays  
   - Top array -> connected to comparator positive (+)  
   - Bottom array -> connected to comparator negative (–)
     
- Each array has:   
   - Binary weighted capacitors :       

$$
C_i = 2C_{i+1}
$$
     
  | Capacitor  | Weight  | Capacitance  |
  |------------|---------|--------------|
  | C₉ = C₈    | 128C    |              |
  | C₈         | 128C    |  MSB (split) |
  | C₇         | 64C     |              |
  | C₆         | 32C     |              |
  | C₅         | 16C     |              |
  | C₄         | 8C      |              |
  | C₃         | 4C      |              |
  | C₂         | 2C      |              |
  | C₁         | 1C      |  LSB         |

   Total = 256C 

   
   - An extra capacitor:
   
$$
C_9 = C_8
$$

(dummy / matching capacitor)

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
