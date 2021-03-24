# Digital electronics 1
## First point: preparation tasks (done before the lab at home)

Write characteristic equations and complete truth tables for D, JK, T flip-flops where `Qn` represents main output value before clock edge and `Q(n+1)` represents value after the edge.

   | **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 |  |  |
   | 0 | 1 |  |  |
   | 1 |  |  |  |
   | 1 |  |  |  |

   | **J** | **K** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | 0 | No change |
   | 0 | 0 | 1 | 1 | No change |
   | 0 |  |  |  |  |
   | 0 |  |  |  |  |
   | 1 |  |  |  |  |
   | 1 |  |  |  |  |
   | 1 |  |  |  |  |
   | 1 |  |  |  |  |

   | **T** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 |  |  |
   | 0 | 1 |  |  |
   | 1 |  |  |  |
   | 1 |  |  |  |



```vhdl
-- LED(7:4) indicators
    -- Turn LED(4) on if input value is equal to 0, ie "0000"

       LED(4) <=   '0' when (SW = "0000") else
                        '1' ;
    -- Turn LED(5) on if input value is greater than "1001", ie 9

       LED(5) <=   '0' when (SW > "1001") else
                        '1'; 
    
    -- Turn LED(6) on if input value is odd, ie 1, 3, 5, ...
    
      LED(6) <=   '0' when (SW = "0001") else
                        '0' when (SW = "0011") else
                        '0' when (SW = "0101") else
                        '0' when (SW = "0111") else
                        '0' when (SW = "1001") else
                        '0' when (SW = "1011") else                        
                        '0' when (SW = "1101") else                        
                        '0' when (SW = "1111") else
                        '1';
           
    
    -- Turn LED(7) on if input value is a power of two, ie 1, 2, 4, or 8
    
    LED(7) <=   '0' when (SW = "0001") else
                        '0' when (SW = "0010") else                     
                        '0' when (SW = "0100") else                        
                        '0' when (SW = "1000")else
                        '1' ;  
```  

![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)
