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
**Illustration**
# Exemple de Code pour Arduino : Envoyer et Recevoir des Commandes Texte via Bluetooth

## Matériel Nécessaire
- **Arduino Uno (ou autre modèle compatible)**
- **Module Bluetooth HC-05 ou HC-06**
- **Câblage de connexion**

## Schéma de Connexion
- **VCC du HC-05/HC-06** à **5V de l'Arduino**
- **GND du HC-05/HC-06** à **GND de l'Arduino**
- **TX du HC-05/HC-06** à **RX de l'Arduino (Pin 0)**
- **RX du HC-05/HC-06** à **TX de l'Arduino (Pin 1)**

> **Remarque :** Pour éviter des conflits lors du chargement du code, il est recommandé de débrancher le module Bluetooth ou d'utiliser des broches logicielles via la bibliothèque `SoftwareSerial`.

## Code Arduino

```cpp
#include <SoftwareSerial.h>

// Initialisation des broches RX et TX pour la communication Bluetooth
SoftwareSerial bluetooth(2, 3); // RX, TX

void setup() {
  // Démarrage de la communication série avec l'ordinateur et le module Bluetooth
  Serial.begin(9600);
  bluetooth.begin(9600);

  Serial.println("Bluetooth est prêt. Connectez-vous et envoyez des commandes !");
}

void loop() {
  // Vérifie si des données sont disponibles depuis le moniteur série
  if (Serial.available()) {
    String commandePC = Serial.readStringUntil('\n'); // Lit la commande envoyée par le PC
    bluetooth.println(commandePC); // Envoie la commande au module Bluetooth
    Serial.print("Envoyé via Bluetooth : ");
    Serial.println(commandePC);
  }

  // Vérifie si des données sont disponibles depuis le module Bluetooth
  if (bluetooth.available()) {
    String commandeBluetooth = bluetooth.readStringUntil('\n'); // Lit la commande reçue par Bluetooth
    Serial.print("Reçu via Bluetooth : ");
    Serial.println(commandeBluetooth);

    // Exécute des actions selon la commande reçue
    if (commandeBluetooth == "LED ON") {
      // Allumer une LED ou exécuter une action spécifique
      Serial.println("Commande reçue : Allumer la LED");
      // digitalWrite(pinLED, HIGH); // Exemple pour allumer une LED
    } else if (commandeBluetooth == "LED OFF") {
      // Éteindre la LED ou exécuter une autre action
      Serial.println("Commande reçue : Éteindre la LED");
      // digitalWrite(pinLED, LOW); // Exemple pour éteindre une LED
    } else {
      Serial.println("Commande inconnue");
    }
  }
}
```

## Explication du Code

### 1. Initialisation
- Le code utilise la bibliothèque `SoftwareSerial` pour créer une communication série sur les broches 2 (RX) et 3 (TX), libérant ainsi les broches série 0 et 1 pour le téléchargement du code et le moniteur série.
- La vitesse de communication est fixée à 9600 baud, ce qui est une vitesse courante pour les modules Bluetooth HC-05 et HC-06.

### 2. Envoi de Commandes depuis le Moniteur Série
- Si des données sont disponibles depuis le moniteur série de l'Arduino, elles sont lues jusqu'à la fin de la ligne (`\n`) et envoyées au module Bluetooth.

### 3. Réception de Commandes depuis Bluetooth
- Si des données sont disponibles depuis le module Bluetooth, elles sont lues et affichées sur le moniteur série.
- Les commandes reçues peuvent être traitées avec des conditions `if` pour déclencher des actions spécifiques, comme allumer ou éteindre une LED.

## Conseils
- **Connexion Bluetooth :** Assurez-vous que le périphérique Bluetooth de votre téléphone est appairé avec le module HC-05/HC-06 avant d'essayer de communiquer.
- **Dépannage :** Si le code ne fonctionne pas comme prévu, vérifiez les connexions et assurez-vous que les vitesses de communication (`baud rate`) sont identiques entre les dispositifs.

Ce guide vous permettra de démarrer avec l'envoi et la réception de commandes texte via Bluetooth entre votre Arduino et un autre appareil utilisant l'application.

  
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
