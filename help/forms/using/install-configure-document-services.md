---
title: Installer et configurer des services de document
description: Installez les services de documents d’AEM Forms pour créer, assembler, publier, archiver des documents PDF, ajouter des signatures numériques afin de limiter l’accès aux documents et de décoder les formulaires Barcoded Forms.
topic-tags: installing
role: Admin, Developer
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: c6d38c682dc45e3dcebef194b3b80510ab10f9e2
workflow-type: tm+mt
source-wordcount: '10086'
ht-degree: 99%

---

# Installer et configurer des services de document {#installing-and-configuring-document-services}

AEM Forms fournit un ensemble de services OSGi pour exécuter différentes opérations au niveau du document, par exemple, des services pour créer, assembler, publier et archiver des documents PDF, pour ajouter des signatures numériques afin de limiter l’accès aux documents et de décoder les formulaires Barcoded Forms. Ces services sont inclus dans le package du module complémentaire AEM Forms. Ces services sont collectivement désignés par services de document. Les services de document disponibles et leurs fonctionnalités principales sont les suivants :

* **Service Assembler :** permet de combiner, d’organiser et d’étendre vos documents aux formats PDF et XDP et d’obtenir des informations sur les documents PDF. Ce service permet également de convertir et de valider des documents PDF au format PDF/A standard, il convertit les formulaires PDF et XML aux formats PDF/A-1b, PDF/A-2b et PDFA/A-3b. Pour plus d’informations, consultez la section [Service Assembler](/help/forms/using/assembler-service.md).

* **Service ConvertPDF :** permet de convertir des documents PDF en fichiers PostScript ou en images (aux formats JPEG, JPEG 2000, PNG et TIFF). Pour plus d’informations, consultez la section [Service ConvertPDF](/help/forms/using/using-convertpdf-service.md).

* **Service Barcoded Forms :** permet d’extraire des données depuis des images électroniques de code-barres. Il accepte en entrée des fichiers PDF et TIFF qui contiennent un ou plusieurs codes à barres et extrait les données de code à barres. Pour plus d’informations, consultez la section [Service Barcoded Forms](/help/forms/using/using-barcoded-forms-service.md).

* **Service DocAssurance :** permet de chiffrer et de déchiffrer des documents, d’ajouter des droits d’utilisation aux fonctionnalités d’Adobe Reader ou encore d’ajouter des signatures numériques à vos documents. Le service Doc Assurance se compose en fait de trois services : Signature, Encryption et Reader Extensions. Pour plus d’informations, consultez la section [Service DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Service Encryption :** permet de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Un utilisateur ou une utilisatrice autorisé(e) peut déchiffrer le document pour pouvoir accéder à son contenu. Pour plus d’informations, consultez la section [Service Encryption](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Service Forms :** permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans Forms Designer. Le service Forms restitue sous forme de documents PDF tout type de formulaire que vous créez. Pour plus d’informations, consultez la section [Service Forms](/help/forms/using/forms-service.md).

* **Service Output :** permet de créer des documents dans différents formats, y compris PDF et les formats d’imprimantes laser et d’imprimantes d’étiquettes. Les formats d’imprimantes laser sont les suivants : PostScript et PCL (Printer Control Language). Pour plus d’informations, consultez la section [Service Output](/help/forms/using/output-service.md).

* **Service PDF Generator :** fournit des API pour convertir des formats de fichier natifs en PDF. Il convertit également des fichiers PDF en d’autres formats et optimise la taille des documents PDF. Pour plus d’informations, consultez la section [Service PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Service Reader Extension :** permet à votre organisation de partager facilement des documents PDF interactifs en ajoutant des droits dʼutilisation aux fonctionnalités dʼAdobe Reader. Ce service active des fonctionnalités indisponibles à l’ouverture d’un document PDF dans Adobe Reader, comme l’ajout de commentaires dans un document, le remplissage de formulaires et l’enregistrement du document. Pour plus d’informations, consultez la section [Service Reader Extensions](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Service Signature :** permet d’utiliser des documents et des signatures numériques sur le serveur AEM. Par exemple, le service Signature est généralement utilisé dans les situations suivantes :

   * Le serveur AEM certifie un formulaire avant que ce dernier ne soit envoyé à un utilisateur ou une utilisatrice et ouvert avec Acrobat ou Adobe Reader.
   * Le serveur AEM valide la signature apposée sur un formulaire via Acrobat ou Adobe Reader.
   * Le serveur AEM signe un formulaire au nom d’un notaire.

  Le service Signature accède aux certificats et aux informations d’identification stockées dans le Trust Store. Pour plus d’informations, consultez la section [Service Signature](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms est une plateforme d’entreprise performante et les services de documents ne sont quʼune des fonctionnalités proposées. Pour obtenir la liste complète des fonctionnalités, voir [Présentation d’AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologie de déploiement {#deployment-topology}

Le module complémentaire AEM Forms est une application déployée sur AEM. En général, une seule instance AEM (de création ou de publication) suffit pour exécuter les services de document AEM Forms. La topologie suivante est recommandée pour exécuter les services de document d’AEM Forms. Pour plus d’informations sur les topologies, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Topologies d’architecture et de déploiement pour AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités à partir d’un seul serveur, vous devez planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement utilisant le service PDF Generator pour convertir des milliers de pages par jour et plusieurs formulaires adaptatifs pour capturer des données, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de formulaires adaptatifs. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

## Configuration requise {#system-requirements}

Avant de commencer à installer et à configurer les services de document AEM Forms, assurez-vous que :

* Le matériel et l’infrastructure logicielle sont en place. Pour obtenir une liste détaillée des matériels et logiciels pris en charge, voir [Conditions techniques applicables](/help/sites-deploying/technical-requirements.md).

* Le chemin d’installation de l’instance AEM ne contient pas d’espaces.
* Une instance AEM est en cours d’exécution. Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur en mode de création ou de publication. En général, une seule instance AEM (création ou publication) suffit pour exécuter les services de document AEM Forms :

   * **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
   * **Publication** : une instance AEM qui diffuse le contenu publié au public sur Internet ou sur un réseau interne.

* Les exigences de mémoire sont respectées. Le package complémentaire AEM Forms nécessite :

   * 15 Go d’espace temporaire pour les installations Microsoft® Windows.
   * 6 Go d’espace temporaire pour les installations Unix.

* Les logiciels client requis pour que PDF Generator effectue la conversion sous Microsoft® Windows et Linux® sont installés :

   * **Microsoft® Windows** : installez [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) ou [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator).
   * **Linux®** : installez [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p).

>[!NOTE]
>
>* Sous Microsoft® Windows, PDF Generator prend en charge les itinéraires de conversion WebKit, Acrobat WebCapture et WebToPDF pour convertir des fichiers HTML en documents PDF.
>* Sur les systèmes dʼexploitation UNIX, PDF Generator prend en charge les itinéraires de conversion WebKit et WebToPDF pour convertir des fichiers HTML en documents PDF.
>

### Exigences supplémentaires pour les systèmes d’exploitation UNIX {#extrarequirements}

Si vous utilisez un système d’exploitation UNIX, installez les packages 32 bits suivants à partir des supports d’installation du système d’exploitation correspondant :
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expat</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(PDF Generator uniquement**) Installez la version 32 bits des bibliothèques libcurl, libcrypto et libssl et créez les liens symboliques ci-dessous. Les liens symboliques pointent vers la dernière version des bibliothèques respectives :

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(PDF Generator uniquement)** Le service PDF Generator prend en charge les itinéraires WebKit et WebToPDF pour convertir des fichiers HTML en documents PDF. Pour activer la conversion pour l’itinéraire WebToPDF, installez les bibliothèques 64 bits répertoriées ci-dessous. Ces bibliothèques sont généralement déjà installées. Si une bibliothèque est manquante, installez-la manuellement :

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1
* (PDF Generator uniquement) Pour activer l’itinéraire WebKit sur les configurations RHEL 8 ou RHEL 9, SLES15, la bibliothèque `nspr` 32 bits peut ne pas être disponible par défaut ; installez-la si elle n’est pas présente.

* (PDF Generator uniquement) Si la conversion WebToPDF échoue sur le serveur Unix® avec l’erreur suivante :

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
définissez ensuite la variable d’environnement suivante et redémarrez le serveur :
  `OPENSSL_CONF=/etc/ssl`

>[!NOTE]
>
> La fonctionnalité de graphique utilise également WebToPDF dans les communications interactives. Par conséquent, il est nécessaire de suivre les étapes de configuration de WebToPDF décrites ci-dessus afin de s’assurer que la fonctionnalité de graphique fonctionne correctement.

## Configurations de pré-installation {#preinstallationconfigurations}

Les configurations répertoriées dans la section Configurations de pré-installation s’appliquent uniquement au service PDF Generator. Si vous ne configurez pas le service PDF Generator, vous pouvez ignorer la section Configurations de pré-installation.

### Installation d’Adobe Acrobat et d’applications tierces {#install-adobe-acrobat-and-third-party-applications}

Si vous prévoyez d’utiliser le service PDF Generator pour convertir des formats de fichiers natifs tels que Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice et Adobe Acrobat en documents PDF, assurez-vous que ces applications sont installées sur le serveur AEM Forms.

>[!NOTE]
>
><!-- * If your AEM Forms Server is in an offline or secure environment and internet is not available to activate Adobe Acrobat, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) for instructions to activate such instances of Adobe Acrobat. -->
>* Adobe Acrobat, Microsoft® Word, Excel et PowerPoint sont disponibles uniquement pour Microsoft® Windows. Si vous utilisez le système d’exploitation UNIX, installez OpenOffice pour convertir les fichiers de texte enrichi et les fichiers Microsoft® Office pris en charge en documents PDF.
>* Fermez toutes les boîtes de dialogue qui s’affichent après l’installation d’Adobe Acrobat et d’un logiciel tiers pour tous les utilisateurs configurés pour utiliser le service PDF Generator.
>* Démarrez tous les logiciels installés au moins une fois. Fermez toutes les boîtes de dialogue pour tous les utilisateurs configurés pour utiliser le service PDF Generator.
>* [Vérifiez la date d’expiration de vos numéros de série Adobe Acrobat](https://helpx.adobe.com/fr/enterprise/kb/volume-license-expiration-check.html) et définissez une date pour mettre à jour la licence ou [migrez votre numéro de série](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) selon la date d’expiration.

### Installer Adobe Acrobat Pro DC

#### Prérequis

Avant d’installer Acrobat, passez en revue ces exigences essentielles. Prérequis :

* Familiarité avec [Adobe Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html)
* Compréhension de votre [architecture de déploiement AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)
* Privilèges d’administration sur Adobe Admin Console et le serveur exécutant AEM Forms.
* Personne disposant d’un [accès d’administration](https://helpx.adobe.com/in/enterprise/using/admin-roles.html) à Adobe [Admin Console](https://adminconsole.adobe.com). En règle générale, l’administration de votre entreprise dispose déjà d’un compte avec un accès d’administration. Vous pouvez regarder cette [vidéo d’instruction](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) pour savoir comment ajouter un administrateur ou une administratrice.
* Compte d’utilisation doté du rôle [Administration de déploiement](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) dans Adobe Admin Console. La même [vidéo d’instruction](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) montre comment ajouter un administrateur ou une administratrice de déploiement.
* Privilèges d’administration locale sur la machine exécutant AEM Forms
* Système d’exploitation Windows 64 bits
* Connexion Internet stable pour l’activation des licences
<!-- Backup solution for existing Acrobat settings
 Supported version of Adobe Acrobat (see [Adobe documentation](https://helpx.adobe.com/acrobat/kb/acrobat-dc-compatibility-with-windows-macos.html) for details) -->


#### Workflow et chronologie d’implémentation

Le processus complet prend généralement 1 à 2 heures, selon votre environnement :

| Étape | Temps estimé | Prérequis |
|------|----------------|---------------|
| &#x200B;1. Créer le package FRL dans Admin Console | 15 à 20 minutes | [Vue d’ensemble d’Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html) |
| &#x200B;2. Octroyer des autorisations de téléchargement | 5 à 10 minutes | [Vue d’ensemble d’Admin Console](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) |
| &#x200B;3. Désinstaller la version précédente d’Acrobat | 10 à 15 minutes | Accès de l’administration du serveur |
| &#x200B;4. Télécharger et installer Adobe Acrobat Pro | 10 à 15 minutes | Accès de l’administration du serveur |
| &#x200B;5. Télécharger et déployer le package FRL | 20 à 30 minutes | Accès de l’administration du serveur |
| &#x200B;6. Vérifier l’installation | 5 à 10 minutes | Accès au serveur |

<!-- ![Workflow diagram showing the FRL implementation process](/help/forms/using/assets/frl.svg) -->

**Choisir votre chemin d’installation**

Le processus d’installation d’Adobe Acrobat Pro DC pour l’installation de Microsoft Office varie légèrement en fonction du type de licence et du scénario de déploiement. Pour vous assurer de suivre les étapes appropriées pour votre environnement spécifique, sélectionnez l’onglet correspondant à votre configuration :

* **Type de licence** : licence au détail ou en volume
* **Type de déploiement** : utilisation unique ou utilisations multiples

Chaque onglet contient des instructions personnalisées optimisées pour votre configuration spécifique, ce qui vous permet d’éviter les problèmes de configuration et d’assurer une conformité de licence appropriée.

>[!VIDEO](https://video.tv.adobe.com/v/3469669)

>[!NOTE]
>
>La vidéo présente le processus d’installation d’une configuration Licence au détail - Utilisation unique. Pour les autres scénarios de déploiement (Au détail - Utilisations multiples, En volume - Utilisation unique ou en volume - Utilisations multiples), reportez-vous aux instructions spécifiques de l’étape 9 dans les onglets correspondants ci-dessous pour garantir le démarrage correct du serveur et l’activation de la licence pour votre type de déploiement.

>[!BEGINTABS]

>[!TAB Licence au détail - Utilisation unique]

#### Configuration de la gestion des licences avec restrictions de fonctionnalités (FRL) pour Adobe Acrobat sur votre serveur AEM Forms

Ces étapes supposent que vous disposiez des privilèges d’administration nécessaires sur Adobe Admin Console et le serveur exécutant AEM Forms.

##### Préparation du package FRL (Adobe Admin Console)

Ces étapes doivent être effectuées avec un accès d’*administration système* à Adobe Admin Console.

###### Étape 1 : se connecter à Adobe Admin Console

1. Ouvrez un navigateur web et accédez à [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Connectez-vous à l’aide d’un compte avec des privilèges d’*administration système*.
1. (Facultatif) Si votre organisation a accès à plusieurs organisations IMS, utilisez l’option de sélection d’organisation dans le coin supérieur droit d’Admin Console pour choisir l’organisation appropriée. Dans la plupart des scénarios client, cette valeur est déjà définie sur la valeur par défaut de votre organisation, car les personnes n’ont généralement accès qu’à leur propre organisation.

###### Étape 1 : créer le package FRL

1. Dans Admin Console, accédez à l’onglet Package. Il s’agit d’un package Adobe Admin Console, et non d’un package AEM.
1. Sélectionnez la vignette **Licence avec fonctionnalités restreintes** et cliquez sur le bouton **Commencer**. Assurez-vous de sélectionner le type de licence approprié.
1. Sur l’écran **Créer un package**, configurez les paramètres du package :

   | Configuration | Valeur recommandée | Remarques |
   |---------|-------------------|-------|
   | Méthode d’activation | Hors ligne | Option recommandée |
   | Droit | Génération de PDF (PDFG) | Conditions requises pour AEM Forms PDF Generator |
   | Configurer la plateforme | Windows 64 bits | Apple macOS n’est actuellement pas pris en charge. |
   | Activer le mode local | « Utiliser la langue du SE » | Paramètre par défaut |
   | Langue | Votre langue préférée | Pour l’interface Acrobat |
   | Choisir les applications - applications disponibles | Conservez Adobe Acrobat dans les applications disponibles. Ne pas déplacer vers l’application sélectionnée | Téléchargez [Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) à partir de la page Adobe Experience League à l’Étape 6. |
   | Choisir les applications - applications sélectionnées | Conserver uniquement le fichier de licence dans les applications sélectionnées | Paramètre par défaut pour le déploiement FRL |
   | Modules externes | Ne pas apporter de modifications sur cet écran | |
   | Options | Ne pas apporter de modifications sur cet écran | |
   | Finaliser | Nom du package : « Acrobat FRL AEM Forms » | Utiliser un nom explicite |

1. Cliquez sur **Créer** pour créer le package.

###### Étape 3 : accorder des autorisations de téléchargement à une personne

Il est recommandé de créer un compte de service dédié pour gérer les packages FRL. Si vous ne disposez pas déjà d’un compte dédié, vous pouvez suivre [cette vidéo d’instructions](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) pour apprendre à ajouter une personne à votre organisation Adobe.

Une fois que vous disposez du compte approprié, procédez comme suit pour accorder des autorisations de téléchargement :

1. Dans Admin Console, accédez à l’onglet **Utilisateurs et utilisatrices**.
2. Recherchez ou créez un compte d’utilisation pour accorder des autorisations de téléchargement.
3. Cliquez sur le nom de la personne pour ouvrir son profil.
4. Cliquez sur l’icône en regard de **Modifier les droits d’administration** correspondant à la personne.
5. Attribuez le rôle **Administration de déploiement** à la personne. D’autres rôles d’administration peuvent également fonctionner, mais le rôle Administration de déploiement est recommandé. Cliquez sur **Enregistrer**.


##### Déployer le package FRL (serveur AEM Forms)

Les étapes suivantes sont effectuées sur le serveur AEM Forms, avec les droits d’*administration locale* sur la machine.

###### Étape 4 : se connecter au serveur exécutant AEM Forms en tant qu’administrateur ou administratrice

Accédez au serveur exécutant AEM Forms à l’aide de la méthode appropriée. Assurez-vous d’utiliser un compte disposant des privilèges d’administration locale pour accéder au serveur.

###### Étape 5 : désinstaller la version précédente d’Acrobat (le cas échéant)

**Important :** sauvegardez tous les paramètres, profils ou configurations Acrobat personnalisés avant de procéder à la désinstallation.

1. Ouvrez le Panneau de Contrôle Windows.
2. Accédez à **Paramètres** et ouvrez **Applications**.
3. Localisez **Adobe Acrobat** dans la liste des programmes installés.
4. Sélectionnez **Désinstaller** et suivez les invites pour supprimer l’application. Le cas échéant, redémarrez le serveur.
5. Vérifiez que toutes les versions Classic du programme sont désinstallées. Utilisez l’[outil Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) si nécessaire pour en effectuer la suppression complète.

###### Étape 6 : télécharger et installer Adobe Acrobat Pro

Après avoir désinstallé la version précédente, vous devez télécharger et installer une version compatible d’Adobe Acrobat Pro :

1. Accédez à la page [Téléchargements Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Accédez à la section **Programme d’installation d’Acrobat Pro**.
3. Pour une utilisation avec AEM Forms PDF Generator, téléchargez le programme d’installation « Pour Windows (32 bits) », car il s’agit de la version prise en charge avec AEM Forms PDF Generator.
4. Suivez ensuite les instructions d’installation fournies dans cette page :
   * Procédez à l’extraction du fichier .zip téléchargé dans un répertoire de votre ordinateur.
   * Accédez au fichier Setup.exe (n’exécutez pas le fichier Setup.exe à partir du fichier .zip).
   * Double-cliquez sur Setup.exe pour démarrer l’installation.
   * Suivez les instructions à l’écran pour terminer l’installation.
5. Après l’installation, ouvrez Adobe Acrobat Pro et terminez la configuration initiale en fermant toutes les boîtes de dialogue de bienvenue.
6. Vérifiez l’installation en créant un PDF simple.

###### Étape 7 : télécharger le package FRL

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) à l’aide du *compte d’utilisation* auquel vous avez fourni des autorisations de téléchargement à l’Étape 3.
1. Accédez à l’onglet **Packages**.
1. Recherchez le package FRL que vous avez créé à l’Étape 2 (nommé « Acrobat FRL AEM Forms » ou votre nom de package personnalisé).
1. Cliquez sur **Télécharger** pour télécharger le package sur le serveur.

###### Étape 8 : déployer le package

1. **Extraire le package :** extrayez le contenu du fichier .zip téléchargé dans un répertoire du serveur (par exemple, `C:\AcrobatFRL`). Assurez-vous que le répertoire d’extraction est facilement accessible.

2. **Ouvrir l’invite de commandes en tant qu’administrateur ou administratrice (Windows) :** cliquez avec le bouton droit sur le bouton Démarrer et sélectionnez « Invite de commandes (Admin) » ou « Windows PowerShell (Admin) ».

3. **Accédez au répertoire Extraction :**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Exécutez la commande Activation :**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Important :**
   > * Remplacez `<JSON_FILE_NAME>.json` par le nom de fichier *exact* du fichier JSON dans le package extrait.
   > * Le nom de fichier JSON est sensible à la casse.
   > * Vérifiez deux fois le nom du fichier pour détecter les fautes de frappe.

   **Sortie attendue :**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ **Remarque :** le processus d’activation peut prendre environ 30 secondes.

5. **Présentation des paramètres de commande :**

   | Paramètre | Description |
   |-----------|-------------|
   | `-p` | Spécifie la plateforme (détecte automatiquement le système d’exploitation). |
   | `-i` | Indique à l’outil d’installer et d’activer la licence. |
   | `-f` | Indique le chemin d’accès au fichier de licence JSON. |

###### Étape 9 : tester le service PDF Generator

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Ouvrez l’interface d’administration d’AEM Forms.
2. Accédez au service PDF Generator.
3. Essayez de convertir un document Microsoft Office simple en PDF.
4. Vérifiez que la conversion est correcte.

#### Vérifiez la version d’Acrobat après l’activation de FRL.

1. Ouvrez Adobe Acrobat Pro DC sur le serveur.
2. Accédez à l’Aide → À propos d’Adobe Acrobat Pro DC.
3. Vérifiez que le numéro de version correspond à la version attendue.
4. Confirmez que le statut de licence s’affiche comme étant activé.

>[!TAB Licence au détail - Plusieurs utilisateurs et utilisatrices]

#### Configuration de la gestion des licences avec restrictions de fonctionnalités (FRL) pour Adobe Acrobat sur votre serveur AEM Forms

Ces étapes supposent que vous disposiez des privilèges d’administration nécessaires sur Adobe Admin Console et le serveur exécutant AEM Forms.

##### Préparation du package FRL (Adobe Admin Console)

Ces étapes doivent être effectuées avec un accès d’*administration système* à Adobe Admin Console.

###### Étape 1 : se connecter à Adobe Admin Console

1. Ouvrez un navigateur web et accédez à [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Connectez-vous à l’aide d’un compte avec des privilèges d’*administration système*.
1. (Facultatif) Si votre organisation a accès à plusieurs organisations IMS, utilisez l’option de sélection d’organisation dans le coin supérieur droit d’Admin Console pour choisir l’organisation appropriée. Dans la plupart des scénarios client, cette valeur est déjà définie sur la valeur par défaut de votre organisation, car les personnes n’ont généralement accès qu’à leur propre organisation.

###### Étape 1 : créer le package FRL

1. Dans Admin Console, accédez à l’onglet Package. Il s’agit d’un package Adobe Admin Console, et non d’un package AEM.
1. Sélectionnez la vignette **Licence avec fonctionnalités restreintes** et cliquez sur le bouton **Commencer**. Assurez-vous de sélectionner le type de licence approprié.
1. Sur l’écran **Créer un package**, configurez les paramètres du package :

   | Configuration | Valeur recommandée | Remarques |
   |---------|-------------------|-------|
   | Méthode d’activation | Hors ligne | Option recommandée |
   | Droit | Génération de PDF (PDFG) | Conditions requises pour AEM Forms PDF Generator |
   | Configurer la plateforme | Windows 64 bits | Apple macOS n’est actuellement pas pris en charge. |
   | Activer le mode local | « Utiliser la langue du SE » | Paramètre par défaut |
   | Langue | Votre langue préférée | Pour l’interface Acrobat |
   | Choisir les applications - applications disponibles | Conservez Adobe Acrobat dans les applications disponibles. Ne pas déplacer vers l’application sélectionnée | Téléchargez [Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) à partir de la page Adobe Experience League à l’Étape 6. |
   | Choisir les applications - applications sélectionnées | Conserver uniquement le fichier de licence dans les applications sélectionnées | Paramètre par défaut pour le déploiement FRL |
   | Modules externes | Ne pas apporter de modifications sur cet écran | |
   | Options | Ne pas apporter de modifications sur cet écran | |
   | Finaliser | Nom du package : « Acrobat FRL AEM Forms » | Utiliser un nom explicite |

1. Cliquez sur **Créer** pour créer le package.

###### Étape 3 : accorder des autorisations de téléchargement à une personne

Il est recommandé de créer un compte de service dédié pour gérer les packages FRL. Si vous ne disposez pas déjà d’un compte dédié, vous pouvez suivre [cette vidéo d’instructions](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) pour apprendre à ajouter une personne à votre organisation Adobe.

Une fois que vous disposez du compte approprié, procédez comme suit pour accorder des autorisations de téléchargement :

1. Dans Admin Console, accédez à l’onglet **Utilisateurs et utilisatrices**.
2. Recherchez ou créez un compte d’utilisation pour accorder des autorisations de téléchargement.
3. Cliquez sur le nom de la personne pour ouvrir son profil.
4. Cliquez sur l’icône en regard de **Modifier les droits d’administration** correspondant à la personne.
5. Attribuez le rôle **Administration de déploiement** à la personne. D’autres rôles d’administration peuvent également fonctionner, mais le rôle Administration de déploiement est recommandé. Cliquez sur **Enregistrer**.


##### Déployer le package FRL (serveur AEM Forms)

Les étapes suivantes sont effectuées sur le serveur AEM Forms, avec les droits d’*administration locale* sur la machine.

###### Étape 4 : se connecter au serveur exécutant AEM Forms en tant qu’administrateur ou administratrice

Accédez au serveur exécutant AEM Forms à l’aide de la méthode appropriée. Assurez-vous d’utiliser un compte disposant des privilèges d’administration locale pour accéder au serveur.

###### Étape 5 : désinstaller la version précédente d’Acrobat (le cas échéant)

**Important :** sauvegardez tous les paramètres, profils ou configurations Acrobat personnalisés avant de procéder à la désinstallation.

1. Ouvrez le Panneau de Contrôle Windows.
2. Accédez à **Paramètres** et ouvrez **Applications**.
3. Localisez **Adobe Acrobat** dans la liste des programmes installés.
4. Sélectionnez **Désinstaller** et suivez les invites pour supprimer l’application. Le cas échéant, redémarrez le serveur.
5. Vérifiez que toutes les versions Classic du programme sont désinstallées. Utilisez l’[outil Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) si nécessaire pour en effectuer la suppression complète.

###### Étape 6 : télécharger et installer Adobe Acrobat Pro

Après avoir désinstallé la version précédente, vous devez télécharger et installer une version compatible d’Adobe Acrobat Pro :

1. Accédez à la page [Téléchargements Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Accédez à la section **Programme d’installation d’Acrobat Pro**.
3. Pour une utilisation avec AEM Forms PDF Generator, téléchargez le programme d’installation « Pour Windows (32 bits) », car il s’agit de la version prise en charge avec AEM Forms PDF Generator.
4. Suivez ensuite les instructions d’installation fournies dans cette page :
   * Procédez à l’extraction du fichier .zip téléchargé dans un répertoire de votre ordinateur.
   * Accédez au fichier Setup.exe (n’exécutez pas le fichier Setup.exe à partir du fichier .zip).
   * Double-cliquez sur Setup.exe pour démarrer l’installation.
   * Suivez les instructions à l’écran pour terminer l’installation.
5. Après l’installation, ouvrez Adobe Acrobat Pro et terminez la configuration initiale en fermant toutes les boîtes de dialogue de bienvenue.
6. Vérifiez l’installation en créant un PDF simple.

###### Étape 7 : télécharger le package FRL

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) à l’aide du *compte d’utilisation* auquel vous avez fourni des autorisations de téléchargement à l’Étape 3.
1. Accédez à l’onglet **Packages**.
1. Recherchez le package FRL que vous avez créé à l’Étape 2 (nommé « Acrobat FRL AEM Forms » ou votre nom de package personnalisé).
1. Cliquez sur **Télécharger** pour télécharger le package sur le serveur.

###### Étape 8 : déployer le package

1. **Extraire le package :** extrayez le contenu du fichier .zip téléchargé dans un répertoire du serveur (par exemple, `C:\AcrobatFRL`). Assurez-vous que le répertoire d’extraction est facilement accessible.

2. **Ouvrir l’invite de commandes en tant qu’administrateur ou administratrice (Windows) :** cliquez avec le bouton droit sur le bouton Démarrer et sélectionnez « Invite de commandes (Admin) » ou « Windows PowerShell (Admin) ».

3. **Accédez au répertoire Extraction :**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Exécutez la commande Activation :**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Important :**
   > * Remplacez `<JSON_FILE_NAME>.json` par le nom de fichier *exact* du fichier JSON dans le package extrait.
   > * Le nom de fichier JSON est sensible à la casse.
   > * Vérifiez deux fois le nom du fichier pour détecter les fautes de frappe.

   **Sortie attendue :**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ **Remarque :** le processus d’activation peut prendre environ 30 secondes.

5. **Présentation des paramètres de commande :**

   | Paramètre | Description |
   |-----------|-------------|
   | `-p` | Spécifie la plateforme (détecte automatiquement le système d’exploitation). |
   | `-i` | Indique à l’outil d’installer et d’activer la licence. |
   | `-f` | Indique le chemin d’accès au fichier de licence JSON. |

###### Étape 9 : démarrer le serveur AEM Forms

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Démarrez le serveur AEM Forms à partir d’une console de ligne de commande dans une session d’utilisation interactive. (Connectez-vous au serveur et lancez manuellement AEM Forms à partir de la ligne de commande.)
2. Gardez la session d’utilisation active après le démarrage du serveur. Ne vous déconnectez pas de l’ordinateur, car cela mettrait fin au processus du serveur. Vous pouvez fermer en toute sécurité la fenêtre Bureau à distance (RDP) sans vous déconnecter ; le serveur continue à fonctionner tant que la session reste active.
3. Pour une meilleure fiabilité, configurez une tâche de démarrage ou une tâche planifiée pour lancer automatiquement le serveur AEM Forms lorsque la personne se connecte.

###### Étape 10 : tester le service PDF Generator

1. Ouvrez l’interface d’administration d’AEM Forms.
2. Accédez au service PDF Generator.
3. Essayez de convertir un document Microsoft Office simple en PDF.
4. Vérifiez que la conversion est correcte.

#### Vérifiez la version d’Acrobat après l’activation de FRL.

1. Ouvrez Adobe Acrobat Pro DC sur le serveur.
2. Accédez à l’Aide → À propos d’Adobe Acrobat Pro DC.
3. Vérifiez que le numéro de version correspond à la version attendue.
4. Confirmez que le statut de licence s’affiche comme étant activé.

>[!TAB Licence en volume - Utilisation unique]

#### Configuration de la gestion des licences avec restrictions de fonctionnalités (FRL) pour Adobe Acrobat sur votre serveur AEM Forms

Ces étapes supposent que vous disposiez des privilèges d’administration nécessaires sur Adobe Admin Console et le serveur exécutant AEM Forms.

##### Préparation du package FRL (Adobe Admin Console)

Ces étapes doivent être effectuées avec un accès d’*administration système* à Adobe Admin Console.

###### Étape 1 : se connecter à Adobe Admin Console

1. Ouvrez un navigateur web et accédez à [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Connectez-vous à l’aide d’un compte avec des privilèges d’*administration système*.
1. (Facultatif) Si votre organisation a accès à plusieurs organisations IMS, utilisez l’option de sélection d’organisation dans le coin supérieur droit d’Admin Console pour choisir l’organisation appropriée. Dans la plupart des scénarios client, cette valeur est déjà définie sur la valeur par défaut de votre organisation, car les personnes n’ont généralement accès qu’à leur propre organisation.

###### Étape 1 : créer le package FRL

1. Dans Admin Console, accédez à l’onglet Package. Il s’agit d’un package Adobe Admin Console, et non d’un package AEM.
1. Sélectionnez la vignette **Licence avec fonctionnalités restreintes** et cliquez sur le bouton **Commencer**. Assurez-vous de sélectionner le type de licence approprié.
1. Sur l’écran **Créer un package**, configurez les paramètres du package :

   | Configuration | Valeur recommandée | Remarques |
   |---------|-------------------|-------|
   | Méthode d’activation | Hors ligne | Option recommandée |
   | Droit | Génération de PDF (PDFG) | Conditions requises pour AEM Forms PDF Generator |
   | Configurer la plateforme | Windows 64 bits | Apple macOS n’est actuellement pas pris en charge. |
   | Activer le mode local | « Utiliser la langue du SE » | Paramètre par défaut |
   | Langue | Votre langue préférée | Pour l’interface Acrobat |
   | Choisir les applications - applications disponibles | Conservez Adobe Acrobat dans les applications disponibles. Ne pas déplacer vers l’application sélectionnée | Téléchargez [Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) à partir de la page Adobe Experience League à l’Étape 6. |
   | Choisir les applications - applications sélectionnées | Conserver uniquement le fichier de licence dans les applications sélectionnées | Paramètre par défaut pour le déploiement FRL |
   | Modules externes | Ne pas apporter de modifications sur cet écran | |
   | Options | Ne pas apporter de modifications sur cet écran | |
   | Finaliser | Nom du package : « Acrobat FRL AEM Forms » | Utiliser un nom explicite |

1. Cliquez sur **Créer** pour créer le package.

###### Étape 3 : accorder des autorisations de téléchargement à une personne

Il est recommandé de créer un compte de service dédié pour gérer les packages FRL. Si vous ne disposez pas déjà d’un compte dédié, vous pouvez suivre [cette vidéo d’instructions](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) pour apprendre à ajouter une personne à votre organisation Adobe.

Une fois que vous disposez du compte approprié, procédez comme suit pour accorder des autorisations de téléchargement :

1. Dans Admin Console, accédez à l’onglet **Utilisateurs et utilisatrices**.
2. Recherchez ou créez un compte d’utilisation pour accorder des autorisations de téléchargement.
3. Cliquez sur le nom de la personne pour ouvrir son profil.
4. Cliquez sur l’icône en regard de **Modifier les droits d’administration** correspondant à la personne.
5. Attribuez le rôle **Administration de déploiement** à la personne. D’autres rôles d’administration peuvent également fonctionner, mais le rôle Administration de déploiement est recommandé. Cliquez sur **Enregistrer**.


##### Déployer le package FRL (serveur AEM Forms)

Les étapes suivantes sont effectuées sur le serveur AEM Forms, avec les droits d’*administration locale* sur la machine.

###### Étape 4 : se connecter au serveur exécutant AEM Forms en tant qu’administrateur ou administratrice

Accédez au serveur exécutant AEM Forms à l’aide de la méthode appropriée. Assurez-vous d’utiliser un compte disposant des privilèges d’administration locale pour accéder au serveur.

###### Étape 5 : désinstaller la version précédente d’Acrobat (le cas échéant)

**Important :** sauvegardez tous les paramètres, profils ou configurations Acrobat personnalisés avant de procéder à la désinstallation.

1. Ouvrez le Panneau de Contrôle Windows.
2. Accédez à **Paramètres** et ouvrez **Applications**.
3. Localisez **Adobe Acrobat** dans la liste des programmes installés.
4. Sélectionnez **Désinstaller** et suivez les invites pour supprimer l’application. Le cas échéant, redémarrez le serveur.
5. Vérifiez que toutes les versions Classic du programme sont désinstallées. Utilisez l’[outil Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) si nécessaire pour en effectuer la suppression complète.

###### Étape 6 : télécharger et installer Adobe Acrobat Pro

Après avoir désinstallé la version précédente, vous devez télécharger et installer une version compatible d’Adobe Acrobat Pro :

1. Accédez à la page [Téléchargements Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Accédez à la section **Programme d’installation d’Acrobat Pro**.
3. Pour une utilisation avec AEM Forms PDF Generator, téléchargez le programme d’installation « Pour Windows (32 bits) », car il s’agit de la version prise en charge avec AEM Forms PDF Generator.
4. Suivez ensuite les instructions d’installation fournies dans cette page :
   * Procédez à l’extraction du fichier .zip téléchargé dans un répertoire de votre ordinateur.
   * Accédez au fichier Setup.exe (n’exécutez pas le fichier Setup.exe à partir du fichier .zip).
   * Double-cliquez sur Setup.exe pour démarrer l’installation.
   * Suivez les instructions à l’écran pour terminer l’installation.
5. Après l’installation, ouvrez Adobe Acrobat Pro et terminez la configuration initiale en fermant toutes les boîtes de dialogue de bienvenue.
6. Vérifiez l’installation en créant un PDF simple.

###### Étape 7 : télécharger le package FRL

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) à l’aide du *compte d’utilisation* auquel vous avez fourni des autorisations de téléchargement à l’Étape 3.
1. Accédez à l’onglet **Packages**.
1. Recherchez le package FRL que vous avez créé à l’Étape 2 (nommé « Acrobat FRL AEM Forms » ou votre nom de package personnalisé).
1. Cliquez sur **Télécharger** pour télécharger le package sur le serveur.

###### Étape 8 : déployer le package

1. **Extraire le package :** extrayez le contenu du fichier .zip téléchargé dans un répertoire du serveur (par exemple, `C:\AcrobatFRL`). Assurez-vous que le répertoire d’extraction est facilement accessible.

2. **Ouvrir l’invite de commandes en tant qu’administrateur ou administratrice (Windows) :** cliquez avec le bouton droit sur le bouton Démarrer et sélectionnez « Invite de commandes (Admin) » ou « Windows PowerShell (Admin) ».

3. **Accédez au répertoire Extraction :**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Exécutez la commande Activation :**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Important :**
   > * Remplacez `<JSON_FILE_NAME>.json` par le nom de fichier *exact* du fichier JSON dans le package extrait.
   > * Le nom de fichier JSON est sensible à la casse.
   > * Vérifiez deux fois le nom du fichier pour détecter les fautes de frappe.

   **Sortie attendue :**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ **Remarque :** le processus d’activation peut prendre environ 30 secondes.

5. **Présentation des paramètres de commande :**

   | Paramètre | Description |
   |-----------|-------------|
   | `-p` | Spécifie la plateforme (détecte automatiquement le système d’exploitation). |
   | `-i` | Indique à l’outil d’installer et d’activer la licence. |
   | `-f` | Indique le chemin d’accès au fichier de licence JSON. |

###### Étape 9 : démarrer le serveur AEM Forms

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Utilisez le Bureau à distance (RDP) pour vous connecter au serveur et démarrer le serveur AEM Forms à l’aide des services.
2. Une fois le serveur en cours d’exécution, ne fermez pas la fenêtre RDP. Au lieu de cela, déconnectez-vous en déconnectant la personne, de sorte que la session se termine correctement pendant que le service continue à s’exécuter en arrière-plan.

###### Étape 10 : tester le service PDF Generator

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Ouvrez l’interface d’administration d’AEM Forms.
2. Accédez au service PDF Generator.
3. Essayez de convertir un document Microsoft Office simple en PDF.
4. Vérifiez que la conversion est correcte.

###### Étape 11 : vérifier la version d’Acrobat après l’activation de FRL

1. Ouvrez Adobe Acrobat Pro DC sur le serveur.
2. Accédez à l’Aide → À propos d’Adobe Acrobat Pro DC.
3. Vérifiez que le numéro de version correspond à la version attendue.
4. Confirmez que le statut de licence s’affiche comme étant activé.

>[!TAB Licence en volume - Utilisations multiples]

#### Configuration de la gestion des licences avec restrictions de fonctionnalités (FRL) pour Adobe Acrobat sur votre serveur AEM Forms

Ces étapes supposent que vous disposiez des privilèges d’administration nécessaires sur Adobe Admin Console et le serveur exécutant AEM Forms.

##### Préparation du package FRL (Adobe Admin Console)

Ces étapes doivent être effectuées avec un accès d’*administration système* à Adobe Admin Console.

###### Étape 1 : se connecter à Adobe Admin Console

1. Ouvrez un navigateur web et accédez à [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Connectez-vous à l’aide d’un compte avec des privilèges d’*administration système*.
1. (Facultatif) Si votre organisation a accès à plusieurs organisations IMS, utilisez l’option de sélection d’organisation dans le coin supérieur droit d’Admin Console pour choisir l’organisation appropriée. Dans la plupart des scénarios client, cette valeur est déjà définie sur la valeur par défaut de votre organisation, car les personnes n’ont généralement accès qu’à leur propre organisation.

###### Étape 1 : créer le package FRL

1. Dans Admin Console, accédez à l’onglet Package. Il s’agit d’un package Adobe Admin Console, et non d’un package AEM.
1. Sélectionnez la vignette **Licence avec fonctionnalités restreintes** et cliquez sur le bouton **Commencer**. Assurez-vous de sélectionner le type de licence approprié.
1. Sur l’écran **Créer un package**, configurez les paramètres du package :

   | Configuration | Valeur recommandée | Remarques |
   |---------|-------------------|-------|
   | Méthode d’activation | Hors ligne | Option recommandée |
   | Droit | Génération de PDF (PDFG) | Conditions requises pour AEM Forms PDF Generator |
   | Configurer la plateforme | Windows 64 bits | Apple macOS n’est actuellement pas pris en charge. |
   | Activer le mode local | « Utiliser la langue du SE » | Paramètre par défaut |
   | Langue | Votre langue préférée | Pour l’interface Acrobat |
   | Choisir les applications - applications disponibles | Conservez Adobe Acrobat dans les applications disponibles. Ne pas déplacer vers l’application sélectionnée | Téléchargez [Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) à partir de la page Adobe Experience League à l’Étape 6. |
   | Choisir les applications - applications sélectionnées | Conserver uniquement le fichier de licence dans les applications sélectionnées | Paramètre par défaut pour le déploiement FRL |
   | Modules externes | Ne pas apporter de modifications sur cet écran | |
   | Options | Ne pas apporter de modifications sur cet écran | |
   | Finaliser | Nom du package : « Acrobat FRL AEM Forms » | Utiliser un nom explicite |

1. Cliquez sur **Créer** pour créer le package.

###### Étape 3 : accorder des autorisations de téléchargement à une personne

Il est recommandé de créer un compte de service dédié pour gérer les packages FRL. Si vous ne disposez pas déjà d’un compte dédié, vous pouvez suivre [cette vidéo d’instructions](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) pour apprendre à ajouter une personne à votre organisation Adobe.

Une fois que vous disposez du compte approprié, procédez comme suit pour accorder des autorisations de téléchargement :

1. Dans Admin Console, accédez à l’onglet **Utilisateurs et utilisatrices**.
2. Recherchez ou créez un compte d’utilisation pour accorder des autorisations de téléchargement.
3. Cliquez sur le nom de la personne pour ouvrir son profil.
4. Cliquez sur l’icône en regard de **Modifier les droits d’administration** correspondant à la personne.
5. Attribuez le rôle **Administration de déploiement** à la personne. D’autres rôles d’administration peuvent également fonctionner, mais le rôle Administration de déploiement est recommandé. Cliquez sur **Enregistrer**.


##### Déployer le package FRL (serveur AEM Forms)

Les étapes suivantes sont effectuées sur le serveur AEM Forms, avec les droits d’*administration locale* sur la machine.

###### Étape 4 : se connecter au serveur exécutant AEM Forms en tant qu’administrateur ou administratrice

Accédez au serveur exécutant AEM Forms à l’aide de la méthode appropriée. Assurez-vous d’utiliser un compte disposant des privilèges d’administration locale pour accéder au serveur.

###### Étape 5 : désinstaller la version précédente d’Acrobat (le cas échéant)

**Important :** sauvegardez tous les paramètres, profils ou configurations Acrobat personnalisés avant de procéder à la désinstallation.

1. Ouvrez le Panneau de Contrôle Windows.
2. Accédez à **Paramètres** et ouvrez **Applications**.
3. Localisez **Adobe Acrobat** dans la liste des programmes installés.
4. Sélectionnez **Désinstaller** et suivez les invites pour supprimer l’application. Le cas échéant, redémarrez le serveur.
5. Vérifiez que toutes les versions Classic du programme sont désinstallées. Utilisez l’[outil Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) si nécessaire pour en effectuer la suppression complète.

###### Étape 6 : télécharger et installer Adobe Acrobat Pro

Après avoir désinstallé la version précédente, vous devez télécharger et installer une version compatible d’Adobe Acrobat Pro :

1. Accédez à la page [Téléchargements Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Accédez à la section **Programme d’installation d’Acrobat Pro**.
3. Pour une utilisation avec AEM Forms PDF Generator, téléchargez le programme d’installation « Pour Windows (32 bits) », car il s’agit de la version prise en charge avec AEM Forms PDF Generator.
4. Suivez ensuite les instructions d’installation fournies dans cette page :
   * Procédez à l’extraction du fichier .zip téléchargé dans un répertoire de votre ordinateur.
   * Accédez au fichier Setup.exe (n’exécutez pas le fichier Setup.exe à partir du fichier .zip).
   * Double-cliquez sur Setup.exe pour démarrer l’installation.
   * Suivez les instructions à l’écran pour terminer l’installation.
5. Après l’installation, ouvrez Adobe Acrobat Pro et terminez la configuration initiale en fermant toutes les boîtes de dialogue de bienvenue.
6. Vérifiez l’installation en créant un PDF simple.

###### Étape 7 : télécharger le package FRL

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) à l’aide du *compte d’utilisation* auquel vous avez fourni des autorisations de téléchargement à l’Étape 3.
1. Accédez à l’onglet **Packages**.
1. Recherchez le package FRL que vous avez créé à l’Étape 2 (nommé « Acrobat FRL AEM Forms » ou votre nom de package personnalisé).
1. Cliquez sur **Télécharger** pour télécharger le package sur le serveur.

###### Étape 8 : déployer le package

1. **Extraire le package :** extrayez le contenu du fichier .zip téléchargé dans un répertoire du serveur (par exemple, `C:\AcrobatFRL`). Assurez-vous que le répertoire d’extraction est facilement accessible.

2. **Ouvrir l’invite de commandes en tant qu’administrateur ou administratrice (Windows) :** cliquez avec le bouton droit sur le bouton Démarrer et sélectionnez « Invite de commandes (Admin) » ou « Windows PowerShell (Admin) ».

3. **Accédez au répertoire Extraction :**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Exécutez la commande Activation :**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Important :**
   > * Remplacez `<JSON_FILE_NAME>.json` par le nom de fichier *exact* du fichier JSON dans le package extrait.
   > * Le nom de fichier JSON est sensible à la casse.
   > * Vérifiez deux fois le nom du fichier pour détecter les fautes de frappe.

   **Sortie attendue :**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ **Remarque :** le processus d’activation peut prendre environ 30 secondes.

5. **Présentation des paramètres de commande :**

   | Paramètre | Description |
   |-----------|-------------|
   | `-p` | Spécifie la plateforme (détecte automatiquement le système d’exploitation). |
   | `-i` | Indique à l’outil d’installer et d’activer la licence. |
   | `-f` | Indique le chemin d’accès au fichier de licence JSON. |

###### Étape 9 : démarrer le serveur AEM Forms

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Démarrez le serveur AEM Forms à partir d’une console de ligne de commande dans une session d’utilisation interactive. (Connectez-vous au serveur et lancez manuellement AEM Forms à partir de la ligne de commande.)
2. Gardez la session d’utilisation active après le démarrage du serveur. Ne vous déconnectez pas de l’ordinateur, car cela mettrait fin au processus du serveur. Vous pouvez fermer en toute sécurité la fenêtre Bureau à distance (RDP) sans vous déconnecter ; le serveur continue à fonctionner tant que la session reste active.
3. Pour une meilleure fiabilité, configurez une tâche de démarrage ou une tâche planifiée pour lancer automatiquement le serveur AEM Forms lorsque la personne se connecte.

###### Étape 10 : tester le service PDF Generator

Une fois tous les processus terminés, effectuez un test d’action rapide pour confirmer que l’installation est valide :

1. Ouvrez l’interface d’administration d’AEM Forms.
2. Accédez au service PDF Generator.
3. Essayez de convertir un document Microsoft Office simple en PDF.
4. Vérifiez que la conversion est correcte.

#### Vérifiez la version d’Acrobat après l’activation de FRL.

1. Ouvrez Adobe Acrobat Pro DC sur le serveur.
2. Accédez à l’Aide → À propos d’Adobe Acrobat Pro DC.
3. Vérifiez que le numéro de version correspond à la version attendue.
4. Confirmez que le statut de licence s’affiche comme étant activé.

>[!ENDTABS]



### Désactivation du mode protégé au démarrage dans Acrobat

Après avoir activé Feature Restricted Licensing (FRL) et vérifié l’activation d’Acrobat, il est recommandé de désactiver le « Mode protégé au démarrage » dans Adobe Acrobat pour garantir la compatibilité avec AEM Forms PDF Generator.

Procédez comme suit :

1. Ouvrez **Adobe Acrobat Pro DC** sur le serveur.
2. Accédez à **Menu** > **Préférences**.
3. Dans la fenêtre Préférences, sélectionnez **Sécurité (renforcée)** dans le volet de gauche.
4. Dans la section **Protections des sandbox**, **décochez** l’option **« Activer le mode protégé au démarrage »**.
5. Cliquez sur **Oui**, le cas échéant.
6. Cliquez sur **OK** pour enregistrer vos modifications et fermer la fenêtre Préférences.
7. Redémarrez Adobe Acrobat Pro DC pour que les modifications soient prises en compte.

>[!NOTE]
>
>La désactivation du mode protégé est requise pour les scénarios d’automatisation côté serveur, tels qu’AEM Forms PDF Generator. Ce paramètre ne doit être modifié que sur les environnements de serveur dédiés, et non sur les ordinateurs de bureau des utilisateurs finaux et utilisatrices finales.

Pour plus d’informations, voir la documentation d’[Adobe en mode protégé](https://helpx.adobe.com/fr/acrobat/kb/protected-mode-troubleshooting-reader.html).



### Définition des variables d’environnement {#setup-environment-variables}

Définissez des variables d’environnement pour Java Development Kit 64 bits, des applications tierces et Adobe Acrobat. Les variables d’environnement doivent contenir le chemin d’accès absolu de l’exécutable utilisé pour démarrer l’application correspondante, par exemple, le tableau ci-dessous répertorie les variables d’environnement pour quelques applications :

<table>
 <tbody>
  <tr>
   <td><p><strong>Application</strong></p> </td>
   <td><p><strong>Variable d’environnement</strong></p> </td>
   <td><p><strong>Exemple</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK (64 bits)</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk11</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>Bloc-notes</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice </strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice 4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Toutes les variables d’environnement et les chemins respectifs sont sensibles à la casse.
>* JAVA_HOME et Acrobat_PATH (Windows uniquement) sont des variables d’environnement obligatoires.
>* La variable d’environnement OpenOffice_PATH est définie sur le dossier d’installation et non pas sur le chemin d’accès au fichier exécutable.
>* Ne définissez pas de variables d’environnement pour des applications Microsoft® Office telles que Word, PowerPoint, Excel et Project, ni pour des applications AutoCAD. Si ces applications sont installées sur le serveur, le service Generate PDF les démarre automatiquement.
>* Sur les plates-formes UNIX, installez OpenOffice en tant que /root. Si OpenOffice n’est pas installé en tant qu’utilisateur ou utilisatrice root, le service PDF Generator ne parvient pas à convertir les documents OpenOffice en documents PDF. Si vous devez installer et exécuter OpenOffice en tant qu’utilisateur non root, indiquez les droits sudo pour l’utilisateur non-root.
>* Si vous utilisez OpenOffice sur une plateforme UNIX, exécutez la commande suivante pour définir la variable de chemin :\
> `export OpenOffice_PATH=/opt/openoffice.org4`
>* Sur les plateformes SUSE® Linux® (SLES 15 SP6 ou ultérieures), procédez comme suit pour configurer OpenOffice :
>     * Installez la dernière version 32 bits d’`OpenOffice 4.1.x` dans un répertoire tel que `/opt/openoffice4`.
>     * Définissez la variable d’environnement `OpenOffice_PATH` de manière à ce qu’elle pointe vers cet emplacement. Par exemple : `OpenOffice_PATH=/opt/openoffice4`.
>     * Assurez-vous que la variable `OpenOffice_PATH` est définie globalement (par exemple, à l’aide de `/etc/profile` ou de l’équivalent spécifique au système) afin qu’elle soit disponible pour tous les utilisateurs et utilisatrices lors de la connexion.

### (Uniquement pour IBM® WebSphere®) Configurer le fournisseur de socket SSL IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Pour configurer le fournisseur de socket SSL IBM®, procédez comme suit :

1. Créez une copie du fichier java.security. L’emplacement par défaut du fichier est `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Ouvrez le fichier java.security copié pour le modifier.
1. Modifiez les fabriques de socket SSL par défaut pour utiliser les fabriques JSSE2 au lieu des fabriques IBM® WebSphere® par défaut :

   **Contenu par défaut:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Contenu modifié :**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Pour activer le serveur AEM Forms pour utiliser le fichier java.security mis à jour, lors du démarrage du serveur AEM Forms, ajoutez l’argument java suivant :

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Windows uniquement) Configurer les paramètres de blocage des fichiers pour Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Modifiez les paramètres du Centre de gestion de la confidentialité Microsoft® Office pour permettre au service PDF Generator de convertir des fichiers créés avec des versions précédentes de Microsoft® Office.

1. Ouvrez une application Microsoft® Office. Par exemple, Microsoft® Word. Accédez à **[!UICONTROL Fichier]** >**[!UICONTROL Options]**. La boîte de dialogue Options s’affiche.

1. Cliquez sur **[!UICONTROL Centre de confiance]**, puis sur **[!UICONTROL Paramètres du Centre de confiance]**.
1. Dans les **[!UICONTROL Paramètres du Centre de confiance]**, cliquez sur **[!UICONTROL Paramètres de blocage des fichiers]**.
1. Dans la liste **[!UICONTROL Type de fichier]**, désélectionnez l’option **[!UICONTROL Ouvrir]** pour le type de fichier que le service PDF Generator devrait être autorisé à convertir en documents PDF.

### (Windows uniquement) Accorder le droit Remplacer un jeton de niveau processus {#grant-the-replace-a-process-level-token-privilege}

Le compte utilisateur utilisé pour démarrer le serveur d’applications doit avoir le droit de **Remplacer un jeton de niveau processus**. Le compte système local possède le droit de **Remplacer un jeton de niveau processus** par défaut. Pour les serveurs s’exécutant avec un utilisateur ou une utilisatrice du groupe d’administration locale, le droit doit être accordé explicitement. Effectuez les étapes suivantes pour accorder le droit :

1. Ouvrez l’éditeur de politique de groupe de Microsoft® Windows. Pour ouvrir l’éditeur de politique de groupe, cliquez sur **[!UICONTROL Démarrer]**, saisissez **gpedit.msc** dans la zone Lancer la recherche, puis cliquez sur **[!UICONTROL Éditeur de politique de groupe]**.
1. Accédez à **[!UICONTROL Politique d’ordinateur local]** > **[!UICONTROL Configuration d’ordinateur]** > **[!UICONTROL Paramètres Windows]** > **[!UICONTROL Paramètres de sécurité]** > **[!UICONTROL Politiques locales]** > **[!UICONTROL Attribution des droits utilisateur]** et modifiez la politique **[!UICONTROL Remplacer un jeton de niveau processus]** pour y inclure le groupe Administrateurs et administratrices.
1. Ajoutez l’utilisateur ou l’utilisatrice à l’entrée Remplacer un jeton de niveau processus.

>[!NOTE]
>
> Comme indiqué ci-dessus, si le serveur AEM s’exécute en tant que service sous le compte système local (LSA), l’attribution explicite de ce privilège à une personne n’est pas nécessaire.

### (Windows uniquement) Activer le service PDF Generator pour les utilisateurs non-administrateurs {#enable-the-pdf-generator-service-for-non-administrators}

Vous pouvez permettre à un utilisateur non-administrateur d’utiliser le service PDF Generator. Normalement, seuls les utilisateurs disposant de droits d’administrateur peuvent utiliser le service :

1. Créez une variable d’environnement PDFG_NON_ADMIN_ENABLED.
1. Définissez la valeur de la variable d’environnement sur TRUE.
1. Redémarrez l’instance AEM Forms.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

### (Windows uniquement) Désactiver le contrôle de compte d’utilisateur (UAC) {#disable-user-account-control-uac}

1. Pour accéder à l’utilitaire de configuration système, sélectionnez **[!UICONTROL Démarrer > Exécuter]** et saisissez **[!UICONTROL MSCONFIG]**.
1. Cliquez sur l’onglet **[!UICONTROL Outils]**, faites défiler l’écran vers le bas, puis sélectionnez **[!UICONTROL Modifier les paramètres de contrôle de compte d’utilisateur]**. Cliquez sur **[!UICONTROL Démarrer]** pour lancer la commande dans une nouvelle fenêtre.
1. Déplacez le curseur sur le niveau Ne jamais m’avertir. Cela fait, fermez la fenêtre de commande, puis celle de la configuration du système.
1. Vérifiez que le paramètre de registre pour l’UAC est défini sur 0 (zéro). Pour vérifier, procédez comme suit :

   1. Microsoft® recommande de sauvegarder le registre avant de le modifier. Pour obtenir la procédure détaillée, voir [Comment sauvegarder et restaurer le registre dans Windows](https://support.microsoft.com/fr-fr/help/322756).
   1. Ouvrez l’éditeur de registre Microsoft® Windows. Pour ouvrir l’éditeur de registre, accédez à Démarrer > Exécuter, saisissez regedit, puis cliquez sur OK.
   1. Accédez à `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assurez-vous que la valeur de EnableLUA est définie sur 0 (zéro).
   1. Assurez-vous que la valeur de **EnableLUA** est définie sur 0 (zéro). Si la valeur n’est pas 0, remplacez-la par 0. Fermez l’éditeur du registre.

1. Redémarrez l’ordinateur.

### (Windows uniquement) Désactiver le service de rapport d’erreur {#disable-error-reporting-service}

Lors de la conversion d’un document au format PDF à l’aide du service PDF Generator sous Windows Server, ce dernier signale parfois que le fichier exécutable a rencontré un problème et doit fermer. La conversion au format PDF n’est toutefois pas affectée et se poursuit en arrière-plan.

Pour éviter de recevoir cette erreur, vous pouvez désactiver le rapport d’erreurs Windows. Pour en savoir plus sur la désactivation des rapports d’erreur, consultez la section [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Windows uniquement) Configurer la conversion de fichiers HTML en PDF {#configure-html-to-pdf-conversion}

Le service PDF Generator fournit des méthodes ou des itinéraires WebKit, WebCapture et WebToPDF pour convertir des fichiers HTML en documents PDF. Sous Windows, pour activer la conversion des itinéraires WebKit et Acrobat WebCapture, copiez la police Unicode vers le répertoire %windir%\fonts.

>[!NOTE]
>
>À chaque installation de nouvelles polices dans le dossier de polices, redémarrez l’instance AEM Forms.

### (Plateformes UNIX uniquement) Configurations supplémentaires pour la conversion de fichiers HTML en PDF  {#extra-configurations-for-html-to-pdf-conversion}

Sur les plateformes UNIX, le service PDF Generator prend en charge les itinéraires WebKit et WebToPDF pour convertir des fichiers HTML en documents PDF. Pour activer la conversion de fichiers HTML en PDF, effectuez les configurations suivantes, applicables à l’itinéraire de conversion de votre choix :

### (Plateformes UNIX uniquement) Activer la prise en charge des polices Unicode (WebKit uniquement) {#enable-support-for-unicode-fonts-webkit-only}

Copiez la police Unicode vers l’un des répertoires suivants, en fonction de votre système d’exploitation :

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* Sous Red Hat® Enterprise Linux® 6.x et versions ultérieures, les polices Courier ne sont pas disponibles. Pour installer les polices Courier, téléchargez l’archive font-ibm-type1-1.0.3.zip. Extrayez le fichier d&#39;archives sur /usr/share/fonts. Créez un lien symbolique de /usr/share/X11/fonts vers /usr/share/fonts.
>* Supprimez tous les fichiers de mémoire cache des polices .lst dans les répertoires Html2PdfSvc/bin et /usr/share/fonts.
>* Vérifiez que les répertoires /usr/lib/X11/fonts et /usr/share/fonts existent. Si les répertoires n’existent pas, utilisez la commande ln pour créer un lien symbolique de /usr/share/X11/fonts vers /usr/lib/X11/fonts et un autre lien symbolique à partir de /usr/share/fonts vers /usr/share/X11/fonts. Vérifiez également que les polices Courier sont disponibles à l’emplacement /usr/lib/X11/fonts
>* Vérifiez que toutes les polices (Unicode et non Unicode) sont disponibles dans le répertoire /usr/share/fonts ou /usr/share/X11/fonts.
>* Lorsque vous exécutez le service PDF Generator en tant qu’utilisateur non root, donnez à l’utilisateur non root un accès en lecture et en écriture à tous les répertoires de polices.
>* À chaque installation de nouvelles polices dans le dossier de polices, redémarrez l’instance AEM Forms.
>

## Installation du package complémentaire AEM Forms {#install-aem-forms-add-on-package}

Le module complémentaire AEM Forms est une application déployée sur AEM. Le package contient des services de document AEM Forms et d’autres fonctionnalités AEM Forms. Pour installer le package, procédez comme suit : 

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Sélectionnez **[!UICONTROL Adobe Experience Manager]** situé dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Sélectionnez le nom de package applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les conditions du CLUF]**, puis sélectionnez **[!UICONTROL Télécharger]**.
1. Ouvrez le [gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Charger le package]** pour charger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

   Vous pouvez également télécharger le package via le lien direct répertorié dans l’article [Version d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

1. Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **N’arrêtez pas le serveur immédiatement.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log et que le journal soit stable.

## Configurations post-installation {#post-installation-configurations}

### Configuration de Boot Delegation pour les bibliothèques RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Désactivez l’instance AEM. Accédez au dossier [Répertoire d’installation AEM]\crx-quickstart\conf\. Ouvrez le fichier sling.properties pour modification.

   Si vous utilisez `[AEM installation directory]\crx-quickstart\bin\start.bat` pour démarrer une instance AEM, modifiez le fichier sling.properties situé à l’emplacement suivant :`[AEM_root]\crx-quickstart\`.

1. Ajoutez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (AIX® uniquement) Ajoutez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Enregistrez et fermez le fichier.

### Configurer le service de gestion de polices  {#configuring-the-font-manager-service}

1. Connectez-vous à [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) en tant qu’administrateur.
1. Recherchez et ouvrez le service **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]**. Indiquez le chemin d’accès des répertoires des polices système, Adobe Server et client. Cliquez sur **[!UICONTROL Enregistrer]**.

   >[!NOTE]
   >
   >Vos droits d’utilisation relatifs aux polices fournies par des sociétés autres qu’Adobe sont régis par les contrats de licence accompagnant ces polices. Ils ne sont pas couverts par la licence d’utilisation du logiciel Adobe qui vous est concédée. Adobe vous recommande de vous assurer que vous agissez en conformité avec tous les contrats de licence non-Adobe applicables avant d’utiliser des polices non-Adobe avec des logiciels Adobe, notamment en ce qui concerne l’utilisation de polices dans des environnements de serveurs.
   >Lorsque vous installez de nouvelles polices dans le dossier de polices, redémarrez l’instance AEM Forms.
   >

### Configuration d’un compte d’utilisateur local pour exécuter le service PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Un compte d’utilisateur local est requis pour exécuter le service PDF Generator. Pour les étapes de création d’un utilisateur local, voir [Créer un compte d’utilisateur dans Windows](https://support.microsoft.com/fr-fr/help/13951/windows-create-user-account) ou créer un compte d’utilisateur sur des plateformes UNIX.

1. Ouvrez la page [Configuration de PDF Generator dans AEM Forms.](http://localhost:4502/libs/fd/pdfg/config/ui.html)

1. Dans l’onglet **[!UICONTROL Comptes d’utilisateurs]**, saisissez les informations d’identification d’un compte d’utilisateur local, puis cliquez sur **[!UICONTROL Envoyer]**. Si Microsoft® Windows vous y invite, autorisez l’accès à l’utilisateur ou à l’utilisatrice. Une fois ajouté, l’utilisateur configuré est affiché sous la section **[!UICONTROL Vos comptes d’utilisateurs]** dans l’onglet **[!UICONTROL Comptes d’utilisateurs]**.

### Configuration des paramètres de délai d’expiration {#configure-the-time-out-settings}

1. Dans [AEM Configuration Manager](http://localhost:4502/system/console/configMgr), recherchez et ouvrez le service **[!UICONTROL Jacorb ORB Provider]**.

   Ajoutez l’élément suivant au champ **[!UICONTROL Properties.name personnalisé]** et cliquez sur **[!UICONTROL Enregistrer]**. Il définit le délai de la réponse en attente (également appelé délai d’attente du client CORBA) à 600 secondes.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Connectez-vous à l’instance de création AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Outils]** > **[!UICONTROL Forms]** > **[!UICONTROL Configuration de PDF Generator]**. L’URL par défaut est <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Ouvrez l’onglet **[!UICONTROL Configuration générale]** et modifiez la valeur des champs suivants pour votre environnement :

<table>
 <tbody>
  <tr>
   <td>Champ</td>
   <td>Description</td>
   <td>Valeur par défaut</td>
  </tr>
  <tr>
   <td>Expiration de conversion sur le serveur</td>
   <td>Une conversion PDFG reste active pendant le nombre de secondes définies dans le délai de conversion du serveur.</td>
   <td>270 secondes<br /> </td>
  </tr>
  <tr>
   <td>Secondes d’analyse de nettoyage PDFG</td>
   <td>Nombre de secondes requises pour exécuter des opérations après la conversion.<br /> </td>
   <td>3600 secondes</td>
  </tr>
  <tr>
   <td>Secondes avant expiration de la tâche</td>
   <td>Durée pendant laquelle le service PDF Generator peut exécuter une conversion. Assurez-vous que la valeur de Secondes avant expiration de la tâche est supérieure à celle de Secondes d’analyse de nettoyage PDFG.</td>
   <td>7200 secondes</td>
  </tr>
 </tbody>
</table>

### (Windows uniquement) Configurer Acrobat pour le service PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

Sous Microsoft® Windows, le service PDF Generator utilise Adobe Acrobat pour convertir les formats de fichiers pris en charge en document PDF. Pour configurer Adobe Acrobat pour le service PDF Generator, procédez comme suit :

1. Ouvrez Acrobat et sélectionnez **[!UICONTROL Modifier]** > **[!UICONTROL Préférences]** > **[!UICONTROL Mises à jour]**. Dans Rechercher les mises à jour maintenant, décochez **[!UICONTROL Installer automatiquement les mises à jour]** et cliquez sur **[!UICONTROL OK]**. Fermez Acrobat.
1. Cliquez deux fois sur un document PDF sur votre système. Lors du premier démarrage d’Acrobat, les boîtes de dialogue de connexion, l’écran de bienvenue et le CLUF s’affichent. Fermez ces boîtes de dialogue pour tous les utilisateurs et utilisatrices configurés pour utiliser PDF Generator.
1. Exécutez le fichier de commandes de l’utilitaire PDF Generator pour configurer Acrobat pour le service PDF Generator :

   1. Ouvrez [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) et téléchargez le fichier `adobe-aemfd-pdfg-common-pkg-[version].zip` depuis le gestionnaire de modules.
   1. Décompressez le fichier .zip téléchargé. Ouvrez l’invite de commande avec des droits d’administration.
   1. Accédez à `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`.
   1. Décompressez le fichier `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. Accédez au répertoire `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]`. Exécutez le fichier de commandes suivant :

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat est configuré pour s’exécuter avec le service PDF Generator.

1. Exécutez l’[outil System Readiness (SRT)](#SRT) pour valider l’installation d’Acrobat.


### (Windows uniquement) Configurer l’itinéraire principal pour la conversion de fichiers HTML en PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Le service PDF Generator fournit plusieurs itinéraires pour convertir des fichiers HTML en documents PDF : WebKit, Acrobat WebCapture (Windows uniquement) et WebToPDF. Adobe recommande d’utiliser l’itinéraire WebToPDF, car il peut gérer le contenu dynamique, ne dépend pas des bibliothèques 32 bits et ne nécessite aucune police supplémentaire. En outre, l’itinéraire WebToPDF ne requiert pas d’accès sudo ou root pour exécuter la conversion.

L’itinéraire principal par défaut pour les conversions HTML en PDF est WebKit. Pour modifier l’itinéraire de conversion :

1. Sur l’instance de création AEM, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Forms]** > **[!UICONTROL Configuration de PDF Generator]**.

1. Dans l’onglet **[!UICONTROL Configuration générale]**, sélectionnez l’itinéraire de votre choix dans le menu déroulant **[!UICONTROL Itinéraire principal pour les conversions HTML en PDF]**.

### Initialisez Global Trust Store {#intialize-global-trust-store}

Trust Store Management vous permet d’importer, de modifier et de supprimer des certificats de confiance sur le serveur pour valider des signatures numériques et l’authentification de certificats. Vous pouvez en importer et en exporter autant que vous le souhaitez. Une fois qu’un certificat a été importé, vous pouvez modifier les paramètres d’approbation et le type de Trust Store. Pour initialiser un Trust Store, procédez comme suit :

1. Connectez-vous à une instance AEM Forms en tant qu’administrateur.
1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Trust Store]**.
1. Cliquez sur **[!UICONTROL Créer un Trust Store]**. Définissez le mot de passe, puis sélectionnez **[!UICONTROL Enregistrer]**.

### Configurer les certificats pour le service Chiffrement et l’extension Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

Le service DocAssurance peut appliquer des droits d’utilisation aux documents PDF. Pour appliquer des droits d’utilisation aux documents PDF, configurez les certificats :

Avant de configurer des certificats, assurez -vous que vous disposez des éléments suivants :

* Fichier de certificat (.pfx).

* Mot de passe de la clé privée, fourni avec le certificat.

* Alias de la clé privée. Vous pouvez exécuter la commande Java keytool pour afficher l’alias de la clé privée :
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Mot de passe du fichier KeyStore. Si vous utilisez le certificat Reader Extensions d’Adobe, le mot de passe du fichier KeyStore est toujours identique au mot de passe de la clé privée.

Pour configurer les certificats, procédez comme suit :

1. Connectez-vous à l’instance de création AEM en tant qu’administrateur ou administratrice. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
1. Cliquez sur le champ **[!UICONTROL nom]** du compte d’utilisateur ou d’utilisatrice. La page **[!UICONTROL Modifier les paramètres utilisateur]** s’affiche. Sur l’instance de création AEM, les certificats résident dans un KeyStore. Si vous n’avez pas créé de KeyStore précédemment, cliquez sur **[!UICONTROL Créer KeyStore]** et définissez un nouveau mot de passe pour le KeyStore. Si le serveur contient déjà un KeyStore, ignorez cette étape.  Si vous utilisez le certificat Reader Extensions d’Adobe, le mot de passe du fichier Key Store est toujours identique au mot de passe de la clé privée.
1. Sur la page **[!UICONTROL Modifier les paramètres utilisateur]**, sélectionnez lʼonglet **[!UICONTROL KeyStore]**. Développez l’option **[!UICONTROL Ajouter la clé privée à partir du fichier de magasin de clés]**, puis fournissez un alias. L’alias est utilisé pour effectuer l’opération Reader Extensions.
1. Pour télécharger le fichier de certificat, cliquez sur **[!UICONTROL Sélectionner le fichier du magasin de clés]**, puis téléchargez un fichier &lt;filename>.pfx.

   Ajoutez les **[!UICONTROL mot de passe du magasin de clés]**, **[!UICONTROL mot de passe de la clé privée]** et **[!UICONTROL alias de la clé privée]** associés au certificat dans les champs respectifs. Cliquez sur **[!UICONTROL Envoyer]**.

   >[!NOTE]
   >
   >Dans l’environnement de production, remplacez les informations d’identification d’évaluation par celles de production. Veillez à supprimer vos anciennes informations d’identification Reader Extensions avant de mettre à jour des informations d’identification expirées ou d’évaluation.

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** sur la page **[!UICONTROL Modifier les paramètres utilisateur]**.

### Activation du chiffrement AES-256 {#enable-aes}

Pour utiliser le chiffrement AES 256 pour les fichiers PDF, récupérez et installez les fichiers Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Remplacez les fichiers local_policy.jar et US_export_policy.jar dans le dossier jre/lib/security. Par exemple, si vous utilisez Sun JDK, copiez les fichiers téléchargés dans le dossier `[JAVA_HOME]/jre/lib/security`.

Le service Assembler dépend des services Reader Extensions, Signatures, Forms et Output. Pour vérifier que les services requis sont opérationnels, procédez comme suit :

1. Connectez-vous à lʼadresse `https://'[server]:[port]'/system/console/bundles` en tant qu’administrateur.
1. Recherchez les services suivants et vérifiez qu’ils sont en cours d’exécution :

<table>
 <tbody>
  <tr>
   <th>Nom du service</th>
   <th>Nom du lot</th>
  </tr>
  <tr>
   <td>Service Signatures</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Service Reader Extensions</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Service Forms</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>Service Output</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

### (Windows uniquement) Configurer l’entrée de registre pour Microsoft® Project {#configure-registry-entry-for-microsoft-project}

Après avoir installé le module complémentaire AEM Forms et Microsoft® Project sur votre ordinateur, enregistrez une entrée pour Microsoft® Project dans l’emplacement 64 bits. Cela facilite l’exécution des tests de conversion de Project en PDFG. Vous trouverez ci-dessous les étapes décrivant le processus d’entrée du registre :

1. Ouvrez l’éditeur du registre Microsoft® Windows (regedit). Pour ouvrir l’éditeur du registre, accédez à Démarrer > Exécuter, saisissez regedit, puis cliquez sur OK.
1. Accédez à `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`, puis créez un registre de **valeur binaire** et renommez-le **Project**.
1. Remplacez la valeur de données du registre binaire créé par 01 et cliquez sur OK.
1. Fermez l’entrée du registre.


## Problèmes connus et dépannage {#known-issues-and-troubleshooting}

* La conversion de fichiers HTML au format PDF échoue si un fichier d’entrée compressé comprend des fichiers HTML dont le nom contient des caractères à deux octets. Pour éviter ce problème, n’utilisez aucun caractère à deux octets dans le nom des fichiers HTML.

* Sur les systèmes d’exploitation UNIX, effectuez les opérations suivantes pour rechercher les bibliothèques manquantes :

1. Accéder à `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Exécutez la commande suivante pour répertorier toutes les bibliothèques requises par WebToPDF pour convertir un fichier HTML en PDF.

   `ldd phantomjs`

   Exécutez la commande suivante pour répertorier les bibliothèques manquantes.

   `ldd phantomjs | grep not`

1. Installez manuellement les bibliothèques manquantes.

## Outil System Readiness (SRT) {#SRT}

L’[outil System Readiness](#srt-configuration) vérifie si l’ordinateur est correctement configuré pour exécuter les conversions de PDF Generator. L’outil génère un rapport à l’emplacement spécifié. Pour exécuter l’outil :

1. Ouvrez l’invite de commande. Accédez au dossier `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools`.

1. Exécutez la commande suivante à partir de l’invite de commande :

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   La commande génère un rapport et crée également le fichier srt_config.yaml. Vous pouvez l’utiliser pour configurer les options de l’outil SRT. Il est facultatif de configurer les options de l’outil SRT.

   >[!NOTE]
   >
   >* Si l’outil System Readiness signale que le fichier pdfgen.api n’est pas disponible dans le dossier des modules externes Acrobat, copiez le fichier pdfgen.api du répertoire `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` au répertoire `[Acrobat_root]\Acrobat\plug_ins`.

1. Accédez à `[Path_of_reports_folder]`. Ouvrez le fichier SystemReadinessTool.html. Vérifiez le rapport et résolvez les problèmes mentionnés.

### Configurer les options de l’outil SRT {#srt-configuration}

Vous pouvez utiliser le fichier srt_config.yaml pour configurer différents paramètres de l’outil SRT. Le format du fichier est :

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
   #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
   locale: en
   
   #aemTempDir: AEM Temp direcotry
   aemTempDir:
   
   #users: provide PDFG converting users list
   #users:
   # - user1
   # - user2
   users:
   
   #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
   profile:
   
   #outputDir: directory where output files will be saved
   outputDir:
```

* **Paramètres régionaux :** ce paramètre est obligatoire. Il prend en charge l’anglais (en), l’allemand (de), le français (fr) et le japonais (ja). La valeur par défaut est en. Cela n’a aucun impact sur les services PDF Generator s’exécutant sur AEM Forms sur OSGi.
* **aemTempDir :** ce paramètre est facultatif. Il spécifie l’emplacement de stockage temporaire d’Adobe Experience Manager.
* **Utilisateurs :** ce paramètre est facultatif. Vous pouvez spécifier un utilisateur ou une utilisatrice pour vérifier s’il ou elle dispose des autorisations requises et d’un accès en lecture/écriture sur les répertoires obligatoires pour exécuter PDF Generator. Si aucun(e) utilisateur ou utilisatrice n’est spécifié(e), les vérifications spécifiques à l’utilisateur ou à l’utilisatrice sont ignorées et affichées comme ayant échoué dans le rapport.
* **outputDir :** indiquez l’emplacement d’enregistrement du rapport SRT. L’emplacement par défaut est le répertoire de travail actuel de l’outil SRT.

## Résolution des problèmes

Si vous rencontrez des problèmes même après avoir corrigé tous les problèmes signalés par l’outil SRT, effectuez les vérifications suivantes :

Avant d’effectuer les vérifications suivantes, assurez-vous que l’[outil System Readiness](#SRT) ne signale aucune erreur.

+++ Adobe Acrobat

* Assurez-vous que seules les [versions prises en charge](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de Microsoft® Office (32 bits) et d’Adobe Acrobat sont installées et que les boîtes de dialogue d’ouverture sont annulées.
<!-- (Acrobat 2020 only) Ensure that Adobe Acrobat Update Service is disabled. -->
* Assurez-vous que le fichier de commandes [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) a été exécuté avec les privilèges d’administrateur.
* Assurez-vous qu’un utilisateur ou qu’une utilisatrice de PDF Generator est ajouté(e) à l’interface utilisateur de configuration du PDF.
* Assurez-vous que l’autorisation [Remplacer un jeton de niveau processus](#grant-the-replace-a-process-level-token-privilege) est ajoutée à l’utilisateur ou à l’utilisatrice de PDF Generator.
* Assurez-vous que l’Add-in Acrobat PDFMaker Office COM est activé pour les applications Microsoft Office.

+++

+++OpenOffice 

**Microsoft® Windows**

* Assurez-vous que la [version 32 bits prise en charge &#x200B;](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de Microsoft Office est installée et que les boîtes de dialogue d’ouverture sont annulées pour toutes les applications.
* Assurez-vous qu’un utilisateur ou qu’une utilisatrice de PDF Generator est ajouté(e) à l’interface utilisateur de configuration du PDF.
* Assurez-vous que l’utilisateur ou l’utilisatrice de PDF Generator est membre du groupe d’administrateurs et que le privilège [Remplacer un jeton de niveau processus](#grant-the-replace-a-process-level-token-privilege) est défini pour l’utilisateur ou l’utilisatrice.
* Assurez-vous que l’utilisateur ou l’utilisatrice est configuré(e) dans l’interface utilisateur de PDF Generator et qu’il ou elle effectue les actions suivantes :
   1. Se connecter à Microsoft® Windows en tant qu’utilisateur ou utilisatrice de PDF Generator.
   1. Ouvrir les applications Microsoft® Office ou OpenOffice et annuler toutes les boîtes de dialogue.
   1. Définir AdobePDF comme imprimante par défaut.
   1. Définir Acrobat comme programme par défaut pour les fichiers PDF.
   1. Effectuer une conversion manuelle à l’aide des options Fichier > Imprimer et ruban Acrobat dans les applications Microsoft Office et annuler toutes les boîtes de dialogue.
   1. Arrêter tous les processus liés à la conversion tels que winword.exe, powerpoint.exe et excel.exe.
   1. Redémarrer le serveur AEM Forms.

**Linux®**

* Installez la [version prise en charge](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) d’OpenOffice. AEM Forms prend en charge les versions 32 bits et 64 bits. Après l’installation, ouvrez toutes les applications OpenOffice, annulez toutes les fenêtres de boîte de dialogue et fermez les applications. Rouvrez les applications et assurez-vous qu’aucune boîte de dialogue ne s’affiche lors de l’ouverture d’une application OpenOffice.

* Créez une variable d’environnement `OpenOffice_PATH` et définissez-la pour qu’elle pointe vers l’installation OpenOffice définie dans la [console](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) ou le profil dt (arborescence des appareils).
* En cas de problèmes lors de l’installation d’OpenOffice, assurez-vous que les [bibliothèques 32 bits](#extrarequirements) requises pour l’installation d’OpenOffice sont disponibles.

+++

+++Problèmes de conversion d’HTML vers PDF

* Assurez-vous que les répertoires de polices sont ajoutés dans l’interface utilisateur de configuration de PDF Generator.

**Linux et Solaris (itinéraire de conversion WebToPDF)**

* Assurez-vous que la bibliothèque 32 bits est disponible (libicudata.so.42) pour la conversion HTMLToPDF basée sur Webkit et que les bibliothèques 64 bits (libicudata.so.42) sont disponibles pour la conversion HTMLToPDF basée sur WebToPDF.

* Exécutez la commande suivante pour répertorier les bibliothèques manquantes pour WebToPDF :

  ```
  ldd phantomjs | grep not
  ```

**Linux® et Solaris™ (itinéraire de conversion WebKit)**

* Assurez-vous que les répertoires `/usr/lib/X11/fonts` et `/usr/share/fonts` existent. Si les répertoires n’existent pas, créez un lien symbolique à partir de `/usr/share/X11/fonts` vers `/usr/lib/X11/fonts` et un autre lien symbolique de `/usr/share/fonts` vers `/usr/share/X11/fonts`.

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* Assurez-vous que les polices IBM sont copiées sous usr/share/fonts.
* Assurez-vous que le correctif de vulnérabilité fantôme glibc est disponible sur l’ordinateur. Utilisez votre gestionnaire de modules par défaut pour effectuer la mise à jour vers la dernière version de glibc. Cela inclut le correctif de vulnérabilité fantôme.
* Assurez-vous que les dernières versions des bibliothèques libssl, libcrypto et lib curl 32 bits sont installées sur le système. Créez également des liens symboliques `/usr/lib/libcurl.so` (ou libcurl.a pour AIX®), `/usr/lib/libcrypto.so` (ou libcrypto.a pour AIX®) et `/usr/lib/libssl.so` (ou libssl.a pour AIX®) pointant vers les dernières versions (32 bits) des bibliothèques respectives.

* Pour configurer le fournisseur de socket SSL IBM®, procédez comme suit :
   1. Copiez le fichier java.security de `<WAS_Installed_JAVA>\jre\lib\security` à n’importe quel emplacement de votre serveur AEM Forms. L’emplacement par défaut est Default Location = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Modifiez le fichier java.security à l’emplacement copié et modifiez les fabriques de socket SSL par défaut avec les usines JSSE2 (utilisez les fabriques JSSE2 au lieu de WebSphere®).

      Modifiez les fabriques de socket JSSE par défaut suivantes :

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      par

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

<!-- +++ Unable to add a PDF Generator (PDFG) user

* (Acrobat 2020 only) Ensure Microsoft&reg; Visual C++ 2012 x86 and Microsoft&reg; Visual C++ 2013 x86 (32-bit) redistributable are installed on Windows.

+++
-->
+++Échec des tests d’automatisation

* Pour Microsoft® Office et OpenOffice, effectuez au moins une conversion manuellement (pour chaque utilisateur ou utilisatrice) afin de garantir qu’aucune boîte de dialogue ne s’affiche pendant la conversion. Si une boîte de dialogue apparaît, fermez-la. Aucune boîte de dialogue de ce type ne doit apparaître lors de la conversion automatisée.

* Avant d’exécuter l’automatisation sur un environnement AEM Forms sur OSGi, assurez-vous que le module de test est installé et actif.

+++

<!-- +++ (Acrobat 2020 only) Multiple user conversion failures 

* Verify the server logs to check if the conversion is failing for a particular user.(Process Explorer can help you check running process for different users)

* Ensure that the user configured for PDF Generator has local admin rights.

* Ensure that PDF Generator user has read, write, and execute permissions on LC temp and PDFG temp users.

* For Microsoft&reg; Office and OpenOffice, perform at least one conversion manually (as each user) to ensure that no dialogue pops up during conversion. If any dialogue appears, dismissed it. No such dialogue should appear during automated conversion.

* Perform a sample conversion.

+++ -->

<!-- (Acrobat 2020 only) License of Adobe Acrobat installed on AEM Forms Server expires

* If you have an existing license of Adobe Acrobat and it has expired, [Download the latest version of Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), and migrating your serial number. Before [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Use the following commands to generate prov.xml and reserialize the existing install using the prov.xml file instead of commands provided in [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) number article.

      ```

         adobe_prtk --tool=VolumeSerialize --generate --serial=<serialnum> [--leid=<LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=<Absolute path to prov.xml>]

      ```

   * Volume serialize the package (Re-serialize the existing install using the prov.xml file and the new serial): Run the following command from the PRTK installation folder as an administrator to serialize and activate the deployed packages on client machines:

      ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
      ```

* For large-scale installations, use the [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) to remove previous versions of Reader and Acrobat. Customize the installer and deploy it to all the machines of your organization.

(Acrobat 2020 only) AEM Forms Server is in an offline or secure environment and internet is not available to activate Acrobat.

* You can go online within 7 days of the first launch of your Adobe product to complete an online activation and registration or use an internet-enabled device and your product's serial number to complete this process. For detailed instructions, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++ -->

+++ Impossible de convertir un fichier Word ou Excel en PDF sous Windows Server.

Lorsque l’utilisateur ou l’utilisatrice tente de convertir des fichiers Word ou Excel en PDF sur Microsoft Windows Server, l’erreur suivante se produit :

*Message d’erreur du convertisseur principal :
ALC-PDG-015-003-Le système ne peut pas ouvrir le fichier d’entrée. Envoyez à nouveau le fichier ou contactez votre administrateur ou administratrice système.*

Pour résoudre le problème, consultez [Impossible de convertir un fichier Word ou Excel en PDF sous Windows Server](/help/forms/using/disable-uac-for-pdfgconfiguration.md).

+++

+++ Impossible de convertir des fichiers Excel au format PDF sous Windows Server 2019

Lorsque vous convertissez des fichiers Microsoft Excel 2019 au format PDF sous Microsoft Windows Server 2019, vous devez vous assurer que les conditions suivantes sont remplies :

* Lors de l’utilisation du service PDF Generator, votre ordinateur Windows ne doit pas avoir de connexion distante active au serveur AEM (session Windows RDP).
* L’imprimante par défaut doit être définie sur Adobe PDF.

  >[!NOTE]
  >* Pour Apple macOS et Ubuntu OS, il n’est pas nécessaire de configurer les paramètres ci-dessus.

+++

+++ Impossible de convertir des fichiers XPS au format PDF

Pour résoudre le problème, [créez une clé de registre spécifique à une fonctionnalité sous Windows](https://helpx.adobe.com/fr/acrobat/kb/unable-convert-xps-to-pdfs.html).

+++


## Étapes suivantes {#next-steps}

Vous disposez d’un environnement de documents de services AEM Forms fonctionnel. Vous pouvez utiliser les services de document via :

* [Processus basés sur l’utilisation de Forms on OSGi](/help/forms/using/aem-forms-workflow.md)
* [Dossiers de contrôle](/help/forms/using/watched-folder-in-aem-forms.md)
* [API de services de document](/help/forms/using/aem-document-services-programmatically.md)
