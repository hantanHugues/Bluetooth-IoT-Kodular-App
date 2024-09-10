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
3. [conception de l'application](#conception-de-l'application)
4. [À Propos du Concepteur](#à-propos-du-concepteur)

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
## Contrôle d'une Voiture à Moteurs avec Arduino et Bluetooth

## Composants Nécessaires

- **Arduino** (UNO, Nano, etc.)
- **Module Bluetooth** (HC-05 ou HC-06)
- **Pont en H** (L298N) pour contrôler les moteurs
- **Moteurs DC** (2 ou 4 selon votre configuration)
- **Alimentation** pour les moteurs (batterie)
- **Câblage** pour les connexions

## Branchement des Moteurs

- **Moteurs** : Connectez les moteurs aux sorties du module L298N.
- **Alimentation** : Connectez l'alimentation des moteurs à l'entrée du L298N (Vcc et GND).
- **Contrôle des Moteurs** : Connectez les broches de contrôle du L298N à l'Arduino pour chaque moteur (IN1, IN2, IN3, IN4).

  ## code arduino
  ```Cpp
   #include <SoftwareSerial.h>
    Créer une instance de SoftwareSerial pour le module Bluetooth
   SoftwareSerial bluetoothSerial(2, 3); // RX, TX

   // Définir les broches de contrôle des moteurs
   const int motor1Pin1 = 8; // IN1 sur le L298N
   const int motor1Pin2 = 9; // IN2 sur le L298N
   const int motor2Pin1 = 10; // IN3 sur le L298N
   const int motor2Pin2 = 11; // IN4 sur le L298N

   void setup() {
   Serial.begin(9600); // Initialiser la communication série avec le moniteur série
     bluetoothSerial.begin(9600); // Initialiser la communication série avec le module Bluetooth
     Serial.println("Prêt à recevoir des données Bluetooth...");
      pinMode(motor1Pin1, OUTPUT);
     pinMode(motor1Pin2, OUTPUT);
      pinMode(motor2Pin1, OUTPUT);
     pinMode(motor2Pin2, OUTPUT);
   }

   void loop() {
     // Vérifier si des données sont disponibles à lire depuis le Bluetooth
     if (bluetoothSerial.available()) {
       char receivedChar = bluetoothSerial.read(); // Lire un caractère
       Serial.print("Reçu : ");
       Serial.println(receivedChar);
        // Commande pour avancer
       if (receivedChar == 'A') {
         avancer();
       }
       // Commande pour reculer
       else if (receivedChar == 'R') {
         reculer();
       }
       // Commande pour tourner à gauche
       else if (receivedChar == 'G') {
         tournerGauche();
       }
       // Commande pour tourner à droite
       else if (receivedChar == 'D') {
         tournerDroite();
       }
       // Commande pour s'arrêter
       else if (receivedChar == 'S') {
         arreter();
       } 
       receivedChar = 0;// Afficher le caractère reçu sur le moniteur série
     }
   }
   // Fonction pour avancer
   void avancer() {
     digitalWrite(motor1Pin1, HIGH);
     digitalWrite(motor1Pin2, LOW);
     digitalWrite(motor2Pin1, HIGH);
     digitalWrite(motor2Pin2, LOW);
     Serial.println("Avancer");
   }

   // Fonction pour reculer
   void reculer() {
     digitalWrite(motor1Pin1, LOW);
     digitalWrite(motor1Pin2, HIGH);
     digitalWrite(motor2Pin1, LOW);
     digitalWrite(motor2Pin2, HIGH);
     Serial.println("Reculer");
   }

   // Fonction pour tourner à gauche
   void tournerGauche() {
    digitalWrite(motor1Pin1, LOW);
     digitalWrite(motor1Pin2, HIGH);
     digitalWrite(motor2Pin1, HIGH);
     digitalWrite(motor2Pin2, LOW);
     Serial.println("Gauche");
   }

   // Fonction pour tourner à droite
   void tournerDroite() {
     digitalWrite(motor1Pin1, HIGH);
     digitalWrite(motor1Pin2, LOW);
     digitalWrite(motor2Pin1, LOW);
     digitalWrite(motor2Pin2, HIGH);
     Serial.println("Droite");
   }

   // Fonction pour s'arrêter
   void arreter() {
     digitalWrite(motor1Pin1, LOW);
     digitalWrite(motor1Pin2, LOW);
     digitalWrite(motor2Pin1, LOW);
     digitalWrite(motor2Pin2, LOW);
     Serial.println("Arrêté");
      }
  

## Fonctionnement du Code

- **Initialisation** :
  - Les broches pour contrôler les moteurs sont définies et configurées comme sorties.
  - La communication série est initialisée pour le module Bluetooth et le moniteur série.

- **Boucle Principale (`loop`)** :
  - Vérifie si des données sont disponibles via Bluetooth.
  - Lit chaque commande (`A`, `R`, `G`, `D`, `S`) et appelle la fonction correspondante pour contrôler les moteurs.

- **Fonctions de Contrôle** :
  - **`avancer()`** : Active les moteurs pour avancer.
  - **`reculer()`** : Active les moteurs pour reculer.
  - **`tournerGauche()`** et **`tournerDroite()`** : Contrôle les moteurs pour tourner à gauche ou à droite.
  - **`arreter()`** : Arrête tous les moteurs.

## Tests et Vérifications

1. **Tester chaque commande individuellement** pour s'assurer que les moteurs répondent correctement.
2. **Vérifier les connexions des broches** entre l'Arduino, le L298N, et les moteurs pour s'assurer qu'elles sont correctes.
3. **Vérifier l'alimentation des moteurs** pour éviter les baisses de tension et les comportements inattendus.
.

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

  
## Conception de l'application
## Fonctionnalités de l'Application

### 1. **Chat Bluetooth avec Arduino**

**Description :**  
Cette fonctionnalité permet une communication bidirectionnelle entre l'Arduino et votre téléphone via Bluetooth. Vous pouvez envoyer des commandes à l'Arduino et recevoir des réponses en temps réel.

**Conception :**  
- **Kodular Utilisé :** Utilisation du composant BluetoothClient pour gérer la communication Bluetooth.
- **Écran :** Créez un écran avec des boutons pour envoyer des commandes et une zone de texte pour afficher les réponses .
- **Logique :** Implémentez des blocs pour envoyer des données via Bluetooth lorsqu'un bouton est pressé et recevoir des réponses à afficher dans la zone de texte.

  **Image de l'interface**

### 2. **Contrôle à Distance via Joystick Analogique**

**Description :**  
Permet de contrôler des appareils à distance en utilisant un joystick analogique. Les coordonnées de déplacement sont envoyées au microcontrôleur, permettant un contrôle précis.

**Conception :**  
- **Kodular Utilisé :** Utilisation du composant Canvas pour afficher le joystick et récupérer les coordonnées.
- **Écran :** Créez un écran avec un composant Canvas pour le joystick et un autre pour afficher les données de contrôle.
- **Logique :** Utilisez des blocs pour lire les coordonnées du joystick et envoyer ces données via Bluetooth au microcontrôleur.

### 3. **Lecture de Données en Temps Réel**

**Description :**  
Cette fonctionnalité permet de lire et d'afficher les données envoyées par le microcontrôleur en temps réel, comme les valeurs des capteurs.

**Conception :**  
- **Kodular Utilisé :** Utilisation du composant BluetoothClient pour recevoir les données et du composant Label pour afficher les données.
- **Écran :** Créez un écran avec des composants Label pour afficher les données.
- **Logique :** Utilisez des blocs pour recevoir les données via Bluetooth et mettre à jour les labels en temps réel avec ces données.

**Image de l'interface**

### 4. **Commandes Vocales**

**Description :**  
Permet de contrôler l'application en envoyant des commandes vocales via la reconnaissance vocale de Google.

**Conception :**  
- **Kodular Utilisé :** Utilisation du composant SpeechRecognizer pour capter les commandes vocales.
- **Écran :** Créez un écran avec un bouton pour activer la reconnaissance vocale et un Label pour afficher les commandes reconnues.
- **Logique :** Utilisez des blocs pour démarrer la reconnaissance vocale lorsqu'un bouton est pressé, puis envoyer les commandes reconnues via Bluetooth à l'Arduino.
- 

### 5. **Authentification par Mot de Passe**

**Description :**  
Un système d'authentification qui vérifie le mot de passe saisi et renvoie une confirmation basée sur la validité du mot de passe.

**Conception :**  
- **Kodular Utilisé :** Utilisation du composant TextBox pour saisir le mot de passe et du composant Button pour soumettre.
- **Écran :** Créez un écran avec un TextBox pour saisir le mot de passe, un Button pour soumettre et un Label pour afficher les résultats de la vérification.
- **Logique :** Utilisez des blocs pour comparer le mot de passe saisi avec le mot de passe attendu, puis envoyer le résultat via Bluetooth à l'Arduino. Affichez le message de résultat dans le Label.

  **Image de l'interface**

### 6. **Gestion de la Connexion Bluetooth**

**Description :**  
Facilite la connexion et la déconnexion avec les appareils Bluetooth.

**Conception :**  
- **Kodular Utilisé :** Utilisation des composants BluetoothClient et ListPicker pour gérer les connexions.
- **Écran :** Créez un écran avec des boutons pour se connecter et se déconnecter, et un ListPicker pour sélectionner les appareils disponibles.
- **Logique :** Utilisez des blocs pour afficher la liste des appareils disponibles et se connecter ou se déconnecter selon l'action de l'utilisateur.

  **image de l'interface**


Il me serais malheuresement difficile d'expliquer le fonctionnement de chaque chose, surtout la logique derrière chaque fonctionnement de manière clair vu que c'est très complexe. Pour les plus passionnés qui désirent s'inspirer de mon travail pour faire leur propre application je laisserai les fichier de designer pour les screen et de blocs pour la logique de mon projet pour mieux comprendre le fonctionnement de chaque bloc. Je vous pmettrai mes sources pour les differents fonctionnements dont les plus complex comme le joystick. 
Merci. 

**Image des blocs**
en annlysant les blocs de logiques  utilisées vous pourez mieux avoir une idée des composants utilisées pour les screen.



## À Propos du Concepteur

Cette application marque le début d'un projet IoT ambitieux développé avec passion grâce à Kodular. Bien que cette première version présente encore des opportunités d'amélioration, elle a été conçue pour répondre à vos besoins en matière de contrôle et de gestion d'appareils connectés.
Il m'a été difficile de trouver des cours et videos tuto pour me guider dans mon projet j'ai donc eu l'idée de le mettre sur un depot git en espérant que cela puisse aider. 

Pour toute question ou retour, n'hésitez pas à me contacter....


## Source et reference
[Kodular community 1](https://community.kodular.io/t/how-to-create-a-joystick-with-the-canvas-component/58129)
[Koduar community](https://community.kodular.io/t/advanced-joystick-controls-in-kodular/155580)
[youtube](https://www.youtube.com/watch?v=RM0G7q-G6bo)
[documentation](https://docs.kodular.io/)
