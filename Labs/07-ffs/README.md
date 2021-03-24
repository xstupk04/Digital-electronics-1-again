# Digital electronics 1
## First point: preparation tasks (done before the lab at home)

Write characteristic equations and complete truth tables for D, JK, T flip-flops where `Qn` represents main output value before clock edge and `Q(n+1)` represents value after the edge.

   | **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | Q | /Q |
   | 0 | 1 | Q | /Q |
   | 1 | 0 | 0 | 1 |
   | 1 | 1 | 1 | 0 |

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

```  

![Time2](https://user-images.githubusercontent.com/60606149/110390174-dfd0fe00-8065-11eb-888b-35829a19f53b.png)
