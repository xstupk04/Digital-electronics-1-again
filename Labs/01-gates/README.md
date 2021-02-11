# Digital electronics 1
  link to my github: https://github.com/xstupk04/Digital-electronics-1-again
## Second point 

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
```bash
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

![Prubeh](https://user-images.githubusercontent.com/60606149/107642241-e2ae1e00-6c74-11eb-9e5b-a164c7d4c200.png)

* Link to VHDL code: [Eda playgroud code](https://www.edaplayground.com/x/FU4c)

## Thrid point 

