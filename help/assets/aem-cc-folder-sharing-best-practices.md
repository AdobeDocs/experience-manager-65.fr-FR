---
title: 'Meilleures pratiques de partage de dossiers vers [!DNL Adobe Creative Cloud] '
description: Configurez  [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] pour échanger des dossiers avec des utilisateurs de Adobe Creative Cloud (CC).
contentOwner: AG
role: Business Practitioner, Administrator
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 17%

---

# [!DNL Adobe Experience Manager] vers le partage de  [!DNL Adobe Creative Cloud] dossiers  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La fonction de [!DNL Experience Manager] vers [!DNL Creative Cloud] partage de dossiers est obsolète. Adobe recommande vivement d’utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) ou [l’appli de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr). Pour en savoir plus, consultez [Bonnes pratiques d’intégration des Experience Manager et des Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] peut être configuré pour permettre aux utilisateurs de  [!DNL Assets] partager des dossiers avec les utilisateurs des  [!DNL Adobe Creative Cloud] applications. Ils sont donc disponibles en tant que dossiers partagés dans le service  [!DNL Adobe Creative Cloud] Assets. La fonctionnalité peut être utilisée pour échanger des fichiers entre les équipes créatives et les utilisateurs [!DNL Assets], en particulier lorsque les utilisateurs créatifs n’ont pas accès au déploiement [!DNL Assets] (ils ne se trouvent pas sur le réseau d’entreprise).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à [!DNL Assets]:

* [!DNL Assets] les utilisateurs partagent un ensemble de ressources numériques spécifiques avec les utilisateurs de  [!DNL Adobe Creative Cloud] fichiers (par exemple, un résumé créatif et un ensemble de ressources approuvées pour le travail de conception d’une nouvelle activité marketing).
* [!DNL Assets] les utilisateurs reçoivent les nouveaux fichiers créés par les utilisateurs de l’ [!DNL Adobe Creative Cloud] application.

>[!NOTE]
>
>Avant de lire ce document, vous pouvez consulter les [bonnes pratiques d’intégration des Experience Manager et des Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) générales pour un aperçu de l’intégration.

## Présentation {#overview}

[!DNL Experience Manager] le partage vers les  [!DNL Creative Cloud] dossiers repose sur le partage côté serveur de dossiers et de fichiers entre  [!DNL Assets] et  [!DNL Creative Cloud] comptes. Les professionnels de la création, qui utilisent l’appli de bureau [!DNL Creative Cloud] sur leur bureau, peuvent également rendre les dossiers partagés disponibles directement sur leurs disques à l’aide de la technologie [!DNL Adobe CreativeSync].

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **[!DNL Experience Manager Assets]** déployé dans le réseau d’entreprise (services gérés ou on-premise) : Le partage de dossiers est lancé ici.
* **[!DNL Adobe Marketing Cloud Assets]core service** : Agit comme intermédiaire entre  [!DNL Experience Manager] et les services  [!DNL Creative Cloud] de stockage. Un administrateur d’une organisation qui utilise l’intégration doit établir une relation de confiance entre l’organisation du Marketing Cloud et le déploiement [!DNL Assets]. Ils définissent également [une liste de collaborateurs Creative Cloud approuvés](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que les utilisateurs [!DNL Assets] peuvent partager des dossiers également pour plus de sécurité.

* **[!DNL Creative Cloud]Services web Assets**  (stockage et interface utilisateur web des  [!DNL Creative Cloud] fichiers) : C’est là que des utilisateurs spécifiques de l’application de Creative Cloud, avec lesquels un  [!DNL Assets] dossier a été partagé, peuvent accepter l’invitation et voir le dossier dans le stockage de leur compte de Creative Cloud.
* **Application** de bureau de Creative Cloud : (Facultatif) Permet un accès direct aux dossiers/fichiers partagés depuis le bureau de l’utilisateur créatif via une synchronisation avec le stockage  [!DNL Creative Cloud] Assets.

## Caractéristiques et limites {#characteristics-and-limitations}

* **Diffusion unidirectionnelle des modifications :** les modifications de fichier sont propagées dans une seule direction uniquement à partir du système ([!DNL Experience Manager]  ou  [!DNL Creative Cloud Assets]) où la ressource a été créée à l’origine (téléchargée). L’intégration ne fournit pas de synchronisation entièrement automatisée et bidirectionnelle entre les deux systèmes.
* **Contrôle de version:**

   * [!DNL Experience Manager] crée uniquement des versions d’une ressource lors des mises à jour si le fichier provient de  [!DNL Experience Manager] et y est mis à jour.
   * [!DNL Creative Cloud] Assets fournit sa propre [fonctionnalité de création de versions](https://helpx.adobe.com/fr/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées 10 jours).

* **Limites d’espace :**  la taille et le volume des fichiers échangés sont limités par le  [quota spécifique de ressources du ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud pour les utilisateurs créatifs (dépend du niveau d’abonnement) et une taille de fichier maximale de 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Marketing Cloud Assets.

* **Exigences d’espace :** les fichiers des dossiers partagés doivent également être stockés physiquement dans  [!DNL Experience Manager] puis dans le  [!DNL Creative Cloud] compte, avec une copie mise en cache dans le service  [!DNL Marketing Cloud Assets] principal.
* **Mise en réseau et bande passante :** les fichiers des dossiers partagés et toutes les mises à jour doivent être transportés sur le réseau entre les systèmes. Vous devez vous assurer que seuls les fichiers et les mises à niveau appropriées sont partagés.
* **Type** de dossier : Le partage d’un  [!DNL Assets] dossier de type  `sling:OrderedFolder` n’est pas pris en charge dans le cadre du partage dans  [!DNL Adobe Marketing Cloud]. Si vous souhaitez partager un dossier, lors de sa création dans [!DNL Assets], ne sélectionnez pas l’option [!UICONTROL Ordered].

## Bonnes pratiques {#best-practices}

Les bonnes pratiques pour utiliser le partage de dossiers [!DNL Experience Manager] vers [!DNL Creative Cloud] incluent :

* **Volume :** [!DNL Experience Manager] et le  [!DNL Creative Cloud] partage de dossiers doivent être utilisés pour partager un plus petit nombre de fichiers, par exemple, pertinents pour une campagne ou une activité spécifique. Pour partager des jeux de ressources plus volumineux, comme toutes les ressources approuvées dans l’organisation, utilisez d’autres méthodes de distribution (par exemple, [!DNL Assets Brand Portal]) ou l’appli de bureau [!DNL Experience Manager].
* **Évitez de partager des hiérarchies profondes :**  le partage fonctionne de manière récursive et n’autorise pas l’annulation sélective du partage. En règle générale, seuls les dossiers sans sous-dossiers, ou avec une hiérarchie très superficielle, comme 1 niveau de sous-dossiers, doivent être pris en compte pour le partage.
* **Séparez les dossiers pour un partage unidirectionnel :** des dossiers distincts doivent être utilisés pour partager les ressources finales de  [!DNL Assets] vers  [!DNL Creative Cloud] les fichiers et pour partager les ressources prêtes pour les créatifs  [!DNL Creative Cloud] des fichiers vers  [!DNL Assets]. Associé à une bonne convention d’affectation des noms pour ces dossiers, il crée un environnement de travail plus facile à comprendre pour les utilisateurs [!DNL Assets] et [!DNL Creative Cloud].
* **Évitez les travaux en cours dans le dossier partagé :**  le dossier partagé ne doit pas être utilisé pour le travail en cours ; utilisez un dossier distinct dans les fichiers Creative Cloud pour effectuer le travail qui nécessite des modifications fréquentes du fichier.
* **Démarrer une nouvelle tâche en dehors du dossier partagé :** les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans le dossier de travail en cours distinct dans les fichiers Creative Cloud. Lorsqu’elles sont prêtes à être partagées avec  [!DNL Assets] les utilisateurs, elles doivent être déplacées ou enregistrées dans le dossier partagé.
* **Simplifiez la structure de partage :** pour une configuration opérationnelle plus gérable, pensez à simplifier la structure de partage. Au lieu de les partager avec tous les utilisateurs créatifs, les dossiers [!DNL Assets] doivent être partagés uniquement avec les représentants de l’équipe, comme un directeur créatif ou un chef d’équipe. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. Ils peuvent utiliser des fonctions de collaboration de Creative Cloud pour coordonner le travail, puis sélectionner et remettre les ressources prêtes à être partagées dans [!DNL Assets] dans leur dossier partagé prêt pour les créatifs.

Le diagramme suivant illustre un exemple de configuration pour la création de conceptions basées sur les ressources finales existantes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
