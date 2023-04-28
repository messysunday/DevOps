# Laboratorium nr 3

**1.Znalezienie projektu umożliwiającego łatwe wykonywanie testów:**

- Wybranie [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot), gdyż cały projekt napisany jest w języku Python, z którym jestem zaznajomiona i wykonuje się w nim prosto testy. Ponadto jest opis do tego jak wykonywac testy, co ułatwiło mi pracę: [python-telegram-bot-tests](https://github.com/python-telegram-bot/python-telegram-bot/blob/master/tests/README.rst).
- Pobranie repozytorium przy użyciu GitHub CLI:

![1](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/1.png)

**2.Przeprowadzenie budowy i konfiguracji środowiska:**

- Konfiguracja środowiska -pobrania Pythona:

![2](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/2.png)

- Pobranie polecenie pip oraz pytest, przy użyciu którego będę następnie dokonywała testowania.

![3](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/3.png)

![4](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/4.png)

- Zainstalowanie zawartości pliku requirements.txt:

![5](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/5.png)

- Instalacja web-frameworka, który jest również bibliotekę Pythona:

![6](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/6.png)

- Instalacja dodatkowych zależności, które zawarte były w Readmie repozytorium:

![7](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/7.png)

![8](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/8.png)

**3.Uruchmienie testów:**

- Uruchomienie testów poleceniem, które zostało zawarte w Readmie repozytorium:

![9](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/9.png)

- Rezultat końcowy uruchomienia testów:

![10](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/10.png)

**4.Ponowienie procesu w kontenerze:**

- Uruchomienie kontenera, jako baza został wybrany ofucjalny obraz Python z Dockerhub'a,:

![11](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/11.png)

- Uruchomienie kontenera w trybie interaktywnym:

![12](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/12.png)

- Pobranie repozytorium przy użyciu tokenu:

![13](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/13.png)

- Konfiguracja środowiska (instalacja zawartości pliku requirements, biblioteki tornado oraz dodatkowych zależności, zawartych w rezpotorium, dzięki zawartości obrazu pytona pominięto intslację pythona):

![brakujacy ss](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/brakujacy%20ss.png)

- Uruchomienie testów:

![14](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/14.png)

- Wynik testów:

![15](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/15.png)

**5.Stworzenie Dockerfile, który będzie realizował powyższy proces:**
``` 
FROM python:latest
# update
RUN apt-get -y update
# clone repo
RUN git clone https://github.com/python-telegram-bot/python-telegram-bot.git
WORKDIR "python-telegram-bot/"
# install
RUN python setup.py install
# pip install all requirements
RUN pip install -r requirements-dev.txt tornado pytz python-telegram-bot[passport] python-telegram-bot[http2] python-telegram-bot[callback-data]
```
**6.Zbudowanie Dockerfile:**

![16](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/16.png)

**7.Stworzenie nowego Dockerfile'a bazującego na nowoutworzonym obrazie, nowy kontener uruchamia testy:**
```
FROM python-telegram-bot:latest
# run tests
RUN python -m pytest -m no_req
```
- Zbudowanie obrazu:

![17](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/17.png)

- Uruchomione obrazy:

![18](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/18.png)

**7.zdefiniowanie kompozycji:**

- Skorzystałam tutaj z Docker Compose, który jest narzędziem do uruchamiania multi-container aplikacji. Pobrałam oraz skonfigurowałam Docker Compose korzystjąc z [docker-compose-on-ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)

![19](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/19.png)

- Następnie stworzyłam plik yml, która stworzy dwie usługi na podstawie zaprezentowanych wcześniej Dockerfile'i:

```
version: "3.9"
services:
  python-telegram-bot:
    image: python-telegram-bot:latest
    build: 
      context: .
      dockerfile: ptb.Dockerfile
  python-telegram-bot-tests:
    image: python-telegram-bot-tests:latest
    build:
      context: .
      dockerfile: ptbtest.Dockerfile
    depends_on:
      - python-telegram-bot
    
```

- Uruchomienie:

![20](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/20.png)

- Zakończenie działania:

![21](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/MJ407205/JM407205/lab3/ss/21.png)

Dyskusja:
1.Czy program nadaje się do wdrażania i publikowania jako kontener, czy taki sposób interakcji nadaje się tylko do builda
Wybrany projekt jest aplikacją interaktywną, ze względu na specyfikę programu interakcja poprzez kontener jest wystarczająca, program nadaje się do wdrażania jako kontener. Dodatkowo warto wziąć pod uwagę oczekiwania klientów, środowisko finalnego uruchamiania, w pewnych przypadkach publikacja poprzez pakiety jest korzystniejsza

2.Opisz w jaki sposób miałoby zachodzić przygotowanie finalnego artefaktu
jeżeli program miałby być publikowany jak? A może dedykowany deploy-and-publish byłby oddzielną ścieżką (inne Dockerfiles)? Czy zbudowany program należałoby dystrybuować jako pakiet, np. JAR, DEB, RPM, EGG?
-jeśli aplikacja ma być publikowana jako kontener należy oczyścić wszelkie pozostałości po build'zie, aby ograniczyć zużycie miejsca
-jeśli mamy do czynienia z bardziej zawansowanymi projektami można rozważyć dedykowaną ścieżkę deploy-and-publish, można wtedy zdefiniować osobne Dockerfile dla budowania i publikowania kontenera, które będą zawierać tylko niezbędne pliki i oprogramowanie.
-jeśli projekt nie nadaje się do publikacji jako kontener należy rozważyć opcję publikacji jako pakiet (np. JAR, DEB, RPM, EGG). Jednak raczej nie będzie zalecane zrobienie tego jako eggs gdyż zostało to wyparte na rzecz Wheels. Ogółem to w środku program zawiera już ext pakiet

3.W jaki sposób zapewnić taki format? Dodatkowy krok (trzeci kontener)? Jakiś przykład?
Można stworzyć dodatkowy krok w Dockerfile, który wykorzysta odpowiednie narzędzia do "pakowania" programu w wybrany format. W ten sposób, po zbudowaniu kontenera, zostanie wygenerowany plik np. JAR, który będzie można wykorzystać do dystrybucji programu. Alternatywnie, można stworzyć oddzielny kontener, który będzie zajmował się "pakowaniem" programu w wybrany format. 






