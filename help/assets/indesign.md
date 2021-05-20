---
title: Intégrer [!DNL Assets] avec [!DNL InDesign Server]
description: Découvrez comment intégrer [!DNL Adobe Experience Manager Assets] avec [!DNL Adobe InDesign Server].
contentOwner: AG
role: Administrator
feature: Publication
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 38%

---

# Intégrer [!DNL Adobe Experience Manager Assets] avec [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilise:

* Un proxy pour distribuer la charge de certaines tâches de traitement. Un proxy est une instance [!DNL Experience Manager] qui communique avec un programme de traitement du proxy pour accomplir une tâche spécifique, et avec d’autres instances [!DNL Experience Manager] pour diffuser les résultats.
* Le programme de traitement du proxy définit et gère une tâche spécifique.
Il peut s&#39;agir de diverses tâches; par exemple, l’utilisation d’une balise [!DNL InDesign Server] pour traiter les fichiers.

Pour charger intégralement des fichiers dans [!DNL Experience Manager Assets] que vous avez créés avec [!DNL Adobe InDesign], un proxy est utilisé. Cela utilise un worker de proxy pour communiquer avec [!DNL Adobe InDesign Server], où [les scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) sont exécutés pour extraire des métadonnées et générer divers rendus pour [!DNL Experience Manager Assets]. Le worker de proxy active la communication bidirectionnelle entre les instances [!DNL InDesign Server] et [!DNL Experience Manager] dans une configuration cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] est proposé sous la forme de deux offres distinctes. [Adobe de l’appli de bureau ](https://www.adobe.com/fr/products/indesign.html) InDesigns utilisée pour concevoir des mises en page pour l’impression et la distribution numérique. [Adobe InDesign ](https://www.adobe.com/fr/products/indesignserver.html) Server vous permet de créer des documents automatisés par programmation en fonction de ce que vous avez créé avec  [!DNL InDesign]. Il fonctionne comme un service offrant une interface à son moteur [ExtendScript](https://www.adobe.com/devnet/scripting.html). Les scripts sont écrits dans [!DNL ExtendScript], ce qui est similaire à [!DNL JavaScript]. Pour plus d’informations sur les scripts [!DNL InDesign], voir [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Fonctionnement de l’extraction {#how-the-extraction-works}

[!DNL Adobe InDesign Server] peut être intégré à [!DNL Experience Manager Assets] afin que les fichiers INDD créés avec [!DNL InDesign] puissent être transférés, que des rendus puissent être générés, que tous les médias (par exemple, la vidéo) puissent être extraits et stockés en tant que ressources :

>[!NOTE]
>
>Les versions précédentes de [!DNL Experience Manager] pouvaient extraire XMP et la miniature, maintenant tous les médias peuvent être extraits.

1. Téléchargez votre fichier INDD vers [!DNL Experience Manager Assets].
1. Une structure envoie des scripts de commande à [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
Ce script de commande permet d’effectuer les opérations suivantes :

   * Récupérer le fichier INDD.
   * Exécuter les commandes [!DNL InDesign Server] :

      * La structure, le texte et tous les fichiers multimédias sont extraits.
      * Des rendus PDF et JPG sont générés.
      * Des rendus HTML et IDML sont générés.
   * Republiez les fichiers obtenus dans [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML est un format XML qui effectue le rendu de tout le contenu du fichier [!DNL InDesign]. Il est stocké sous la forme d’un package compressé à l’aide de la compression [ZIP](https://www.techterms.com/definition/zip). Pour plus d’informations, voir [Formats d’échange d’InDesigns INX et IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si [!DNL InDesign Server] n’est pas installé ou configuré, vous pouvez tout de même télécharger un fichier INDD dans [!DNL Experience Manager]. Toutefois, les rendus générés seront limités aux formats PNG et JPEG. Vous ne pourrez pas générer de code HTML ou .idml, ni générer des rendus de page.

1. Après l’extraction et la génération du rendu :

   * La structure est identique à `cq:Page` (type de rendu).
   * Le texte et les fichiers extraits sont stockés dans [!DNL Experience Manager Assets].
   * Tous les rendus sont stockés dans [!DNL Experience Manager Assets], dans la ressource elle-même.

## Intégrer le [!DNL InDesign Server] au Experience Manager {#integrating-the-indesign-server-with-aem}

Pour intégrer le [!DNL InDesign Server] à utiliser avec [!DNL Experience Manager Assets] et après avoir configuré votre proxy, vous devez :

1. [Installer InDesign Server](#installing-the-indesign-server).
1. Si nécessaire, [configurez le workflow Ressources du Experience Manager](#configuring-the-aem-assets-workflow).
Cette opération n’est nécessaire que si les valeurs par défaut ne sont pas adaptées à votre instance.
1. Configurer un [programme de traitement du proxy pour InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installer [!DNL InDesign Server] {#installing-the-indesign-server}

Pour installer et démarrer [!DNL InDesign Server] à utiliser avec [!DNL Experience Manager] :

1. Téléchargez et installez le fichier [!DNL InDesign Server].

1. Si nécessaire, vous pouvez personnaliser la configuration de votre instance [!DNL InDesign Server].

1. À partir de la ligne de commande, démarrez le serveur :

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Cela démarre le serveur avec le module complémentaire SOAP en écoute sur le port 8080. Tous les messages de journal et les résultats sont écrits directement dans la fenêtre de commande.

   >[!NOTE]
   >
   >Si vous souhaitez enregistrer les messages de sortie vers un fichier, puis utiliser une redirection ; par exemple, sous Windows :
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configuration du workflow [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispose d’une ressource de mise à jour de  **[!UICONTROL gestion des actifs numériques]** de workflow préconfigurée, qui comprend plusieurs étapes de processus spécifiques à  [!DNL InDesign]:

* [Extraction de médias](#media-extraction)
* [Extraction de page  ](#page-extraction)

Ce workflow est configuré avec les valeurs par défaut qui peuvent être adaptées à votre configuration pour diverses instances d’auteur (il s’agit d’un workflow standard, aussi des informations supplémentaires sont disponibles sous [Modifier un workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si vous utilisez les valeurs par défaut (port SOAP compris), aucune configuration n’est nécessaire.

Après la configuration, le chargement de fichiers [!DNL InDesign] dans [!DNL Experience Manager Assets] (par l’une des méthodes habituelles) déclenche le workflow pour traiter la ressource et préparer les différents rendus. Testez votre configuration en chargeant un fichier INDD dans [!DNL Experience Manager Assets] pour confirmer que vous voyez les différents rendus créés par IDS sous `<*your_asset*>.indd/Renditions`

#### Extraction de médias {#media-extraction}

Cette étape commande l’extraction de médias à partir du fichier INDD.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de médias]**.

![Arguments d’extraction de médias et chemins de scripts](assets/media_extraction_arguments_scripts.png)

Arguments d’extraction de médias et chemins de scripts

* **Bibliothèque ExtendScript** : Il s’agit d’une simple bibliothèque de méthodes HTTP GET/POST, requise par les autres scripts.

* **Étendre les scripts** : Vous pouvez spécifier différentes combinaisons de script ici. Si vous souhaitez que vos propres scripts soient exécutés sur [!DNL InDesign Server], enregistrez-les à l’emplacement `/apps/settings/dam/indesign/scripts`.

Pour plus d’informations sur les scripts [!DNL Adobe InDesign], voir la [documentation InDesign destinée aux développeurs](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Ne modifiez pas la bibliothèque ExtendScript. Cette bibliothèque fournit la fonctionnalité HTTP requise pour communiquer avec Sling. Ce paramètre spécifie la bibliothèque à envoyer à [!DNL InDesign Server] pour l’utiliser ici.

Le script `ThumbnailExport.jsx` exécuté par l’étape du workflow Extraction des médias génère un rendu miniature au format JPG. Ce rendu est utilisé par l’étape du workflow Miniatures des processus afin de générer les rendus statiques requis par [!DNL Experience Manager].

Vous pouvez configurer l’étape du workflow Miniatures des processus de manière à générer des rendus statiques de différentes tailles. Veillez à ne pas supprimer les valeurs par défaut, car elles sont requises par l’interface [!DNL Experience Manager Assets]. Enfin, l’étape de workflow Supprimer le rendu d’aperçu d’image supprime le rendu de miniature JPG, car il n’est plus nécessaire.

#### Extraction de page {#page-extraction}

Cela crée une page [!DNL Experience Manager] à partir des éléments extraits. Un gestionnaire d’extraction est utilisé pour extraire les données d’un rendu (actuellement HTML ou IDML). Ces données sont ensuite utilisées pour créer une page avec PageBuilder.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de page]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestionnaire d’extraction de page** : Dans la liste déroulante, sélectionnez le gestionnaire à utiliser. Un gestionnaire d’extraction fonctionne sur un rendu spécifique, sélectionné par un `RenditionPicker` associé (voir l’API `ExtractionHandler`).
Dans une installation [!DNL Experience Manager] standard, les éléments suivants sont disponibles :
   * Gestionnaire d’extraction d’exportation IDML : Fonctionne sur le rendu `IDML` généré à l’étape MediaExtract .

* **Nom de page** : Indiquez le nom que vous souhaitez attribuer à la page résultant du processus. Si vous laissez le champ vide, le nom est « page » (ou une variante si « page » existe déjà).

* **Titre** de la page : Indiquez le titre que vous souhaitez attribuer à la page résultant du processus.

* **Chemin racine de la page** : Chemin d’accès à l’emplacement racine de la page résultant du processus. Si vous laissez le champ vide, le nœud contenant les rendus de la ressource sera utilisé.

* **Modèle de page** : Modèle à utiliser lors de la génération de la page résultant du processus.

* **Conception de page** : Conception de page à utiliser lors de la génération de la page résultant du processus.

### Configurez le programme de traitement du proxy pour [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

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

###  de Day CQ Link Externalizer{#configuring-day-cq-link-externalizer}

Si [!DNL InDesign Server] et [!DNL Experience Manager] se trouvent sur des hôtes différents ou que l’une de ces applications ou les deux ne fonctionnent pas sur les ports par défaut, configurez [!UICONTROL l’externaliseur de liens Day CQ] pour définir le nom d’hôte, le port et le chemin d’accès au contenu pour [!DNL InDesign Server].

1. Accédez à la console web à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Recherchez la configuration **[!UICONTROL Day CQ Link Externalizer]**. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir.
1. Les paramètres de l’externaliseur de liens permettent de créer des URL absolues pour le déploiement [!DNL Experience Manager] et pour [!DNL InDesign Server]. Utilisez le champ **[!UICONTROL Domains]** pour spécifier le nom d’hôte et le chemin d’accès au contexte pour [!DNL Adobe InDesign Server]. Cliquez sur **Enregistrer**.

   ![Paramètre de l’externaliseur de lien](assets/link-externalizer-config.png)

### Activer le traitement parallèle des tâches pour [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Vous pouvez désormais activer le traitement parallèle des tâches pour IDS. Déterminez le nombre maximal de tâches parallèles (`x`) qu’une [!DNL InDesign Server] peut traiter :

* Sur une seule machine à multiprocesseur, le nombre maximal de tâches parallèles (`x`) qu’un [!DNL InDesign Server] peut traiter est inférieur au nombre de processeurs exécutant IDS.
* Lorsque vous exécutez IDS sur plusieurs machines, vous devez compter le nombre total de processeurs disponibles (sur chaque ordinateur) et soustraire le nombre total d’ordinateurs.

Pour configurer le nombre de tâches parallèles d’IDS :

1. Ouvrez l’onglet **[!UICONTROL Configurations]** de la console Felix ; par exemple :   `https://[aem_server]:[port]/system/console/configMgr`.

1. Sélectionnez la file d’attente de traitement IDS sous `Apache Sling Job Queue Configuration`.

1. Définissez :

   * **Type** - `Parallel`
   * **Nombre max. de tâches parallèles** - `<*x*>` (conformément au calcul ci-dessus)

1. Enregistrez ces modifications.
1. Pour activer la prise en charge multi-session pour Adobe CS6 et versions ultérieures, cochez la case `enable.multisession.name` sous la configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Créez un [groupe de `x` traitement IDS en ajoutant des points d’extrémité SOAP à la configuration du traitement IDS](#configuring-the-proxy-worker-for-indesign-server).

   Si plusieurs machines exécutent [!DNL InDesign Server], ajoutez des points d’entrée SOAP (nombre de processeurs par ordinateur -1) pour chaque machine.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Lorsque vous travaillez avec un groupe de travailleurs, vous pouvez activer la liste bloquée des travailleurs IDS.
>
>Pour ce faire, cochez la case **[!UICONTROL enable.retry.name]** sous la configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, ce qui permet de nouvelles tentatives pour les tâches IDS.
>
>En outre, sous la configuration `com.day.cq.dam.ids.impl.IDSPoolImpl.name` , définissez une valeur positive pour le paramètre `max.errors.to.blacklist` qui détermine le nombre de tentatives pour une tâche avant qu’un IDS ne soit exclu de la liste des gestionnaires de tâches.
>
>Par défaut, après le temps configurable (`retry.interval.to.whitelist.name`) en minutes, le programme de travail IDS est revalidé. Si le programme de traitement est en ligne, il est retiré de la liste bloquée.

## Activation de la prise en charge de [!DNL InDesign Server] 10.0 ou version ultérieure {#enabling-support-for-indesign-server-or-later}

Pour [!DNL InDesign Server] 10.0 ou version ultérieure, procédez comme suit pour activer la prise en charge multi-session.

1. Ouvrez Configuration Manager à partir de votre instance [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Sélectionnez l’option **[!UICONTROL ids.cc.enable]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Pour l’intégration de [!DNL InDesign Server] à [!DNL Experience Manager Assets], utilisez un processeur à plusieurs coeurs, car la fonctionnalité de prise en charge de session nécessaire à l’intégration n’est pas prise en charge sur les systèmes à un seul coeur.

## Configuration des [!DNL Experience Manager] informations d’identification {#configure-aem-credentials}

Vous pouvez modifier les informations d’identification d’administrateur par défaut (nom d’utilisateur et mot de passe) pour accéder à [!DNL InDesign Server] à partir de votre déploiement [!DNL Experience Manager] sans interrompre l’intégration à [!DNL InDesign Server].

1. Accédez à `/etc/cloudservices/proxy.html`.
1. Dans la boîte de dialogue, indiquez le nouveau nom d’utilisateur et le nouveau mot de passe.
1. Enregistrez les identifiants.

>[!MORELIKETHIS]
>
>* [À propos d’Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

