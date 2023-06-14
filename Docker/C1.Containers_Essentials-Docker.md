
## Aspecte de bază


Virtualizarea a apărut ca o soluție pentru a putea crea un mediu izolat pe o mașina fizică prin intermediul unei mașini virtuale. Pentru aplicațiile care rulează pe mașina virtuală, poate părea ca și cum ar fi pe propria lor mașină dedicată (fizică), cu propriul sistem de operare și programe . De exemplu, cu ajutorul unui program de virtualizare (ex. VirtualBox) pe care îl instalăm local, se poate descărca o imagine de Linux și instala astfel încât să avem un server virtual de Linux unde putem testa diferite configurații. Unul dintre avantaje este acela că poți recrea serverul de Linux în doar câteva minute fără a afecta cu nimic serverul gazdă, ele fiind două medii separate. Calculatorul tău va pune la dispoziție doar resursele sale (memorie RAM și putere de procesare). Totuși, în cazul utilizării unei mașini virtuale pentru o aplicație relativ mică, sunt multe resurse folosite pentru a o putea rula (un întreg sistem de operare doar pentru a putea ține acea aplicație activă). 

Ca rezultat al acestei nevoi au apărut containerele. Acestea sunt soluții de virtualizare definite la nivel de sistem de operare prin intermediul cărora se pot obține mai multe medii izolate pe același hardware. Spre deosebire de mașinile virtuale, acestea folosesc același kernel și hardware ca mașina gazdă. Ce este de reținut este că o mașină virtuală va ține "captive" resursele calculatorului gazdă chiar dacă mașina virtuală nu face prea multe lucruri în acel moment. Acest lucru va face calculatorul gazdă să meargă foarte greu ( în funcție și de câte resurse îi dăm ) . În cazul containerelor , acestea rulează mai mult sau mai puțin ca niște simple procese și consumă resurse doar la nevoie ( ca și cum am avea un browser web pornit fără niciun tab deschis și care consumă mai puține resurse ca unul ce rulează 20 de pagini simultan ).

Containerele oferă o soluție de izolare securizată prin utilizarea componentelor din kernel-ul de Linux: chroot, namespaces, AppArmor, SELinux etc. Aplicațiile ce rulează în interiorul acestora pot fi pornite foarte rapid deoarece nu exista niciun sistem de operare care trebuie să booteze înainte ( putem spune că aceste containerele ruleză ca orice alt proces de la laptopul personal ). Resursele sunt alocate și gestionate de kernel-ul mașinii gazdă și pot fi alocate conform unor reguli de QoS (Quality of Service). Totuși, chiar și containerele au un dezavantaj în comparație cu un hypervisor: *nu oferă o izolare completă*. Docker este scris în limbajul de programare Go (golang) și este în continuare cel mai popular tool ce folosește virtualizarea la nivel de sistem de operare pentru a crea containere.

![](https://cursuri.telacad.ro/assets/courseware/v1/c2e400ba0e4bc85917bf3af748bd2f55/asset-v1:telecomacademy+ContainersEssentialsDocker+2022_T1+type@asset+block/containers-vs-virtual-machines.jpg)

## Instalare Docker

1)  Pentru a face update la baza de date de repositories, odată updatată, Linux va ști de unde să descarce pachetele necesare cu versiunile cele mai recente.

De obicei, pe măsură ce pentru Docker apar alte versiuni mai noi, modul de instalare și configurare poate fi diferit. De aceea vă recomand să urmăriți și documentația de Docker din linkul următor, unde se prezintă pașii de instalare: https://docs.docker.com/engine/install/ubuntu/

În continuare, vă voi prezenta pașii de instalare din acest moment pe care îi puteți găsii și pe documentația oficială.

Comanda folosită: **sudo apt-get update**

2) Acum vom instala o serie de 4 pachete ce ne vor ajuta în procesul de instalare de Docker folosind comenzile:

   sudo apt-get install \

    ca-certificates \

    curl \

    gnupg \

    lsb-release

3) Vom adăuga GPG key-ul de la Docker. Prin această comandă se verifică autenticitatea software-ului înainte de a fi instalat.

Vom crea un director nou în locație folosind comanda:  /etc/apt/keyrings

Pentru că userul pe care îl folosim în mod normal nu are drepturi de a crea un folder în acea locație, va fi nevoie să rulăm comanda cu dreputuri de sudo: **sudo mkdir -p /etc/apt/keyrings**

Vom descărca și pune cheia în folderul nou creat: curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

4) Momentan Dockerul nu este instalat. Am descărcat cheia ce ne va confirma faptul că software-ul este autentic și am instalat câteva dependințe. Acum vom adăuga o nouă sursă în lista noastră de repo-uri și anume vom crea fișierul docker.lis

  echo \

  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \

  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

5) Chiar dacă am adăugat docker.list, avem nevoie de următoarea comandă pentru ca Linux să își updateze baza de date ce acum va conține și docker.list: **sudo apt-get update**

6) Abia acum vom instala componente de docker: **sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin**

7) Pentru a verifica faptul că Docker a fost instalat și a verificat versiunea putem rula: **docker --version**

În mod normal userul utilizat fără drepturi de sudo nu ar putea rula comenzi de Docker momentan. 

Dacă vom dori să rulăm o comandă de Docker: ex docker container ls nu vom avea permisiunea momentan. De accea va fi nevoie să rulăm inițial: sudo docker container ls

Pentru a adăuga userul pe grupul Docker vom folosi comanda: sudo usermod -aG docker $USER

Acum userul face parte din grupul Docker și implicit poate rula comenzi de Docker. Totuși, este necesar să dăm un "refresh" la shell-ul curent pentru a fi actualizate setările de acces. Aici avem 2 variante:

a) Închidem și deschidem terminalul și apoi vom putea rula : docker container ls

b) Sau ne vom deloga și loga din nou pe userul curent cu comenzile următoare:

- pentru a ne face root folosim: **sudo su**

- pentru a schimba din nou în userul anterior folosim: **su USERUL_TAU**

Putem verifica faptul că userul este acum în grupul Docker rulând: groups

Acum va funcționa și comanda: docker container ls


## Docker Engine


Docker folosește tehnica numită workspaces pentru a izola containerele. Când rulezi un container de docker, Docker creează un set de workspace-uri pentru acel container. Aceste spații de nume oferă un strat de izolare.

Docker Engine este o tehnologie de containerizare open source pentru construirea și containerizarea aplicațiilor. Docker Engine este o aplicație de tip client server formată din:

- un server care rulează ca proces daemon – acesta se numește dockerd

- un API de tip REST care oferă posibilitatea programelor de a accesa și controla daemon-ul

- o interfață CLI prin comanda docker care folosește API-ul de REST pentru a putea asigura interacțiunea cu procesul daemon pentru a putea crea obiecte de tip Docker cum ar fi: imagini, containere, rețele, volume despre care vom vorbi in paginile următoare.

![](https://cursuri.telacad.ro/assets/courseware/v1/3185f40a56d6a22b714b444d515be3f0/asset-v1:telecomacademy+ContainersEssentialsDocker+2022_T1+type@asset+block/engine-components-flow.png)


## Docker client, docker registry si obiecte docker

**Docker client**

Utilizatorii Docker pot interacționa cu Docker printr-un client. Când rulează orice comenzi docker, clientul le trimite către demonul dockerd, care le execută. Docker API este folosit de comenzile Docker. 

**Registrii docker**

Este locația în care sunt stocate imaginile Docker. Poate fi un registru docker public sau un registru docker privat. Docker Hub este locul implicit al imaginilor docker unde oricine își poate crea o imagine de docker și o să pună public. De asemenea, tot acolo puteți crea și rula propriul registru privat. Este asemănător cu GitHub, dar echivalentul pentru Docker .

**Obiecte docker**

Când lucrați cu Docker, utilizați imagini, containere, volume, rețele. Toate acestea sunt obiecte Docker și vor fi prezentate pe rând în secțiunile următoare.

Comenzi:

docker run -d -p 8000:80 --name="simple_http" \



## Ce sunt imaginile Docker ?

O imagine Docker este un șablon care conține un set de instrucțiuni pentru crearea unui container care poate rula pe platforma Docker. Imaginile descriu aplicațiile și cum pot fi rulate și un container de docker rulează pe baza acelei  imagini. Practic containerele sunt instanțele acelei imagini, în care pot fi rulate mai multe containere ( se pot rula mai multe containere pe baza aceleiași imagini, fiecare cu configurații diferite) .

 Cum precizam și în capitolul anterior, containerele sunt ca ca “niște procese”, dar aceste procese au propriul sistem de fișiere care este dat de imagine. Ca sa vedeți diferență între un docker și un container puteți sa va gândiți că o imagine este un CD cu windows și containerul este calculatorul după ce am instalat pe el sistemul de operare de pe acel CD . Putem avea mai multe dispozitive care rulează acel sistem de operare instalat din acea sursă și initial acestea vor avea aceeași stare, dar pe parcurs ce fiecare utlizator îl folosește, va avea fișiere diferite. 

![docker image-docker container](https://cursuri.telacad.ro/assets/courseware/v1/db2748efe84c9f4b9d041ed0d1f6de32/asset-v1:telecomacademy+ContainersEssentialsDocker+2022_T1+type@asset+block/dockerimage.png)


## Structura imaginii

**1. Cum descarcă****m o imagine de docker?**

Majoritatea imaginilor de docker se descarca de pe un repository, care nu este altceva decât un locație de stocare a fișierelor. Acest repository poate fi public și toată lumea are acces la el sau privat în care accesul este limitat unui grup de persoane. Daca ați folosit GitHub este același lucru doar că este pentru docker. Docker Hub este un serviciu oferit de Docker pentru găsirea și partajarea imaginilor containerelor cu echipa dvs. Pentru a descarca o imagine se folosește comanda:

##### docker pull nume_imagine:tag

Ex: Dacă dorim să descărcăm imaginea httpd folosim comanda: **docker pull httpd:latest**

În caz de nu precizam tag-ul, se va lua by default valoarea “latest” ceea ce înseamnă ultima versiune disponibilă. Imaginea de mai sus poate fi descărcată și de pe repository-ul oficial de docker, numit dockerhub .

[https://hub.docker.com/_/httpd](https://hub.docker.com/_/httpd)


**2. Cum verificăm faptul că imaginea s-a descarcat ?**

Docker images -> cu aceasta comandă putem verifica ce imagini avem descărcate local

De exemplu putem avea o imagine de docker de tip **apache2**. Dacă decidem să pornim un container pe baza acestei imagini, containerul va rula serviciul apache2 ce conține o pagină http de tip “hello world” ca în imaginea 1.1 .

Astfel încât dacă accesăm ip-ul containerului și portul corespunzător, ni se va răspunde cu mesajul “hello world”.  Legat de ip-ul containerului tot ce trebuie să rețineți în acest moment este că un container poate avea o adresă IP asignată.

Putem ulterior sa rulăm un alt container, pe baza aceleiași imagini, dar în acest caz vom accesa locația unde se afla fișierul sursă index.html care în mod normal afișează “hello world” , edităm acel fișier și scriem “hello world from another container” . În acest moment avem 2 containere care rulează si ambele sunt pe baza aceleiași imagini. Dacă le vom accesa pe fiecare în parte vom vedea că unul va afișa “hello world” pe când celalalt va afișa “hello world from another container”.


**3. Structura imaginii**

UFS – Union File System este sistemul de fișiere folosit de imaginile de Docker, si este compus din mai multe layere. De fiecare data când se face o schimbare la nivel de sistem de fișiere, adică atunci când un fișier este adăugat, un nou layer este adăugat deasupra layerelor deja existente. Toate aceste layere unite (de unde vine si denumirea sistemului de “Union”) formează sistemul de fișiere care este expus in container.

Dacă vom descărca un container de mysql versiunea **mysql:5.7-oracle** și apoi **mysql:8-oracle**

Când dăm pentru prima dată comanda **docker pull mysql:5.7-oracle** se va descărca local acestă imagine și un numar de n layere. Dacă ulterior vom dori să descărcăm **mysql:8-oracle** descărcarea noii imagini va dura mult mai puțin deoarece aceastea au layere comune și se va descărca doar layerele pe care versiunea 8 le are in plus. Acest lucru este foarte eficient din punct de vedere al spațiului de stocare și al vitezei.


## Cum creăm imagini cu Dockerfile

Până acum am utilizat imagini descărcate din repositotory-ul public de dockerhub. Acest lucru se intamplă când rulam **docker pull nume_imagine**. Totuși, sunt multe cazuri în care în cadrul proiectului la care lucrăm sa avem imagini custom, de exemplu un site web cu fișierele noastre html și php. Astfel, atunci când pornim un container pe baza acelei imagini, să avem acces la varianta finală, fără a mai face și alte modificări.

**Ce este un Dockerfile ?**

Un Dockerfile este o rețetă pentru a crea imagini Docker. Un Dockerfile este un document text care conține toate comenzile pe care un utilizator le-ar putea apela pe linia de comandă pentru a asambla o imagine. Folosind apoi comanda **docker build** utilizatorii pot crea o versiune automată care execută mai multe instrucțiuni de linie de comandă succesive. Putem lua o imagine publică de **httpd** și o putem customiza după cum dorim.

**Exemplu 1:**

mkdir public-html -> creăm un folder public-html

echo “my custom configuration works!” >  ./public-html/index.html

touch Dockerfile și adaugăm urmatorul text în Dockerfile:

**FROM httpd:2.4**

**COPY ./public-html/ /usr/local/apache2/htdocs/**

Acum dorim să facem un imagine pe baza acestui fișier numit Dockerfile. Acest lucru se poate face executând comanda de mai jos. Este necesar ca fișierul să se numească Dockerfile , altfel comanda docker build nu va funcționa. Acel punct de la final reprezintă faptul că dorim să facem acea imaginie pe baza unu dockerfile din locația curentă .

**docker build -t nume_imagine:nume_tag .**

**docker build -t myimage:v1**

Imaginea a fost creată. Putem verifica asta cu comanda docker images . De asemenea, putem crea un container pe baza acelei imagini.

 **docker run –d myimage:v1** 

Diferențele se pot vedea în cele două poze și astfel ne putem crea un website customizat cu un singur fișier Dockerfile.


## Video || Prezentare Dockerlife

Este necesar ca in directorul curent sa avem un **Dockerfile** si un folder cu numele public-html care sa aiba un fisier **index.html**

1) Dockerfile va avea urmatorul continut:

**FROM httpd:2.4**

**COPY ./public-html/ /usr/local/apache2/htdocs**

**EXPOSE 80**

2) **index.html** este doar un simplu fisier de html

De exemplu:
``` html
<!DOCTYPE html>

<html>

    <head>

        <title>Example</title>

    </head>

    <body>

        <p>This is an example of a simple HTML page with one paragraph.</p>

    </body>

</html> 
```


3) docker build -t custom_website .

custom_website -> va fi numele imaginii de docker, aici poate fi pus orice nume

punct -> reprezinta locatia de unde vrem sa citim Dockerfile

4) docker run -d -p 80:80 ID_IMAGINE_GENERATA_ANTERIOR

De asemenea, poate fi si custom_website

5) docker container ls

6) docker stop ID_CONTAINER
7) 
```

Best # Docker Containers for Home Server!
https://www.youtube.com/watch?v=9uF2us2PabM

```

