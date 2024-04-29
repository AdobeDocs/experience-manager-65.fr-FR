---
title: Fragments de contenu - Navigateur de configurations
description: Découvrez comment activer certaines fonctionnalités de fragments de contenu dans l’explorateur de configurations afin d’utiliser les puissantes fonctionnalités de diffusion en mode découplé d’Adobe Experience Manager.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '272'
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
