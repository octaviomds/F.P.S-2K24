# Intégration Firebase dans un projet Unity

Guide d'intégration du SDK Firebase dans un projet Unity, de la création du projet Firebase jusqu'à l'initialisation dans le code.

---

## Prerequis

- Unity 2021 LTS ou version ulterieure
- Plateformes Apple uniquement :
  - Xcode 16.2 ou version ulterieure
  - CocoaPods 1.12.0 ou version ulterieure
- Cibles de build minimales :
  - iOS 15 ou version ulterieure
  - tvOS 15 ou version ulterieure
  - Android API niveau 23 (Marshmallow) ou version ulterieure
- Un compte Google pour acceder a la console Firebase

---

## Etape 1 - Creer un projet Firebase

1. Rendez-vous sur [console.firebase.google.com](https://console.firebase.google.com)
2. Cliquez sur "Ajouter un projet" et suivez les etapes de configuration
3. Une fois le projet cree, vous arrivez sur le tableau de bord du projet

---

## Etape 2 - Enregistrer votre application

1. Depuis le tableau de bord, cliquez sur l'icone Unity pour demarrer le workflow de configuration
2. Selectionnez la ou les cibles de build a enregistrer (iOS, Android, ou les deux)
3. Renseignez les identifiants specifiques a chaque plateforme :
   - iOS : ID de bundle (exemple : `com.studio.nomjeu`)
   - Android : nom du package (exemple : `com.studio.nomjeu`)
4. Cliquez sur "Enregistrer l'application"

> Si vous publiez sur iOS et Android, enregistrez les deux cibles dans le meme projet Firebase. Si vous avez plusieurs variantes de build avec des identifiants differents, chacune doit etre enregistree separement.

---

## Etape 3 - Ajouter les fichiers de configuration

1. Telechargez les fichiers de configuration depuis la console Firebase :
   - iOS : `GoogleService-Info.plist`
   - Android : `google-services.json`
2. Dans Unity, ouvrez la fenetre "Project"
3. Glissez-deposez les fichiers dans le dossier `Assets/`

---

## Etape 4 - Importer le SDK Firebase Unity

1. Telechargez le SDK Firebase Unity depuis la console Firebase (ou depuis [firebase.google.com/docs/unity](https://firebase.google.com/docs/unity))
2. Decompressez l'archive a l'emplacement de votre choix
3. Dans Unity, allez dans `Assets > Import Package > Custom Package`
4. Selectionnez les packages correspondant aux produits Firebase utilises :

| Produit Firebase         | Package a importer                  |
|--------------------------|-------------------------------------|
| Google Analytics         | `FirebaseAnalytics.unitypackage`    |
| Authentication           | `FirebaseAuth.unitypackage`         |
| Realtime Database        | `FirebaseDatabase.unitypackage`     |
| Firestore                | `FirebaseFirestore.unitypackage`    |
| Cloud Messaging (FCM)    | `FirebaseMessaging.unitypackage`    |
| Remote Config            | `FirebaseRemoteConfig.unitypackage` |
| Storage                  | `FirebaseStorage.unitypackage`      |

5. Dans la fenetre "Import Unity Package", cliquez sur "Import"

> Pour iOS : ne desactivez pas le swizzling de methode. Il est requis par le SDK, notamment pour la gestion des jetons FCM.

---

## Etape 5 - Verifier Google Play Services (Android uniquement)

Certains produits Firebase pour Android necessitent que Google Play Services soit a jour. Ajoutez le code suivant au demarrage de votre application pour verifier et corriger les dependances si necessaire.

```csharp
using Firebase.Extensions;

Firebase.FirebaseApp.CheckAndFixDependenciesAsync().ContinueWithOnMainThread(task =>
{
    var dependencyStatus = task.Result;

    if (dependencyStatus == Firebase.DependencyStatus.Available)
    {
        // Firebase est pret a etre utilise
        var app = Firebase.FirebaseApp.DefaultInstance;
        // Initialisez vos services Firebase ici
    }
    else
    {
        UnityEngine.Debug.LogError(
            string.Format("Impossible de resoudre les dependances Firebase : {0}", dependencyStatus)
        );
        // Le SDK Firebase ne peut pas etre utilise dans cet etat
    }
});
```

---

## Configuration Desktop (Beta)

Le SDK Firebase Unity peut egalement s'executer sous Windows, macOS, Linux et dans l'editeur Unity, ce qui facilite les tests en cours de developpement.

### Mise en place

Suivez les memes etapes que pour une plateforme mobile. Firebase detecte automatiquement le fichier de configuration mobile (`GoogleService-Info.plist` ou `google-services.json`) et genere un fichier de configuration desktop (`google-services-desktop.json`) dans le dossier `StreamingAssets/`.

### Mode Edition Unity

Le SDK peut aussi s'executer en mode Edition. Dans ce cas, n'utilisez pas l'instance par defaut de `FirebaseApp` pour eviter les conflits. Creez une instance nommee :

```csharp
// Ne pas faire en mode Edition :
// var app = Firebase.FirebaseApp.DefaultInstance;

// Faire a la place :
var app = Firebase.FirebaseApp.Create(options, "nom-unique-editeur");
```

> Attention : la compatibilite desktop est une fonctionnalite beta reservee au developpement. Ne l'utilisez pas en production.

---

## Structure du projet recommandee

```
Assets/
  Firebase/                       -- Fichiers du SDK Firebase (generes a l'import)
  GoogleService-Info.plist        -- Configuration iOS
  google-services.json            -- Configuration Android
  Scripts/
    Firebase/
      FirebaseManager.cs          -- Initialisation et gestion Firebase
      AuthManager.cs              -- Gestion de l'authentification
      DatabaseManager.cs          -- Acces a la base de donnees
  StreamingAssets/
    google-services-desktop.json  -- Configuration desktop (generee automatiquement)
```

---

## Ressources

- [Documentation officielle Firebase pour Unity](https://firebase.google.com/docs/unity/setup)
- [Console Firebase](https://console.firebase.google.com)
- [Exemple de jeu MechaHamster (GitHub)](https://github.com/google/mechahamster)
- [Depannage et FAQ Unity](https://firebase.google.com/docs/unity/troubleshooting-faq)
- [Produits Firebase compatibles avec le SDK Unity](https://firebase.google.com/docs/unity/setup#available-libraries)
