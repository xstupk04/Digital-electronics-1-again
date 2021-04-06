# Digital electronics 1
## First point: preparation tasks (done before the lab at home)

| **Input P** | `0` | `0` | `1` | `1` | `0` | `1` | `0` | `1` | `1` | `1` | `1` | `0` | `0` | `1` | `1` | `1` |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **Clock** | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) | ![rising](https://user-images.githubusercontent.com/60606149/113711732-95cf4c80-96e5-11eb-9236-76dc203bd66f.png) |
| **State** | A | A | B | C | C | D | A | B | C | D | B | B | B | C | D | B |
| **Output R** | `0` | `0` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `0` | `1` | `0` |

### Connection of two RGB LEDs.

![image](https://user-images.githubusercontent.com/60606149/113676690-0d3cb600-96bd-11eb-8cd6-bad7fb485e68.png)


| **RGB LED** | **Artix-7 pin names** | **Red** | **Yellow** | **Green** |
| :-: | :-: | :-: | :-: | :-: |
| LD16 | N15, M16, R12 | `1,0,0` | `1,1,0` | `0,1,0` |
| LD17 | N16,R11,G14 | `1,0,0` | `1,1,0` | `0,1,0` |

## Second point: Traffic light controller

![image](https://user-images.githubusercontent.com/60606149/113711176-eabe9300-96e4-11eb-9e92-7a981f5e18f7.png)

## Listing of VHDL code of sequential process p_traffic_fsm
```vhdl 
 p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then       -- Synchronous reset
                s_state <= STOP1 ;      -- Set initial state
                s_cnt   <= c_ZERO;      -- Clear all bits

            elsif (s_en = '1') then
                -- Every 250 ms, CASE checks the value of the s_state 
                -- variable and changes to the next state according 
                -- to the delay value.
                case s_state is

                    -- If the current state is STOP1, then wait 1 sec
                    -- and move to the next GO_WAIT state.
                    when STOP1 =>
                        -- Count up to c_DELAY_1SEC
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= WEST_GO;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;

                     when WEST_GO =>
                        -- Count up to c_DELAY_4SEC
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= WEST_WAIT;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;
                        
                    when WEST_WAIT =>
                        -- Count up to c_DELAY_2SEC
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= STOP2;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;
                        
                    when STOP2 =>
                        -- Count up to c_DELAY_1SEC
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= SOUTH_GO;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;
                        
                    when SOUTH_GO =>
                        -- Count up to c_DELAY_4SEC
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= SOUTH_WAIT;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;  
                          
                    when SOUTH_WAIT =>
                        -- Count up to c_DELAY_2SEC
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= STOP1;
                            -- Reset local counter value
                            s_cnt   <= c_ZERO;
                        end if;      

                    -- It is a good programming practice to use the 
                    -- OTHERS clause, even if all CASE choices have 
                    -- been made. 
                    when others =>
                        s_state <= STOP1;

                end case;
            end if; -- Synchronous reset
        end if; -- Rising edge
    end process p_traffic_fsm;
```

## Listing of VHDL code of combinatorial process p_output_fsm
```vhdl 

```

