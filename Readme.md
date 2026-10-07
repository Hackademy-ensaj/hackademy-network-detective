# 🕵️ HACKademy — Network Detective

> **Après avoir appris à enquêter sur un système Linux, il est temps de comprendre comment cette machine communique avec le réseau.**

Bienvenue dans **Network Detective**, le deuxième laboratoire de la série proposée par **HACKademy**.

Dans ce lab, tu vas utiliser ton propre ordinateur pour découvrir progressivement :

- son adresse IP ;
- sa passerelle ;
- les ports ouverts ;
- les services réseau ;
- le fonctionnement de HTTP ;
- le DNS ;
- et les premières notions de reconnaissance avec Nmap.

⚠️ **Aucune machine virtuelle n'est nécessaire.**  
Toutes les manipulations sont réalisées sur ton **PC réel**.

---

## 🎯 Objectifs

À la fin du laboratoire, tu seras capable de :

- identifier l'adresse IP de ta machine ;
- identifier la passerelle par défaut ;
- tester une connexion réseau avec `ping` ;
- consulter les ports en écoute ;
- lancer un petit serveur web local ;
- utiliser `curl` pour communiquer avec un service HTTP ;
- découvrir un service avec Nmap ;
- comprendre le rôle du DNS.

---

## 🧰 Prérequis

Ce laboratoire fait suite à **Linux Detective**.

Tu dois connaître les commandes Linux de base :

```bash
pwd
ls
cd
mkdir
cat
```

### Environnement

- 💻 PC réel
- 🐧 Linux recommandé
- 🌐 Connexion réseau
- 🔎 Nmap

Aucune machine virtuelle n'est nécessaire.

---

# 🕵️ Mission 1 — Trouver ton identité réseau

Chaque machine connectée à un réseau possède une adresse IP.

Commence par découvrir les interfaces réseau de ton ordinateur :

```bash
ip addr
```

Observe les différentes interfaces et cherche une adresse IPv4 ressemblant à :

```text
192.168.x.x
```

ou :

```text
10.x.x.x
```

ou :

```text
172.16.x.x
```

### 🔎 Questions

- Quelle est ton adresse IPv4 ?
- Quelle interface réseau est actuellement utilisée ?
- Que représente l'adresse `127.0.0.1` ?

---

# 🕵️ Mission 2 — Trouver la sortie

Une machine doit savoir vers où envoyer les paquets destinés à un autre réseau.

Affiche la table de routage :

```bash
ip route
```

Tu devrais trouver une ligne ressemblant à :

```text
default via 192.168.1.1 dev ...
```

L'adresse après `default via` correspond généralement à ta **passerelle par défaut**.

### 🔎 Questions

- Quelle est ta passerelle ?
- Quelle interface est utilisée pour sortir du réseau local ?
- À quoi sert une passerelle ?

---

# 🕵️ Mission 3 — Tester la communication

Teste maintenant ta propre machine :

```bash
ping 127.0.0.1
```

Observe les réponses.

Puis teste ta passerelle :

```bash
ping ADRESSE_DE_TA_PASSERELLE
```

Par exemple :

```bash
ping 192.168.1.1
```

Arrête le test avec :

```text
Ctrl + C
```

### 🔎 Questions

- Quelle différence entre `127.0.0.1` et l'adresse de ta passerelle ?
- Que signifie une réponse reçue par `ping` ?
- Que se passe-t-il si aucune réponse n'est reçue ?

---

# 🕵️ Mission 4 — Chercher les portes ouvertes

Une application réseau utilise généralement un **port** pour recevoir des connexions.

Affiche les ports actuellement en écoute :

```bash
ss -tuln
```

Tu peux observer des lignes comme :

```text
LISTEN
```

### 🔎 Questions

- Quels ports sont actuellement ouverts sur ta machine ?
- Quelle différence entre TCP et UDP ?
- Pourquoi une application a-t-elle besoin d'un port ?

---

# 🕵️ Mission 5 — Installer ton premier service

Nous allons maintenant créer un petit serveur web directement sur ton ordinateur.

Crée un dossier :

```bash
mkdir network-detective
cd network-detective
```

Crée ensuite une petite page :

```bash
echo "HACKademy Network Detective" > index.html
```

Lance le serveur :

```bash
python3 -m http.server 8000
```

Tu devrais obtenir un message indiquant que le serveur écoute sur le port `8000`.

⚠️ Laisse ce terminal ouvert.

---

# 🕵️ Mission 6 — Communiquer avec ton serveur

Ouvre un **deuxième terminal**.

Teste ton serveur avec :

```bash
curl http://127.0.0.1:8000
```

Tu devrais obtenir :

```text
HACKademy Network Detective
```

Tu peux également ouvrir ton navigateur et accéder à :

```text
http://127.0.0.1:8000
```

### 🔎 Questions

- Quelle adresse utilises-tu ?
- Quel port est utilisé ?
- Quel protocole est utilisé ?
- Quelle est la différence entre `http://127.0.0.1:8000` et `http://127.0.0.1` ?

---

# 🕵️ Mission 7 — Observer le port

Pendant que le serveur Python fonctionne, exécute :

```bash
ss -tuln
```

Cherche maintenant le port :

```text
8000
```

Tu viens de créer un **service réseau local**.

### 🔎 Réflexion

Avant de lancer le serveur, le port `8000` n'était probablement pas présent.

Après son lancement, il apparaît comme un port en écoute.

**Question :**

> Qu'est-ce qui a changé sur ta machine ?

---

# 🕵️ Mission 8 — Utiliser Nmap

Nmap est un outil utilisé pour découvrir des hôtes, des ports et des services réseau.

Pour cette première utilisation, nous allons scanner **uniquement ta propre machine**.

Lance :

```bash
nmap 127.0.0.1
```

Observe les résultats.

Puis vérifie directement le port de notre serveur :

```bash
nmap -p 8000 127.0.0.1
```

Tu devrais voir quelque chose ressemblant à :

```text
8000/tcp open
```

### 🔎 Questions

- Que signifie `open` ?
- Quel service avons-nous volontairement rendu accessible ?
- Pourquoi utilise-t-on `127.0.0.1` ici ?

---

# 🕵️ Mission 9 — Identifier le service

Nmap peut également essayer d'identifier le service qui fonctionne derrière un port.

Lance :

```bash
nmap -sV -p 8000 127.0.0.1
```

Observe le résultat.

Tu devrais pouvoir identifier le serveur Python utilisé précédemment.

### 🔎 Question

> Comment Nmap peut-il obtenir des informations sur le service présent derrière le port ?

---

# 🕵️ Mission 10 — Enquêter sur le DNS

Lorsque tu écris un nom de domaine comme :

```text
example.com
```

ton ordinateur doit trouver l'adresse IP correspondante.

Teste avec :

```bash
nslookup example.com
```

Si `nslookup` n'est pas disponible, tu peux utiliser :

```bash
dig example.com
```

Observe l'adresse IP retournée.

### 🔎 Questions

- Quel est le rôle du DNS ?
- Pourquoi utilise-t-on des noms de domaine plutôt que seulement des adresses IP ?
- Quelle adresse IP est associée au domaine interrogé ?

---

# 🏁 Mission finale — Deviens Network Detective

Tu disposes maintenant de plusieurs outils.

Sans regarder les étapes précédentes, essaie de répondre aux questions suivantes :

### 🔍 1. Identité

Trouve :

- ton adresse IP ;
- ton interface réseau ;
- ta passerelle.

Commandes utiles :

```bash
ip addr
ip route
```

### 🔍 2. Communication

Teste :

```bash
ping 127.0.0.1
```

puis ta passerelle.

### 🔍 3. Services

Trouve les ports en écoute :

```bash
ss -tuln
```

### 🔍 4. Serveur

Lance :

```bash
python3 -m http.server 8000
```

Puis vérifie :

```bash
ss -tuln
```

### 🔍 5. Reconnaissance

Utilise :

```bash
nmap -p 8000 127.0.0.1
```

Puis :

```bash
nmap -sV -p 8000 127.0.0.1
```

### 🔍 6. DNS

Interroge :

```bash
nslookup example.com
```

---

# 🧠 Ce que tu viens d'apprendre

Tu as utilisé plusieurs outils fondamentaux de l'administration système et de la cybersécurité :

| Outil | Utilisation |
|---|---|
| `ip` | Informations réseau et routage |
| `ping` | Tester la connectivité |
| `ss` | Observer les ports et services |
| `curl` | Communiquer avec un serveur HTTP |
| Python HTTP Server | Créer un service local |
| `nmap` | Découvrir ports et services |
| `nslookup` / `dig` | Interroger le DNS |

---

# 🎓 Compétences développées

À la fin de ce lab, tu as commencé à pratiquer :

- Linux Networking
- IPv4
- Routage
- TCP / UDP
- Ports réseau
- HTTP
- DNS
- Network Enumeration
- Nmap
- Network Troubleshooting

---

**Welcome to cybersecurity. 🕵️‍♂️🔐**

---

## HACKademy

**HACKademy — Cybersecurity Club**  
École Nationale des Sciences Appliquées d'El Jadida (ENSAJ)

> Learn. Hack. Create
