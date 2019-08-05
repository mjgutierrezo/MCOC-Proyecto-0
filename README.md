# MCOC-Proyecto-0
import scipy as sp
import matplotlib.pylab as plt
import numpy as np

ejemplo=0
resultados_reales=[]
resultados32=[]
resultados64=[]
while ejemplo<=4:
    x1= float(raw_input("inserte un número:"))
    #x1 es el primer npumero co que se trabajará
    x2 = float(raw_input("inserte segundo número:"))
    sol_real=x1+x2
    resultados_reales.append(sol_real)    
    print sol_real
    Binario_x1=[] #lista que contiene x1 representado en forma binaria
    Binario_x2=[]#lista que contiene x2 representado en forma binaria

    while x1>0 or x2>0:
        resto1 = int(x1%2)
        resto2 = int(x2%2)
        Binario_x1.append(resto1)
        Binario_x2.append(resto2)
        if x1==0:
            Binario_x1.pop()
        if x2==0:
            Binario_x2.pop()
        x1 = x1//2
        x2 = x2//2
                
    Binario_x1.reverse()
    Binario_x2.reverse()
    exponente1= len(Binario_x1)-1
    exponente2=len(Binario_x2)-1
    #ambos deben quedar con el mismo exponente
    if exponente1>exponente2:
        while exponente1> exponente2:
            Binario_x2.insert(0,0)
            exponente2+=1
            
    if exponente2>exponente1:
        while exponente2> exponente1:
            Binario_x1.insert(0,0)
            exponente1+=1
                                
    if exponente1==exponente2:
        print "suma de binarios"
                                    
#suma entre números
    suma=[0]
    x=len(Binario_x1)-1
    Nuevo_binario=[]
    while x>=0:
        suma.append(Binario_x1[x])
        suma.append(Binario_x2[x])
        if suma.count(1)==3:
            Nuevo_binario.append(1)
            suma=[1]
            x-=1
            continue
        if suma.count(1)==1:
            Nuevo_binario.append(1)
            suma=[0]
            x-=1
            continue
        if suma.count(1)==2:
            Nuevo_binario.append(0)
            if x==0:
                Nuevo_binario.append(1)
                suma=[1]
                x-=1
                continue
            if suma.count(1)==0:
                Nuevo_binario.append(0)
                suma=[0]
                x-=1
                continue
            
    Nuevo_binario.reverse()
    print Nuevo_binario
            
    Nuevo_binario.pop(0)
    exponencial=len(Nuevo_binario) + 127
    Binario_exponencial=[]
    while exponencial>0:
        resto = int(exponencial%2)
        Binario_exponencial.append(resto)
        exponencial = x1//2
        if exponencial==0:
            Binario_exponencial.append(1)
            Binario_exponencial.reverse()
                                                    
    for t in Nuevo_binario:
        Binario_exponencial.append(t)
    
    Valores=[]
    indice=len(Nuevo_binario)
    for i in Binario_exponencial:
        if indice > 0:
            Valores.append(i*2**indice)
            indice-=1
            Valores.append(1)
            
    bin32=Binario_exponencial
    bin64=Binario_exponencial
    numero64b=0
    numero32b=0
    #pasar a 64 bit
    if len(bin64)>63:
        Valores[:63]
        for n in Valores:
            numero64b+=n
            resultados64.append(numero64b)
            #pasar a 32 bit 
    if len(bin32)>31:
        Valores[:31]
        for j in Valores:
            numero32b+=j
            resultados32.apprend(numero32b)                
    #calcular margen de error 
    error32b= (sol_real-numero32b)/sol_real
    error64b= (sol_real-numero64b)/sol_real
                            
    print numero32b
    print "margen de error:", error32b*100, "%"
    print numero64b
    print "margen de error:", error64b*100, "%"
    
    ejemplo+=1 
    
pyplot.plot(resultados_reales, resultados32, "rs")
pyplot.plot(resultados_reales, resultados64,"s")   
pyplot.show() 
