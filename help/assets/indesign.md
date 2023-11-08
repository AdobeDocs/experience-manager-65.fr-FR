---
title: Intégration d’ [!DNL Assets]  à  [!DNL InDesign Server]
description: Découvrez comment intégrer  [!DNL Adobe Experience Manager Assets]  à  [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 91%

---

# Intégration d’[!DNL Adobe Experience Manager Assets] à [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilise :

* un proxy pour distribuer la charge de certaines tâches de traitement. Un proxy est une instance [!DNL Experience Manager] qui communique avec un programme de traitement du proxy afin d’accomplir une tâche spécifique, et avec d’autres instances [!DNL Experience Manager] pour diffuser les résultats.
* Le programme de traitement du proxy définit et gère une tâche spécifique.
Il peut couvrir une grande variété de tâches ; par exemple l’utilisation d’[!DNL InDesign Server] pour traiter les fichiers.

Pour charger intégralement des fichiers créés avec [!DNL Adobe InDesign] vers [!DNL Experience Manager Assets], un proxy est utilisé. Cette méthode utilise un programme de traitement du proxy pour communiquer avec [!DNL Adobe InDesign Server], qui exécute des [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) afin d’extraire des métadonnées et de générer divers rendus pour [!DNL Experience Manager Assets]. Le programme de traitement du proxy permet une communication bidirectionnelle entre [!DNL InDesign Server] et les instances [!DNL Experience Manager] dans une configuration cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] est proposé sous la forme de deux offres distinctes. L’application de bureau [Adobe InDesign](https://www.adobe.com/fr/products/indesign.html) utilisée pour concevoir des dispositions pour la distribution papier et numérique. [Adobe InDesign Server](https://www.adobe.com/fr/products/indesignserver.html) vous permet de créer des documents de façon automatisée, et par programmation, sur la base de vos dispositions créées avec [!DNL InDesign]. Il fonctionne comme un service offrant une interface à son moteur [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting). Les scripts sont écrits dans [!DNL ExtendScript], qui est similaire à [!DNL JavaScript]. Pour plus d’informations sur les scripts [!DNL InDesign], rendez-vous à l’adresse [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Fonctionnement de l’extraction {#how-the-extraction-works}

[!DNL Adobe InDesign Server] peut être intégré à [!DNL Experience Manager Assets], de telle sorte que les fichiers INDD créés avec [!DNL InDesign] puissent être chargés, que des rendus puissent être générés, et que tous les médias (des vidéos, par exemple) puissent être extraits et stockés sous la forme de ressources :

>[!NOTE]
>
>Les versions précédentes d’[!DNL Experience Manager] permettaient seulement d’extraire le XMP et la miniature. Désormais, tous les médias peuvent être extraits.

1. Chargez votre fichier INDD vers [!DNL Experience Manager Assets].
1. Un framework envoie des scripts de commande vers [!DNL InDesign Server] via un protocole SOAP (Simple Object Access Protocol).
Ce script de commande permet d’effectuer les opérations suivantes :

   * Récupérer le fichier INDD.
   * Exécuter les commandes [!DNL InDesign Server] :

      * La structure, le texte et tous les fichiers multimédias sont extraits.
      * Des rendus de PDF et de JPG sont générés.
      * Les rendus HTML et IDML sont générés.

   * Republier les fichiers résultants dans [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML est un format XML qui effectue le rendu de tout le contenu du fichier [!DNL InDesign]. Il est stocké sous la forme d’un package compressé au format [ZIP](https://www.techterms.com/definition/zip). Pour plus d’informations, consultez les [Formats d’échange d’InDesigns INX et IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si [!DNL InDesign Server] n’est pas installé ou configuré, vous pouvez tout de même charger un fichier INDD dans [!DNL Experience Manager]. Toutefois, les rendus générés sont limités au format PNG et JPEG. Vous ne pourrez pas générer les rendus de HTML, .idml ou de page.

1. Après l’extraction et la génération du rendu :

   * La structure est identique à `cq:Page` (type de rendu).
   * Le texte et les fichiers extraits sont stockés dans [!DNL Experience Manager Assets].
   * Tous les rendus sont stockés dans [!DNL Experience Manager Assets], dans la ressource même.

## Intégration d’ [!DNL InDesign Server] à Experience Manager {#integrating-the-indesign-server-with-aem}

Pour intégrer [!DNL InDesign Server] afin de l’utiliser avec [!DNL Experience Manager Assets], après la configuration de votre proxy, vous devez :

1. [installer InDesign Server](#installing-the-indesign-server) ;
1. Si nécessaire, [configuration du processus Experience Manager Assets](#configuring-the-aem-assets-workflow).
Cette opération n’est nécessaire que si les valeurs par défaut ne sont pas adaptées à votre instance.
1. Configurer un [programme de traitement du proxy pour InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installation d’[!DNL InDesign Server] {#installing-the-indesign-server}

Pour installer et démarrer [!DNL InDesign Server] afin de l’utiliser avec [!DNL Experience Manager] :

1. Téléchargez et installez [!DNL InDesign Server].

1. Si nécessaire, vous pouvez personnaliser la configuration de votre [!DNL InDesign Server] instance.

1. À partir de la ligne de commande, démarrez le serveur :

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Cela démarre le serveur avec le module complémentaire SOAP en écoute sur le port 8080. Tous les messages de journal et les résultats sont écrits directement dans la fenêtre de commande.

   >[!NOTE]
   >
   >Si vous souhaitez enregistrer les messages de sortie vers un fichier, puis utiliser une redirection ; par exemple, sous Windows :
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurez le workflow [!DNL Experience Manager Assets]. {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispose d’un workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** préconfiguré, qui comprend plusieurs étapes de workflow spécifiques à [!DNL InDesign] :

* [Extraction de médias](#media-extraction)
* [Extraction de page](#page-extraction)

Ce workflow est configuré avec les valeurs par défaut qui peuvent être adaptées à votre configuration pour diverses instances d’auteur (il s’agit d’un workflow standard, aussi des informations supplémentaires sont disponibles sous [Modifier un workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si vous utilisez les valeurs par défaut (port SOAP compris), aucune configuration n’est nécessaire.

Après la configuration, le chargement de fichiers [!DNL InDesign] dans [!DNL Experience Manager Assets] (via les méthodes habituelles) déclenche le workflow pour le traitement de la ressource et la préparation des différents rendus. Testez votre configuration en chargeant un fichier INDD dans [!DNL Experience Manager Assets] afin de confirmer que vous voyez les différents rendus créés par IDS sous `<*your_asset*>.indd/Renditions`.

#### Extraction de médias {#media-extraction}

Cette étape commande l’extraction de médias à partir du fichier INDD.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de médias]**.

![Arguments d’extraction de médias et chemins de scripts](assets/media_extraction_arguments_scripts.png)

Arguments d’extraction de médias et chemins de scripts

* **Bibliothèque ExtendScript** : il s’agit d’une simple bibliothèque de méthodes HTTP GET/POST, requise par les autres scripts.

* **Développer les scripts** : vous pouvez indiquer ici différentes combinaisons de script. Si vous souhaitez que vos propres scripts soient exécutés sur [!DNL InDesign Server], enregistrez-les sous `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Ne modifiez pas la bibliothèque ExtendScript. Cette bibliothèque fournit la fonctionnalité HTTP requise pour communiquer avec Sling. Ce paramètre spécifie la bibliothèque à envoyer à [!DNL InDesign Server] pour qu’il l’utilise.

Le script `ThumbnailExport.jsx` exécuté par l’étape de workflow Extraction des médias génère un rendu miniature au format .jpg. Ce rendu est utilisé par l’étape du workflow Traiter les miniatures afin de générer les rendus statiques requis par [!DNL Experience Manager].

Vous pouvez configurer l’étape du workflow Traiter les miniatures de manière à générer des rendus statiques de différentes tailles. Assurez-vous de ne pas supprimer les valeurs par défaut car elles sont requises par l’interface utilisateur d’[!DNL Experience Manager Assets]. Enfin, l’étape Supprimer le rendu d’aperçu d’image efface le rendu de miniature JPG, car il n’est plus nécessaire.

#### Extraction de page {#page-extraction}

Cette opération crée une page [!DNL Experience Manager] à partir des éléments extraits. Un gestionnaire d’extraction est utilisé pour extraire les données d’un rendu (actuellement HTML ou IDML). Ces données sont ensuite utilisées pour créer une page avec PageBuilder.

Pour la personnaliser, vous pouvez modifier l’onglet **[!UICONTROL Arguments]** dans l’étape **[!UICONTROL Extraction de page]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestionnaire d’extraction de page** : dans la liste déroulante, sélectionnez le gestionnaire que vous souhaitez utiliser. Un gestionnaire d’extraction fonctionne sur un rendu spécifique, sélectionné par un `RenditionPicker` associé (voir l’API `ExtractionHandler`). Dans une installation standard [!DNL Experience Manager], les éléments suivants sont disponibles :
   * Gestionnaire d’extraction d’exportation IDML : fonctionne sur le rendu `IDML` généré lors de l’étape MediaExtract.

* **Nom de la page** : indique le nom que vous souhaitez attribuer à la page résultante. Si vous laissez le champ vide, le nom est « page » (ou une variante si « page » existe déjà).

* **Titre de la page** : indique le titre que vous souhaitez attribuer à la page résultante.

* **Racine de la page** : chemin d’accès à la racine de la page résultante. Si rien n’est indiqué, le noeud contenant les rendus de la ressource est utilisé.

* **Modèle de page** : modèle à utiliser lors de la génération de la page résultante.

* **Conception de page** : conception de page à utiliser lors de la génération de la page résultante.

### Configuration du programme de traitement du proxy pour [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Le programme de travail réside sur l’instance proxy.

1. Dans la console Outils, développez **[!UICONTROL Configurations Cloud Services]** dans le volet de gauche. Développez ensuite **[!UICONTROL Configuration de proxy Cloud]**.

1. Double-cliquez sur **[!UICONTROL IDS Worker]** pour ouvrir la configuration.

1. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir la boîte de dialogue de configuration et définir les paramètres requis :

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Points d’entrée SOAP à utiliser pour communiquer avec [!DNL InDesign Server]. Vous pouvez ajouter, supprimer ou trier les éléments au besoin.

1. Cliquez sur OK pour enregistrer.

### Configuration de l’externaliseur de lien Day CQ {#configuring-day-cq-link-externalizer}

Si [!DNL InDesign Server] et [!DNL Experience Manager] sont exécutés sur des hôtes différents ou si ces deux applications ne fonctionnent pas sur les ports par défaut, configurez [!UICONTROL l’externaliseur de liens Day CQ] afin de définir le nom d’hôte, le port et le chemin d’accès au contenu pour [!DNL InDesign Server].

1. Accédez à la console web `https://[aem_server]:[port]/system/console/configMgr`.
1. Localisez la configuration **[!UICONTROL Externalisateur de lien Day CQ]**. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir.
1. Les paramètres de l’externaliseur de liens permettent de créer des URL absolues pour le déploiement d’[!DNL Experience Manager] et pour [!DNL InDesign Server]. Utilisez le champ **[!UICONTROL Domaines]** pour spécifier le nom d’hôte de [!DNL Adobe InDesign Server]. Cliquez sur **Enregistrer**.

   Dans les URL absolues, utilisez `localhost` comme nom d’hôte de votre instance locale (d’auteur) et nom d’hôte ou adresse IP de l’instance de publication, comme illustré ci-dessous.

   ![Paramètre de l’externaliseur de lien](assets/link-externalizer-config.png)

### Activation du traitement parallèle des tâches [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Vous pouvez désormais activer le traitement parallèle des tâches pour IDS. Déterminez le nombre maximal de tâches parallèles (`x`) et qu’[!DNL InDesign Server] peut traiter :

* Sur une machine unique à processeur multi-cœurs, le nombre maximum de tâches parallèles (`x`) qu’[!DNL InDesign Server] peut traiter est égal au nombre de processeurs qui exécutent IDS, moins un.
* Lorsque vous exécutez IDS sur plusieurs machines, vous devez comptabiliser le nombre total de processeurs disponibles (c’est-à-dire sur toutes les machines), puis soustraire le nombre total de machines.

Pour configurer le nombre de tâches IDS parallèles :

1. Ouvrez l’onglet **[!UICONTROL Configurations]** de la console Felix ; par exemple :     `https://[aem_server]:[port]/system/console/configMgr`.

1. Sélectionnez la file d’attente du traitement d’IDS sous `Apache Sling Job Queue Configuration`.

1. Définissez :

   * **Type** - `Parallel`
   * **Nombre max. de tâches parallèles** - `<*x*>` (conformément au calcul ci-dessus)

1. Enregistrez ces modifications.
1. Pour activer la prise en charge multi-session pour Adobe CS6 et les versions ultérieures, cochez la case `enable.multisession.name`, sous la configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Créez un [groupe de programmes de traitement IDS `x` en ajoutant des points d’entrée SOAP à la configuration du programme de traitement IDS](#configuring-the-proxy-worker-for-indesign-server).

   S’il existe plusieurs machines exécutant [!DNL InDesign Server], ajoutez les points d’entrée SOAP (nombre de processeurs par ordinateur -1) pour chaque ordinateur.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Lorsque vous travaillez avec un groupe de programmes de traitement, vous pouvez activer la liste bloquée des programmes de traitement IDS.
>
>Pour ce faire, cochez la case **[!UICONTROL enable.retry.name]** sous la configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, ce qui déclenche de nouvelles tentatives pour les tâches IDS.
>
>En outre, sous la configuration `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, définissez une valeur positive pour le paramètre `max.errors.to.blacklist`, qui détermine le nombre de tentatives pour une tâche avant qu’un IDS ne soit exclu de la liste des gestionnaires de tâches.
>
>Par défaut, le traitement IDS est revalidé après une durée en minutes configurable (`retry.interval.to.whitelist.name`). Si le programme de traitement est en ligne, il est retiré de la liste bloquée.

## Activation de la prise en charge pour [!DNL InDesign Server] 10.0 ou une version ultérieure {#enabling-support-for-indesign-server-or-later}

Pour [!DNL InDesign Server] 10.0 ou une version ultérieure, suivez les étapes suivantes pour activer la prise en charge multisession.

1. Ouvrez Configuration Manager à partir de votre instance [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Sélectionnez l’option **[!UICONTROL ids.cc.enable]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Pour l’intégration de [!DNL InDesign Server] à [!DNL Experience Manager Assets], utilisez un processeur multicœur, car la fonction de prise en charge de sessions nécessaire pour l’intégration n’est pas prise en charge sur les systèmes à un seul cœur.

## Configuration des informations d’identification [!DNL Experience Manager] {#configure-aem-credentials}

Vous pouvez modifier les informations d’identification administrateur par défaut (nom d’utilisateur et mot de passe) qui permettent d’accéder à [!DNL InDesign Server] depuis votre déploiement [!DNL Experience Manager] sans interrompre l’intégration à [!DNL InDesign Server].

1. Accédez à `/etc/cloudservices/proxy.html`.
1. Dans la boîte de dialogue, indiquez le nouveau nom d’utilisateur et le nouveau mot de passe.
1. Enregistrez les identifiants.

>[!MORELIKETHIS]
>
>* [À propos d’Adobe InDesign Server](https://www.adobe.com/fr/products/indesignserver/faq.html)
