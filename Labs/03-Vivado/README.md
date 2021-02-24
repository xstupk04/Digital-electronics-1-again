# Digital electronics 1  
# Third Labs - Logic
  
## First point: Preparation tasks
### The Nexys A7 board provides sixteen switches and LEDs

![Schema](https://raw.githubusercontent.com/xstupk04/Digital-electronics-1-again/main/Labs/03-Vivado/Schéma%20Leds.png)

## Second point: Two-bit wide 4-to-1 multiplexer
### Listing of VHDL architecture from source file:

```vhdl
architecture Behavioral of mux_2bit_4to1 is
begin
    f_o <= a_i when (sel_i = "00") else
           b_i when (sel_i = "01") else
           c_i when (sel_i = "10") else
           d_i;
    
end architecture Behavioral;
```
### Listing of VHDL stimulus process from testbench file:

```vhdl
--------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;
        
        -- First test values
        s_d <= "00"; s_c <= "00"; s_b <= "00"; s_a <= "00"; 
        s_sel <= "00"; wait for 100 ns;
        
        -- Second test values
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "00"; 
        s_sel <= "00"; wait for 100 ns;
        
        -- Thrid test values
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "11"; 
        s_sel <= "00"; wait for 100 ns;
        
        -- Fourth test values
        s_d <= "10"; s_c <= "01"; s_b <= "01"; s_a <= "00"; 
        s_sel <= "01"; wait for 100 ns;
        
        -- Fifht test values
        s_d <= "10"; s_c <= "01"; s_b <= "11"; s_a <= "00"; 
        s_sel <= "01"; wait for 100 ns;
        
        -- Sixth test values
        s_d <= "10"; s_c <= "01"; s_b <= "11"; s_a <= "00"; 
        s_sel <= "01"; wait for 100 ns;



        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;
```

### Screenshot with simulated time waveforms
![Time](https://raw.githubusercontent.com/xstupk04/Digital-electronics-1-again/main/Labs/03-Vivado/Průběh.png)

### A Vivado tutorial
```
--> Create project with name without czech symbols 
- Target language: VHDL
- Simulator language: VHDL
- Type of board : Nexys A7-50T
- Write your code in VHD language and test it with your testbench 
- Start simulation and verify your correctness
- Connect Leds, Switches, buttons, displays with your board 
```

