---
title: Contrôler l’accès à un document protégé par une politique
seo-title: Controlling access to policy-protected documents
description: Découvrez comment afficher, gérer et contrôler l’accès à vos documents protégés par une stratégie.
seo-description: See how you can view, manage and control the access to your policy-protected documents.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 22%

---

# Contrôler l’accès à un document protégé par une politique {#controlling-access-to-policy-protected-documents}

Vous pouvez contrôler la manière dont les destinataires utilisent vos documents protégés par une stratégie, quelle que soit la manière dont vous les distribuez.

La page Documents vous permet d’effectuer les tâches suivantes :

* Recherchez et affichez les détails des documents protégés par une stratégie. Vous pouvez afficher des informations sur le nom du document, le nom de l’éditeur, le nom de la stratégie et la date d’application de la stratégie. Si la stratégie qui protégeait un document est supprimée, vous pouvez également voir l’ID de stratégie supprimé sous le nom de la stratégie. Les utilisateurs peuvent afficher et gérer leurs propres documents protégés par une stratégie. Les administrateurs peuvent afficher et gérer tous les documents protégés par une stratégie.
* Modifiez les détails de la stratégie appliquée à un document. Les utilisateurs peuvent modifier leurs propres stratégies, les administrateurs peuvent modifier des stratégies partagées et personnelles et les coordinateurs de jeux de stratégies peuvent modifier des stratégies partagées dans les jeux de stratégies pour lesquels ils disposent d’autorisations. Vous pouvez accéder à la stratégie associée à un document directement à partir de la page Détails du document .
* Révoquez et rétablissez l’accès à un document protégé par une stratégie. Les administrateurs peuvent révoquer et rétablir l’accès à n’importe quel document. Les coordinateurs de jeux de stratégies (qui sont autorisés à gérer des documents) peuvent révoquer et rétablir l’accès aux documents protégés par une stratégie qui utilisent des stratégies partagées de leurs jeux de stratégies. Les utilisateurs peuvent révoquer l’accès à leurs documents protégés par une stratégie s’ils ont créé la stratégie qui protège le document ou si la stratégie est partagée et autorise cette fonctionnalité.
* Changer la stratégie appliquée à un document. Les utilisateurs qui appliquent des stratégies à des documents peuvent changer de stratégie s’ils les ont créées ou s’il s’agit d’une stratégie partagée qui active cette fonctionnalité. Les coordinateurs de jeux de stratégies peuvent changer de stratégie à partir de leurs jeux de stratégies. Les administrateurs peuvent changer de stratégie appliquée à n’importe quel document.

Lorsqu’un document est protégé par une stratégie et que vous révoquez des privilèges d’accès ou changez de stratégie appliquée, les modifications prennent effet comme suit :

* Si le document est en ligne, les modifications sont appliquées immédiatement, sauf si l’utilisateur l’a ouvert. Dans ce cas, l’utilisateur doit fermer le document pour que les modifications soient prises en compte.
* Si un destinataire utilise le document hors connexion (par exemple, sur un ordinateur portable), les modifications prennent effet la prochaine fois que le destinataire se synchronise avec Document Security en ouvrant un document protégé par une stratégie.

## Affichage des informations sur un document {#view-information-about-a-document}

Pour chaque document répertorié dans la page Documents, vous pouvez afficher le nom du document, le nom de l’éditeur, le nom de la stratégie et la date à laquelle le document a été protégé. Si la stratégie qui protégeait un document a été supprimée, l’ID de la stratégie est répertorié sous Nom de la stratégie.

Vous pouvez également afficher plus de détails, décrits ci-dessous, sur un document particulier sur la page Détails du document :

>[!NOTE]
>
>Vous devez utiliser le lien Nom de la stratégie sur la page Détails du document pour accéder aux stratégies générées automatiquement dans Microsoft Outlook pour les destinataires d’un document joint à un message électronique. Ces stratégies n’apparaissent pas dans la page des stratégies.

**Nom du document :** nom du document sélectionné.

**ID du document :** identifiant unique attribué par Document Security lorsqu’une politique est appliquée au document. Document Security utilise ce numéro pour assurer le suivi du document.

**Statut du document :** statut du document (par exemple actif ou révoqué).

**Éditeur :** nom de l’utilisateur qui a appliqué la politique au document.

**Nom de la politique :** nom de la politique utilisée pour protéger le document. Vous pouvez cliquer sur le nom pour ouvrir la stratégie. Vous devez utiliser ce lien pour accéder aux stratégies générées par Acrobat pour les destinataires d’un document joint à un message électronique dans Outlook. Ces stratégies n’apparaissent pas dans la page Stratégies .

**Type de politique :** type de la politique appliquée au document.

**Date de publication :** date à laquelle la politique a été appliquée au document.

**Itérations associées :** si des itérations sont associées au document, elles apparaissent aussi dans la liste. Cliquez sur le lien pour afficher la liste des itérations associées pour le document.

Les utilisateurs peuvent afficher des informations sur leurs documents protégés. Les administrateurs peuvent afficher des informations sur les documents protégés par une stratégie par un utilisateur. Les coordinateurs de jeux de stratégies peuvent afficher des informations sur les documents protégés par des stratégies provenant de leurs jeux de stratégies.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié. La page Détails du document s’ouvre, affichant des informations détaillées sur le document. Cette page fournit également des options permettant de révoquer l’accès au document, de changer de stratégie et d’afficher les événements liés à ce document.

## Affichage des itérations associées pour un document {#view-related-iterations-for-a-document}

Si le suivi des itérations associées est activé, vous pouvez effectuer le suivi des versions d’un document enregistrées par différents utilisateurs. Cette fonctionnalité est prise en charge uniquement par certaines applications, telles que PTC Pro/ENGINEER Wildfire.

Cette fonctionnalité est utile lorsque plusieurs utilisateurs collaborent et enregistrent différentes versions du même document. Document Security peut effectuer le suivi des différentes itérations. Par conséquent, vous pouvez facilement afficher les informations sur les documents pour les différentes versions.

Si cette fonction est activée, vous pouvez afficher les itérations associées d’un document à partir de la page Documents.

1. Affichez la page Détails du document d’un document. (Voir [Affichage des informations sur un document](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Cliquez sur Afficher les itérations associées. Cette option n’est disponible que si la fonction est activée. La liste des itérations associées s’affiche. Pour chaque itération, vous pouvez afficher les informations suivantes :

   * **Itération :** nom de fichier Il peut différer du nom de fichier d’origine et se termine généralement par un numéro de version.
   * **Editeur :** éditeur du document d’origine
   * **Créé par :** utilisateur qui a enregistré l’itération
   * **Date de création :** date et heure d’enregistrement de l’itération
   * **Politique :** politique qui protège l’itération Différentes itérations peuvent être protégées par différentes stratégies.

1. Pour afficher la page Détails du document de cette itération, cliquez sur le nom de fichier d’une itération.

## Révocation et rétablissement de l’accès aux documents {#revoking-and-reinstating-access-to-documents}

Vous pouvez révoquer et rétablir l’accès aux documents protégés par une stratégie :

**Utilisateurs :** peuvent révoquer ou rétablir l’accès aux documents qu’ils protègent avec leurs propres politiques personnelles ou avec des politiques partagées pour lesquelles le droit de révocation est activé pour les utilisateurs qui appliquent la politique. les utilisateurs qui ne peuvent pas révoquer l’accès à un document ou changer de politique doivent contacter un administrateur.

**Administrateurs :** peuvent révoquer ou rétablir les privilèges d’accès aux documents protégés par une politique, notamment ceux qui sont protégés par des politiques personnelles ou partagées. Si un administrateur révoque l’accès à un document protégé par une politique partagée, seul un administrateur peut rétablir les privilèges d’accès à ce document.

**Coordinateurs de jeux de politiques :** peuvent révoquer ou rétablir les privilèges d’accès aux documents protégés par des politiques appartenant à leurs jeux.

Lorsque vous révoquez ou rétablissez des privilèges d’accès aux documents, la modification prend effet aux moments suivants :

* Si le document est en ligne et fermé, la modification prend effet la prochaine fois que le destinataire se synchronise avec Document Security en ouvrant un document protégé par une stratégie.
* Si le document est en ligne et ouvert, la modification prend effet lorsque le destinataire ferme le document.
* Si le document est hors ligne (utilisé sans connexion Internet, par exemple sur un ordinateur portable), la modification prend effet lors de la prochaine synchronisation du destinataire avec Document Security.

**Révocation de l’accès à un document protégé par une stratégie**

1. Dans la page Document Security, cliquez sur Documents.
1. Cochez la case en regard du document approprié, puis cliquez sur Révoquer. Vous pouvez révoquer l’accès à plusieurs documents à la fois.
1. Sélectionnez un message à afficher pour les utilisateurs qui tentent d’ouvrir le document après sa révocation :

   * **Message général :** indique que l’auteur a révoqué le document.
   * **Document arrêté :** indique que l’auteur a arrêté le document.
   * **Document révisé**: indique que l’auteur a modifié le document.

1. (Facultatif) Si une version plus récente du document est disponible, saisissez l’URL et cliquez sur Tester pour vérifier l’URL.
1. Cliquez sur OK, puis de nouveau sur OK pour revenir à la page Documents.

**Rétablissement des privilèges d’accès aux documents**

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Annuler la révocation, puis sur OK.

## changer une stratégie appliquée à un document ; {#switch-a-policy-that-is-applied-to-a-document}

Les utilisateurs, les coordinateurs de jeux de stratégies et les administrateurs peuvent changer la stratégie appliquée à un document protégé par une stratégie (vous ne pouvez appliquer qu’une seule stratégie à la fois à un document). Les utilisateurs peuvent changer de stratégie appliquée à leurs propres documents protégés par une stratégie s’ils ont créé la stratégie ou si la stratégie est partagée et que cette fonctionnalité est activée. Dans le cas contraire, l’administrateur ou le coordinateur de jeux de stratégies doit changer de stratégie. Les administrateurs peuvent changer de stratégie pour les documents protégés par une stratégie de n’importe quel utilisateur. Les coordinateurs de jeux de stratégies peuvent changer de stratégie à partir de leurs jeux de stratégies.

Lorsque vous changez de stratégie, la nouvelle stratégie est appliquée comme suit :

* Si le document est en ligne et fermé, la modification prend effet la prochaine fois que le destinataire se synchronise avec Document Security en ouvrant un document en ligne protégé par une stratégie.
* Si le document est en ligne et ouvert, la modification prend effet lorsque l’utilisateur ferme le document.
* Si le document est hors ligne (utilisé sans connexion Internet ou réseau active, sur un ordinateur portable par exemple), la modification est appliquée la prochaine fois que l’utilisateur se synchronise avec Document Security en ouvrant un document en ligne protégé par une stratégie.

>[!NOTE]
>
>Pour autoriser l’accès anonyme à un document protégé par une stratégie qui ne dispose actuellement pas de cet accès, supprimez la stratégie existante dans l’application cliente, puis appliquez une stratégie qui autorise l’accès anonyme. Si vous changez de stratégie, les utilisateurs doivent toujours se connecter pour accéder au document.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Changer de stratégie. Une liste de 100 stratégies au maximum s’affiche.
1. Si la stratégie souhaitée ne s’affiche pas, sélectionnez Nom de la stratégie ou ID de la stratégie dans la liste Rechercher, saisissez le nom ou l’identifiant, puis cliquez sur Rechercher.
1. Cliquez sur une nouvelle stratégie dans la liste.
1. Cliquez sur Changer de stratégie, puis sur OK pour revenir à la page Documents.

## Recherche d’un document {#search-for-a-document}

Vous pouvez rechercher des documents sur la page Documents en combinant des critères de période et des critères de recherche disponibles dans la liste. Ces critères incluent le nom du document, le nom de la stratégie ou tous les documents.

Certaines options de recherche supplémentaires ne sont disponibles que pour les administrateurs :

**ID du document :** numéro d’ID unique attribué par Document Security au document lorsque la politique est appliquée.

**Nom du document :** nom du document.

**Nom de l’éditeur :** nom de l’utilisateur qui a appliqué la politique au document. Vous pouvez sélectionner l’utilisateur à partir de tous les domaines ou d’un domaine spécifique.

**ID de la politique :** ID de la politique appliquée au document.

**Nom de la politique :** nom de la politique appliquée au document.

**Tous les documents :** tous les documents protégés par les administrateurs et les utilisateurs. L’utilisation de l’option Tous les documents pour effectuer une recherche peut renvoyer une longue liste de documents.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste Rechercher, sélectionnez les critères de recherche requis.

   Vous pouvez spécifier les critères comme ID de document, nom du document, nom de l’éditeur, identifiant de la stratégie, nom de la stratégie ou tous les documents.

   Si vous indiquez le nom de l’éditeur, cliquez sur l’icône Carnet d’adresses, indiquez le domaine dans lequel vous souhaitez rechercher l’utilisateur, puis cliquez sur OK pour revenir à la page de recherche Documents.

1. (Facultatif) Dans la liste Date, sélectionnez une option de période. Si vous sélectionnez Dates personnalisées, saisissez la date au format aaaa/mm/jj dans les zones qui s’affichent ou utilisez le sélecteur de date pour spécifier la période :

   * Cliquez sur le calendrier pour ouvrir le sélecteur de date.
   * Utilisez les flèches pour trouver un an et un mois.
   * Cliquez sur un jour du mois dans le calendrier.
   * Cliquez sur OK pour fermer le sélecteur de date.

1. Cliquez sur Rechercher.

## Tri de la liste des documents {#sort-the-document-list}

Vous pouvez trier la liste des documents par en-tête de colonne. Les icônes en forme de triangle en regard de l’en-tête de colonne indiquent la colonne à trier. Un triangle orienté vers le haut indique l’ordre croissant, tandis qu’un triangle orienté vers le bas indique l’ordre décroissant.

1. Dans la page Document Security, cliquez sur Documents.
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur la colonne.

## Ajout d’une page de garde à des documents protégés par une stratégie {#add-cover-page-to-policy-protected-documents}

Si la plupart des visionneuses ne sont pas Adobe PDF, si vous ouvrez un document protégé par Document Security, la première page s’affiche sous la forme d’une page vierge ou l’application s’arrête sans ouvrir le document.

Vous pouvez utiliser la prise en charge de la page 0 (Wrapper Document) pour permettre aux visionneuses non Adobe PDF d’ouvrir un document protégé et d’afficher une page de garde dans le document.

>[!NOTE]
>
>Lors de l’affichage de tels documents (contenant une page 0) dans Adobe Reader/Acrobat ou Mobile Reader, le document protégé est ouvert par défaut.

**Pour ajouter une page de garde à un document protégé par une stratégie**

Utilisez les processus suivants dans Workbench :

**Protection
du document avec une page de garde :** sécurise un document PDF avec la politique spécifiée et ajoute une page de garde au document.

**Extraction du document protégé :** extrait le document PDF protégé par une politique du document PDF avec page de garde.

Utilisez les API de Document Security suivants :

**protectDocumentWithCoverPage :** sécurise un PDF donné avec la stratégie spécifiée et renvoie un document avec une page de garde et le document protégé en tant que pièce jointe.
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument :** extrait le document protégé qui est une pièce jointe dans le document avec la page de garde. Le document avec la page de garde peut être créé à l’aide de la méthode protectDocumentWithCoverPage. `//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
