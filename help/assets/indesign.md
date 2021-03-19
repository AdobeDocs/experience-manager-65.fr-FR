---
title: Intégrer [!DNL Assets] avec [!DNL InDesign Server]
description: Découvrez comment intégrer  [!DNL Adobe Experience Manager Assets] à [!DNL Adobe InDesign Server].
contentOwner: AG
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 38%

---


# Intégrer [!DNL Adobe Experience Manager Assets] à [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilise:

* Un proxy pour distribuer la charge de certaines tâches de traitement. Un proxy est une instance [!DNL Experience Manager] qui communique avec un agent proxy pour exécuter une tâche spécifique, et d&#39;autres instances [!DNL Experience Manager] pour fournir les résultats.
* Le programme de traitement du proxy définit et gère une tâche spécifique.
Elles peuvent couvrir une grande variété de tâches; par exemple, l’utilisation d’un [!DNL InDesign Server] pour traiter les fichiers.

Pour télécharger complètement des fichiers vers [!DNL Experience Manager Assets] que vous avez créés avec [!DNL Adobe InDesign] un proxy est utilisé. Il utilise un agent proxy pour communiquer avec [!DNL Adobe InDesign Server], où [les scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) sont exécutés pour extraire des métadonnées et générer divers rendus pour [!DNL Experience Manager Assets]. Le programme de travail proxy active la communication bidirectionnelle entre les instances [!DNL InDesign Server] et [!DNL Experience Manager] dans une configuration de cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] est proposé sous forme de deux offres distinctes. [Adobe de l’application ](https://www.adobe.com/fr/products/indesign.html) InDesignpour bureau utilisée pour concevoir des mises en page pour l’impression et la distribution numérique. [Adobe InDesign ](https://www.adobe.com/fr/products/indesignserver.html) Server vous permet de créer des documents automatisés par programmation en fonction de ce que vous avez créé  [!DNL InDesign]. Il fonctionne comme un service offrant une interface à son moteur [ExtendScript](https://www.adobe.com/devnet/scripting.html). Les scripts sont écrits dans [!DNL ExtendScript], ce qui est similaire à [!DNL JavaScript]. Pour plus d’informations sur les scripts [!DNL InDesign], voir [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Fonctionnement de l&#39;extraction {#how-the-extraction-works}

[!DNL Adobe InDesign Server] peut être intégré à [!DNL Experience Manager Assets] afin que les fichiers INDD créés avec [!DNL InDesign] puissent être téléchargés, des rendus générés, tous les supports extraits (vidéo, par exemple) et stockés en tant que ressources :

>[!NOTE]
>
>Les versions précédentes de [!DNL Experience Manager] ont pu extraire XMP et la miniature, maintenant tous les médias peuvent être extraits.

1. Téléchargez votre fichier INDD dans [!DNL Experience Manager Assets].
1. Une structure envoie des scripts de commande à [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
Ce script de commande permet d’effectuer les opérations suivantes :

   * Récupérer le fichier INDD.
   * Exécutez les commandes [!DNL InDesign Server] :

      * La structure, le texte et tous les fichiers multimédias sont extraits.
      * Des rendus PDF et JPG sont générés.
      * Des rendus HTML et IDML sont générés.
   * Publiez les fichiers obtenus sur [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML est un format XML qui restitue tout le contenu du fichier [!DNL InDesign]. Il est stocké en tant que package compressé à l’aide de la compression [ZIP](https://www.techterms.com/definition/zip). Pour plus d’informations, voir [Formats d’échange d’InDesigns INX et IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si [!DNL InDesign Server] n&#39;est pas installé ou configuré, vous pouvez toujours télécharger un fichier INDD dans [!DNL Experience Manager]. Toutefois, les rendus générés seront limités aux formats PNG et JPEG. Vous ne pourrez pas générer de code HTML ou .idml, ni générer des rendus de page.

1. Après l’extraction et la génération du rendu :

   * La structure est identique à `cq:Page` (type de rendu).
   * Le texte et les fichiers extraits sont stockés dans [!DNL Experience Manager Assets].
   * Tous les rendus sont stockés dans [!DNL Experience Manager Assets], dans la ressource elle-même.

## Intégrer le [!DNL InDesign Server] au Experience Manager {#integrating-the-indesign-server-with-aem}

Pour intégrer le [!DNL InDesign Server] à [!DNL Experience Manager Assets] et après avoir configuré votre proxy, vous devez :

1. [Installer InDesign Server](#installing-the-indesign-server).
1. Si nécessaire, [configurez le flux de travaux des ressources du Experience Manager](#configuring-the-aem-assets-workflow).
Cette opération n’est nécessaire que si les valeurs par défaut ne sont pas adaptées à votre instance.
1. Configurer un [programme de traitement du proxy pour InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installer [!DNL InDesign Server] {#installing-the-indesign-server}

Pour installer et début le [!DNL InDesign Server] à utiliser avec [!DNL Experience Manager] :

1. Téléchargez et installez le [!DNL InDesign Server].

1. Si nécessaire, vous pouvez personnaliser la configuration de votre instance [!DNL InDesign Server].

1. À partir de la ligne de commande, démarrez le serveur :

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Cela démarre le serveur avec le module complémentaire SOAP en écoute sur le port 8080. Tous les messages de journal et les résultats sont écrits directement dans la fenêtre de commande.

   >[!NOTE]
   >
   >Si vous souhaitez enregistrer les messages de sortie vers un fichier, puis utiliser une redirection ; par exemple, sous Windows :
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurer le flux de travaux [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispose d&#39;une ressource **[!UICONTROL de mise à jour]** DAM de processus préconfigurée, qui comprend plusieurs étapes de processus spécifiques pour  [!DNL InDesign]:

* [Extraction de médias](#media-extraction)
* [Extraction de page  ](#page-extraction)

Ce workflow est configuré avec les valeurs par défaut qui peuvent être adaptées à votre configuration pour diverses instances d’auteur (il s’agit d’un workflow standard, aussi des informations supplémentaires sont disponibles sous [Modifier un workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si vous utilisez les valeurs par défaut (y compris le port SOAP), aucune configuration n’est nécessaire.

Après la configuration, le téléchargement de fichiers [!DNL InDesign] dans [!DNL Experience Manager Assets] (par l&#39;une des méthodes habituelles) déclenche le processus de traitement de la ressource et de préparation des divers rendus. Testez votre configuration en téléchargeant un fichier INDD dans [!DNL Experience Manager Assets] pour confirmer que vous voyez les différents rendus créés par IDS sous `<*your_asset*>.indd/Renditions`

#### Extraction des médias {#media-extraction}

Cette étape commande l’extraction de médias à partir du fichier INDD.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de médias]**.

![Arguments d’extraction de médias et chemins de scripts](assets/media_extraction_arguments_scripts.png)

Arguments d’extraction de médias et chemins de scripts

* **Bibliothèque** ExtendScript : Il s’agit d’une simple bibliothèque de méthodes get/post http, requise par les autres scripts.

* **Étendre les scripts** : Vous pouvez spécifier différentes combinaisons de script ici. Si vous souhaitez que vos propres scripts soient exécutés sur [!DNL InDesign Server], enregistrez les scripts sur `/apps/settings/dam/indesign/scripts`.

Pour plus d&#39;informations sur les scripts [!DNL Adobe InDesign], consultez la [documentation destinée aux développeurs d&#39;InDesigns](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

>[!CAUTION]
>
>Ne modifiez pas la bibliothèque ExtendScript. Cette bibliothèque fournit la fonctionnalité HTTP requise pour communiquer avec Sling. Ce paramètre spécifie la bibliothèque à envoyer à [!DNL InDesign Server] pour l&#39;utiliser ici.

Le script `ThumbnailExport.jsx` exécuté par l’étape de flux de travaux de l’Extraction multimédia génère un rendu miniature au format JPG. Ce rendu est utilisé par l’étape du workflow Miniatures des processus afin de générer les rendus statiques requis par [!DNL Experience Manager].

Vous pouvez configurer l’étape du workflow Miniatures des processus de manière à générer des rendus statiques de différentes tailles. Veillez à ne pas supprimer les valeurs par défaut, car elles sont requises par l&#39;interface [!DNL Experience Manager Assets]. Enfin, l’étape de flux de travaux Supprimer le rendu de Prévisualisation d’images supprime le rendu de miniature JPG, car il n’est plus nécessaire.

#### Extraction de page {#page-extraction}

Cela crée une page [!DNL Experience Manager] à partir des éléments extraits. Un gestionnaire d’extraction est utilisé pour extraire les données d’un rendu (actuellement HTML ou IDML). Ces données sont ensuite utilisées pour créer une page avec PageBuilder.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de page]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestionnaire** d&#39;Extractions de page : Dans la liste contextuelle, sélectionnez le gestionnaire à utiliser. Un gestionnaire d’extraction fonctionne sur un rendu spécifique, sélectionné par un `RenditionPicker` associé (voir l’API `ExtractionHandler`).
Dans une installation standard [!DNL Experience Manager], les éléments suivants sont disponibles :
   * Handle d&#39;Extraction d&#39;exportation IDML : Fonctionne sur le rendu `IDML` généré à l’étape MediaExtract.

* **Nom** de page : Indiquez le nom que vous souhaitez attribuer à la page résultante. Si vous laissez le champ vide, le nom est « page » (ou une variante si « page » existe déjà).

* **Titre** de la page : Indiquez le titre que vous souhaitez affecter à la page résultante.

* **Chemin** racine de la page : Chemin d’accès à l’emplacement racine de la page résultante. Si vous laissez le champ vide, le nœud contenant les rendus de la ressource sera utilisé.

* **Modèle** de page : Modèle à utiliser lors de la génération de la page résultante.

* **Conception** de page : Conception de page à utiliser lors de la génération de la page résultante.

### Configurez le service de travail proxy pour [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

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

Si [!DNL InDesign Server] et [!DNL Experience Manager] se trouvent sur des hôtes différents ou si l&#39;une de ces applications ou les deux ne fonctionnent pas sur les ports par défaut, configurez [!UICONTROL Day CQ Link Externalizer] pour définir le nom d&#39;hôte, le port et le chemin d&#39;accès au contenu pour [!DNL InDesign Server].

1. Accédez à la console Web à l&#39;adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Localisez la configuration **[!UICONTROL Externalisateur de lien Day CQ]**. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir.
1. Les paramètres de l&#39;Externalisateur de liens permettent de créer des URL absolues pour le déploiement [!DNL Experience Manager] et pour [!DNL InDesign Server]. Utilisez le champ **[!UICONTROL Domaines]** pour spécifier le nom d&#39;hôte et le chemin de contexte pour [!DNL Adobe InDesign Server]. Cliquez sur **Enregistrer**.

   ![Paramètre de lien externe](assets/link-externalizer-config.png)

### Activer le traitement parallèle des tâches pour [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Vous pouvez désormais activer le traitement parallèle des tâches pour IDS. Déterminez le nombre maximal de tâches parallèles (`x`) qu’un [!DNL InDesign Server] peut traiter :

* Sur un seul ordinateur multiprocesseur, le nombre maximal de tâches parallèles (`x`) qu&#39;un [!DNL InDesign Server] peut traiter est inférieur au nombre de processeurs exécutant IDS.
* Lorsque vous exécutez IDS sur plusieurs machines, vous devez compter le nombre total de processeurs disponibles (sur chaque ordinateur) et soustraire le nombre total d’ordinateurs.

Pour configurer le nombre de tâches parallèles d’IDS :

1. Ouvrez l’onglet **[!UICONTROL Configurations]** de la console Felix ; par exemple :   `https://[aem_server]:[port]/system/console/configMgr`.

1. Sélectionnez la file d’attente de traitement IDS sous `Apache Sling Job Queue Configuration`.

1. Définissez :

   * **Type** - `Parallel`
   * **Nombre max. de tâches parallèles** - `<*x*>` (conformément au calcul ci-dessus)

1. Enregistrez ces modifications.
1. Pour activer la prise en charge de plusieurs sessions pour Adobe CS6 et versions ultérieures, cochez la case `enable.multisession.name`, sous `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuration.
1. Créez un [groupe de `x` traitement IDS en ajoutant des points d’extrémité SOAP à la configuration du traitement IDS](#configuring-the-proxy-worker-for-indesign-server).

   S&#39;il y a plusieurs ordinateurs exécutant [!DNL InDesign Server], ajoutez des points de terminaison SOAP (nombre de processeurs par ordinateur -1) pour chaque ordinateur.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Lorsque vous travaillez avec un groupe de travailleurs, vous pouvez activer la liste bloquée des travailleurs IDS.
>
>Pour ce faire, activez la case à cocher **[!UICONTROL enable.retry.name]**, sous la configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, qui active les nouvelles tentatives de travaux IDS.
>
>En outre, sous la configuration `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, définissez une valeur positive pour le paramètre `max.errors.to.blacklist` qui détermine le nombre de retests de tâche avant d&#39;interdire un ID de la liste des gestionnaires de tâches.
>
>Par défaut, après le temps configurable (`retry.interval.to.whitelist.name`) en minutes, le programme de travail IDS est revalidé. Si le programme de traitement est en ligne, il est retiré de la liste bloquée.

## Activer la prise en charge de [!DNL InDesign Server] 10.0 ou version ultérieure {#enabling-support-for-indesign-server-or-later}

Pour [!DNL InDesign Server] 10.0 ou version ultérieure, effectuez les étapes suivantes pour activer la prise en charge de plusieurs sessions.

1. Ouvrez Configuration Manager à partir de votre instance [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Sélectionnez l’option **[!UICONTROL ids.cc.enable]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Pour l&#39;intégration de [!DNL InDesign Server] à [!DNL Experience Manager Assets], utilisez un processeur multicoeur car la fonction de prise en charge de session nécessaire à l&#39;intégration n&#39;est pas prise en charge sur les systèmes à noyau unique.

## Configurer les [!DNL Experience Manager] informations d&#39;identification {#configure-aem-credentials}

Vous pouvez modifier les informations d’identification d’administrateur par défaut (nom d’utilisateur et mot de passe) pour accéder à [!DNL InDesign Server] à partir de votre déploiement [!DNL Experience Manager] sans rompre l’intégration avec [!DNL InDesign Server].

1. Accédez à `/etc/cloudservices/proxy.html`.
1. Dans la boîte de dialogue, indiquez le nouveau nom d’utilisateur et le nouveau mot de passe.
1. Enregistrez les identifiants.

>[!MORELIKETHIS]
>
>* [A propos de Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

