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
## Exemple de Code pour Arduino : Envoyer et Recevoir des Commandes Texte via Bluetooth

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

  ## Exemple de code pour l'Arduino : reception de commande vocal
Vous pouvez envoyer des commandes textuelles pour allumer une LED, activer un buzzer, ou faire tourner un moteur.

## Matériel Nécessaire
- **Arduino Uno (ou compatible)**
- **Module Bluetooth HC-05/HC-06**
- **LED, Buzzer, Moteur**
- **Câblage**

## Schéma de Connexion
- **VCC du HC-05/HC-06** à **5V de l'Arduino**
- **GND du HC-05/HC-06** à **GND de l'Arduino**
- **TX du HC-05/HC-06** à **RX de l'Arduino (Pin 0)**
- **RX du HC-05/HC-06** à **TX de l'Arduino (Pin 1)**

> **Note :** Déconnectez le module Bluetooth lors du téléchargement du code pour éviter les conflits.

## Code Arduino

```c++
#include <SoftwareSerial.h>

// Définition des broches
const int ledPin = 9;       // Broche de la LED
const int buzzerPin = 10;   // Broche du buzzer
const int motorPin = 11;    // Broche du moteur

// Initialisation de la communication Bluetooth
SoftwareSerial bluetooth(2, 3); // RX, TX

void setup() {
  // Initialisation des broches
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(motorPin, OUTPUT);

  // Démarrage des communications série
  Serial.begin(9600);
  bluetooth.begin(9600);

  Serial.println("Bluetooth est prêt. Envoyez des commandes pour contrôler la LED, le buzzer et le moteur !");
}

void loop() {
  // Vérifie si des données sont disponibles depuis le module Bluetooth
  if (bluetooth.available()) {
    String commandeBluetooth = bluetooth.readStringUntil('\n'); // Lit la commande reçue par Bluetooth
    Serial.print("Reçu via Bluetooth : ");
    Serial.println(commandeBluetooth);

    // Exécute des actions selon la commande reçue
    if (commandeBluetooth == "LED ON") {
      digitalWrite(ledPin, HIGH);  // Allume la LED
      Serial.println("LED allumée");
    } else if (commandeBluetooth == "LED OFF") {
      digitalWrite(ledPin, LOW);   // Éteint la LED
      Serial.println("LED éteinte");
    } else if (commandeBluetooth == "BUZZER ON") {
      digitalWrite(buzzerPin, HIGH); // Allume le buzzer
      Serial.println("Buzzer allumé");
    } else if (commandeBluetooth == "BUZZER OFF") {
      digitalWrite(buzzerPin, LOW);  // Éteint le buzzer
      Serial.println("Buzzer éteint");
    } else if (commandeBluetooth == "MOTOR ON") {
      digitalWrite(motorPin, HIGH);  // Active le moteur
      Serial.println("Moteur en marche");
    } else if (commandeBluetooth == "MOTOR OFF") {
      digitalWrite(motorPin, LOW);   // Arrête le moteur
      Serial.println("Moteur arrêté");
    } else {
      Serial.println("Commande inconnue");
    }
  }
}
```

## Explication du Code

1. **Initialisation :**  
   - Configure les broches pour la LED, le buzzer, et le moteur.
   - Initialise la communication série avec le PC et le module Bluetooth.

2. **Traitement des Commandes :**  
   - **LED ON/OFF :** Allume ou éteint la LED.
   - **BUZZER ON/OFF :** Active ou désactive le buzzer.
   - **MOTOR ON/OFF :** Fait fonctionner ou arrêter le moteur.

3. **Affichage des États :**  
   - Les actions sont affichées sur le moniteur série pour suivi et débogage.

## Conseils
- **Connexion Bluetooth :** Assurez-vous que le module est appairé avec votre appareil avant de commencer.
- **Dépannage :** Vérifiez les connexions et la vitesse de communication (`baud rate`) si des problèmes surviennent.

Avec ce code il vous suffiras de dire les commandes spécifiées sans l'application pour faire réagire l'arduino en conséquence et effectuer la commande que vous avez donner essayez de personaliser ce code pour mieux comprendre et aussi explorer les differentes possibilitées qu offre cette fonctionnalitée.


### Authentification par Mot de Passe

Un système d'authentification par mot de passe avec un clavier virtuel permet de protéger l'accès à certaines fonctionnalités. L'Arduino vérifie le code reçu et affiche "Correct" ou "Entrez le mot de passe" selon la validité du mot de passe.

**Utilisation :**
- Saisissez le mot de passe à l'aide du clavier virtuel pour accéder aux fonctionnalités protégées.

  ## exemple de code arduino : mot de passe
  ## Matériel Nécessaire

- Arduino (Uno, Nano, etc.)
- Module Bluetooth (HC-05, HC-06, etc.)
- LED verte
- LED rouge
- Buzzer
- Résistances pour les LEDs (220Ω à 330Ω)
- Câbles de connexion

##  Schémas de Branchements

- **Module Bluetooth :**
  - TX du module Bluetooth à RX de l'Arduino (broche 2)
  - RX du module Bluetooth à TX de l'Arduino (broche 3)
  - VCC du module Bluetooth à 5V de l'Arduino
  - GND du module Bluetooth à GND de l'Arduino

- **LED Verte :**
  - Anode de la LED verte à la broche 4 de l'Arduino
  - Cathode de la LED verte à GND via une résistance (220Ω à 330Ω)

- **LED Rouge :**
  - Anode de la LED rouge à la broche 5 de l'Arduino
  - Cathode de la LED rouge à GND via une résistance (220Ω à 330Ω)

- **Buzzer :**
  - Broche positive du buzzer à la broche 6 de l'Arduino
  - Broche négative du buzzer à GND

## Code Arduino

```cpp
#include <SoftwareSerial.h>

// Initialisation des broches pour la communication Bluetooth
SoftwareSerial bluetooth(2, 3); // RX, TX

// Définir les broches des LEDs et du buzzer
const int greenLED = 4; // Broche de la LED verte
const int redLED = 5;   // Broche de la LED rouge
const int buzzer = 6;   // Broche du buzzer

// Définir le mot de passe attendu
const String password = "1234"; // Changez ce mot de passe selon vos besoins

void setup() {
  // Démarrage des communications série
  Serial.begin(9600);
  bluetooth.begin(9600);

  // Configuration des broches
  pinMode(greenLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(buzzer, OUTPUT);

  // Éteindre les LEDs et le buzzer au démarrage
  digitalWrite(greenLED, LOW);
  digitalWrite(redLED, LOW);
  digitalWrite(buzzer, LOW);

  Serial.println("Bluetooth est prêt. Envoyez le mot de passe !");
}

void loop() {
  // Vérifie si des données sont disponibles depuis le module Bluetooth
  if (bluetooth.available()) {
    String receivedValue = bluetooth.readStringUntil('\n'); // Lit la chaîne reçue par Bluetooth
    Serial.print("Reçu : ");
    Serial.println(receivedValue);

    // Compare la valeur reçue avec le mot de passe
    if (receivedValue.trim() == password) {
      // Mot de passe correct
      digitalWrite(greenLED, HIGH); // Allume la LED verte
      digitalWrite(redLED, LOW);    // Éteint la LED rouge
      digitalWrite(buzzer, LOW);    // Éteint le buzzer
      bluetooth.println("0");       // Réponse correcte
      Serial.println("Réponse envoyée : 0");
    } else {
      // Mot de passe incorrect
      digitalWrite(greenLED, LOW);  // Éteint la LED verte
      digitalWrite(redLED, HIGH);   // Allume la LED rouge
      digitalWrite(buzzer, HIGH);   // Fait sonner le buzzer
      delay(500);                   // Attend 500 ms pour le buzzer
      digitalWrite(buzzer, LOW);    // Éteint le buzzer
      bluetooth.println("1");       // Réponse incorrecte
      Serial.println("Réponse envoyée : 1");
    }
  }
}
```
## Explication du Code

### Initialisation
- Configure la communication série pour l'Arduino et le module Bluetooth.
- Définit les broches pour les LEDs et le buzzer.

### Vérification du Mot de Passe
- Lit les données envoyées via Bluetooth.
- Compare le mot de passe reçu avec celui stocké.

### Réactions
- **Mot de passe correct :**
  - Allume la LED verte.
  - Éteint la LED rouge et le buzzer.
  - Envoie "0".
- **Mot de passe incorrect :**
  - Allume la LED rouge.
  - Éteint la LED verte.
  - Fait sonner le buzzer pendant 500 ms, puis éteint le buzzer.
  - Envoie "1".


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
