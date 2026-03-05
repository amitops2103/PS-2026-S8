
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
   - Binary weighted capacitors
         **Ci​=2Ci+1**
   - So :
     
    | Capacitor  | Weight  | Capacitance  |
    |------------|---------|--------------|
    | C₉ = C₈    | 128C    |  MSB (split) |
    | C₈         | 128C    |              |
    | C₇         | 64C     |              |
    | C₆         | 32C     |              |
    | C₅         | 16C     |              |
    | C₄         | 8C      |              |
    | C₃         | 4C      |              |
    | C₂         | 2C      |              |
    | C₁         | 1C      |  LSB         |

   Total = 256C                   
    ​
-----
## Individual Block :

### **1. Capacitor DAC**

   <img width="1021" height="580" alt="image" src="https://github.com/user-attachments/assets/cc039a85-4fa5-4a51-a109-b76faa38e8ba" />
- The Capacitaor network serves as both S/H circuit and a reference DAC capacitor array. 
