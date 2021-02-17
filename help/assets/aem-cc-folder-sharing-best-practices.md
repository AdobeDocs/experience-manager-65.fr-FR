---
title: Partage de dossiers avec  [!DNL Adobe Creative Cloud] les meilleures pratiques
description: Configurez  [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] pour échanger des dossiers avec des utilisateurs Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] au partage de  [!DNL Adobe Creative Cloud] dossiers  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La fonction de partage de dossiers [!DNL Experience Manager] vers [!DNL Creative Cloud] est obsolète. L’Adobe recommande vivement d’utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou [application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr). En savoir plus sur les [meilleures pratiques d&#39;intégration des Experience Manager et des Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] peuvent être configurés pour permettre  [!DNL Assets] aux utilisateurs de partager des dossiers avec les utilisateurs d’ [!DNL Adobe Creative Cloud] applications, de sorte qu’ils soient disponibles sous forme de dossiers partagés dans le service  [!DNL Adobe Creative Cloud] ressources. Cette fonction permet d’échanger des fichiers entre les équipes créatives et les utilisateurs [!DNL Assets], en particulier lorsque les utilisateurs créatifs n’ont pas accès au déploiement [!DNL Assets] (ils ne se trouvent pas sur le réseau de l’entreprise).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à [!DNL Assets]:

* [!DNL Assets] les utilisateurs partagent un ensemble de ressources numériques spécifiques avec les utilisateurs de  [!DNL Adobe Creative Cloud] fichiers (par exemple, un dossier créatif et un ensemble de ressources approuvées pour le travail de conception d’une nouvelle activité marketing).
* [!DNL Assets] les utilisateurs reçoivent les nouveaux fichiers créés par les utilisateurs de  [!DNL Adobe Creative Cloud] l’application.

>[!NOTE]
>
>Avant de lire ce document, vous pouvez consulter les meilleures pratiques d’intégration [Experience Manager et Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) pour un aperçu de l’intégration.

## Présentation {#overview}

[!DNL Experience Manager] le partage  [!DNL Creative Cloud] entre dossiers repose sur le partage côté serveur de dossiers et de fichiers entre  [!DNL Assets] et  [!DNL Creative Cloud] comptes. Les professionnels de la création, qui utilisent l&#39;application de bureau [!DNL Creative Cloud] sur leurs ordinateurs de bureau, peuvent en outre rendre les dossiers partagés disponibles directement sur leurs disques à l&#39;aide de la technologie [!DNL Adobe CreativeSync].

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **[!DNL Experience Manager Assets]** déployés dans le réseau d’entreprise (services gérés ou sur site) : Le partage de dossiers est initié ici.
* **[!DNL Adobe Marketing Cloud Assets]service** principal : Intermédiaire entre  [!DNL Experience Manager] et  [!DNL Creative Cloud] les services d&#39;enregistrement. Un administrateur d&#39;une organisation qui utilise l&#39;intégration doit établir une relation de confiance entre l&#39;organisation de Marketing Cloud et le déploiement [!DNL Assets]. Ils [définissent également une liste de collaborateurs Creative Cloud approuvés](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), selon laquelle les utilisateurs [!DNL Assets] peuvent partager des dossiers pour plus de sécurité.

* **[!DNL Creative Cloud]Services**  Web Assets (interface utilisateur Web d’enregistrement et de  [!DNL Creative Cloud] fichiers) : C’est là que des utilisateurs d’applications Creative Cloud spécifiques, avec lesquels un  [!DNL Assets] dossier a été partagé, peuvent accepter l’invitation et voir le dossier dans leur enregistrement de compte Creative Cloud.
* **Application** de bureau Creative Cloud : (Facultatif) Permet un accès direct aux dossiers/fichiers partagés depuis le bureau de l’utilisateur créatif via la synchronisation avec l’enregistrement  [!DNL Creative Cloud] Ressources.

## Caractéristiques et limites {#characteristics-and-limitations}

* **Propagation unidirectionnelle des modifications : les modifications apportées aux** fichiers sont propagées dans une seule direction - à partir du système ([!DNL Experience Manager] ou  [!DNL Creative Cloud Assets]), où la ressource a été créée à l’origine (téléchargée). L’intégration ne fournit pas de synchronisation entièrement automatisée et bidirectionnelle entre les deux systèmes.
* **Contrôle de version:**

   * [!DNL Experience Manager] crée uniquement des versions d’un fichier lors des mises à jour si le fichier est d’origine  [!DNL Experience Manager] et y est mis à jour.
   * [!DNL Creative Cloud] Assets fournit sa propre [fonctionnalité de création de versions](https://helpx.adobe.com/fr/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées 10 jours).

* **Limites d’espace :** Les tailles et les volumes des fichiers échangés sont limités par le  [quotient Ressources du ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud spécifique pour les utilisateurs créatifs (selon le niveau d’abonnement) et par une taille de fichier maximale de 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Marketing Cloud Assets.

* **Espace requis :** Les fichiers des dossiers partagés doivent également être physiquement stockés dans  [!DNL Experience Manager] puis dans un  [!DNL Creative Cloud] compte, avec une copie mise en cache dans le service  [!DNL Marketing Cloud Assets] principal.
* **Mise en réseau et bande passante :** les fichiers des dossiers partagés et toutes les mises à jour doivent être transportés sur le réseau entre les systèmes. Vous devez vous assurer que seuls les fichiers et les mises à niveau appropriées sont partagés.
* **Type** de dossier : Le partage d&#39;un  [!DNL Assets] dossier de type  `sling:OrderedFolder` n&#39;est pas pris en charge dans le contexte du partage dans  [!DNL Adobe Marketing Cloud]. Si vous souhaitez partager un dossier, lors de sa création dans [!DNL Assets], ne sélectionnez pas l&#39;option [!UICONTROL Commandé].

## Bonnes pratiques {#best-practices}

Les meilleures pratiques pour exploiter le partage de dossiers [!DNL Experience Manager] à [!DNL Creative Cloud] incluent :

* **Considérations relatives au volume :** [!DNL Experience Manager] et le partage de  [!DNL Creative Cloud] dossiers doivent être utilisés pour partager un plus petit nombre de fichiers, par exemple, pertinents pour une campagne ou une activité spécifique. Pour partager des ensembles de ressources plus volumineux, comme toutes les ressources approuvées dans l’organisation, utilisez d’autres méthodes de distribution (par exemple, [!DNL Assets Brand Portal]) ou [!DNL Experience Manager] application de bureau.
* **Evitez de partager des hiérarchies profondes :** le partage fonctionne de manière récursive et ne permet pas un déséchange sélectif. En règle générale, seuls les dossiers sans sous-dossiers ou avec une hiérarchie très superficielle, comme 1 niveau de sous-dossier, doivent être pris en compte pour le partage.
* **Dossiers distincts pour le partage à sens unique :** Des dossiers distincts doivent être utilisés pour partager des fichiers finaux de  [!DNL Assets] vers  [!DNL Creative Cloud] des fichiers et pour partager des fichiers prêts à l’emploi à partir de  [!DNL Creative Cloud] fichiers vers  [!DNL Assets]. Associé à une convention d’affectation de nom efficace pour ces dossiers, il crée un environnement de travail plus facile à comprendre pour les utilisateurs [!DNL Assets] et [!DNL Creative Cloud].
* **Evitez les travaux en cours dans le dossier partagé :Le dossier** partagé ne doit pas être utilisé pour le travail en cours. Utilisez un dossier distinct dans les fichiers Creative Cloud pour effectuer des travaux nécessitant des modifications fréquentes du fichier.
* **Début d’une nouvelle tâche en dehors du dossier partagé :** Les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans le dossier WIP distinct des fichiers Creative Cloud et, lorsqu’elles sont prêtes à être partagées avec  [!DNL Assets] les utilisateurs, elles doivent être déplacées ou enregistrées dans le dossier partagé.
* **Simplifier la structure de partage :** Pour une configuration d&#39;exploitation plus gérable, pensez à simplifier la structure de partage. Au lieu de le partager avec tous les utilisateurs créatifs, les dossiers [!DNL Assets] doivent être partagés avec les représentants de l’équipe uniquement, comme un directeur créatif ou un responsable d’équipe. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. Ils peuvent utiliser les fonctions de collaboration des Creative Cloud pour coordonner le travail, et enfin sélectionner et placer les ressources prêtes à être partagées dans [!DNL Assets] leur dossier partagé prêt à l&#39;emploi.

Le diagramme suivant illustre un exemple de configuration pour la création de conceptions basées sur les ressources finales existantes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
