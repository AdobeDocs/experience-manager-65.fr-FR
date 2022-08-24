---
title: Partage de dossiers vers [!DNL Adobe Creative Cloud] bonnes pratiques
description: Configurer [!DNL Adobe Experience Manager] pour permettre aux utilisateurs d’ [!DNL Experience Manager Assets] pour échanger des dossiers avec des utilisateurs de Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 17%

---

# [!DNL Adobe Experience Manager] to [!DNL Adobe Creative Cloud] partage de dossiers {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Le [!DNL Experience Manager] to [!DNL Creative Cloud] La fonctionnalité de partage de dossiers est obsolète. Adobe recommande vivement d’utiliser des fonctionnalités plus récentes, telles que [Adobe d’un lien de ressource](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) ou [application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr). En savoir plus dans [Bonnes pratiques d’intégration Experience Manager et Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] peut être configuré pour autoriser les utilisateurs à [!DNL Assets] pour partager des dossiers avec les utilisateurs de [!DNL Adobe Creative Cloud] applications, elles sont donc disponibles en tant que dossiers partagés dans les [!DNL Adobe Creative Cloud] service assets. Cette fonctionnalité peut être utilisée pour échanger des fichiers entre les équipes créatives et [!DNL Assets] , en particulier lorsque les utilisateurs créatifs n’ont pas accès à la variable [!DNL Assets] déploiement (ils ne se trouvent pas sur le réseau de l’entreprise).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à [!DNL Assets]:

* [!DNL Assets] les utilisateurs partagent un ensemble de ressources numériques spécifiques avec les utilisateurs de [!DNL Adobe Creative Cloud] fichiers (par exemple, un résumé créatif et un ensemble de ressources approuvées pour le travail de conception d’une nouvelle activité marketing).
* [!DNL Assets] les utilisateurs reçoivent les nouveaux fichiers créés par [!DNL Adobe Creative Cloud] utilisateurs de l’application.

>[!NOTE]
>
>Avant de lire ce document, vous pouvez consulter [Bonnes pratiques d’intégration Experience Manager et Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) pour une présentation de l’intégration.

## Présentation {#overview}

[!DNL Experience Manager] to [!DNL Creative Cloud] le partage de dossiers repose sur le partage côté serveur de dossiers et de fichiers entre les [!DNL Assets] et [!DNL Creative Cloud] comptes. Les professionnels de la création qui utilisent la variable [!DNL Creative Cloud] L’appli de bureau sur son bureau peut, en outre, rendre les dossiers partagés disponibles directement sur ses disques à l’aide de [!DNL Adobe CreativeSync] technologie.

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **[!DNL Experience Manager Assets]** déployé dans le réseau d’entreprise (services gérés ou on-premise) : Le partage de dossiers est lancé ici.
* **[!DNL Adobe Marketing Cloud Assets]core service**: Agit comme intermédiaire entre [!DNL Experience Manager] et [!DNL Creative Cloud] services de stockage. Un administrateur d’une organisation qui utilise l’intégration doit établir une relation de confiance entre l’organisation de Marketing Cloud et la [!DNL Assets] déploiement. Elles aussi [définir une liste des collaborateurs Creative Cloud approuvés ;](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que [!DNL Assets] les utilisateurs peuvent également partager des dossiers pour plus de sécurité.

* **[!DNL Creative Cloud]Services web Assets** (stockage et [!DNL Creative Cloud] Interface utilisateur web des fichiers) : C’est là que se trouvent les utilisateurs spécifiques de l’application de Creative Cloud, avec lesquels un [!DNL Assets] était partagé, pouvait accepter l’invitation et voir le dossier dans le stockage de leur compte de Creative Cloud.
* **application de bureau Creative Cloud**: (Facultatif) Permet un accès direct aux dossiers/fichiers partagés depuis le bureau de l’utilisateur créatif via la synchronisation avec [!DNL Creative Cloud] Stockage des ressources.

## Caractéristiques et limites {#characteristics-and-limitations}

* **Diffusion unidirectionnelle des modifications :** Les modifications de fichier sont propagées dans une seule direction à partir du système ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), où la ressource a été créée à l’origine (téléchargée). L’intégration ne fournit pas de synchronisation entièrement automatisée et bidirectionnelle entre les deux systèmes.
* **Contrôle de version:**

   * [!DNL Experience Manager] crée uniquement les versions d’une ressource lors des mises à jour si le fichier est issu de [!DNL Experience Manager] et y est mis à jour.
   * [!DNL Creative Cloud] Assets fournit sa propre [fonctionnalité de création de versions](https://helpx.adobe.com/fr/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées 10 jours).

* **Limites d’espace :** La taille et le volume des fichiers échangés sont limités par les [Quota de ressources Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) pour les utilisateurs créatifs (selon le niveau d’abonnement) et une taille de fichier maximale de 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Marketing Cloud Assets.

* **Exigences d’espace :** Les fichiers des dossiers partagés doivent également être stockés physiquement dans [!DNL Experience Manager] puis dans [!DNL Creative Cloud] compte, avec une copie mise en cache dans [!DNL Marketing Cloud Assets] core service.
* **Mise en réseau et bande passante :** Les fichiers dans les dossiers partagés et toutes les mises à jour doivent être transportés sur le réseau entre les systèmes. Vous devez vous assurer que seuls les fichiers et les mises à niveau appropriées sont partagés.
* **Type de dossier**: Partager [!DNL Assets] dossier du type `sling:OrderedFolder`, n’est pas pris en charge dans le cadre du partage dans [!DNL Adobe Marketing Cloud]. Si vous souhaitez partager un dossier, lors de sa création dans [!DNL Assets], ne sélectionnez pas l’événement [!UICONTROL Commandé] .

## Bonnes pratiques {#best-practices}

Bonnes pratiques relatives à l’utilisation de la variable [!DNL Experience Manager] to [!DNL Creative Cloud] partage de dossiers :

* **Considérations relatives au volume :** [!DNL Experience Manager] et [!DNL Creative Cloud] Le partage de dossiers doit être utilisé pour partager un plus petit nombre de fichiers, par exemple, pertinents pour une campagne ou une activité spécifique. Pour partager des jeux de ressources plus volumineux, comme toutes les ressources approuvées dans l’organisation, utilisez d’autres méthodes de distribution (par exemple, [!DNL Assets Brand Portal]) ou [!DNL Experience Manager] application de bureau .
* **Évitez de partager des hiérarchies profondes :** Le partage fonctionne de manière récursive et n’autorise pas le partage sélectif. En règle générale, seuls les dossiers sans sous-dossiers, ou avec une hiérarchie très superficielle, comme 1 niveau de sous-dossiers, doivent être pris en compte pour le partage.
* **Séparez les dossiers pour un partage unidirectionnel :** Des dossiers distincts doivent être utilisés pour partager des ressources finales à partir de [!DNL Assets] to [!DNL Creative Cloud] et pour partager des ressources prêtes pour les créatifs à partir de [!DNL Creative Cloud] fichiers vers [!DNL Assets]. Associé à une bonne convention d’affectation des noms pour ces dossiers, il crée un environnement de travail plus facile à comprendre pour [!DNL Assets] et [!DNL Creative Cloud] utilisateurs comme .
* **Évitez les travaux en cours dans le dossier partagé :** Le dossier partagé ne doit pas être utilisé pour le travail en cours : utilisez un dossier distinct dans les fichiers du Creative Cloud pour effectuer le travail qui nécessite des modifications fréquentes du fichier.
* **Démarrez une nouvelle tâche en dehors du dossier partagé :** Les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans le dossier de travaux en cours distinct dans les fichiers Creative Cloud et lorsqu’elles sont prêtes à être partagées avec . [!DNL Assets] utilisateurs, ils doivent être déplacés ou enregistrés dans le dossier partagé.
* **Simplifiez la structure de partage :** Pour une configuration opérationnelle plus gérable, pensez à simplifier la structure de partage. Au lieu de partager avec tous les utilisateurs créatifs, [!DNL Assets] Les dossiers doivent être partagés avec les représentants de l’équipe uniquement, comme un directeur créatif ou un chef d’équipe. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. Ils peuvent utiliser des fonctions de collaboration Creative Cloud pour coordonner le travail, puis sélectionner et réutiliser les ressources prêtes à être partagées dans [!DNL Assets] dans leur dossier partagé prêt pour les créatifs.

Le diagramme suivant illustre un exemple de configuration pour la création de conceptions basées sur des ressources finales existantes à partir de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
