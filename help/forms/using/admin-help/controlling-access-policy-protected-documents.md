---
title: Contrôle de l’accès à un document protégé par une stratégie
seo-title: Contrôle de l’accès à un document protégé par une stratégie
description: Découvrez comment vous pouvez afficher, gérer et contrôler l’accès à vos documents protégés par une stratégie.
seo-description: Découvrez comment vous pouvez afficher, gérer et contrôler l’accès à vos documents protégés par une stratégie.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 85%

---


# Contrôle de l’accès à un document protégé par une stratégie {#controlling-access-to-policy-protected-documents}

Vous pouvez contrôler la manière dont les destinataires utilisent vos documents protégés par une stratégie, quel que soit leur mode de distribution.

La page Documents vous permet d’effectuer les tâches suivantes :

* Rechercher et afficher les détails des documents protégés par une stratégie. Les informations disponibles englobent le nom du document, le nom de l’éditeur, le nom de la stratégie et la date d’application de la stratégie. Si la stratégie qui protégeait un document est supprimée, l’ID de la stratégie supprimée apparaît également sous son nom. Les utilisateurs peuvent afficher et gérer leurs propres documents protégés par une stratégie. Les administrateurs peuvent afficher et gérer tous les documents protégés par une stratégie.
* Modifier les détails de la stratégie appliquée à un document. Les utilisateurs peuvent modifier leurs propres stratégies ; les administrateurs peuvent modifier les stratégies partagées et les stratégies personnelles ; et les coordinateurs de jeux de stratégies peuvent modifier les stratégies partagées figurant dans les jeux de stratégies sur lesquels ils disposent des droits appropriés. Vous pouvez accéder à la stratégie associée à un document, directement depuis la page Détails du document.
* Révoquer et rétablir l’accès à un document protégé par une stratégie. Les administrateurs peuvent révoquer et rétablir l’accès à tous les documents. Les coordinateurs de jeux de stratégies (autorisés à gérer les documents) peuvent révoquer et rétablir l’accès aux documents protégés par une stratégie qui utilisent des stratégies partagées relevant de leurs jeux de stratégies. Les utilisateurs peuvent révoquer l’accès à leurs documents protégés par une stratégie s’ils ont créé la stratégie qui protège le document ou si la stratégie est une stratégie partagée autorisant cette opération.
* Changer la stratégie appliquée à un document. Les utilisateurs qui appliquent des stratégies à des documents peuvent changer de stratégie s’ils ont créé la stratégie ou s’il s’agit d’une stratégie partagée autorisant cette opération. Les coordinateurs de jeux de stratégies peuvent choisir une autre stratégie dans leurs jeux. Les administrateurs peuvent changer les stratégies appliquées à n’importe quel document.

Lorsqu’un document est protégé par une stratégie et que vous révoquez des privilèges d’accès ou changez la stratégie appliquée, la modification est appliquée dans les conditions suivantes :

* Si le document est en ligne, la modification est appliquée immédiatement, sauf si l’utilisateur a ouvert le document. Si tel est le cas, l’utilisateur doit fermer le document pour que la modification soit prise en compte.
* Si un destinataire utilise le document hors connexion (par exemple, sur un ordinateur portable), la modification prend effet lorsque le destinataire se synchronise avec Document Security en ouvrant un document protégé par une stratégie.

## Affichage des informations sur un document {#view-information-about-a-document}

Pour chacun des documents répertoriés dans la page Documents, vous pouvez voir le nom du document, le nom de l’éditeur, le nom de la stratégie et la date à laquelle le document a été protégé. Si la stratégie qui protégeait un document a été supprimée, son ID apparaît sous le nom de la stratégie.

La page Détails du document permet également d’afficher d’autres informations sur un document, décrites ci-dessous :

>[!NOTE]
>
>Vous devez cliquer sur le lien Nom de la stratégie dans la page Détails du document pour accéder aux stratégies qui sont générées automatiquement dans Microsoft Outlook pour les destinataires d’un document joint à un courrier électronique. Ces stratégies n’apparaissent pas dans la page Stratégies.

**Nom du document :** nom du document sélectionné.

**ID de document :** identifiant unique attribué par document Security lorsqu’une stratégie est appliquée au document. Document Security utilise ce numéro pour assurer le suivi du document.

**Etat du document :** état du document (principal ou révoqué, par exemple).

**Editeur :** nom de l’utilisateur qui a associé la stratégie au document.

**Nom de la stratégie : nom** de la stratégie utilisée pour protéger le document. Vous pouvez cliquer sur le nom pour ouvrir la stratégie. Utilisez ce lien pour accéder aux stratégies générées par Acrobat pour les destinataires d’un document joint à un courrier électronique dans Outlook. Ces stratégies n’apparaissent pas dans la page Stratégies.

**Type de stratégie :** type de stratégie appliqué au document.

**Date de publication : date** à laquelle la stratégie a été appliquée au document.

**Itérations associées :** si le document comporte des itérations associées, cet élément apparaît également dans la liste. Cliquez sur le lien pour afficher la liste des itérations associées pour le document.

Les utilisateurs peuvent afficher les informations relatives à leurs documents protégés. Les administrateurs peuvent afficher des informations sur les documents que les utilisateurs ont protégés avec une stratégie. Les coordinateurs de jeux de stratégies peuvent afficher des informations sur les documents protégés par des stratégies appartenant à leurs jeux.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié. La page Détails du document qui apparaît affiche des informations détaillées sur le document. Elle fournit également des options permettant de révoquer l’accès au document, de changer de stratégie et d’afficher les événements concernant ce document.

## Affichage des itérations associées pour un document  {#view-related-iterations-for-a-document}

Si le suivi des itérations associées est activé, vous pouvez procéder au suivi des versions d’un document enregistrées par différents utilisateurs. Cette fonction est uniquement prise en charge par certaines applications, telles que PTC Pro/ENGINEER Wildfire.

Elle se révèle très utile lorsque plusieurs utilisateurs collaborent et enregistrent différentes versions du même document. Document Security peut garder la trace des différentes itérations, ce qui vous permet d’afficher facilement les informations du document pour les différentes versions.

Si cette fonction est activée, vous pouvez afficher les itérations associées d’un document à partir de la page Documents.

1. Affichez la page Détails du document d’un document (voir [Affichage des informations sur un document](controlling-access-policy-protected-documents.md#view-information-about-a-document)).
1. Cliquez sur Afficher les itérations associées. Cette option n’est disponible que si la fonction est activée. La liste des itérations associées apparaît. Pour chaque itération, vous pouvez afficher les informations suivantes :

   * **Itération :** nom de fichier Il peut différer du nom de fichier d’origine et se termine généralement par un numéro de version.
   * **Editeur :** éditeur du document d’origine
   * **Créé par :** utilisateur qui a enregistré l’itération
   * **Date de création :** date et heure d’enregistrement de l’itération
   * **Stratégie :** stratégie qui protège l’itération Différentes itérations peuvent être protégées par des stratégies distinctes.

1. Pour afficher la page Détails du document de cette itération, cliquez sur le nom de fichier d’une itération.

## Révocation et rétablissement de l’accès aux documents  {#revoking-and-reinstating-access-to-documents}

Vous pouvez révoquer et rétablir l’accès à des documents protégés par une stratégie :

**Utilisateurs :** peut révoquer ou rétablir l’accès aux documents qu’ils protègent avec leurs propres stratégies personnelles ou avec des stratégies partagées pour lesquelles la fonctionnalité de révocation est activée pour l’utilisateur qui applique la stratégie. les utilisateurs qui ne peuvent pas révoquer l’accès à un document ou changer de stratégie doivent contacter un administrateur.

**Administrateurs :** peut révoquer ou rétablir des privilèges d’accès à tout document protégé par une stratégie, y compris ceux protégés par des stratégies personnelles ou partagées. Si un administrateur révoque l’accès à un document protégé par une stratégie partagée, seul un administrateur peut rétablir les privilèges d’accès à ce document.

**Coordinateurs de jeux de stratégies :** peut révoquer ou rétablir des privilèges d’accès pour les documents protégés par des stratégies issues de leurs jeux de stratégies.

Lorsque vous révoquez ou rétablissez des privilèges d’accès à des documents, l’application de la modification varie selon l’état du document :

* Si le document est en ligne et fermé, la modification est appliquée lorsque le destinataire se synchronise avec Document Security en ouvrant un document protégé par une stratégie.
* Si le document est en ligne et ouvert, la modification prend effet lorsque le destinataire ferme le document.
* Si le document est hors connexion (utilisé sans connexion à Internet, sur un ordinateur portable par exemple), la modification prend effet lorsque le destinataire se resynchronise avec Document Security.

**Révocation de l’accès à un document protégé par une stratégie**

1. Dans la page Document Security, cliquez sur Documents.
1. Cochez la case correspondant au document approprié, puis cliquez sur Révoquer. Vous pouvez révoquer l’accès à plusieurs documents simultanément.
1. Sélectionnez le message à afficher aux utilisateurs qui tentent d’ouvrir le document après sa révocation :

   * **Message général :** indique que l’auteur a révoqué le document.
   * **Document arrêté :** indique que l’auteur a arrêté le document.
   * **Document révisé :** indique que l’auteur a révisé le document.

1. (Facultatif) Si une version plus récente du document est disponible, indiquez son URL et cliquez sur Tester pour vérifier l’URL.
1. Cliquez sur OK, puis de nouveau sur OK pour revenir à la page Documents.

**Rétablissement de privilèges d’accès aux documents**

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Annuler la révocation et cliquez sur OK.

## Changement de la stratégie appliquée à un document  {#switch-a-policy-that-is-applied-to-a-document}

Les utilisateurs, les coordinateurs de jeux de stratégies et les administrateurs peuvent changer la stratégie appliquée à un document protégé (vous ne pouvez appliquer à un document qu’une seule stratégie à la fois). Les utilisateurs peuvent changer la stratégie appliquée à l’un de leurs documents protégés, s’ils ont créé cette stratégie ou s’il s’agit d’une stratégie partagée autorisant cette opération. Dans le cas contraire, seul l’administrateur ou le coordinateur de jeux de stratégies peut changer la stratégie. Les administrateurs peuvent changer les stratégies de n’importe quel document protégé par un utilisateur. Les coordinateurs de jeux de stratégies peuvent choisir une autre stratégie dans leurs jeux.

Lorsque vous changez une stratégie, la nouvelle est appliquée comme suit :

* Si le document est en ligne et fermé, la modification est appliquée lorsque le destinataire se synchronise avec Document Security en ouvrant un document en ligne protégé par une stratégie.
* Si le document est en ligne et ouvert, la modification prend effet lorsque l’utilisateur ferme le document.
* Si le document est hors ligne (utilisé sans connexion à Internet ou au réseau, sur un ordinateur portable par exemple), la modification est appliquée lorsque l’utilisateur se synchronise avec Document Security en ouvrant un document en ligne protégé par une stratégie.

>[!NOTE]
>
>Si vous souhaitez autoriser un accès anonyme à un document protégé par une stratégie qui ne permet pas ce type d’accès, vous devez supprimer la stratégie existante dans l’application cliente, puis en appliquer une qui autorise l’accès anonyme. Si vous changez de stratégie, les utilisateurs doivent ouvrir une session pour accéder au document.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste des documents, cliquez sur le document approprié.
1. Cliquez sur Changer de stratégie. Une liste proposant jusqu’à 100 stratégies apparaît.
1. Si la stratégie souhaitée n’apparaît pas, sélectionnez Nom de la stratégie ou ID de la stratégie dans la liste Rechercher, saisissez le nom ou l’ID de la stratégie, puis cliquez sur Rechercher.
1. Sélectionnez une nouvelle stratégie dans la liste.
1. Cliquez sur Changer de stratégie, puis sur OK pour revenir à la page Documents.

## Recherche d’un document  {#search-for-a-document}

Vous pouvez rechercher des documents dans la page Documents en combinant des plages de dates et des critères de recherche disponibles dans la liste. Ces critères incluent le nom du document, le nom de la stratégie ou tous les documents.

Des options de recherche supplémentaires sont disponibles uniquement pour les administrateurs :

**ID de document : numéro d’ID** unique attribué par document Security au document lorsque la stratégie est appliquée.

**nom du document :** nom du document.

**Nom de l’éditeur :** nom de l’utilisateur qui a associé la stratégie au document. Vous pouvez sélectionner l’utilisateur à partir de tous les domaines ou d’un domaine spécifique.

**ID de stratégie :** ID de la stratégie associée au document.

**Nom de la stratégie :** nom de la stratégie associée au document.

**Tous les documents :** tous les documents protégés par les administrateurs et les utilisateurs. L’utilisation de cette option risque de renvoyer une liste de documents particulièrement longue.

1. Dans la page Document Security, cliquez sur Documents.
1. Dans la liste Rechercher, sélectionnez les critères de recherche requis.

   Vous pouvez spécifier les critères tels que l’ID du document, le nom du document, le nom de l’éditeur, l’ID de la stratégie, le nom de la stratégie ou tous les documents.

   Si vous spécifiez le nom de l’éditeur, cliquez sur l’icône représentant un carnet d’adresses et spécifiez le domaine dans lequel vous souhaitez rechercher l’utilisateur, puis cliquez sur le bouton OK pour revenir à la page Documents.

1. (Facultatif) Dans la liste Date, sélectionnez une option de plage de dates. Si vous sélectionnez Dates personnalisées, saisissez la date au format aaaa/mm/jj dans les zones prévues à cet effet. Vous pouvez également spécifier la plage de dates à l’aide du Sélecteur de date en procédant comme suit :

   * Cliquez sur le calendrier pour ouvrir le Sélecteur de date.
   * Utilisez les flèches pour sélectionner l’année et le mois.
   * Cliquez sur un jour du mois dans le calendrier.
   * Cliquez sur OK pour fermer le Sélecteur de date.

1. Cliquez sur Rechercher.

## Tri de la liste des documents  {#sort-the-document-list}

Vous pouvez trier la liste des documents par en-tête de colonne. Le triangle situé à côté de l’en-tête de colonne indique la colonne triée. Lorsque le triangle est dirigé vers le haut, l’ordre de tri est croissant et lorsqu’il est dirigé vers le bas, l’ordre de tri est décroissant.

1. Dans la page Document Security, cliquez sur Documents.
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur l’en-tête de colonne.

## Ajout d’une page de garde aux documents protégés par une stratégie  {#add-cover-page-to-policy-protected-documents}

Dans la plupart des visionneuses PDF autres qu’Adobe, si vous ouvrez un document protégé par Document Security, la première page est vide ou l’application s’interrompt sans ouvrir le document.

Vous pouvez utiliser la prise en charge Page 0 (Wrapper Document) pour permettre aux visionneuses PDF autres qu’Adobe d’ouvrir un document protégé et d’afficher la page de garde du document.

>[!NOTE]
>
>Lorsque vous consultez un document de ce type (contenant une page 0) dans Adobe Reader/Acrobat ou Mobile Reader, le document protégé s’ouvre par défaut.

**Pour ajouter une page de garde à un document protégé par une stratégie**

Utilisez les processus suivants dans Workbench :

**Document Protect avec page de couverture :** sécurise un document PDF avec la stratégie spécifiée et ajoute une page de garde au document.

**Extraire le Document protégé :** extrait le document PDF protégé par une stratégie du document PDF avec la page de garde.

Utilisez les API de Document Security suivants :

**protectDocumentWithCoverPage :** sécurise un PDF donné avec la stratégie spécifiée et renvoie un document avec une page de garde et le document protégé en tant que pièce jointe 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extraieProtectedDocument :** Extrait le document protégé qui est une pièce jointe dans le document avec la page de garde. Le document avec la page de garde peut être créé à l’aide de la méthode protectDocumentWithCoverPage. `//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`