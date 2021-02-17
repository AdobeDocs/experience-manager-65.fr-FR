---
title: Flux de produit
seo-title: Flux de produit
description: Découvrez-en davantage sur le flux de produits AEM.
seo-description: Découvrez-en davantage sur le flux de produits AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 71%

---


# Flux de produit {#product-feed}

AEM s’intègre à [Search &amp; Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) et vous permet de :

* d’utiliser l’API eCommerce, indépendamment de la structure de référentiel et de la plateforme de commerce sous-jacentes ;
* de tirer parti de la fonction de connecteur d’index de Search&amp;Promote pour constituer un flux de produit au format XML ;
* de tirer parti de la fonction de contrôle à distance de Search&amp;Promote pour effectuer des requêtes à la demande ou planifiées du flux de produit ;
* de générer des flux pour différents comptes Search&amp;Promote, configurés comme configurations de services cloud.

Vous devez disposer d&#39;un compte valide et [configurer la connexion à Search &amp; Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). Vous devez également vérifier que vous utilisez le centre de données [correct](/help/sites-administering/search-and-promote.md#configuring-the-data-center) et vous assurer que l&#39;URI de serveur **distant **est configuré.

## Configuration du flux de produit {#set-up-the-product-feed}

Vous devez d’abord saisir une racine de site web et un attribut d’identifiant. Pour ce faire :

1. Accédez à la configuration de Search&amp;Promote.
1. Cliquez sur **[!UICONTROL Modifier]**.
1. Cliquez sur l’onglet **[!UICONTROL Configuration des flux du connecteur d’index]**.
1. Saisissez l&#39;attribut **[!UICONTROL racine du site Web]** et **[!UICONTROL Identificateur]**.

   >[!NOTE]
   >
   >La **[!UICONTROL racine du site Web]** est la racine de votre site Web de commerce électronique, par exemple `/content/geometrixx-outdoors/en`.
   >
   >L&#39;attribut **[!UICONTROL Identifier]** est une propriété JCR qui identifie de manière unique le produit : `identifier`.

1. Cliquez sur **[!UICONTROL OK]**.

Vous devez également modifier deux configurations dans la console web pour générer des flux de produit.

### Configuration de la mise en œuvre du moteur de recherche de produits Search&amp;Promote Day CQ pour Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Accédez à [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cliquez sur **[!UICONTROL Configuration de la mise en œuvre du moteur de recherche de produits Search&amp;Promote Day CQ pour Geometrixx]**.
1. Spécifiez le numéro de compte Search&amp;Promote auquel ce moteur de recherche est lié. Il sera utilisé pour rechercher une configuration de services cloud utilisée par ce moteur de recherche.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

### Configuration du générateur de flux de produits Search&amp;Promote Day CQ pour Geometrixx  {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Accédez à [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cliquez sur **[!UICONTROL Configuration de la mise en œuvre du générateur de flux de produits Search&amp;Promote Day CQ pour Geometrixx]**.
1. Spécifiez le numéro de compte Search&amp;Promote auquel ce générateur est lié. Il sera utilisé pour rechercher une configuration de services cloud utilisée par ce générateur.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Planification du flux de produit  {#schedule-the-product-feed}

Pour activer la génération de flux planifiée, vous devez configurer le planificateur.
Un planificateur est configuré comme configuration enfant de votre configuration de services cloud de Search&amp;Promote.

1. Accédez à la configuration de Search&amp;Promote.
1. Cliquez sur **[!UICONTROL +]** en regard de **[!UICONTROL Configuration du planificateur]**.
1. Saisissez un **[!UICONTROL Titre]** reconnaissable aux auteurs de pages et un **[!UICONTROL Nom]** unique.
1. Cliquez sur **[!UICONTROL Créer]**. Une boîte de dialogue s’ouvre.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Saisissez le **[!UICONTROL mot de passe de contrôle à distance]**. Il s’agit du mot de passe que vous avez configuré dans votre compte Search&amp;Promote.

   >[!NOTE]
   >
   >Il ne s’agit pas du mot de passe de votre compte Search&amp;Promote. Vous pouvez trouver et modifier ce mot de passe en vous connectant à votre compte de Search &amp; Promote et en accédant à **[!UICONTROL Index]** puis à **[!UICONTROL Remote control]**.

1. Cochez la case **[!UICONTROL Activer la planification]**.
1. Sélectionnez une **[!UICONTROL planification]**. Il s’agit de la planification de génération de flux.
1. Cochez ou non **[!UICONTROL Indexation à la demande]**. Cette fonction sert à appeler manuellement l’index Search&amp;Promote. Si **[!UICONTROL Demander le flux de produits complet]** est coché, le Search &amp; Promote demandera un flux de produits complet. Dans le cas contraire, un flux de produits incrémentiel est demandé.

   >[!NOTE]
   >
   >La fonction d’indexation à la demande utilise la fonction de contrôle à distance de Search&amp;Promote. Lorsqu’une d’indexation distante est appelée, l’indexation ne commence pas immédiatement, mais une requête d’indexation est publiée vers Search&amp;Promote à l’aide de la fonction de contrôle à distance.

1. Cliquez sur **[!UICONTROL OK]**.

Maintenant que vous avez tout configuré, vous pouvez voir une page XML contenant tous les produits sous la racine du site Web configurée : [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
