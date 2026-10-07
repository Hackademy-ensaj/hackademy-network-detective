# 🕵️ HACKademy — Network Detective

> **Après avoir appris à enquêter sur un système Linux, il est temps de comprendre comment cette machine communique avec le réseau.**

**Network Detective** est le deuxième laboratoire de la série de labs pratiques proposés par **HACKademy**.

L'objectif est de découvrir progressivement les bases du réseau en utilisant **son propre PC**, sans machine virtuelle.

Tu vas apprendre à identifier ta configuration réseau, tester la connectivité, observer les ports, créer un service web local, utiliser Nmap et comprendre le fonctionnement du DNS.

---

## 🎯 Objectifs

À la fin de ce lab, tu seras capable de :

- identifier l'adresse IP de ta machine ;
- identifier ta passerelle réseau ;
- tester une communication avec `ping` ;
- comprendre les notions de port et de service ;
- afficher les ports en écoute avec `ss` ;
- créer un serveur HTTP local avec Python ;
- communiquer avec ce serveur avec `curl` ;
- utiliser Nmap pour découvrir un port et un service ;
- comprendre le principe de résolution DNS.

---

## 🧰 Prérequis

Ce laboratoire fait suite à **Linux Detective**.

Il est recommandé d'avoir réalisé le premier lab avant de commencer celui-ci.

Tu dois connaître quelques commandes Linux de base :

```bash
pwd
ls
cd
mkdir
cat
```

### 🖥️ Environnement

Le laboratoire peut être réalisé dans les environnements suivants :

- 🐧 Linux natif
- 🪟 Windows avec WSL

Aucune machine virtuelle à installer ou à configurer n'est nécessaire.

> **Note pour WSL :** certaines informations affichées par `ip addr` et `ip route`
> correspondent à l'environnement Linux utilisé par WSL et non directement à la
> carte réseau physique de Windows. Utilise les valeurs affichées par les commandes
> pendant le laboratoire.

---

# 🗺️ Parcours

Le laboratoire est organisé en plusieurs missions.

### 🔍 1. Communication

Découvrir l'adresse `127.0.0.1`, tester sa propre machine avec `ping` et identifier puis tester la passerelle réseau.

👉 [Commencer la mission](missions/01-communication.md)

---

### 🔍 2. Services

Découvrir les ports réseau et les services actuellement en écoute sur la machine avec `ss`.

👉 [Commencer la mission](missions/02-services.md)

---

### 🔍 3. Serveur

Créer un petit serveur HTTP local avec Python, communiquer avec lui et observer le port utilisé.

👉 [Commencer la mission](missions/03-server.md)

---

### 🔍 4. Reconnaissance

Découvrir les premières bases de la reconnaissance réseau avec Nmap en analysant uniquement la machine locale.

👉 [Commencer la mission](missions/04-reconnaissance.md)

---

### 🔍 5. DNS

Comprendre comment un nom de domaine est associé à une adresse IP grâce au DNS.

👉 [Commencer la mission](missions/05-dns.md)

---

# 🧠 Ce que tu vas pratiquer

| Outil / commande | Utilisation |
|---|---|
| `ip` | Consulter la configuration réseau |
| `ping` | Tester la connectivité |
| `ss` | Observer les ports et services |
| `curl` | Communiquer avec un serveur HTTP |
| `python3 -m http.server` | Créer un serveur web local |
| `nmap` | Découvrir des ports et services |
| `nslookup` / `dig` | Interroger le DNS |

---

# 🔐 Règles de sécurité

Ce laboratoire est conçu pour apprendre les bases de la reconnaissance réseau dans un environnement contrôlé.

Pour les premières manipulations avec Nmap, utilise uniquement :

```text
127.0.0.1
```

Il s'agit de ta propre machine.

⚠️ **Ne scanne pas des machines, réseaux ou services qui ne t'appartiennent pas ou pour lesquels tu n'as pas d'autorisation.**

L'objectif du lab est de comprendre les outils et leur fonctionnement dans un environnement sûr.

---

# 🎓 Compétences développées

En réalisant ce lab, tu commenceras à pratiquer :

- Linux Networking
- IPv4
- Routage
- TCP / UDP
- Ports réseau
- Services réseau
- HTTP
- DNS
- Network Enumeration
- Nmap
- Network Troubleshooting

---

# 🏁 Mission finale

À la fin du parcours, tu devras être capable d'expliquer simplement :

> **Comment mon ordinateur se connecte-t-il au réseau ?**

et de répondre à des questions comme :

- Quelle est mon adresse IP ?
- Quelle est ma passerelle ?
- Quels ports sont en écoute ?
- Quel service utilise un port donné ?
- Comment créer un
