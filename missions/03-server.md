# 🔍 Mission 3 — Créer un serveur web local

## 🎯 Objectif

Créer un petit serveur HTTP sur son propre ordinateur et observer
le port utilisé par ce serveur.

## 1. Créer le dossier

mkdir network-detective
cd network-detective

## 2. Créer une page

echo "HACKademy Network Detective" > index.html

## 3. Lancer le serveur

python3 -m http.server 8000

### Que se passe-t-il ?

...

## 4. Tester avec curl

Dans un deuxième terminal :

curl http://127.0.0.1:8000

## 5. Tester avec le navigateur

http://127.0.0.1:8000

## 6. Observer le port

ss -tuln

Cherche :

8000

## 🧠 Comprendre

Expliquer :

PC → serveur Python → port 8000 → requête HTTP

## ❓ Questions

- Quel port avons-nous utilisé ?
- Quel protocole ?
- Que fait curl ?
- Pourquoi le serveur doit-il rester lancé ?

.
