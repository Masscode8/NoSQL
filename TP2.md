# Guide MongoDB : Base de Données `lesfilms`

## 1. Installation de MongoDB sur WSL
Pour installer MongoDB sur WSL (Windows Subsystem for Linux) :

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt update
sudo apt install -y mongodb-org
```

## 2. Démarrer MongoDB sur WSL
- **Démarrer MongoDB :**
```bash
sudo systemctl start mongod
```
- **Activer le démarrage automatique :**
```bash
sudo systemctl enable mongod
```

## 3. Importer une Collection de Films
Pour importer un fichier JSON dans la base `lesfilms` :

```bash
mongoimport --db lesfilms --collection films --file films.json --jsonArray
```

## 4. Vérifier l'Importation
- **Compter les documents :**
```bash
db.films.countDocuments()
```
- **Afficher un document :**
```bash
db.films.findOne()
```

## 5. Requêtes MongoDB sur la Collection `films`

### 6. Afficher tous les films d'Action
```bash
db.films.find({ genre: "Action" })
```

### 7. Compter le nombre de films d'Action
```bash
db.films.countDocuments({ genre: "Action" })
```

### 8. Afficher les films d'Action produits en France
```bash
db.films.find({ genre: "Action", country: "FR" })
```

### 9. Afficher les films d'Action produits en France en 1963
```bash
db.films.find({ genre: "Action", country: "FR", year: 1963 })
```

### 10. Afficher les titres et les grades des films d'Action réalisés en France
```bash
db.films.find(
  { genre: "Action", country: "FR" },
  { _id: 0, title: 1, grades: 1 }
)
```

### 11. Afficher les films d'Action réalisés en France avec au moins une note > 10
```bash
db.films.find(
  { genre: "Action", country: "FR", "grades.note": { $gt: 10 } },
  { _id: 0, title: 1, grades: 1 }
)
```

### 12. Afficher les films d'Action réalisés en France ayant uniquement des notes > 10
```bash
db.films.find(
  { genre: "Action", country: "FR", grades: { $not: { $elemMatch: { note: { $lte: 10 } } } } },
  { _id: 0, title: 1, grades: 1 }
)
```

### 13. Afficher les différents genres de la base `lesfilms`
```bash
db.films.distinct("genre")
```

### 14. Afficher les différents grades attribués
```bash
db.films.distinct("grades.grade")
```

### 15. Afficher tous les films avec au moins un des artistes suivants : `artist:4`, `artist:18`, `artist:11`
```bash
db.films.find(
  { "actors": { $in: ["artist:4", "artist:18", "artist:11"] } },
  { _id: 0, title: 1, actors: 1 }
)
```

### 16. Afficher tous les films qui n'ont pas de résumé
```bash
db.films.find(
  { "resume": { $exists: false } },
  { _id: 0, title: 1 }
)
```

### 17. Afficher tous les films avec Leonardo DiCaprio en 1997
```bash
db.films.find(
  { "actors.last_name": "DiCaprio", "actors.first_name": "Leonardo", year: 1997 },
  { _id: 0, title: 1, actors: 1, year: 1 }
)
```

## Conclusion
Ce guide regroupe les principales commandes MongoDB pour explorer et interagir avec la base `lesfilms`. Adaptez-les selon vos besoins.

