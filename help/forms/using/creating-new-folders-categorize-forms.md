---
title: Création de dossiers pour classer les formulaires
seo-title: Création de dossiers pour classer les formulaires
description: Utilisez des dossiers pour organiser vos modèles de formulaire, vos fichiers PDF, vos ressources et vos formulaires adaptatifs.
seo-description: Utilisez des dossiers pour organiser vos modèles de formulaire, vos fichiers PDF, vos ressources et vos formulaires adaptatifs.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 82%

---


# Création de dossiers pour classer les formulaires {#create-new-folders-to-categorize-forms}

Vous pouvez mieux organiser vos ressources à l’aide de dossiers. Dans la mesure où AEM Forms prend en charge plusieurs types de ressources (modèles de formulaire, fichiers PDF, documents, ressources et formulaires adaptatifs) avec différentes métadonnées, vous pouvez utiliser des dossiers pour classer vos formulaires selon les critères de votre choix.

AEM Forms permet de modifier le titre d’un dossier. Le titre est différent de celui du nœud sous lequel le dossier est stocké dans le référentiel. Il est conservé sous forme de métadonnées pour le dossier. Si vous modifiez le titre d’un dossier, le chemin d’accès à toute ressource contenue dans celui-ci n’est pas affecté.

## Créer un dossier {#create-a-folder}

Vous pouvez créer un dossier dans AEM Forms à l’aide de l’une des méthodes suivantes :

* Téléchargement d’un fichier ZIP contenant les ressources dans la structure de dossiers souhaitée (voir [Obtention de documents XDP et PDF dans AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Création d’un dossier vide

1. Connectez-vous à l’interface utilisateur AEM Forms à l’adresse `https://<server>:<port>/aem/forms.html`.
1. Accédez à l’emplacement où vous souhaitez créer un dossier.
1. Cliquez sur l&#39;icône ![aem6forms_add](assets/aem6forms_add.png) dans la barre d&#39;outils, puis sélectionnez **[!UICONTROL Créer un dossier]**.

1. Saisissez les informations suivantes :

   * **Titre : nom** d’affichage du dossier
   * **Nom :** *(Obligatoire)* nom du nœud sous lequel vous souhaitez stocker le dossier dans le référentiel.

   >[!NOTE]
   >
   >Par défaut, la valeur du champ de nom est automatiquement renseignée à partir du titre. Le nom peut contenir uniquement des caractères alphanumériques, des tirets (-) et des traits de soulignement (_). Tout autre caractère spécial saisi dans le titre est automatiquement remplacé par un tiret. Vous êtes alors invité à confirmer le nouveau nom. Vous pouvez choisir de conserver le nom proposé ou de le modifier.

1. Cliquez sur **[!UICONTROL Envoyer].**

   Un nouveau dossier avec le titre que vous avez défini s’affiche à l’emplacement spécifié dans la liste des ressources.

   Si un dossier portant le même nom que celui spécifié existe déjà, l’envoi échoue avec une erreur. Vous pouvez vue le message d’erreur en passant la souris sur l’icône ![aem6forms_error_alert](assets/aem6forms_error_alert.png) qui s’affiche en regard du champ de nom.

### Modification du titre d’un dossier {#edit-the-folder-title-br}

1. Sélectionnez le dossier dont vous souhaitez modifier le titre.
1. Cliquez sur l’icône de modification ![aem6forms_edit](assets/aem6forms_edit.png) dans la barre d’outils.
1. Entrez le nouveau titre. Le champ de texte est prérenseigné avec la valeur actuelle du titre du dossier. Vous pouvez remplacer cette valeur.
1. Cliquez sur **[!UICONTROL Envoyer].**

