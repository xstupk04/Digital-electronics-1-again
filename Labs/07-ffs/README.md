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
### Listing of VHDL reset and stimulus processes from the testbench tb_d_latch.vhd
### Screenshot with simulated time waveforms; always display all inputs and outputs.



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
