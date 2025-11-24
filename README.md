# 🤖 SERVI-BOT

![Status](https://img.shields.io/badge/Status-En%20Développement-blue)
![Version](https://img.shields.io/badge/Version-1.0-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

> **Système de Service Robotisé pour la Restauration** - Une solution innovante pour fluidifier le service restaurant et améliorer l'expérience client

## 📋 Table des Matières

- [À Propos](#-à-propos)
- [Problématique](#-problématique)
- [Architecture du Système](#️-architecture-du-système)
- [Workflow](#-workflow)
- [Technologies Utilisées](#-technologies-utilisées)
- [Caractéristiques Techniques](#-caractéristiques-techniques)
- [Installation](#-installation)
- [Équipe](#-équipe)
- [Licence](#-licence)

## 🎯 À Propos

**SERVI-BOT** est un système robotisé intelligent conçu pour automatiser la livraison des commandes dans les restaurants. Il combine une interface de commande web, un dashboard de gestion en cuisine et un robot autonome de livraison.

### Objectifs Principaux

- ✅ Fluidifier le service entre la table et la cuisine
- ✅ Réduire les erreurs de commande
- ✅ Améliorer l'expérience client pendant les pics d'affluence
- ✅ Permettre au personnel de se concentrer sur des tâches à haute valeur ajoutée

## 🎯 Problématique

Les restaurants font face à plusieurs défis :
- Gestion difficile pendant les pics d'affluence
- Erreurs fréquentes dans les commandes
- Temps d'attente prolongés
- Personnel surchargé

**SERVI-BOT** apporte une solution complète et automatisée à ces problèmes.

## 🏗️ Architecture du Système

Le système repose sur **3 modules interconnectés** :

### 1️⃣ Interface Client (Application Web)

```
📱 Accès : QR Code unique par table
🍽️ Menu : Consultation et sélection interactive
🛒 Panier : Constitution de la commande
💳 Paiement : Intégration Kkiapay (Mobile Money)
🔐 Sécurité : Code unique 4 chiffres généré après paiement
```

**Technologies** : HTML5, CSS3, JavaScript, ESP32 Web Server

### 2️⃣ Dashboard Cuisine (Interface de Gestion)

```
📱 Support : Tablette ou écran tactile
📡 Connexion : WiFi (Mode AP via ESP32)
🔄 Réception : Commandes en temps réel
📊 Gestion : Suivi de l'état des commandes
✅ Contrôle : Lancement des livraisons
```

**Hébergement** : Local sur ESP32

### 3️⃣ Robot de Livraison (Unité Robotique)

```
🧠 Contrôle : ESP32 (WiFi/BT natif)
⚙️ Déplacement : Moteurs DC + Encodeurs
🔒 Casiers : 4-5 casiers avec gâchettes électromécaniques
🔢 Interface : Clavier matriciel 4x4
👁️ Navigation : Capteurs IR (suivi de ligne)
📏 Précision : Odométrie (encodeurs moteurs)
📡 Sécurité : Capteurs ultrasons HC-SR04
```

## 🔄 Workflow

### Phase 1 : Prise de Commande & Paiement

1. 📱 Le client **scanne le QR code** sur sa table
2. 🍽️ Navigation sur le **menu interactif**
3. 🛒 Sélection des plats et validation du panier
4. 💳 **Paiement sécurisé** via Kkiapay API
5. 🔐 Génération du **code unique à 4 chiffres**

### Phase 2 : Préparation

1. 📊 La commande apparaît sur le **Dashboard Cuisine**
2. 🍳 Le cuisinier **prépare** les plats
3. ✅ Mise à jour du statut : **"Prête"**

### Phase 3 : Expédition & Navigation

1. 📦 Placement de la commande dans un **casier du robot**
2. 🔒 **Verrouillage automatique** du casier
3. 🚀 Lancement de la livraison : **"Table N"**
4. 🛤️ **Navigation intelligente** :
   - Suivi de ligne tracée au sol (capteurs IR)
   - Calcul précis de distance (odométrie)
   - Arrêt automatique à la table cible
5. 🚧 **Évitement d'obstacles** en temps réel

### Phase 4 : Réception Sécurisée

1. 🛑 Le robot s'immobilise à la **table cible**
2. 🔢 Le client saisit son **code à 4 chiffres**
3. 🔐 **Système de sécurité** :
   - ✅ Code correct → Déverrouillage + Bip de validation
   - ❌ Code incorrect → Message d'erreur (2 tentatives)
   - 🚨 3ème échec → Buzzer + Alerte Dashboard
4. 📦 **Récupération** de la commande
5. ⏱️ **Expiration** : Code expire 5 secondes après fermeture
6. 🔙 **Retour automatique** à la cuisine

## 🛠️ Technologies Utilisées

### Hardware

| Composant | Modèle | Rôle |
|-----------|--------|------|
| **Microcontrôleur** | ESP32 | Unité de contrôle, serveur web, gestion WiFi |
| **Moteurs** | DC avec encodeurs | Déplacement précis et odométrie |
| **Actionneurs** | Gâchettes électromécaniques | Verrouillage sécurisé des casiers |
| **Interface Utilisateur** | Clavier matriciel 4x4 | Authentification client |
| **Capteurs Obstacles** | HC-SR04 (Ultrasons) | Détection et évitement |
| **Capteurs Navigation** | Infrarouge (IR) | Suivi de ligne au sol |

### Software

- **Frontend** : HTML5, CSS3, JavaScript
- **Backend** : ESP32 Web Server (Mode AP)
- **Communication** : WiFi (HTTP)
- **Paiement** : Kkiapay API
- **Protocole** : HTTP RESTful

## ⚙️ Caractéristiques Techniques

### Communication Inter-Modules

```
Client ←→ ESP32 (Robot) ←→ Dashboard Cuisine
        ↓
    Mode AP WiFi
    Protocole HTTP
```

### Navigation Précise

- **Méthode** : Suivi de ligne + Odométrie
- **Précision** : ±5 cm
- **Exemples de distances** :
  - Table 4 : 2.50 m
  - Table 7 : 6.00 m

### Système de Sécurité

🔐 **Multi-niveaux** :
- Code unique 4 chiffres généré dynamiquement
- Expiration rapide (5 secondes après fermeture)
- Limite de 3 tentatives
- Alertes sonores (Buzzer) et visuelles (Dashboard)
- Verrouillage mécanique des casiers
- Détection d'obstacles en temps réel

## 📦 Installation

### Prérequis

```bash
- ESP32 Development Board
- Arduino IDE ou PlatformIO
- Moteurs DC avec encodeurs
- Capteurs HC-SR04 et IR
- Clavier matriciel 4x4
- Gâchettes électromécaniques
```

### Configuration ESP32

1. **Cloner le repository**
```bash
git clone https://github.com/votre-username/servi-bot.git
cd servi-bot
```

2. **Installer les bibliothèques requises**
```cpp
// Dans Arduino IDE
- WiFi.h
- WebServer.h
- ESP32Servo.h
- Keypad.h
```

3. **Configurer les paramètres WiFi**
```cpp
const char* ssid = "SERVI-BOT-AP";
const char* password = "votre_mot_de_passe";
```

4. **Uploader le code sur l'ESP32**

5. **Tester la connexion**
   - Connectez-vous au réseau WiFi créé par l'ESP32
   - Accédez à l'IP du robot dans votre navigateur

## 👥 Équipe

| Rôle | Nom |
|------|-----|
| **Chef de Projet** | Max Hounkpatin |
| **Développeur** | Loïc Zannou |
| **Développeur** | TAIROU Naoufal |
| **Superviseur** | Mr. DJOHOU Carmel |

## 📅 Timeline

- **Conception** : Octobre 2025
- **Prototypage** : Novembre 2025
- **Tests** : Décembre 2025
- **Déploiement** : Janvier 2026

## 🎥 Démonstration

> 🚧 Vidéo de démonstration à venir

## 📸 Captures d'Écran

> 🚧 Screenshots à venir

## 🤝 Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Forkez le projet
2. Créez une branche (`git checkout -b feature/AmazingFeature`)
3. Committez vos changements (`git commit -m 'Add AmazingFeature'`)
4. Pushez vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## 📝 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 📧 Contact

**Max Hounkpatin (Max_Adis)**
- GitHub: [@votre-username](https://github.com/Max_Adis)
- Email: maxhounkpatin001@gmail..com

## 🙏 Remerciements

- Mr. DJOHOU Carmel pour son encadrement
- L'équipe de développement pour leur dévouement
- La communauté ESP32 pour leurs ressources

---

<div align="center">

**⭐ Si ce projet vous plaît, n'hésitez pas à lui donner une étoile ! ⭐**

Made with ❤️ by Team SERVI-BOT

</div>
