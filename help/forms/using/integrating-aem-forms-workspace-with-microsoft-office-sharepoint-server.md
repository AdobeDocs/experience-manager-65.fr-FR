---
title: Intégration d’AEM Forms Workspace à Microsoft Office SharePoint Server
seo-title: Intégration d’AEM Forms Workspace à Microsoft Office SharePoint Server
description: 'Vous pouvez intégrer AEM Forms Workspace à Microsoft Office SharePoint Server. '
seo-description: 'Vous pouvez intégrer AEM Forms Workspace à Microsoft Office SharePoint Server. '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 86%

---


# Intégration d’AEM Forms Workspace à Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Conditions préalables**

**Connaissances préalablesAvant de pouvoir ajouter AEM Forms Workspace à SharePoint Server, vous devez avoir accès à SharePoint Server avec les privilèges appropriés et connaître l’URL d’accès à Workspace.**
Les étapes ci-dessous supposent que vous connaissez SharePoint Server. Pour en savoir plus sur les composants Webpart de SharePoint Server, consultez Composants Webpart sous Windows SharePoint Services.

**Niveau d’utilisateur** Début

Vous pouvez utiliser AEM Forms Workspace en tant que composant Webpart dans Microsoft Office SharePoint Server (par exemple, Microsoft Office SharePoint Server 2007). Les utilisateurs peuvent accéder à AEM Forms Workspace lors de la connexion à votre serveur SharePoint à l’aide d’un navigateur Web pour offrir une expérience unifiée. Dans cet article, vous allez découvrir les étapes de base pour afficher AEM Forms Workspace en tant que composant Webpart dans Microsoft Office SharePoint Server. Vous pouvez exécuter les étapes décrites dans cet article pour offrir une expérience unifiée de sorte que les utilisateurs qui se connectent à votre serveur SharePoint puissent accéder à AEM Forms Workspace à partir du même port.

>[!NOTE]
>
>Les étapes mentionnées dans cet article sont spécifiques à Microsoft SharePoint Server 2007. Vous pouvez également configurer HTML Workspace avec d’autres versions prises en charge de Microsoft SharePoint.

## Intégrer AEM Forms Workspace à Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Effectuez les étapes suivantes pour intégrer AEM Forms Workspace à un composant Webpart :

1. Dans un navigateur Web, accédez au site SharePoint tel que, `https://[myMOSSserver]:44299/default.aspx` où `[myMOSSserver]` correspond au nom ou à l&#39;adresse IP du serveur SharePoint.

   >[!NOTE]
   >
   >44299 est le numéro de port par défaut pour le serveur Sharepoint. Le numéro de port varie en fonction de votre installation de SharePoint Server.

1. Dans le coin supérieur droit de la page Web, cliquez sur **Actions du site** et sélectionnez **Modifier la page**.
1. Cliquez sur le bouton **Ajouter un composant Webpart.**
1. Dans la boîte de dialogue Ajouter des composants Webpart - boîte de dialogue de la page Web, sous Divers, sélectionnez **Composant Webpart de la visionneuse de pages**, puis cliquez sur **Ajouter**.
1. Dans la zone Composant Webpart de la visionneuse de pages, cliquez sur **Modifier,** puis sélectionnez **Modifier le composant Webpart partagé**.

   >[!NOTE]
   >
   >La zone Composant Webpart de la visionneuse de pages apparaît sous le bouton **Ajouter un composant Webpart** sur lequel vous avez cliqué à l’étape 3, comme le montre l’illustration suivante (figure 1) :

   ![Zone Composant Webpart de la visionneuse de pages de Microsoft Office SharePoint Server.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figure 1. - La zone Composant Webpart de la visionneuse de pages de Microsoft Office SharePoint Server.

1. Sur la page Visionneuse de pages, effectuez les tâches suivantes :

   1. Dans la zone Lien, saisissez l’URL de AEM Forms Workspace, par exemple `https://[AEM_forms_Server]:8080/lc/ws` où `[AEM_forms_Server]` représente l’adresse IP ou le nom du serveur d’AEM formulaires.
   1. Cliquez sur **Aspect** et modifiez la hauteur, la largeur et le titre de sorte que vous puissiez voir l’ensemble de l’interface utilisateur de Workspace. Par exemple, vous pouvez définir une hauteur et une largeur de 6 pouces et 11 pouces respectivement.
   1. Cliquez sur **Tester le lien**. Une nouvelle fenêtre de navigateur Web apparaît et Workspace y est affiché.
   1. (Facultatif) Cliquez sur **Disposition** et modifiez la disposition de Workspace dans Composant Webpart.
   1. (Facultatif) Cliquez sur **Avancé** et modifiez les autres paramètres, tels que la description et si Workspace peut être réduit ou fermé dans le composant Webpart.

      Cliquez sur **Appliquer**.

1. Cliquez sur **Quitter le mode Edition** et vérifiez que vous pouvez accéder à Workspace.

Une fois que vous avez effectué toutes les étapes ci-dessus, votre site SharePoint ressemble à l’illustration suivante (figure 2) :

![AEM Forms Workspace intégré à Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figure 2 : AEM Forms Workspace intégré à Microsoft Office SharePoint Server

