# 📡 LAB-18 | BroadcastReceiver-AirplaneMode
Une application Android démontrant l'utilisation des **BroadcastReceivers** pour écouter des événements système, illustrée avec la détection du **mode avion**, un broadcast personnalisé et un receiver au démarrage du téléphone.

---

## ✨ Fonctionnalités

- 📡 **Receiver dynamique** : écoute les changements du mode avion en temps réel
- 🔄 **Activation/Désactivation** du receiver depuis l'interface
- 📣 **Custom Broadcast** : envoi et réception d'un broadcast intra-application
- 🔔 **Receiver statique** : détection du démarrage du téléphone (`BOOT_COMPLETED`)
- 💬 **Feedback Toast** à chaque événement reçu

---

## ⚠️ Limitation Android importante

> Android **interdit** aux applications tierces de modifier le mode avion depuis le code (depuis Android 4.2).
> Ce droit est réservé aux applications système signées avec la clé constructeur.

L'application **écoute** uniquement le changement de mode avion — l'utilisateur doit l'activer/désactiver manuellement depuis les **Paramètres du téléphone**.

---

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Langage | Java |
| UI | XML Layouts |
| Receivers | BroadcastReceiver (dynamique + statique) |
| Événement système | `Intent.ACTION_AIRPLANE_MODE_CHANGED` |
| Démarrage système | `Intent.ACTION_BOOT_COMPLETED` |
| Broadcast custom | `sendBroadcast()` + `IntentFilter` |
| UI Components | TextView, Button, Toast |

---

## 📁 Architecture du projet

```bash
com.example.receiverdemo
├── MainActivity.java              # Interface utilisateur + gestion des receivers
├── AirplaneModeReceiver.java      # Receiver dynamique : détecte le mode avion
├── CustomEventReceiver.java       # Receiver : écoute un broadcast personnalisé
├── BootReceiver.java              # Receiver statique : détecte le boot du téléphone
└── res/layout/
    └── activity_main.xml          # Layout principal
```

---

## 🧠 Concepts Android abordés

- 📌 `BroadcastReceiver` dynamique (`registerReceiver` / `unregisterReceiver`)
- 📌 `BroadcastReceiver` statique (déclaré dans le `AndroidManifest.xml`)
- 📌 `IntentFilter` et actions système
- 📌 `sendBroadcast()` pour les broadcasts personnalisés
- 📌 `Intent.ACTION_AIRPLANE_MODE_CHANGED`
- 📌 `Intent.ACTION_BOOT_COMPLETED`
- 📌 Gestion du cycle de vie (`onDestroy`) pour éviter les fuites mémoire
- 📌 Limitations de sécurité Android (permissions système)

---

## 🔄 Fonctionnement

### Receiver Mode Avion (dynamique)
1. L'utilisateur clique sur **Activer Receiver Avion**
2. L'app enregistre dynamiquement `AirplaneModeReceiver` avec `registerReceiver()`
3. L'utilisateur active/désactive le mode avion depuis les **Paramètres Android**
4. Le receiver reçoit le broadcast et affiche un Toast
5. Un clic sur **Désactiver Receiver Avion** désenregistre le receiver

### Custom Broadcast
1. L'utilisateur clique sur **Envoyer Broadcast**
2. `MainActivity` envoie un `Intent` avec l'action `CUSTOM_EVENT`
3. `CustomEventReceiver` reçoit l'intent et affiche le message via Toast

### Boot Receiver (statique)
1. Déclaré dans le `AndroidManifest.xml` avec l'action `BOOT_COMPLETED`
2. Se déclenche automatiquement au démarrage du téléphone
3. Affiche un Toast de confirmation (nécessite la permission `RECEIVE_BOOT_COMPLETED`)

---

## 📱 Interface

- **Zone de statut** : affiche l'état actuel du receiver (`ACTIVÉ` / `DÉSACTIVÉ`)
- **Bouton Activer/Désactiver Receiver Avion** : enregistre ou désenregistre le receiver dynamique
- **Bouton Envoyer Broadcast** : déclenche le custom broadcast intra-application

---

## 🔐 Permissions requises

À déclarer dans `AndroidManifest.xml` :

```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
```

Et déclarer les receivers statiques :

```xml
<receiver android:name=".BootReceiver"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>

<receiver android:name=".CustomEventReceiver"
    android:exported="false">
    <intent-filter>
        <action android:name="com.example.receiverdemo.CUSTOM_EVENT" />
    </intent-filter>
</receiver>
```

---

## 📦 Dépendances

Aucune dépendance externe — uniquement les APIs Android natives :

```gradle
dependencies {
    implementation 'androidx.appcompat:appcompat:1.x.x'
    // BroadcastReceiver inclus nativement dans Android SDK
}
```

---

## ✨ Demo:

https://github.com/user-attachments/assets/048c0cd9-9a84-4b7e-a01f-6a09b2f596d5

---

## 🎯 Objectif pédagogique

Ce laboratoire introduit les BroadcastReceivers Android, et montre comment :

- Enregistrer et désenregistrer un receiver **dynamiquement** au runtime
- Déclarer un receiver **statique** dans le manifeste pour les événements système
- Créer et envoyer des **broadcasts personnalisés** intra-application
- Comprendre les **limitations de sécurité** imposées par Android
- Gérer le cycle de vie correctement pour éviter les **fuites mémoire**

---

## 👨‍💻 Auteur
**Mourad EL OUATIK** | Réalisé dans le cadre du **Lab 18 Android** | Programmation & Securite des Applications Mobile
