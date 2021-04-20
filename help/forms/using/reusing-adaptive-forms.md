---
title: Réutilisation de formulaires adaptatifs
seo-title: Réutilisation de formulaires adaptatifs
description: Vous pouvez réutiliser un formulaire adaptatif existant afin d’en créer de nouveaux.
seo-description: Vous pouvez réutiliser un formulaire adaptatif existant afin d’en créer de nouveaux.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 75%

---


# Réutilisation de formulaires adaptatifs {#reusing-adaptive-forms}

## Présentation {#introduction}

Si vous souhaitez utiliser certaines des propriétés d’un formulaire adaptatif existant pour en générer un nouveau, il vous suffit d’utiliser la fonctionnalité de copier-coller. Vous pouvez, en outre, coller le nouveau formulaire adaptatif dans le dossier de votre choix. Toutes les propriétés de métadonnées sont répliquées ; les XFA et XSD relatifs aux formulaires adaptatifs basés sur XFA et XSD sont également copiés.

>[!NOTE]
>
>L’état et les détails de révision ne sont pas copiés. Par exemple, si votre formulaire adaptatif est copié après avoir été publié, le formulaire collé se trouve dans l’état « non publié ». De même, si un élément copié est en cours de révision, l’élément collé ne se trouve pas sous la même révision.

### Copie d’un formulaire adaptatif {#copy-an-adaptive-form}

Copiez un formulaire adaptatif en utilisant l’une des méthodes suivantes :

1. Cliquez sur l&#39;icône Copier ![aem6forms_copy](assets/aem6forms_copy.png) dans Actions rapides.

   >[!NOTE]
   >
   >Les actions rapides sont des éléments d’action qui sont affichés sur une vignette lors du pointage de la souris.

1. Sélectionnez le formulaire adaptatif. Le processus de sélection est différent pour chaque vue.

   Si vous êtes en vue de carte, passez en mode de sélection en cliquant sur l’icône ![aem6forms_check-circle](assets/aem6forms_check-circle.png) et cliquez sur tous les formulaires adaptatifs à copier.

   Si le mode Liste est actif, cochez les cases à cocher de tous les formulaires adaptatifs pour les sélectionner.

   >[!NOTE]
   >
   >Tous les éléments sélectionnés doivent être des formulaires adaptatifs, car la fonctionnalité de copier-coller n’est prise en charge que pour ces formulaires, et tous doivent figurer dans le même dossier.

   Après avoir sélectionné les actifs, cliquez sur l’icône de copie ![aem6forms_copy](assets/aem6forms_copy.png) présente dans la barre d’outils pour copier le formulaire adaptatif sélectionné.

### Coller un formulaire adaptatif {#paste-an-adaptive-form}

Cliquez sur l’action de copie pour quitter automatiquement le mode de sélection et rendre visible l’icône de collage ![aem6forms_coller](assets/aem6forms_paste.png). Accédez maintenant au chemin d’accès du dossier de votre choix et cliquez sur l’icône de collage ![aem6forms_coller](assets/aem6forms_paste.png) pour coller le formulaire adaptatif copié.

Si vous collez le formulaire dans le même dossier ou s’il existe déjà un autre fichier portant le même nom de nœud (avec lequel il est stocké dans le référentiel CRX) dans ce dossier cible, une unité est ajoutée au suffixe (par exemple, myaf devient myaf1 et si myaf1 existe déjà au même emplacement, myaf devient myaf2). Toutes les autres propriétés restent identiques au formulaire adaptatif d’origine.

Après avoir cliqué sur l’icône de collage ![aem6forms_coller](assets/aem6forms_paste.png), il se masquera à nouveau. Vous ne pouvez effectuer qu’une seule opération de copie à la fois. Pour créer une autre copie d’un même élément, copiez le à nouveau.

### Modification du contenu du nouveau formulaire adaptatif {#change-contents-of-new-adaptive-form}

Le contenu d’un formulaire adaptatif collé peut être modifié en utilisant les méthodes suivantes en vue de le rendre différent du formulaire copié :

1. **Modification des propriétés de métadonnées :** 

   Vous pouvez modifier les propriétés de métadonnées du formulaire adaptatif ; le titre et la description, par exemple. Pour plus d’informations sur les propriétés de métadonnées et sur la manière de les modifier, voir [Gestion des métadonnées de formulaire](/help/forms/using/manage-form-metadata.md).

1. **Modifiez XFA/XSD pour Forms adaptatif basé sur XFA/XSD :**

   Vous pouvez modifier le XFA/XSD utilisé dans les formulaires adaptatifs. Pour savoir comment ces formulaires adaptatifs peuvent être modifiés, reportez-vous à la section [Gestion des métadonnées de formulaire](/help/forms/using/manage-form-metadata.md) 

1. **Republier:**

   L’élément collé est différent de celui qui a été copié. Vous pouvez le publier en tant que nouvel élément afin de le mettre à la disposition des utilisateurs finaux. Pour savoir comment publier un élément, reportez-vous à la section [Publication et annulation de publication de formulaires](/help/forms/using/publishing-unpublishing-forms.md).

