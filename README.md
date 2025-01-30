# README : Rapport de TP sur Redis

## Introduction à Redis
Redis (REmote DIctionary Server) est une base de données NoSQL de type clé-valeur, souvent utilisée comme cache, broker de messages ou base de données principale. Redis est en mémoire, ce qui garantit des performances élevées, et prend en charge des structures de données variées comme les chaînes, les listes, les ensembles, les ensembles triés et les tables de hachage.

---

Tout d'abord, on installe redis : 

`sudo apt update`
pour être à jour sur la liste des paquets
`sudo apt install -y redis-server`
pour installer redis

## Commandes de base de Redis

### 1. `redis-server`
**Description :** Cette commande démarre le serveur Redis.

**Exemple :**
```bash
redis-server
```
Une fois le serveur lancé, il écoute par défaut sur le port 6379.

### 2. `redis-cli`
**Description :** Cette commande ouvre le client en ligne de commande pour interagir avec le serveur Redis.

**Exemple :**
```bash
redis-cli
```
Une fois connecté, vous pouvez exécuter des commandes directement dans le shell Redis.

---

## Structures de données et leurs commandes associées

### Chaînes (Strings)
Les chaînes sont la structure de données la plus simple et peuvent contenir du texte ou des nombres.

#### 1. `SET`
**Description :** Associe une clé à une valeur.

**Exemple :**
```bash
SET key "Hello, Redis!"
```

#### 2. `GET`
**Description :** Récupère la valeur associée à une clé.

**Exemple :**
```bash
GET key
```
**Résultat :**
```
"Hello, Redis!"
```

#### 3. `INCR`
**Description :** Incrémente la valeur numérique d’une clé.

**Exemple :**
```bash
SET counter 1
INCR counter
GET counter
```
**Résultat :**
```
2
```

#### 4. `EXPIRE` et `TTL`
- **`EXPIRE` :** Définit une durée d'expiration pour une clé (en secondes).
- **`TTL` :** Récupère le temps restant avant l'expiration d'une clé.

**Exemple :**
```bash
SET temp "temporary"
EXPIRE temp 10
TTL temp
```

#### 5. `DEL`
**Description :** Supprime une clé.

**Exemple :**
```bash
DEL key
```

---

### Listes (Lists)
Les listes sont des collections ordonnées de chaînes.

#### 1. `RPUSH` et `LPUSH`
- **`RPUSH` :** Ajoute un élément à la fin de la liste.
- **`LPUSH` :** Ajoute un élément au début de la liste.

**Exemple :**
```bash
RPUSH mylist "A"
LPUSH mylist "B"
LRANGE mylist 0 -1
```
**Résultat :**
```
1) "B"
2) "A"
```

#### 2. `LRANGE`
**Description :** Récupère une plage d’éléments dans une liste.

#### 3. `LPOP` et `RPOP`
- **`LPOP` :** Retire le premier élément de la liste.
- **`RPOP` :** Retire le dernier élément.

---

### Ensembles (Sets)
Les ensembles sont des collections non ordonnées de chaînes uniques.

#### 1. `SADD`
**Description :** Ajoute un ou plusieurs éléments à un ensemble.

**Exemple :**
```bash
SADD myset "A" "B" "C"
```

#### 2. `SMEMBERS`
**Description :** Récupère tous les éléments d’un ensemble.

#### 3. `SREM`
**Description :** Supprime un élément d'un ensemble.

#### 4. `SUNION`
**Description :** Récupère l'union de plusieurs ensembles.

---

### Ensembles triés (Sorted Sets)
Les ensembles triés associent chaque élément à un score, permettant un tri par ordre croissant ou décroissant.

#### 1. `ZADD`
**Description :** Ajoute un élément avec un score.

#### 2. `ZRANGE` et `ZREVRANGE`
- **`ZRANGE` :** Récupère les éléments par ordre croissant.
- **`ZREVRANGE` :** Par ordre décroissant.

#### 3. `ZRANK`
**Description :** Retourne le rang d'un élément.

---

### Tables de hachage (Hashes)
Les tables de hachage stockent des paires clé-valeur dans une clé principale.

#### 1. `HSET` et `HMSET`
- **`HSET` :** Définit un champ dans une table de hachage.
- **`HMSET` :** Définit plusieurs champs.

#### 2. `HGETALL`
**Description :** Récupère tous les champs et valeurs.

#### 3. `HINCRBY`
**Description :** Incrémente un champ numérique dans un hachage.

---

### Publication/Abonnement (Pub/Sub)
Redis permet la communication en temps réel via des canaux de publication et d'abonnement.

#### 1. `SUBSCRIBE` et `PSUBSCRIBE`
- **`SUBSCRIBE` :** S'abonne à un canal spécifique.
- **`PSUBSCRIBE` :** S'abonne avec un motif.

#### 2. `PUBLISH`
**Description :** Publie un message sur un canal.

**Exemple :**
```bash
PUBLISH mychannel "Hello, subscribers!"
```

---

## Conclusion
Redis est une solution puissante et polyvalente pour la gestion des données en mémoire. Les commandes explorées dans ce TP offrent une base solide pour manipuler les structures de données et tirer parti des capacités de Redis dans divers scénarios.

