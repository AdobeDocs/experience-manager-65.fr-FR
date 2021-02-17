---
title: Démarrage des processus
seo-title: Démarrage des processus
description: 'Comment utiliser l’espace de travail AEM Forms LiveCycle : sélectionner des processus, ajouter des notes et des pièces jointes, enregistrer des brouillons et ajouter aux favoris.'
seo-description: 'Comment utiliser l’espace de travail AEM Forms LiveCycle : sélectionner des processus, ajouter des notes et des pièces jointes, enregistrer des brouillons et ajouter aux favoris.'
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 90%

---


# Démarrage des processus {#starting-processes}

L’espace de travail AEM Forms organise les processus selon les catégories définies par l’administrateur ou le concepteur de processus. Il vous est également possible de placer les processus que vous utilisez souvent dans la catégorie Favoris pour les retrouver plus rapidement.

Lors du démarrage d’un processus, vous devez éventuellement remplir un formulaire pour démarrer un processus d’entreprise contrôlé par l’espace de travail AEM Forms. Lors du lancement d’un nouveau processus, certaines informations peuvent être préremplies dans le formulaire s’il utilise un processus de préparation des données.

Par exemple, vous avez besoin d’acheter un nouvel écran pour votre ordinateur, vous démarrez donc un processus appelé *Bon de commande*. Dès le démarrage du processus, un formulaire s’ouvre vous invitant à fournir des informations sur l’article à commander. Il se peut que votre nom, votre numéro d’employé et le nom du responsable soient préremplis dans le formulaire. Dès l’envoi de la demande, un processus d’entreprise est lancé. En fonction de la définition de processus, le serveur achemine automatiquement la demande vers votre gestionnaire. La tâche démarre et apparaît dans la liste des tâches de votre gestionnaire. Lorsque votre gestionnaire approuve la demande, le flux de production de formulaires achemine la demande vers le service des achats et vous envoie une notification électronique.

## Sélection de processus à démarrer  {#selecting-processes-to-start}

Vous pouvez sélectionner un processus pour le démarrer ou pour consulter les informations le concernant.

Lors de la sélection d’un processus à démarrer, vous devez éventuellement remplir un formulaire associé à ce dernier. L’envoi du formulaire déclenche le processus.

Des formulaires dans différents types de formats de fichier sont pris en charge, notamment les formats Adobe PDF, HTML et SWF. Un formulaire peut ressembler à un formulaire Web ou à un formulaire classique imprimable ou peut vous guider à travers une série de panneaux de type assistant nécessaires à la collecte d’informations.

Si le formulaire et le processus le permettent, vous pouvez également enregistrer le formulaire hors connexion, le remplir, puis l’envoyer pour terminer la tâche. Lorsque le formulaire est envoyé, votre client de messagerie électronique est démarré avec l’adresse électronique du serveur appropriée, si un point de contact de messagerie est configuré. Vous pouvez alors envoyer le formulaire renseigné au serveur par courrier électronique.

Lorsque vous sélectionnez un processus, les onglets Formulaires et Détails s’affichent. Si le processus vous permet d’ajouter des notes ou des pièces jointes, l’onglet Pièces jointes et Notes s’affiche également. Si vous avez également configuré l’URL de résumé avec le processus, l’onglet Résumé s’affiche aussi. L’onglet Formulaires affiche le formulaire associé et l’onglet Détails affiche des informations sur la tâche actuelle et le processus dont elle fait partie.

### Démarrage d’un processus d’entreprise  {#start-a-business-process}

1. Dans la liste située à gauche de la page Démarrer le processus, sélectionnez une catégorie. Tous les processus auxquels vous pouvez accéder dans cette catégorie s’affichent sur la droite.

   >[!NOTE]
   >
   >Si le panneau Catégories est réduit, cliquez sur « Ouvrir les catégories », dans la zone en haut à gauche de l’espace de travail AEM Forms, pour ouvrir le panneau.

1. Sélectionnez un processus en cliquant sur une tâche. Le formulaire associé au processus s’ouvre dans l’onglet Formulaire.

   Chaque formulaire d’un processus possède une URL unique. Vous pouvez utiliser l’URL unique pour lancer directement l’espace de travail HTML avec le processus et le formulaire spécifiques. Le format de l’URL est https://&lt;serveur>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;NomApplication>%2F&lt;NomProcessus>. La chaîne &lt;ApplicationName>%2F&lt;ProcessName> est toujours codée en URL. Par exemple, http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La chaîne ApplicationName%2FProcessName de l&#39;exemple est codée en URL.

1. Remplissez le formulaire selon les instructions fournies. Si nécessaire, cliquez sur **Agrandir** pour augmenter la zone visible du formulaire.
1. Si l’onglet Pièces jointes est disponible, ajoutez des pièces jointes comme requis.
1. Si l’onglet Notes est disponible, fournissez des notes si nécessaire.
1. Exécutez l’une des étapes suivantes :

   * Cliquez sur le bouton Envoyer sur le formulaire, s’il y en a un.
   * Cliquez sur Terminer sous le formulaire, si le formulaire n’a pas de bouton Envoyer.

   Process Management démarre le processus et achemine le formulaire vers les listes de tâches des personnes appropriées qui doivent effectuer la tâche suivante dans le processus.

   Si vous devez fermer un formulaire avant de l’envoyer et sans perdre les données que vous avez entrées, enregistrez un brouillon et terminez-le ultérieurement si le processus le permet. Si le formulaire et le processus le permettent, vous pouvez également cliquer sur **Hors connexion** et l’envoyer plus tard depuis Adobe Reader®, Adobe Acrobat® Professional ou Acrobat Standard.

   >[!NOTE]
   >
   >l’option hors ligne est disponible pour les formulaires PDF uniquement.

## Ajout de notes et de pièces jointes  {#adding-notes-and-attachments}

Vous pouvez ajouter des notes et des pièces jointes à un processus si ce dernier le permet. Vous pouvez fournir des autorisations pour d’autres utilisateurs, qui participent au processus pour afficher, mettre à jour et supprimer les notes ou les pièces jointes.

### Ajout d’une note  {#add-a-note}

Vous pouvez ajouter plusieurs notes, modifier les notes écrites, et les supprimer. Chaque note est dotée d’un titre, d’une description et d’une autorisation d’accès associés. Vous pouvez définir l’une des autorisations d’accès suivantes sur une note :

* En lecture seule (l’autorisation par défaut)
* Lecture/Modification/Suppression
* Lecture/Modification
* Lecture/Suppression
* Pas d’accès

1. Ouvrez une tâche et cliquez sur l’onglet **Notes**, si le processus vous le permet.
1. Saisissez un titre pour la note dans la zone **Titre**, puis saisissez le texte de la note dans la zone **Note**.
1. Sélectionnez le niveau des **Autorisations** relatives à la note pour les autres utilisateurs participant au processus.
1. Cliquez sur **OK**. Un fichier texte contenant votre note est attaché au formulaire. Vous pouvez mettre à jour une note en cliquant sur celle-ci et en modifiant directement le texte. Vous pouvez supprimer une note en cliquant sur le bouton **Supprimer** ![Image d&#39;une corbeille ](assets/icondelete.png) en regard de la note.

### Ajout d’une pièce jointe {#add-an-attachment}

Vous pouvez également ajouter vos commentaires sur la pièce jointe. Vous pouvez définir l’un des droits d’accès suivants sur une pièce jointe :

* En lecture seule (l’autorisation par défaut)
* Lecture/Modification/Suppression
* Lecture/Modification
* Lecture/Suppression
* Pas d’accès

1. Cliquez sur l’onglet **Pièces jointes** et sélectionnez **Pièce jointe**.
1. Cliquez sur **Parcourir** pour sélectionner le fichier à attacher.
1. Sélectionnez le niveau des **Autorisations** relatives à la pièce jointe pour les autres utilisateurs participant au processus. Si vous sélectionnez **Lecture**, d’autres utilisateurs peuvent enregistrer le fichier localement. Si vous sélectionnez l’une des autorisations de modification, les autres utilisateurs peuvent également télécharger un nouveau fichier pour remplacer votre pièce jointe.
1. Cliquez sur **OK**. Le fichier est attaché au formulaire. Vous pouvez supprimer un fichier en cliquant sur le bouton **Supprimer** ![Image d&#39;une corbeille ](assets/icondelete.png) en regard de la pièce jointe.

## Enregistrement des brouillons de formulaires {#saving-draft-copies-of-forms}

Si vous devez remplir et envoyer un formulaire ultérieurement, vous pouvez enregistrer un brouillon de formulaire afin de ne pas perdre le travail effectué. Les brouillons sont ajoutés à la catégorie Brouillons de la page Tâches.

Dès la réouverture et l’envoi d’un brouillon de formulaire, ce dernier est supprimé de la catégorie Brouillons.

Vous pouvez également configurer l’espace de travail afin qu’il enregistre automatiquement les informations saisies par l’utilisateur en tant que brouillon. Pour plus d’informations, voir [Gestion des préférences](/help/forms/using/getting-started-livecycle-html-workspace.md). 

>[!NOTE]
>
>le bouton Enregistrer est indisponible pour certains formulaires selon les processus auxquels ils sont associés.

### Enregistrement d’un brouillon  {#save-a-draft-copy}

1. Cliquez sur **Enregistrer** dans le coin inférieur gauche de n’importe quel onglet. Le formulaire est ajouté à la catégorie Brouillons de votre page Tâches. Toutes les modifications apportées au formulaire sont enregistrées.

### Réouverture d’un brouillon  {#reopen-a-draft-copy}

1. Dans la page Tâches, sélectionnez la file d’attente **Brouillons**, puis cliquez sur le brouillon du formulaire.

   Si le formulaire contient une série de panneaux, vous devez éventuellement accéder au panneau dans lequel vous avez terminé votre dernière session.

## Ajout de processus à la catégorie Favoris  {#adding-processes-to-the-favorites-category}

Vous pouvez ajouter tout processus à votre catégorie Favoris. Lorsque vous définissez vos favoris, vous pouvez regrouper tous les processus que vous démarrez fréquemment dans une seule catégorie pour les retrouver rapidement.

>[!NOTE]
>
>Si vous avez l’habitude de démarrer des processus lorsque vous utilisez l’espace de travail AEM Forms, vous pouvez définir la préférence Emplacement de démarrage de manière à afficher la catégorie Favoris au démarrage de l’espace de travail AEM Forms. Pour plus d’informations, voir Gestion des préférences dans [Prise en main de l’espace de travail AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Pour marquer un processus en tant que favori, sélectionnez la tâche dans sa catégorie, puis cliquez sur l’étoile au contour creux. L’étoile devient dorée. Pour annuler le marquage d’un processus en tant que favori, cliquez de nouveau sur l’étoile dorée.
