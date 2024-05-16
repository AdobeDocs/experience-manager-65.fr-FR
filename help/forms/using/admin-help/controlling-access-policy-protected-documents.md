---
title: Contrôler l’accès à un document protégé par une politique
description: Découvrez comment afficher, gérer et contrôler l’accès à vos documents protégés par une politique.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '2167'
ht-degree: 100%

---

# Contrôler l’accès à un document protégé par une politique {#controlling-access-to-policy-protected-documents}

Vous pouvez contrôler la manière dont les destinataires utilisent vos documents protégés par une politique, quel que soit leur mode de distribution.

La page Documents vous permet d’effectuer les tâches suivantes :

* Rechercher et afficher les détails des documents protégés par une politique. Les informations disponibles englobent le nom du document, le nom de l’éditeur, le nom de la politique et la date d’application de la politique. Si la politique qui protégeait un document est supprimée, vous pouvez également voir l’ID de la politique supprimé sous le nom de la politique. Les utilisateurs et utilisatrices peuvent afficher et gérer leurs propres documents protégés par une politique. Les administrateurs et administratrices peuvent afficher et gérer tous les documents protégés par une politique.
* Modifiez les détails de la politique appliquée à un document. Les utilisateurs et utilisatrices peuvent modifier leurs propres politiques, les administrateurs et administratrices peuvent modifier des politiques partagées et personnelles et les coordinateurs et coordinatrices de jeux de politiques peuvent modifier des politiques partagées dans les jeux de politiques pour lesquels ils disposent d’autorisations. Vous pouvez accéder à la politique associée à un document directement à partir de la page Détails du document.
* Révoquer et rétablir l’accès à un document protégé par une politique. Les administrateurs et administratrices peuvent révoquer et rétablir l’accès à n’importe quel document. Les coordinateurs et coordinatrices de jeux de politiques (qui sont autorisés à gérer des documents) peuvent révoquer et rétablir l’accès aux documents protégés par une politique qui utilisent des politiques partagées de leurs jeux de politiques. Les utilisateurs et utilisatrices peuvent révoquer l’accès à leurs documents protégés par une politique s’ils ont créé la politique qui protège le document ou si la politique est partagée et autorise cette fonctionnalité.
* Changer la politique appliquée à un document. Les utilisateurs et utilisatrices qui appliquent des politiques à des documents peuvent changer de politique s’ils les ont créées ou s’il s’agit d’une politique partagée qui active cette fonctionnalité. Les coordinateurs et coordinatrices de jeux de politiques peuvent changer de politique dans leurs jeux de politiques. Les administrateurs et administratrices peuvent changer de politique appliquée à n’importe quel document.

Lorsqu’un document est protégé par une politique et que vous révoquez des privilèges d’accès ou changez de politique appliquée, les modifications prennent effet comme suit :

* Si le document est en ligne, les modifications sont appliquées immédiatement, sauf si l’utilisateur ou l’utilisatrice l’a ouvert. Dans ce cas, l’utilisateur ou l’utilisatrice doit fermer le document pour que les modifications soient prises en compte.
* Si un ou une destinataire utilise le document hors connexion (par exemple, sur un ordinateur portable), les modifications prennent effet la prochaine fois que le ou la destinataire se synchronise avec Document Security en ouvrant un document protégé par une politique.

## Affichage des informations sur un document {#view-information-about-a-document}

Pour chaque document répertorié dans la page Documents, vous pouvez afficher le nom du document, le nom de l’éditeur, le nom de la politique et la date à laquelle le document a été protégé. Si la politique qui protégeait un document a été supprimée, l’ID de la politique est répertorié sous Nom de la politique.

Vous pouvez également afficher plus de détails, décrits ci-dessous, sur un document particulier sur la page Détails du document :

>[!NOTE]
>
>Utilisez le lien Nom de la politique sur la page Détails du document pour accéder aux politiques générées automatiquement dans Microsoft Outlook pour les destinataires d’un document joint à un e-mail. Ces politiques n’apparaissent pas dans la page des politiques.

**Nom du document :** nom du document sélectionné.

**ID du document :** identifiant unique attribué par Document Security lorsqu’une politique est appliquée au document. Document Security utilise ce numéro pour assurer le suivi du document.

**Statut du document :** statut du document (par exemple actif ou révoqué).

**Éditeur :** nom de l’utilisateur qui a appliqué la politique au document.

**Nom de la politique :** nom de la politique utilisée pour protéger le document. Vous pouvez cliquer sur le nom pour ouvrir la politique. Utilisez ce lien pour accéder aux politiques générées par Acrobat pour les destinataires d’un document joint à un e-mail dans Outlook. Ces politiques n’apparaissent pas dans la page Politiques.

**Type de politique :** type de la politique appliquée au document.

**Date de publication :** date à laquelle la politique a été appliquée au document.

**Itérations associées :** si des itérations sont associées au document, elles apparaissent aussi dans la liste. Cliquez sur le lien pour afficher la liste des itérations associées pour le document.

Les utilisateurs et utilisatrices peuvent afficher des informations sur leurs documents protégés. Les administrateurs et administratrices peuvent afficher des informations sur les documents protégés par une politique par un utilisateur ou une utilisatrice. Les coordinateurs et coordinatrices de jeux de politiques peuvent afficher des informations sur les documents protégés par des politiques provenant de leurs jeux de politiques.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié. La page Détails du document s’ouvre, affichant des informations détaillées relatives au document. Cette page fournit également des options permettant de révoquer l’accès au document, de changer de politique et d’afficher les événements liés à ce document.

## Affichage des itérations associées pour un document {#view-related-iterations-for-a-document}

Si le suivi des itérations associées est activé, vous pouvez suivre les versions d’un document enregistrées par différents utilisateurs ou différentes utilisatrices. Cette fonctionnalité n’est prise en charge que par certaines applications, telles que PTC Pro/ENGINEER Wildfire.

Cette fonctionnalité est utile lorsque plusieurs utilisateurs ou utilisatrices collaborent et enregistrent différentes versions du même document. Document Security peut effectuer le suivi des différentes itérations. Par conséquent, vous pouvez facilement afficher les informations sur les documents pour les différentes versions.

Si cette fonctionnalité est activée, vous pouvez afficher les itérations associées d’un document à partir de la page Documents.

1. Affichez la page Détails du document pour un document. (voir [Affichage des informations sur un document](controlling-access-policy-protected-documents.md#view-information-about-a-document)).
1. Cliquez sur Afficher les itérations associées. Cette option n’est disponible que si la fonctionnalité est activée. La liste des itérations associées s’affiche. Pour chaque itération, vous pouvez afficher les informations suivantes :

   * **Itération :** nom de fichier Il peut différer du nom de fichier d’origine et se termine généralement par un numéro de version.
   * **Editeur :** éditeur du document d’origine
   * **Créé par :** utilisateur qui a enregistré l’itération
   * **Date de création :** date et heure d’enregistrement de l’itération
   * **Politique :** politique qui protège l’itération Différentes itérations peuvent être protégées par différentes politiques.

1. Pour afficher la page Détails du document de cette itération, cliquez sur le nom de fichier d’une itération.

## Révocation et rétablissement de l’accès aux documents {#revoking-and-reinstating-access-to-documents}

Vous pouvez révoquer et rétablir l’accès aux documents protégés par une politique :

**Utilisateurs :** peuvent révoquer ou rétablir l’accès aux documents qu’ils protègent avec leurs propres politiques personnelles ou avec des politiques partagées pour lesquelles le droit de révocation est activé pour les utilisateurs qui appliquent la politique. les utilisateurs qui ne peuvent pas révoquer l’accès à un document ou changer de politique doivent contacter un administrateur.

**Administrateurs :** peuvent révoquer ou rétablir les privilèges d’accès aux documents protégés par une politique, notamment ceux qui sont protégés par des politiques personnelles ou partagées. Si un administrateur révoque l’accès à un document protégé par une politique partagée, seul un administrateur peut rétablir les privilèges d’accès à ce document.

**Coordinateurs de jeux de politiques :** peuvent révoquer ou rétablir les privilèges d’accès aux documents protégés par des politiques appartenant à leurs jeux.

Lorsque vous révoquez ou rétablissez des privilèges d’accès à des documents, l’application de la modification varie selon l’état du document :

* Si le document est en ligne et fermé, la modification est appliquée lorsque le ou la destinataire se synchronise avec Document Security en ouvrant un document protégé par une politique.
* Si le document est en ligne et ouvert, la modification prend effet lorsque le ou la destinataire le ferme.
* Si le document est hors ligne, à savoir qu’il est utilisé sans connexion Internet, par exemple sur un ordinateur portable, la modification prend effet lors de la synchronisation suivante du ou de la destinataire avec Document Security.

**Révocation de l’accès à un document protégé par une politique**

1. Dans la page Document Security, cliquez sur Documents.
1. Cochez la case en regard du document approprié, puis cliquez sur Révoquer. Vous pouvez révoquer l’accès à plusieurs documents à la fois.
1. Sélectionnez un message à afficher pour les personnes qui tentent d’ouvrir le document après sa révocation :

   * **Message général :** indique que l’auteur a révoqué le document.
   * **Document arrêté :** indique que l’auteur a arrêté le document.
   * **Document révisé** : indique que l’auteur ou l’autrice a révisé le document.

1. (Facultatif) Si une version plus récente du document est disponible, saisissez l’URL et cliquez sur Tester pour vérifier l’URL.
1. Cliquez sur OK, puis de nouveau sur OK pour revenir à la page Documents.

**Rétablissement de privilèges d’accès aux documents**

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Annuler la révocation, puis sur OK.

## Changement de la politique appliquée à un document {#switch-a-policy-that-is-applied-to-a-document}

Les utilisateurs et utilisatrices, les coordinateurs et coordinatrices de jeux de politiques et les équipes d’administration peuvent changer la politique appliquée à un document protégé par une politique (vous ne pouvez appliquer qu’une seule politique à la fois à un document). Les utilisateurs et utilisatrices peuvent changer la politique appliquée à leurs propres documents protégés par une politique s’ils ont créé la politique ou si la politique est partagée et que cette fonctionnalité est activée. Dans le cas contraire, l’équipe d’administration, le coordinateur ou la coordinatrice de jeux de politiques doit changer de politique. Les administrateurs et administratrices peuvent changer la politique des documents protégés de l’ensemble des utilisateurs et utilisatrices. Les coordinateurs et coordinatrices de jeux de politiques peuvent changer de politique dans leurs jeux de politiques.

Lorsque vous changez de politique, la nouvelle politique est appliquée comme suit :

* Si le document est en ligne et fermé, la modification prend effet la prochaine fois que le ou la destinataire se synchronise avec Document Security en ouvrant un document en ligne protégé par une politique.
* Si le document est en ligne et ouvert, la modification prend effet lorsque la personne ferme le document.
* Si le document est hors ligne (utilisé sans connexion à Internet ou au réseau, sur un ordinateur portable par exemple), la modification est appliquée lorsque la personne se synchronise avec Document Security en ouvrant un document en ligne protégé par une politique.

>[!NOTE]
>
>Si vous souhaitez autoriser un accès anonyme à un document protégé par une politique qui ne permet pas ce type d’accès, vous devez supprimer la politique existante dans l’application cliente, puis en appliquer une qui autorise l’accès anonyme. Si vous changez de politique, les utilisateurs et utilisatrices doivent ouvrir une session pour accéder au document.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Changer de politique. Une liste proposant jusqu’à 100 politique apparaît.
1. Si la politique souhaitée n’apparaît pas, sélectionnez Nom de la politique ou ID de la politique dans la liste Rechercher, saisissez le nom ou l’ID de la politique, puis cliquez sur Rechercher.
1. Cliquez sur une nouvelle politique dans la liste.
1. Cliquez sur Changer de politique, puis sur OK pour revenir à la page Documents.

## Recherche d’un document {#search-for-a-document}

Vous pouvez rechercher des documents dans la page Documents en combinant des critères de périodes et de recherche disponibles dans la liste. Ces critères incluent le nom du document, le nom de la politique ou tous les documents.

Certaines options de recherche supplémentaires ne sont disponibles que pour les administrateurs et administratrices :

**ID du document :** numéro d’ID unique attribué par Document Security au document lorsque la politique est appliquée.

**Nom du document :** nom du document.

**Nom de l’éditeur :** nom de l’utilisateur qui a appliqué la politique au document. Vous pouvez sélectionner l’utilisateur à partir de tous les domaines ou d’un domaine spécifique.

**ID de la politique :** ID de la politique appliquée au document.

**Nom de la politique :** nom de la politique appliquée au document.

**Tous les documents :** tous les documents protégés par les administrateurs et les utilisateurs. L’utilisation de cette option risque de renvoyer une liste de documents particulièrement longue.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste Rechercher, sélectionnez les critères de recherche requis.

   Vous pouvez spécifier les critères tels que l’ID du document, le nom du document, le nom de l’éditeur ou de l’éditrice, l’ID de la politique, le nom de la politique ou tous les documents.

   Si vous indiquez le nom de l’éditeur ou de l’éditrice, cliquez sur l’icône Carnet d’adresses, indiquez le domaine dans lequel rechercher l’utilisateur ou l’utilisatrice, puis cliquez sur OK pour revenir à la page de recherche Documents.

1. (Facultatif) Dans la liste Date, sélectionnez une option de période. Si vous sélectionnez Dates personnalisées, saisissez la date au format aaaa/mm/jj dans les zones qui s’affichent ou utilisez le sélecteur de date pour spécifier la période :

   * Cliquez sur le calendrier pour ouvrir le Sélecteur de date.
   * Utilisez les flèches pour sélectionner l’année et le mois.
   * Cliquez sur un jour du mois dans le calendrier.
   * Cliquez sur OK pour fermer le Sélecteur de date.

1. Cliquez sur Rechercher.

## Tri de la liste des documents {#sort-the-document-list}

Vous pouvez trier la liste des documents par en-tête de colonne. Le triangle situé à côté de l’en-tête de colonne indique la colonne triée. Lorsque le triangle est dirigé vers le haut, l’ordre de tri est croissant et lorsqu’il est dirigé vers le bas, l’ordre de tri est décroissant.

1. Dans la page Document Security, cliquez sur Documents.
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur la colonne.

## Ajout d’une page de garde à un document protégé par une police {#add-cover-page-to-policy-protected-documents}

Dans la plupart des visionneuses PDF autres qu’Adobe, si vous ouvrez un document protégé par Document Security, la première page est vide ou l’application s’interrompt sans ouvrir le document.

Vous pouvez utiliser la prise en charge Page 0 (Wrapper Document) pour permettre aux visionneuses PDF autres qu’Adobe d’ouvrir un document protégé et d’afficher la page de garde du document.

>[!NOTE]
>
>Lors de l’affichage de tels documents (contenant une page 0) dans Adobe Reader/Acrobat ou Mobile Reader, le document protégé est ouvert par défaut.

**Pour ajouter une page de garde à un document protégé par une police**

Utilisez les processus suivants dans Workbench :

**Protection
du document avec une page de garde :** sécurise un document PDF avec la politique spécifiée et ajoute une page de garde au document.

**Extraction du document protégé :** extrait le document PDF protégé par une politique du document PDF avec page de garde.

Utilisez les API de Document Security suivants :

**protectDocumentWithCoverPage :** sécurise un PDF donné avec la stratégie spécifiée et renvoie un document avec une page de garde et le document protégé en tant que pièce jointe.
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument :** extrait le document protégé qui est une pièce jointe dans le document avec la page de garde. Le document avec la page de garde peut être créé à l’aide de la méthode protectDocumentWithCoverPage. `//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
