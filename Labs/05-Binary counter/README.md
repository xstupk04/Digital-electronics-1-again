# Digital electronics 1
## First point: preparation tasks (done before the lab at home)

   | **Time interval** | **Number of clk periods** | **Number of clk periods in hex** | **Number of clk periods in binary** |
   | :-: | :-: | :-: | :-: |
   | 2&nbsp;ms | 200 000 | `x"3_0d40"` | `b"0011_0000_1101_0100_0000"` |
   | 4&nbsp;ms | 400 000 | `x"61A80`   | `b"1100001101010000000"`      |
   | 10&nbsp;ms | 1 000 0000 |`x"F4240`| `b"11110100001001000000"`     |
   | 250&nbsp;ms |25 000 000|`x"17D7840`|`b"1011111010111100001000000"`|
   | 500&nbsp;ms |50 000 000|`x"2FAF080`|`b"10111110101111000010000000"`|
   | 1&nbsp;sec | 100 000 000 | `x"5F5_E100"` | `b"0101_1111_0101_1110_0001_0000_0000"` |
   
   ![Schematic](https://raw.githubusercontent.com/xstupk04/Digital-electronics-1-again/main/Labs/03-Vivado/Schéma%20Leds.png)
   
   ### Second point: Bidirectional counter
   
   #### Listing of VHDL code of the process p_cnt_up_down
  ```vhdl 
    begin
        if rising_edge(clk) then
        
            if (reset = '1') then               -- Synchronous reset
                s_cnt_local <= (others => '0'); -- Clear all bits

            elsif (en_i = '1') then       -- Test if counter is enabled


            -- TEST COUNTER DIRECTION HERE
                if (cnt_up_i = '1') then
                
                  s_cnt_local <= s_cnt_local + 1;
 
               else 
                 
                 s_cnt_local <= s_cnt_local - 1;
             end if;
            end if;
        end if;
    end process p_cnt_up_down;
   
 ```
 
  #### Listing of VHDL reset and stimulus processes from testbench file tb_cnt_up_down.vhd
  
```vhdl 
   p_reset_gen : process
    begin
        s_reset <= '0';
        wait for 12 ns;
        
        -- Reset activated
        s_reset <= '1';
        wait for 73 ns;

        s_reset <= '0';
        wait;
    end process p_reset_gen;

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;

        -- Enable counting
        s_en     <= '1';
        
        -- Change counter direction
        s_cnt_up <= '1';
        wait for 380 ns;
        s_cnt_up <= '0';
        wait for 220 ns;

        -- Disable counting
        s_en     <= '0';

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
 ```
 
 ### Thrid point: Top modul

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity top is
    Port ( 
           CLK100MHZ    : in STD_LOGIC;
           BTNC         : in STD_LOGIC;
           SW           : in STD_LOGIC_VECTOR (1-1 downto 0);
           LED          : in STD_LOGIC_VECTOR (4-1 downto 0);
           CA           : out STD_LOGIC;
           CB           : out STD_LOGIC;
           CC           : out STD_LOGIC;
           CD           : out STD_LOGIC;
           CE           : out STD_LOGIC;
           CF           : out STD_LOGIC;
           CG           : out STD_LOGIC;
           AN           : out STD_LOGIC_VECTOR (8-1 downto 0));
end top;

------------------------------------------------------------------------
-- Architecture body for top level
------------------------------------------------------------------------
architecture Behavioral of top is

    -- Internal clock enable
    signal s_en  : std_logic;
    -- Internal counter
    signal s_cnt : std_logic_vector(4 - 1 downto 0);

begin

    --------------------------------------------------------------------
    -- Instance (copy) of clock_enable entity
    clk_en0 : entity work.clock_enable
        generic map(
            g_MAX => 100000000
        )
        port map(
            clk   => CLK100MHZ,
            reset => BTNC,
            ce_o  =>  s_en
        );

    --------------------------------------------------------------------
    -- Instance (copy) of cnt_up_down entity
    bin_cnt0 : entity work.cnt_up_down
        generic map(
           g_CNT_WIDTH => 4
        )
        port map(
            clk     =>  CLK100MHZ,
            reset   =>  BTNC,
            en_i    =>  s_en,
            cnt_up_i=>  SW(0),
            cnt_o   =>  s_cnt
        );          

    -- Display input value on LEDs
    LED(3 downto 0) <= s_cnt;

    --------------------------------------------------------------------
    -- Instance (copy) of hex_7seg entity
    hex2seg : entity work.hex_7seg
        port map(
            hex_i    => s_cnt,
            seg_o(6) => CA,
            seg_o(5) => CB,
            seg_o(4) => CC,
            seg_o(3) => CD,
            seg_o(2) => CE,
            seg_o(1) => CF,
            seg_o(0) => CG
        );

    -- Connect one common anode to 3.3V
    AN <= b"1111_1110";

end architecture Behavioral;
 ```

