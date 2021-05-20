---
title: Configuration des paramètres du service
seo-title: Configuration des paramètres du service
description: Découvrez comment configurer les paramètres du service.
seo-description: Découvrez comment configurer les paramètres du service.
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '10710'
ht-degree: 63%

---

# Configuration des paramètres du service {#configure-service-settings}

Vous pouvez utiliser la page Gestion des services pour configurer les paramètres de chacun des services qui font partie d’AEM forms. Les paramètres disponibles varient selon le service configuré.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Arrêtez le service avant de le modifier (voir la section [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
1. Cliquez sur le nom du service que vous souhaitez configurer.
1. Si le service dispose d’un onglet Configuration, utilisez-le pour modifier les paramètres du service. Vous trouverez la liste des liens ci-dessous pour plus d’informations.

   >[!NOTE]
   >
   >certains services répertoriés dans la page Gestion des services ne possèdent pas d’onglet Configuration. L’onglet Configuration des processus créés s’affiche uniquement lorsque vous ajoutez un paramètre de configuration à ces processus dans Workbench (voir Paramètres de configuration dans [l’Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Cliquez sur l’onglet Sécurité et définissez les paramètres de protection du service (voir [Modification des paramètres de sécurité d’un service](configure-service-settings.md#modifying-security-settings-for-a-service)).
1. Si le service dispose d’un onglet Points de fin, utilisez-le pour modifier les paramètres des points de fin (voir [Gestion des points de fin](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md)).
1. Cliquez sur l’onglet Mise en pool et définissez les paramètres de la mise en pool (voir [Configuration du pool d’un service](configure-service-settings.md#configuring-pooling-for-a-service)).
1. Cliquez sur Enregistrer pour enregistrer vos modifications ou sur Annuler pour les ignorer.
1. Cochez la case en regard du nom du service et cliquez sur Démarrer pour redémarrer le service.

## Paramètres du service Audit Workflow {#audit-workflow-service-settings}

Workbench permet d’enregistrer des instances de processus au moment de l’exécution, puis de les relire pour observer le comportement du processus (Voir [l’Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)). Pour préserver l’espace disponible sur le système de fichiers du serveur Forms, vous pouvez limiter la quantité de données d’enregistrement de processus conservées. Vous pouvez configurer les propriétés suivantes du service Audit Workflow Service (`AuditWorkflowService`) :

**maxNumberOfRecordingInstances :** nombre maximal d’enregistrements stockés. Lorsque le nombre maximum est atteint, l’enregistrement le plus ancien est supprimé du système de fichiers lors de la création d’un nouvel enregistrement. Cette propriété est utile si vous avez tendance à créer un grand nombre d’enregistrements et souhaitez supprimer les anciens de manière automatique. La valeur par défaut est 50.

**MaxNumberOfRecordingEntries :** nombre maximal d’entrées de données pouvant être stockées pour chaque enregistrement. Les entrées de données sont des informations se rapportant aux opérations du processus. Plusieurs entrées sont conservées pour chaque exécution d’une opération, par exemple si l’opération a démarré, si elle a été menée à bien et si le chemin menant à l’opération est complet. Cette propriété est utile lorsque des processus peuvent inclure un grand nombre d’exécutions d’opérations, par exemple en cas de boucle sans fin. La valeur par défaut est 50.

## Paramètres du service Barcoded Forms  {#barcoded-forms-service-settings}

Le service Barcoded Forms `(BarcodedFormsService)` extrait les données de code-barres des images numérisées. Ce service reçoit un formulaire à code-barres (TIFF ou PDF) en entrée, puis extrait la représentation machine des données codées par le code-barres.

Les paramètres ci-dessous sont disponibles pour le service Barcoded Forms.

**Lecture à gauche :** lorsque cette option est sélectionnée, les images de code à barres sont numérisées horizontalement, de droite à gauche.

**Lecture à droite :** lorsque cette option est sélectionnée, les images de code à barres sont numérisées horizontalement de gauche à droite.

**Lecture vers le haut :** lorsque cette option est sélectionnée, les images de code à barres sont numérisées verticalement du bas vers le haut.

**Lecture vers le bas :** lorsque cette option est sélectionnée, les images de code à barres sont numérisées verticalement du haut vers le bas.

>[!NOTE]
>
>par défaut, tous les paramètres sont sélectionnés. Désélectionnez un paramètre uniquement si vous êtes certain qu’aucun code-barres n’apparaît sous cette forme dans vos formulaires.

**Chemin d’accès au fichier de base :**  chemin d’accès au fichier relatif auquel les paramètres d’entrée et de sortie du lot pour les opérations Run XML File Job et Run Flat File Job sont résolus. Dans les configurations en grappe, le chemin d’accès au fichier de base doit être un emplacement de système de fichiers partagé auquel tous les noeuds de la grappe ont accès en lecture/écriture.

**Nom de la source de données :** nom de la source de données utilisé pour conserver les informations d’état et d’historique concernant les tâches de traitement par lots. La source de données spécifiée doit prendre en charge les transactions globales (XA).

## Paramètres (obsolètes) du service Central Migration Bridge {#central-migration-bridge-service-settings}

Le service Central migration Bridge (`CentralMigrationBridge`) appelle un sous-ensemble de fonctionnalités Adobe Central Pro Output Server (Central), qui comprend les commandes JFMERGE, JFTRANS et XMLIMPORT. Les opérations du service Central Migration Bridge vous permettent de réutiliser les actifs Central suivants dans AEM Forms :

* conception de modèle (&amp;ast;.ifd)
* Modèles de sortie (&amp;ast;.mdf)
* Fichiers de données (&amp;fichiers ast;.dat)
* Fichiers de préface (&amp;ast;.pre)
* Fichiers de définition de données (&amp;ast;.tdf)

Le paramètre ci-dessous est disponible pour le service Central Migration Bridge.

**Répertoire d’installation de Central :** répertoire dans lequel Adobe Central 5.7 est installé.

## Paramètres du service Content Repository Connector for EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

Le service Content Repository Connector for EMC Documentum (`EMCDocumentumContentRepositoryConnector`) vous permet de créer des processus qui interagissent avec le contenu stocké dans un référentiel Documentum.

Le paramètre suivant est disponible pour le service Content Repository Connector for EMC Documentum.

**Asset Link Object Default Path :** la partie par défaut du chemin dans le référentiel Documentum pour stocker l’objet Asset Link. Le chemin d’accès se compose du chemin par défaut et de l’emplacement du modèle de formulaire dans le référentiel AEM forms.

Par exemple, si le chemin par défaut est défini sur `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` et que le modèle de formulaire est stocké dans un dossier `/Docbase/forms/`, l’objet Asset Link est stocké à l’emplacement suivant :

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

La valeur par défaut de ce paramètre est `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Paramètres du service Content Repository Connector for IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

Le service Content Repository Connector for IBM FileNet vous permet de créer des processus qui interagissent avec le contenu stocké dans un référentiel IBM FileNet.

Le paramètre ci-dessous est disponible pour le service Content Repository Connector for IBM FileNet.

**Asset Link Object Default Path :** la partie par défaut du chemin dans le référentiel IBM FileNet pour le stockage de l’objet Asset Link. Le chemin d’accès se compose du chemin par défaut et de l’emplacement du modèle de formulaire dans le référentiel AEM forms.

Par exemple, si le chemin par défaut est défini sur `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` et que le modèle de formulaire est stocké dans un dossier `/Docbase/forms/`, l’objet Asset Link est stocké à l’emplacement suivant :

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

La valeur par défaut de ce paramètre est `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Paramètres du service Convert PDF {#convert-pdf-service-settings}

Le service Convert PDF (`ConvertPdfService`) convertit des documents PDF en PostScript® et en de nombreux formats d’image (JPEG, JPEG 2000, PNG et TIFF). La conversion d’un document PDF en PostScript est utile pour les impressions sans assistance reposant sur un serveur exécutées sur n’importe quelle imprimante PostScript. La conversion d’un document PDF en fichier TIFF comportant plusieurs pages est pratique lors de l’archivage de documents dans des systèmes de gestion de contenu qui ne prennent pas en charge les documents PDF.

Les paramètres ci-dessous sont disponibles pour le service Convert PDF.

**Type de transaction :** indique comment un contexte de transaction doit être propagé à une opération.

**Obligatoire :**  prend en charge un contexte de transaction s’il en existe un ; dans le cas contraire, un nouveau contexte de transaction est créé. Il s’agit de la valeur par défaut.

**Nécessite :** crée toujours un contexte de transaction. Si un contexte de transaction actif existe, il est suspendu.

**Transaction Time Out (in sec) :** nombre de secondes pendant lesquelles le fournisseur de transactions sous-jacent doit attendre avant de restaurer une transaction qui termine cette opération. Cette valeur sera ignorée si un contexte de transaction existant est propagé. La valeur par défaut est 180.

**Résolution du seuil pour le lissage (en ppp) :**  résolution de l’image sous laquelle le lissage (ou anti-crénelage) est appliqué au texte, aux dessins au trait et aux images, si vous avez sélectionné les options &quot;Appliquer le lissage à&quot; pour ces éléments.

**Appliquer le lissage au texte :** contrôle le lissage du texte. Pour désactiver le lissage du texte et rendre le texte plus net et plus facile à lire à l’aide d’un agrandisseur d’écran, désélectionnez cette case.

**Apply smoothing to LineArt :** applique le lissage pour supprimer les angles brusques des lignes.

**Apply smoothing to images :** applique le lissage pour minimiser les modifications brusques des images.

## Paramètres du service Distiller {#distiller-service-settings}

Le service Distiller (`DistillerService`) convertit les fichiers PostScript, Encapsulated PostScript (EPS) et PRN en fichiers PDF sur un réseau.

Les paramètres ci-dessous sont disponibles pour le service Distiller.

**Paramètres Adobe PDF :**  les paramètres préconfigurés suivants sont appliqués au PDF généré :

* High quality print (Haute qualité d’impression)
* Oversized pages (Pages surdimensionnées)
* PDFA1b 2005 CMJN
* PDFA1b 2005 RVB
* PDFX1a 2001
* PDFX3 2002
* Press quality (Qualité de presse)
* Smallest file size (Taille de fichier réduite)
* Standard

Vous pouvez créer des paramètres dans l’interface utilisateur de PDF Generator.

**Paramètres de protection :** paramètres de protection préconfigurés appliqués aux documents PDF générés. La valeur par défaut est No Security. Vous devez créer des paramètres de protection dans l’interface utilisateur graphique de LiveCycle PDF Generator, puis saisir le paramètre voulu dans ce champ.

**Taille du pool :** taille initiale du pool. Lors du déploiement du service Distiller, cette valeur permet de déterminer le nombre d’instances d’implémentation du service à créer et à affecter au pool libre en attente de demandes d’appel. Le conteneur du service peut alors répondre immédiatement aux demandes d’appel sans initialisation préalable d’une instance de service.

## Paramètres du service Document Management  {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Pour savoir comment configurer Content Services (obsolète), consultez [Administration de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

Le service Document Management (`DocumentManagementService`) permet aux processus d’utiliser la fonctionnalité de gestion de contenu fournie par Content Services (obsolète). Les opérations de Document Management fournissent des tâches de bases requises pour gérer les espaces et le contenu dans le système de gestion de contenu. Voici quelques exemple de tâches de ce type : copier, supprimer, déplacer, récupérer et stocker du contenu, créer des espaces et des associations, ainsi qu’obtenir et définir des attributs de contenu.

Les paramètres ci-dessous sont disponibles pour le service Document Management.

**Schéma de magasin :**  schéma du magasin dans lequel se trouve le contenu. La valeur par défaut est workspace.

**Port HTTP :** port utilisé pour accéder à Content Services (obsolète). La valeur par défaut est 8080.

## Paramètres du service Email  {#email-service-settings}

Le service Email est généralement utilisé pour diffuser du contenu ou fournir des informations d’état dans le cadre d’un processus automatisé. `EmailService` permet aux processus de recevoir des courriers électroniques d’un serveur POP3 ou IMAP et d’en envoyer à un serveur SMTP.

Par exemple, un processus utilise le service Email pour envoyer un courrier électronique pourvu d’un formulaire PDF joint. Le service Email se connecte à un serveur SMTP pour envoyer le courrier électronique avec la pièce jointe. Le formulaire au format PDF est conçu pour permettre au destinataire d’appuyer sur le bouton d’envoi lorsqu’il l’a rempli. Le formulaire est alors renvoyé sous forme de pièce jointe au serveur de messagerie indiqué. Le service Email récupère le courrier électronique renvoyé, puis stocke le formulaire complété dans une variable de formulaire des données de processus.

Les paramètres ci-dessous sont disponibles pour le service Email.

**Hôte SMTP :** adresse IP ou URL du serveur SMTP à utiliser pour l’envoi des emails.

**Numéro de port SMTP :** port utilisé pour se connecter au serveur SMTP.

**Authentification SMTP :** sélectionnez cette option si l’authentification de l’utilisateur est requise pour se connecter au serveur SMTP.

**SMTP User :** nom d’utilisateur du compte utilisateur à utiliser pour se connecter au serveur SMTP.

**Mot de passe SMTP :** mot de passe associé au compte utilisateur SMTP.

**SMTP Transport Security :** protocole de sécurité à utiliser pour la connexion au serveur SMTP :

* Sélectionnez None si aucun protocole n’est utilisé (les données sont envoyées en clair).
* Sélectionnez SSL si le protocole Secure Sockets Layer est utilisé.
* Sélectionnez TLS si le protocole Transport Layer Security est utilisé.

**Hôte POP3/IMAP :** adresse IP ou URL du serveur POP3 ou IMAP à utiliser pour l’envoi des emails.

**Nom d’utilisateur POP3/IMAP :**  nom d’utilisateur du compte utilisateur à utiliser pour se connecter au serveur POP3 ou IMAP.

**Mot de passe POP3/IMAP :**  mot de passe associé au compte utilisateur POP3 ou IMAP.

**POP3/IMAP Port Number :**  port utilisé pour se connecter au serveur POP3 ou IMAP.

**POP3/IMAP :** protocole à utiliser pour envoyer et recevoir des emails.

**Receive Transport Security :** protocole de sécurité à utiliser pour la connexion au serveur SMTP :

* Sélectionnez None si aucun protocole n’est utilisé (les données sont envoyées en clair).
* Sélectionnez SSL si le protocole Secure Sockets Layer est utilisé.
* Sélectionnez TLS si le protocole Transport Layer Security est utilisé.

## Paramètres du service Encryption {#encryption-service-settings}

Le service Encryption (`EncryptionService`) vous donne la possibilité de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Un utilisateur autorisé peut déchiffrer le document pour accéder à son contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Adobe Acrobat. De même, si un document PDF est chiffré avec un certificat, l’utilisateur doit déchiffrer le document PDF avec la clé publique correspondant au certificat (clé privée) qui a été utilisé pour chiffrer le document PDF.

Les paramètres ci-dessous sont disponibles pour le service Encryption.

**Serveur LDAP par défaut auquel se connecter :** nom d’hôte du serveur LDAP utilisé pour récupérer les certificats pour le chiffrement des documents.

**Port LDAP par défaut auquel se connecter :** numéro de port du serveur LDAP.

**Nom d’utilisateur LDAP par défaut :** si le serveur LDAP requiert une authentification, indiquez le nom d’utilisateur à utiliser pour la connexion au serveur LDAP.

**Mot de passe LDAP par défaut :** si le serveur LDAP requiert une authentification, indiquez le mot de passe correspondant au nom d’utilisateur à utiliser pour la connexion au serveur LDAP.

>[!NOTE]
>
>utilisez l’authentification simple (nom d’utilisateur et mot de passe) uniquement lorsque la connexion est protégée via SSL (utilisation de LDAPS).

**Mode de compatibilité :**

## Paramètres du service FTP {#ftp-service-settings}

Le service  (`FTP`FTP) permet aux processus d’interagir avec un serveur FTP. Les opérations de ce service permettent de récupérer des fichiers du serveur FTP, de placer des fichiers sur le serveur FTP et de supprimer des fichiers du serveur FTP. Par exemple, vous pouvez stocker des documents, tels que des rapports générés à partir d’un processus, sur un serveur FTP, en vue de les distribuer. Un système externe peut également générer des fichiers en fonction des étapes précédentes d’un processus. Dans une étape suivante du processus, les fichiers peuvent être transférés à un emplacement distant.

Les paramètres ci-dessous sont disponibles pour le service FTP.

**Hôte par défaut :** adresse IP ou URL du serveur FTP.

**Port par défaut :** port utilisé pour la connexion au serveur FTP. La valeur par défaut est 21.

**Nom d’utilisateur par défaut :** nom du compte utilisateur que vous pouvez utiliser pour accéder au serveur FTP. Le compte utilisateur doit disposer de droits suffisants pour effectuer les opérations FTP que ce service requiert.

**Mot de passe par défaut :** mot de passe à utiliser avec le nom d’utilisateur spécifié pour l’authentification auprès du serveur FTP.

## Paramètres du service Generate PDF {#generate-pdf-service-settings}

Le service Generate PDF (`GeneratePDFService`) convertit des fichiers de nombreux formats natifs en documents PDF et convertit des documents PDF en plusieurs formats de fichier.

Les paramètres ci-dessous sont disponibles pour le service Generate PDF.

**Paramètres Adobe PDF :** nom des paramètres Adobe PDF préconfigurés à appliquer à une tâche de conversion, si ces paramètres ne sont pas spécifiés comme faisant partie des paramètres d’appel de l’API. Les paramètres Adobe PDF sont configurés dans Administration Console en cliquant sur Services > PDF Generator > Paramètres Adobe PDF. Ces paramètres sont applicables uniquement aux conversions basées sur PDFMaker.

**Paramètres de sécurité :** nom des paramètres de sécurité préconfigurés à appliquer à une tâche de conversion, si ces paramètres ne sont pas spécifiés comme faisant partie des paramètres d’appel de l’API. Les paramètres de protection sont configurés dans Administration Console en cliquant sur Services > PDF Generator > Paramètres de protection.

**Paramètres de type de fichier :** nom du paramètre de type de fichier préconfiguré à appliquer à une tâche de conversion, si ces paramètres ne sont pas spécifiés comme faisant partie des paramètres d’appel de l’API. Les paramètres de type de fichier sont configurés dans Administration Console en cliquant sur Services > PDF Generator > Paramètres de type de fichier.

**Utiliser Acrobat WebCapture (Windows uniquement) :** lorsque ce paramètre est défini sur true, le service Generate PDF utilise Acrobat X Pro pour toutes les conversions HTML en PDF. La qualité des fichiers PDF produits à partir de fichiers HTML peut en être améliorée, bien que la performance puisse être légèrement plus faible. La valeur par défaut est false. 

**Utiliser la conversion d’images Acrobat (Windows uniquement) :** lorsque ce paramètre est défini sur true, le service Generate PDF utilise Acrobat X Pro pour toutes les conversions Image en PDF. Ce paramètre est utile uniquement si le mécanisme de conversion Java pur par défaut ne peut pas convertir correctement une proportion significative des images d’entrée. La valeur par défaut est false. 

**Activer les conversions AutoCAD basées sur Acrobat (Windows uniquement) :**  lorsque ce paramètre est défini sur true, le service Generate PDF utilise Acrobat X Pro pour toutes les conversions DWG en PDF. Ce paramètre est utile uniquement si AutoCAD n’est pas installé sur le serveur ou si le mécanisme de conversion AutoCAD ne peut pas convertir correctement les fichiers.

**Expressions régulières pour trouver les caractères spéciaux interdits dans le nom d’utilisateur (Windows uniquement) :** spécifie les caractères qui interfèrent avec les opérations d’Export PDF et de Optimize PDF lorsque les caractères apparaissent dans le nom d’un utilisateur.

**Taille du pool ImageToPDF :**  taille du pool du convertisseur Image en PDF par défaut (Java pur) dans le service Generate PDF. Ce paramètre contrôle le nombre maximal de conversions Image en PDF qui peuvent être exécutées simultanément par le service Generate PDF. La valeur par défaut de ce paramètre (recommandée pour les systèmes à un processeur) est 3. Vous pouvez augmenter cette valeur pour les systèmes à plusieurs processeurs.

**Taille du pool HTML vers PDF :**  taille du pool du convertisseur HTML vers PDF dans le service Generate PDF. Ce paramètre contrôle le nombre maximal de conversions HTML en PDF qui peuvent être exécutées simultanément par le service Generate PDF. La valeur par défaut de ce paramètre (recommandée pour les systèmes à un processeur) est 3. Vous pouvez augmenter cette valeur pour les systèmes à plusieurs processeurs.

**Taille du pool OCR :**  taille du pool PaperCaptureService utilisé par PDF Generator pour la reconnaissance optique des caractères (OCR). La valeur par défaut de ce paramètre (recommandée pour les systèmes à un processeur) est 3. Vous pouvez augmenter cette valeur pour les systèmes à plusieurs processeurs. Ce paramètre n’est valide que sur les systèmes Windows.

**Famille de polices de secours pour les conversions HTML en PDF :**  nom de la famille de polices à utiliser dans les documents PDF lorsque la police utilisée dans le code HTML d’origine n’est pas disponible pour le serveur AEM forms. Spécifiez une famille de polices si vous envisagez de convertir des pages HTML qui utilisent des polices non disponibles. Par exemple, les pages créées dans des langues régionales pourraient utiliser des polices non disponibles.

**Retry Logic for Native** ConversionsGos La génération de PDF tente de relancer si la première tentative de conversion a échoué :

**No Retry (Pas de nouvelle tentative) :**

ne pas effectuer de nouvelle tentative de conversion si la première tentative a échoué.

**Réessayer**

effectuer une nouvelle tentative de conversion PDF sans considérer si le délai maximal est atteint. Le délai par défaut pour la première tentative est de 270 s.

**Retry if time permits (Nouvelle tentative selon le temps) :**

effectuer une nouvelle tentative de conversion PDF si la première tentative de conversion a duré moins de temps que le délai spécifié. Par exemple, si le délai spécifié est de 270 s et que la première tentative a duré 200 s, PDF Generator effectue une nouvelle tentative. Si la première tentative a duré 270 s, aucune nouvelle tentative ne sera effectuée.

## Paramètres du service Guides ES4 Utilities  {#guides-es4-utilities-service-settings}

Lorsque vous créez un Guide, certaines ressources, telles que sa définition, sont intégrées dans ce Guide. Les ressources peuvent également se présenter sous la forme de références aux éléments d’application stockés localement ou sur le serveur AEM forms. Le Guide ne contient aucune donnée, et les valeurs des entrées et de l’emplacement d’envoi ne sont pas adaptées à tous les environnements externes.

Dans la plupart des cas, les services de rendu de Guides par défaut suffisent pour préparer un Guide en vue de son utilisation dans Workspace ou dans d’autres environnements externes (dans l’affichage Services de Workbench, le service par défaut est Guides (system)/Processes/Render Guide - 1.0). Le service Guide Utilities (`GuidesUtility`) vous permet de créer un processus personnalisé pour le rendu d’un Guide, si nécessaire.

Les opérations de Guide Utilities vous permettent d’ajouter les tâches de rendu de Guide suivantes à un processus :

* Déterminer si des données sont disponibles pour renseigner le Guide
* Intégrer les données du Guide ou les convertir en lien
* Convertir le contenu référencé en URL accessibles en externe
* Remplacer des valeurs dans un document HTML ou autre wrapper, ou les convertir en URL accessibles en externe
* Définir l’emplacement d’envoi
* Spécifier des valeurs d’entrée
* Créer un paramètre pour représenter le contenu référencé
* Si des variations sont disponibles, en définir une

Les valeurs par défaut du service Guide Utilities prennent en charge la plupart des utilisations. Vous pouvez toutefois, si nécessaire, modifier les valeurs suivantes.

**publicPaths :** cette option a été abandonnée. Ne l’utilisez pas avec AEM forms.

**pathInfoExpiryInSeconds :**  intervalle après lequel expire une demande d’informations de chemin d’accès d’un client. La valeur par défaut est 1.

**supportsExpiryInSeconds :**  intervalle après lequel expire une demande de document provenant d’un client. La valeur par défaut est 315576000.

**mismatchExpiryInSeconds :** intervalle après lequel une demande de document provenant d’un client expire, lorsque l’eTag (balise d’entité) ne correspond pas. (une eTag est un en-tête de réponse HTTP). La valeur par défaut est 1.

**guideContext :** racine de contexte de l’application web Guides. Correspond à la valeur définie via l’application Web Guides. Par défaut, cette valeur est réglée sur /Guides/.

**secureRandomAlgorithm :** algorithme à utiliser lors de la génération de clés et d’identifiants. Cette valeur est transmise à la méthode getInstance de la classe Java SecureRandom. Par défaut, cette valeur est réglée sur SHA1PRNG.

**idBytes :** nombre d’octets aléatoires à utiliser pour un identifiant de clé. La valeur par défaut est 6.

**macAlgorithm :** algorithme MAC (code d’authentification de message) à utiliser pour la vérification d’URL collatérale. Cette méthode est transmise à la méthode getInstance de la classe Mac. Par défaut, cette valeur est réglée sur HmacSHA1.

**macRefreshIntervalInMinutes :** la durée pendant laquelle une clé est principale. Lorsqu’une clé a été active pendant cette durée, une nouvelle clé est générée. La nouvelle clé devient la clé active. La clé précédemment active est conservée pendant une durée équivalente à 10 % de l’intervalle d’actualisation. Ce comportement permet aux URL générées avec l’ancienne clé de continuer à fonctionner pendant le changement de clé. La valeur par défaut est 144000.

**macOverlapIntervalInMinutes :**  durée pendant laquelle la clé précédente reste valide après la génération d’une nouvelle clé. La valeur par défaut est 1 440 minutes (1 jour).

**macKeySeed :**  valeur de départ pour la génération de l’URL sécurisée. Lorsque cette valeur est une option, la clé n’est jamais actualisée. En définissant la même valeur de base sur différents serveurs, ces serveurs génèrent des URL sécurisées compatibles. Cela peut s’avérer utile lorsque plusieurs serveurs Forms sont en cours d’utilisation en même temps qu’un programme d’équilibrage de charge. Entrez une séquence aléatoire de caractères et de nombres en tant que valeur de base.

### Utilisation des guides dans une grappe de serveurs  {#using-guides-in-a-server-cluster}

Le rendu d’un guide dans une grappe de serveurs qui n’utilise pas l’affinité de session échoue et génère une exception NullPointerException. Les demandes de guide exploitent des URL sécurisées qui, par défaut, sont uniques pour le serveur sur lequel elles sont générées. Dans une grappe utilisant l’affinité de session, quand une demande a atteint un nœud de la grappe, toutes les demandes suivantes de cette session ou de l’utilisateur sont acheminées exclusivement à ce serveur. Dans le cas d’une grappe n’utilisant pas l’affinité de session, les demandes suivantes peuvent atteindre n’importe quel serveur de la grappe. Si le serveur atteint par les demandes n’est pas le serveur d’origine, ces dernières ne parviennent pas à résoudre l’URL sécurisée.

Si vous utilisez des guides dans une grappe de serveurs sans affinité de session, définissez la valeur macKeySeed pour le service GuidesUtility, puis arrêtez et redémarrez la grappe.

La valeur macKeySeed constitue le point de départ du générateur de nombres aléatoires utilisé pour générer les URL sécurisées. Si cette valeur est définie, chaque nœud de la grappe initialise le générateur de nombres aléatoires de la même manière et donne accès aux mêmes URL sécurisées. Vous pouvez utiliser n’importe quelle chaîne aléatoire pour cette valeur de départ.

Modifiez la valeur macKeySeed lorsqu’il est nécessaire d’actualiser les URL sécurisées. La régénération des URL sécurisées dépend de votre politique de sécurité. Elle est similaire à la stratégie de régénération permettant de changer le mot de passe racine principal du serveur. La valeur macSeedValue est analogue au mot de passe principal pour les URL sécurisées, car elle est utilisée pour générer un numéro aléatoire unique utilisé pour la génération et la récupération des URL sécurisées.

Vous devez redémarrer la grappe, car macSeedValue est en lecture seule au démarrage du système. Tous les nœuds nécessitent un redémarrage afin de lire la valeur, car ils utilisent cette dernière indépendamment afin d’initialiser leurs nombres aléatoires internes avec la valeur de départ.

## Paramètres du service JDBC  {#jdbc-service-settings}

Le service JDBC (`JdbcService`) permet aux processus d’interagir avec des bases de données.

Le paramètre ci-dessous est disponible pour le service JDBC.

**datasourceName :**  valeur string qui représente le nom JNDI de la source de données à utiliser pour la connexion au serveur de base de données. La source de données doit être définie sur le serveur d’applications qui héberge le serveur Forms. La valeur par défaut correspond au nom JNDI de la source de données de la base de données AEM forms.

## Paramètres du service JMS  {#jms-service-settings}

Le service  (`JMS`JMS) permet l’interaction avec les fournisseurs JMS (Java Messaging System) qui implémentent la messagerie point à point et la messagerie de type publish-subscribe.

Configurez le service JMS avec les propriétés par défaut pour que les opérations du service puissent se connecter et interagir avec un fournisseur JMS et un service JNDI associé. Les propriétés du service sont définies sur les valeurs par défaut basées sur le serveur d’applications JBoss. Modifiez ces valeurs si vous utilisez un autre serveur d’applications pour héberger AEM forms.

Les paramètres ci-dessous sont disponibles pour le service JMS.

**URL du fournisseur :** URL du fournisseur de services JNDI. La valeur par défaut est basée sur le serveur d’applications JBoss. Les URL suivantes sont les valeurs par défaut pour les serveurs d’applications pris en charge par AEM Forms :

**JBoss :**`<server name>:1099` 

**WebLogic :**`<server name>:7001`

**WebSphere :**`<server name>:2809`

**Nom d’utilisateur JNDI :** nom d’utilisateur du compte à utiliser pour l’authentification auprès du fournisseur de services JNDI utilisé pour rechercher les noms de file d’attente et de rubrique. La valeur par défaut est guest.

**Mot de passe JNDI :** mot de passe associé au nom d’utilisateur spécifié pour le nom d’utilisateur JNDI. La valeur par défaut est guest.

**Initial Context Factory :** classe Java à utiliser comme fabrique de contexte initiale. Le service JMS utilise cette classe pour créer un contexte initial qui représente le point de départ pour la résolution des noms des rubriques et des files d’attente. La valeur par défaut est la fabrique de contexte de nommage initial pour le service JMS sur JBoss. Les classes suivantes sont les fabriques de contexte de nommage initial pour les serveurs d’applications pris en charge par AEM Forms :

**JBoss :** org.jnp.interfaces.NamingContextFactory

**WebLogic :** weblogic.jndi.WLInitialContextFactory

**WebSphere :** com.ibm.websphere.naming.WsnInitialContextFactory

**Connection Username :** mot de passe associé au nom d’utilisateur spécifié pour Connection Username. La valeur par défaut est guest.

**Mot de passe de connexion :** mot de passe associé au nom d’utilisateur spécifié pour le nom d’utilisateur de connexion. La valeur par défaut est guest.

**Autres propriétés :** paires nom-valeur de propriété que vous pouvez transmettre au fournisseur de services JNDI. Ces propriétés dépendent de l’implémentation et de la configuration du fournisseur que vous utilisez. 

Les paires nom-valeur de propriétés sont séparées par des points-virgules **;**. Par exemple, le texte suivant indique la valeur qui serait spécifiée pour deux propriétés appelées name1 et name2, avec les valeurs value1 et value2, respectivement :

`name1=value1;name2=value2`

## Paramètres du service LDAP {#ldap-service-settings}

Le service LDAP (`LDAPService`) fournit des opérations permettant d’interroger les répertoires LDAP. Les répertoires LDAP sont généralement utilisés pour stocker des informations sur les personnes, les groupes et les services d’une entreprise.

Les paramètres ci-dessous sont disponibles pour le service LDAP.

**Initial Context Factory :** classe Java à utiliser comme fabrique de contexte. Cette classe est utilisée pour créer une connexion au serveur LDAP. La valeur par défaut est com.sun.jndi.ldap.LdapCtxFactory ; elle est appropriée pour la plupart des serveurs LDAP.

**URL du fournisseur :** URL à utiliser pour la connexion au service LDAP. Le format de la valeur est `ldap://server name:port`

*nom du serveur* est le nom de l’ordinateur qui héberge le serveur LDAP.

*port* est le port de communication que le service LDAP utilise. La valeur par défaut est 389 ; elle représente le port standard utilisé pour les connexions LDAP.

**Nom d’utilisateur :** nom d’utilisateur du compte utilisateur à utiliser pour se connecter au serveur LDAP. Le compte utilisateur doit disposer d’une autorisation pour se connecter au serveur et lire les informations contenues dans le répertoire LDAP. 

Selon le serveur LDAP, le nom d’utilisateur peut être un nom d’utilisateur simple tel que `myname` ou un nom unique, tel que `cn=myname,cn=users,dc=myorg`.

**Mot de passe :** mot de passe correspondant au nom d’utilisateur fourni pour le paramètre Nom d’utilisateur.

**Autres propriétés :** valeur string qui représente d’autres propriétés et leurs valeurs correspondantes que vous pouvez fournir au serveur LDAP. La valeur utilise le format suivant :

`property=value;property=value;...`

## Paramètres du service de configuration Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

Le service de configuration Microsoft SharePoint `(MSSharePointConfigService)`vous permet de spécifier les informations d’identification de l’utilisateur d’AEM forms disposant des droits d’emprunt d’identité. Pour plus d’informations sur les droits d’emprunt d’identité, consultez [Configuration du connecteur pour Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Les paramètres suivants sont disponibles pour le service de configuration Microsoft SharePoint :

* Nom d’utilisateur d’un utilisateur disposant de droits d’emprunt d’identité.
* Mot de passe pour ce même utilisateur

**Activer SSL (HTTPS) :**

**Durée de vie :**  durée, en secondes, pendant laquelle ce profil d’approvisionnement est valide et mis en cache sur le client. La valeur par défaut est 86400 (24 heures). Lorsqu’une application cliente se synchronise avec le serveur et que le temps spécifié est écoulé, l’application cliente demande un nouveau profil d’approvisionnement au serveur.

**Chiffrement :** indique s’il faut chiffrer les données stockées sur le périphérique mobile.

**Application Forms :** active la fonction Forms dans les applications clientes mobiles. Lorsque cette option est sélectionnée, les utilisateurs peuvent ouvrir des formulaires et lancer des processus à partir de leurs périphériques mobiles.

**Application de tâches :** active la fonction Tâches dans les applications clientes mobiles. Lorsque cette option est sélectionnée, les utilisateurs peuvent accéder à la liste des tâches et effectuer des tâches à partir de leurs appareils mobiles.

**Application Content Services :** active la fonctionnalité Content Services dans l’application cliente mobile. Cette fonctionnalité est disponible uniquement pour iOS. Lorsque cette option est sélectionnée, les utilisateurs d’iPhone et d’iPad peuvent accéder aux fichiers stockés sur le serveur WebDAV de votre entreprise.

**Prise en charge hors ligne :** permet aux utilisateurs de continuer à utiliser les applications clientes mobiles même s’ils n’ont pas de connexion au serveur (par exemple, lorsqu’elles sont hors plage de cellules ou en mode avion). Les utilisateurs doivent également activer le paramètre Prise en charge hors ligne sur leurs appareils mobiles. Cette fonctionnalité est disponible pour les appareils Android et iOS. Par défaut, cette fonctionnalité est désactivée.

>[!NOTE]
>
>Si la prise en charge hors ligne a été activée, puis que vous la désactivez, les profils d’approvisionnement des utilisateurs sont mis à jour immédiatement ou dès qu’ils sont en ligne. Si un utilisateur a travaillé hors ligne, toutes les tâches en attente sont renvoyées à leur liste Tâches et tous les éléments de leur file d’attente, y compris les formulaires en attente, les tâches et les formulaires contenant des erreurs de validation, sont supprimés de la file d’attente.

**Android :** permet aux appareils Android de se connecter au serveur.

**Apple iOS :** permet aux iPhone et aux iPad de se connecter au serveur.

**AIR :** permet aux périphériques exécutant des applications basées sur Adobe AIR® de se connecter au serveur.

**BlackBerry :** permet aux périphériques BlackBerry de se connecter au serveur.

**Android Microsoft Exchange ActiveSync requis :** indique si le gestionnaire de stratégies Microsoft Exchange ActiveSync (EA) doit être installé et principal sur les appareils Android. Lorsque cette option est sélectionnée, EA doit être appliqué sur l’appareil Android. Lorsque cette option n’est pas sélectionnée, aucune vérification n’est effectuée, bien que d’autres exigences soient toujours appliquées.

**Longueur minimale du code PIN Android :**  les appareils Android doivent avoir un paramètre global qui permet d’exiger que le code PIN ou le mot de passe soit au moins de cette longueur. Le simple fait d’avoir un code PIN de la longueur spécifiée ne suffit pas. La longueur du code PIN doit être appliquée par le système afin que les utilisateurs ne puissent pas le supprimer ni le raccourcir ultérieurement. La valeur par défaut est 4.

**Android Nombre maximal de tentatives de suppression du mot de passe :** les appareils Android disposent d’un paramètre global qui efface le système après un nombre spécifié de tentatives de mot de passe non valides. Ce paramètre global est activé et égal ou inférieur à la valeur spécifiée ici. La valeur par défaut est 5.

**Android Wipe On Removal :** indique ce qui se produit lorsqu’une violation de stratégie se produit sur un appareil Android. Lorsque cette option est sélectionnée, le compte est supprimé. Lorsque cette option n’est pas sélectionnée, le mot de passe du compte stocké et les données mises en cache sont supprimés. Aucune autre tentative de synchronisation n’est effectuée tant que l’utilisateur n’a pas corrigé la violation de stratégie.

## Paramètres du service Output {#output-service-settings}

Le service Output `(OutputService)`vous permet de fusionner des données de formulaire XML avec une conception de formulaire créée dans AEM Forms Designer pour créer un flux de sortie de document dans l’un des formats suivants :

* PDF ou PDF/A ;
* Adobe PostScript ;
* PCL (Printer Control Language, langage de contrôle d’imprimante) ;
* ZPL (Zebra Programming Language, langage de programmation Zebra).

Le flux de sortie peut être envoyé vers une imprimante réseau, une imprimante locale ou un fichier de disque. Lorsque vous utilisez le service Output dans le cadre d’un processus, vous pouvez également envoyer le flux de sortie vers un destinataire de messagerie en tant que pièce jointe.

Les paramètres ci-dessous sont disponibles pour le service Output.

**Type de transaction :** indique comment un contexte de transaction doit être propagé à une opération :

**Obligatoire :**  prend en charge un contexte de transaction s’il en existe déjà un ; dans le cas contraire, un nouveau contexte de transaction est créé. Il s’agit de la valeur par défaut.

**Nécessite :** crée toujours un contexte de transaction. Si un contexte de transaction actif existe, il est suspendu.

**Transaction Time Out (in sec) :** nombre de secondes pendant lesquelles le fournisseur de transactions sous-jacent attend avant de restaurer une transaction qui englobe cette opération. Cette valeur est ignorée si un contexte de transaction existant est propagé. 

En cas de traitement de fichiers de données volumineux ou d’exploitation d’un serveur fortement sollicité, il peut être nécessaire d’augmenter le délai d’expiration du service Output. Pour modifier la valeur du délai, assurez-vous que les serveurs matériels disposent de la quantité de mémoire appropriée et que celle-ci est disponible pour le tas du serveur d’applications Java. La valeur par défaut est `180`.

## Paramètres du service PDFG Config {#pdfg-config-service-settings}

Les paramètres ci-dessous sont disponibles pour le service PDFG Config ( `PDFGConfigService`).

**User Job Options Directory :** chemin d’accès du dossier du système de fichiers dans lequel le service c écrit les fichiers d’options de tâche accessibles à Acrobat Pro Extended. La valeur par défaut est [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**PS Startup Directory :** chemin d’accès au dossier du système de fichiers dans lequel les fichiers de démarrage requis par Adobe Acrobat Distiller sont enregistrés. La valeur par défaut est [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**PS Startup File :** nom du fichier de démarrage requis par Adobe Acrobat Distiller. La valeur par défaut est example.ps.

**Délai d’expiration de conversion du serveur :**  délai d’expiration de conversion de tâche maximal (en secondes) pour le service Generate PDF et le service Distiller. Ce paramètre limite le délai d’expiration de conversion maximal qui peut être spécifié dans le fichier config.xml et dans les pages de Administration Console pour PDF Generator. La valeur par défaut est 270.

**Délai d’expiration global du serveur :** lors des conversions PDF, un serveur Forms prend en compte le délai d’expiration. Configurez la valeur du délai d’expiration pour résoudre ce problème.

**Préfixe des options de tâche :** préfixe utilisé par le service Generate PDF pour ajouter en préfixe une chaîne courte aux fichiers d’options de tâche qu’il crée temporairement pour être utilisés par Acrobat Distiller. La valeur par défaut est pdfg.

**Applications non Unicode :** liste séparée par des virgules de noms d’application connus pour être incompatibles avec l’Unicode. Cette liste est préremplie avec les noms de plusieurs applications, dont la prise en charge est préconfigurée dans PDF Generator. Si vous choisissez d’ajouter une prise en charge pour des conversions PDF via des applications tierces incompatibles avec Unicode, vous devez les ajouter à cette liste. La valeur par défaut est Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**Server Threadpool Count :** contrôle la taille du pool de threads que le service Generate PDF utilise en interne pour traiter les demandes de conversion HTML vers PDF qui impliquent une indexation (conversion de pages liées accessibles à partir de la page principale). La valeur par défaut est 20.

**Secondes d’analyse de nettoyage PDFG :** reportez-vous à la section Secondes avant expiration de la tâche pour plus d’informations.

**Secondes avant expiration de la tâche :** le service Generate PDF supprime les fichiers d’entrée dès qu’ils sont convertis. Il stocke les fichiers de sortie de façon temporaire, pendant une durée définie par les paramètres Secondes d’analyse de nettoyage PDFG et Secondes avant expiration de la tâche. 

Le paramètre Secondes avant expiration de la tâche spécifie l’ancienneté que doit avoir un fichier ou un dossier vide avant de pouvoir être supprimé. Le paramètre Secondes d’analyse de nettoyage PDFG indique la fréquence d’analyse, par un thread de nettoyage, des fichiers temporaires à la recherche de fichiers pouvant être supprimés.

Par exemple, si Secondes avant expiration de la tâche est défini sur 100 et Secondes d’analyse de nettoyage PDFG sur 200, le thread de nettoyage s’exécute toutes les 200 secondes et supprime les fichiers datant de 100 secondes ou plus. 

La valeur par défaut de Secondes d’analyse de nettoyage PDFG est `43200` (12 heures). La valeur par défaut de Secondes avant expiration de la tâche est `86400` (24 heures).

**Paramètres régionaux par défaut :** permet de remplacer les paramètres régionaux par défaut (pays + langue) du serveur sur lequel le service Generate PDF est déployé. Si ce paramètre n’est pas spécifié, les paramètres régionaux par défaut sont alors déterminés à partir du système d’exploitation dans lequel le service est déployé. Ce paramètre contrôle la langue dans laquelle les messages d’erreur sont renvoyés aux API.

## Paramètres du service Forms Workflow Data Services  {#forms-workflow-data-services-service-settings}

Les services suivants forment une extension de Data Services et exposent les assembleurs utilisés par Workspace pour communiquer avec le serveur. Ne modifiez pas les options de configuration pour ces services à moins que vous n’y soyez invité par l’assistance technique d’Adobe. Ces services ne sont pas censés être directement accessibles :

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Paramètres du service Remoting {#remoting-service-settings}

La plupart des services sont configurés afin que vous puissiez y accéder avec AEM forms Remoting (obsolète pour AEM forms). Pour plus d’informations sur AEM Forms Remoting (obsolète pour AEM Forms), consultez [Programmation avec AEM Forms](https://adobe.com/go/learn_aemforms_programming_63).

Les paramètres ci-dessous sont disponibles pour le service Remoting.

**Méthode d’authentification du client Flex :** détermine le type de réponse que le serveur renvoie au client lorsque le service appelé est activé pour la sécurité, l’opération appelée ne prend pas en charge les appels anonymes et le client transmet des informations d’identification non valides ou aucune information d’identification non valide. Choisissez entre Personnalisée ou Standard. La valeur par défaut est Standard.

**Autoriser la sérialisation des classes non sérialisables :**  la plupart des points de fin d’AEM forms autorisent uniquement l’utilisation de classes sérialisables pour l’appel. Dans les versions antérieures, les points de fin Remoting autorisaient l’utilisation des classes non sérialisables pour les appels depuis les clients Flex. Pour éviter toute vulnérabilité de sécurité décrite dans APS11-15, ceci a été modifié. Si vous souhaitez continuer à utiliser des classes non-sérialisables avec le point de fin Flex Remoting, cochez cette case.

## Paramètres du service Repository  {#repository-service-settings}

Le service Repository (`RepositoryService`) fournit du stockage de ressources et des services de gestion à AEM forms. Lorsque des développeurs créent une application, ils peuvent déployer les actifs dans le référentiel plutôt que dans un système de fichiers. Les actifs peuvent être constitués de formulaires XML, de formulaires PDF (y compris de formulaires Acrobat), de fragments de formulaire, d’images, de profils, de stratégies, de fichiers SWF, DDX et WSDL, de schémas XML et de données de test.

Vous pouvez utiliser le référentiel par défaut inclus dans AEM forms ou utiliser un référentiel tiers (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager).

Le service Repository Provider est un délégué de service qui sert d’interface à un service du fournisseur. Il vous permet de vous connecter à une interface API commune et de ne pas avoir à connaître le service du fournisseur qui implémente les capacités de stockage. Le service Repository Provider fournit un stockage de base de données pour les ressources du service Repository.

Le paramètre ci-dessous est disponible pour le service Repository.

**Provider Service :** nom du service utilisé comme fournisseur de stockage. La valeur par défaut est RepositoryProviderService.

## Paramètres du service Signature {#signature-service-settings}

Le service Signature `SignatureService`( ) permet à votre entreprise de garantir la sécurité et la confidentialité des documents Adobe PDF qu’elle diffuse et reçoit. Ce service utilise les signatures et certifications numériques pour s’assurer que les documents ne sont pas modifiés. La modification d’un document rompt sa signature. Les fonctions de sécurité étant appliquées au document proprement dit, ce dernier reste protégé et contrôlé tout au long de son cycle de vie, aussi bien de l’autre côté du pare-feu que dans le cadre de son téléchargement hors connexion ou de son renvoi à l’entreprise.

Les paramètres ci-dessous sont disponibles pour le service Signature.

**Nom du service SPI HSM distant :** Cette option est à utiliser lorsque le HSM est installé sur un ordinateur distant. Spécifiez cette option quand AEM forms est installé sur un système Windows 64 bits et que vous utilisez des périphériques HSM pour la signature.

**URL du service Web HSM distant :** spécifiez cette option lorsque AEM forms est installé sur Windows 64 bits et que vous utilisez des périphériques HSM pour la signature.

**Certification To Include Form Load Changes :** lorsque cette option est sélectionnée, l’état du formulaire XFA est certifié en plus du modèle XFA. Notez que l’activation de cette option peut avoir un impact négatif sur les performances. La valeur par défaut est true.

**Exécuter les scripts JavaScript du document :** indique s’il faut exécuter les scripts JavaScript du document lors des opérations de signature. La valeur par défaut est false. 

**Traiter les documents avec compatibilité Acrobat 9 :** indique s’il faut activer la compatibilité Acrobat 9. Par exemple, lorsque cette option est sélectionnée, l’option Visible Certification in Dynamics PDFs est activée. La valeur par défaut est false. 

**Incorporer les informations de révocation lors de la signature :** indique si les informations de révocation sont incorporées lors de la signature du document PDF. La valeur par défaut est false. 

**Incorporer les informations de révocation lors de la certification :** indique si les informations de révocation sont incorporées lors de la certification du document PDF. La valeur par défaut est false. 

**Application de l’incorporation des informations de révocation pour tous les certificats lors de la signature/certification :** indique si une opération de signature ou de certification échoue si des informations de révocation valides pour tous les certificats ne sont pas incorporées. Notez que si un certificat ne contient pas d’informations CRL ou OCSP, il est considéré comme valide, même si aucune information de révocation n’est récupérée. La valeur par défaut est false. 

**Ordre de vérification de révocation :** spécifie l’ordre de vérification de révocation lorsque la vérification est possible par le biais des mécanismes Liste de révocation des certificats (CRL) et Protocole d’état du certificat en ligne (OCSP). La valeur par défaut est OCSPFirst.

**Taille maximale des informations d’archivage de révocation :**  taille maximale des informations d’archivage de révocation en kilo-octets. AEM forms tente de stocker le plus grand nombre d’informations de révocation possible sans dépasser cette limite. La valeur par défaut est 10 Ko.

**Prise en charge des signatures créées à partir des versions antérieures des produits Adobe :**  lorsque cette option est sélectionnée, la signature créée à l’aide de la version préliminaire des produits Adobe sera validée correctement. La valeur par défaut est false. 

**Option de durée de vérification :** indique l’heure de vérification du certificat d’un signataire. La valeur par défaut est Secure Time Else Current Time.

**Utiliser les informations de révocation archivées dans la signature lors de la validation :** indique si les informations de révocation archivées avec la signature sont utilisées pour la vérification de révocation. La valeur par défaut est true.

**Utiliser les informations de validation stockées dans le document pour la validation des signatures :**  lorsque cette option est sélectionnée, les informations de validation (y compris les informations de révocation et d’horodatage) intégrées dans le document sont utilisées pour valider les signatures. La valeur par défaut est true.

**Nombre maximal de sessions de vérification imbriquées autorisé :**  nombre maximal de sessions de vérification imbriquées autorisées. AEM forms utilise cette valeur pour empêcher une boucle infinie lors de la vérification des certificats des signataires OCSP ou CRL en cas de configuration incorrecte du certificat OCSP ou CRL. La valeur par défaut est 10.

**Ecartement maximal de l’horloge pour la vérification :**  durée maximale, en minutes, pendant laquelle l’heure de signature peut être postérieure à l’heure de validation. Si le décalage est supérieur à cette valeur, la signature n’est pas valable. la valeur par défaut est de 65 minutes.

**Cache de durée de vie du certificat :**  durée de vie d’un certificat, récupéré en ligne ou par d’autres moyens, dans le cache. La valeur par défaut est de 1 jour.

### Options de transport {#transport-options}

**Hôte du proxy :** URL de l’hôte du proxy. Attribut utilisé uniquement si une valeur valide est indiquée. Pas de valeur par défaut.

**Port du proxy :** port du proxy. Saisissez tout numéro de port valide compris entre 0 et 65535. La valeur par défaut est 80.

**Nom d’utilisateur de connexion au proxy :** nom d’utilisateur de connexion au proxy. Attribut utilisé uniquement si une valeur valide est indiquée pour l’hôte proxy et le port du proxy. Pas de valeur par défaut.

**Mot de passe de connexion du proxy :** mot de passe de connexion du proxy. utilisé uniquement si une valeur valide est indiquée pour l’hôte proxy, le port du proxy et le nom d’utilisateur de connexion du proxy. Pas de valeur par défaut.

**Limite maximale de téléchargement :** quantité maximale de données, en Mo, pouvant être reçue par connexion. Valeur minimale : 1 Mo. Valeur maximale : 1 024 Mo. La valeur par défaut est de 16 Mo.

**Délai d’expiration de la connexion :**  durée maximale d’attente, en secondes, pour établir une nouvelle connexion. Valeur minimale : 1. Valeur maximale : 300. Valeur par défaut : 5.

**Délai d’expiration du socket :**  durée d’attente maximale, en secondes, avant l’expiration du socket (en attendant le transfert des données). Valeur minimale : 1. Valeur maximale : 3600. Valeur par défaut : 30.

### Options de validation du chemin d’accès {#path-validation-options}

**Require Explicit Policy :** indique si le chemin doit être valide pour au moins l’une des stratégies de certificat associées à l’ancre de confiance du certificat du signataire. La valeur par défaut est false. 

**Inhibit ANY Policy :** indique si l’identifiant d’objet de stratégie (OID) doit être traité s’il est inclus dans un certificat. La valeur par défaut est false. 

**Inhibit Policy Mapping :** indique si le mappage de stratégie est autorisé dans le chemin de certification. La valeur par défaut est false. 

**Check All Paths :** indique si tous les chemins doivent être validés ou si la validation doit s’arrêter après avoir trouvé le premier chemin valide. Sélectionnez true ou false. La valeur par défaut est false. 

**Serveur LDAP :** serveur LDAP utilisé pour rechercher des certificats pour la validation du chemin. Pas de valeur par défaut.

**Suivez les URI dans l’AIA de certificat :** indique si les URI (Uniform Resource Identifiers) dans l’AIA de certificat sont traités lors de la découverte du chemin. La valeur par défaut est false. 

**Extension de contraintes de base requise dans les certificats d’autorité de certification :** indique si l’extension de contraintes de base de l’autorité de certification (CA) doit être présente pour les certificats d’autorité de certification. Certains des tout premiers certificats racine allemands certifiés (7 et antérieurs) ne sont pas conformes à la RFC 3280 et ne contiennent pas l’extension de contraintes de base. Si le certificat EE d’un utilisateur est associé à une telle racine, désactivez cette case à cocher. La valeur par défaut est true.

**Exiger une signature de certificat valide lors de la création de chaînes :** indique si le créateur de chaînes nécessite des signatures valides sur les certificats utilisés pour créer des chaînes. Lorsque cette case est cochée, le générateur de chaînes ne crée pas de chaînes comportant des signatures RSA non valides dans les certificats. Soit la chaîne CA > ICA > EE où la signature de l’AC (Autorité de certification) sur une ICA est incorrecte. Si ce paramètre est true, la création de chaînes s’arrête au niveau de l’ICA, et l’AC n’est pas incluse dans la chaîne. Si ce paramètre est false, la chaîne complète des trois certificats est générée. Ce paramètre n’a aucune incidence sur les signatures DSA. Valeur par défaut : false.

### Options du fournisseur d’horodatage  {#timestamp-provider-options}

**URL du serveur TSP :** URL du fournisseur d’horodatage par défaut. Attribut utilisé uniquement si une valeur valide est indiquée. Pas de valeur par défaut.

**Nom d’utilisateur du serveur TSP :** nom d’utilisateur s’il est requis par le fournisseur d’horodatage. Utilisé uniquement si une valeur valide est indiquée pour l’URL. Pas de valeur par défaut.

**Mot de passe du serveur TSP :** mot de passe du nom d’utilisateur ci-dessus si le fournisseur d’horodatage l’exige. Utilisé uniquement si une valeur valide est indiquée pour l’URL et le nom d’utilisateur. Pas de valeur par défaut.

**Algorithme de hachage de requête :** indique l’algorithme de hachage à utiliser lors de la création de la demande pour le fournisseur d’horodatage. La valeur par défaut est SHA1.

**Style de vérification de révocation :** spécifie le style de vérification de révocation utilisé pour déterminer l’état de confiance du certificat du fournisseur d’horodatage à partir de son état de révocation observé. La valeur par défaut est BestEffort.

**Envoyer une valeur à usage unique :** indique si une valeur à usage unique est envoyée avec la demande du fournisseur d’horodatage. Une telle valeur peut être un horodatage, un compteur de visites sur une page Web ou bien un marqueur spécial destiné à limiter ou empêcher la réplication ou la reproduction non autorisées d’un fichier. La valeur par défaut est true.

**Utiliser les horodatages expirés lors de la validation :**  lorsque cette option est sélectionnée, les horodatages expirés peuvent être utilisés pour récupérer les heures de validation des signatures. La valeur par défaut est true.

**Taille de réponse TSP :** taille estimée, en octets, de la réponse TSP. Cette valeur doit correspondre à la taille maximale de la réponse de l’horodatage que le fournisseur d’horodatage configuré peut renvoyer. Ne la modifiez pas à moins d’être parfaitement sûr de ce que vous faites. Valeur minimale : 60 octets. Valeur maximale : 10 240 octets. Valeur par défaut : 4 096 octets.

**Ignorer l’extension du serveur de tampons temporels** : sélectionnez **Ignorer l’extension du serveur de tampons temporels** afin d’empêcher le serveur AEM Forms de contacter le serveur de tampons temporels spécifié. La sélection de cette option permet d’éviter les échecs de processus qui se produisent en raison du délai de connexion entre les serveurs AEM Forms et de tampons temporels.

### Options de listes de révocation des certificats  {#certificate-revocation-list-options}

**Consult Local URI First :** indique si l’emplacement de la CRL fourni dans l’URI local ou la recherche CRL doit recevoir la préférence de tout emplacement spécifié dans un certificat à des fins de vérification de révocation. La valeur par défaut est false. 

**URI local pour la recherche de CRL :**  URL du fournisseur de CRL local. Cette valeur est consultée uniquement si le paramètre Consult Local URI First ci-dessus est défini sur true. Pas de valeur par défaut.

**Style de vérification de révocation :** spécifie le style de vérification de révocation utilisé pour déterminer l’état de confiance du certificat du fournisseur de CRL à partir de son état de révocation observé. La valeur par défaut est BestEffort.

**Serveur LDAP pour la recherche CRL :** serveur LDAP utilisé pour obtenir les CRL (comme www.ldap.com). Toutes les requêtes DN de CRL sont adressées à ce serveur. Pas de valeur par défaut.

**Go Online :** indique s’il faut se connecter pour récupérer une CRL. Avec la valeur false, seules les CRL en cache (sur le disque local ou incorporées avec signature) sont consultées. La valeur par défaut est true.

**Ignorer les dates de validité :** indique s’il faut ignorer les heures thisUpdate et nextUpdate de la réponse, ce qui empêche ces heures d’avoir un effet négatif sur la validité de la réponse. La valeur par défaut est false. 

**Require AKI extension in CRL :** indique si l’extension de l’identifiant de clé d’autorité doit être incluse dans une CRL. Valeur par défaut : false.

### Options du protocole OCSP (Online Certificate Status Protocol)  {#online-certificate-status-protocol-options}

**URL du serveur OCSP :** URL du serveur OCSP par défaut. Le fait que le serveur OCSP spécifié via cette URL soit utilisé ou non dépend du paramètre Option URL à consulter. Pas de valeur par défaut.

**Option URL à consulter :** contrôle la liste et l’ordre des serveurs OCSP utilisés pour effectuer la vérification d’état. La valeur par défaut est UseAIAInCert.

**Revocation Check Style** : indique le style de vérification de révocation utilisé lors de la vérification du certificat du serveur OCSP. La valeur par défaut est CheckIfAvailable.

**Envoyer à usage unique :** indique si une valeur à usage unique est envoyée avec la requête OCSP. Une telle valeur peut être un horodatage, un compteur de visites sur une page Web ou bien un marqueur spécial destiné à limiter ou empêcher la réplication ou la reproduction non autorisées d’un fichier. La valeur par défaut est true.

**Max Clock Skew Time :** décalage maximal autorisé, en minutes, entre le temps de réponse et l’heure locale. Valeur minimale : 0. Valeur maximale : 2 147 483 647 min. La valeur pas défaut est : 5 min.

**Response Freshness Time :** durée maximale, en minutes, pour laquelle une réponse OCSP préconstruite est considérée comme valide. Valeur minimale : 1 Min. Valeur maximale : 2 147 483 647 min. La valeur par défaut est de 525600 (un an).

**Sign OCSP Request :** indique si la requête OCSP doit être signée. La valeur par défaut est false. 

**Request Signer Credential Alias :** spécifie l’alias d’identification à utiliser pour signer la demande OCSP si la signature est activée. Cette option est utilisée uniquement si la signature de la demande OCSP est activée. Pas de valeur par défaut.

**Go Online :** indique s’il faut se connecter pour vérifier la révocation. La valeur par défaut est true.

**Ignorer les heures thisUpdate et nextUpdate de la réponse :** indique s’il faut ignorer les heures thisUpdate et nextUpdate de la réponse, ce qui empêche ces heures d’avoir un effet négatif sur la validité de la réponse. La valeur par défaut est false. 

**Allow OCSPNoCheck extension :** indique si l’extension OCSPNoCheck est autorisée dans le certificat de signature de la réponse. La valeur par défaut est true.

**Require OCSP ISIS-MTT CertHash Extension :** indique si une extension de hachage de clé publique de certificat doit être incluse dans les réponses OCSP. Valeur par défaut : false.

### Options de gestion des erreurs pour le débogage  {#error-handling-options-for-debugging}

**Purger le cache de certificats lors de l’appel API suivant :** indique s’il faut purger le cache de certificats lors de l’appel de l’opération de service Signature suivante. Une fois l’opération appelée, cette option reprend la valeur false. La valeur par défaut est false. 

**Purger le cache de CRL lors de l’appel API suivant :** indique s’il faut purger le cache de CRL lors de l’appel de l’opération du service Signature suivante. Une fois l’opération appelée, cette option reprend la valeur false. La valeur par défaut est false. 

**Purger le cache OCSP lors de l’appel API suivant :** indique s’il faut purger le cache OCSP lors de l’appel de l’opération du service Signature suivante. Une fois l’opération appelée, cette option reprend la valeur false. Valeur par défaut : false.

## Paramètres du service Watched Folder  {#watched-folder-service-settings}

Le service Watched Folder (`WatchedFolder`) permet de configurer les attributs communs à tous les points de fin Watched Folder. Il fournit également des valeurs par défaut pour les points de fin des dossiers de contrôle (voir [Configuration des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)). Il n’est pas appelé par des applications clientes externes ni utilisé dans des processus créés avec Workbench.

Les paramètres ci-dessous sont disponibles pour le service WatchedFolder.

**Expression cron :** expression cron utilisée par quartz pour planifier l’interrogation du répertoire d’entrée.

**Nombre de répétitions :** nombre d’interrogations du répertoire d’entrée. Nombre de répétitions par défaut à utiliser si cette valeur n’est pas spécifiée dans la configuration des points de fin. La valeur -1 indique une analyse indéfinie du répertoire. La valeur par défaut est -1.

**Intervalle de répétition :** nombre par défaut de secondes entre chaque interrogation. Cette valeur est utilisée comme intervalle de répétition à moins qu’une valeur différente ne soit définie dans la configuration du point de fin du dossier de contrôle. La valeur par défaut est 5. Pour plus d’informations, voir la description du paramètre Batch Size.

**Asynchrone :** identifie le type d’appel comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est asynchrone.

**Temps d’attente :** valeur par défaut du temps, en secondes, après lequel les fichiers sont récupérés dans les dossiers d’entrée. Si le fichier ou le dossier sont plus anciens que la durée définie dans l’attribut Durée d’attente, ils sont sélectionnés pour traitement. La valeur par défaut est 0.

**Taille du lot :**  valeur par défaut du nombre de fichiers ou de dossiers traités par analyse. La valeur par défaut est 2.

Les paramètres Intervalle de répétition et Taille du lot permettent de déterminer le nombre de fichiers sélectionnés par Watched Folder pour chaque analyse. Watched Folder utilise un pool de threads Quartz pour analyser le dossier input. Le pool de threads est partagé avec d’autres services. Si l’intervalle d’analyse défini est court, les threads analysent fréquemment le dossier input. Si des fichiers sont déposés régulièrement dans le dossier de contrôle, faites en sorte que l’intervalle d’analyse soit court. Si au contraire, des fichiers y sont déposés peu fréquemment, utilisez un intervalle d’analyse plus long afin que les autres services puissent utiliser les threads. 

Si un gros volume de fichiers est déposé, définissez une grande taille de lot. Si par exemple, le service invoqué par le point de fin Watched Folder peut traiter 700 fichiers par minute et que les utilisateurs déposent des fichiers dans le dossier input à la même fréquence, la définition de la taille du lot sur 350 et de l’intervalle de répétition sur 30 secondes permet de maintenir les performances de Watched Folder sans subir les conséquences d’une analyse du dossier de contrôle trop fréquente.  

Lorsque des fichiers sont déposés dans le dossier de contrôle, ce dernier les répertorie dans les entrées, ce qui réduit parfois les performances si l’analyse s’effectue toutes les secondes. L’allongement de l’intervalle d’analyse permet d’améliorer les performances. Si le volume des fichiers déposés est réduit, ajustez la taille du lot et l’intervalle de répétition en conséquence. Par exemple, si 10 fichiers sont déposés toutes les secondes, essayez de définir l’intervalle de répétition sur 1 et la taille du lot sur 10. 

Dans une configuration en grappe, la taille du lot d’un dossier de contrôle n’est pas mise à l’échelle sur plusieurs nœuds de la grappe. Par exemple, si la taille du lot est définie sur `2` (grappe à deux nœuds) et que l’option Ralentissement est sélectionnée, les nœuds traitent ensemble les fichiers par lots de deux. Cette opération remplace le traitement simultané de deux fichiers par chaque nœud.

**Remplacer les noms de fichier en double :** chaîne booléenne qui indique si le dossier de contrôle remplace les noms de fichier de résultat en double et si les documents conservés du même nom doivent être remplacés.

**Conserver le dossier :** valeur par défaut du dossier preserve. Ce dossier est utilisé pour copier les fichiers source en cas de traitement réussi de l’entrée. Il peut s’agir d’un chemin d’accès vide, relatif ou absolu avec un modèle de fichier, tel que décrit pour le paramètre Result Folder.

**Dossier d’échec :** nom du dossier dans lequel les fichiers d’échec sont copiés. Il peut s’agir d’un chemin d’accès vide, relatif ou absolu avec un modèle de fichier, tel que décrit pour le paramètre Result Folder.

**Result Folder :** nom par défaut du dossier result. Ce dossier est utilisé pour copier les fichiers obtenus. Il peut s’agir d’un chemin d’accès vide, relatif ou absolu répondant au modèle de fichier suivant :

* %F = préfixe du nom du fichier
* %E = extension du nom du fichier
* %Y = année (complète)
* %y = année (deux derniers chiffres)
* %M = mois
* %D = jour du mois
* %d = jour de l’année
* %H = heure (horloge 24 heures)
* %h = heure (horloge 12 heures)
* %m = minute
* %s = seconde
* %l = milliseconde
* %R = nombre aléatoire (de 0 à 9)
* %P = ID de processus ou de travail

Par exemple, s’il est 20 h, que nous sommes le 17 juillet 2009 et que vous indiquez `C:/Test/WF0/failure/%Y/%M/%D/%H/`, le dossier de résultats est `C:/Test/WF0/failure/2009/07/17/20`.

Si le chemin d’accès n’est pas absolu, mais relatif, le dossier est créé dans le dossier de contrôle. Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>plus les dossiers de résultats sont petits, plus les performances de Watched Folder augmentent. Par exemple, si la charge estimée pour le dossier de contrôle est de 1 000 fichiers par heure, utilisez un modèle de type `result/%Y%M%D%H`, afin qu’un nouveau sous-dossier soit créé toutes les heures. Si la charge est moindre (par exemple, 1 000 fichiers par jour), vous pouvez utiliser un modèle de type `result/%Y%M%D`.

**Dossier d’évaluation :** nom par défaut du dossier d’évaluation dans le dossier de contrôle.

**Input Folder :** nom par défaut du dossier input dans le dossier de contrôle.

**Conserver en cas d’échec :** si la valeur est true, les fichiers d’origine sont conservés dans le dossier failure en cas d’échec.

**Ralentissement :** lorsque cette option est sélectionnée, elle limite le nombre de tâches du dossier de contrôle AEM processus des formulaires à un moment donné. La valeur Taille du lot détermine le nombre maximal de tâches (voir A propos du ralentissement).

## Paramètres du service Web Service {#web-service-service-settings}

Le service Web Service (`WebService`) permet aux processus d’appeler les opérations correspondantes.

Le service Web Service permet aux processus d’appeler les opérations correspondantes. Par exemple, une entreprise peut souhaiter intégrer un processus pour stocker et récupérer des informations, telles que les détails de contact et de compte, en appelant les services Web exposés d’un fournisseur de services. Le service Web Service appelle un service Web spécifié et transmet les valeurs de chacun de ses paramètres, puis enregistre les valeurs de renvoi de l’opération dans une variable désignée d’un processus.

Le service Web Service interagit avec les services Web en envoyant et en recevant des messages SOAP. Il prend également en charge l’envoi de pièces jointes MIME, MTOM et SwaRef avec des messages SOAP à l’aide du protocole WS-Attachment. Les interactions du service Web Service sont compatibles avec les systèmes SAP et les services Web .NET.

Les paramètres ci-dessous sont disponibles pour le service Web Service.

**Key Store :** chemin d’accès complet au fichier de stockage de clés contenant la clé privée à utiliser pour l’authentification. Le serveur Forms doit être en mesure d’accéder au fichier.

**Mot de passe du Key Store :** mot de passe du fichier de KeyStore.

**Type de magasin de clés :** type du magasin de clés. N’indiquez aucune valeur si vous souhaitez utiliser le type de fichier de stockage des clés par défaut configuré pour la machine virtuelle Java exécutant le serveur Forms. Dans le cas contraire, spécifiez une des valeurs suivantes :

* jks
* pkcs12
* cms
* jceks

**Trust Store :** chemin d’accès complet au fichier Trust Store qui contient la clé publique du serveur de services Web.

**Mot de passe Trust Store :** mot de passe du fichier truststore.

**Type de Trust Store :** type de Trust Store. N’indiquez aucune valeur si vous souhaitez utiliser le type de fichier de stockage des clés par défaut configuré pour la machine virtuelle Java exécutant le serveur Forms. Dans le cas contraire, spécifiez une des valeurs suivantes :

* jks
* pkcs12
* cms
* jceks

## Paramètres du service XSLT Transformation  {#xslt-transformation-service-settings}

Le service XSLT Transformation (`XSLTService`) permet aux processus d’appliquer des transformations XSLT (eXtensible Stylesheet Language Transformations) aux documents XML.

Le paramètre ci-dessous est disponible pour le service XSLT Transformation.

**Nom d’usine :** nom qualifié complet de la classe Java à utiliser pour exécuter des transformations XSLT. Si aucune valeur n’est spécifiée, la valeur d&#39;usine par défaut configurée dans la machine virtuelle Java exécutant le serveur Forms est utilisée.

## Modification des paramètres de sécurité d’un service  {#modifying-security-settings-for-a-service}

Le serveur Forms vous permet de configurer des paramètres de sécurité pour chaque service. Vous pouvez ainsi configurer un contrôle d’accès affiné service par service.

Les profils de sécurité par défaut sont installés, et vous pouvez les configurer en fonction des besoins de votre système. Chaque profil de sécurité est associé à un domaine et créé au niveau de l’utilisateur ou du groupe.

### Modification des paramètres de sécurité d’un service  {#modify-security-settings-for-a-service}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Cliquez sur l’onglet Sécurité.
1. Dans la liste Demander aux appelants de s’authentifier, sélectionnez Oui ou Non pour indiquer si le service peut être appelé avec ou sans informations d’identification.

   Si vous sélectionnez Oui, l’appelant du service doit être authentifié et l’entité de sécurité utilisateur de cet appelant doit être autorisée à appeler le service ; si ce n’est pas le cas, la tentative d’appel est refusée.

   Si vous sélectionnez Non, l’appelant du service peut être ou non authentifié. L’appel du service réussit toujours puisqu’aucune vérification des autorisations n’est effectuée.

1. Pour les services qui contiennent une ou plusieurs opérations marquées pour l’accès anonyme, sélectionnez ou désélectionnez Accès anonyme autorisé. Lorsque l’accès anonyme est activé, tout utilisateur du système peut appeler des opérations dans le service. S’il est désactivé, les utilisateurs doivent être autorisés à appeler le service et invoquer des opérations. Ces autorisations sont accordées aux utilisateurs directement ou lorsque ces utilisateurs font partie d’un groupe disposant d’autorisations de ce type.
1. Pour certains services, le compte utilisateur qui exécute l’opération a une incidence sur le résultat. Par exemple, dans Content Services (obsolète), l’utilisateur qui stocke du contenu devient propriétaire de ce contenu, ce qui a une incidence sur les utilisateurs qui seront par la suite autorisés à y accéder. Si vous utilisez un processus pour stocker du contenu, réfléchissez à l’utilisateur qui exécutera le service Document Management, car il deviendra en effet propriétaire du contenu stocké.

   Pour spécifier l’identité d’exécution utilisée par un service pour exécuter des opérations, sélectionnez Spécifier Exécuter en tant que, puis une option dans la liste associée, et cliquez sur enregistrer. Faites votre choix parmi les options suivantes :

   **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

   **Système :** utilise l’utilisateur Système pour exécuter le service avec des droits illimités.

   **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Lors de la sélection de cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, qui vous permet de rechercher et sélectionner l’utilisateur.

   Si vous ne sélectionnez pas Spécifier Exécuter en tant que, le comportement par défaut est utilisé.

   >[!NOTE]
   >
   >les services de rendu et d’envoi utilisés avec les variables xfaForm, Document Form et Form sont toujours exécutés à l’aide du compte utilisateur Système.

1. Cliquez sur Ajouter une entité de sécurité pour indiquer les droits dont disposent les utilisateurs et les groupes pour ce service.
1. L’écran Sélectionner une entité de sécurité affiche les utilisateurs et les groupes configurés dans User Management. Si l’utilisateur ou le groupe souhaité n’est pas affiché, utilisez la fonction de recherche pour le trouver. Cliquez sur un nom d’utilisateur ou de groupe.
1. Dans l’écran Ajouter des droits, sélectionnez les droits à affecter à l’utilisateur ou au groupe pour ce service.

   * **INVOKE_PERM :** invocation de toutes les opérations sur le service.
   * **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.
   * **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.
   * **START_STOP_PERM :** démarrage et arrêt d’un service.
   * **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points de fin d’un service.
   * **CREATE_VERSION_PERM :** création d’une nouvelle version du service.
   * **DELETE_VERSION_PERM :** suppression d’une version du service.
   * **MODIFY_VERSION_PERM :** modification d’une version du service.
   * **READ_PERM :** affichage du service.
   * **PROCESS_OWNER_PERM :** utilisation dans une future version d’AEM forms. N’utilisez pas ce droit.
   * **SERVICE_MANAGER_PERM :** utilisation dans une future version d’AEM forms. N’utilisez pas ce droit.
   * **SERVICE_AGENT_PERM :** Utilisation réservée à une future version d’AEM forms. N’utilisez pas ce droit.

1. Cliquez sur Ajouter.

### Suppression de l’entité de sécurité dans un profil de sécurité  {#remove-the-principal-from-a-security-profile}

1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Cliquez sur l’onglet **Sécurité**, sélectionnez le profil de sécurité à supprimer, puis cliquez sur **Supprimer**.

## Configuration du pool d’un service  {#configuring-pooling-for-a-service}

Chaque service peut tirer parti des options de pool pour traiter les demandes d’appel entrantes. Le recours à un pool de service garantit que les instances du service sont appelées par un seul thread à la fois et qu’elles sont réutilisées sur l’ensemble des demandes d’appel, ce qui permet d’optimiser les performances. Vous pouvez également recourir à un pool pour définir l’option Instances maximales des services asynchrones, qui autorise les services à limiter le nombre de demandes traitées en parallèle.

### Activation du pool  {#enable-pooling}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Cliquez sur l’onglet Mise en pool.
1. Dans la liste Stratégie de traitement de requête, sélectionnez Instances mises en pool pour toutes les requêtes.
1. Dans le champ Taille initiale du pool d’instances de service, saisissez la taille initiale du pool. Lors du déploiement du service, cette valeur permet de déterminer le nombre d’instances d’implémentation du service à créer et à affecter au pool libre en attente de demandes d’appel. Le conteneur du service peut alors répondre immédiatement aux demandes d’appel sans initialisation préalable d’une instance de service.
1. Dans le champ Taille maximale du pool d’instances de service, indiquez le nombre maximal d’instances autorisées dans le pool pour un service donné. Ce paramètre contrôle le nombre de threads susceptibles d’exécuter un service à un moment donné. La valeur par défaut est 0 ; elle autorise une taille illimitée pour le pool.
1. Dans le champ Instances maximales des services asynchrones, indiquez le nombre maximal d’instances du pool qui peuvent être utilisées pour répondre aux demandes asynchrones à un moment donné. Ce paramètre permet au service de limiter le nombre de demandes traitées en parallèle.
1. Dans le champ Délai d’attente d’appel, saisissez le délai (en millisecondes) d’attente pour qu’un service soit disponible pour une demande d’appel. Si vous ne définissez aucune valeur pour ce paramètre, la valeur par défaut est 0, autrement dit, aucun délai d’attente.
1. Cliquez sur Enregistrer.

### Suppression du pool  {#remove-pooling}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Cliquez sur l’onglet Mise en pool.
1. Dans la liste Stratégie de traitement de requête, sélectionnez Nouvelle instance pour chaque requête ou Instance unique pour toutes les requêtes.

   **Instance unique pour toutes les requêtes :**  une instance de service est créée et mise en cache lorsque la première requête entre dans le conteneur. Chaque requête suivant cette demande utilise la même instance de service pour gérer la demande.

   **Nouvelle instance pour chaque requête :** une nouvelle instance de service est créée pour chaque appel reçu.

1. Cliquez sur Enregistrer.
