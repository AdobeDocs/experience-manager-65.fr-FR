---
title: Partage de dossiers vers les bonnes pratiques  [!DNL Adobe Creative Cloud]
description: Configurez  [!DNL Adobe Experience Manager]  pour permettre aux utilisateurs d’ [!DNL Experience Manager Assets]  d’échanger des dossiers dans avec des utilisateurs Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 96%

---

# Partage de dossiers [!DNL Adobe Experience Manager] vers [!DNL Adobe Creative Cloud] {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La fonction de partage de dossiers entre [!DNL Experience Manager] et [!DNL Creative Cloud] est obsolète. Adobe recommande d’utiliser les dernières fonctionnalités, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou l’[application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr). En savoir plus sur les [bonnes pratiques d’intégration d’ Experience Manager et de Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] peut être configuré pour permettre aux utilisateurs d’[!DNL Assets] de partager des dossiers avec les utilisateurs des applications [!DNL Adobe Creative Cloud], afin qu’ils soient disponibles en tant que dossiers partagés dans les services de ressources [!DNL Adobe Creative Cloud]. Cette fonction peut être utilisée pour échanger des fichiers entre les équipes créatives et les utilisateurs d’,[!DNL Assets]surtout si les créatifs n’ont pas accès au déploiement d’[!DNL Assets] (s’ils ne se trouvent pas sur le réseau de l’entreprise).

Ce type d’intégration peut être utilisé dans les deux cas d’utilisation, en particulier lorsque vous travaillez avec des utilisateurs qui n’ont pas d’accès direct à [!DNL Assets] :

* Les utilisateurs d’[!DNL Assets] partagent un ensemble de ressources numériques spécifiques avec les utilisateurs de fichiers [!DNL Adobe Creative Cloud] (par exemple, un briefing de création et un ensemble de ressources approuvées pour le travail de conception lié à une nouvelle activité marketing).
* Les utilisateurs d’[!DNL Assets] reçoivent les nouveaux fichiers créés par utilisateurs des applications [!DNL Adobe Creative Cloud].

>[!NOTE]
>
>Avant de lire ce document, vous pouvez consulter les [bonnes pratiques générales d’intégration d’Experience Manager et de Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) pour obtenir un aperçu général du sujet.

## du commerce électronique {#overview}

Le partage de dossiers [!DNL Experience Manager] vers [!DNL Creative Cloud] repose sur le partage côté serveur de dossiers et de fichiers entre les comptes [!DNL Assets] et [!DNL Creative Cloud]. Les spécialistes de la création qui utilisent l’application de bureau [!DNL Creative Cloud] sur leurs ordinateurs de bureau peuvent également rendre les dossiers partagés disponibles directement sur leurs disques à l’aide de la technologie [!DNL Adobe CreativeSync].

Le diagramme suivant offre une vue d’ensemble du processus d’intégration.

![chlimage_1-179](assets/chlimage_1-406.png)

L’intégration comprend les éléments suivants :

* **[!DNL Experience Manager Assets]** déployé dans le réseau de l’entreprise (services gérés ou sur site) : le partage de dossiers commence ici.
* Le service principal **[!DNL Adobe Experience Cloud Assets]** : sert d’intermédiaire entre [!DNL Experience Manager] et les services de stockage [!DNL Creative Cloud]. L’administrateur ou l’administratrice d’une organisation qui utilise cette intégration doit établir une relation de confiance entre l’organisation Experience Cloud et le déploiement [!DNL Assets]. Il définit également [une liste des collaborateurs Creative Cloud approuvés](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html) avec qui les utilisateurs d’[!DNL Assets] peuvent partager des dossiers, pour plus de sécurité.

* Les services Web **[!DNL Creative Cloud] Assets**(IU Web de fichiers [!DNL Creative Cloud] et de stockage) : endroit où des utilisateurs de Creative Cloud spécifiques, avec lesquels un dossier [!DNL Assets] a été partagé, peuvent accepter l’invitation et visualiser le dossier dans l’espace de stockage de leur compte Creative Cloud.
* **Application de bureau Creative Cloud** : (facultatif) permet un accès direct aux dossiers/fichiers partagés depuis le bureau du concepteur à l’aide d’une synchronisation avec l’espace de stockage [!DNL Creative Cloud] Assets.

## Caractéristiques et limites {#characteristics-and-limitations}

* **Diffusion unidirectionnelle des modifications :** les modifications de fichier se propagent dans une seule direction, à partir du système ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]) où la ressource a été créée (téléchargée) à l’origine. L’intégration ne fournit pas de synchronisation bidirectionnelle entièrement automatisée entre les deux systèmes.
* **Contrôle de version :**

   * [!DNL Experience Manager] crée uniquement des versions d’une ressource lors des mises à jour si le fichier provient d’[!DNL Experience Manager] et y est mis à jour.
   * [!DNL Creative Cloud] Assets fournit sa propre [fonctionnalité de contrôle de versions](https://helpx.adobe.com/fr/creative-cloud/help/versioning-faq.html), qui vise les mises à jour de travail en cours (en général, les mises à jour sont conservées dix jours).

* **Limites d’espace :** la taille et le volume des fichiers échangés sont limités par le [quota spécifique de Creative Cloud Assets](https://helpx.adobe.com/fr/creative-cloud/kb/file-storage-quota.html) pour les spécialistes de la création (en fonction du niveau d’abonnement) et la taille du fichier ne peut pas excéder 5 Go. L’espace est en outre limité par le quota de ressources que l’organisation possède dans le service principal d’Adobe Experience Cloud Assets.

* **Exigences d’espace :** les fichiers des dossiers partagés doivent également être physiquement stockés dans [!DNL Experience Manager], puis sur le compte [!DNL Creative Cloud], avec une copie en mémoire cache dans le service principal de [!DNL Experience Cloud Assets].
* **Réseau et bande passante :** les fichiers des dossiers partagés et toutes les mises à jour doivent être transmis entre les systèmes via le réseau. Assurez-vous que seuls les fichiers et les mises à niveau appropriés sont partagés.
* **Type de fichier** : le partage d’un dossier [!DNL Assets] du type `sling:OrderedFolder` n’est pas pris en charge dans le cadre du partage dans [!DNL Adobe Experience Cloud]. Si vous souhaitez partager un dossier, lors de sa création dans [!DNL Assets], ne sélectionnez pas l’option [!UICONTROL Ordonné].

## Bonnes pratiques {#best-practices}

Les bonnes pratiques d’utilisation du partage de dossier entre [!DNL Experience Manager] et [!DNL Creative Cloud] comprennent :

* **Considérations relatives au volume :** le partage de dossiers entre [!DNL Experience Manager] et [!DNL Creative Cloud] doit être utilisé pour partager un plus petit nombre de fichiers, par exemple pour une campagne ou une activité spécifique. Pour partager de plus grands ensembles de ressources, comme toutes les ressources approuvées dans l’organisation, utilisez d’autres méthodes de distribution (par exemple, [!DNL Assets Brand Portal]) ou l’application de bureau [!DNL Experience Manager].
* **Évitez de partager des hiérarchies profondes :** le partage doit se produire de manière récurrente et ne permet pas l’annulation sélective du partage. En règle générale, seuls les dossiers sans sous-dossiers, ou ayant une hiérarchie simple, comme un niveau de sous-dossiers, doivent être considérés pour le partage.
* **Partage unilatéral de dossiers séparés :** des dossiers séparés doivent être utilisés pour partager les ressources finales de [!DNL Assets] vers [!DNL Creative Cloud], et pour partager en retour les ressources dont les créations sont prêtes à l’emploi de [!DNL Creative Cloud] vers [!DNL Assets]. Cette pratique, associée à une bonne convention d’attribution des noms de dossiers, permet de créer un environnement de travail intuitif pour les utilisateurs d’[!DNL Assets] comme de [!DNL Creative Cloud].
* **Évitez les travaux en cours dans le dossier partagé :** N’utilisez pas de dossier partagé pour le travail en cours : utilisez un dossier distinct dans les fichiers du Creative Cloud pour effectuer des tâches qui nécessitent des modifications fréquentes du fichier.
* **Démarrez les nouvelles tâches en dehors du dossier partagé :** les nouvelles conceptions (fichiers créatifs) doivent être démarrées dans un dossier séparé de travail en cours dans Creative Cloud Files. Lorsqu’elles sont prêtes à être partagées avec les utilisateurs d’[!DNL Assets], elles doivent être déplacées ou enregistrées dans le dossier partagé.
* **Simplifiez la structure de partage :** pour une configuration opérationnelle plus gérable, pensez à simplifier la structure de partage. Au lieu de partager les dossiers [!DNL Assets] avec tous les spécialistes de la création, ils doivent être partagés uniquement avec les représentants de l’équipe, tels qu’un directeur ou une directrice artistique ou un(e) responsable d’équipe. Le responsable artistique doit recevoir les ressources finales, déterminer l’attribution des tâches, puis permettre aux concepteurs de travailler sur les ressources de travail en cours sur leurs comptes Creative Cloud respectifs. Il peut utiliser les fonctions de collaboration Creative Cloud pour coordonner le travail et, finalement, sélectionner et replacer les ressources prêtes à être partagées dans [!DNL Assets], au sein du dossier partagé dédié aux créations.

Le diagramme suivant illustre un exemple de configuration pour créer des conceptions basées sur les ressources finales existantes à partir d’[!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
