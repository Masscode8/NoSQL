# Guide Pratique Redis

## Introduction
Redis (Remote Dictionary Server) est un système de gestion de données open-source, in-memory, utilisé comme base de données, cache et message broker.

## Installation et Lancement de Redis

### Installation sur Linux (via WSL pour Windows)
Pour exécuter Redis sur Windows, il est nécessaire d'installer **WSL (Windows Subsystem for Linux)** ou d'utiliser une machine virtuelle. Voici les commandes pour l'installation :

```bash
sudo apt-get update
sudo apt-get install redis
```

### Démarrer Redis
- **Lancer le serveur Redis :**
  ```bash
  redis-server
  ```
- **Ouvrir l'interface de commande :**
  ```bash
  redis-cli
  ```

## 1. Clés et Valeurs
Redis utilise des paires clé-valeur pour le stockage.

### Définir et Récupérer une Valeur
```bash
SET utilisateur "Alice"
GET utilisateur   # Retourne "Alice"
```

### Incrémentation d'une Valeur Numérique
```bash
SET compteur 5
INCR compteur   # Devient 6
```

### Expiration et Suppression
```bash
EXPIRE utilisateur 60   # Expire après 60 secondes
TTL utilisateur         # Temps restant
DEL utilisateur         # Suppression immédiate
```

## 2. Listes (List)
Une liste est une collection ordonnée d'éléments.

### Manipuler les Listes
```bash
RPUSH fruits "pomme" "banane"
LPUSH fruits "orange"

LRANGE fruits 0 -1  # Affiche : orange, pomme, banane
LPOP fruits         # Supprime "orange"
RPOP fruits         # Supprime "banane"
```

## 3. Ensembles (Sets)
Les ensembles sont des collections de valeurs uniques et non ordonnées.

### Manipuler les Ensembles
```bash
SADD langages "Python" "Java"
SMEMBERS langages    # Affiche : Python, Java
SREM langages "Java" # Supprime Java
```

### Opérations sur les Ensembles
```bash
SADD setA "a" "b" "c"
SADD setB "b" "c" "d"
SUNION setA setB    # Fusion : a, b, c, d
```

## 4. Sets Triés (Sorted Sets)
Similaires aux sets mais chaque élément est associé à un score pour un tri automatique.

### Manipuler les Sets Triés
```bash
ZADD scores 100 "Alice" 85 "Bob" 95 "Charlie"

ZRANGE scores 0 -1      # Ordre croissant : Bob, Charlie, Alice
ZREVRANGE scores 0 -1   # Ordre décroissant : Alice, Charlie, Bob
ZRANK scores "Bob"      # Position : 1
```

## 5. Hachages (Hashes)
Les hachages sont des collections clé-valeur similaires aux objets.

### Manipuler les Hachages
```bash
HSET utilisateur:1 nom "Jean" age 30 ville "Paris"
HGET utilisateur:1 nom        # Retourne "Jean"
HGETALL utilisateur:1         # Retourne tous les champs
HINCRBY utilisateur:1 age 5   # Incrémente l'âge : 35
```

## 6. Publication/Abonnement (Pub/Sub)
Redis permet la communication en temps réel via des canaux.

### Publier et S'abonner
```bash
SUBSCRIBE mychannel          # S'abonne à un canal
PUBLISH mychannel "Message" # Envoie un message
```

## 7. Fonctionnalités Avancées

### Transactions
Exécute plusieurs commandes de manière atomique.
```bash
MULTI
SET compte 100
INCRBY compte 50
EXEC
```

### Persistance des Données
Redis peut sauvegarder les données sur disque.
```bash
SAVE    # Synchrone
BGSAVE  # Asynchrone
```

### Verrouillage avec `SETNX`
```bash
SETNX verrou "actif"  # Crée uniquement si elle n'existe pas
```

### Expiration en Millisecondes
```bash
PEXPIRE session 5000  # Expiration après 5000 ms
```

## Conclusion
Redis propose des structures de données variées et performantes pour de nombreux cas d'usage. Ce guide couvre les bases essentielles pour démarrer efficacement avec Redis.

