---
title: Meilleures pratiques de partage de dossiers entre AEM et Creative Cloud
description: Configurez Adobe Experience Manager (AEM) pour permettre aux utilisateurs d’échanger des dossiers dans AEM Assets avec des utilisateurs Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Meilleures pratiques de partage de dossiers entre AEM et Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La fonction de partage de dossiers entre AEM et Creative Cloud est obsolète. Adobe recommande vivement d’utiliser des fonctionnalités plus récentes, telles qu’ [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) ou l’application [de bureau](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)AEM. Learn more in [AEM and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Manager (AEM) peut être configuré pour permettre aux utilisateurs d’AEM Assets de partager des dossiers avec les utilisateurs des applications Adobe Creative Cloud. Ils sont donc disponibles sous forme de dossiers partagés dans le service Adobe Creative Cloud Assets. La fonction peut être utilisée pour échanger des fichiers entre les équipes créatives et les utilisateurs AEM Assets, surtout si les créatifs n’ont pas accès à l’instance AEM Assets (ils ne se trouvent pas sur le réseau de l’entreprise).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à AEM Assets :

* Les utilisateurs d’AEM Assets partagent un ensemble de ressources spécifiques avec les utilisateurs d’Adobe Creative Cloud Files (par exemple, un briefing de création et un ensemble de ressources approuvées pour le travail de conception lié à une nouvelle activité marketing).
* Les utilisateurs d’AEM Assets reçoivent les nouveaux fichiers créés par les utilisateurs d’Adobe Creative Cloud.

>[!NOTE]
>
>Avant de lire ce document, vous pouvez consulter les [meilleures pratiques générales d’intégration d’AEM et de Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) pour un aperçu général du sujet.

## Présentation {#overview}

Le partage de dossiers AEM vers Creative Cloud repose sur le partage côté serveur de dossiers et de fichiers entre les ressources AEM et les comptes Creative Cloud. Les professionnels de la conception, qui utilisent l’application pour postes de travail Creative Cloud sur leurs ordinateurs de bureau, peuvent également rendre les dossiers partagés disponibles directement sur leurs disques à l’aide de la technologie Adobe CreativeSync.

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **Serveur** AEM Assets déployé dans le réseau d’entreprise (services gérés ou sur site) : Le partage de dossiers est initié ici.
* Le **service de base Adobe Marketing Cloud Assets** : sert d’intermédiaire entre AEM et les services de stockage Creative Cloud. L’administrateur de l’entreprise qui utilise l’intégration se doit d’établir des relations de confiance entre l’organisation Marketing Cloud et l’instance AEM Assets. Il définit également [une liste des collaborateurs Creative Cloud approuvés](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html), avec qui les utilisateurs d’AEM Assets peuvent partager des dossiers pour plus de sécurité.

* **Services** Web Creative Cloud Assets (stockage et interface utilisateur Web Creative Cloud Files) : C’est là que des utilisateurs spécifiques de l’application Creative Cloud, avec lesquels un dossier AEM Assets a été partagé, peuvent accepter l’invitation et voir le dossier dans leur espace de stockage de compte Creative Cloud.
* **Application** de bureau Creative Cloud : (Facultatif) Permet un accès direct aux dossiers/fichiers partagés depuis le bureau de l’utilisateur créatif via la synchronisation avec le stockage des ressources Creative Cloud.

## Caractéristiques et limites {#characteristics-and-limitations}

* **** Propagation unidirectionnelle des modifications : Les modifications apportées aux fichiers sont propagées dans une seule direction - à partir du système (AEM ou Creative Cloud Assets), où la ressource a été créée à l’origine (téléchargée). L’intégration ne fournit pas de synchronisation entièrement automatisée et bidirectionnelle entre les deux systèmes.
* **Création de versions:**

   * AEM crée uniquement les versions d’une ressource lors des mises à jour si le fichier provient d’AEM et y est mis à jour.
   * Creative Cloud Assets fournit sa propre [fonctionnalité de création de versions](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées 10 jours).

* **** Limites d&#39;espace : Les tailles et les volumes de fichiers échangés sont limités par le quota [spécifique de ressources](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud pour les utilisateurs créatifs (dépend du niveau d’abonnement) et par une taille de fichier maximale de 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Marketing Cloud Assets.

* **** Espace requis : Les fichiers des dossiers partagés doivent également être physiquement stockés dans AEM, puis dans un compte Creative Cloud, avec une copie mise en cache dans le service principal Ressources Marketing Cloud.
* **** Réseau et bande passante : Les fichiers des dossiers partagés et toutes les mises à jour doivent être transportés sur le réseau entre les systèmes. Vous devez vous assurer que seuls les fichiers et les mises à niveau appropriées sont partagés.
* **Type de fichier** : partager un dossier de ressources du type `sling:OrderedFolder` n’est pas pris en charge dans le cadre du partage dans Adobe Marketing Cloud. Si vous souhaitez partager un dossier, lors de sa création dans AEM Assets, ne sélectionnez pas l’option Ordre.

## Bonnes pratiques {#best-practices}

Les meilleures pratiques d’utilisation du partage de dossier entre AEM et Creative Cloud comprennent :

* **** Remarques sur le volume : Le partage de dossiers AEM/Creative Cloud doit être utilisé pour partager un plus petit nombre de fichiers, par exemple en rapport avec une campagne ou une activité spécifique. Pour partager de plus grands ensembles de ressources, comme toutes les ressources approuvées dans l’organisation, utilisez d’autres méthodes de distribution (par exemple, AEM Assets Brand Portal) ou l’application de bureau AEM.

* **** Evitez de partager des hiérarchies profondes : Le partage fonctionne de manière récursive et ne permet pas un déspartage sélectif. En règle générale, seuls les dossiers sans sous-dossiers ou avec une hiérarchie très superficielle, comme 1 niveau de sous-dossier, doivent être pris en compte pour le partage.
* **** Dossiers distincts pour le partage unidirectionnel : Des dossiers distincts doivent être utilisés pour le partage des fichiers finaux d’AEM Assets vers des fichiers Creative Cloud et pour le partage de fichiers prêts à l’emploi depuis des fichiers Creative Cloud vers AEM Assets. Associé à une convention d’affectation de nom efficace pour ces dossiers, il crée un environnement de travail plus facile à comprendre pour les utilisateurs d’AEM Assets et de Creative Cloud.
* **** Evitez les travaux en cours dans le dossier partagé : Le dossier partagé ne doit pas être utilisé pour le travail en cours : utilisez un dossier distinct dans les fichiers Creative Cloud pour effectuer des tâches qui nécessitent des modifications fréquentes du fichier.
* **** Démarrer une nouvelle tâche en dehors du dossier partagé : Les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans le dossier WIP distinct des fichiers Creative Cloud et, lorsqu’elles sont prêtes à être partagées avec les utilisateurs d’AEM Assets, elles doivent être déplacées ou enregistrées dans le dossier partagé.
* **** Simplifier la structure de partage : Pour une configuration d’exploitation plus gérable, pensez à simplifier la structure de partage. Plutôt que de les partager avec tous les utilisateurs créatifs, les dossiers AEM Assets doivent être partagés avec les représentants de l’équipe uniquement, comme un directeur créatif ou un chef d’équipe. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. Ils peuvent utiliser les fonctions de collaboration Creative Cloud pour coordonner le travail et finalement sélectionner et placer les ressources prêtes à être partagées dans le dossier partagé AEM Assets dans leur dossier partagé prêt pour la création.

Le schéma suivant illustre un exemple de configuration permettant de créer des conceptions basées sur les ressources finales existantes d’AEM Assets.

![chlimage_1-180](assets/chlimage_1-407.png)
