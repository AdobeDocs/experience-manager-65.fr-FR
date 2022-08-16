---
title: Choix de l’interface utilisateur
seo-title: Selecting your UI
description: Pour offrir davantage de confort à ces utilisateurs, l’IU destinée aux écrans tactiles permet de basculer vers l’IU classique lorsque cela s’avère nécessaire.
seo-description: For convenience to authoring users, the touch-enabled UI does allow for switching to the classic UI when necessary.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 55%

---

# Choix de l’interface utilisateur{#selecting-your-ui}

Comme l’IU tactile remplace l’IU classique, l’utilisateur ou l’administrateur de l’instance AEM doit prendre une principale décision de continuer à utiliser l’IU classique. L’IU classique n’étant plus gérée, il n’est plus possible pour l’utilisateur de création de simplement passer de l’IU classique à l’IU équivalente dans l’IU tactile.

Pour offrir davantage de confort à ces utilisateurs, l’IU destinée aux écrans tactiles permet de basculer vers l’IU classique lorsque cela s’avère nécessaire. Pour plus d’informations, voir [Choix de l’interface utilisateur](/help/sites-authoring/select-ui.md) dans la documentation de création standard.

>[!NOTE]
>
>Les instances mises à niveau à partir d’une version précédente conservent l’IU classique pour la création de pages.
>
>Après la mise à niveau, la création de pages ne passe pas automatiquement à l’interface utilisateur tactile, mais vous pouvez la configurer à l’aide de la fonction[Configuration OSGi](/help/sites-deploying/configuring-osgi.md) de **Service WCM Author UI Mode** ( `AuthoringUIMode` ). Voir [IU par défaut en fonction de l’éditeur](#uioverridesfortheeditor).

## Configuration de l’IU par défaut pour votre instance {#configuring-the-default-ui-for-your-instance}

Un administrateur système peut configurer l’IU qui s’affiche au démarrage et lors de la connexion à l’aide du [mappage à la racine](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Les paramètres par défaut de l’utilisateur ou les paramètres de la session peuvent remplacer ce comportement.
