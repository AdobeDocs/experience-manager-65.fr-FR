---
title: Présentation des services de document AEM
seo-title: Overview of AEM Document Services
description: Les services de document AEM sont un ensemble de services OSGi permettant de créer, d’assembler et de sécuriser des documents PDF.
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 59%

---

# Présentation des services de document AEM{#overview-of-aem-document-services}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) |
| AEM 6.5 | Cet article |


Les Services de document AEM sont un ensemble de services OSGi permettant de créer, d’assembler et de sécuriser des documents PDF. Les services suivants sont disponibles dans les Services de document :

## Service Output {#output-service}

Le service Output vous permet de créer des documents dans différents formats, y compris PDF et les formats d’imprimantes laser et d’imprimantes d’étiquettes. Les formats d’imprimantes laser sont les suivants : PostScript et PCL (Printer Control Language). La liste suivante indique les formats d’imprimantes d’étiquettes :

* Zebra (ZPL)
* IPL (Intermec)
* Datamax (DPL)
* TecToshiba (TPCL)

Un document peut être envoyé à une imprimante réseau, à une imprimante locale ou à un fichier du système de fichiers. Le service Output fusionne les données du formulaire XML avec une conception de formulaire pour générer un document. Il peut générer un document sans fusionner les données du formulaire XML dans le document. Toutefois, le processus principal fusionne les données dans le document.

>[!NOTE]
>
>la création d’une conception de formulaire se fait généralement à l’aide de Designer. Pour plus d’informations sur la création de conceptions de formulaire pour le service Output, voir l’aide de Designer.

Lorsque vous utilisez le service Output pour fusionner des données XML avec une conception de formulaire, il en résulte la création d’un document PDF non interactif. Dans ce type de document, les utilisateurs n’ont pas la possibilité de saisir des données dans les champs. En revanche, vous pouvez utiliser le service Forms pour créer un formulaire de PDF interactif qui permet aux utilisateurs de saisir des données dans ses champs.

Les quatre opérations suivantes du service Output sont disponibles :

* **generatePDFOuput**: Fusionne une conception de formulaire avec des données pour générer un document de PDF
* **generatePrintedOutput** : fusionne une conception de formulaire avec des données pour générer un document à envoyer à une imprimante laser ou une imprimante d’étiquettes réseau.

* **generatePDFOutputBatch**: Fusionne plusieurs modèles avec plusieurs enregistrements de données en un seul appel pour générer un lot de fichiers de PDF. Il existe également une option pour générer un PDF unique en combinant tous les PDF.
* **generatePrintedOutputBatch** : fusionne en un seul appel plusieurs modèles avec plusieurs enregistrements de données pour générer un lot de documents d’impression (PS, PCL, ZPL, DPL, IPL, TPCL). Il existe également une option pour générer un document d’impression unique.

## Incohérence affectant le service assembleur {#assembler-service}

Le service Assembler vous permet de combiner, d’organiser et d’étendre vos documents aux formats PDF et XDP. Grâce à lui, vous pouvez également obtenir des informations sur les documents PDF. Chacun des travaux envoyés au service Assembler inclut un document DDX (Document Description XML), ainsi qu’un ensemble de documents source et de ressources externes (chaînes et graphiques). Le document DDX fournit des instructions sur l’utilisation des documents source pour produire un ensemble de documents cible.

Outre les fonctionnalités mentionnées ci-dessus, le service Assembler :

* Convertit les documents de PDF en PDF/A standard.
* Transformation des formulaires PDF, formulaires XML (créés dans Designer) et formulaires PDF créés dans Acrobat aux formats PDF/A-1b, PDF/A-2b et PDFA/A-3b.
* Conversion des documents PDF signés ou non (Digital Signatures requis).
* Valide la conformité d’un fichier PDF/A et le convertit si nécessaire.

### A propos de DDX {#about-ddx}

Le service Assembler utilise un langage de type XML, appelé Document Description XML (DDX), avec lequel vous pouvez décrire la sortie que vous souhaitez obtenir. DDX est un langage de marquage déclaratif dont les éléments représentent des blocs de création de documents. Ces blocs de création comprennent des documents PDF, des documents XDP, des fragments de formulaire XDP et d’autres éléments tels que des commentaires, des signets et du texte stylisé.

Un document DDX peut spécifier des documents cible présentant les caractéristiques suivantes :

* Un document PDF assemblé à partir de documents PDF multiples.
* Divers documents PDF issus d’un document PDF unique.
* Un portfolio PDF incluant une interface utilisateur autonome et plusieurs documents, PDF et non PDF.
* Un document XDP assemblé à partir de plusieurs documents XDP.
* Un document XDP contenant des fragments XML insérés de manière dynamique dans un document XDP.
* Un document PDF contenant un document XDP.
* Des fichiers XML fournissant des informations sur les caractéristiques d’un document PDF. Les caractéristiques présentées incluent du texte, des commentaires, des données de formulaire, des pièces jointes, des fichiers utilisés dans des portfolios PDF, des signets et des propriétés PDF. Les propriétés de PDF incluent les propriétés de formulaire, la rotation de page et l’auteur du document.

Vous pouvez utiliser DDX pour étendre les documents PDF dans le cadre de l’assemblage et du désassemblage de documents. Vous pouvez définir n’importe quelle combinaison des effets suivants :

* ajout ou suppression de filigranes ou d’arrière-plans sur les pages sélectionnées ; 
* insertion ou suppression d’en-têtes et de pieds de page sur les pages sélectionnées ; 
* suppression de la structure et des capacités de navigation dans un package PDF ou un portfolio PDF ; Le résultat est un fichier de PDF unique.
* renumérotation des intitulés de page ; Les libellés de page sont généralement utilisés pour la numérotation des pages.
* importation de métadonnées à partir d’un autre document source ;
* ajout ou suppression de pièces jointes, de signets, de liens, de commentaires et de tout élément JavaScript ;
* définition des caractéristiques d’affichage initiales et optimisation de l’affichage sur le Web ;
* définition de droits pour les PDF chiffrés ;
* rotation de pages ou rotation et déplacement du contenu des pages ;
* modification de la taille des pages sélectionnées ;
* fusion des données avec un PDF basé sur XFA.

Vous pouvez utiliser une simple mise en correspondance des entrées pour indiquer l’emplacement des documents source et cible. Vous pouvez également utiliser les types d’URL de données externes suivants :

* File
* FTP
* HTTP/HTTPS

## Service Doc Assurance {#doc-assurance-service}

Le service Doc Assurance vous permet de chiffrer et de déchiffrer des documents, d’étendre les fonctionnalités d’Adobe Reader avec des droits d’utilisation supplémentaires et d’ajouter des signatures numériques à vos documents. Vos utilisateurs peuvent facilement interagir avec des PDF forms et des documents, tandis que votre entreprise améliore la sécurité, l’archivage et la conformité.

Le service Doc Assurance se compose en fait de trois services : Signature, Encryption et Reader Extensions.

### Service Signature {#signature-service}

Le service Signature vous permet d’utiliser des signatures et des documents numériques sur le serveur AEM. Par exemple, le service Signature est généralement utilisé dans les situations suivantes :

* Le serveur AEM certifie un formulaire avant qu’il ne soit envoyé à un utilisateur pour qu’il s’ouvre à l’aide d’Acrobat ou d’Adobe Reader.
* Le serveur d’AEM valide la signature qui a été ajoutée à un formulaire à l’aide d’Acrobat ou d’Adobe Reader.
* Le serveur AEM signe un formulaire au nom d&#39;un notaire.

Le service Signature accède aux certificats et aux informations d’identification stockées dans le trust store.

### Service Encryption {#encryption-service}

Le service Encryption permet de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Vous pouvez chiffrer l’intégralité d’un document PDF (contenu, métadonnées et pièces jointes), tous les éléments autres que ses métadonnées ou uniquement les pièces jointes. Un utilisateur autorisé peut déchiffrer le document pour pouvoir accéder à son contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Acrobat. Si un document de PDF est chiffré avec un certificat, l’utilisateur doit déchiffrer le document de PDF avec une clé privée (certificat). La clé privée utilisée pour déchiffrer le document du PDF doit correspondre à la clé publique utilisée pour le chiffrer.

### Service d’extension de Reader {#reader-extension-service}

Le service Reader Extensions permet à votre entreprise de partager facilement des documents PDF interactifs en étendant la fonctionnalité d’Adobe Reader avec des droits d’utilisation supplémentaires. Le service Reader Extensions fonctionne avec Adobe Reader 7.0 et versions ultérieures. Ce service ajoute des droits d’utilisation dans un document PDF. Cela active des fonctionnalités généralement indisponibles à l’ouverture d’un document PDF dans Adobe Reader, comme l’ajout de commentaires dans un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation.

Lorsque les droits d’utilisation appropriés sont ajoutés aux documents PDF, les destinataires peuvent effectuer les activités suivantes depuis Adobe Reader :

* Remplissez des documents et des formulaires PDF en ligne ou hors ligne, ce qui permet aux destinataires d’enregistrer des copies localement pour leurs enregistrements et de conserver intactes les informations ajoutées.
* Enregistrement de documents PDF sur un disque dur local afin de conserver le document d’origine ainsi que tous les commentaires, données ou pièces jointes supplémentaires
* Joindre des fichiers et des clips multimédia à des documents PDF
* Signature, certification et authentification de documents PDF par l’application de signatures numériques à l’aide des technologies PKI (Public Key Infrastructure, infrastructure à clé publique) standard
* Envoi électronique de documents PDF complétés ou annotés
* Utiliser des documents et des formulaires PDF comme interface de développement intuitive pour les bases de données internes et les services Web
* Partage de documents PDF pour que les réviseurs puissent ajouter des commentaires à l’aide d’outils intuitifs d’insertion de commentaires et d’annotations, tels que notes autocollantes, tampons, texte surligné et texte barré. Les mêmes fonctions sont disponibles dans Acrobat.
* Prise en charge du décodage des formulaires à code à barres.

Ces fonctions d’utilisateur spéciales sont automatiquement activées lorsqu’un utilisateur ouvre un document PDF défini avec les droits d’utilisation appropriés dans Adobe Reader. Dès que l’utilisateur a fini de travailler sur un document défini avec ces droits d’utilisation, ces fonctions sont de nouveau désactivées dans Adobe Reader, Ils restent désactivés jusqu’à ce que l’utilisateur reçoive un autre document de PDF dont les droits sont activés.

Le service DocAssurance n’est pas disponible en standard. Pour configurer le service DocAssurance, voir [Installer et configurer les services Document](../../forms/using/install-configure-document-services.md).

## Service SendToPrinter {#send-to-printer-service}

Le service Send To Printer fournit une API pour envoyer des documents à imprimer vers l’imprimante spécifiée.
