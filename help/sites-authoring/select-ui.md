---
title: Sélectionner votre interface utilisateur dans AEM
description: Configurez l’interface que vous utilisez pour travailler dans AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 43%

---

# Choisir votre interface utilisateur{#selecting-your-ui}

L’interface utilisateur tactile de Adobe Experience Manager (AEM) est désormais l’interface utilisateur standard et la parité des fonctionnalités a presque été atteinte avec l’administration et la modification des sites. Cependant, il peut arriver que l’utilisateur souhaite passer à la variable [IU classique](/help/sites-classic-ui-authoring/classicui.md). Il existe plusieurs options pour ce faire.

>[!NOTE]
>
>Pour plus d’informations sur le statut de parité des fonctionnalités avec l’IU classique, consultez le document [Parité des fonctionnalités de l’IU tactile](/help/release-notes/touch-ui-features-status.md).

Il existe différents emplacements où vous pouvez définir l’interface utilisateur à utiliser :

* [Configuration de l’IU par défaut pour votre instance](#configuring-the-default-ui-for-your-instance)
Cette option définit l’interface utilisateur par défaut à afficher lors de la connexion de l’utilisateur. L’utilisateur peut être en mesure de remplacer cela et sélectionner une autre interface utilisateur pour son compte ou la session en cours.

* [Définition de la création d’interfaces utilisateur classiques pour votre compte](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
L’interface utilisateur est définie comme valeur par défaut lors de la modification des pages, bien que l’utilisateur puisse remplacer cette option et sélectionner une autre interface utilisateur pour son compte ou la session en cours.

* [Passage à l’IU classique pour la session en cours](#switching-to-classic-ui-for-the-current-session)
Passe à l’IU classique pour la session en cours.

* Pour le cas de [création de pages, le système effectue certains remplacements dans la relation avec l’interface utilisateur.](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Plusieurs options permettant de passer à l’IU classique ne sont pas immédiatement disponibles clé en main. Elles doivent être configurées pour votre instance.
>
>Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

>[!NOTE]
>
>Les instances mises à niveau à partir d’une version précédente conservent l’IU classique pour la création de pages.
>
>Après la mise à niveau, la création de pages n’est pas automatiquement basculée vers l’interface utilisateur tactile, mais vous pouvez la configurer à l’aide de l’option [Configuration OSGi](/help/sites-deploying/configuring-osgi.md) de **Service WCM Author UI Mode** ( `AuthoringUIMode` ). Consultez la section [IU par défaut en fonction de l’éditeur](#ui-overrides-for-the-editor).

## Configurer l’UI par défaut pour votre instance {#configuring-the-default-ui-for-your-instance}

Un administrateur ou une administratrice système peut configurer l’interface utilisateur qui s’affiche au démarrage et lors de la connexion à l’aide du [Mappage racine](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Ceci peut être remplacé par les paramètres par défaut de l’utilisateur ou de l’utilisatrice, ou les paramètres de session.

## Définir l’UI classique pour la création sur votre compte {#setting-classic-ui-authoring-for-your-account}

Chaque utilisateur peut accéder à ses propres [préférences utilisateur](/help/sites-authoring/user-properties.md#userpreferences) pour définir s’ils souhaitent utiliser l’IU classique pour la création de pages, au lieu de l’IU par défaut.

Ceci peut être remplacé par les paramètres de session.

## Passer à l’UI classique pour la session en cours {#switching-to-classic-ui-for-the-current-session}

Lorsque vous utilisez l’IU tactile, les utilisateurs de bureau peuvent souhaiter revenir à l’IU classique (ordinateur de bureau uniquement). Plusieurs méthodes permettent de passer à l’UI classique pour la session en cours :

* **Liens de navigation**

  >[!CAUTION]
  >
  >Cette option de basculement vers l’IU classique n’est pas disponible immédiatement, prête à l’emploi. Elle doit être configurée pour votre instance.
  >
  >
  >Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

  Si cette option est activée, une icône s’affiche (un symbole de moniteur) chaque fois que vous pointez sur une console appropriée. Appuyez/cliquez sur cette option pour ouvrir l’emplacement approprié dans l’IU classique.

  Par exemple, les liens de **Sites** to **siteadmin**:

  ![syui-01](assets/syui-01.png)

* **URL**

  Pour accéder à l’IU classique, utilisez l’URL de l’écran d’accueil à l’adresse `welcome.html`. Par exemple :

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >L’IU tactile est accessible via `sites.html`. Par exemple :
  >
  >
  >`https://localhost:4502/sites.html`

### Activation de l’IU classique en cours de modification de page {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Cette option de basculement vers l’IU classique n’est pas disponible immédiatement, prête à l’emploi. Elle doit être configurée pour votre instance.
>
>Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

Si cette option est activée, l’option **Ouvrir l’IU classique** est disponible dans la boîte de dialogue **Informations sur la page** :

![syui-02](assets/syui-02.png)

### Remplacements d’UI pour l’éditeur {#ui-overrides-for-the-editor}

Les paramètres définis par un utilisateur ou un administrateur système peuvent être remplacés par le système en cas de création de pages.

* Lors de la création de pages :

   * le recours à l’éditeur classique est forcé lors de l’accès à la page à l’aide de `cf#` dans l’URL. Par exemple :
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Le recours à l’éditeur tactile est forcé lors de l’utilisation de `/editor.html` dans l’URL ou lors de l’utilisation d’un appareil tactile. Par exemple :
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Tout recours forcé à un certain éditeur est temporaire et valide uniquement pour la session en cours.

   * Un jeu de cookies est défini selon qu’il est tactile ou non ( `editor.html`) ou classique ( `cf#`) est utilisée.

* Lors de l’ouverture de pages par `siteadmin`, des vérifications sont effectuées pour vérifier l’existence des éléments suivants :

   * Présence du cookie
   * Préférence utilisateur
   * S’il n’en existe aucun, il utilise par défaut les définitions définies dans le [Configuration OSGi](/help/sites-deploying/configuring-osgi.md) de **Service WCM Author UI Mode** ( `AuthoringUIMode` ).

>[!NOTE]
>
>If [un utilisateur a déjà défini une préférence pour la création de pages ;](#settingthedefaultauthoringuiforyouraccount), qui n’est pas remplacé par la modification de la propriété OSGi.

>[!CAUTION]
>
>En raison de l’utilisation de cookies, comme décrit plus haut, il n’est pas recommandé de :
>
>* Modifier manuellement l’URL : une URL non standard peut entraîner une situation inconnue et un manque de fonctionnalité.
>* Ouvrir les deux éditeurs en même temps ; dans des fenêtres distinctes, par exemple.
