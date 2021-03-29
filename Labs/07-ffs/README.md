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

```vhdl

```
### Screenshot with simulated time waveforms; always display all inputs and outputs.
![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)


## Thrid point: D latch
### VHDL code listing of the processes p_d_ff_arst

```vhdl
architecture Behavioral of d_ff_arst is

begin

p_d_ff_arst : process (arst, clk)
    begin
        if (arst = '1' ) then
            q     <= '0';
            q_bar <= '1';
        elsif rising_edge (clk)then
            q     <= d;
            q_bar <= not d;
            
        end if;
    end process p_d_ff_arst;

end Behavioral;
```
### Listing of VHDL clock, reset and stimulus processes from the testbench files with syntax highlighting and asserts
```vhdl
--------------------------------------------------------------------
    -- Clock generation process
--------------------------------------------------------------------        
        
 p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
 
 --------------------------------------------------------------------
    -- Reset generation process
 --------------------------------------------------------------------
    
    p_reset_gen : process
    begin
        s_arst <= '0';
        wait for 58 ns;
        
        -- Reset activated
        s_arst <= '1';
        wait for 15 ns;

        -- Reset deactivated
        s_arst <= '0';

        wait;
    end process p_reset_gen;
   
 p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        -- 3.142
          wait for 13 ns;          
          s_d   <= '1';
          wait for 10 ns;
          s_d   <= '0';
          wait for 10 ns;
           s_d  <= '1';
          wait for 10 ns;
          s_d   <= '0';
          wait for 10 ns;
          s_d   <= '1';
          wait for 10 ns;
          s_d   <= '0';
          wait for 10 ns;         

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;   

end Behavioral;
```
### Screenshot with simulated time waveforms; always display all inputs and outputs.


### VHDL code listing of the processes  p_d_ff_rst
```vhdl
 p_d_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                q     <= '0';
                q_bar <= '1';
            else
                q     <= d;
                q_bar <= not d;
            end if;
        end if;
    end process p_d_ff_rst;

end Behavioral;
```
### Listing of VHDL clock, reset and stimulus processes from the testbench files with syntax highlighting and asserts
```vhdl
--------------------------------------------------------------------
    -- Clock generation process
    --------------------------------------------------------------------
    p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset_gen :   process
    begin
        s_rst <=  '1';
        wait for 10 ns;
        s_rst <=  '0';
        wait for 20 ns;
        s_rst <=  '1';
        wait for 20 ns;

        s_rst <=  '0';
        
        wait;
    end process p_reset_gen;
    
    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_t     <= '0';
        wait for 20 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        
        assert(s_q =  '1' and s_q_bar = '0')
        report "First assert s_q = 1, s_q_bar = 0" severity error;
        
        wait for 10 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        
        assert(s_q =  '0' and s_q_bar = '1')
        report "Second assert s_q = 0, s_q_bar = 1" severity error;

        wait for 10 ns;
        
        s_t     <= '0';

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;


end Behavioral;
```
### Screenshot with simulated time waveforms; always display all inputs and outputs.

### VHDL code listing of the processes  p_jk_ff_rst
```vhdl
architecture Behavioral of jk_ff_rst is
    signal s_q : std_logic;
begin
    p_jk_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                s_q <= '0';
            else
                if (j = '0' and k = '0') then
                    s_q <= s_q;
                    
                elsif (j = '0' and k = '1') then
                    s_q <= '0';
                    
                elsif (j = '1' and k = '0') then
                    s_q <= '1';
                    
                elsif (j = '1' and k = '1') then
                    s_q <= not s_q;
                
                end if;
            end if;
        end if;
    end process p_jk_ff_rst;

    q       <= s_q;
    q_bar   <= not s_q;
    
end Behavioral;
```
### Listing of VHDL clock, reset and stimulus processes from the testbench files with syntax highlighting and asserts
```vhdl
 --------------------------------------------------------------------
    -- Clock generation process
    --------------------------------------------------------------------
    p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset_gen :   process
    begin
        s_rst <=  '0';
        wait for 40 ns;
        
        s_rst <=  '1';
        wait for 40 ns;
        
        s_rst <=  '0';
        
        wait;
    end process p_reset_gen;

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        
        s_j     <= '0';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '0';
        s_k     <= '1';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '1';
        wait for 10 ns;
        
        assert(s_q =  '1' and s_q_bar = '0')
        report "First assert s_q = 1, s_q_bar = 0" severity error;
        
        s_j     <= '0';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '0';
        s_k     <= '1';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '1';
        
        assert(s_q =  '1' and s_q_bar = '0')
        report "Second assert s_q = 1, s_q_bar = 0" severity error;

        wait for 10 ns;

        s_j     <= '0';
        s_k     <= '0';

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
    
end Behavioral;
```
### Screenshot with simulated time waveforms; always display all inputs and outputs.

### VHDL code listing of the processes p_t_ff_rst
```vhdl
p_t_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                s_q     <= '0';
                s_q_bar <= '1';
            elsif (t = '1') then
                s_q     <= not s_q;
                s_q_bar <= s_q;
            end if;
        end if;
    end process p_t_ff_rst;
    q       <= s_q;
    q_bar   <= s_q_bar;
end Behavioral;

```
### Listing of VHDL clock, reset and stimulus processes from the testbench files with syntax highlighting and asserts
```vhdl
 --------------------------------------------------------------------
    -- Clock generation process
    --------------------------------------------------------------------
    p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset_gen :   process
    begin
        s_rst <=  '1';
        wait for 10 ns;
        s_rst <=  '0';
        wait for 20 ns;
        s_rst <=  '1';
        wait for 20 ns;

        s_rst <=  '0';
        
        wait;
    end process p_reset_gen;
    
    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_t     <= '0';
        wait for 20 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        
        assert(s_q =  '1' and s_q_bar = '0')
        report "First assert s_q = 1, s_q_bar = 0" severity error;
        
        wait for 10 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        
        assert(s_q =  '0' and s_q_bar = '1')
        report "Second assert s_q = 0, s_q_bar = 1" severity error;

        wait for 10 ns;
        
        s_t     <= '0';

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;


end Behavioral;
```
### Screenshot with simulated time waveforms; always display all inputs and outputs.




## Fourth point: Shift register 
### Image of the shift register schematic.


```vhdl
-- LED(7:4) indicators

```  

![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)
