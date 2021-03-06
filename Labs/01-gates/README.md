# Digital electronics 1
  link to my github: https://github.com/xstupk04/Digital-electronics-1-again
## Second point 
### Verification of De Morgan's laws of function f(c,b,a).

| **c** | **b** |**a** | **f(c,b,a)** |
| :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |

![gif latex-1](https://user-images.githubusercontent.com/60606149/107531301-fbf39380-6bbc-11eb-8954-df8fea841bc8.gif)

![gif latex-2](https://user-images.githubusercontent.com/60606149/107535585-26dfe680-6bc1-11eb-9cbe-f7e53bfc7b4f.gif)

![gif latex-3](https://user-images.githubusercontent.com/60606149/107536541-2e53bf80-6bc2-11eb-844b-54f0c4c99065.gif)




```vhdl
------------------------------------------------------------------------
--
-- Example of basic OR, AND, XOR gates.
-- Nexys A7-50T, Vivado v2020.1, EDA Playground
--
-- Copyright (c) 2019-2020 Tomas Fryza
-- Dept. of Radio Electronics, Brno University of Technology, Czechia
-- This work is licensed under the terms of the MIT license.
--
------------------------------------------------------------------------

library ieee;               -- Standard library
use ieee.std_logic_1164.all;-- Package for data types and logic operations

------------------------------------------------------------------------
-- Entity declaration for basic gates
------------------------------------------------------------------------
entity gates is
    port(
        a_i    : in  std_logic;         -- Data input
        b_i    : in  std_logic;         -- Data input
        c_i	   : in  std_logic;
        f_o  : out std_logic;        -- OR output function
        fnand_o : out std_logic;         -- AND output function
        fnor_o : out std_logic          -- XOR output function
    );
end entity gates;

------------------------------------------------------------------------
-- Architecture body for basic gates
------------------------------------------------------------------------
architecture dataflow of gates is
begin
    f_o  <= ((not b_i) and a_i) or ((not c_i) and (not b_i));
    fnand_o <= not((not (not b_i and a_i)) and not(((not c_i) and (not b_i))));
    fnor_o <= not (b_i or not a_i) or not (c_i or b_i);

end architecture dataflow;
```
* Link to VHDL code: [EDA playgroud code](https://www.edaplayground.com/x/FU4c)

#### Screenshot with simulated time waveforms
![Prubeh](https://user-images.githubusercontent.com/60606149/107642241-e2ae1e00-6c74-11eb-9e5b-a164c7d4c200.png)


## Thrid point 
### Verification of Distributive laws and basic Boolean postulates
![Boolean](https://user-images.githubusercontent.com/60606149/107653578-1479b180-6c82-11eb-8de1-e77bd16e4581.gif)

![Boolean](https://user-images.githubusercontent.com/60606149/107653583-16437500-6c82-11eb-932d-2ad325b4d364.gif)

![Boolean](https://user-images.githubusercontent.com/60606149/107653592-180d3880-6c82-11eb-95f8-59803c288771.gif)

![Boolean](https://user-images.githubusercontent.com/60606149/107653595-19d6fc00-6c82-11eb-9003-469eaf389aa1.gif)



![Distributive laws](https://user-images.githubusercontent.com/60606149/107654420-f1033680-6c82-11eb-8ee8-f97803c750b0.gif)

![Distributive laws](https://user-images.githubusercontent.com/60606149/107654426-f2346380-6c82-11eb-8ee6-1653158f0760.gif)

Listing of VHDL code
```vhdl
------------------------------------------------------------------------
--
-- Example of basic OR, AND, XOR gates.
-- Nexys A7-50T, Vivado v2020.1, EDA Playground
--
-- Copyright (c) 2019-2020 Tomas Fryza
-- Dept. of Radio Electronics, Brno University of Technology, Czechia
-- This work is licensed under the terms of the MIT license.
--
------------------------------------------------------------------------

library ieee;               -- Standard library
use ieee.std_logic_1164.all;-- Package for data types and logic operations

------------------------------------------------------------------------
-- Entity declaration for basic gates
------------------------------------------------------------------------
entity gates is
    port(
        x_i     : in  std_logic;         -- Data input
        y_i     : in  std_logic;         -- Data input
        z_i     : in  std_logic;         -- Data input
        f1_o    : out std_logic;         -- output function 1
        f2_o    : out std_logic;         -- output function 2
        f3_o    : out std_logic;         -- output function 3
        f4_o    : out std_logic;          -- output function 4
        f5_o    : out std_logic;          -- output function 5
        f6_o    : out std_logic;         -- output function 6
        f7_o    : out std_logic;          -- output function 7
        f8_o    : out std_logic          -- output function 8
    );
end entity gates;

------------------------------------------------------------------------
-- Architecture body for basic gates
------------------------------------------------------------------------
architecture dataflow of gates is
begin
   	f1_o <= (x_i and y_i) or (x_i and z_i);
    f2_o <= x_i and (y_i or z_i);
    f3_o <= (x_i or y_i) and (x_i or z_i);
    f4_o <= x_i or (y_i and z_i);
    f5_o <= x_i and not x_i;
    f6_o <= x_i or not x_i;
    f7_o <= x_i or x_i or x_i;
    f8_o <= x_i or (y_i and z_i);
    

end architecture dataflow;

```
* Link to VHDL code: [EDA playgroud code](https://www.edaplayground.com/x/NiR2)

#### Screenshot with simulated time waveforms
![Prubeh](https://user-images.githubusercontent.com/60606149/107651071-65d47180-6c7f-11eb-822e-a0ddef5f6a76.png)
###### f1_o ÷ f4_o verify Distributive laws
###### f5_o ÷ f8_o verify basic Boolean postulates
 
