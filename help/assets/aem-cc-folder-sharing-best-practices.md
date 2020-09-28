---
title: Méthodes [!DNL Adobe Creative Cloud] de partage de dossiers
description: ' [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] Configurez pour échanger des dossiers avec des utilisateurs Adobe Creative Cloud (CC).'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 17%

---


# [!DNL Adobe Experience Manager] vers le [!DNL Adobe Creative Cloud] partage de dossiers {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>The [!DNL Experience Manager] to [!DNL Creative Cloud] Folder Sharing feature is deprecated. L’Adobe recommande vivement d’utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou application [de bureau](https://docs.adobe.com/content/help/fr-FR/experience-manager-desktop-app/using/using.html)Experience Manager. Learn more in [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] peuvent être configurés pour permettre aux utilisateurs de [!DNL Assets] partager des dossiers avec les utilisateurs d’ [!DNL Adobe Creative Cloud] applications, de sorte qu’ils soient disponibles sous forme de dossiers partagés dans le service [!DNL Adobe Creative Cloud] ressources. The feature can be used to exchange files between creative teams and [!DNL Assets] users, especially when the creative users do not have access to the [!DNL Assets] deployment (they are not on the enterprise network).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à [!DNL Assets]:

* [!DNL Assets] les utilisateurs partagent un ensemble de ressources numériques spécifiques avec les utilisateurs de [!DNL Adobe Creative Cloud] fichiers (par exemple, un dossier créatif et un ensemble de ressources approuvées pour le travail de conception d’une nouvelle activité marketing).
* [!DNL Assets] les utilisateurs reçoivent les nouveaux fichiers créés par les utilisateurs de [!DNL Adobe Creative Cloud] l’application.

>[!NOTE]
>
>Before reading this document, you can review the overall [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md) for an overview of the integration.

## Présentation {#overview}

[!DNL Experience Manager] le partage [!DNL Creative Cloud] des dossiers repose sur le partage côté serveur des dossiers et des fichiers entre [!DNL Assets] et [!DNL Creative Cloud] les comptes. Creative professionals, who use the [!DNL Creative Cloud] desktop app on their desktops, can additionally make the shared folders available directly on their disks using [!DNL Adobe CreativeSync] technology.

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **[!DNL Experience Manager Assets]** déployés dans le réseau d’entreprise (services gérés ou sur site) : Le partage de dossiers est initié ici.
* **[!DNL Adobe Marketing Cloud Assets]service** principal : Agit en tant qu&#39;intermédiaire entre les services [!DNL Experience Manager] et les services [!DNL Creative Cloud] d&#39;enregistrement. Un administrateur d’une organisation qui utilise l’intégration doit établir une relation de confiance entre l’organisation de Marketing Cloud et le [!DNL Assets] déploiement. They also [define a list of approved Creative Cloud collaborators](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html), that [!DNL Assets] users can share folders too for additional security.

* **[!DNL Creative Cloud]Services** Web Assets (interface utilisateur Web d’enregistrement et de [!DNL Creative Cloud] fichiers) : C’est là que des utilisateurs d’applications Creative Cloud spécifiques, avec lesquels un [!DNL Assets] dossier a été partagé, peuvent accepter l’invitation et voir le dossier dans leur enregistrement de compte Creative Cloud.
* **Application** de bureau Creative Cloud : (Facultatif) Permet un accès direct aux dossiers/fichiers partagés depuis le bureau de l’utilisateur créatif via la synchronisation avec l’enregistrement [!DNL Creative Cloud] Ressources.

## Caractéristiques et limites {#characteristics-and-limitations}

* **Propagation unidirectionnelle des modifications :** Les modifications apportées aux fichiers sont propagées dans une seule direction - à partir du système ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), où la ressource a été créée à l’origine (téléchargée). L’intégration ne fournit pas de synchronisation entièrement automatisée et bidirectionnelle entre les deux systèmes.
* **Contrôle de version:**

   * [!DNL Experience Manager] ne crée des versions d’un fichier que lors des mises à jour si le fichier est d’origine [!DNL Experience Manager] et y est mis à jour.
   * [!DNL Creative Cloud] Assets fournit sa propre [fonctionnalité de création de versions](https://helpx.adobe.com/fr/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées 10 jours).

* **Limites d&#39;espace :** Les tailles et les volumes des fichiers échangés sont limités par le quota [d’actifs](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud spécifique pour les utilisateurs créatifs (dépend du niveau d’abonnement) et par une taille de fichier maximale de 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Marketing Cloud Assets.

* **Espace requis :** Les fichiers des dossiers partagés doivent également être physiquement stockés dans [!DNL Experience Manager] puis dans [!DNL Creative Cloud] le compte, avec une copie mise en cache dans le service [!DNL Marketing Cloud Assets] principal.
* **Réseau et bande passante :** Les fichiers des dossiers partagés et toutes les mises à jour doivent être transportés sur le réseau entre les systèmes. Vous devez vous assurer que seuls les fichiers et les mises à niveau appropriées sont partagés.
* **Type** de dossier : Le partage d&#39;un [!DNL Assets] dossier de type `sling:OrderedFolder`n&#39;est pas pris en charge dans le contexte du partage dans [!DNL Adobe Marketing Cloud]. If you want to share a folder, when creating it in [!DNL Assets], do not select the [!UICONTROL Ordered] option.

## Bonnes pratiques {#best-practices}

Best practices for leveraging the [!DNL Experience Manager] to [!DNL Creative Cloud] folder sharing include:

* **Considérations relatives au volume :** [!DNL Experience Manager] et [!DNL Creative Cloud] le partage de dossiers doit être utilisé pour partager un nombre plus petit de fichiers, par exemple, pertinents pour une campagne ou une activité spécifique. To share larger sets of assets, like all approved assets in the organization, use other distribution methods (for example, [!DNL Assets Brand Portal]) or [!DNL Experience Manager] desktop app.
* **Evitez de partager des hiérarchies profondes :** Le partage fonctionne de manière récursive et ne permet pas un déséchange sélectif. En règle générale, seuls les dossiers sans sous-dossiers ou avec une hiérarchie très superficielle, comme 1 niveau de sous-dossier, doivent être pris en compte pour le partage.
* **Dossiers distincts pour le partage à sens unique :** Des dossiers distincts doivent être utilisés pour partager des fichiers finaux [!DNL Assets] vers [!DNL Creative Cloud] des fichiers et pour partager des fichiers créatifs à partir de [!DNL Creative Cloud] fichiers vers [!DNL Assets]. Together with a good naming convention for these folders, it creates an easier-to-understand working environment for [!DNL Assets] and [!DNL Creative Cloud] users alike.
* **Evitez les travaux en cours dans le dossier partagé :** Le dossier partagé ne doit pas être utilisé pour le travail en cours : utilisez un dossier distinct dans les fichiers Creative Cloud pour effectuer le travail qui nécessite des modifications fréquentes du fichier.
* **Début d’une nouvelle tâche en dehors du dossier partagé :** Les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans le dossier WIP distinct des fichiers Creative Cloud et, lorsqu’elles sont prêtes à être partagées avec [!DNL Assets] les utilisateurs, elles doivent être déplacées ou enregistrées dans le dossier partagé.
* **Simplifier la structure de partage :** Pour une configuration d&#39;exploitation plus gérable, pensez à simplifier la structure de partage. Instead of sharing with all creative users, [!DNL Assets] folders should be shared with team representative(s) only, like a creative director or team manager. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. They can use Creative Cloud collaboration features to coordinate the work, and finally select and put assets that are ready to share back to [!DNL Assets] into their creative-ready shared folder.

The following diagram illustrates an example configuration for creating new designs based on existing final assets from [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
