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

