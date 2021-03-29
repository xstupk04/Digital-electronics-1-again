# Digital electronics 1
## First point: preparation tasks (done before the lab at home)

Write characteristic equations and complete truth tables for D, JK, T flip-flops where `Qn` represents main output value before clock edge and `Q(n+1)` represents value after the edge.

   | **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | R |
   | 0 | 1 | 0 | R |
   | 1 | 0 | 1 | S |
   | 1 | 1 | 1 | S |

   | **J** | **K** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | 0 | No change |
   | 0 | 0 | 1 | 1 | No change |
   | 0 | 1 | 0 | 0 | R |
   | 0 | 1 | 1 | 0 | R |
   | 1 | 0 | 0 | 1 | S |
   | 1 | 0 | 1 | 1 | S |
   | 1 | 1 | 0 | 1 | Invert |
   | 1 | 1 | 1 | 0 | Invert |

   | **T** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | No change |
   | 0 | 1 | 1 | No change |
   | 1 | 1 | 1 | Invert |
   | 1 | 0 | 0 | Invert |

## Second point: D latch
### VHDL code listing of the process p_d_latch with syntax highlighting

```vhdl
p_d_latch : process (d, arst, en)
    begin
        if (arst = '1' ) then
            q     <= '0';
            q_bar <= '1';
        elsif (en = '1')then
            q     <= d;
            q_bar <= not d;
        end if;
    end process p_d_latch;
```

### Listing of VHDL reset and stimulus processes from the testbench tb_d_latch.vhd
```vhdl
entity tb_d_latch is
--  Port ( );
end tb_d_latch;

architecture Behavioral of tb_d_latch is

           signal s_en       : STD_LOGIC;
           signal s_d        : STD_LOGIC;
           signal s_arst     : STD_LOGIC;
           signal s_q        : STD_LOGIC;
           signal s_q_bar    : STD_LOGIC;

begin
 uut_d_latch : entity work.d_latch
        port map(
           en       => s_en,
           d        => s_d,
           arst     => s_arst,
           q        => s_q,
           q_bar    => s_q_bar
        );
  -- arst process
        p_arst_gen : process       

begin
        s_arst <= '0';
        wait for 10 ns;        
        
        -- arst activated
        s_arst <= '1';
        wait for 10 ns;

        -- arst deactivated
        s_arst <= '0';
        wait for 200 ns;
        
        s_arst <= '1';         

        wait;
    end process p_arst_gen;

         p_stimulus : process
    begin
        report "Stimulus process started" severity note;
            
          s_en <= '0';
          s_d <= '0';         
         
          wait for 6 ns;          
          s_d   <= '1';
          wait for 5 ns;
          s_d   <= '0';
          wait for 8 ns;
           s_d  <= '1';
          wait for 6 ns;
          s_d   <= '0';
          wait for 9 ns;
          s_d   <= '1';
          wait for 4 ns;
          s_d   <= '0';
          wait for 5 ns;          
          
          s_en  <= '1';
          wait for 6 ns;          
          s_d   <= '1';
          wait for 3 ns;
          s_d   <= '0';
          wait for 10 ns;
          s_d   <= '1';
          wait for 5 ns;
          s_d   <= '0';
          wait for 6 ns;
          s_d  <= '1';
          wait for 25 ns;
          s_d   <= '0';
          wait for 15 ns;
          s_en  <= '0';
          wait for 4 ns;
          s_d  <= '1';
          wait for 16 ns;
          
          s_en  <= '1';
          wait for 6 ns;          
          s_d   <= '1';
          wait for 5 ns;
          s_d   <= '0';
          wait for 5 ns;
           s_d  <= '1';
          wait for 5 ns;
          s_d   <= '0';
          wait for 5 ns;
           s_d  <= '1';
          wait for 5 ns;
          s_d   <= '0';
          wait for 17 ns;
          
          s_d   <= '1';
          wait for 10 ns;
          s_en  <= '0';
          wait for 10 ns;
          s_d   <= '0';          
          wait for 6 ns;          
          s_d   <= '1';
          wait for 15 ns;
          s_d   <= '0';
          wait for 6 ns;
           s_d  <= '1';
           wait for 5 ns;
          s_en  <= '1';
          wait for 3 ns;
          s_d   <= '0';
          wait for 5 ns;
           s_d  <= '1';
          wait for 8 ns;
          s_d   <= '0';
          wait for 15 ns;
         
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
    
   p_assert : process
    begin
      wait for 3 ns;
              
        -- assert in 80 ns
        assert(s_q = '0' and s_q_bar = '1')
        report "Error - in 3 ns " severity error;
        
      wait for 45 ns;
         -- assert in 125 ns
        assert(s_q = '0' and s_q_bar = '1')
        report "Error -  in 125 ns" severity error;
       
    end process p_assert;
          
end Behavioral;
```

### Screenshot with simulated time waveforms; always display all inputs and outputs.
![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)


## Thrid point: D latch
### VHDL code listing of the processes p_d_ff_arst, p_d_ff_rst, p_jk_ff_rst, p_t_ff_rst
### Listing of VHDL clock, reset and stimulus processes from the testbench files with syntax highlighting and asserts
### Screenshot with simulated time waveforms; always display all inputs and outputs.

## Fourth point: Shift register 
### Image of the shift register schematic.


```vhdl
-- LED(7:4) indicators

```  

![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)
