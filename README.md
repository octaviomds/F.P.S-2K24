


ENREGISTRER L APPLICATION SUR FIREBASE:

Vous pouvez enregistrer une ou plusieurs applications ou jeux pour vous connecter à votre projet Firebase.

Si vous publiez votre jeu à la fois sur iOS et Android, enregistrez les deux cibles de build de votre projet Unity avec le même projet Firebase . Si vous disposez de plusieurs variantes de build avec différents ID de bundle iOS ou ID d'application Android définis, vous devez enregistrer chaque variante avec le même projet Firebase.
Accédez à la console Firebase .
Au centre de la page de présentation du projet, cliquez sur l'icône Unity ( plat_unity ) pour lancer le workflow de configuration.


Si vous avez déjà ajouté une application à votre projet Firebase, cliquez sur Ajouter une application pour afficher les options de la plateforme.
Sélectionnez la cible de build de votre projet Unity que vous souhaitez enregistrer, ou vous pouvez même choisir d'enregistrer les deux cibles maintenant en même temps.


Remarque : Si vous enregistrez maintenant une seule cible de build de votre projet Unity, vous pourrez toujours revenir au workflow de configuration ultérieurement pour 
enregistrer l'autre cible de build.
Saisissez le(s) ID spécifique(s) à la plateforme de votre projet Unity.


Pour iOS : saisissez l'ID iOS de votre projet Unity dans le champ ID du bundle iOS .
Pour Android : saisissez l'ID Android de votre projet Unity dans le champ Nom du package Android .
Les termes nom de package et ID d’application sont souvent utilisés de manière interchangeable.
 Où trouvez-vous l'ID de votre projet Unity ?
 

Assurez-vous de saisir l'ID que votre projet utilise réellement. La valeur de l'ID est sensible à la casse et elle ne peut pas être modifiée pour ces applications Firebase une fois qu'elles sont enregistrées dans votre projet Firebase.
(Facultatif) Saisissez le(s) surnom(s) spécifique(s) à la plateforme de votre projet Unity.
Ces surnoms sont des identifiants internes pratiques et ne sont visibles que par vous dans la console Firebase.
Cliquez sur Enregistrer l'application .


Étape 3 : Ajouter les fichiers de configuration Firebase


Obtenez vos fichiers de configuration Firebase spécifiques à la plate-forme dans le workflow de configuration de la console Firebase.


Si vous enregistrez à la fois une cible de build iOS et Android de votre projet Unity, vous devrez télécharger et ajouter les fichiers de configuration pour les deux plates-formes.
Pour iOS : cliquez sur Télécharger GoogleService-Info.plist .
Pour Android : cliquez sur Télécharger google-services.json .
 Que devez-vous savoir sur ce fichier de configuration ?
 

Ouvrez la fenêtre Projet de votre projet Unity, puis déplacez votre ou vos fichiers de configuration dans le dossier Assets .
De retour dans la console Firebase, dans le workflow de configuration, cliquez sur Suivant .
Étape 4 : ajouter des SDK Firebase Unity


Remarque : Le flux de travail de configuration suivant est recommandé pour les nouveaux utilisateurs du SDK Unity. Pour des cas d'utilisation particuliers, Firebase propose des flux de configuration alternatifs .
Dans la console Firebase, cliquez sur Télécharger le SDK Firebase Unity , puis décompressez le SDK dans un endroit pratique.


Vous pouvez télécharger à nouveau le SDK Firebase Unity à tout moment.
Le SDK Firebase Unity n'est pas spécifique à la plate-forme.
Dans votre projet Unity ouvert, accédez à Assets > Import Package > Custom Package .
Dans le SDK décompressé, sélectionnez les produits Firebase pris en charge que vous souhaitez utiliser dans votre application.
