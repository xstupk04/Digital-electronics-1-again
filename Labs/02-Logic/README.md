# Digital-electronics-1
  ## Second Labs 


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

**Second point: 2-bit comparator**

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

[EDA Playground](https://www.edaplayground.com/x/PyYQ)

**Third point: 2-bit comparator**


