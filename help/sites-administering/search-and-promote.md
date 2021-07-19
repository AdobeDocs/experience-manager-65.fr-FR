---
title: Intégration à Adobe Search & Promote
description: Découvrez comment appliquer l’intégration à Adobe Search&Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 33%

---

# Intégration à Adobe Search &amp; Promote{#integrating-with-adobe-search-promote}

Pour appeler le service Adobe Search&amp;Promote depuis votre site web, effectuez les opérations suivantes :

1. Indiquez l’URL du cloud.
1. Configurez la connexion au service Search&amp;Promote.
1. Ajouter les composants Search&amp;Promote au sidekick.
1. Utilisez les composants pour créer le contenu. (Voir [Ajout de fonctionnalités de Search &amp; Promote à une page web](/help/sites-authoring/search-and-promote.md).)
1. Ajout de bannières à vos pages. Les images de bannière sont sensibles aux données Search&amp;Promote.
1. Générez un plan du site pour l’utilisation du service Search&amp;Promote.

>[!NOTE]
>
>Si vous utilisez Search &amp; Promote avec une configuration de proxy personnalisée, vous devez configurer les deux configurations de proxy client HTTP, car certaines fonctionnalités d’Adobe Experience Manager utilisent les API 3.x et d’autres les API 4.x :
>
>* La version 3.x est configurée avec [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* La version 4.x est configurée avec [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Modification de l’URL du service Search &amp; Promote {#changing-the-search-promote-service-url}

L’URL par défaut configurée pour le service Search &amp; Promote est `https://searchandpromote.omniture.com/px/`. Pour utiliser un autre service, utilisez la console OSGi afin de spécifier une autre URL.

1. Ouvrez la console OSGi et sélectionnez l’onglet **[!UICONTROL Configuration]** . ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Sélectionnez l’élément Configuration de la Search &amp; Promote Day CQ .
1. Saisissez l’URL dans la zone URI du serveur distant, puis sélectionnez **[!UICONTROL Enregistrer]**.

## Configurer la connexion à Search &amp; Promote {#configuring-the-connection-to-search-promote}

Configurez une ou plusieurs connexions à Search&amp;Promote afin que vos pages web puissent interagir avec le service. Pour vous connecter, vous avez besoin du numéro d’identification et de compte du membre de votre compte Search&amp;Promote.

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > sélectionnez **[!UICONTROL Cloud Services]**.

   Si vous vous trouvez sur un ordinateur local, l’URL du tableau de bord ressemble à ce qui suit :

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Sur la page Cloud Services, sélectionnez le lien du Search &amp; Promote d’Adobe ou l’icône de Search &amp; Promote.

1. Si vous configurez Adobe Search &amp; Promote pour la première fois, sélectionnez **[!UICONTROL Configurer maintenant]** pour ouvrir le panneau Créer une configuration .

   Pour en savoir plus sur Search &amp; Promote, sélectionnez **[!UICONTROL En savoir plus]**.

   ![](assets/chlimage_1-59.png)

1. Saisissez un **[!UICONTROL Titre]** reconnaissable par les auteurs de pages, et saisissez un **[!UICONTROL Nom]** unique.
1. Sélectionnez **[!UICONTROL Créer]**.

   De plus, la configuration nouvellement créée apparaît sous **Configurations disponibles** dans l’élément de liste Adobe Search&amp;Promote **Tableau de bord Services cloud**.

   ![](assets/chlimage_1-60.png)

1. Dans la boîte de dialogue **[!UICONTROL Modifier le composant]**, ajoutez les éléments suivants aux champs.

   * **ID de membre**
   * **Numéro de compte**

   >[!NOTE]
   >
   >Pour obtenir ces informations **vous-même,** vous devez d’abord vous connecter à
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >à l’aide de vos identifiants Search&amp;Promote (adresse électronique/mot de passe) valides.
   >Ensuite, vous devez consulter votre URL dans la barre d’adresse de votre navigateur, qui doit ressembler à ceci :
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Où :**
   >
   >    * **** XXXXXXXXcorrespond à votre** ID de membre**
   >    * **** spYYYYYYYcorrespond à votre numéro de  **compte**


1. Sélectionnez **[!UICONTROL Se connecter à Search &amp; Promote]**.

   Lorsque le message de réussite de la connexion s’affiche, sélectionnez **[!UICONTROL OK]**.

   (Après la connexion, le texte du bouton passe à** Reconnecter à Search &amp; Promote**.)

1. **[!UICONTROL Cliquez sur OK]**. La page Paramètres de Search &amp; Promote s’affiche pour la configuration que vous avez créée.

## Configuration du centre de données {#configuring-the-data-center}

Si votre compte Search &amp; Promote se trouve en Asie ou en Europe, vous devez modifier le centre de données par défaut afin qu’il pointe vers le bon (le centre de données par défaut est destiné aux comptes nord-américains).

**Pour configurer le centre de données :**

1. Accédez à la console web à l’adresse `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. En fonction de l’emplacement du serveur, redéfinissez l’URI sur l’une des URI suivantes :

   * Amérique du Nord : [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA : [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC : [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Sélectionnez **[!UICONTROL Enregistrer]**.

## Ajouter les composants Search&amp;Promote au sidekick {#adding-search-promote-components-to-sidekick}

En mode création, modifiez un composant **par** pour autoriser les composants Search&amp;Promote dans le sidekick. (Voir la documentation [Composants](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) pour en savoir plus.)

Pour plus d’informations sur l’utilisation des composants, voir [Ajout de fonctionnalités de Search &amp; Promote à une page web](/help/sites-authoring/search-and-promote.md).

## Spécification du service de Search &amp; Promote utilisé par vos pages {#specifying-the-search-promote-service-that-your-pages-use}

Configurez les pages web afin qu’elles utilisent un service Search&amp;Promote spécifique. Les composants Search&amp;Promote utilisent automatiquement le service de leur page hôte.

Lorsque vous configurez les propriétés Search&amp;Promote d’une page, toutes les pages enfants héritent des paramètres. Si nécessaire, vous pouvez configurer les pages enfants pour remplacer les paramètres hérités.

>[!NOTE]
>
>La connexion au service doit être préalablement configurée. (Voir [Configuration de la connexion à Search&amp;Promote](#connection).)

1. Ouvrez la boîte de dialogue **[!UICONTROL Propriétés de la page]**. Par exemple, sur la page** Sites Web**, cliquez avec le bouton droit de la souris sur la page et sélectionnez **[!UICONTROL Propriétés]**.
1. Sélectionnez l’onglet **[!UICONTROL Services cloud]**.
1. Pour désactiver l’héritage des configurations de services cloud d’une page parente, sélectionnez l’icône de cadenas en regard du chemin d’héritage.

   ![](assets/sandpinheritpadlock.png)

1. Sélectionnez **[!UICONTROL Ajouter un service]**.
1. Sélectionnez **[!UICONTROL Adobe de Search &amp; Promote]**, puis **[!UICONTROL OK]**.
1. Sélectionnez la configuration de la connexion pour votre compte Search &amp; Promote, puis cliquez sur **OK**.

## Flux de produit {#product-feed}

L&#39;intégration de Search &amp; Promote permet d&#39;effectuer les opérations suivantes :

* Utilisez l’API eCommerce, indépendamment de la structure de référentiel sous-jacente et de la plateforme commerciale.
* Utilisez la fonction Connecteur d’index de Search &amp; Promote pour qu’un flux de produits soit disponible au format XML.
* Utilisez la fonction de contrôle à distance de Search &amp; Promote si vous souhaitez effectuer des demandes à la demande ou planifiées du flux de produits.
* Génération de flux pour différents comptes de Search &amp; Promote, configurés en tant que configurations de services cloud.

Pour plus d’informations, voir [Flux de produits](/help/sites-administering/product-feed.md).
