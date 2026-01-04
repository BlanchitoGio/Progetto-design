Lanciare lo script
cd "g:\Il mio Drive\MAGISTALE\SECONDO ANNO - PRIMO SEMESTRE\DESIGN\progetto\Progetto-design" ; python script




##---Buckling evaluation---
    print(f"Sy: {Sy:.2f} MPa")
    #Bucling of the vessel
    Dt_c=math.sqrt(Eyoung*10**3/((1-NUpoisson**2)*Sy)) #Critical slenderness ratio
    #print(f"D/t: {Dt_c:.2f}")
    Dt = (r_Vout*2)/t
    print(f"D/t: {Dt:.2f}")
    if Dt < Dt_c:
        print("Plastic collapse buckling")
    else: 
        print("Elastic collapse buckling")
    #Critical pressures for the buckling in a thin tubes (Rext/t>7,5)
    pe=2*(Eyoung*10**3/(1-NUpoisson**2))/Dt**3 #Buckling elsatic collapse pressure
    p0=2*Sy/Dt #Plastic collapse pressure
    print(f"pe: {pe:.2f} MPa")
    print(f"p0: {p0:.2f} MPa")
    print(f"p0/pe: {p0/pe:.2f} MPa")
    W = 0.01 #Ovalization factor
    Z = math.sqrt(3)*(2*Dt+1)*W/4 #Imperfection factor
    print(f"Z: {Z:.2f}")
    Pu= p0/math.sqrt(1+Z**2)  #Lower bound collapse pressure
    Pl= (p0+pe*(1+Z)-math.sqrt((p0+pe*(1+Z))**2-(4*pe*p0)))/2  #Lower bound collapse pressure
    #if p0/pe<
    #Pallow=Pl/1.5 #Allowable buckling pressure with safety factor 1.5
    muz= 0.35*log10(pe/p0)-0.125 #Reduction factor for the buckling pressure
    Pallow=(muz*Pu+(1-muz)*Pl)/1.5 #Allowable buckling pressure with safety factor 1.5
    t=Bthickness(t, Sy, r_Vin, r_Vout, Eyoung, NUpoisson, muz)
    '