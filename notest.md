### instalacja dockera

https://docs.docker.com/engine/install/ubuntu/
https://www.omgubuntu.co.uk/how-to-install-docker-on-ubuntu-20-04

na ubunto 20.4  `sudo apt install docker.io`
`sudo apt update`

`sudo systemctl enable docker` uruchamia srodowisko

docker ps - wyswietla stan

poczatkowo trzeba dodac uzytkowanika do grupy dockera

`sudo usermod -aG docker nazwaUsera`

spawdzenei czy jest ok  `docker ps`

### instalacja docker compose

https://docs.docker.com/compose/install/

`sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

trzea ustawic uprawnienia 

`sudo chmod +x /usr/local/bin/docker-compose`

sprawdzenei `docker-compose`

### jenkins

`docker pull jenkins/jenkins`

sprawdzenie gdzie jest obraz dockerowy  `docker images`

`docker info | grep -i root`  pokaze nam lokalizacje dockera

sparwdzenie ile MB maja obrazy dockera  `sudo du -sh /var/lib/docker`   


`mkdir -d jenkins/jenkins-data`

tworzymy plik konfiguracyjny `vim docker-compose.yml` lub `nano docker-compose.yml`

aby widziec w naszym utworzonym katalogu dockerowym wszytsko trzeba ustawic dostepy

wpisujemy `id` i widzymy ze nasz user ma dostepy na 1000

trzeba to ustawic `sudo chown 1000:1000 jenkins_home -R`    to jest katalog utworzony na podstawie pliku

`docker logs -f jenkins`  jenkins to jest nazwa obrazu  - pokazuje logi wszytskie

uruchomienie obrazu na zasadzie utworzenia `docker-compose up -d`  
potem pozna robic `docker-compose start`  lub `docker-compose stop`  mozemy `docker-compose restart nazwa_obrazu` 
moza `docker-compose down` zatrzymuje i usuwa



`ip a`  pokazuje uzyte adresy ip 

druga pozycja 'enp0s3' to adres naszej maszyny chyba virtualnej u mnie 192.168.8.108

w przegladarce bedziemy wizec 192.168.8.107:8080 jenkinsa


dodajemy DNS w lokalizacji `C:\Windows\System32\drivers\etc\host`  '192.168.8.107 jenkins.ubuntu'
dzieki temu mozna wolac palikacje po nazwie a nie po IP

`docker exec -ti jenkins bash` odpali nam terminal i bedziemy tam zaogowani wyjscie komanda `exit`

LINUX `echo "Current date and time is $(date)"`
LINUX `echo "Current date is $(whoami)"`

w configure projektu jenkins dodajemy buid > exeute shell - to jet to samo jak bysm sie zalogowali do terminala w docker jenkins komenda docker exec ....


LINUX 
`NAME=Bartek
echo "Hello $NAME. Current date and time is $(date)"`

zapisanie do pliku  `echo "Hello $NAME. Current date and time is $(date)" > /tmp/info`

### Script in bash:

zaczynamy od 
`#!/bin/bash`
`NAME=$1`
`LASTNAME=$2`
`echo "Hello, $NAME $LASTNAME"`

zapisujemy w do pliku np script.sh

uruchomienie `./script.sh`

treba zmienic uprawnienia

`chmod +x ./script.sh`

aby prawidlowo uruchomoc musimy podac dwie zmienne zadeklarowane
`./script.ch Bart Jan`


aby ten plik byl widoczny w docker obecnie mozemy skopiowac go:

`docker cp script.sh jenkins:/tmp/script.sh`

w jenkins shell mozemy kozystac z tego skryptu `/tmp/script.sh Bart Jan`

w bash deklaracja zmiennych jest bez pustego miejsca musi byc >> zmienna=wartosc


Wywolac z exeute shell mozna rowniez poprzez zmienne:
`NAME=Bart`
`LASTNAME=Jan`
`/tmp/script.sh $NAME $LASTNAME`

### wykozystanie parametrow  >> 'this project is parametrize'

poedynczy paramer string > 'String parameter'

lista parametrow ktora bedzie do wyboru przy Buid >> 'Choice Parameter'

nowy script:

`NAME=Bart`
`LASTNAME=Jan`
`SHOW=$3`

`if [ "$SHOW" = "true" ]; then`
   `echo "Hello" $NAME $LASTNAME`
`else
    echo "If you want to see the name, please mark the show option"
 fi`
 
