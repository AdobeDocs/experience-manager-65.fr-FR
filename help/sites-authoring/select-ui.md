---
title: Choix de l’interface utilisateur
seo-title: Choix de l’interface utilisateur
description: Configurez l’interface que vous utiliserez pour travailler dans AEM.
seo-description: Configurez l’interface que vous utiliserez pour travailler dans AEM.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 82%

---


# Choix de l’interface utilisateur{#selecting-your-ui}

Bien que l’IU tactile soit désormais l’IU standard et que la parité des fonctions soit presque atteinte pour ce qui est de l’administration et de la modification des sites, il peut arriver que l’utilisateur souhaite passer à l’[IU classique](/help/sites-classic-ui-authoring/classicui.md). Pour ce faire, plusieurs possibilités s’offrent à lui.

>[!NOTE]
>
>Pour plus d’informations sur l’état de parité des fonctionnalités avec l’IU classique, voir le document [Parité des fonctionnalités de l’IU tactile](/help/release-notes/touch-ui-features-status.md).

Vous pouvez choisir quelle IU utiliser à divers emplacements :

* [Configuration de l’IU par défaut pour votre instance](#configuring-the-default-ui-for-your-instance)
Détermine l’IU affichée par défaut lorsque l’utilisateur se connecte. L’utilisateur peut cependant sélectionner une autre IU pour le compte ou la session en cours.

* [Définition de l’IU de création classique pour votre compte](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account) 
Détermine l’IU utilisée par défaut lors de la modification des pages. Cependant, l’utilisateur peut ignorer ce paramètre et sélectionner une autre IU pour le compte ou la session en cours.

* [Activation de l’IU classique pour la session en cours](#switching-to-classic-ui-for-the-current-session)
Active l’IU classique pour la session en cours.

* En cas de [création de pages, le système procède à certains remplacements dans la relation à l’interface utilisateur](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Plusieurs options de basculement vers l’interface utilisateur classique ne sont pas immédiatement disponibles. Elles doivent être configurées spécifiquement pour votre instance.
>
>Voir [Activation de l’accès à l’interface utilisateur classique](/help/sites-administering/enable-classic-ui.md) pour plus d’informations.

>[!NOTE]
>
>Les instances mises à niveau à partir d’une version précédente conservent l’IU classique pour la création de pages.
>
>Après la mise à niveau, la création de pages ne sera pas automatiquement basculée vers l’interface utilisateur tactile, mais vous pouvez la configurer à l’aide du [service de configuration OSGi](/help/sites-deploying/configuring-osgi.md) du **service de mode d’interface utilisateur de création WCM** (service `AuthoringUIMode`). Voir [IU par défaut en fonction de l’éditeur](#ui-overrides-for-the-editor).

## Configuration de l’IU par défaut pour votre instance {#configuring-the-default-ui-for-your-instance}

Un administrateur système peut configurer l’IU qui s’affiche au démarrage et lors de la connexion à l’aide du [mappage à la racine](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Les paramètres par défaut de l’utilisateur ou les paramètres de la session peuvent remplacer ce comportement.

## Définition de l’IU de création classique pour votre compte {#setting-classic-ui-authoring-for-your-account}

Chaque utilisateur peut accéder à ses [préférences utilisateur](/help/sites-authoring/user-properties.md#userpreferences) pour définir s’il souhaite utiliser l’IU classique pour la création de pages (au lieu de l’IU par défaut).

Les paramètres de la session peuvent remplacer ce comportement.

## Activation de l’IU classique pour la session en cours  {#switching-to-classic-ui-for-the-current-session}

Ainsi, si l’IU tactile est activée sur un ordinateur de bureau, les utilisateurs peuvent souhaiter revenir à l’IU classique (ordinateur de bureau uniquement). Plusieurs méthodes permettent de basculer vers l’IU classique pour la session en cours :

* **Liens de navigation**

   >[!CAUTION]
   >
   >Cette option de basculement vers l’interface utilisateur classique n’est pas immédiatement disponible. Elle doit être configurée spécifiquement pour votre instance.
   >
   >
   >Voir [Activation de l’accès à l’interface utilisateur classique](/help/sites-administering/enable-classic-ui.md) pour plus d’informations.

   Si cette option est activée, lorsque vous faites passer le pointeur de la souris sur une console appropriée, une icône s’affiche (symbole d’un moniteur). En appuyant/cliquant sur cette dernière, vous accédez à l’emplacement correspondant dans l’IU classique.

   Par exemple, les liens de **Sites** à **siteadmin** :

   ![syui-01](assets/syui-01.png)

* **URL**

   L’interface utilisateur classique est accessible à l’aide de l’URL de l’écran de bienvenue à l’adresse `welcome.html`. Par exemple :

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
>Cette option de basculement vers l’interface utilisateur classique n’est pas immédiatement disponible. Elle doit être configurée spécifiquement pour votre instance.
>
>Voir [Activation de l’accès à l’interface utilisateur classique](/help/sites-administering/enable-classic-ui.md) pour plus d’informations.

Si cette option est activée, l’option **Ouvrir l’IU classique** est disponible dans la boîte de dialogue **Informations sur la page** :

![syui-02](assets/syui-02.png)

### UI Overrides for the Editor {#ui-overrides-for-the-editor}

Les paramètres définis par un utilisateur ou un administrateur du système peuvent être remplacés par les paramètres système en cas de création de page.

* Lors de la création de pages :

   * L’utilisation de l’éditeur classique est forcée lors de l’accès à la page à l’aide de `cf#` dans l’URL. Par exemple :
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * L’utilisation de l’éditeur tactile est forcée lors de l’utilisation de `/editor.html` dans l’URL ou lors de l’utilisation d’un périphérique tactile. Par exemple :
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Tout recours forcé à un certain éditeur est temporaire et valide uniquement pour la session en cours.

   * Un jeu de cookies sera défini selon que l’option tactile ( `editor.html`) ou classique ( `cf#`) est utilisée ou non.

* Lors de l&#39;ouverture de pages par `siteadmin`, des vérifications seront effectuées pour vérifier l&#39;existence de :

   * présence du cookie ;
   * préférence utilisateur ;
   * en l’absence de tels paramètres, l’IU définie par défaut dans la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) du service **WCM Authoring UI Mode** (service `AuthoringUIMode`) est utilisée.

>[!NOTE]
>
>Si [un utilisateur a déjà défini une préférence pour la création de pages](#settingthedefaultauthoringuiforyouraccount), ce paramètre est conservé lors de la modification de la propriété OSGi.

>[!CAUTION]
>
>En raison de l’utilisation des cookies, comme indiqué ci-dessus, les opérations suivantes ne sont pas recommandées :
>
>* Modifier manuellement l’URL : une URL non standard risque de générer une situation inconnue et une absence de fonctionnalité.
>* Ouvrir les deux éditeurs en même temps ; dans des fenêtres distinctes, par exemple.

