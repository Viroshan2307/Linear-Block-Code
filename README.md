# Linear-Block-Code
# Aim
Write a simple python program to Generate Matrix, Codeword, Hamming weight, Syndrome matrix and find the error on received codeword using Linear block code. 
# Tools required
# Program
```
import itertools
import numpy as np

p=int(input("Enter the Parity bits : "))
m=int(input("Enter the Message bits : "))

rows=[]
for i in range(m):
    r=list(map(int,input(f"Enter the row values : {i+1} (Separated by space) : ").split()))
    rows.append(r)

n=m+p

# Generator Matrix
G=[]
for i in range(m):
    row=rows[i]+[0]*m
    row[p+i]=1
    G.append(row)

print("\nGenerator Matrix G\n")
for i in G:
    print(*i)

G=np.array(G)

print("\nMessage Bits  Codeword  Hamming Weight")

codewords=[]

for msg in itertools.product([0,1],repeat=m):

    msg=np.array(msg)
    c=np.mod(np.dot(msg,G),2)

    codewords.append(c)

    print(*msg," ",*c," ",sum(c))

# Minimum Hamming Distance
non_zero_weights=[w for w in weights if w!=0]
dmin=min(non_zero_weights)

print("\nMinimum Hamming Distance =",dmin)

# Parity Check Matrix
P=G[:,0:p]
H=np.concatenate((np.identity(p,dtype=int),P.T),axis=1)

print("\nParity Check Matrix H\n")

for i in H:
    print(*i)

# Syndrome Table
print("\nError Pattern   Syndrome")

for i in range(n):
    e=[0]*n
    e[i]=1

    s=np.mod(np.dot(H,np.array(e).T),2)

    print(*e,"   ",*s)

# Error Detection
r=np.array(list(map(int,input("\nEnter Received Codeword : ").split())))

s=np.mod(np.dot(H,r.T),2)

print("Syndrome :",*s)

if np.all(s==0):
    print("No Error")
    print("Correct Codeword :",*r)

else:
    print("Error Detected")

    error_pos=-1

    for i in range(n): 
        if np.array_equal(H[:,i],s):
            error_pos=i
            break

    if error_pos!=-1:
        print("Error Position :",error_pos+1)

        r[error_pos]=(r[error_pos]+1)%2

        print("Correct Codeword :",*r)
```
# Output 
<img width="394" height="630" alt="image" src="https://github.com/user-attachments/assets/20369d58-9bb6-4cac-91ff-77456c67ba84" />

# Results
Thus linear block code operation for the given input is successfully verified.`
