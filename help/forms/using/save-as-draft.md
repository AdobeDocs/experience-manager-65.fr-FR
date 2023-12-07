---
title: Enregistrer une tâche ou un formulaire en tant que brouillon
description: Procédure d’enregistrement d’un brouillon d’une tâche ou d’un formulaire dans l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 20%

---

# Enregistrer une tâche ou un formulaire en tant que brouillon {#saving-a-task-or-form-as-a-draft}

L’option Enregistrer en tant que brouillon enregistre un instantané d’une tâche ou d’un formulaire avec les données renseignées dans le formulaire associé. Vous pouvez également créer un brouillon à partir d’un modèle. Les brouillons sont enregistrés sur le périphérique mobile et synchronisés avec le serveur Adobe Experience Manager Forms pour une récupération ultérieure.

Vous pouvez [mettre à jour le formulaire](/help/forms/using/working-with-form.md), [l’annoter](/help/forms/using/add-attachments.md) avec des photos et des notes par saisie tactile. Au fur et à mesure que vous continuez à mettre à jour un formulaire, il est recommandé de l’enregistrer en tant que brouillon. Dans les cas où vous décidez d’envoyer ultérieurement un formulaire rempli, il est utile de l’enregistrer en tant que brouillon.

Pour activer la fonctionnalité Enregistrer en tant que brouillon pour les formulaires enregistrés sur le portail de formulaires, voir [Enregistrer un formulaire HTML5 en tant que brouillon](/help/forms/using/saving-html5-form-draft.md).
Pour configurer l’envoi des formulaires adaptatifs, voir [Composant Drafts &amp; Submission](/help/forms/using/draft-submission-component.md). (Non valide pour les formulaires synchronisés avec le serveur AEM Forms JEE.)

Pour créer un brouillon, ouvrez le formulaire et sélectionnez le **Enregistrer en tant que brouillon** ![save-as-draft](assets/save-as-draft.png). Indiquez le nom du brouillon et sélectionnez **Enregistrer**. Le brouillon est enregistré dans le dossier Brouillons et synchronisé avec le serveur. Il est enregistré dans le dossier de boîte d’envoi si l’application est hors ligne.

Si vous mettez à jour le formulaire correspondant par la suite, les modifications sont répercutées immédiatement. Lors de la synchronisation de l’application AEM Forms avec le serveur AEM Forms, le brouillon est chargé sur le serveur AEM Forms. En outre, le brouillon est déplacé de la boîte d’envoi vers le dossier Tâches ou Brouillons . Une icône de modification s’affiche en regard de celle-ci.

Au fur et à mesure que vous continuez à travailler sur plusieurs tâches et points de départ et que vous les enregistrez, les brouillons sont enregistrés. Chaque fois que votre application est synchronisée avec le serveur AEM Forms, le brouillon est enregistré sur le serveur. Cela vous permet de récupérer à tout moment les brouillons en fonction de la date et de l’heure de dernier enregistrement. Par exemple, si vous réinstallez l’application ou modifiez votre périphérique mobile, vous pouvez télécharger le brouillon à partir du serveur.

## Supprimer un brouillon {#delete-a-draft}

Le dossier des brouillons répertorie tous les brouillons. Vous pouvez utiliser l’option Supprimer le brouillon pour supprimer définitivement les brouillons du périphérique mobile et du serveur.

L’option de suppression des brouillons créés à partir d’une tâche n’est pas disponible. Lors de la suppression d’un brouillon créé à partir d’une tâche, la tâche est abandonnée.

Vous pouvez ignorer les brouillons en mode hors ligne et en ligne. Lorsque vous ignorez les brouillons en mode hors ligne, ils ne sont supprimés du serveur que lorsque la connexion au serveur est restaurée.

Pour supprimer un brouillon, procédez comme suit :

1. Dans l’application AEM Forms, accédez aux **Formulaires.**
1. Cliquez sur **Brouillons** dans la liste déroulante en regard de Rechercher.
1. Un formulaire avec l’icône de modification ![edit-draft-app](assets/edit-draft-app.png) indique un brouillon. Sélectionnez les points de suspension horizontaux en regard du brouillon.
1. Dans les options qui s’affichent lorsque vous sélectionnez les points de suspension horizontaux, sélectionnez **Supprimer le brouillon**.
