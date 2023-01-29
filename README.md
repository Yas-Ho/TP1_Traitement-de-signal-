# Traitement-de-signal

TRAITEMENT-DU-SIGNAL-TP-1



# Objectifs
Représentation de signaux et applications de la transformée de Fourier discrète (TFD) sous Matlab. • Evaluation de l’intérêt du passage du domaine temporel au domaine fréquentiel dans l’analyse et l’interprétation des signaux physiques réels.

L’objectif du ce TP est de voir ensemble comment se servir des outils de traitement du signal pour analyser les signaux échantillonnés. Pour cela, nous allons utiliser le logiciel MATLAB pour la simulation

Tracé des figures : toutes les figures devront être tracées avec les axes et les légendes des axes appropriés.

Travail demandé : un script Matlab commenté contenant le travail réalisé et des commentaires sur ce que vous avez compris et pas compris, ou sur ce qui vous a semblé intéressant ou pas, bref tout commentaire pertinent sur le TP.

# Représentation-temporelle-et-fréquentielle
Considérons un signal périodique x(t) constitué d’une somme de deux sinusoïdes de fréquences 15Hz et 20Hz. 𝐱(𝐭) = 𝐬𝐢𝐧(𝟐𝝅𝟏𝟓𝒕) + 𝐬𝐢𝐧(𝟐𝝅𝟐𝟎𝒕)

1- Tracer le signal x(t). Pas de temps : Te = 1/50s, Intervalle : 0, 10-Te. Pour approximer la TF continue d’un signal x(t), représenté suivant un pas Te, on utilise les deux commandes : fft et fftshif.

Te=1/50;
x=[0:Te:10-Te];
y = sin(30*pi*x) + sin(40*pi*x);
subplot(3,2,1);
plot(x,y);
title('signal x(t) :'); 
![image](https://user-images.githubusercontent.com/97410524/215338332-ecb8f8c1-cdc6-49cf-9ece-b5ddf96cae3a.png)

On remarquera que la TF est une fonction complexe et que la fonction ainsi obtenue décrit la TF de x(t) entre –1/(2Te) et 1/(2Te) par pas de 1/(nTe) où n est le nombre de points constituant le signal x(t).

f=(0:length(x)-1)*(1/Te*length(x)); 
fy=abs(fft(y));
subplot(3,2,2); 
plot(f,fy);
title('spectre du  x(t) :'); 
![image](https://user-images.githubusercontent.com/97410524/215346690-b30c6a3e-1644-48ce-b7b7-826838f72289.png)

Une fois notre signal généré, calculons maintenant sa Transformée de Fourier.

fsh=[-500/2:(500/2)-1]*50/500;
fy=abs(fft(y));
subplot(3,2,3);
plot(fsh,fftshift(fy));
title('spectre du  x(t) :');
![image](https://user-images.githubusercontent.com/97410524/215346700-ade7fb9c-baab-4eb2-a2cb-99acc425f02f.png)

Pour se rapprocher de la réalité nous allons simuler la présence d’un bruit de mesure. Pour observer le même signal que x(t), nous allons générer un bruit aléatoire Gaussien.

noise = 2*randn(size(x));
Afin de créer un signal bruité, ajoutons noise à x(t)

xnoise = x+noise; 
plot(t,xnoise,'.')
grid
title('signal x bruité');
xlabel('Temps');
ylabel('Amplitudesà');
![image](https://user-images.githubusercontent.com/97410524/215346710-1178c7cf-219d-41f3-a806-aa07207352e3.png)

Calculons à nouveau la Transformée de Fourier du signal bruité Sb(t)

![image](https://user-images.githubusercontent.com/97410524/215346715-fe29931c-cb91-406e-8ff2-304338d434ff.png)

![image](https://user-images.githubusercontent.com/97410524/215346718-2b649144-2c40-44a1-adda-1f81a0695e7f.png)

Conception du filtre pass bas idéal FILTRAGE IDEAL

![image](https://user-images.githubusercontent.com/97410524/215346729-5beab3eb-7cef-4f29-8c71-97a03506dc04.png)

On l’applique sur le spectre de x(t)

![image](https://user-images.githubusercontent.com/97410524/215346738-6564ae04-10c9-4497-a53d-ac98dbc529ca.png)

![image](https://user-images.githubusercontent.com/97410524/215346743-163c8934-0805-46ef-9c8f-97641a7a2144.png)

