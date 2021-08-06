---
title: Configuration de Dynamic Media - mode Scene7
description: Découvrez comment configurer le mode Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration, mode Scene7
source-git-commit: 5769ddeefe2d01d32bb9a0611dc06af68a848936
workflow-type: tm+mt
source-wordcount: '6941'
ht-degree: 49%

---

# Configuration de Dynamic Media - mode Scene7{#configuring-dynamic-media-scene-mode}

Si vous utilisez Adobe Experience Manager configuré pour différents environnements, tels que le développement, l’évaluation et la production, configurez les Cloud Services Dynamic Media pour chacun de ces environnements.

## Schéma d’architecture de Dynamic Media – mode Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

Le schéma d’architecture suivant décrit le fonctionnement de Dynamic Media – mode Scene7.

Avec la nouvelle architecture, Experience Manager est responsable des ressources source Principales et des synchronisations avec Dynamic Media pour le traitement et la publication des ressources :

1. Lorsque la ressource source Principale est téléchargée vers Experience Manager, elle est répliquée vers Dynamic Media. À ce stade, Dynamic Media gère l’intégralité du traitement des ressources et de la génération du rendu, comme le codage vidéo et les variantes dynamiques d’une image.
(En mode Dynamic Media - Scene7, la taille du fichier de chargement par défaut est de 2 Go ou moins. Pour activer les tailles de fichiers de chargement de 2 Go à 15 Go, voir [(Facultatif) Configuration du mode Dynamic Media - Scene7 pour le chargement de ressources de plus de 2 Go](#optional-config-dms7-assets-larger-than-2gb).)
1. Une fois les rendus générés, Experience Manager peut accéder en toute sécurité aux rendus Dynamic Media distants et les prévisualiser (aucune donnée binaire n’est renvoyée à l’instance de Experience Manager).
1. Une fois que le contenu est prêt à être publié et approuvé, il déclenche le service Dynamic Media pour diffuser du contenu vers les serveurs de diffusion et mettre en cache le contenu sur le réseau de diffusion de contenu (CDN).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>La liste suivante de fonctionnalités nécessite l’utilisation du réseau de diffusion de contenu prêt à l’emploi fourni avec Adobe Experience Manager - Dynamic Media. Les autres réseaux de diffusion de contenu personnalisés ne sont pas pris en charge avec ces fonctionnalités.
>
>* [Imagerie dynamique](/help/assets/imaging-faq.md)
* [Invalidation du cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
* [Protection des liens dynamiques](/help/assets/hotlink-protection.md)
* [Diffusion de contenu HTTP/2](/help/assets/http2.md)
* Redirection d’URL au niveau du réseau de diffusion de contenu
* Akamai ChinaCDN (pour une diffusion optimale en Chine)


## Activation de Dynamic Media en mode Scene7 {#enabling-dynamic-media-in-scene-mode}

[Par défaut, ce module complémentaire est désactivé. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Pour tirer parti des fonctionnalités de Dynamic Media, vous devez l’activer.

>[!WARNING]
Dynamic Media : le mode Scene7 est réservé à l’instance *Auteur Experience Manager*. Par conséquent, vous devez configurer `runmode=dynamicmedia_scene7` sur l’instance d’auteur du Experience Manager, *et non* l’instance de publication du Experience Manager.

Pour activer Dynamic Media, vous devez démarrer Experience Manager à l’aide du mode d’exécution `dynamicmedia_scene7` à partir de la ligne de commande en saisissant ce qui suit dans une fenêtre de terminal (l’exemple de port utilisé est 4502) :

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Facultatif) Migration des paramètres prédéfinis et des configurations Dynamic Media de la version 6.3 vers la version 6.5 sans interruption {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

La mise à niveau de Experience Manager Dynamic Media de la version 6.3 vers la version 6.4 ou 6.5 inclut désormais la possibilité de réaliser des déploiements sans interruption. Pour migrer tous vos paramètres prédéfinis et configurations de `/etc` vers `/conf` en CRXDE Lite, veillez à exécuter la commande curl suivante.

>[!NOTE]
Si vous exécutez votre instance de Experience Manager en mode de compatibilité (c’est-à-dire si le package de compatibilité est installé), vous n’avez pas besoin d’exécuter ces commandes.

Pour toutes les mises à niveau, avec ou sans le module de compatibilité, vous pouvez copier les paramètres prédéfinis de visionneuse par défaut fournis avec Dynamic Media en exécutant la commande curl Linux® suivante :

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Pour migrer les paramètres prédéfinis et configurations de visionneuse personnalisés que vous avez créés de `/etc` vers `/conf`, exécutez la commande curl Linux® suivante :

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installer le Feature Pack 18912 pour la migration de ressources en masse {#installing-feature-pack-for-bulk-asset-migration}

L’installation du Feature Pack 18912 est *optionnel*.

Le Feature Pack 18912 vous permet soit d’ingérer des ressources par FTP en masse, soit de migrer des ressources de Dynamic Media en mode hybride ou de Dynamic Media Classic vers Dynamic Media en mode Scene7 sur Experience Manager. Il est disponible à partir de [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Pour plus d’informations, voir [Installation du Feature Pack 18912 pour la migration des ressources en masse](/help/assets/bulk-ingest-migrate.md) .

## Création d’une configuration Dynamic Media dans les Cloud Services {#configuring-dynamic-media-cloud-services}

**Avant de configurer Dynamic Media**  : une fois que vous avez reçu l’e-mail de mise en service avec les informations d’identification Dynamic Media, vous devez ouvrir l’ [application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started), puis vous connecter à votre compte pour modifier votre mot de passe. Le mot de passe fourni dans l’e-mail de mise en service est généré par le système et il est attribué uniquement de manière temporaire. Il est important que vous mettiez à jour le mot de passe afin que Dynamic Media Cloud Service soit configuré avec les informations d’identification correctes.

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**Pour créer une configuration Dynamic Media en Cloud Services :**

1. En mode d’auteur Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale et sélectionnez l’icône Outils, puis accédez à **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration Dynamic Media]**.
1. Sur la page du navigateur de configuration Dynamic Media, dans le volet de gauche, sélectionnez **[!UICONTROL global]** (ne sélectionnez pas l’icône de dossier située à gauche de **[!UICONTROL global]**), puis sélectionnez **[!UICONTROL Créer]**.
1. Sur la page **[!UICONTROL Créer une configuration Dynamic Media]**, saisissez un titre, l’adresse email du compte Dynamic Media et un mot de passe, puis sélectionnez votre région. Ces informations vous sont fournies par Adobe dans l’e-mail de mise en service. Contactez l’assistance clientèle d’Adobe si vous n’avez pas reçu l’e-mail.

   Sélectionnez **[!UICONTROL Connexion à Dynamic Media]**.

   >[!NOTE]
   Une fois que vous avez reçu l’e-mail de mise en service avec les informations d’identification Dynamic Media, ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), puis connectez-vous à votre compte pour modifier votre mot de passe. Le mot de passe fourni dans l’e-mail de mise en service est généré par le système et il est attribué uniquement de manière temporaire. Il est important que vous mettiez à jour le mot de passe afin que Dynamic Media Cloud Service soit configuré avec les informations d’identification correctes.

1. Lorsque la connexion est établie, définissez les options suivantes. Les en-têtes avec un astérisque (*) sont obligatoires :

   * **[!UICONTROL Société]** : nom du compte Dynamic Media. Vous disposez de plusieurs comptes Dynamic Media. Par exemple, vous pouvez avoir différentes sous-marques, divisions, environnements d’évaluation ou environnements de production.

   * **[!UICONTROL Chemin d’accès au dossier racine de l’entreprise]**

   * **[!UICONTROL Publication de ressources]** : vous pouvez choisir parmi les trois options suivantes :
      * **[!UICONTROL Immédiatement]** signifie que lorsque les ressources sont chargées, le système intègre les ressources et fournit instantanément l’URL/le code intégré. Aucune intervention n’est nécessaire de la part de l’utilisateur pour publier des ressources.
      * **[!UICONTROL Lors de]** l’activation : signifie que vous devez publier explicitement la ressource avant qu’un lien URL/code intégré ne soit fourni.<br><!-- CQDOC-17478, Added March 9, 2021-->À partir de la version 6.5.8 de Experience Manager, l’instance de publication de Experience Manager reflète des valeurs de métadonnées Dynamic Media précises, telles que  `dam:scene7Domain` et  `dam:scene7FileStatus` dans le mode de publication  **[!UICONTROL Lors de l’]** activation uniquement. Pour activer cette fonctionnalité, installez le Service Pack 8, puis redémarrez Experience Manager. Accédez au Gestionnaire de configuration Sling. Recherchez la configuration pour `Scene7ActivationJobConsumer Component` ou créez-en une). Cochez la case **[!UICONTROL Répliquer les métadonnées après la publication de Dynamic Media]**, puis sélectionnez **[!UICONTROL Enregistrer]**.

         ![Case Répliquer les métadonnées après publication Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Option]** Publier sélectiveCette option vous permet de contrôler les dossiers publiés dans Dynamic Media. Il vous permet d’utiliser des fonctionnalités telles que le recadrage intelligent ou les rendus dynamiques, ou de déterminer les dossiers qui sont publiés exclusivement en Experience Manager à des fins de prévisualisation. Ces mêmes ressources *ne sont pas* publiées dans Dynamic Media pour diffusion dans le domaine public.<br>Vous pouvez définir cette option ici dans la  **[!UICONTROL configuration du cloud de]** Dynamic Media ou, si vous préférez, vous pouvez choisir de définir cette option au niveau du dossier, dans les  **[!UICONTROL Propriétés]** d’un dossier.<br>Voir  [Utilisation de la publication sélective dans Dynamic Media](/help/assets/selective-publishing.md).<br>Si vous modifiez cette configuration par la suite ou au niveau du dossier, ces modifications n’affectent que les nouvelles ressources que vous chargez à partir de ce moment-là. L’état de publication des ressources existantes dans le dossier reste tel quel jusqu’à ce que vous modifiiez manuellement ces ressources à partir de la boîte de dialogue **[!UICONTROL Publication rapide]** ou **[!UICONTROL Gérer la publication]**.
   * **[!UICONTROL Serveur d’aperçu sécurisé]** : permet de définir le chemin URL de votre serveur d’aperçu des rendus sécurisé. En d’autres termes, une fois les rendus générés, Experience Manager peut accéder en toute sécurité aux rendus Dynamic Media distants et les prévisualiser (aucune donnée binaire n’est renvoyée à l’instance de Experience Manager).
À moins que vous ayez pris des dispositions spéciales pour utiliser le serveur de votre entreprise ou un serveur spécial, Adobe vous conseille de conserver ce paramètre tel que spécifié.

   * **[!UICONTROL Synchroniser tout le contenu]**  :  <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->sélectionné par défaut. Désélectionnez cette option si vous souhaitez inclure ou exclure des ressources de la synchronisation avec Dynamic Media. La désélection de cette option vous permet de choisir l’un des deux modes de synchronisation Dynamic Media :

   * **[!UICONTROL Mode de synchronisation Dynamic Media]**
      * **[!UICONTROL Activé par défaut]** : la configuration s’applique par défaut à tous les dossiers, sauf si vous marquez un dossier spécifique à exclure. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Désactivé par défaut]** : la configuration n’est appliquée à aucun dossier tant que vous ne marquez pas explicitement un dossier sélectionné pour synchronisation avec Dynamic Media.
Pour marquer un dossier sélectionné en vue de sa synchronisation avec Dynamic Media, sélectionnez un dossier de ressources, puis, sur la barre d’outils, sélectionnez **[!UICONTROL Propriétés]**. Sous l’onglet **[!UICONTROL Détails]**, dans la liste déroulante **[!UICONTROL Mode de synchronisation Dynamic Media]**, choisissez l’une des trois options suivantes. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**. *À retenir : ces trois options ne sont pas disponibles si vous avez sélectionné auparavant **[!UICONTROL Synchroniser tout le contenu]**.* Voir aussi  [Utilisation de la publication sélective au niveau du dossier dans Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Hérité]**  : aucune valeur de synchronisation explicite sur le dossier ; au lieu de cela, le dossier hérite de la valeur de synchronisation de l’un de ses dossiers ancêtres ou du mode par défaut dans la configuration cloud. Le statut détaillé de l’héritage s’affiche par le biais d’une info-bulle.
         * **[!UICONTROL Activé pour les sous-dossiers]** : incluez tous les éléments de cette sous-arborescence dans la synchronisation avec Dynamic Media. Les paramètres propres au dossier remplacent le mode par défaut dans la configuration du cloud.
         * **[!UICONTROL Désactivé pour les sous-dossiers]** : excluez tous les éléments de cette sous-arborescence de la synchronisation avec Dynamic Media.

   >[!NOTE]
   Le contrôle de version n’est pas pris en charge dans DMS7. En outre, l’activation différée ne s’applique que si l’option **[!UICONTROL Publier des ressources]** dans la page de configuration de Dynamic Media est définie sur **[!UICONTROL Dès l’activation]**, puis uniquement jusqu’à la première activation de la ressource.
   Une fois qu’une ressource est activée, toutes les mises à jour sont immédiatement publiées en direct sur la livraison S7.

1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Pour prévisualiser en toute sécurité le contenu Dynamic Media avant qu’il ne soit publié, vous devez &quot;placer sur la liste autorisée&quot; l’instance d’auteur du Experience Manager pour vous connecter à Dynamic Media :

   * Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis connectez-vous à votre compte. Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

   * Dans la barre de navigation située en haut à droite de la page, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Configuration de la publication]** > **[!UICONTROL Serveur d’images]**.

   * Sur la page Publication sur hébergeur d’images, dans la liste déroulante Contexte de publication, sélectionnez **[!UICONTROL Test de l’hébergeur d’images]**.
   * Pour le filtre d’adresses client, sélectionnez **[!UICONTROL Ajouter]**.
   * Pour activer l’adresse, cochez la case. Saisissez l’adresse IP de l’instance d’auteur du Experience Manager (et non l’adresse IP du Dispatcher).
   * Sélectionnez **[!UICONTROL Enregistrer]**.

Vous avez à présent terminé la configuration de base ; vous êtes prêt à utiliser le mode Scene7 de Dynamic Media.

Si vous souhaitez personnaliser davantage votre configuration, vous pouvez éventuellement effectuer l’une des tâches de la rubrique [(Facultatif) Configuration de paramètres avancés dans le mode Scene7 de Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Facultatif) Configuration des paramètres avancés en mode Dynamic Media - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Si vous souhaitez personnaliser davantage l’installation et la configuration du mode Scene7 de Dynamic Media, ou en optimiser les performances, vous pouvez effectuer une ou plusieurs des tâches *facultatives* suivantes :

* [(Facultatif) Configurez le mode Dynamic Media - Scene7 pour le chargement de ressources d’une taille supérieure à 2 Go.](#optional-config-dms7-assets-larger-than-2gb)

* [(Facultatif) Installation et configuration des paramètres du mode Scene7 de Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Facultatif) Réglage des performances du mode Dynamic Media - Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Facultatif) Filtrage des ressources pour la réplication](#optional-filtering-assets-for-replication)

### (Facultatif) Configurez le mode Dynamic Media - Scene7 pour le chargement de ressources d’une taille supérieure à 2 Go. {#optional-config-dms7-assets-larger-than-2gb}

En mode Dynamic Media - Scene7, la taille de fichier de chargement de ressource par défaut est de 2 Go ou moins. Cependant, vous pouvez éventuellement configurer le chargement de ressources de plus de 2 Go et de 15 Go.

Si vous avez l’intention d’utiliser cette fonction, tenez compte des conditions préalables et des points suivants :

* Vous devez exécuter Experience Manager 6.5 avec Service Pack 6.5.4.0 ou version ultérieure en mode Dynamic Media - Scene7 .
* Cette fonctionnalité de chargement volumineuse n’est prise en charge que pour les clients [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html).
* Assurez-vous que votre instance de Experience Manager est configurée avec le stockage Blob Amazon S3 ou Microsoft® Azure.

   >[!NOTE]
   Configurez le stockage Blob de Microsoft Azure avec les deux clés d’accès (key1 et key2), car cette fonctionnalité de chargement volumineuse n’est pas prise en charge avec AzureSas dans la configuration de stockage Blob.

* Le [téléchargement Direct Binary Access](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) d’Oak est activé (le *téléchargement Direct Binary Access* d’Oak n’est pas requis).

   Pour activer le téléchargement Direct Binary Access, définissez la propriété `presignedHttpDownloadURIExpirySeconds > 0` dans la configuration de la banque de données. La valeur doit être suffisamment longue pour télécharger des fichiers binaires plus volumineux et éventuellement effectuer une nouvelle tentative.

* Les ressources de plus de 15 Go ne sont pas chargées. (La limite de taille est définie à l’étape 8 ci-dessous.)
* Lorsque le workflow de retraitement des ressources **[!UICONTROL Dynamic Media]** est déclenché sur un dossier, il retraite toutes les ressources volumineuses qui sont déjà synchronisées avec la société Dynamic Media. Toutefois, si des ressources volumineuses ne sont pas encore synchronisées dans le dossier, elles ne sont pas chargées. Par conséquent, pour synchroniser les ressources volumineuses existantes dans Dynamic Media, vous pouvez exécuter le workflow **[!UICONTROL Retraitement de Dynamic Media]** sur des ressources individuelles.

**Pour configurer le mode Dynamic Media - Scene7 pour le chargement de ressources de plus de 2 Go :**

1. Dans Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.

1. Dans la fenêtre du CRXDE Lite, effectuez l’une des opérations suivantes :

   * Dans le rail de gauche, accédez au chemin suivant :

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copiez et collez le chemin d’accès ci-dessus dans le champ Chemin du CRXDE Lite sous la barre d’outils, puis appuyez sur `Enter`.

1. Dans le rail de gauche, cliquez avec le bouton droit de la souris sur `fileupload`, puis, dans le menu contextuel, sélectionnez **[!UICONTROL Noeud de recouvrement]**.

   ![Option Noeud de recouvrement](/help/assets/assets-dm/uploadassets15gb_a.png)

1. Dans la boîte de dialogue Noeud de recouvrement , cochez la case **[!UICONTROL Faire correspondre les types de noeud]** pour activer l’option, puis sélectionnez **[!UICONTROL OK]**.

   ![Noeud de recouvrement, boîte de dialogue](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Dans la fenêtre du CRXDE Lite, effectuez l’une des opérations suivantes :

   * Dans le rail de gauche, accédez au chemin d’accès au noeud de recouvrement suivant :

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copiez et collez le chemin d’accès ci-dessus dans le champ Chemin du CRXDE Lite sous la barre d’outils, puis appuyez sur `Enter`.

1. Dans l’onglet **[!UICONTROL Propriétés]**, sous la colonne **[!UICONTROL Nom]**, localisez `sizeLimit`.
1. À droite du nom `sizeLimit`, dans la colonne **[!UICONTROL Valeur]**, double-cliquez sur le champ de valeur.
1. Saisissez la valeur appropriée en octets afin d’augmenter la taille limite à la taille maximale souhaitée pour le transfert. Par exemple, pour augmenter la limite de la taille de la ressource de chargement à 10 Go, saisissez `10737418240` dans le champ Valeur.
Vous pouvez saisir une valeur allant jusqu’à 15 Go (`2013265920` octets). Dans ce cas, les ressources chargées de plus de 15 Go ne sont pas chargées.


   ![Valeur limite de taille](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Près du coin supérieur gauche de la fenêtre du CRXDE Lite, sélectionnez **[!UICONTROL Enregistrer tout]**.

   *Définissez maintenant le délai d’attente pour le gestionnaire de tâches de processus externe de processus Granite Adobe en procédant comme suit :*

1. Dans Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale.
1. Effectuez l’une des opérations suivantes :

   * Accédez au chemin d’accès à l’URL suivant :

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copiez et collez le chemin d’accès ci-dessus dans le champ URL de votre navigateur. Veillez à remplacer `localhost:4502` par votre propre instance de Experience Manager.

1. Dans la boîte de dialogue **[!UICONTROL Adobe du gestionnaire de tâches de processus externe de processus Granite]**, dans le champ **[!UICONTROL Délai d’expiration maximal]**, définissez la valeur sur `18000` minutes (cinq heures). La valeur par défaut est de 10 800 minutes (trois heures).

   ![Valeur de délai d’expiration maximale](/help/assets/assets-dm/uploadassets15gb_d.png)

1. Dans le coin inférieur droit de la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]**.

   *Définissez maintenant le délai d’attente de l’étape de processus Transfert de binaire direct de Scene7 en procédant comme suit :*

1. Dans Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale.
1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]**.
1. Sur la page Modèles de processus , sélectionnez **[!UICONTROL Vidéo de codage Dynamic Media]**.
1. Dans la barre d’outils, sélectionnez **[!UICONTROL Modifier]**.
1. Sur la page du workflow, double-cliquez sur l’étape de processus **[!UICONTROL Transfert binaire direct de Scene7]** .
1. Dans la boîte de dialogue **[!UICONTROL Propriétés des étapes]**, sous l’onglet **[!UICONTROL Commun]**, sous l’en-tête **[!UICONTROL Paramètres avancés]**, dans le champ **[!UICONTROL Délai d’expiration]**, saisissez une valeur de `18000` minutes (cinq heures). La valeur par défaut est `3600` minutes (une heure).
1. **[!UICONTROL Cliquez sur OK]**.
1. Sélectionnez **[!UICONTROL Synchronisation]**.
1. Répétez les étapes 14 à 21 pour le modèle de workflow **[!UICONTROL Ressource de mise à jour de gestion des actifs numériques]** et le modèle de workflow **[!UICONTROL Retraitement Dynamic Media]** .

### (Facultatif) Installation et configuration des paramètres du mode Scene7 de Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

Lorsque vous êtes en mode d’exécution `dynamicmedia_scene7`, utilisez l’interface utilisateur de Dynamic Media Classic pour modifier vos paramètres Dynamic Media.

Certaines des tâches ci-dessus exigent que vous ouvriez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis que vous vous connectiez à votre compte.

Les tâches d’installation et de configuration incluent :

* [Configuration de la publication pour Image Server](#publishing-setup-for-image-server)
* [Configuration des paramètres généraux de l’application](#configuring-application-general-settings)
* [Configuration de la gestion des couleurs](#configuring-color-management)
* [Modification des types MIME pour les formats pris en charge](#editing-mime-types-for-supported-formats)
* [Ajout de types MIME pour les formats non pris en charge](#adding-mime-types-for-unsupported-formats)
* [Création de paramètres prédéfinis d’ensemble par lot pour générer automatiquement des visionneuses d’images et des visionneuses à 360°](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Configuration de la publication pour Image Server {#publishing-setup-for-image-server}

Les paramètres de configuration de la publication déterminent comment les ressources sont diffusées par défaut à partir de Dynamic Media. Si aucun paramètre n’est spécifié, Dynamic Media diffuse une ressource selon les paramètres par défaut définis dans Configuration de la publication. Par exemple, une requête de diffusion d’image qui ne comporte pas d’attribut de résolution produit une image avec le paramètre de résolution d’objet par défaut.

Pour configurer la configuration de la publication : dans Dynamic Media Classic, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Configuration de la publication]** > **[!UICONTROL Image Server]**.

L’écran Image Server permet de définir les paramètres par défaut pour la diffusion des images. Voir l’écran de l’interface utilisateur pour la description de chaque paramètre.

* **[!UICONTROL Attributs de requête]** : ces paramètres imposent des limites aux images qui peuvent être diffusées à partir du serveur.
* **[!UICONTROL Attributs de requête par défaut]** : ces paramètres concernent l’aspect par défaut des images.
* **[!UICONTROL Attributs de miniature courants]** : ces paramètres concernent l’aspect par défaut des images miniatures.
* **[!UICONTROL Valeurs par défaut des champs de catalogue]** : ces paramètres concernent la résolution et le type de miniature par défaut des images.
* **[!UICONTROL Attributs de gestion des couleurs]** : ces paramètres déterminent les profils de couleurs ICC utilisés.
* **[!UICONTROL Attributs de compatibilité]** : ce paramètre permet aux paragraphes de début et de fin des calques de texte d’être traités tels qu’ils l’étaient dans la version 3.6, ce qui les rend rétrocompatibles.
* **[!UICONTROL Aide à la localisation]** : ces paramètres vous permettent de gérer divers attributs de paramètres régionaux. Ils vous permettent également de définir une chaîne de mappage de paramètres régionaux afin de définir les langues à prendre en charge pour les différentes info-bulles dans les visionneuses. Pour plus d’informations sur la configuration de la **[prise en charge de la localisation]**, voir [Considérations à prendre en compte lors de la configuration de la localisation des ressources](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html?lang=en#considerations-when-setting-up-localization-of-assets).

#### Configuration des paramètres généraux de l’application {#configuring-application-general-settings}

Pour ouvrir la page Paramètres généraux de l’application, dans la barre de navigation globale de Dynamic Media Classic, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**.

**[!UICONTROL Serveurs]** : au moment de la mise en service du compte, Dynamic Media fournit automatiquement les serveurs attribués à votre entreprise. Ces serveurs sont utilisés pour créer des chaînes URL pour votre site web et vos applications. Ces appels d’URL sont spécifiques à votre compte. Ne modifiez aucun nom de serveur, sauf si l’assistance clientèle Adobe vous a demandé de le faire.

**[!UICONTROL Écraser les images]** : Dynamic Media ne permet pas que deux fichiers portent le même nom. L’identifiant de l’URL de chaque élément (le nom de fichier sans l’extension) doit être unique. Ces options spécifient la manière dont les ressources de remplacement sont chargées : elles peuvent remplacer l’original ou devenir un doublon. Les ressources en double sont renommées en ajoutant « -1 » (par exemple, chaise.tif devient chaise-1.tif). Ces options affectent les ressources chargées dans un dossier autre que celui d’origine ou les ressources dont l’extension est différente de celle du fichier d’origine (telle que JPG, TIF ou PNG).

* **[!UICONTROL Écraser dans dossier actuel, même nom/même extension de fichier de base]** : cette option est la règle la plus stricte pour le remplacement. Elle implique que vous chargiez l’image de remplacement dans le même dossier que l’original, et qu’elle ait la même extension que le fichier d’origine. Si ces conditions ne sont pas remplies, un doublon est créé.

>[!NOTE]
Pour maintenir la cohérence avec Experience Manager, sélectionnez toujours ce paramètre : **Écraser dans le dossier actuel, même nom/même extension d’image de base**

* **[!UICONTROL Écraser dans un dossier, même nom/même extension de fichier de base]** : nécessite que l’image de remplacement ait la même extension que l’image d’origine (par exemple, chaise.jpg peut remplacer uniquement chaise.jpg, et non chaise.tif). Vous pouvez néanmoins télécharger l’image de remplacement dans un dossier différent de celui de l’image d’origine. L’image mise à jour se trouve dans le nouveau dossier ; le fichier d’origine n’est plus disponible à l’emplacement d’origine.
* **[!UICONTROL Écraser dans un dossier, même nom de fichier, extension indépendante]** : cette option est la règle de remplacement la plus inclusive. Elle vous permet de charger une image de remplacement dans un dossier autre que celui de l’image d’origine, de charger un fichier dont l’extension est différente de celle du fichier d’origine et de remplacer le fichier d’origine. Si le fichier d’origine se trouve dans un dossier différent, l’image de remplacement est enregistrée dans le nouveau dossier où elle a été chargée.

**[!UICONTROL Profils de couleurs par défaut]**  : voir  [Configuration de la ](#configuring-color-management) gestion des couleurs pour plus d’informations.

>[!NOTE]
Par défaut, le système affiche 15 rendus lorsque vous sélectionnez **[!UICONTROL Rendus]** et 15 paramètres prédéfinis de la visionneuse lorsque vous sélectionnez **[!UICONTROL Visionneuses]** dans la vue détaillée de la ressource. Vous pouvez augmenter cette limite. Voir [Augmentation du nombre de paramètres d’image prédéfinis qui s’affichent](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Augmentation du nombre de paramètres de visionneuse prédéfinis qui s’affichent](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Configuration de la gestion des couleurs {#configuring-color-management}

La gestion des couleurs de Dynamic Media vous permet de corriger les couleurs des ressources. Avec la correction des couleurs, les ressources intégrées conservent leur espace colorimétrique (RVB, CMJN, gris) et leur profil de couleur intégré. Lorsque vous demandez un rendu dynamique, la couleur de l’image est corrigée dans l’espace colorimétrique cible en utilisant une sortie CMJN, RVB ou grise. Voir [Configuration des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md).

Pour configurer les propriétés de couleur par défaut afin que la correction des couleurs soit activée lorsque des images sont demandées :

1. Ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis connectez-vous à votre compte à l’aide des informations d’identification fournies lors de la mise en service.
1. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]**.
1. Développez la zone **[!UICONTROL Configuration de la publication]** et sélectionnez **[!UICONTROL Image Server]**. Définissez **[!UICONTROL Contexte de publication]** sur **[!UICONTROL Imager Server]** lors de la définition des paramètres par défaut des instances de publication.
1. Faites défiler l’écran jusqu’à la propriété que vous souhaitez modifier. Par exemple, une propriété de la zone **[!UICONTROL Attributs de gestion des couleurs]**.

   Vous pouvez définir les propriétés de correction des couleurs suivantes :

   * **[!UICONTROL Espace colorimétrique CMJN par défaut]** : nom du profil de couleurs CMJN par défaut.
   * **[!UICONTROL Espace colorimétrique de niveaux de gris par défaut]** : nom du profil de niveaux de gris par défaut.
   * **[!UICONTROL Espace colorimétrique RVB par défaut]** : nom du profil de couleurs RVB par défaut.
   * **[!UICONTROL Intention de rendu de conversion de couleurs]** : indique l’intention de rendu. Les valeurs possibles sont les suivantes : **[!UICONTROL perception]**, **[!UICONTROL colorimétrie relative]**, **[!UICONTROL saturation]** et **[!UICONTROL colorimétrie absolue]**. Adobe recommande d’utiliser **[!UICONTROL colorimétrie relative]** comme valeur par défaut.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

Par exemple, vous pouvez définir l’**[!UICONTROL Espace colorimétrique RVB par défaut]** sur *sRVB* et l’**[!UICONTROL Espace colorimétrique CMJN par défaut]** sur *WebCoated*.

Cela aura les effets suivants :

* Active la correction des couleurs pour les images RVB et CMJN.
* Les images RVB qui n’ont pas de profil colorimétrique sont considérées comme se trouvant dans l’espace colorimétrique *sRVB*.
* Les images CMJN qui n’ont pas de profil colorimétrique sont considérées comme se trouvant dans l’espace colorimétrique *WebCoated*.
* Les rendus dynamiques qui renvoient une sortie RVB le font dans l’espace colorimétrique *sRVB*.
* Les rendus dynamiques qui renvoient une sortie CMJN, la renvoient dans l’espace colorimétrique *WebCoated*.

#### Modification des types MIME pour les formats pris en charge {#editing-mime-types-for-supported-formats}

Vous pouvez définir les types de ressources traités par Dynamic Media et personnaliser les paramètres de traitement des ressources avancé. Vous pouvez, par exemple, spécifier les paramètres de traitement des ressources de façon à ce qu’ils effectuent les opérations suivantes :

* Conversion d’un PDF Adobe en ressource de catalogue électronique.
* Conversion d’un document Adobe Photoshop (.psd) en ressource de modèle de bannière afin de permettre la personnalisation.
* Pixellisation d’un fichier Adobe Illustrator (.ai) ou d’un fichier PostScript® encapsulé Adobe Photoshop (.eps).
* [Les ](/help/assets/video-profiles.md) profils vidéo et  [ ](/help/assets/image-profiles.md) d’imagerie peuvent être utilisés pour définir le traitement des vidéos et des images, respectivement.

Voir la section [Chargement des ressources](/help/assets/manage-assets.md#uploading-assets).

**Pour modifier les types MIME pour les formats pris en charge :**

1. Dans Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans le rail de gauche, accédez à ce qui suit :

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Types MIME](assets/mimetypes.png)

1. Sous le dossier mimeTypes, sélectionnez un type MIME.
1. Sur le côté droit de la page CRXDE Lite, dans la partie inférieure :

   * Double-cliquez sur le champ **[!UICONTROL activé]**. Par défaut, tous les types MIME des ressources sont activés (définis sur **[!UICONTROL true]**), ce qui signifie que les ressources sont synchronisées avec Dynamic Media pour traitement. Si vous souhaitez exclure ce type MIME de ressource du traitement, définissez ce paramètre sur **[!UICONTROL false]**.

   * Appuyez deux fois sur **[!UICONTROL jobParam]** pour ouvrir le champ de texte associé. Voir [Types MIME pris en charge](/help/assets/assets-formats.md#supported-mime-types) pour connaître la liste des valeurs de paramètres de traitement que vous pouvez utiliser pour un type MIME donné.

1. Utilisez l’une des méthodes suivantes :

   * Répétez les étapes 3 et 4 pour modifier d’autres types de MIME.
   * Dans la barre de menus de la page du CRXDE Lite, sélectionnez **[!UICONTROL Enregistrer tout]**.

1. Dans le coin supérieur gauche de la page, sélectionnez **[!UICONTROL CRXDE Lite]** pour revenir à Experience Manager.

#### Ajout de types MIME pour les formats non pris en charge {#adding-mime-types-for-unsupported-formats}

Vous pouvez ajouter des types de MIME personnalisés pour les formats non pris en charge dans Experience Manager Assets. Assurez-vous que tout nouveau noeud ajouté en CRXDE Lite n’est pas supprimé par Experience Manager en déplaçant le type MIME avant `image_`. Assurez-vous également que sa valeur activée est définie sur **[!UICONTROL false]**.

**Pour ajouter des types MIME pour des formats non pris en charge:**

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Un nouvel onglet du navigateur s’ouvre sur la page **[!UICONTROL Adobe Experience Manager Web Console Configuration]** (Configuration de la console web Adobe Experience Manager).

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Sur la page, faites défiler l’écran jusqu’à atteindre *Adobe CQ Scene7 Asset MIME type Service*, comme illustré ci-dessous. A droite du nom, sélectionnez **[!UICONTROL Editer les valeurs de configuration]** (icône crayon).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Sur la page **Adobe CQ Scene7 Asset MIME type Service** , sélectionnez l’icône &lt;+> de signe plus. L’emplacement dans le tableau où vous sélectionnez le signe plus pour ajouter le nouveau type MIME est trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Entrez `DWG=image/vnd.dwg` dans le champ de texte vide que vous venez d’ajouter.

   L’exemple `DWG=image/vnd.dwg` est fourni à des fins de démonstration uniquement. Le type MIME que vous ajoutez ici peut être tout autre format non pris en charge.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Dans le coin inférieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.

   À ce stade, vous pouvez fermer l’onglet du navigateur dans lequel la page de configuration de la console web d’Adobe Experience Manager est ouverte.

1. Revenez à l’onglet du navigateur qui contient votre console de Experience Manager ouverte.
1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Dans le rail de gauche, accédez à ce qui suit :

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Faites glisser le type MIME `image_vnd.dwg` et déposez-le directement au-dessus de `image_` de l’arborescence, comme dans la capture d’écran suivante.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Avec le type MIME `image_vnd.dwg` toujours sélectionné, dans l’onglet **[!UICONTROL Propriétés]**, dans la ligne **[!UICONTROL enabled]**, sous l’en-tête de colonne **[!UICONTROL Valeur]**, appuyez deux fois sur la valeur pour ouvrir la liste déroulante **[!UICONTROL Valeur]**.
1. Tapez `false` dans le champ (ou sélectionnez **[!UICONTROL false]** dans la liste déroulante).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Près du coin supérieur gauche de la page du CRXDE Lite, sélectionnez **[!UICONTROL Enregistrer tout]**.

#### Création de paramètres prédéfinis d’ensemble par lot pour générer automatiquement des visionneuses d’images et des visionneuses à 360° {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Utilisez les paramètres prédéfinis d’ensemble par lot pour automatiser la création de visionneuses d’images ou de jeux de rotation lorsque des ressources sont téléchargées sur Dynamic Media.

Tout d’abord, définissez la convention d’affectation des noms pour la manière dont les ressources sont regroupées dans un ensemble. Créez ensuite un paramètre prédéfini d’ensemble par lot qui est un ensemble d’instructions autonome nommé de manière unique. Il doit définir comment construire la visionneuse à l’aide d’images qui correspondent aux conventions d’affectation de nom définies dans la recette de paramètres prédéfinis.

Lorsque vous téléchargez des fichiers, Dynamic Media crée automatiquement une visionneuse avec tous les fichiers qui correspondent à la convention de nommage définie dans les paramètres prédéfinis actifs.

##### Configuration de l’affectation de nom par défaut

Créez une convention de nommage par défaut qui est utilisée dans n’importe quelle recette de paramètre prédéfini d’ensemble par lot. La convention d’affectation de nom par défaut sélectionnée dans la définition de paramètre prédéfini d’ensemble par lot est probablement tout ce dont votre entreprise a besoin pour générer des ensembles par lot. Un paramètre prédéfini d’ensemble par lot est créé pour utiliser la convention de nommage par défaut que vous définissez. Vous pouvez créer autant de paramètres prédéfinis d’ensemble par lot que nécessaire avec des conventions de nommage différentes et personnalisées pour une visionneuse de contenu spécifique au cas où il existe une exception dans le nommage par défaut défini par l’entreprise.

Bien que la configuration d’une convention d’affectation de nom par défaut ne soit pas nécessaire pour utiliser la fonctionnalité de paramètres prédéfinis d’ensemble par lot, il est recommandé d’utiliser la convention d’affectation de nom par défaut. Il vous permet de définir autant d’éléments de votre convention d’affectation de nom que vous souhaitez regrouper dans un ensemble afin de pouvoir rationaliser la création d’un ensemble de lots.

Vous pouvez également utiliser **[!UICONTROL Afficher le code]** sans champ de formulaire disponible. Dans cet affichage, vous créez vos définitions de convention d’affectation de nom entièrement à l’aide d’expressions régulières.

Deux éléments sont disponibles pour la définition : correspondance et nom de base. Ces champs vous permettent de définir tous les éléments de la convention de nommage et d’identifier la partie de la convention utilisée pour nommer la visionneuse dans laquelle ils se trouvent. La convention de dénomination individuelle d’une entreprise utilise souvent une ou plusieurs lignes de définition pour chacun de ces éléments. Vous pouvez utiliser autant de lignes que vous le souhaitez pour votre définition unique et les regrouper dans des éléments distincts, par exemple, pour l’image principale, les éléments Couleur, Affichage secondaire et Échantillon.

**Pour configurer l’affectation de nom par défaut:**

1. Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis connectez-vous à votre compte.

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1. Dans la barre de navigation située en haut de la page, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres prédéfinis d’ensemble par lot]** > **[!UICONTROL Affectation de nom par défaut]**.
1. Sélectionnez **[!UICONTROL Afficher le formulaire]** ou **[!UICONTROL Afficher le code]** pour indiquer le mode de visualisation et de saisie des informations sur chaque élément.

   Vous pouvez cocher la case **[!UICONTROL Afficher le code]** pour afficher la valeur d’expression régulière qui se crée à côté de vos sélections dans le formulaire. Vous pouvez saisir ou modifier ces valeurs pour définir les éléments de la convention de nommage si l’affichage sous forme de formulaire vous limite pour quelque raison que ce soit. Si vos valeurs ne peuvent pas être analysées dans l’affichage de formulaire, les champs de formulaire seront inactifs.

   >[!NOTE]
   Les champs de formulaire désactivés ne permettent pas de confirmer que vos expressions régulières sont correctes. Vous verrez les résultats de l’expression régulière que vous créez pour chaque élément après la ligne de résultat. L’expression régulière est visible en entier en bas de la page.

1. Développez chaque élément selon vos besoins et indiquez les conventions de nommage que vous souhaitez utiliser.
1. Si nécessaire, effectuez l’une des opérations suivantes :

   * Sélectionnez **[!UICONTROL Ajouter]** pour ajouter une autre convention d’affectation des noms pour un élément.
   * Sélectionnez **[!UICONTROL Supprimer]** pour supprimer une convention d’affectation de nom pour un élément.

1. Utilisez l’une des méthodes suivantes :

   * Sélectionnez **[!UICONTROL Enregistrer sous]** et saisissez le nom du paramètre prédéfini.
   * Sélectionnez **[!UICONTROL Enregistrer]** si vous modifiez un paramètre prédéfini existant.

##### Création d’un paramètre prédéfini d’ensemble par lot

Dynamic Media utilise les paramètres prédéfinis d’ensemble par lot pour organiser les ressources en visionneuses d’images (images de remplacement, options de couleur, rotation à 360°) pour l’affichage dans des visionneuses. Les paramètres prédéfinis d’ensemble par lot s’exécutent automatiquement avec les processus de transfert des ressources dans Dynamic Media.

Vous pouvez créer, modifier et gérer vos paramètres prédéfinis d’ensemble par lot. Il existe deux formes de définitions de paramètres prédéfinis d’ensemble par lot : l’une pour une convention d’affectation de nom par défaut que vous pouvez configurer, l’autre pour les conventions d’affectation de nom personnalisées que vous créez à la volée.

Vous pouvez utiliser la méthode de champ de formulaire pour définir un paramètre prédéfini d’ensemble par lot ou la méthode de code, qui vous permet d’utiliser des expressions régulières. Comme dans le nommage par défaut, vous pouvez sélectionner Afficher le code en même temps que vous définissez la vue Formulaire et utilisez des expressions régulières pour créer vos définitions. Vous pouvez également désélectionner l’une des deux vues pour utiliser uniquement l’une ou l’autre.

**Pour créer un paramètre prédéfini d’ensemble par lot:**

1. Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis connectez-vous à votre compte.

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1. Dans la barre de navigation située en haut de la page, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres prédéfinis d’ensemble par lot]** > **[!UICONTROL Paramètre prédéfini d’ensemble par lot]**.

   **[!UICONTROL Afficher le formulaire]**, tel que défini dans le coin supérieur droit de la page Détails, est la vue par défaut.

1. Dans le panneau Liste des paramètres prédéfinis, sélectionnez **[!UICONTROL Ajouter]** pour activer les champs de définition dans le panneau Détails situé à droite de l’écran.
1. Dans le panneau Détails, nommez le paramètre prédéfini dans le champ Nom du paramètre prédéfini.
1. Dans le menu déroulant Type d’ensemble par lot, sélectionnez un type de paramètre prédéfini.
1. Utilisez l’une des méthodes suivantes :

   * Si vous utilisez une convention d’affectation de nom par défaut que vous avez précédemment définie sous **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres prédéfinis d’ensemble par lot]** > **[!UICONTROL Affectation de nom par défaut]**, développez **[!UICONTROL Conventions d’affectation de nom]**, puis dans la liste déroulante Affectation de nom de fichier, sélectionnez **[!UICONTROL Par défaut]**.

   * Pour définir une nouvelle convention d’affectation de nom lors de la configuration du paramètre prédéfini, développez **[!UICONTROL Conventions d’affectation de nom]**, puis, dans la liste déroulante Affectation de nom de fichier, sélectionnez **[!UICONTROL Personnalisé]**.

1. Pour l’ordre des séquences, définissez l’ordre d’affichage des images une fois la visionneuse regroupée dans Dynamic Media.

   Par défaut, les ressources sont classées par ordre alphanumérique. Cependant, vous pouvez utiliser une liste d’expressions régulières séparées par des virgules pour définir l’ordre.

1. Dans Options de création et d’affectation de nom de l’ensemble, indiquez le suffixe ou le préfixe du nom de base que vous avez défini dans la convention d’affectation de nom. Définissez également l’emplacement de création de la visionneuse dans la structure de dossiers de Dynamic Media.

   Si vous définissez un grand nombre d’ensembles, séparez-les des dossiers contenant les ressources elles-mêmes. Par exemple, créez un dossier Visionneuses d’images et insérez-y les visionneuses générées.

1. Dans le panneau Détails, sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionnez **[!UICONTROL Principal]** en regard du nouveau nom du paramètre prédéfini.

   L’activation du paramètre prédéfini garantit que, lorsque vous chargez des ressources vers Dynamic Media, le paramètre prédéfini d’ensemble par lot est appliqué pour générer la visionneuse.

##### Création d’un paramètre prédéfini d’ensemble par lot pour la génération automatique d’une visionneuse à 360° en 2D

Vous pouvez utiliser le type d’ensemble par lot **[!UICONTROL Visionneuse à 360° multi-axe]** pour créer une recette qui automatise la génération des visionneuses à 360° en 2D. Le regroupement des images utilise des expressions régulières de ligne et de colonne afin que les ressources d’image soient correctement alignées à l’emplacement correspondant dans le tableau multidimensionnel. Il n’existe aucune limite minimale ou maximale quant au nombre de lignes ou de colonnes nécessaires dans la visionneuse à 360° multi-axe.

Par exemple, supposons que vous souhaitiez créer une visionneuse à 360° multi-axe nommée `spin-2dspin`. Vous disposez d’un ensemble d’images de visionneuse à 360° qui contient trois lignes, avec 12 images par ligne. Les images sont nommées comme suit :

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Avec ces informations, votre recette de type d’ensemble par lot peut être créée comme suit :

![chlimage_1-560](assets/chlimage_1-560.png)

Le regroupement de la partie du nom de ressource partagée de la visionneuse à 360° est ajouté au champ **[!UICONTROL Correspondance]** (comme indiqué en surbrillance). La partie variable du nom de ressource contenant la ligne et la colonne est ajoutée respectivement aux champs **[!UICONTROL Ligne]** et **[!UICONTROL Colonne]**.

Lorsque la visionneuse à 360° est téléchargée et publiée, vous activez le nom de la recette de visionneuse à 360° en 2D répertoriée sous **[!UICONTROL Paramètres prédéfinis d’ensemble par lot]** dans la boîte de dialogue **[!UICONTROL Télécharger les options de la tâche]**.

**Pour créer un paramètre prédéfini d’ensemble par lot pour la génération automatique d’une visionneuse à 360° en 2D:**

1. Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) puis connectez-vous à votre compte.

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1. Dans la barre de navigation située en haut de la page, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres prédéfinis d’ensemble par lot]** > **[!UICONTROL Paramètre prédéfini d’ensemble par lot]**.

   **[!UICONTROL Afficher le formulaire]**, tel que défini dans le coin supérieur droit de la page Détails, est la vue par défaut.

1. Dans le panneau Liste des paramètres prédéfinis, sélectionnez **[!UICONTROL Ajouter]** pour activer les champs de définition dans le panneau Détails situé à droite de l’écran.
1. Dans le panneau Détails, nommez le paramètre prédéfini dans le champ Nom du paramètre prédéfini.
1. Dans le menu déroulant Type d’ensemble par lot, sélectionnez **[!UICONTROL Visionneuse de ressources]**.
1. Dans la liste déroulante Sous-type, sélectionnez **[!UICONTROL Visionneuse à 360° multi-axe]**.
1. Développez **[!UICONTROL Conventions d’affectation de nom]**, puis, dans la liste déroulante Affectation de nom de fichier, sélectionnez **[!UICONTROL Personnalisé]**.
1. Utilisez les attributs **[!UICONTROL Correspondance]** et, éventuellement, **[!UICONTROL Nom de base]** pour définir une expression régulière pour nommer les fichiers d’image qui constituent le regroupement.

   Par exemple, votre expression régulière Correspondance littérale peut se présenter comme suit :

   `(w+)-w+-w+`

1. Développez **[!UICONTROL Position des colonnes/lignes]**, puis définissez le format de nom de la position de la ressource image dans le tableau de la visionneuse à 360° en 2D.

   Placez la position de ligne ou de colonne entre parenthèses dans le nom de fichier.

   Par exemple, pour votre expression régulière de ligne, elle peut se présenter comme suit :

   `\w+-R([0-9]+)-\w+`

   ou

   `\w+-(\d+)-\w+`

   Pour l’expression régulière de colonne, elle peut se présenter comme suit :

   `\w+-\w+-C([0-9]+)`

   ou

   `\w+-\w+-C(\d+)`

   Les exemples ci-dessus sont fournis à des fins de démonstration uniquement. Vous pouvez créer votre expression régulière comme bon vous semble, en fonction de vos besoins.

   >[!NOTE]
   Si la combinaison d’expressions régulières de ligne et de colonne ne parvient pas à déterminer la position de la ressource dans le tableau de la visionneuse à 360° multidimensionnelle, la ressource n’est pas ajoutée à la visionneuse. Une erreur est également consignée.

1. Dans Options de création et d’affectation de nom de l’ensemble, indiquez le suffixe ou le préfixe du nom de base que vous avez défini dans la convention d’affectation de nom.

   Définissez également l’emplacement de création de la visionneuse à 360° dans la structure de dossiers de Dynamic Media Classic.

   Si vous définissez un grand nombre d’ensembles, séparez-les des dossiers contenant les ressources elles-mêmes. Par exemple, créez un dossier Visionneuses à 360° pour y placer les visionneuses générées.

1. Dans le panneau Détails, sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionnez **[!UICONTROL Principal]** en regard du nouveau nom du paramètre prédéfini.

   L’activation du paramètre prédéfini garantit que, lorsque vous chargez des ressources vers Dynamic Media, le paramètre prédéfini d’ensemble par lot est appliqué pour générer la visionneuse.

### (Facultatif) Réglage des performances du mode Dynamic Media - Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Pour que le mode Dynamic Media - Scene7 fonctionne correctement, Adobe recommande les conseils d’optimisation des performances/évolutivité de la synchronisation suivants :

* Mise à jour des paramètres de tâche prédéfinis pour le traitement de différents formats de fichier.
* Mise à jour des threads de traitement de file d’attente de workflows Granite prédéfinis (ressources vidéo).
* Mise à jour des threads de traitement de file d’attente de workflows Granite prédéfinis (images et ressources non vidéo).
* Mise à jour du nombre maximal de connexions de chargement au serveur Dynamic Media Classic.

#### Mise à jour des paramètres de tâche prédéfinis pour le traitement de différents formats de fichier

Vous pouvez régler les paramètres de tâche pour accélérer le traitement des fichiers lors du chargement. Par exemple, si vous téléchargez des fichiers PSD, mais que vous ne souhaitez pas les traiter en tant que modèles, vous pouvez définir l’extraction du calque sur false (désactivé). Dans ce cas, le paramètre de tâche affiné se présente comme suit : `process=None&createTemplate=false`.

Si vous souhaitez activer la création de modèles, utilisez les paramètres suivants : `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe recommande d’utiliser les paramètres de tâche « affiné » suivants pour les fichiers PDF, PostScript® et PSD :

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Type de fichier | Paramètres de tâche recommandés |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Pour mettre à jour l’un de ces paramètres, procédez comme indiqué dans la [Activation de la prise en charge du paramètre de tâche de chargement Assets/Dynamic Media Classic basé sur le type MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Mise à jour de la file d’attente de workflows transitoires Granite {#updating-the-granite-transient-workflow-queue}

La file d’attente de workflows Granite est utilisée pour le workflow **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques (DAM)]**. Dans Dynamic Media, elle est utilisée pour l’intégration et le traitement des images.

**Pour mettre à jour la file d’attente de workflow transitoire Granite :**

1. Accédez à [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) et recherchez **File d’attente : File d’attente des workflows transitoires Granite**.

   >[!NOTE]
   Il est nécessaire d’effectuer une recherche par texte au lieu d’utiliser une URL directe, car le PID OSGi est généré dynamiquement.

1. Dans le champ **[!UICONTROL Maximum Parallel Jobs]** (Nombre maximal de tâches en parallèle), modifiez le nombre en fonction de la valeur souhaitée.

   Vous pouvez augmenter le **[!UICONTROL nombre maximal de tâches en parallèle]** afin de prendre en charge le chargement intensif de fichiers vers Dynamic Media. La valeur exacte dépend de la capacité matérielle. Dans certains cas, c’est-à-dire lors d’une migration initiale ou d’un chargement en masse ponctuel, vous pouvez utiliser une valeur importante. Sachez toutefois que l’utilisation d’une valeur élevée (par exemple deux fois le nombre de cœurs) peut avoir des effets négatifs sur les activités simultanées. Testez et ajustez la valeur en fonction de votre cas d’utilisation particulier.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Sélectionnez **[!UICONTROL Enregistrer]**.

#### Mise à jour de la file d’attente de workflows Granite {#updating-the-granite-workflow-queue}

La file d’attente de workflows Granite est utilisée pour les workflows non transitoires. Dans Dynamic Media, elle est utilisée pour le traitement de la vidéo avec le workflow **[!UICONTROL Vidéo de codage Dynamic Media]**.

**Pour mettre à jour la file d’attente de workflows Granite :**

1. Accédez à `https://<server>/system/console/configMgr` et recherchez **Queue: Granite Workflow Queue** (File d’attente : file d’attente de workflows Granite).

   >[!NOTE]
   Il est nécessaire d’effectuer une recherche par texte au lieu d’utiliser une URL directe, car le PID OSGi est généré dynamiquement.

1. Dans le champ **[!UICONTROL Maximum Parallel Jobs]** (Nombre maximal de tâches en parallèle), modifiez le nombre en fonction de la valeur souhaitée.

   Vous pouvez augmenter le nombre maximal de tâches en parallèle afin de prendre en charge le chargement intensif de fichiers vers Dynamic Media. La valeur exacte dépend de la capacité matérielle. Dans certains cas, c’est-à-dire lors d’une migration initiale ou d’un chargement en masse ponctuel, vous pouvez utiliser une valeur importante. Sachez toutefois que l’utilisation d’une valeur élevée (par exemple deux fois le nombre de cœurs) peut avoir des effets négatifs sur les activités simultanées. Testez et ajustez la valeur en fonction de votre cas d’utilisation particulier.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Sélectionnez **[!UICONTROL Enregistrer]**.

#### Mise à jour de la connexion de chargement vers Dynamic Media Classic {#updating-the-scene-upload-connection}

Le paramètre de connexion de chargement vers Scene7 synchronise les ressources Experience Manager avec les serveurs Dynamic Media Classic.

**Pour mettre à jour la connexion de chargement vers Dynamic Media Classic :**

1. Accédez à `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`.
1. Dans le champ **[!UICONTROL Number of connections]** (Nombre de connexions) et/ou **[!UICONTROL Active job timeout]** (Délai d’expiration des tâches actives), modifiez le nombre en fonction de vos besoins.

   Le paramètre **[!UICONTROL Nombre de connexions]** contrôle le nombre maximal de connexions HTTP autorisées pour le téléchargement Experience Manager vers Dynamic Media ; généralement, la valeur prédéfinie de dix connexions est suffisante.

   Le paramètre **[!UICONTROL Active job timeout]** détermine le temps d’attente avant que les ressources Dynamic Media chargées ne soient publiées sur le serveur de diffusion. Cette valeur est de 2 100 secondes ou 35 minutes, par défaut.

   Dans la plupart des cas d’utilisation, le paramètre de 2 100 est suffisant.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Sélectionnez **[!UICONTROL Enregistrer]**.

### (Facultatif) Filtrage des ressources pour la réplication {#optional-filtering-assets-for-replication}

Dans les déploiements autres que Dynamic Media, vous répliquez toutes les *ressources* (images et vidéo) de votre environnement de création de Experience Manager vers le noeud de publication de Experience Manager. Ce workflow est nécessaire, car les serveurs de publication du Experience Manager diffusent également les ressources.

Toutefois, dans les déploiements Dynamic Media, dans la mesure où les ressources sont diffusées par le biais du Cloud Service, il n’est pas nécessaire de répliquer ces mêmes ressources sur les noeuds de publication du Experience Manager. Un tel workflow de &quot;publication hybride&quot; évite des coûts de stockage supplémentaires et des temps de traitement plus longs pour répliquer les ressources. D’autres contenus, tels que les pages du site, continuent à être diffusés à partir des noeuds de publication du Experience Manager.

Les filtres permettent d’exclure *les ressources* de la réplication sur le noeud de publication du Experience Manager.

#### Utilisez les filtres de ressource par défaut pour la réplication {#using-default-asset-filters-for-replication}

Si vous utilisez Dynamic Media pour les images ou les vidéos, ou les deux, vous pouvez utiliser les filtres par défaut fournis en l’état par Adobe. Les filtres suivants sont activés par défaut :

|  | Filtrer | Type MIME | Rendus |
| --- | --- | --- | --- |
| Diffusion d’images Dynamic Media | filter-image<br>filter-sets | Commence par **image/**<br> Contient **applications/** et se termine par **set**. | Les &quot;filter-images&quot; prêts à l’emploi (s’applique aux ressources d’images uniques, y compris les images interactives) et les &quot;filter-sets&quot; (s’applique aux visionneuses à 360°, aux visionneuses de supports variés et aux visionneuses de carrousel) :<br> ・ Exclure de la réplication l’image d’origine et les rendus d’image statiques. |
| Diffusion vidéo Dynamic Media | filter-video | Commence par **video/** | La &quot;vidéo de filtrage&quot; prête à l’emploi :<br> ・ Exclure de la réplication la vidéo d’origine et les rendus de miniatures statiques. |

>[!NOTE]
Les filtres s’appliquent aux types MIME et ne peuvent pas être spécifiques au chemin d’accès.

#### Personnalisation des filtres de ressources pour la réplication {#customizing-asset-filters-for-replication}

1. Dans Experience Manager, sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` pour consulter les filtres.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Pour définir le type MIME du filtre, vous pouvez localiser le type MIME comme suit : 

   Dans le rail de gauche, développez `content > dam > <locate_your_asset> > jcr:content > metadata`, puis, dans le tableau, localisez `dc:format`.

   L’illustration ci-dessous est un exemple de chemin d’une ressource vers `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notez que la valeur `dc:format` de la ressource `Fiji Red.jpg` est `image/jpeg`.

   Pour que ce filtre s’applique à toutes les images, quel que soit leur format, définissez la valeur sur `image/*` où `*` est une expression régulière appliquée à toutes les images de n’importe quel format.

   Pour que le filtre s’applique uniquement aux images de type JPEG, saisissez la valeur `image/jpeg`.

1. Définissez les rendus que vous souhaitez inclure ou exclure de la réplication.

   Voici des exemples de caractères que vous pouvez utiliser afin de filtrer la réplication :

   | Caractère à utiliser | Filtrage des ressources pour la réplication |
   | --- | --- |
   | * | Caractère générique |
   | + | Inclut des ressources pour la réplication |
   | - | Exclut les ressources de la réplication |

   Accéder à `content/dam/<locate your asset>/jcr:content/renditions`.

   L’illustration ci-dessous est un exemple de rendu d’une ressource.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Si vous ne souhaitez répliquer que l’original, saisissez `+original`.
