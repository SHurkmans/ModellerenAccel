helling=slider(10,0,30)
alpha=(helling/180)*3.14159265359
hoogte=slider(3.0,0.1,8.0)
offset=input(0.4)

cabine=input(6)
trailer1=input(12)
trailer2=input(12)

cabineDomein=vSeq(0,cabine*10)
trailer1Domein=vSeq(0,trailer1*10)
trailer2Domein=vSeq(0,trailer2*10)

cabineDomeinMeter=cabineDomein/10
trailer1DomeinMeter=trailer1Domein/10
trailer2DomeinMeter=trailer2Domein/10

CabineHoogte=#(L,cabineDomeinMeter, cos(alpha - (asin(cabineDomeinMeter/cabine * sin(3.14159265359 - alpha)))) * (hoogte - (tan(alpha - (asin(cabineDomeinMeter/cabine * sin(3.14159265359 - alpha)))) * (cabineDomeinMeter + offset)))   ,vAppend)
Trailer1Hoogte=#(L,trailer1DomeinMeter, cos(alpha - (asin(trailer1DomeinMeter/trailer1 * sin(3.14159265359 - alpha)))) * (hoogte - (tan(alpha - (asin(trailer1DomeinMeter/trailer1 * sin(3.14159265359 - alpha)))) * (trailer1DomeinMeter + offset)))   ,vAppend)
Trailer2Hoogte=#(L,trailer2DomeinMeter, cos(alpha - (asin(trailer2DomeinMeter/trailer2 * sin(3.14159265359 - alpha)))) * (hoogte - (tan(alpha - (asin(trailer2DomeinMeter/trailer2 * sin(3.14159265359 - alpha)))) * (trailer2DomeinMeter + offset)))   ,vAppend)

Q1=#(i,CabineHoogte,i,min)
Q2=#(i,Trailer1Hoogte,i,min)
Q3=#(i,Trailer2Hoogte,i,min)

minCabineHoogte=#(i,Q1,i,min)
minTrailer1Hoogte=#(i,Q2,i,min)
minTrailer2Hoogte=#(i,Q3,i,min)

Vrachtwagens=[minCabineHoogte,minTrailer1Hoogte,minTrailer2Hoogte]
minVrachtwagen=#(i,Vrachtwagens,i,min)

Marge=if(hoogte>=3,0.5,0.2)
MaxDoorrijhoogte1=(minVrachtwagen-Marge)*10
MaxDoorrijhoogte2=round(MaxDoorrijhoogte1)
MaxDoorrijhoogte=MaxDoorrijhoogte2/10



midden=50

x=midden-0.5*lengte
lengte=slider(50,0,100)
y=5

helling1=helling
helling2=helling
x2=hoogte/tan(alpha)
x3=hoogte/tan(alpha)

 //de waarde die op het bord komt te staan.
plotWeg=[locations:[icon:"none", data:[[x:x,y:y],[x:x+lengte,y:y]]],edges:[col_r:50, col_g:50, col_b:50, thickness:1, b:0, e:1]]
plotBrug=[locations:[icon:"none", data:[[x:x-offset,y:y+hoogte*3],[x:x+lengte+offset,y:y+hoogte*3]]],edges:[col_r:0, col_g:0, col_b:0, thickness:1, b:0, e:1]]
plotHelling1=[locations:[icon:"none", data:[[x:x+lengte,y:y],[x:x+lengte+x3,y:y+hoogte*2]]],edges:[col_r:100, col_g:100, col_b:100, thickness:1, b:0, e:1]]
plotHelling2=[locations:[icon:"none", data:[[x:x,y:y],[x:x-x2,y:y+hoogte*2]]],edges:[col_r:100, col_g:100, col_b:100, thickness:1, b:0, e:1]]

 //de data voor het tekenen van het bord.


uitkomstcheck=MaxDoorrijhoogte

voordeKomma=floor(MaxDoorrijhoogte)
 //eerste cijfer voor op het bord
decimaal=MaxDoorrijhoogte-voordeKomma
 //berekening van de rest
achterdeKomma=round(10*decimaal)
 //omrekening rest naar geheel getal
vertaling=[0:"0",1:"1",2:"2",3:"3",4:"4",5:"5",6:"6",7:"7",8:"8",9:"9"]
 //vector voor vertaling van cijfers in strings
z=vertaling[voordeKomma]
w=vertaling[achterdeKomma]
 //de data voor het tekenen van de brug, weg en helligen.

 //de paal.
plotStick=[locations:[icon:"none", data:[[x:70,y:70],[x:70,y:30]]],edges:[col_r:0, col_g:0, col_b:0, thickness:2, b:0, e:1]]

 //het bord.
plotWhite=[locations:[rad:9, x:70, y:70, thickness:18, col_r:255, col_g:255, col_b:255]]
plotRed=[locations:[rad:18, x:70, y:70, thickness:4, col_r:255, col_g:0, col_b:0]]
plotNum1=[locations:[rad:0, x:65, y:65, thickness:0, col_r:255, col_g:255, col_b:255, tag:z, pointSize:10]]
plotPunt=[locations:[rad:0, x:70, y:65, thickness:0, col_r:255, col_g:255, col_b:255, tag:'.']]
 //bedoeld om de komma in het getal weer te geven, werkt nog niet
plotDinges=[locations:[rad:0, x:81, y:65, thickness:0, col_r:255, col_g:255, col_b:255, tag:'m', pointSize:5]]
plotNum2=[locations:[rad:0, x:74, y:65, thickness:0, col_r:255, col_g:255, col_b:255, tag:w, pointSize:5]]

 //de driehoeken op het bord.
plotDriehoekonder=[locations:[rad:1, x:70, y:57, thickness:3, col_r:0, col_g:0, col_b:0]]
plotDriehoekonder2=[locations:[rad:0, x:70, y:57, thickness:1, col_r:0, col_g:0, col_b:0]]
plotDriehoekboven=[locations:[rad:1, x:70, y:82, thickness:3, col_r:0, col_g:0, col_b:0]]
plotDriehoekboven2=[locations:[rad:0, x:70, y:82, thickness:1, col_r:0, col_g:0, col_b:0]]

plotStreep1=[locations:[icon:"none", data:[[x:70,y:60],[x:66,y:55]]],edges:[col_r:255, col_g:255, col_b:255, thickness:2, b:0, e:1]]
plotStreep2=[locations:[icon:"none", data:[[x:66,y:55],[x:74,y:55]]],edges:[col_r:255, col_g:255, col_b:255, thickness:1.4, b:0, e:1]]
plotStreep3=[locations:[icon:"none", data:[[x:74,y:55],[x:70,y:60]]],edges:[col_r:255, col_g:255, col_b:255, thickness:2, b:0, e:1]]

plotStreep4=[locations:[icon:"none", data:[[x:70,y:79],[x:66,y:84]]],edges:[col_r:255, col_g:255, col_b:255, thickness:2, b:0, e:1]]
plotStreep5=[locations:[icon:"none", data:[[x:66,y:84],[x:74,y:84]]],edges:[col_r:255, col_g:255, col_b:255, thickness:1.4, b:0, e:1]]
plotStreep6=[locations:[icon:"none", data:[[x:74,y:84],[x:70,y:79]]],edges:[col_r:255, col_g:255, col_b:255, thickness:2, b:0, e:1]]

 // hier word ook echt alles op het scherm gezet
plotResult=descartes([plotWeg, plotBrug, plotHelling1, plotHelling2, plotStick, plotWhite, plotRed, plotNum1, plotNum2, plotPunt, plotDinges, plotDriehoekonder, plotDriehoekonder2, plotDriehoekboven, plotDriehoekboven2, plotStreep1, plotStreep2, plotStreep3, plotStreep4, plotStreep5, plotStreep6])

