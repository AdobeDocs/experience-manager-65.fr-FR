---
title: Fragments de contenu - Navigateur de configurations
description: Découvrez comment activer certaines fonctionnalités de fragments de contenu dans l’explorateur de configurations afin d’utiliser les puissantes fonctionnalités de diffusion en mode découplé d’Adobe Experience Manager.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
subfeature_v2:
  - id: b7f5d1e0-aa2f-4a55-83f4-c2b35a8bd3a7
    internal-label: Content fragments
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 100%
---
# Fragments de contenu - Navigateur de configurations{#content-fragments-configuration-browser}

Découvrez comment activer certaines fonctionnalités de fragments de contenu dans l’explorateur de configurations afin d’utiliser les puissantes fonctionnalités de diffusion en mode découplé d’Adobe Experience Manager.

## Activation de la fonctionnalité de fragments de contenu pour votre instance {#enable-content-fragment-functionality-instance}

Avant d’utiliser les fragments de contenu, utilisez l’**explorateur de configurations** pour activer les éléments suivants :

* **Modèles de fragment de contenu** – obligatoire
* **Requêtes persistantes GraphQL** – facultatif

>[!CAUTION]
>
>Si vous n’activez pas les **modèles de fragment de contenu** :
>
>* L’option **Créer** ne sera pas disponible pour la création de modèles.
>* Vous ne pouvez pas [sélectionner la configuration Sites pour créer le point d’entrée associé](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

Pour activer la fonctionnalité de fragment de contenu, procédez comme suit :

* activez l’utilisation de la fonctionnalité de fragment de contenu par le biais de l’explorateur de configurations ;
* appliquer la configuration à votre dossier de ressources.

### Activation de la fonctionnalité de fragments de contenu dans l’explorateur de configurations {#enable-content-fragment-functionality-in-configuration-browser}

Pour utiliser certaines [fonctionnalités de fragments de contenu](#creating-a-content-fragment-model), vous **devez** d’abord les activer par le biais de l’**explorateur de configurations** :

>[!NOTE]
>
>Pour plus d’informations, consultez [Explorateur de configurations](/help/sites-administering/configurations.md#using-configuration-browser).

1. Accédez à **Outils**, **Général**, puis ouvrez l’**Explorateur de configurations**.

1. Utilisez le bouton **Créer** pour ouvrir la boîte de dialogue.

   1. Spécifiez un **Titre**.
   1. Pour activer leur utilisation, sélectionnez
      * **Modèles de fragment de contenu**
      * **Requêtes persistantes GraphQL**

      ![Définir la configuration](assets/cfm-conf-01.png)

1. Sélectionnez **Créer** pour enregistrer la définition.

<!-- 1. Select the location appropriate to your website. -->

### Application de la configuration à votre dossier de ressources {#apply-the-configuration-to-your-assets-folder}

Lorsque la configuration **global** est activée pour la fonctionnalité de fragments de contenu, elle s’applique à tout dossier Ressources.

Pour utiliser d’autres configurations (c.-à-d. avec une exclusion globale) avec un dossier de ressources comparable, vous devez définir la connexion. Pour ce faire, utilisez **Configuration** sous l’onglet **Services cloud** des **Propriétés du dossier** du dossier approprié.

![Appliquer la configuration](assets/cfm-conf-02.png)
