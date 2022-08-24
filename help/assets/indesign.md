---
title: Intégration d’ [!DNL Assets] à [!DNL InDesign Server]
description: Découvrez comment intégrer [!DNL Adobe Experience Manager Assets] avec [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 38%

---

# Intégration de [!DNL Adobe Experience Manager Assets] à [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilise:

* Un proxy pour distribuer la charge de certaines tâches de traitement. Un proxy est un [!DNL Experience Manager] instance qui communique avec un programme de traitement du proxy pour accomplir une tâche spécifique, et d’autres [!DNL Experience Manager] instances pour diffuser les résultats.
* Le programme de traitement du proxy définit et gère une tâche spécifique.
Il peut s&#39;agir de diverses tâches; par exemple, en utilisant une [!DNL InDesign Server] pour traiter les fichiers.

Pour charger complètement des fichiers dans [!DNL Experience Manager Assets] que vous avez créé avec [!DNL Adobe InDesign] un proxy est utilisé. Cela utilise un worker de proxy pour communiquer avec le [!DNL Adobe InDesign Server]où [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) sont exécutés pour extraire des métadonnées et générer divers rendus pour . [!DNL Experience Manager Assets]. Le worker de proxy active la communication bidirectionnelle entre la variable [!DNL InDesign Server] et le [!DNL Experience Manager] dans une configuration cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] est proposé sous la forme de deux offres distinctes. [Adobe InDesign](https://www.adobe.com/fr/products/indesign.html) application de bureau utilisée pour concevoir des mises en page pour la distribution papier et numérique. [Adobe InDesign Server](https://www.adobe.com/fr/products/indesignserver.html) vous permet de créer des documents automatisés par programmation en fonction de ce que vous avez créé avec [!DNL InDesign]. Il fonctionne comme un service offrant une interface à ses [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Les scripts sont écrits dans [!DNL ExtendScript], qui est similaire à [!DNL JavaScript]. Pour plus d’informations sur [!DNL InDesign] les scripts [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Fonctionnement de l’extraction {#how-the-extraction-works}

Le [!DNL Adobe InDesign Server] peut être intégré à [!DNL Experience Manager Assets] afin que les fichiers INDD créés avec [!DNL InDesign] peuvent être transférés, des rendus générés, tous les médias extraits (vidéo, par exemple) et stockés en tant que ressources :

>[!NOTE]
>
>Versions précédentes d’ [!DNL Experience Manager] ont pu extraire XMP et la miniature, maintenant tous les médias peuvent être extraits.

1. Téléchargez votre fichier INDD vers [!DNL Experience Manager Assets].
1. Une structure envoie des scripts de commande au [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
Ce script de commande permet d’effectuer les opérations suivantes :

   * Récupérer le fichier INDD.
   * Exécuter [!DNL InDesign Server] Commandes :

      * La structure, le texte et tous les fichiers multimédias sont extraits.
      * Des rendus PDF et JPG sont générés.
      * Des rendus HTML et IDML sont générés.
   * Republiez les fichiers obtenus dans [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML est un format XML qui effectue le rendu de tout le contenu de la variable [!DNL InDesign] fichier . Il est stocké sous la forme d’un package compressé à l’aide de [ZIP](https://www.techterms.com/definition/zip) compression. Pour plus d’informations, voir [Formats d’échange d’InDesigns INX et IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si la variable [!DNL InDesign Server] n’est pas installé ou configuré, vous pouvez toujours télécharger un fichier INDD dans [!DNL Experience Manager]. Toutefois, les rendus générés seront limités aux formats PNG et JPEG. Vous ne pourrez pas générer de code HTML ou .idml, ni générer des rendus de page.

1. Après l’extraction et la génération du rendu :

   * La structure est identique à `cq:Page` (type de rendu).
   * Le texte et les fichiers extraits sont stockés dans [!DNL Experience Manager Assets].
   * Tous les rendus sont stockés dans [!DNL Experience Manager Assets], dans la ressource elle-même.

## Intégrez la variable [!DNL InDesign Server] avec Experience Manager {#integrating-the-indesign-server-with-aem}

Pour intégrer la variable [!DNL InDesign Server] pour une utilisation avec [!DNL Experience Manager Assets] et après avoir configuré votre proxy, vous devez :

1. [Installer InDesign Server](#installing-the-indesign-server).
1. Si nécessaire, [configuration du processus Experience Manager Assets](#configuring-the-aem-assets-workflow).
Cette opération n’est nécessaire que si les valeurs par défaut ne sont pas adaptées à votre instance.
1. Configurer un [programme de traitement du proxy pour InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installez le [!DNL InDesign Server] {#installing-the-indesign-server}

Pour installer et démarrer le [!DNL InDesign Server] pour une utilisation avec [!DNL Experience Manager]:

1. Téléchargez et installez le [!DNL InDesign Server].

1. Si nécessaire, vous pouvez personnaliser la configuration de votre [!DNL InDesign Server] instance.

1. À partir de la ligne de commande, démarrez le serveur :

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Cela démarre le serveur avec le module complémentaire SOAP en écoute sur le port 8080. Tous les messages de journal et les résultats sont écrits directement dans la fenêtre de commande.

   >[!NOTE]
   >
   >Si vous souhaitez enregistrer les messages de sortie vers un fichier, puis utiliser une redirection ; par exemple, sous Windows :
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurez la variable [!DNL Experience Manager Assets] workflow {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispose d’un workflow préconfiguré. **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]**, qui comprend plusieurs étapes de processus spécifiques pour [!DNL InDesign]:

* [Extraction de médias](#media-extraction)
* [Extraction de page  ](#page-extraction)

Ce workflow est configuré avec les valeurs par défaut qui peuvent être adaptées à votre configuration pour diverses instances d’auteur (il s’agit d’un workflow standard, aussi des informations supplémentaires sont disponibles sous [Modifier un workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si vous utilisez les valeurs par défaut (port SOAP compris), aucune configuration n’est nécessaire.

Après la configuration, transférez les fichiers [!DNL InDesign] fichiers dans [!DNL Experience Manager Assets] (par l’une des méthodes habituelles) déclenche le workflow pour traiter la ressource et préparer les différents rendus. Testez votre configuration en chargeant un fichier INDD dans [!DNL Experience Manager Assets] pour confirmer que vous voyez les différents rendus créés par IDS sous `<*your_asset*>.indd/Renditions`

#### Extraction de médias {#media-extraction}

Cette étape commande l’extraction de médias à partir du fichier INDD.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de médias]**.

![Arguments d’extraction de médias et chemins de scripts](assets/media_extraction_arguments_scripts.png)

Arguments d’extraction de médias et chemins de scripts

* **Bibliothèque ExtendScript**: Il s’agit d’une simple bibliothèque de méthodes HTTP GET/POST, requise par les autres scripts.

* **Étendre les scripts**: Vous pouvez spécifier différentes combinaisons de script ici. Si vous souhaitez que vos propres scripts soient exécutés sur la variable [!DNL InDesign Server], enregistrez les scripts à l’adresse `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Ne modifiez pas la bibliothèque ExtendScript. Cette bibliothèque fournit la fonctionnalité HTTP requise pour communiquer avec Sling. Ce paramètre spécifie la bibliothèque à envoyer au [!DNL InDesign Server] à utiliser ici.

Le `ThumbnailExport.jsx` script exécuté par l’étape de workflow Extraction de médias génère un rendu miniature au format JPG. Ce rendu est utilisé par l’étape du workflow Miniatures des processus afin de générer les rendus statiques requis par [!DNL Experience Manager].

Vous pouvez configurer l’étape du workflow Miniatures des processus de manière à générer des rendus statiques de différentes tailles. Veillez à ne pas supprimer les valeurs par défaut, car elles sont requises par la variable [!DNL Experience Manager Assets] . Enfin, l’étape de workflow Supprimer le rendu d’aperçu d’image supprime le rendu de miniature du JPG, car il n’est plus nécessaire.

#### Extraction de page {#page-extraction}

Cela crée une [!DNL Experience Manager] à partir des éléments extraits. Un gestionnaire d’extraction est utilisé pour extraire les données d’un rendu (actuellement HTML ou IDML). Ces données sont ensuite utilisées pour créer une page avec PageBuilder.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de page]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestionnaire d’extraction de page**: Dans la liste déroulante, sélectionnez le gestionnaire à utiliser. Un gestionnaire d’extraction fonctionne sur un rendu spécifique, sélectionné par un `RenditionPicker` associé (voir l’API `ExtractionHandler`).
Dans une norme [!DNL Experience Manager] installez les éléments suivants :
   * Gestionnaire d’extraction d’exportation IDML : Fonctionne sur la variable `IDML` rendu généré lors de l’étape MediaExtract .

* **Nom de la page**: Indiquez le nom que vous souhaitez attribuer à la page résultant du processus. Si vous laissez le champ vide, le nom est « page » (ou une variante si « page » existe déjà).

* **Titre de la page**: Indiquez le titre que vous souhaitez attribuer à la page résultant du processus.

* **Chemin racine de la page**: Chemin d’accès à l’emplacement racine de la page résultant du processus. Si vous laissez le champ vide, le nœud contenant les rendus de la ressource sera utilisé.

* **Modèle de page**: Modèle à utiliser lors de la génération de la page résultant du processus.

* **Conception de page**: Conception de page à utiliser lors de la génération de la page résultant du processus.

### Configuration du worker de proxy pour [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Le programme de traitement réside sur une instance de proxy.

1. Dans la console Outils, développez **[!UICONTROL Configurations Cloud Services]** dans le volet de gauche. Développez ensuite **[!UICONTROL Configuration de proxy Cloud]**.

1. Double-cliquez sur **[!UICONTROL IDS Worker]** pour ouvrir la configuration.

1. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir la boîte de dialogue de configuration et définir les paramètres requis :

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Points d’extrémité SOAP à utiliser pour communiquer avec [!DNL InDesign Server]. Vous pouvez ajouter, supprimer ou trier les éléments au besoin.

1. Cliquez sur OK pour enregistrer.

###  de Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Si la variable [!DNL InDesign Server] et [!DNL Experience Manager] se trouvent sur des hôtes différents ou l’une ou l’autre de ces applications ne fonctionne pas sur les ports par défaut, puis configurez [!UICONTROL Externalisateur de lien Day CQ] pour définir le nom d’hôte, le port et le chemin d’accès au contenu pour la variable [!DNL InDesign Server].

1. Accédez à la console web à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Localisation de la configuration **[!UICONTROL Externalisateur de lien Day CQ]**. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir.
1. Les paramètres de l’externaliseur de liens permettent de créer des URL absolues pour le [!DNL Experience Manager] et pour le déploiement [!DNL InDesign Server]. Utilisation **[!UICONTROL Domaines]** pour spécifier le nom d’hôte de la variable [!DNL Adobe InDesign Server]. Cliquez sur **Enregistrer**.

   Dans les URL absolues, utilisez `localhost` comme nom d’hôte de votre instance locale (d’auteur) et nom d’hôte ou adresse IP de l’instance de publication, comme illustré ci-dessous.

   ![Paramètre de l’externaliseur de lien](assets/link-externalizer-config.png)

### Activation du traitement parallèle des tâches [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Vous pouvez désormais activer le traitement parallèle des tâches pour IDS. Déterminer le nombre maximal de tâches parallèles (`x`) et [!DNL InDesign Server] peut traiter :

* Sur une seule machine à multiprocesseur, nombre maximal de tâches parallèles (`x`) qu’un [!DNL InDesign Server] Le processus peut être inférieur au nombre de processeurs exécutant IDS.
* Lorsque vous exécutez IDS sur plusieurs machines, vous devez compter le nombre total de processeurs disponibles (sur chaque ordinateur) et soustraire le nombre total d’ordinateurs.

Pour configurer le nombre de tâches parallèles d’IDS :

1. Ouvrez l’onglet **[!UICONTROL Configurations]** de la console Felix ; par exemple :   `https://[aem_server]:[port]/system/console/configMgr`.

1. Sélectionnez la file d’attente de traitement IDS sous `Apache Sling Job Queue Configuration`.

1. Définissez :

   * **Type** - `Parallel`
   * **Nombre max. de tâches parallèles** - `<*x*>` (conformément au calcul ci-dessus)

1. Enregistrez ces modifications.
1. Pour activer la prise en charge multi-session pour Adobe CS6 et versions ultérieures, cochez la case `enable.multisession.name` , sous `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuration.
1. Créez un [groupe de `x` traitement IDS en ajoutant des points d’extrémité SOAP à la configuration du traitement IDS](#configuring-the-proxy-worker-for-indesign-server).

   Si plusieurs machines sont en cours d’exécution [!DNL InDesign Server], ajoutez des points d’entrée SOAP (nombre de processeurs par ordinateur -1) pour chaque machine.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Lorsque vous travaillez avec un groupe de travailleurs, vous pouvez activer la liste bloquée des travailleurs IDS.
>
>Pour ce faire, activez la fonction **[!UICONTROL enable.retry.name]** , sous `com.day.cq.dam.ids.impl.IDSJobProcessor.name` qui active les tentatives de tâche IDS.
>
>En outre, sous `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configuration, définir une valeur positive pour `max.errors.to.blacklist` qui détermine le nombre de tentatives pour une tâche avant qu’un IDS ne soit exclu de la liste des gestionnaires de tâches.
>
>Par défaut, après la variable configurable (`retry.interval.to.whitelist.name`) en minutes, le programme de travail IDS est revalidé. Si le programme de traitement est en ligne, il est retiré de la liste bloquée.

## Activer la prise en charge pour [!DNL InDesign Server] 10.0 ou version ultérieure {#enabling-support-for-indesign-server-or-later}

Pour [!DNL InDesign Server] Pour activer la prise en charge multi-session, procédez comme suit ou version ultérieure.

1. Ouvrez Configuration Manager depuis votre [!DNL Experience Manager Assets] instance `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Sélectionnez l’option **[!UICONTROL ids.cc.enable]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Pour [!DNL InDesign Server] intégration avec [!DNL Experience Manager Assets], utilisez un processeur multicoeur, car la fonctionnalité de prise en charge de session nécessaire à l’intégration n’est pas prise en charge sur les systèmes à un seul coeur.

## Configurer [!DNL Experience Manager] informations {#configure-aem-credentials}

Vous pouvez modifier les informations d’identification d’administrateur par défaut (nom d’utilisateur et mot de passe) pour accéder à la variable [!DNL InDesign Server] de votre [!DNL Experience Manager] déploiement sans interrompre l’intégration avec la méthode [!DNL InDesign Server].

1. Accédez à `/etc/cloudservices/proxy.html`.
1. Dans la boîte de dialogue, indiquez le nouveau nom d’utilisateur et le nouveau mot de passe.
1. Enregistrez les identifiants.

>[!MORELIKETHIS]
>
>* [À propos d’Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

