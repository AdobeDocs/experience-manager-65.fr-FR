---
title: Sélectionner votre interface utilisateur dans AEM
description: Configurez l’interface que vous utilisez pour travailler dans AEM.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '745'
ht-degree: 100%

---

# Choisir votre interface utilisateur{#selecting-your-ui}

Bien que l’UI tactile soit maintenant l’UI standard et que la parité des fonctionnalités ait presque été atteinte lors de l’administration et de la modification des sites, il peut arriver que l’utilisateur ou l’utilisatrice souhaite passer à l’[UI classique](/help/sites-classic-ui-authoring/classicui.md). Il existe plusieurs options pour ce faire.

>[!NOTE]
>
>Pour plus d’informations sur le statut de parité des fonctionnalités avec l’IU classique, consultez le document [Parité des fonctionnalités de l’IU tactile](/help/release-notes/touch-ui-features-status.md).

Il existe différents emplacements où vous pouvez définir l’interface utilisateur à utiliser :

* [Configuration de l’IU par défaut pour votre instance](#configuring-the-default-ui-for-your-instance)
Détermine l’IU affichée par défaut lorsque l’utilisateur se connecte. L’utilisateur peut cependant sélectionner une autre IU pour le compte ou la session en cours.

* [Définition de l’IU de création classique pour votre compte](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account) 
Détermine l’IU utilisée par défaut lors de la modification des pages. Cependant, l’utilisateur peut ignorer ce paramètre et sélectionner une autre IU pour le compte ou la session en cours.

* [Activation de l’IU classique pour la session en cours](#switching-to-classic-ui-for-the-current-session)
Active l’IU classique pour la session en cours.

* Dans le cas de la [création de pages, le système effectue certains remplacements dans la relation avec l’interface utilisateur](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Plusieurs options permettant de passer à l’UI classique ne sont pas immédiatement prêtes à l’emploi. Elles doivent être configurées spécifiquement pour votre instance.
>
>Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

>[!NOTE]
>
>Les instances mises à niveau à partir d’une version précédente conservent l’IU classique pour la création de pages.
>
>Après la mise à niveau, la création de pages ne bascule pas automatiquement vers l’IU tactile. Vous pouvez cependant configurer ce basculement à l’aide de la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) du **service Mode d’IU de création de la gestion de contenu web** (service `AuthoringUIMode`). Consultez la section [IU par défaut en fonction de l’éditeur](#ui-overrides-for-the-editor).

## Configurer l’UI par défaut pour votre instance {#configuring-the-default-ui-for-your-instance}

Un administrateur ou une administratrice système peut configurer l’interface utilisateur qui s’affiche au démarrage et lors de la connexion à l’aide du [mappage racine](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Ceci peut être remplacé par les paramètres par défaut de l’utilisateur ou de l’utilisatrice, ou les paramètres de session.

## Définir l’UI classique pour la création sur votre compte {#setting-classic-ui-authoring-for-your-account}

Chaque utilisateur et utilisatrice peut accéder à ses [préférences](/help/sites-authoring/user-properties.md#userpreferences) pour définir si l’UI classique doit être utilisée pour la création de pages (au lieu de l’UI par défaut).

Ceci peut être remplacé par les paramètres de session.

## Passer à l’UI classique pour la session en cours {#switching-to-classic-ui-for-the-current-session}

Ainsi, si l’IU tactile est activée sur un ordinateur de bureau, les utilisateurs peuvent souhaiter revenir à l’IU classique (ordinateur de bureau uniquement). Plusieurs méthodes permettent de passer à l’UI classique pour la session en cours :

* **Liens de navigation**

   >[!CAUTION]
   >
   >Cette option permettant de passer à l’UI classique n’est pas immédiatement disponible, elle doit être configurée spécifiquement pour votre instance.
   >
   >
   >Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

   Si cette option est activée, lorsque vous faites passer le pointeur de la souris sur une console appropriée, une icône s’affiche (symbole d’écran). En appuyant ou cliquant sur cette dernière, vous accédez à l’emplacement correspondant dans l’IU classique.

   Par exemple, les liens de **Sites** à **siteadmin** :

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
>Cette option permettant de passer à l’UI classique n’est pas immédiatement disponible, elle doit être configurée spécifiquement pour votre instance.
>
>Pour plus d’informations, reportez-vous à la section [Activation de l’accès à l’IU classique](/help/sites-administering/enable-classic-ui.md).

Si cette option est activée, l’option **Ouvrir l’IU classique** est disponible dans la boîte de dialogue **Informations sur la page** :

![syui-02](assets/syui-02.png)

### Remplacements d’UI pour l’éditeur {#ui-overrides-for-the-editor}

Les paramètres définis par un utilisateur ou une utilisatrice, ou un administrateur ou une administratrice système, peuvent être remplacés par le système dans le cas de la création de pages.

* Lors de la création de pages :

   * le recours à l’éditeur classique est forcé lors de l’accès à la page à l’aide de `cf#` dans l’URL. Par exemple :
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Le recours à l’éditeur tactile est forcé lors de l’utilisation de `/editor.html` dans l’URL ou lors de l’utilisation d’un appareil tactile. Par exemple :
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Tout recours forcé à un certain éditeur est temporaire et valide uniquement pour la session en cours.

   * Un jeu de cookies est défini selon qu’il s’agit de l’éditeur tactile (`editor.html`) ou classique (`cf#`).

* Lors de l’ouverture de pages en tant que `siteadmin`, plusieurs contrôles ont lieu :

   * Présence du cookie
   * Préférence utilisateur
   * En l’absence de tels paramètres, l’IU définie par défaut dans la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) du service **Mode d’IU de création de la gestion de contenu web** (service `AuthoringUIMode`) est utilisée.

>[!NOTE]
>
>Si [un utilisateur ou une utilisatrice a déjà défini une préférence pour la création de pages](#settingthedefaultauthoringuiforyouraccount), elle ne sera pas remplacée par la modification de la propriété OSGi.

>[!CAUTION]
>
>En raison de l’utilisation de cookies, comme décrit plus haut, il n’est pas recommandé de :
>
>* Modifier manuellement l’URL : une URL non standard peut entraîner une situation inconnue et un manque de fonctionnalité.
>* Ouvrir les deux éditeurs en même temps ; dans des fenêtres distinctes, par exemple.

