---
title: Configuration d’une page de redirection
seo-title: Configuring redirect page
description: Après avoir rempli un formulaire adaptatif, les utilisateurs peuvent être redirigés vers une page web que les auteurs de formulaires peuvent configurer lors de la création du formulaire.
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 69%

---

# Configuration d’une page de redirection{#configuring-redirect-page}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | Cet article |

Pour chaque formulaire, les auteurs peuvent configurer une page vers laquelle les utilisateurs seront redirigés après l’envoi du formulaire.

1. En mode d’édition, sélectionnez un composant, puis cliquez sur ![field-level](assets/field-level.png) > **Conteneur de formulaires adaptatifs**, puis cliquez sur ![cmppr](assets/cmppr.png).

1. Dans la barre latérale, cliquez sur **Envoi**.

1. Indiquez L’URL de la page de redirection sous Page de remerciement dans la section Envoyer. 
1. Sous Action Envoyer, vous pouvez éventuellement configurer le paramètre à transmettre à la page de redirection pour l’action Envoyer vers le point d’entrée REST.

![Configuration de la page de redirection](assets/thank-you-setting-1.png)

Configuration de la page de redirection

Les auteurs de formulaires peuvent utiliser les paramètres suivants qui sont transmis à la page de remerciement. Les paramètres `status` et `owner` sont transmis pour toutes les actions d’envoi disponibles. Outre ces deux paramètres, des paramètres supplémentaires sont transmis pour les actions d’envoi suivantes :

* **Action Stocker le contenu** (obsolète) : `contentPath`--le chemin d’accès du nœud dans le référentiel où sont stockées les données envoyées est transmis.

* **Action Stocker le PDF** (obsolète) : `contentPath`--des données envoyées et le chemin d’accès au nœud de stockage du fichier PDF dans le référentiel sont transmis.

* **Workflow Envoyer aux formulaires** : les paramètres de sortie renvoyés à partir du workflow des formulaires sont transmis.

* **Envoyer vers le point d’entrée REST** : les paramètres ajoutés pour la correspondance entre le champ et le paramètre sont transmis. Les paramètres `status` et `owner` ne sont pas transmis à cette action d’envoi. Pour en savoir plus, consultez [Configuration de l’action d’envoi Envoyer vers le point d’entrée REST](../../forms/using/configuring-submit-actions.md). 
