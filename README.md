# Case-studies
Details the codes used to solve problems in case studies
from gurobipy import *
import numpy as np

#Sewa Case study: Profit maximisation
#Linear programming solution
#Max: 26000X1+37000X2+15000X3
#             st
#       X1+X2+X3<=25      Farmsize contraint

Prof = [26000, 37000,15000]
#create model
Sewa= Model('profit')
#add variable
x= np.array([None for j in range(3)])
for k in range(3):
    x[k]= Sewa.addVar(name = 'x%d' %k)
Sewa.update()
#set objective
Sewa.setObjective(np.dot(Prof,x), GRB.MAXIMIZE)

#add constraints
Sewa.addConstr(x[0]+x[1]+x[2]<=25)
Sewa.update()

print('Sewa.status:', Sewa.status)
Sewa.write('Sewa.lp')
Sewa.optimize()

for i in Sewa.getVars():
    print('%s %g' % (i.varName, i.x))
print('Obj: %g' % Sewa.ObjVal)
