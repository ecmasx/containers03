# Containerizare si Virtualizare - Laboratorul 4: Utilizarea containerelor ca medii de execuție

## 1. Denumirea lucrării de laborator

Utilizarea containerelor ca medii de execuție

## 2. Scopul lucrării de laborator

Familiarizarea cu comenzile de bază ale OS Debian/Ubuntu, crearea unui container cu server web Apache.

## 3. Sarcina lucrării de laborator

Pornind de la imaginea oficială a sistemului de operare Ubuntu, să se creeze un container care să conțină un server web Apache. Să se creeze o pagină web care să conțină textul "Hello, World!" și să se afișeze într-un browser.

## 4. Descrierea executării lucrării de laborator

### 4.1. Pregătire

Docker este instalat pe computer.

### 4.2. Crearea și pornirea containerului

1. Deschideți terminalul în directorul `containers03`.
2. Executați comanda:

   ```bash
   docker run -ti -p 8000:80 --name containers03 ubuntu bash
   ```

   - **Scop:** Această comandă creează și pornește un container nou numit `containers03` bazat pe imaginea Ubuntu.
     - `-ti`: Alocă un pseudo-TTY și menține STDIN deschis, permițându-vă să interacționați cu containerul.
     - `-p 8000:80`: Publică portul 80 al containerului pe portul 8000 al mașinii gazdă. Asta înseamnă că traficul către portul 8000 al computerului dvs. va fi redirecționat către portul 80 al containerului.
     - `--name containers03`: Atribuie numele `containers03` containerului.
     - `ubuntu`: Specifica imaginea Ubuntu care va fi utilizată pentru a crea containerul.
     - `bash`: Specifica comanda `bash` care va fi executată în container după pornire. Aceasta vă oferă un shell interactiv în interiorul containerului.
   - **Rezultat:** Se va crea un nou container și voi intra în linia de comandă a containerului.

   ![docker run](/images/docker%20run%20-ti.jpg)

### 4.3. Instalarea serverului Apache

În fereastra deschisă, executați următoarele comenzi:

1. Actualizați lista de pachete:

   ```bash
   apt update
   ```

   - **Scop:** Actualizează lista de pachete disponibile din depozitele Ubuntu.
   - **Rezultat:** Lista de pachete este actualizată.
     ![apt update](./images/apt%20update.jpg)

2. Instalați serverul Apache:

   ```bash[]
   apt install apache2 -y
   ```

   - **Scop:** Instalează serverul web Apache2 și toate dependențele sale.
     - `-y`: Răspunde automat cu "yes" la toate întrebările de instalare, evitând astfel întreruperile.
   - **Rezultat:** Serverul Apache2 este instalat.
   - **Afișare în consolă:** ![apt install](/images/apt%20install%20apache2%20-y.png)

3. Porniți serverul Apache:

   ```bash
   service apache2 start
   ```

   - **Scop:** Pornește serverul Apache2.
   - **Rezultat:** Serverul Apache2 este pornit.
   - **Afisare** ![apache start](/images/apache%20start.png)

4. Deschideți browserul și introduceți în bara de adrese `http://localhost:8000`.

   - **Ce vedeți?** Ar trebui să vedeți pagina implicită a serverului Apache2.

   ![apache default page](/images/ce%20va%20fi%20afisat.jpg)

### 4.4. Crearea paginii "Hello, World!"

1. Verificați conținutul directorului `/var/www/html/`:

   ```bash
   ls -l /var/www/html/
   ```

   - **Scop:** Listează fișierele și directoarele din directorul `/var/www/html/`, care este directorul rădăcină implicit pentru serverul web Apache.
   - **Rezultat:** Vom vedea o listă cu fișierele din directorul `/var/www/html/`, inclusiv fișierul `index.html` implicit.

2. Creați o pagină web "Hello, World!":

   ```bash
   echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
   ```

   - **Scop:** Suprascrie fișierul `index.html` existent cu un nou fișier care conține textul "Hello, World!".
   - **Rezultat:** Fișierul `index.html` este înlocuit.

3. Reîmprospătați pagina în browser (`http://localhost:8000`).

   - **Ce vedeți?** Vedem textul "Hello, World!".

   ![hello world](./images/dupa%20folosirea%20comenzii%20echo%20'HEllo%20World'.jpg)

### 4.5. Configurarea Apache

1. Accesați directorul cu site-urile disponibile:

   ```bash
   cd /etc/apache2/sites-enabled/
   ```

   - **Scop:** Schimbă directorul curent în `/etc/apache2/sites-enabled/`, unde sunt stocate configurațiile pentru site-urile web activate pe serverul Apache.
   - **Rezultat:** Directorul curent este schimbat.

2. Vizualizați conținutul fișierului `000-default.conf`:

   ```bash
   cat 000-default.conf
   ```

   - **Scop:** Afișează conținutul fișierului `000-default.conf`, care este fișierul de configurare implicit pentru site-ul web implicit al serverului Apache.
   - **Rezultat:** Vom vedea conținutul fișierului de configurare.

   ![cat config](/images/000-default.conf.png)

### 4.6. Curățare

1. Închideți fereastra terminalului cu comanda:

   ```bash
   exit
   ```

   - **Scop:** Închide sesiunea curentă în container și vă întoarce la linia de comandă a mașinii gazdă.
   - **Rezultat:** Ieșiți din container.
   - **Afișare în consolă:** (Nu ar trebui să existe o afișare semnificativă în consolă)

2. Afișați lista de containere:

   ```bash
   docker ps -a
   ```

   - **Scop:** Listează toate containerele Docker, inclusiv cele care sunt oprite.
     - `-a`: Afișează toate containerele (implicit, `docker ps` afișează doar containerele care rulează).
   - **Rezultat:** Va fi o listă cu toate containerele, inclusiv `containers03`.

   ![docker ps -a](/images/docker%20ps.png)

3. Ștergeți containerul:

   ```bash
   docker rm containers03
   ```

   - **Scop:** Elimină containerul cu numele `containers03`.
   - **Rezultat:** Containerul este șters.

## 5. Concluzii

În cadrul acestei lucrări de laborator, am învățat cum să creăm un container Docker bazat pe imaginea Ubuntu, să instalăm și să configurăm un server web Apache în interiorul containerului și să afișăm o pagină web simplă. Am explorat, de asemenea, comenzile de bază Docker pentru gestionarea containerelor.
