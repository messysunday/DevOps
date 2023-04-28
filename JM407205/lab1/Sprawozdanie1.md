# Sprawozdanie lab1

**1. Utworzenie kluczy:**

![ss1](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss1.png)

![ss2](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss2.png)

**2. Dodanie do Github'a:**

![ss3](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss3.png)

**3. Sklonowanie repozytorium:**

![ss4](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss4.png)

**4. Utworzenie nowej gałęzi:**

![ss5](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss5.png)

**5. Utworzenie katologu z własnymi inicjałami:**

![ss6](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss6.png)

**6.Utworzenie hooka, sprawdzającego poprawność wiadomości commit'a, umieszczenie go w .git/hooks oraz działanie:**

![ss7](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss7.png)

![ss8](https://github.com/InzynieriaOprogramowaniaAGH/MDO2023_S/blob/JM407205/JM407205/ss/ss8.png)

```
#!/usr/bin/python3

import sys

commit_msg_path = sys.argv[1]

with open(commit_msg_path, "r+") as f:
    commit_msg = f.read()
    if("407205" in commit_msg):
        print("Inicjaly znajduja sie")
    else:
        print("nie ma inicjalow")
        ```
  
            
            
 



