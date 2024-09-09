# Bluetooth-IoT-Kodular-App
# Documentation de l'Application IoT

## Introduction

Bienvenue dans la documentation de l'application IoT développée avec Kodular. Cette application est conçue pour faciliter les interactions avec des appareils via Bluetooth. Elle permet l'envoi et la réception de commandes, l'affichage de données en temps réel, et le contrôle à distance de divers appareils.

## Table des Matières

1. [Fonctionnalités Principales](#fonctionnalités-principales)
   - [Chat Bluetooth avec Arduino](#chat-bluetooth-avec-arduino)
   - [Contrôle à Distance via Joystick Analogique](#contrôle-à-distance-via-joystick-analogique)
   - [Lecture de Données en Temps Réel](#lecture-de-données-en-temps-réel)
   - [Commandes Vocales](#commandes-vocales)
   - [Authentification par Mot de Passe](#authentification-par-mot-de-passe)
   - [Gestion de la Connexion Bluetooth](#gestion-de-la-connexion-bluetooth)
2. [Conseils pour Résoudre les Problèmes](#conseils-pour-résoudre-les-problèmes)
3. [À Propos du Concepteur](#à-propos-du-concepteur)

## Fonctionnalités Principales

### Chat Bluetooth avec Arduino

L'application propose une fonctionnalité de chat bidirectionnelle permettant de communiquer entre le moniteur série de l'Arduino et votre téléphone. Cette fonctionnalité est utile pour envoyer des commandes à l'Arduino et afficher les réponses sous forme de messages reçus. Elle facilite le diagnostic et l'interaction en temps réel.

**Utilisation :**
- Connectez votre téléphone à l'Arduino via Bluetooth.
- Envoyez des commandes et recevez des réponses directement sur l'interface de l'application.

### Contrôle à Distance via Joystick Analogique

Le joystick analogique intégré permet de contrôler des appareils à distance avec une grande précision. Les coordonnées de déplacement sont envoyées au microcontrôleur pour une réponse adéquate.

**Exemple de code :**
- Des exemples pour tester cette fonctionnalité avec un Arduino Uno sont disponibles sur mon GitHub.

### Lecture de Données en Temps Réel

Cette fonctionnalité permet de lire et d'afficher les données envoyées par le microcontrôleur, comme les valeurs des capteurs, directement depuis la page du joystick.

**Utilisation :**
- Accédez à la page du joystick pour voir les données en temps réel.

### Commandes Vocales

L'application intègre la reconnaissance vocale de Google pour envoyer des commandes vocales à l'Arduino. Cette fonctionnalité simplifie le contrôle de vos appareils par la voix.

**Utilisation :**
- Activez la reconnaissance vocale et prononcez vos commandes pour interagir avec l'Arduino.

### Authentification par Mot de Passe

Un système d'authentification par mot de passe avec un clavier virtuel permet de protéger l'accès à certaines fonctionnalités. L'Arduino vérifie le code reçu et affiche "Correct" ou "Incorrect" selon la validité du mot de passe.

**Utilisation :**
- Saisissez le mot de passe à l'aide du clavier virtuel pour accéder aux fonctionnalités protégées.

### Gestion de la Connexion Bluetooth

Des boutons pour afficher la liste des appareils disponibles et pour se déconnecter sont disponibles sur la page de connexion. Pour une connexion stable, assurez-vous que le Bluetooth est activé avant d'entrer dans l'application et connectez-vous au moins une fois à l'appareil cible via le gestionnaire Bluetooth de votre téléphone.

**Conseils :**
- Redémarrez le Bluetooth et l'application en cas de problème de connexion.

## Conseils pour Résoudre les Problèmes

- **Connexion Bluetooth :** Si l'appareil cible ne s'affiche pas, redémarrez le Bluetooth et l'application.
- **Passage entre Fonctions :** Déconnectez-vous avant de changer de fonctionnalité et reconnectez-vous après avoir redémarré le Bluetooth.
- **Redémarrage :** Redémarrez l'application avant de vous connecter à un nouvel appareil.

## À Propos du Concepteur

Cette application marque le début d'un projet IoT ambitieux développé avec passion grâce à Kodular. Bien que cette première version présente encore des opportunités d'amélioration, elle a été conçue pour répondre à vos besoins en matière de contrôle et de gestion d'appareils connectés.

Pour toute question ou retour, n'hésitez pas à me contacter.
