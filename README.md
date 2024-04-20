# Sistemas-de-control-II
%Asignacion de variables y tiempos de integracion 
%x1 es como varia la corriente en el tiempo
%x2 es como varia la tension en el capacitor en el tiempo
%x = A* x(t) + B* x(t)
%y = Ct * x(t)
L=1e-6; R= 47; Cap=100e-9; %Asigno valores  a L,R y C
A=[-R/L, -1/L; 1/Cap , 0]; B=[1/L; 0]; Ct= [R, 0]; D=0; %Defino matrices con variables de estados
x = [0;0]; xop=[0;0]; y(1)=0; %Condiciones iniciales nulas
system= ss(A,B,Ct,D); %Creo el modelo de estados a partir de las matrices de estado
FdT=tf(system); % Formo la funcion de transferencia del sistema.
polos_FdT=pole(FdT); %Busco polos para encontrar la dinamica mas rapida y mas lenta de mi FdT, asi puedo elegir mi tiempo de integracion y el tiempo de simulacion
polo1= polos_FdT(1) ;%Dinamica mas rapida
polo2= polos_FdT(2); %Dinamica mas lenta
tr= log(0.95)/polo1;
Ti= abs(tr/10); % Divido por 10 para tener un tiempo de integracion de Euler adecuado;
