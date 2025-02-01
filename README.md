# Socat for Windows

![Screenshot_2023-11-08-23-38-22-47_40deb401b9ffe8e1df2f1cc5ba480b12](https://github.com/valorisa/socat-1.7.4.4_for_Windows/assets/13067566/c562ce4c-64e6-463b-8863-e9dd8e30d053)

socat (SOcket CAT: netcat on steroids) is a relay for bidirectional data transfer between two independent data
channels. Each of these data channels may be a file, pipe, device (serial line
etc. or a pseudo terminal), a socket (UNIX, IP4, IP6 - raw, UDP, TCP), an
SSL socket, proxy CONNECT connection, a file descriptor (stdin etc.), the GNU
line editor (readline), a program, or a combination of two of these.
These modes include generation of "listening" sockets, named pipes, and pseudo
terminals.

Some of the examples of using socat are :

- TCP relay (one-shot or daemon)
- External socksifier
- Shell interface to Unix sockets
- IPv6 relay
- Netcat and rinetd replacement
- Redirecting TCP-oriented programs to a serial line
- Establishing a relatively secure environment (su and chroot) for running client or server shell scripts inside network connections.

 <http://www.dest-unreach.org/socat/doc/socat.html#EXAMPLES>
  
## socat-1.8.0.1 for Windows 7, 8.1, 10 & 11 & Server

socat 1.8.0.1-x86_64 for Windows 7, 8.1, 10 & 11 & Server
[2024-08-24]

The procedure for those who want to compile from the source files.

Otherwise for the others, there is one ready-made file **'socat-1.8.0.1.7z'**.
You can download it by going to : [socat-1.8.0.1.7z](https://github.com/valorisa/socat-1.8.0.1_for_Windows/blob/main/socat-1.8.0.1.7z) and proceeding by keyboard shortcut (Ctrl + Shift + s).

First of all, if it is not done yet, download and install Cygwin (last version) : <https://www.cygwin.com/setup-x86_64.exe>

### **Pourquoi compiler `socat` à partir de Cygwin ?**
- Tu peux obtenir la dernière version de `socat` (si elle n'est pas disponible dans les paquets Cygwin).
- Tu peux personnaliser la compilation (par exemple, activer ou désactiver des fonctionnalités).
- C'est une excellente façon d'apprendre comment compiler des programmes sous Windows avec des outils Unix.

---

### **Étape 1 : Installer les outils de compilation dans Cygwin**

Pour compiler `socat`, tu as besoin des outils de développement comme `gcc`, `make`, et d'autres dépendances. Suis ces étapes pour les installer :

1. **Ouvre Cygwin** :
   - Lance Cygwin depuis le menu Démarrer ou en double-cliquant sur l'icône du bureau.

2. **Installe les paquets nécessaires** :
   - Dans la fenêtre Cygwin, tape la commande suivante pour installer les outils de compilation :
     ```bash
     apt-cyg install gcc-core make automake autoconf libtool git
     ```
   - Si `apt-cyg` n'est pas installé, tu peux l'ajouter en suivant les instructions sur [apt-cyg](https://github.com/transcode-open/apt-cyg).

   - Ces paquets incluent :
     - `gcc-core` : Le compilateur C.
     - `make` : Un outil pour gérer la compilation.
     - `automake`, `autoconf`, `libtool` : Des outils pour configurer le projet.
     - `git` : Pour télécharger le code source de `socat`.

---

### **Étape 2 : Télécharger le code source de `socat`**

1. **Clone le dépôt Git de `socat`** :
   - Dans Cygwin, tape la commande suivante pour télécharger le code source :
     ```bash
     git clone http://repo.or.cz/socat.git
     ```
   - Cela va créer un dossier appelé `socat` dans ton répertoire actuel.

2. **Va dans le dossier `socat`** :
   ```bash
   cd socat
   ```

---

### **Étape 3 : Configurer et compiler `socat`**

1. **Génère les fichiers de configuration** :
   - Si le projet utilise `autoconf` et `automake`, tu dois d'abord générer les fichiers de configuration. Tape :
     ```bash
     autoreconf -i
     ```

2. **Configure le projet** :
   - Exécute le script `configure` pour préparer la compilation :
     ```bash
     ./configure
     ```
   - Cela vérifie que toutes les dépendances sont installées et configure le projet pour ton système.

3. **Compile `socat`** :
   - Utilise `make` pour compiler le programme :
     ```bash
     make
     ```
   - Cela peut prendre quelques minutes, selon la puissance de ton ordinateur.

4. **Installe `socat` (optionnel)** :
   - Si tu veux installer `socat` dans Cygwin pour pouvoir l'utiliser depuis n'importe où, tape :
     ```bash
     make install
     ```
   - Cela copiera le fichier `socat` dans le répertoire `/usr/local/bin` de Cygwin.

---

### **Étape 4 : Vérifier que `socat` fonctionne**

1. **Vérifie la version de `socat`** :
   - Tape la commande suivante pour vérifier que `socat` a bien été compilé et installé :
     ```bash
     socat -V
     ```
   - Cela devrait afficher la version de `socat`.

2. **Teste `socat`** :
   - Tu peux tester `socat` en créant un simple relais TCP. Par exemple :
     ```bash
     socat TCP-LISTEN:8080,fork TCP:example.com:80
     ```
   - Cela écoutera sur le port 8080 de ton ordinateur et redirigera le trafic vers `example.com` sur le port 80.

---

### **Étape 5 : Ajouter `socat` au PATH (Optionnel)**

Si tu as compilé `socat` mais ne l'as pas installé avec `make install`, tu peux ajouter le fichier binaire `socat` à ton PATH manuellement.

1. **Trouve le fichier `socat`** :
   - Après la compilation, le fichier `socat` se trouve dans le dossier `socat` (là où tu as exécuté `make`).

2. **Ajoute-le au PATH** :
   - Copie le fichier `socat` dans un répertoire inclus dans ton PATH, par exemple :
     ```bash
     cp socat /usr/local/bin/
     ```

---

### **Résumé des Étapes**
1. Installe les outils de compilation dans Cygwin (`gcc`, `make`, etc.).
2. Télécharge le code source de `socat` avec `git clone`.
3. Configure et compile `socat` avec `./configure` et `make`.
4. Installe `socat` avec `make install` (optionnel).
5. Vérifie que `socat` fonctionne avec `socat -V`.

---

### **Avantages de compiler `socat`**
- Tu obtiens la dernière version du programme.
- Tu peux personnaliser la compilation.
- C'est une excellente façon d'apprendre à compiler des programmes sous Windows avec Cygwin
