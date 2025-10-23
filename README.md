# Exemple d’application de chat

Une simple application de démonstration de chat construite avec un **frontend React** et un **backend Node.js**, utilisant le **polling** pour les mises à jour en temps réel au lieu de connexions WebSocket.
Toutes les données sont stockées uniquement en mémoire (aucune base de données requise).

## Architecture

* **Frontend** : Application React exécutée sur le port 3000
* **Backend** : Serveur Express.js exécuté sur le port 3001
* **Communication** : API REST avec mécanisme de polling
* **Stockage** : Tableaux en mémoire (maximum 100 messages)

## Structure du projet

```
chat_app_example/
├── client/                 # Frontend React
│   ├── public/
│   ├── src/
│   │   ├── App.js         # Composant principal du chat
│   │   ├── App.css        # Styles
│   │   ├── index.js       # Point d’entrée React
│   │   └── index.css      # Styles de base
│   └── package.json
├── server/                 # Backend Node.js
│   ├── server.js          # Serveur Express
│   └── package.json
├── package.json           # Fichier principal du projet
└── README.md
```

## Prérequis

* Node.js (version 16 ou supérieure)
* npm

## Démarrage rapide

1. **Cloner et naviguer dans le dossier du projet**

   ```bash
   cd chat_app_example
   ```

2. **Installer toutes les dépendances**

   ```bash
   npm run install-all
   ```

3. **Démarrer l’application**

   ```bash
   npm start
   ```

Cela lancera simultanément le serveur (port 3001) et le client (port 3000).

4. **Ouvrir votre navigateur**
   Accédez à `http://localhost:3001` pour utiliser l’application de chat.

## Points de terminaison de l’API

### GET /api/messages

Récupère tous les messages stockés en mémoire.

**Réponse :**

```json
{
  "success": true,
  "messages": [
    {
      "id": 1,
      "username": "John",
      "message": "Bonjour à tous !",
      "timestamp": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

### POST /api/messages

Envoie un nouveau message.

**Corps de la requête :**

```json
{
  "username": "John",
  "message": "Bonjour à tous !"
}
```

**Réponse :**

```json
{
  "success": true,
  "message": {
    "id": 1,
    "username": "John",
    "message": "Bonjour à tous !",
    "timestamp": "2024-01-15T10:30:00.000Z"
  }
}
```

### GET /api/health

Point de vérification de l’état du serveur.

**Réponse :**

```json
{
  "success": true,
  "message": "Le serveur est en marche",
  "timestamp": "2024-01-15T10:30:00.000Z",
  "totalMessages": 5
}
```

## Fonctionnement du Polling

Le frontend React utilise `setInterval` pour récupérer les messages toutes les 2 secondes :

1. Le composant se monte et récupère immédiatement les messages
2. Un intervalle de polling (2000 ms) est configuré
3. Les messages sont continuellement récupérés en arrière-plan
4. L’interface est mise à jour lorsque de nouveaux messages sont détectés
5. L’intervalle est nettoyé à la désactivation du composant

## Licence

Licence **MIT** — Vous pouvez librement utiliser ce code à des fins d’apprentissage et de développement.
