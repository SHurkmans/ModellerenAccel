clc                                                 % scherm leeg
clear all                                           % verwijdering variabelen
clf                                                 % figuur scherm leeg 
hold on                                             % zorgt voor vasthouden grafieken
standaard = questdlg('Welke afmetingen wilt u gebruiken?', ...
	'Afmetingen', ...
	'Een trekker met oplegger','Een vrachtwagen met oplegger',...
    'Custom afmetingen','Custom afmetingen');
switch standaard                                    % voert gewenste afmetingen in
    case 'Een trekker met oplegger'
        disp(standaard)
        stukken2=2;
        lengte=[4.42 9.40];                         % standaard afmeting
    case 'Een vrachtwagen met oplegger'
        disp(standaard)
        stukken2=2;
        lengte=[6.45 6.10];                         % standaard afmeting
    case 'Custom afmetingen'
        disp(standaard)        
        stukken = input('Aantal delen = ');
        stukken2=stukken;
        i=0;

        if stukken>1
            while stukken~=1                            
                i=i+1;                              % zorgt voor nummer in str
                str=['Wielbasis oplegger ',num2str(i),'  = '];  
                lengte(stukken) = input(str);
                stukken = stukken - 1;
            end
        end
        lengte(1) = input('Wielbasis trekker = ');

end

alpha = input ('Helling = ');                       % input alle variabelen
alpha = alpha/180*pi;
y = input ('Hoogte brug = ');
x2 = input('Inkorting brug = ');                    % einde input alle variabelen


while stukken2~=0                                               
syms x gamma hoogte beta                            % begin berekening hoogte
x1=0:0.02:lengte(stukken2);
gamma = asin(x1./lengte(stukken2) .* sin(pi-alpha));
beta = alpha - gamma;
y1 = tan(beta) .* (x1-x2);
y2= y - y1;
hoogte = cos(beta) .* y2;
hmin(stukken2)=min(hoogte);                         % einde berekening hoogte
if hmin(stukken2)>3.90                              % meenemen veiligheidsmarges
    hoogte = hoogte - 0.50;
    hmin(stukken2) = hmin(stukken2)-0.50;
else
    hoogte = hoogte - 0.20;
    hmin(stukken2) = hmin(stukken2)-0.20;
end                                                 
plot (x1,hoogte)                                    % plot grafiek
stukken2 = stukken2 - 1;
end
hmin=min(hmin);                                     % bepaald laagste doorrijhoogte
disp('De minimale doorrijhoogte is: ')
minmeter=[num2str(hmin),' meter'];
disp(minmeter)                                      % toont minimale doorrijhoogte

xlabel('afstand in brug')                           % labels grafiek
ylabel('doorrijhoogte')
hold off                                            % settings terug zetten
