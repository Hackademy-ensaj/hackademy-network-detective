# 🔍 Mission 4 — Première reconnaissance avec Nmap

## 🎯 Objectif

Découvrir comment identifier un port ouvert et un service
fonctionnant sur une machine.

## ⚠️ Règle de sécurité

Dans ce laboratoire, nous scannons uniquement :

127.0.0.1

Il s'agit de la machine locale.

## 1. Scanner la machine locale

nmap 127.0.0.1

## 2. Scanner notre serveur

nmap -p 8000 127.0.0.1

## 3. Comprendre le résultat

8000/tcp open ...

Expliquer :

- 8000
- tcp
- open

## 4. Identifier le service

nmap -sV -p 8000 127.0.0.1

## 🧠 Comprendre

Expliquer ce que fait :

-sV

## ❓ Questions

- Que signifie open ?
- Pourquoi le port 8000 est-il ouvert ?
- Pourquoi utilisons-nous 127.0.0.1 ?
- Quelle information supplémentaire apporte -sV ?

## 🧩 Mini-défi

Lance le serveur Python puis utilise Nmap pour vérifier
que le port est ouvert.

Arrête ensuite le serveur et relance Nmap.

Que remarques-tu ?
