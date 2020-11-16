---
title: Choix de l’interface utilisateur
seo-title: Choix de l’interface utilisateur
description: Pour offrir davantage de confort à ces utilisateurs, l’IU destinée aux écrans tactiles permet de basculer vers l’IU classique lorsque cela s’avère nécessaire.
seo-description: Pour offrir davantage de confort à ces utilisateurs, l’IU destinée aux écrans tactiles permet de basculer vers l’IU classique lorsque cela s’avère nécessaire.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---


# Choix de l’interface utilisateur{#selecting-your-ui}

Comme l’interface utilisateur tactile remplace l’interface utilisateur classique, l’utilisateur ou l’administrateur de l’instance AEM doit prendre une principale décision de continuer à utiliser l’interface utilisateur classique. L’interface utilisateur classique n’étant plus conservée, l’utilisateur auteur ne peut plus simplement passer de l’interface utilisateur classique à l’équivalent dans l’interface utilisateur tactile.

Pour offrir davantage de confort à ces utilisateurs, l’IU destinée aux écrans tactiles permet de basculer vers l’IU classique lorsque cela s’avère nécessaire. Pour plus d’informations, voir [Choix de l’interface utilisateur](/help/sites-authoring/select-ui.md) dans la documentation de création standard.

>[!NOTE]
>
>Les instances mises à niveau à partir d’une version précédente conservent l’IU classique pour la création de pages.
>
>After upgrade, page authoring will not be automatically switched to the touch-enabled UI, but you can configure this usingthe[OSGi configuration](/help/sites-deploying/configuring-osgi.md) of the **WCM Authoring UI Mode Service** ( `AuthoringUIMode` service). Voir [IU par défaut en fonction de l’éditeur](#uioverridesfortheeditor).

## Configuration de l’IU par défaut pour votre instance {#configuring-the-default-ui-for-your-instance}

Un administrateur système peut configurer l’IU qui s’affiche au démarrage et lors de la connexion à l’aide du [mappage à la racine](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Les paramètres par défaut de l’utilisateur ou les paramètres de la session peuvent remplacer ce comportement.
