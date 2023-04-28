# Sprawozdanie z laboratorium nr 2

*1.Instalacja Dockera w systemie Linuksowym:*

Przy pomocy polecenia `sudo docker -v` sprawdziłam posiadanie Dockera:

![ss1-posiadanie dockera](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss1-posiadanie%20dockera.png)

Kolejenym krokiem było odinstalowanie istniejącej wersji Dockera:

``sudo apt-get remove docker docker-engine docker.io containerd runc``

![usuwanie starego dockera](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/usuwanie%20starego%20dockera.png)

Nastepnie zaktualizowano polecenie apt:

`sudo apt-get update`

![ss6](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss6.png)


Pobranie wymaganych pakietów do ustawienia repozytorium Dockera:
``
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    ``
![ss3-update](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss3-update.png)

Dodanie klucza GPG:

``
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
``
![ss4](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss4.png)


Instalacja Dokcer Engine:

`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

![ss7](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss7.png)

*2.Logowanie do DockerHub i zapoznanie się z przykładowymi obrazami:*

Zalogowałam się za pomocą strony [DockerHub](https://hub.docker.com/):

![ss8](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ss8.png)

Przykładowe obrazy, które znajdują się na stronie:

![przykladowe obraz](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/przykladowe%20obrazy.png)

*3.Pobranie hello-world, busybox, ubuntu i mysql:*

Obrazy zostały pobrane za pomocą komendy:

`sudo docker pull [nazwa obrazu]`

![pobranie obrazow](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/pobranie%20obrazow.png)

![ubuntu](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/ubuntu.png)

*4.Uruchomienie busybox:*

Uruchomiłam busybox i sprawdziałam działanie za pomocą:

``
sudo docker run busybox
sudo docker ps
``

![busybox1](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/busybox1.png)

Następnie podłączyłam sie do kontenera interaktywnie i wywołałam numer sesji za pomocą poleceń:

``
sudo docker run -i -t busybox
ls
``
![busybox-uruchomienie](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/busybox%20-%20uruchomienie.png)

*5.Uruchomienie "systemu w kontenerze"

Zaprzezntowano PID1 w kontenerze i procesy dockera na hoście za pomocą:

`sudo docker run -it --pid=host ubuntu `
![uruchomienie systemu w kontenerze i zaprezentowanie pid1 oraz procesow docker na hoscie](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/uruchomienie%20systemu%20w%20konetnerze%20i%20zaprezentowanie%20pid1%20oraz%20procesow%20docker%20na%20hoscie.png)

Zaktualizowano  pakiety:

`apt update`

![zaktualizowanie pakietów](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/zaktualizowanie%20pakiet%C3%B3w.png)

Wyjście z kontenera:

`exit`

![wyjscie](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/wyjscie%20.png)

*6.Stworzenie Dockerfile i skopiowanie repozytorium:*

Napisany został Dockerfile, który klonuje repozytorium przez token, który wygenerowałam przez swoje konto na GitHubie (losowe litery z tokenu zostały usunięte z powodu bezpieczeństwa). Obraz został stworzony na systemie Ubuntu, `RUN apt-get -y install git` gwarantuje, że utworzony obraz będzie zawierał git'a:

``

FROM ubuntu:latest

RUN apt-get -y update 
RUN apt-get -y install git

RUN git clone https://sundayheathers:ghp_pvYkGj2iNWx9cSn7QT85OeYnCrN6k2fA@github.com/InzynieriaOprogramowaniaAGH/MDO2023_S.git 

``



![token](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/token.png)

Komenda przez, którą stworzyłam Dockerfile (wybrałam edytor tekstu- GNU nano):

![nano](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/nano.png)

Następnie zbudowałam obraz za pomocą:

`sudo docker build - < Dockerfile `

![zbudowanie obrazu](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/zbudowanie%20obrazu.png)

Uruchomiłam kontener w trybie interaktywnym i sprawdziłam czy udało się skopiować repozytorium (jak można zauważyć udało się skopiować repozytorium MdO2023_S):

`sudo docker run -i -t [nazwa obrazu]`

![dzialnie](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/dzialnie.png)

*7. Pokazanie uruchomionych kontenerów oraz wyczyszczenie ich:*

Pokazanie uruchomionych kontenerów za pomocą komendy:

`sudo docker container ls`

![dzialajace kontenery](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/dzialajce%20kontenery.png)

Zatrzymanie działającego kontenera przed usunięciem:

`sudo docker container stop [nazwa kontenera] `

![zatrzymanie kontenera](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/zatrzymanie%20kontenera.png)

Wyczyszczenie kontenera:

`sudo docker container rm [nazwa kontenera] `

![wyczyszczenie kontenerow](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/wyczyszczenie%20kontenerow.png)

*8.Wyczyszczenie obrazów:*

Wyświetlenie obrazów za pomocą komendą:

`sudo docker images`

![wyswietlenie obrazow](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/wyswietlnie%20obrazow.png)

Wyczyszczenie obrazów:

`sudo docker images prune `

![usuniecie obrazow](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/usuniecie%20obrazow.png)

*9.Dodanie Dockerfile do utworzonego folderu lab2: *

![folder](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/lab2/lab2-devops/folder.png)

















