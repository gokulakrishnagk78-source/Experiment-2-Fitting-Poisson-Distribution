# Experiment-2-Fitting-Poisson-Distribution
NAME : GOKULAKRISHNA S 
REG NO : 25018150
SLOT NO : 3P1-1
Aim: 
To fit Poisson distribution for the arrival of objects per minute from the feeder. 
# Software required: 

Python and Visual Component Tool
# Theory: 

1. The Poisson distribution gives the probability of a number of events occurring in a fixed interval of time or space when events occur independently and at a constant average rate (λ).
2. The probability mass function (PMF) is:  
<img width="1171" height="73" alt="image" src="https://github.com/user-attachments/assets/e28da9e9-3b3f-4969-baa9-2ff06c3358ba" />
3. Here, λ = mean number of occurrences, and e = 2.718 (base of natural logarithm).
4. The mean and variance of a Poisson distribution are both equal to λ.
5. Applicable when events occur independently, singly, and at a constant rate.
# Algorithm
<img width="1144" height="412" alt="image" src="https://github.com/user-attachments/assets/6bf357bd-7ba2-4908-8c93-ef74e4747a4f" />

# Program
import numpy as np
import math
import scipy.stats

# Input: Enter the data separated by space
L = [int(i) for i in input("Enter data: ").split()]

N = len(L)
M = max(L)

X = []
f = []

# Compute frequency of each value
for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c += 1
    f.append(c)
    X.append(i)

sf = np.sum(f)

# Probability for each X
p = []
for i in range(M + 1):
    p.append(f[i] / sf)

# Mean of distribution
mean = np.inner(X, p)

p = []
E = []
xi = []

print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")
print("------------------------------------")

# Calculate expected frequency using Poisson & chi-square components
for x in range(M + 1):
    # Poisson probability
    p.append(math.exp(-mean) * mean**x / math.factorial(x))

  # Expected frequency
  E.append(p[x] * sf)

  # Chi-square term
  xi.append(((f[x] - E[x])**2) / E[x])

  print("%2d   %.3f   %4d   %.2f   %.3f" % (x, p[x], f[x], E[x], xi[x]))

print("------------------------------------")

# Total Chi-square
cal_chi2_sq = np.sum(xi)
print("Calculated value of Chi square is %.4f" % cal_chi2_sq)

# Table value at 1% level
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print(f"Table value of Chi square at 1% level is {table_chi2:.4f}")

# Decision
if cal_chi2_sq < table_chi2:
    print("The given data can be fitted in Poisson Distribution at 1% LOS")
else:
    print("The given data cannot be fitted in Poisson Distribution at 1% LOS")


https://colab.research.google.com/drive/1ZR3zKFK63DgMqrhINh2acs90xb-K9jFO?usp=sharing



# Output

![Screenshot_17-11-2025_141856_colab research google com](https://github.com/user-attachments/assets/da36070f-bd19-48b5-b75b-3742270efda3)


#Result
The Poisson Distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 

