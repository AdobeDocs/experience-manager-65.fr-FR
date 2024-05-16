---
title: Présentation des services de document AEM
description: Les services de document AEM sont un ensemble de services OSGi permettant de créer, d’assembler et de sécuriser des documents PDF.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1413'
ht-degree: 100%

---

# Présentation des services de document AEM{#overview-of-aem-document-services}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=fr) |
| AEM 6.5 | Cet article |


Les Services de document AEM sont un ensemble de services OSGi permettant de créer, d’assembler et de sécuriser des documents PDF. Les services suivants sont disponibles dans les Services de document :

## Service Output {#output-service}

Le service Output vous permet de créer des documents dans différents formats, y compris PDF et les formats d’imprimantes laser et d’imprimantes d’étiquettes. Les formats d’imprimantes laser sont les suivants : PostScript et PCL (Printer Control Language). La liste suivante spécifie les formats d’imprimantes d’étiquettes :

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Un document peut être envoyé vers une imprimante réseau, une imprimante locale ou un fichier sur le système de fichiers. Le service Output fusionne les données du formulaire XML avec une conception de formulaire pour générer un document. Il peut générer un document sans fusionner les données du formulaire XML dans le document. Toutefois, le processus principal fusionne les données dans le document.

>[!NOTE]
>
>la création d’une conception de formulaire se fait généralement à l’aide de Designer. Pour plus d’informations sur la création de conceptions de formulaire pour le service Ouput, consultez l’aide de Designer.

Lorsque vous utilisez le service Output pour fusionner des données XML avec une conception de formulaire, il en résulte la création d’un document PDF non interactif. Dans ce type de document, les utilisateurs n’ont pas la possibilité de saisir des données dans les champs. En revanche, vous pouvez utiliser le service Forms pour créer un formulaire PDF interactif permettant aux utilisateurs et aux utilisatrices de saisir des données dans ses champs.

Les quatre opérations du service Output suivantes peuvent être utilisées :

* **generatePDFOuput** : fusionne une conception de formulaire avec des données pour générer un document PDF.
* **generatePrintedOutput** : fusionne une conception de formulaire avec des données pour générer un document à envoyer à une imprimante laser ou une imprimante d’étiquettes réseau.

* **generatePDFOutputBatch** : fusionne en un seul appel plusieurs modèles avec plusieurs enregistrements de données pour générer un lot de fichiers PDF. Il existe également la possibilité de générer un seul PDF en combinant tous les PDF.
* **generatePrintedOutputBatch** : fusionne en un seul appel plusieurs modèles avec plusieurs enregistrements de données pour générer un lot de documents d’impression (PS, PCL, ZPL, DPL, IPL, TPCL). Il existe également une option pour générer un document d’impression unique.

## Incohérence affectant le service assembleur {#assembler-service}

Le service Assembler vous permet de combiner, d’organiser et d’étendre vos documents aux formats PDF et XDP. Grâce à lui, vous pouvez également obtenir des informations sur les documents PDF. Chacun des travaux envoyés au service Assembler inclut un document DDX (Document Description XML), ainsi qu’un ensemble de documents source et de ressources externes (chaînes et graphiques). Le document DDX explique comment utiliser les documents sources pour générer un ensemble de documents cible.

Outre les capacités mentionnées ci-dessus, le service Assembler permet d’effectuer les actions suivantes :

* Conversion de documents PDF au format PDF/A standard.
* Transformation des formulaires PDF, formulaires XML (créés dans Designer) et formulaires PDF créés dans Acrobat aux formats PDF/A-1b, PDF/A-2b et PDFA/A-3b.
* Conversion des documents PDF signés ou non (Digital Signatures requis).
* Validation de la conformité d’un fichier PDF/A et conversion de ce fichier le cas échéant.

### À propos de DDX {#about-ddx}

Le service Assembler utilise un langage de type XML, appelé Document Description XML (DDX), avec lequel vous pouvez décrire la sortie que vous souhaitez obtenir. DDX est un langage de marquage déclaratif dont les éléments représentent des blocs de création de documents. Ces blocs de création comportent des documents PDF et XDP, des fragments de formulaire XDP, ainsi que d’autres éléments tels que des commentaires, des signets et du texte avec style.

Le document DDX peut spécifier les documents cibles avec ces caractéristiques :

* Un document PDF assemblé à partir de documents PDF multiples.
* Divers documents PDF issus d’un document PDF unique.
* Un portfolio PDF incluant une interface utilisateur autonome et plusieurs documents, PDF et non PDF.
* Un document XDP assemblé à partir de plusieurs documents XDP.
* Un document XDP contenant des fragments XML insérés de manière dynamique dans un document XDP.
* Un document PDF contenant un document XDP.
* Des fichiers XML fournissant des informations sur les caractéristiques d’un document PDF. Les caractéristiques présentées incluent du texte, des commentaires, des données de formulaire, des pièces jointes, des fichiers utilisés dans des portfolios PDF, des signets et des propriétés PDF. Les propriétés PDF incluent les propriétés du formulaire, la rotation des pages et le créateur ou la créatrice du document.

Vous pouvez utiliser DDX pour étendre les documents PDF dans le cadre de l’assemblage et du désassemblage de documents. Vous pouvez spécifier n’importe quelle combinaison des effets suivants :

* ajout ou suppression de filigranes ou d’arrière-plans sur les pages sélectionnées ; 
* insertion ou suppression d’en-têtes et de pieds de page sur les pages sélectionnées ; 
* suppression de la structure et des capacités de navigation dans un package PDF ou un portfolio PDF ; Le résultat est un document PDF unique.
* renumérotation des intitulés de page ; Les étiquettes de page servent généralement à numéroter des pages.
* importation de métadonnées à partir d’un autre document source ;
* ajout ou suppression de pièces jointes, de signets, de liens, de commentaires et de tout élément JavaScript ;
* définition des caractéristiques d’affichage initiales et optimisation de l’affichage sur le Web ;
* définition de droits pour les PDF chiffrés ;
* rotation de pages ou rotation et déplacement du contenu des pages ;
* modification de la taille des pages sélectionnées ;
* fusion des données avec un PDF basé sur XFA.

Vous pouvez utiliser une simple mise en correspondance des entrées pour indiquer l’emplacement des documents source et cible. Vous pouvez également utiliser les types d’URL de données externes suivants :

* File
* FTP
* HTTP/HTTPS

## Service Doc Assurance {#doc-assurance-service}

Le service Doc Assurance vous permet de chiffrer et de déchiffrer des documents, d’ajouter des droits d’utilisation aux fonctionnalités d’Adobe Reader ou encore d’ajouter des signatures numériques à vos documents. Vos utilisateurs et utilisatrices peuvent facilement interagir avec les formulaires et documents PDF, tandis que votre organisation améliore la sécurité, l’archivage et la conformité.

Le service Doc Assurance se compose en fait de trois services : Signature, Encryption et Reader Extensions.

### Service Signature {#signature-service}

Le service Signature vous permet d’utiliser des documents et des signatures numériques sur le serveur AEM. Par exemple, le service Signature est généralement utilisé dans les situations suivantes :

* Le serveur AEM certifie un formulaire avant que ce dernier ne soit envoyé à un utilisateur ou une utilisatrice et ouvert avec Acrobat ou Adobe Reader.
* Le serveur AEM valide la signature apposée sur un formulaire via Acrobat ou Adobe Reader.
* Le serveur AEM signe un formulaire au nom d’un notaire.

Le service Signature accède aux certificats et aux informations d’identification stockées dans le Trust Store.

### Service Encryption {#encryption-service}

Le service Encryption permet de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Vous pouvez chiffrer l’intégralité d’un document PDF (contenu, métadonnées et pièces jointes), tous les éléments autres que ses métadonnées ou uniquement les pièces jointes. Un utilisateur autorisé peut déchiffrer le document pour pouvoir accéder à son contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Acrobat. Si un document PDF est chiffré avec un certificat, l’utilisateur ou l’utilisatrice doit le déchiffrer avec une clé privée (certificat). La clé privée utilisée pour déchiffrer le document PDF doit correspondre à la clé publique utilisée pour le chiffrer.

### Service Reader Extension {#reader-extension-service}

Le service Reader Extensions permet à votre entreprise de partager facilement des documents PDF interactifs en étendant la fonctionnalité d’Adobe Reader avec des droits d’utilisation supplémentaires. Le service Reader Extensions fonctionne avec Adobe Reader 7.0 et versions ultérieures. Ce service ajoute des droits d’utilisation dans un document PDF. Cela active des fonctionnalités généralement indisponibles à l’ouverture d’un document PDF dans Adobe Reader, comme l’ajout de commentaires dans un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation.

Lorsque les droits d’utilisation appropriés sont ajoutés aux documents PDF, les destinataires peuvent effectuer les activités suivantes depuis Adobe Reader :

* Remplir des documents et des formulaires PDF en ligne ou hors ligne permettant aux destinataires d’enregistrer des copies localement pour leurs dossiers tout en conservant intactes les informations ajoutées.
* Enregistrer les documents PDF sur un disque dur local pour conserver le document original ainsi que tout commentaire, donnée ou pièce jointe supplémentaire.
* Joindre des fichiers et des éléments multimédias à des documents PDF.
* Signer, certifier et authentifier des documents PDF en appliquant des signatures numériques à l’aide des technologies d’infrastructure à clé publique (PKI) standard du secteur.
* Soumettre électroniquement des documents PDF complétés ou annotés.
* Utiliser des documents et des formulaires PDF comme interface front-end de développement intuitive pour les bases de données internes et les services web.
* Partage de documents PDF pour que les réviseurs puissent ajouter des commentaires à l’aide d’outils intuitifs d’insertion de commentaires et d’annotations, tels que notes autocollantes, tampons, texte surligné et texte barré. Les mêmes fonctions sont disponibles dans Acrobat.
* Le décodage de formulaires à code à barres est pris en charge.

Ces fonctions d’utilisateur spéciales sont automatiquement activées lorsqu’un utilisateur ouvre un document PDF défini avec les droits d’utilisation appropriés dans Adobe Reader. Dès que l’utilisateur a fini de travailler sur un document défini avec ces droits d’utilisation, ces fonctions sont de nouveau désactivées dans Adobe Reader, Elles restent désactivées jusqu’à ce que l’utilisateur ou l’utilisatrice reçoive un autre document PDF dont les droits sont activés.

Le service DocAssurance prêt à l’emploi n’est pas disponible. Pour configurer le service DocAssurance, voir [Installer et configurer les services Document](../../forms/using/install-configure-document-services.md).

## Service SendToPrinter {#send-to-printer-service}

Le service Send To Printer fournit une API pour envoyer des documents à imprimer vers l’imprimante spécifiée.
