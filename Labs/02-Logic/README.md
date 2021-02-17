# Digital-electronics-1
  ## Second Labs 
### First point: Preparation tasks

| **Dec. equivalent** | **B[1:0]** | **A[1:0]** | **B is greater than A** | **B equals A** | **B is less than A** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 0 | 0 0 | 0 | 1 | 0 |
| 1 | 0 0 | 0 1 | 0 | 0 | 1 |
| 2 | 0 0 | 1 0 | 0 | 0 | 1 |
| 3 | 0 0 | 1 1 | 0 | 0 | 1 |
| 4 | 0 1 | 0 0 | 1 | 0 | 0 |
| 5 | 0 1 | 0 1 | 0 | 1 | 0 |
| 6 | 0 1 | 1 0 | 0 | 0 | 1 |
| 7 | 0 1 | 1 1 | 0 | 0 | 1 |
| 8 | 1 0 | 0 0 | 1 | 0 | 0 |
| 9 | 1 0 | 0 1 | 1 | 0 | 0 |
| 10 | 1 0 | 1 0 | 0 | 1 | 0 |
| 11 | 1 0 | 1 1 | 0 | 0 | 1 |
| 12 | 1 1 | 0 0 | 1 | 0 | 0 |
| 13 | 1 1 | 0 1 | 1 | 0 | 0 |
| 14 | 1 1 | 1 0 | 1 | 0 | 0 |
| 15 | 1 1 | 1 1 | 0 | 1 | 0 |

According to the truth table, write canonical SoP (Sum of Products) and PoS (Product of Sums) forms for "equals" and "less than" functions:

![PoS](https://user-images.githubusercontent.com/60606149/108215914-2354de00-7132-11eb-9e93-31527790d3d5.gif)
![SoP](https://user-images.githubusercontent.com/60606149/108217657-25b83780-7134-11eb-856a-1b495bbcbeb5.gif)

### Second point: 2-bit comparator

#### Karnaugh maps for all three functions

##### K-map for the "equals" function is as follows:
![SoP](https://user-images.githubusercontent.com/60606149/108217657-25b83780-7134-11eb-856a-1b495bbcbeb5.gif)
![K1](https://user-images.githubusercontent.com/60606149/108256977-780e4e00-715e-11eb-9ec4-520146cf5102.png)

##### K-map for the "greater" function is as follows:
![K2](https://user-images.githubusercontent.com/60606149/108257180-b7d53580-715e-11eb-877d-32fd9440cd4f.png)

![Greatermin](https://user-images.githubusercontent.com/60606149/108259539-801bbd00-7161-11eb-8ffc-b8e50731b439.gif)

##### K-map for the "less" function is as follows:
![K3](https://user-images.githubusercontent.com/60606149/108257255-ce7b8c80-715e-11eb-91f6-4e503d75d109.png)

![lessmin](https://user-images.githubusercontent.com/60606149/108259668-a8a3b700-7161-11eb-91a8-71a514b0efdc.gif)

EDA Playground example code 2-bit comparator
https://www.edaplayground.com/x/PyYQ 

### Third point: 2-bit comparator

##### Listing of VHDL architecture from design file

```vhdl
------------------------------------------------------------------------
--
-- Example of 4-bit binary comparator using the when/else assignment.
-- EDA Playground
--
-- Copyright (c) 2020-2021 Tomas Fryza
-- Dept. of Radio Electronics, Brno University of Technology, Czechia
-- This work is licensed under the terms of the MIT license.
--
------------------------------------------------------------------------

library ieee;
use ieee.std_logic_1164.all;

------------------------------------------------------------------------
-- Entity declaration for 4-bit binary comparator
------------------------------------------------------------------------
entity comparator_4bit is
    port(
        a_i           : in  std_logic_vector(4 - 1 downto 0);
        b_i           : in  std_logic_vector(4 - 1 downto 0);


        B_less_A_o    		 : out std_logic;       -- B is less than A
        B_greater_A_o	     : out std_logic;       -- B is greater than A
        B_equals_A_o		 : out std_logic       -- B equals than A
        
    );
end entity comparator_4bit;

------------------------------------------------------------------------
-- Architecture body for 4-bit binary comparator
------------------------------------------------------------------------
architecture Behavioral of comparator_4bit is
begin
    B_less_A_o   	<= '1' when (b_i < a_i) else '0';
    B_greater_A_o	<= '1' when (b_i > a_i) else '0';
	B_equals_A_o	<= '1' when (b_i = a_i) else '0';

end architecture Behavioral;
```

##### Listing of VHDL stimulus process from testbench file

```vhdl
library ieee;
use ieee.std_logic_1164.all;

------------------------------------------------------------------------
-- Entity declaration for testbench
------------------------------------------------------------------------
entity tb_comparator_2bit is
    -- Entity of testbench is always empty
end entity tb_comparator_2bit;

------------------------------------------------------------------------
-- Architecture body for testbench
------------------------------------------------------------------------
architecture testbench of tb_comparator_2bit is

    -- Local signals
    signal s_a       : std_logic_vector(2 - 1 downto 0);
    signal s_b       : std_logic_vector(2 - 1 downto 0);
    signal s_B_greater_A : std_logic;
    signal s_B_equals_A  : std_logic;
    signal s_B_less_A    : std_logic;

begin
    -- Connecting testbench signals with comparator_2bit entity (Unit Under Test)
    uut_comparator_2bit : entity work.comparator_2bit
        port map(
            a_i           => s_a,
            b_i           => s_b,
            B_greater_A_o => s_B_greater_A,
            B_equals_A_o  => s_B_equals_A,
            B_less_A_o    => s_B_less_A
        );

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;


        -- First test values
        s_b <= "00"; s_a <= "00"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        
        -- Second test values
        s_b <= "00"; s_a <= "01"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        -- Third test values
        s_b <= "01"; s_a <= "01"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        -- Fourth test values
        s_b <= "11"; s_a <= "01"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        -- Fifth test values
        s_b <= "00"; s_a <= "10"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        -- Sixth test values
        s_b <= "10"; s_a <= "10"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
         
        -- Seventh test values
        s_b <= "11"; s_a <= "00"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;
        
        -- Eighth test values
        s_b <= "11"; s_a <= "11"; wait for 100 ns;
        -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 00, 00" severity error;

        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;


```

##### Listing of simulator console output, i.e. with one reported error,

![Stimulus error](https://user-images.githubusercontent.com/60606149/108278278-17413e80-717b-11eb-9586-913f348c5aab.png)

##### Link to my public EDA Playground example with 4-bit comparator
https://www.edaplayground.com/x/QZQE

