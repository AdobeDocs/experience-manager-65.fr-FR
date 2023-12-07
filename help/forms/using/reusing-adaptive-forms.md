---
title: Réutiliser des formulaires adaptatifs
description: Vous pouvez réutiliser un formulaire adaptatif existant pour créer de nouveaux formulaires adaptatifs.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 59%

---

# Réutiliser des formulaires adaptatifs {#reusing-adaptive-forms}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html) |
| AEM 6.5 | Cet article |

## Présentation {#introduction}

Si vous souhaitez utiliser certaines des propriétés d’un formulaire adaptatif existant pour en générer un nouveau, vous pouvez simplement utiliser la fonctionnalité de copier-coller. En outre, vous pouvez coller le nouveau formulaire adaptatif au chemin du dossier souhaité. Toutes les propriétés de métadonnées sont répliquées ; les XFA et XSD relatifs aux formulaires adaptatifs basés sur XFA et XSD sont également copiés.

>[!NOTE]
>
>L’état et les détails de révision ne sont pas copiés. Par exemple, si votre formulaire adaptatif est publié, puis que vous le copiez, le formulaire adaptatif collé est à l’état non publié. De même, si un élément copié est en cours de révision, l’élément collé ne se trouve pas sous la même révision.

### Copier un formulaire adaptatif {#copy-an-adaptive-form}

Copiez un formulaire adaptatif en utilisant l’une des méthodes suivantes :

1. Cliquez sur l’icône de copie ![aem6forms_copy](assets/aem6forms_copy.png) dans les actions rapides.

   >[!NOTE]
   >
   >Les actions rapides sont les éléments d’action qui s’affichent sur une vignette lorsque vous pointez dessus.

1. Sélectionnez le formulaire adaptatif. Le processus de sélection est différent pour chaque vue.

   Si le mode d’affichage Vignette est activé, accédez au mode de sélection en cliquant sur l’icône de sélection ![aem6forms_check-circle](assets/aem6forms_check-circle.png), puis cliquez sur tous les formulaires adaptatifs à copier.

   Si la vue Liste est active, cochez les cases à cocher de tous les formulaires adaptatifs pour les sélectionner.

   >[!NOTE]
   >
   >Tous les éléments sélectionnés doivent être des formulaires adaptatifs, car la fonctionnalité de copier-coller n’est prise en charge que pour ces formulaires, et tous doivent figurer dans le même dossier.

   Après avoir sélectionné les éléments, cliquez sur l’icône de copie ![aem6forms_copy](assets/aem6forms_copy.png) de la barre d’outils pour copier le formulaire adaptatif sélectionné.

### Coller un formulaire adaptatif {#paste-an-adaptive-form}

Un clic sur l’action de copie fait automatiquement quitter le mode de sélection et rend visible l’icône de collage ![aem6forms_paste](assets/aem6forms_paste.png). Accédez maintenant au dossier de votre choix et cliquez sur l’icône de collage ![aem6forms_paste](assets/aem6forms_paste.png) pour coller le formulaire adaptatif copié.

Si vous collez le formulaire dans le même dossier ou s’il existe déjà un autre fichier portant le même nom de nœud (avec lequel il est stocké dans le référentiel CRX) dans ce dossier cible, une unité est ajoutée au suffixe (par exemple, myaf devient myaf1 et si myaf1 existe déjà au même emplacement, myaf devient myaf2). Toutes les autres propriétés restent identiques au formulaire adaptatif d’origine.

Cliquer sur l’icône de collage ![aem6forms_paste](assets/aem6forms_paste.png) la masque à nouveau. Vous ne pouvez effectuer qu’une seule opération de copie à la fois. Pour créer une autre copie d’un même élément, copiez le à nouveau.

### Modification du contenu du nouveau formulaire adaptatif {#change-contents-of-new-adaptive-form}

Le contenu d’un formulaire adaptatif collé peut être modifié en utilisant les méthodes suivantes pour le rendre différent du formulaire copié :

1. **Modification des propriétés de métadonnées :**

   Vous pouvez modifier les propriétés de métadonnées du formulaire adaptatif ; le titre et la description, par exemple. Pour plus d’informations sur les propriétés de métadonnées et la méthode à appliquer pour les modifier, reportez-vous à la section [Gestion de métadonnées de formulaire](/help/forms/using/manage-form-metadata.md).

1. **Modification de XFA/XSD pour les formulaires adaptatifs basés sur XFA/XSD :**

   Vous pouvez modifier le XFA/XSD utilisé dans les formulaires adaptatifs. Pour savoir comment ces formulaires adaptatifs peuvent être modifiés, voir [Gestion des métadonnées de formulaire](/help/forms/using/manage-form-metadata.md)

1. **Republication :**

   La ressource collée est différente de la ressource copiée. Vous pouvez le publier en tant que nouvelle ressource afin de le rendre disponible pour les utilisateurs finaux. Pour savoir comment publier une ressource, voir [Publication et annulation de la publication de formulaires](/help/forms/using/publishing-unpublishing-forms.md)
