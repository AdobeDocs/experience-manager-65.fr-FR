---
title: Démarrage des processus
description: 'Comment utiliser l’espace de travail AEM Forms LiveCycle : sélectionner des processus, ajouter des notes et des pièces jointes, enregistrer des brouillons et ajouter aux favoris.'
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1334'
ht-degree: 100%

---

# Démarrage des processus {#starting-processes}

L’espace de travail AEM Forms organise les processus selon les catégories définies par l’administrateur ou le concepteur de processus. Vous pouvez également placer les processus que vous utilisez fréquemment dans la catégorie Favoris afin de pouvoir les trouver rapidement.

Lors du démarrage d’un processus, vous devez éventuellement remplir un formulaire pour démarrer un processus d’entreprise contrôlé par l’espace de travail AEM Forms. Si un formulaire utilise le processus de préparation des données, certaines informations peuvent être préremplies dans un formulaire vierge lors du lancement d’un nouveau processus.

Par exemple, vous avez besoin d’acheter un nouvel écran pour votre ordinateur, vous démarrez donc un processus appelé *Bon de commande*. Dès le démarrage du processus, un formulaire s’ouvre vous invitant à fournir des informations sur l’article à commander. Il se peut que votre nom, votre numéro d’employé et le nom du responsable soient préremplis dans le formulaire. Dès l’envoi de la demande, un processus d’entreprise est lancé. En fonction de la définition de processus, le serveur achemine automatiquement la demande vers votre gestionnaire. La tâche démarre et apparaît dans la liste des tâches de votre gestionnaire. Lorsque votre responsable approuve la requête, le workflow des formulaires achemine la requête vers le service des achats et vous envoie une notification par e-mail.

## Sélectionner les processus à démarrer {#selecting-processes-to-start}

Vous pouvez sélectionner un processus pour le démarrer ou afficher plus d’informations à son sujet.

Lors de la sélection d’un processus à démarrer, vous devez éventuellement remplir un formulaire associé à ce dernier. L’envoi du formulaire démarre le processus.

Des formulaires dans différents types de formats de fichier sont pris en charge, notamment les formats Adobe PDF, HTML et SWF. Le formulaire peut ressembler à un formulaire web ou à un formulaire classique imprimable, ou peut vous guider à travers une série de panneaux de type assistant nécessaires à la collecte d’informations.

Si le formulaire et le processus le permettent, vous pouvez également enregistrer le formulaire hors connexion, le remplir, puis l’envoyer pour terminer la tâche. Lorsque le formulaire est envoyé, votre client de messagerie électronique est démarré avec l’adresse électronique du serveur appropriée, si un point de contact de messagerie est configuré. Vous pouvez ensuite envoyer le formulaire complété au serveur par e-mail.

Lorsque vous sélectionnez un processus, les onglets Formulaires et Détails s’affichent. Si le processus vous permet d’ajouter des notes ou des pièces jointes, l’onglet Pièces jointes et Notes s’affiche également. Si vous avez également configuré l’URL de résumé avec le processus, l’onglet Résumé s’affiche aussi. L’onglet Formulaires affiche le formulaire associé et l’onglet Détails affiche des informations sur la tâche actuelle et le processus dont elle fait partie.

### Démarrage d’un processus d’entreprise {#start-a-business-process}

1. Dans la liste située à gauche de la page Démarrer le processus, sélectionnez une catégorie. Tous les processus auxquels vous avez accès dans la catégorie apparaissent à droite.

   >[!NOTE]
   >
   >Si le volet Catégories est réduit, cliquez sur « Ouvrir les catégories », dans la zone supérieure gauche de l’espace de travail AEM Forms, pour ouvrir le volet.

1. Sélectionnez un processus en cliquant sur une tâche. Le formulaire associé au processus s’ouvre dans l’onglet Formulaire.

   Chaque formulaire d’un processus comporte une URL unique. Vous pouvez utiliser l’URL unique pour lancer directement l’espace de travail HTML avec le processus et le formulaire spécifiques. Le format de l’URL est https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;ApplicationName>%2F&lt;ProcessName>. La chaîne &lt;ApplicationName>%2F&lt;ProcessName> est toujours encodée en URL. Voici un exemple d’URL : http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La chaîne ApplicationName%2FProcessName de l’exemple est en codage URL.

1. Remplissez le formulaire selon les instructions fournies. Si nécessaire, cliquez sur le bouton **Agrandir** pour augmenter la partie visible du formulaire.
1. Si l’onglet Pièces jointes est disponible, ajoutez des pièces jointes selon les besoins.
1. Si l’onglet Notes est disponible, fournissez des notes si nécessaire.
1. Exécutez l’une des étapes suivantes :

   * Cliquez sur le bouton Envoyer du formulaire, si le formulaire comporte un bouton Envoyer.
   * Cliquez sur Terminer sous le formulaire si le formulaire ne comporte pas de bouton Envoyer.

   Process Management démarre le processus et achemine le formulaire vers les listes de tâches des personnes appropriées qui doivent effectuer la tâche suivante dans le processus.

   Si vous devez fermer un formulaire avant de l’envoyer et sans perdre les données que vous avez entrées, enregistrez un brouillon et terminez-le ultérieurement si le processus le permet. Si le formulaire et le processus le permettent, vous pouvez également cliquer sur **Hors ligne** et plus tard le soumettre depuis Adobe® Reader® ou Adobe® Acrobat® Professional ou Acrobat Standard.

   >[!NOTE]
   >
   >L’option hors ligne est disponible pour les formulaires PDF uniquement.

## Ajouter des notes et des pièces jointes {#adding-notes-and-attachments}

Vous pouvez ajouter des notes et des pièces jointes à un processus si ce dernier le permet. Vous pouvez accorder des autorisations à d’autres utilisateurs et utilisatrices qui participent au processus pour afficher, mettre à jour et supprimer les notes ou les pièces jointes.

### Ajouter une note {#add-a-note}

Vous pouvez ajouter plusieurs notes, modifier les notes écrites, et les supprimer. Chaque note est dotée d’un titre, d’une description et d’une autorisation d’accès associés. Vous pouvez définir l’une des autorisations d’accès suivantes sur une note :

* Lecture seule (autorisation par défaut)
* Lecture/modification/suppression
* Lecture/modification
* Lecture/suppression
* Accès interdit

1. Ouvrez une tâche et cliquez sur l’onglet **Notes**, si le processus vous le permet.
1. Saisissez le titre de la note dans la zone **Titre** et saisissez le texte de la note dans la zone **Note**.
1. Sélectionnez le niveau des **Autorisations** relatives à la note pour les autres utilisateurs et utilisatrices participant au processus.
1. Cliquez sur **OK**. Un fichier texte contenant votre note est attaché au formulaire. Vous pouvez mettre à jour une note en cliquant sur celle-ci et en modifiant directement le texte. Vous pouvez supprimer une note en cliquant sur le bouton **Supprimer** ![Image d’une corbeille](assets/icondelete.png) à côté de la note.

### Ajouter une pièce jointe {#add-an-attachment}

Vous pouvez également ajouter vos commentaires sur la pièce jointe. Vous pouvez définir l’une des autorisations d’accès suivantes sur une pièce jointe :

* Lecture seule (autorisation par défaut)
* Lecture/modification/suppression
* Lecture/modification
* Lecture/suppression
* Accès interdit

1. Cliquez sur l’onglet **Pièces jointes** et sélectionnez **Pièce jointe**.
1. Cliquez sur **Parcourir** pour sélectionner le fichier à joindre.
1. Sélectionnez le niveau des **Autorisations** relatives à la pièce jointe pour les autres utilisateurs participant au processus. Si vous sélectionnez **Lecture**, d’autres utilisateurs peuvent enregistrer le fichier localement. Si vous sélectionnez l’une des autorisations de modification, d’autres personnes peuvent également charger un nouveau fichier pour remplacer votre pièce jointe.
1. Cliquez sur **OK**. Le fichier est attaché au formulaire. Vous pouvez supprimer un fichier en cliquant sur le bouton **Supprimer** ![Image d’une corbeille](assets/icondelete.png) à côté de la pièce jointe.

## Enregistrer des brouillons de formulaires {#saving-draft-copies-of-forms}

Si vous devez remplir et envoyer un formulaire ultérieurement, vous pouvez enregistrer un brouillon de formulaire afin de ne pas perdre le travail effectué. Les brouillons sont ajoutés à la catégorie Brouillons de la page Tâches.

Dès la réouverture et l’envoi d’un brouillon de formulaire, ce dernier est supprimé de la catégorie Brouillons.

Vous pouvez également configurer l’espace de travail afin qu’il enregistre automatiquement les informations saisies par l’utilisateur ou l’utilisatrice en tant que brouillon. Pour plus d’informations, voir [Gestion des préférences](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>Le bouton Enregistrer est indisponible pour certains formulaires selon les processus auxquels ils sont associés.

### Enregistrer un brouillon {#save-a-draft-copy}

1. Cliquez sur **Enregistrer** dans le coin inférieur gauche de n’importe quel onglet. Le formulaire est ajouté à la catégorie Brouillons de votre page Tâches. Toutes les modifications que vous avez apportées au formulaire sont enregistrées.

### Rouvrir un brouillon {#reopen-a-draft-copy}

1. Dans la page Tâches, sélectionnez la file d’attente **Brouillons**, puis cliquez sur le brouillon du formulaire.

   Si le formulaire contient une série de panneaux, vous devrez peut-être accéder au panneau dans lequel vous avez terminé votre dernière session.

## Ajouter des processus à la catégorie Favoris {#adding-processes-to-the-favorites-category}

Vous pouvez ajouter tout processus à votre catégorie Favoris. En définissant des favoris, vous pouvez regrouper tous les processus que vous démarrez fréquemment dans une seule catégorie afin de les retrouver rapidement.

>[!NOTE]
>
>Si vous démarrez généralement des processus lorsque vous utilisez l’espace de travail AEM Forms, vous pouvez définir la préférence Emplacement de démarrage afin d’afficher automatiquement la catégorie Favoris au démarrage de l’espace de travail AEM Forms. Pour plus d’informations, voir Gestion des préférences dans [Prise en main de l’espace de travail AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Pour marquer un processus en tant que favori, sélectionnez la tâche dans sa catégorie, puis cliquez sur l’étoile au contour creux. L’étoile devient dorée. Pour marquer un processus comme favori, cliquez de nouveau sur l’étoile dorée.
