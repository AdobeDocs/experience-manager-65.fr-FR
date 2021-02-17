---
title: Enregistrement d’une tâche ou d’un formulaire en tant que brouillon 
seo-title: Enregistrement d’une tâche ou d’un formulaire en tant que brouillon 
description: Étapes d’enregistrement de brouillon d’une tâche ou d’un formulaire dans l’application AEM Forms
seo-description: Étapes d’enregistrement de brouillon d’une tâche ou d’un formulaire dans l’application AEM Forms
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 89%

---


# Enregistrement d’une tâche ou d’un formulaire en tant que brouillon {#saving-a-task-or-form-as-a-draft}

L’option Enregistrer en tant que brouillon enregistre un instantané d’une tâche ou d’un formulaire avec les données renseignées dans le formulaire associé. Vous pouvez également créer un brouillon à partir d’un modèle. Les brouillons sont enregistrés sur le périphérique mobile et synchronisées avec le serveur Adobe Experience Manager Forms pour une récupération ultérieure.

Vous pouvez [mettre à jour le formulaire](/help/forms/using/working-with-form.md), [l&#39;annoter](/help/forms/using/add-attachments.md) avec des photos et des notes à main levée. Au fur et à mesure que vous continuez à mettre à jour un formulaire, il est conseillé de l’enregistrer en tant que brouillon. Si vous décidez d’envoyer ultérieurement un formulaire complété, son enregistrement en tant que brouillon s’avère utile.

Pour activer la fonction Enregistrer en tant que brouillon pour les formulaires enregistrés sur le portail de formulaires, voir [Enregistrement d’un formulaire HTML5 en tant que brouillon](/help/forms/using/saving-html5-form-draft.md).
Pour configurer l’envoi des formulaires adaptatifs, voir [Composant Drafts &amp; Submission](/help/forms/using/draft-submission-component.md). (Non valide pour les formulaires synchronisés avec le serveur AEM Forms JEE.)

Pour créer un brouillon, ouvrez le formulaire et appuyez sur **Enregistrer en tant que brouillon** ![save-as-draft](assets/save-as-draft.png). Indiquez le nom de l’enregistrement de brouillons et **appuyez sur**. Le brouillon est enregistré dans le dossier Brouillons et synchronisé avec le serveur. Il est enregistré dans le dossier de boîte d’envoi si l’application est hors ligne.

Si par la suite vous mettez à jour le formulaire correspondant, les modifications sont répercutées immédiatement. Lors de la synchronisation de l’application AEM Forms avec le serveur AEM Forms, le brouillon est téléchargé sur le serveur AEM Forms. De plus, il est déplacé de la boîte d’envoi vers le dossier Tâches ou Brouillons. Une icône de modification s’affiche en regard de celui-ci.

Au fur et à mesure que vous continuez à travailler sur plusieurs tâches et points de départ et que vous les enregistrez, les brouillons sont enregistrés. Lorsque vous synchronisez votre application avec le serveur AEM Forms, le brouillon est enregistré sur le serveur. À tout moment, vous pouvez récupérer les brouillons en fonction des dernières date et heure d’enregistrement. Par exemple, si vous devez réinstaller l’application, voire changer de périphérique mobile, vous pouvez télécharger le brouillon depuis le serveur.

## Suppression d’un brouillon  {#delete-a-draft}

Le dossier des brouillons répertorie tous les brouillons. Vous pouvez utiliser l’option Supprimer le brouillon pour supprimer définitivement les brouillons du périphérique mobile et du serveur.

L’option de suppression des brouillons créés à partir d’une tâche n’est pas disponible. Lors de la suppression d’un brouillon créé à partir d’une tâche, celle-ci est abandonnée.

Vous pouvez ignorer les brouillons en mode hors ligne et en ligne. Au rejet des brouillons en mode hors ligne, les brouillons sont supprimés du serveur uniquement lorsque la connexion au serveur est rétablie.

Pour supprimer un brouillon, procédez comme suit :

1. Dans l’application AEM Forms, accédez aux **Formulaires.**
1. Cliquez sur **Brouillons** dans la liste déroulante en regard de Rechercher.
1. Un formulaire avec l’icône de modification ![edit-draft-app](assets/edit-draft-app.png) indique un brouillon. Appuyez sur les points de suspension horizontaux en regard du brouillon.
1. Dans les options qui s’affichent lorsque vous appuyez sur les points de suspension horizontaux, appuyez sur **Supprimer le brouillon**.
