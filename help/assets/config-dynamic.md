---
title: Configuration de Dynamic Media en mode hybride
description: Découvrez comment configurer Dynamic Media en mode hybride.
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: e1a8a73e10101a380183658d64f08a7dc5933ee0
workflow-type: tm+mt
source-wordcount: '7992'
ht-degree: 96%

---

# Configuration de Dynamic Media en mode hybride {#configuring-dynamic-media-hybrid-mode}

## Dynamic Media - Package de module complémentaire hybride (AEM 6.5.23 et versions ultérieures)

À partir du pack de services 23 d’AEM 6.5, un nouveau package complémentaire est disponible pour Dynamic Media en mode hybride. Ce package comprend le lot `cq-scene7-imaging` spécifiquement compatible avec le mode d’exécution hybride de Dynamic Media.

**Correctif clé inclus**

Correction d’un problème dans Dynamic Media - Déploiements hybrides en raison duquel les mises à jour du paramètre `catalog.expiration` sous `/conf/global/settings/dam/dm/imageserver` n’étaient pas reflétées sur les URL du serveur ou de l’auteur, malgré la réussite de la réplication sans erreurs. La mise à jour garantit la cohérence des valeurs d’expiration entre CRX/DE, la réponse du serveur et les URL de diffusion publiques. Elle améliore ensuite le comportement du cache et la fiabilité des transformations d’image. (ASSETS-44837)

**Considérations importantes**

* Le lot `cq-scene7-imaging` de l’installation de base d’AEM 6.5.23 (et versions ultérieures) n’est *pas compatible* avec Dynamic Media en mode d’exécution hybride.
* L’installation du pack de services 23 (et versions ultérieures) seul ne met *pas automatiquement à jour* le lot de `cq-scene7-imaging` existant sur les instances AEM configurées pour Dynamic Media en mode hybride (mode d’exécution `-r dynamicmedia`).

**Quand installer le package de module complémentaire hybride**

* Lors de la mise à niveau directe vers AEM 6.5.23 (et versions ultérieures) à partir d’AEM 6.5.19 ou version antérieure.
* Si des correctifs spécifiques à la fonctionnalité Dynamic Media en mode hybride sont nécessaires.
* Lors du déploiement d’une nouvelle instance Dynamic Media en mode hybride directement depuis AEM 6.5 GA (disponibilité générale) vers le pack de services 23 (et versions ultérieures).

**Télécharger le package complémentaire hybride**

Le package de module complémentaire hybride est disponible publiquement dans la distribution logicielle d’Adobe à compter du jeudi 22 mai 2025, avec la version officielle d’AEM 6.5.23. Les utilisateurs peuvent le trouver en recherchant **Package de module complémentaire hybride AEM 6.5 Dynamic Media** dans la distribution logicielle.


## Fin de la prise en charge de SSL 2.0 et 3.0 et de TLS 1.0 et 1.1.

Fin de la prise en charge de Secure Socket Layer 2.0 et 3.0, ainsi que de Transport Layer Security 1.0 et 1.1.

À compter du 30 avril 2024, Adobe Dynamic Media a arrêté la prise en charge des éléments suivants :

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
* TLS (Transport Layer Security) 1.0 et 1.1
* Les chiffrements faibles suivants dans TLS 1.2 :
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  `TLS_RSA_WITH_AES_256_GCM_SHA384`
  `TLS_RSA_WITH_AES_256_CBC_SHA256`
  `TLS_RSA_WITH_AES_256_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_AES_128_GCM_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

Voir aussi [Limites de Dynamic Media](/help/assets/limitations.md).

<!-- FOR ABOVE - CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->


Dynamic Media en mode hybride doit être activé et configuré pour être utilisé. Selon l’utilisation que vous souhaitez en faire, Dynamic Media prend en charge [plusieurs configurations](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Si vous envisagez de configurer et d’exécuter Dynamic Media en mode d’exécution Scene7, consultez [Configuration de Dynamic Media en mode Scene7](/help/assets/config-dms7.md).
>
>Si vous envisagez de configurer et d’exécuter Dynamic Media en mode d’exécution hybride, suivez les instructions de cette page.

En savoir plus sur l’utilisation des [vidéos](/help/assets/video.md) dans Dynamic Media.

>[!NOTE]
>
>Si vous utilisez Adobe Experience Manager pour différents environnements, tels que le développement, l’évaluation et l’exploitation en direct, configurez les services cloud Dynamic Media pour chaque environnement.

>[!NOTE]
>
>Si vous rencontrez des problèmes avec votre configuration Dynamic Media, recherchez dans les fichiers journaux spécifiques à Dynamic Media. Ces fichiers sont installés automatiquement lorsque vous activez Dynamic Media :
>
>* `s7access.log`
>* `ImageServing.log`
>
>Ils sont documentés dans [Surveiller et gérer votre instance d’Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

La diffusion de contenus et la publication hybride est une fonctionnalité clé lorsque vous ajoutez Dynamic Media à Adobe Experience Manager. La publication hybride vous permet de diffuser des ressources Dynamic Media, comme des images ou des vidéos, depuis le cloud plutôt que depuis les nœuds de publication Experience Manager.

D’autres contenus, comme les visionneuses Dynamic Media, les pages de site et le contenu statique, restent diffusés depuis les nœuds de publication Experience Manager.

Si vous utilisez déjà Dynamic Media, il vous est demandé d’utiliser la publication hybride comme méthode de diffusion pour tout le contenu Dynamic Media.

## Architecture de publication hybride des vidéos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Architecture de publication hybride pour les images {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configurations Dynamic Media prises en charge {#supported-dynamic-media-configurations}

Les tâches de configuration qui suivent font référence aux termes suivants :

| **Terme** | **Dynamic Media activé** | **Description** |
|---|---|---|
| Nœud Auteur Experience Manager | Coche blanche dans un cercle vert | Nœud auteur que vous déployez sur On-Premise ou via les Managed Services. |
| Nœud de publication Experience Manager | « X » blanc dans un carré rouge. | Nœud de publication que vous déployez sur On-Premise ou via les Managed Services. |
| Nœud de publication du service d’image | Coche blanche dans un cercle vert. | Nœud de publication que vous exécutez dans les data centers gérés par Adobe. Renvoie à l’URL du service d’images. |

Vous pouvez choisir d’implémenter Dynamic Media uniquement pour les images, uniquement pour les vidéos ou à la fois pour les images et les vidéos. Pour déterminer les étapes à suivre pour configurer Dynamic Media pour votre scénario, reportez-vous au tableau suivant.

<table>
 <tbody>
  <tr>
   <td><strong>Scénario</strong></td>
   <td ><strong>Fonctionnement</strong></td>
   <td><strong>Étapes de configuration</strong></td>
  </tr>
  <tr>
   <td>Diffusion UNIQUEMENT d’images en production</td>
   <td>Les images sont diffusées via des serveurs situés dans les centres de données mondiaux d’Adobe, puis mises en cache par un CDN pour une portée globale et des performances adaptatives.</td>
   <td>
    <ol>
     <li>Sur le nœud <strong>auteur</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a>.</li>
     <li>Configuration des images dans les <a href="#configuring-dynamic-media-cloud-services">Services cloud Dynamic Media</a>.</li>
     <li><a href="#configuring-image-replication">Configurer la réplication de l’image</a>.</li>
     <li><a href="#replicating-catalog-settings">Répliquer les paramètres du catalogue</a>.</li>
     <li><a href="#replicating-viewer-presets">Répliquer les paramètres prédéfinis de la visionneuse</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utiliser des filtres de ressource par défaut pour la réplication</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configurer les paramètres du serveur d’images Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Livrer les ressources</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Diffusion UNIQUEMENT d’images en préproduction (développement, QE, test, etc.)</td>
   <td>Les images sont livrées via le nœud de publication d’Experience Manager. Dans ce scénario, puisque le trafic est minimal, il n’est pas nécessaire d’envoyer les images vers le centre données d’Adobe. Il permet également un aperçu sécurisé du contenu avant le lancement de l’exploitation.</td>
   <td>
    <ol>
     <li>Sur le nœud <strong>auteur</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a>.</li>
     <li>Sur le nœud de <strong>publication</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Répliquer les paramètres prédéfinis de la visionneuse</a>.</li>
     <li>Configuration du <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtre de ressources pour les images hors production</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configurez les paramètres du serveur d’images Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Livrez les ressources.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Diffusion UNIQUEMENT de vidéos dans n’importe quel environnement (production, développement, QE, test, etc.)</td>
   <td>Les vidéos sont diffusées et mises en cache par un CDN pour des performances adaptatives et une portée globale. L’image d’affiche de la vidéo (la miniature de la vidéo qui s’affiche avant le début de la lecture) sera livrée par l’instance de publication d’Experience Manager.</td>
   <td>
    <ol>
     <li>Sur le nœud <strong>auteur</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a>.</li>
     <li>Sur le nœud de <strong>publication</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a> (l’instance de publication envoie l’image d’affiche de la vidéo et fournit les métadonnées pour la lecture de la vidéo).</li>
     <li>Configuration des vidéos dans les <a href="#configuring-dynamic-media-cloud-services">Services cloud Dynamic Media.</a></li>
     <li><a href="#replicating-viewer-presets">Répliquer les paramètres prédéfinis de la visionneuse</a>.</li>
     <li>Configuration du <a href="#setting-up-asset-filters-for-video-only-deployments">filtre de ressources pour la vidéo uniquement</a>.</li>
     <li><a href="#delivering-assets">Livrez les ressources.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Diffusion d’images ET de vidéos en production</td>
   <td><p>Les vidéos sont diffusées et mises en cache par un CDN pour des performances adaptatives et une portée globale. Les images et les miniatures des vidéos sont diffusées via les serveurs des centres de données mondiaux d’Adobe, puis mises en cache par un CDN pour une portée globale et des performances adaptatives.</p> <p>Reportez-vous aux sections précédentes pour configurer les images ou les vidéos en préexploitation. </p> </td>
   <td>
    <ol>
     <li>Sur le nœud <strong>auteur</strong> d’Experience Manager, <a href="#enabling-dynamic-media">activez Dynamic Media</a>.</li>
     <li>Configuration des vidéos dans les <a href="#configuring-dynamic-media-cloud-services">Services cloud Dynamic Media.</a></li>
     <li>Configuration des images dans les <a href="#configuring-dynamic-media-cloud-services">Services cloud Dynamic Media.</a></li>
     <li><a href="#configuring-image-replication">Configurer la réplication de l’image</a>.</li>
     <li><a href="#replicating-catalog-settings">Répliquer les paramètres du catalogue</a>.</li>
     <li><a href="#replicating-viewer-presets">Répliquer les paramètres prédéfinis de la visionneuse</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilisez les filtres de ressource par défaut pour la réplication.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configurez les paramètres du serveur d’images Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Livrez les ressources.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Activation de Dynamic Media {#enabling-dynamic-media}

Par défaut, [Dynamic Media](https://business.adobe.com/fr/products/experience-manager/assets/dynamic-media.html) est désactivé. Pour bénéficier des fonctionnalités de Dynamic Media, vous devez activer Dynamic Media en utilisant le mode d’exécution `dynamicmedia` comme vous le feriez par exemple pour le mode d’exécution `publish`. Avant l’activation, vérifiez les [exigences techniques](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>L’activation de Dynamic Media via le mode d’exécution remplace la fonctionnalité dans Experience Manager 6.1 et Experience Manager 6.0 qui consistait à définir l’indicateur `dynamicMediaEnabled` sur **[!UICONTROL true]**. Cet indicateur ne correspond à aucune fonctionnalité dans Experience Manager 6.2 et versions ultérieures. Par ailleurs, vous n’avez pas besoin de redémarrer le démarrage rapide pour activer Dynamic Media.

L’activation de Dynamic Media rend les fonctionnalités de contenu multiDynamic Media disponibles via l’interface utilisateur. En outre, chaque ressource image chargée reçoit un rendu *cqdam.pyramid.tiff* utilisé pour accélérer la diffusion des rendus d’image dynamique. Ces PTIFF présentent des avantages significatifs tels que les suivants :

* La possibilité de gérer une seule image source Principale et de générer des rendus infinis à la volée sans stockage supplémentaire
* La possibilité d’utiliser la visualisation interactive (zoom, panoramique et rotation, par exemple)

Pour utiliser Dynamic Media Classic dans Experience Manager, n’activez pas Dynamic Media, à moins que vous n’utilisiez un [scénario spécifique](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media est désactivé, sauf si vous l’activez via le mode d’exécution.

Pour activer Dynamic Media, vous devez activer le mode d’exécution Dynamic Media, soit depuis la ligne de commande, soit en modifiant le nom de fichier de démarrage rapide.

**Activation de Dynamic Media :**

1. Dans la ligne de commande, lorsque vous lancez le démarrage rapide, procédez de la façon suivante :

   * Ajoutez `-r dynamicmedia` à la fin de la ligne de commande lorsque vous démarrez le fichier jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Si vous publiez sur s7delivery, vous devez également inclure les arguments trustStore suivants :

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Demandez `https://localhost:4502/is/image` et assurez-vous que le serveur d’images est désormais en cours d’exécution.

   >[!NOTE]
   >
   >En cas de problème avec Dynamic Media, consultez les journaux suivants dans le répertoire `crx-quickstart/logs/` :
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - Le journal ImageServer fournit des statistiques et des informations permettant d’analyser le comportement du processus ImageServer interne.
   >
   Exemple de nom de fichier de journal Image Server : `ImageServer-57346-2020-07-25.log`
   >
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - Le journal s7access enregistre chaque requête envoyée à Dynamic Media via `/is/image` et `/is/content`.
   >
   Ces journaux sont utilisés uniquement lorsque Dynamic Media est activé. Ils ne sont pas inclus dans le package **Télécharger tout le package** généré depuis la page `system/console/status-Bundlelist` ; si vous contactez le service clientèle pour un problème lié à Dynamic Media, ajoutez ces deux journaux à votre demande.

### Si vous avez installé Experience Manager sur un port ou un chemin d’accès au contexte différent... {#if-you-installed-aem-to-a-different-port-or-context-path}

Si vous déployez [Experience Manager sur un serveur d’application](/help/sites-deploying/application-server-install.md) et que vous avez activé Dynamic Media, vous devez configurer le **domaine self** dans le service Externalizer. Dans le cas contraire, la fonctionnalité de génération de miniature pour les ressources ne fonctionnera pas correctement pour les ressources de Dynamic Media.

En outre, si vous exécutez le démarrage rapide sur un port ou un chemin d’accès au contexte différent, vous devez également changer le **domaine self**.

Lorsque Dynamic Media est activé, les rendus de miniature statiques pour les ressources images sont générés à l’aide de Dynamic Media. Pour que la génération de miniature fonctionne correctement pour le contenu Dynamic Media, Experience Manager doit s’envoyer une requête d’URL et doit connaître à la fois le numéro de port et le chemin d’accès au contexte.

Dans Experience Manager :

* Le **domaine self** du service [Externalizer](/help/sites-developing/externalizer.md) est utilisé pour récupérer à la fois le numéro de port et le chemin d’accès au contexte.
* Si aucun **domaine self** n’est configuré, le numéro de port et le chemin d’accès au contexte sont récupérés via le service HTTP Jetty.

Dans un déploiement WAR QuickStart Experience Manager, le numéro de port et le chemin d’accès au contexte ne peuvent pas être dérivés, vous devez configurer un **domaine self**. Reportez-vous à la [documentation sur le service Externalizer](/help/sites-developing/externalizer.md) relative à la configuration du domaine **self**.

>[!NOTE]
>
Dans un [déploiement autonome Quickstart Experience Manager](/help/sites-deploying/deploy.md), un **domaine self** n’a généralement pas besoin d’être configuré, car le numéro de port et le chemin d’accès au contexte peuvent s’autoconfigurer. Toutefois, si toutes les interfaces réseau sont désactivées, vous devez configurer le **domaine self**.

## Désactivation de Dynamic Media  {#disabling-dynamic-media}

Dynamic Media est désactivé par défaut. Si vous avez déjà activé Dynamic Media, vous pouvez toutefois le désactiver ultérieurement.

Pour désactiver Dynamic Media après l’avoir activé, supprimez l’indicateur de mode d’exécution `-r dynamicmedia`.

**Pour désactiver Dynamic Media :**

1. Dans la ligne de commande, lorsque vous lancez le démarrage rapide, vous pouvez procéder de l’une des façons suivantes :

   * N’ajoutez pas `-r dynamicmedia` à la ligne de commande lorsque vous démarrez le fichier jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Requête `https://localhost:4502/is/image`. Vous recevez un message indiquant que Dynamic Media est désactivé.

   >[!NOTE]
   >
   Une fois que le mode d’exécution Dynamic Media est désactivé, l’étape de workflow qui génère le rendu `cqdam.pyramid.tiff` est automatiquement ignorée. La prise en charge du rendu dynamique est également désactivée, ainsi que d’autres fonctionnalités Dynamic Media.
   >
   Notez également que lorsque le mode d’exécution Dynamic Media est désactivé après configuration du serveur Experience Manager, tous les ressources qui ont été chargés sous ce mode d’exécution son alors invalides.

## (Facultatif) Migration des paramètres prédéfinis et des configurations Dynamic Media versions 6.3 à 6.5, sans interruption {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Si vous effectuez une mise à niveau d’Experience Manager - Dynamic Media de la version 6.3 vers la version 6.5 (qui inclut désormais la possibilité de réaliser des déploiements sans interruption), vous devez exécuter la commande curl suivante. La commande migre tous vos paramètres prédéfinis et configurations à partir de `/etc` vers `/conf` dans CRXDE Lite.

>[!NOTE]
>
Si vous exécutez votre instance d’Experience Manager en mode de compatibilité (c’est-à-dire si le package de compatibilité est installé), il n’est pas nécessaire d’exécuter ces commandes.

Pour toutes les mises à niveau, avec ou sans package de compatibilité, vous pouvez copier les paramètres prédéfinis de la visionneuse prête à l’emploi fournie initialement avec Dynamic Media en exécutant la commande curl Linux® suivante :

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Pour migrer des paramètres prédéfinis de visionneuse et des configurations personnalisés que vous avez créés dans `/etc` vers `/conf`, exécutez la commande curl Linux® suivante :

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configuration de la réplication de l’image {#configuring-image-replication}

La diffusion d’images Dynamic Media se fait en publiant des ressources images, notamment des miniatures vidéo, à partir de l’auteur Experience Manager, puis en les répliquant vers le service de réplication On-Demand d’Adobe (l’URL du service de réplication). Les ressources sont ensuite diffusées par l’intermédiaire du service de diffusion d’images On-Demand (l’URL du service d’images).

Procédez comme suit :

1. [Définissez une authentification](#setting-up-authentication).
1. [Configurez l’agent de réplication](#configuring-the-replication-agent).

L’agent de réplication publie les ressources Dynamic Media telles que des images, des métadonnées et des visionneuses de vidéo, vers le service d’images hébergé par Adobe. L’agent de réplication n’est pas activé par défaut.

Après avoir configuré l’agent de réplication, vous devez [valider et tester que la configuration a bien été effectuée](#validating-the-replication-agent-for-dynamic-media). Cette section décrit ces procédures.

>[!NOTE]
>
La limite de mémoire par défaut pour la création de fichiers PTIFF est de 3 Go pour tous les workflows. Par exemple, vous pouvez traiter une image qui nécessite 3 Go de mémoire pendant que les autres workflows sont en pause, ou traiter 10 images en parallèle qui nécessitent chacune 300 Mo de mémoire.
>
La limite de la mémoire peut être configurée et s’adapte en fonction de la disponibilité des ressources du système et du type de contenu d’image traité. Si vous avez plusieurs ressources volumineuses et que vous avez suffisamment de mémoire dans le système, vous pouvez augmenter cette limite pour être certain de pouvoir traiter les images en parallèle.
>
Une image nécessitant plus de mémoire que la limite maximale prévue sera rejetée.
>
Pour modifier la limite de mémoire pour la création d’images PTIFF, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**> **[!UICONTROL Adobe CQ Scene7 PTiffManager]** et modifiez la valeur **[!UICONTROL maxMemory]**.

### Définition d’une authentification {#setting-up-authentication}

Configurez l’authentification de réplication sur l’auteur afin de pouvoir répliquer les images vers le service de diffusion d’images Dynamic Media. Vous obtenez d’abord un KeyStore, puis vous l’enregistrez sous le **[!UICONTROL dynamic-media-replication]** et configurez-le. L’administrateur de votre société a reçu un e-mail de bienvenue contenant le fichier KeyStore et les informations d’identification nécessaires au cours du processus de provisionnement. Si vous n’avez pas reçu ces informations, contactez le service clientèle d’Adobe.

**Pour configurer l’authentification :**

1. Contactez le service clientèle d’Adobe pour obtenir votre fichier KeyStore et votre mot de passe si vous ne disposez pas déjà du fichier et du mot de passe. Ces informations sont une partie nécessaire de la mise en service. Il associe les clés à votre compte.

1. Dans Experience Manager, sélectionnez le logo Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Paramètres d’image prédéfinis]**.

1. Sur la page Gestion des utilisateurs, accédez à l’utilisateur **[!UICONTROL dynamic-media-replication]**, puis sélectionnez pour ouvrir.

   ![dm-replication](assets/dm-replication.png)

1. Sur la page Modifier les paramètres utilisateur pour la page de réplication Dynamic Media, sélectionnez l’onglet **[!UICONTROL Keystore]** puis sélectionnez **[!UICONTROL Créer le KeyStore]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Saisissez un mot de passe, puis confirmez-le dans la boîte de dialogue **[!UICONTROL Définir le mot de passe d’accès KeyStore]**.

   >[!NOTE]
   >
   Mémorisez le mot de passe car vous devez le saisir à nouveau lorsque vous configurez l’agent de réplication ultérieurement.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. Sur la page **[!UICONTROL Modifier les paramètres utilisateurs pour la réplication Dynamic Media]**, développez l’espace **Ajouter une clé privée depuis le fichier KeyStore** et ajoutez les éléments suivants (voir image suivante) :

   * Dans le champ **[!UICONTROL Nouvel alias]**, saisissez le nom d’un alias que vous souhaitez utiliser ultérieurement dans la configuration de réplication. Par exemple, vous pouvez utiliser `replication` comme alias.
   * Sélectionnez le **[!UICONTROL fichier KeyStore]**. Accédez au fichier KeyStore fourni par Adobe, sélectionnez-le puis sélectionnez **[!UICONTROL Ouvrir]**.
   * Dans le champ **[!UICONTROL Mot de passe du fichier KeyStore]**, entrez le mot de passe du fichier KeyStore. Ce n’est **pas** le mot de passe du KeyStore que vous avez créé à l’étape 5. C’est le mot de passe du fichier KeyStore fourni par Adobe dans l’e-mail de bienvenue qui vous a été envoyé pendant le provisionnement. Contactez le service clientèle Adobe si vous n’avez pas reçu le mot de passe du fichier KeyStore.
   * Dans le champ **[!UICONTROL Mot de passe de la clé privée]**, entrez le mot de passe de la clé privée (ce peut être le même mot de passe de clé privée que celui fourni à l’étape précédente). Adobe vous fournit ce mot de passe de clé privée dans l’e-mail de bienvenue qui vous est envoyé pendant le provisionnement. Contactez le service clientèle Adobe si vous n’avez pas reçu le mot de passe de clé privée.
   * Dans le champ **[!UICONTROL Alias de la clé privée]**, entrez l’alias de la clé privée. Par exemple, `*companyname*-alias`. Adobe vous fournit cet alias de clé privée dans l’e-mail de bienvenue qui vous est envoyé pendant le provisionnement. Contactez le service clientèle Adobe si vous n’avez pas reçu d’alias de clé privée.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Sélectionnez **[!UICONTROL Enregistrer et fermer]** pour enregistrer vos modifications pour cet utilisateur.

   Vous devez ensuite [configurer l’agent de réplication](#configuring-the-replication-agent).

### Configuration de l’agent de réplication {#configuring-the-replication-agent}

1. Dans Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** > **[!UICONTROL Agents sur l’auteur]**.
1. Dans la page Agents sur l’auteur, sélectionnez **[!UICONTROL Réplication des images hybrides Dynamic Media (s7delivery)]**.
1. Sélectionnez **[!UICONTROL Modifier]**.
1. Sélectionnez l’onglet **[!UICONTROL Paramètres]**, et entrez les informations suivantes :

   * **[!UICONTROL Activé]** : cochez cette option pour activer l’agent de réplication.
   * **[!UICONTROL Région]** : indiquez la région appropriée : Amérique du Nord, Europe ou Asie.
   * **[!UICONTROL ID du client]** : il s’agit du nom de votre société/client qui publie du contenu vers le service de réplication. C’est l’ID de client qu’Adobe vous fournit dans l’e-mail de bienvenue qui vous est envoyé lors du provisionnement. Si vous n’avez pas reçu ces informations, contactez le service clientèle d’Adobe.
   * **[!UICONTROL Alias de Keystore]** : cette valeur est identique à celle de la valeur **Nouvel alias** lors de la génération de la clé dans la section [Configuration de l’authentification](#setting-up-authentication), par exemple, `replication`. (Reportez-vous à l’étape 7 de la section [Configuration de l’authentification](#setting-up-authentication).)
   * **[!UICONTROL Mot de passe du Keystore]** : le mot de passe du Keystore créé lorsque vous avez appuyé sur **[!UICONTROL Créer le KeyStore]**. Adobe ne fournit pas ce mot de passe. Reportez-vous à l’étape 5 de la section [Configuration de l’authentification](#setting-up-authentication).

   L’image suivante montre l’agent de réplication avec des exemples de données :

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Sélectionnez **[!UICONTROL OK]**.

### Validation de l’agent de réplication pour Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Pour valider l’agent de réplication pour Dynamic Media, procédez de la façon suivante :

Sélectionnez **[!UICONTROL Tester la connexion]**. Voici un exemple de sortie :

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
>
Vous pouvez également vérifier en effectuant l’une des opérations suivantes :
>
* Vérifiez les journaux de réplication pour vous assurer que la ressource a été répliquée.
* Publiez une image. Sélectionnez l’image puis sélectionnez **[!UICONTROL Visionneuses]** dans le menu déroulant, puis sélectionnez un paramètre prédéfini de visionneuse. Sélectionnez **[!UICONTROL URL]**. Pour vérifier que vous pouvez voir l’image, copiez et collez le chemin de l’URL dans le navigateur.
>

### Dépannage de l’authentification {#troubleshooting-authentication}

Lors de la configuration de l’authentification, voici certains problèmes que vous pourriez rencontrer, ainsi que leurs solutions. Avant de rechercher une solution à ces problèmes, vérifiez que vous avez configuré la réplication.

#### Problème : Code d’état HTTP 401 avec message - Autorisation requise {#problem-http-status-code-with-message-authorization-required}

Ce problème peut être dû à l’échec de la configuration du KeyStore pour l’utilisateur `dynamic-media-replication`.

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**Solution** : vérifiez que le `KeyStore` est enregistré pour l’utilisateur **dynamic-media-replication** et qu’il est fourni avec le bon mot de passe.

#### Problème : Impossible de déchiffrer la clé - Impossible de déchiffrer les données {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**Solution** :
vérifiez le mot de passe. Le mot de passe enregistré dans l’agent de réplication n’est pas le même que celui utilisé pour créer le KeyStore.

#### Problème : InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Ce problème est causé par une erreur de configuration dans votre instance Auteur Experience Manager. Le `javax.net.ssl.trustStore` obtenu par le processus Java™ sur l’auteur n’est pas correct. Vous rencontrez l’erreur suivante dans le journal de réplication :

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

Ou le journal des erreurs :

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**Solution** :
Vérifiez que le processus Java™ sur l’auteur Experience Manager a la propriété `-Djavax.net.ssl.trustStore=` définie sur un TrustStore valide.

#### Problème : le KeyStore n’est pas configuré ou n’a pas été initialisé. {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Le problème peut être dû à un correctif ou à un pack de fonctionnalités qui a écrasé le nœud du KeyStore ou dynamic-media-user.

Exemple de journal de réplication :

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**Solution :**

1. Accédez à la page User Management :
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. Sur la page User Management, accédez à l’utilisateur `dynamic-media-replication`, puis sélectionnez-le pour l’ouvrir.
1. Sélectionnez l’onglet **[!UICONTROL Keystore]**. Si le bouton **[!UICONTROL Créer KeyStore]** apparaît, il vous faut alors répéter les étapes décrites précédemment sous [Configuration de l’authentification](#setting-up-authentication).
1. Si vous avez eu à répéter la configuration du KeyStore, vous devez répéter la [ Configuration de l’agent de réplication](/help/assets/config-dynamic.md#configuring-the-replication-agent) également.

   Reconfigurez l’agent de réplication s7delivery.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Sélectionnez **[!UICONTROL Tester la connexion]** afin que vous puissiez vérifier que la configuration est valide.

#### Problème : l’agent de publication utilise SSL à la place d’OAuth. {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Le problème peut être dû à un correctif ou à un Pack de fonctionnalités qui ne s’est pas installé correctement ou qui a écrasé les paramètres.

Exemple de journal de réplication :

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**Solution :**

1. Dans Experience Manager, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. Naviguez vers le nœud de l’agent de réplication s7delivery.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Ajoutez ce paramètre à l’agent de réplication (Booléen avec la valeur **[!UICONTROL True]**) :

   `enableOauth=true`

1. Dans le coin supérieur gauche de la page, sélectionnez **[!UICONTROL Enregistrer tout]**.

### Tester votre configuration {#testing-your-configuration}

Adobe vous recommande d’effectuer un test complet de la configuration :

Assurez-vous d’avoir déjà effectué les étapes suivantes avant de commencer ce test :

* Ajout de paramètres d’image prédéfinis.
* Configuration de la **[!UICONTROL Configuration de Dynamic Media (version antérieure à 6.3)]** dans les services Cloud. L’URL du service d’images est requise pour ce test.

**Pour tester votre configuration :**

1. Téléchargez une ressource image. (Dans Ressources, accédez à **[!UICONTROL Créer]** > **[!UICONTROL Fichiers]** et sélectionnez le fichier.)
1. Attendez que le workflow se termine.
1. Publiez la ressource image. (Sélectionnez la ressource puis **[!UICONTROL Publication rapide]**.)
1. Accédez aux rendus de cette image en ouvrant l’image et en appuyant sur **[!UICONTROL Rendus]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Sélectionnez n’importe quel rendu dynamique.
1. Pour obtenir l’URL de cette ressource, sélectionnez **[!UICONTROL URL]**.
1. Accédez à l’URL sélectionnée et vérifiez si l’image s’affiche comme prévu.

Une autre manière de tester la diffusion de vos ressources consiste à ajouter req=exists à votre URL.

## Configuration des services cloud Dynamic Media {#configuring-dynamic-media-cloud-services}

Dynamic Media Cloud Service prend en charge la publication et la diffusion hybrides d’images et de vidéos, d’analyses vidéo et de codage vidéo, entre autres.

Lors de la configuration, vous devez entrer un ID d’enregistrement, l’URL du service vidéo, l’URL du service d’images, l’URL du service de réplication et configurer l’authentification. Ces informations vous ont été envoyées par e-mail dans le cadre du processus de configuration du compte. Si vous ne les recevez pas, contactez votre administrateur Adobe Experience Manager ou l’assistance clientèle Adobe pour les obtenir.

>[!NOTE]
>
Avant de configurer les services cloud Dynamic Media, assurez-vous d’avoir configuré l’instance de publication. Vous devez également configurer la réplication avant de configurer les services cloud Dynamic Media.

**Pour configurer les services cloud Dynamic Media :**

1. Dans Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Configuration de Dynamic Media (version antérieure à 6.3)]**.
1. Sur la page Navigateur de configuration Dynamic Media, dans le volet de gauche, sélectionnez **[!UICONTROL global]**, puis cliquez sur **[!UICONTROL Créer]**.
1. Dans la boîte de dialogue **[!UICONTROL Création d’une configuration Dynamic Media]**, saisissez un titre dans le champ Titre.
1. Si vous configurez Dynamic Media pour la vidéo :

   * dans le champ **[!UICONTROL ID d’enregistrement]**, entrez votre ID d’enregistrement ;
   * dans le champ **[!UICONTROL URL du service vidéo]**, entrez l’URL du service vidéo pour la passerelle Dynamic Media.

1. Si vous configurez Dynamic Media pour des images, dans le champ **[!UICONTROL URL du service d’images]**, saisissez l’URL du service d’images pour la passerelle Dynamic Media.
1. Sélectionnez **[!UICONTROL Enregistrer]** pour revenir à la page Navigateur de configuration Dynamic Media.
1. Pour accéder à la console de navigation globale, sélectionnez le logo d’Experience Manager.

## Configuration des rapports vidéo {#configuring-video-reporting}

Vous pouvez configurer les rapports vidéo pour plusieurs installations d’Experience Manager à l’aide de Dynamic Media en mode hybride.

**Utilisation :** au moment de la configuration de Dynamic Media (version antérieure à 6.3), de nombreuses fonctionnalités démarrent, dont celle des rapports vidéo. La configuration crée une suite de rapports dans une entreprise Analytics régionale. Si vous configurez plusieurs nœuds Auteur, vous créez une suite de rapport séparée pour chacun. Par conséquent, les données de rapport sont incohérentes entre les installations. En outre, si chaque nœud Auteur se réfère au même serveur Hybrid Publish, la dernière installation Auteur modifie la suite de rapports de destination pour tous les rapports vidéo. Ce problème surcharge le système d’analyses avec de trop nombreuses suites de rapports.

**Prise en main :** configurez les rapports vidéo en effectuant les trois tâches suivantes.

1. Créez un package de paramètres prédéfinis d’analyses vidéo après avoir configuré la Configuration de Dynamic Media (version antérieure à 6.3) sur le premier nœud de création. Cette première tâche est importante car elle permet à une nouvelle configuration de continuer à utiliser la même suite de rapports.
1. Installez le package de paramètres prédéfinis d’analyses vidéo sur tout ***nouveau*** nœud Auteur ***avant*** de paramétrer la Configuration Dynamic Media (version antérieure à 6.3). 
1. Vérifiez et déboguez l’installation du package.

### Création d’un package de paramètres prédéfinis d’analyses vidéo après la configuration du premier nœud Auteur {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Lorsque vous avez terminé cette tâche, vous disposez d’un fichier de package contenant les paramètres prédéfinis d’analyses vidéo. Ces paramètres prédéfinis comportent une suite de rapports, le serveur de suivi, les espaces de noms de suivi et l’ID d’organisation Experience Cloud, le cas échéant.

1. Si vous ne l’avez pas déjà fait, configurez la Configuration de Dynamic Media (version antérieure à 6.3).
1. (Facultatif) Affichez et copiez l’ID de suite de rapports (vous devez avoir accès au JCR). Bien que disposer de l’identifiant de la suite de rapports ne soit pas nécessaire, cela facilite la validation.
1. Créez un package à l’aide du Gestionnaire de modules.
1. Modifiez le package pour inclure un filtre.

   Dans Experience Manager : `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Créez le package.
1. Téléchargez ou partagez le package de paramètres prédéfinis d’analyses vidéo afin qu’il puisse être partagé avec de futurs nouveaux nœuds de création.

### Installation du package de paramètres prédéfinis d’analyses vidéo préalable à la configuration des nœuds auteur additionnels {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Assurez-vous d’avoir effectué cette tâche ***avant*** de paramétrer la Configuration Dynamic Media (version antérieure à 6.3). Ignorer cette étape résultera en la création d’une autre suite de rapports non utilisée. En outre, même si les rapports vidéo continuent à fonctionner correctement, la collecte des données n’est pas optimisée.

Vérifiez que le package de paramètres prédéfinis d’analyses vidéo du premier nœud Auteur est accessible sur le nouveau nœud Auteur.

1. Téléchargez le package de paramètres prédéfinis d’analyses vidéo que vous avez créé précédemment sur le gestionnaire de packages.
1. Installez le package de paramètres prédéfinis d’analyses vidéo.
1. Configurez la Configuration de Dynamic Media (version antérieure à 6.3).

### Vérification et débogage de l’installation du package {#verifying-and-debugging-the-package-installation}

1. Effectuez l’une des actions suivantes et, si nécessaire, déboguez l’installation du package :

   * **Vérifiez les paramètres prédéfinis d’analyses vidéo au moyen du JCR**
Pour vérifier les paramètres prédéfinis d’analyses vidéo au moyen du JCR, vous devez disposer d’un accès à CRXDE Lite.

     Experience Manager : dans CRXDE Lite, accédez à `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`.

     Comme dans `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

     Si vous n’avez pas accès à CRXDE Lite sur le nœud Auteur, vous pouvez vérifier le paramètre prédéfini via le serveur de publication.

   * **Vérification du paramètre prédéfini d’analyses vidéo via le serveur d’images**

     Vous pouvez valider le paramètre prédéfini d’analyses vidéo directement en effectuant une requête req=userdata sur le serveur d’images.
Par exemple, pour afficher le paramètre prédéfini d’analyse sur le nœud Auteur, vous pouvez effectuer la requête suivante :

     `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

     Pour valider le paramètre prédéfini sur les serveurs de publication, vous pouvez adresser une requête directe similaire sur le serveur de publication. La réponse est la même sur les nœuds d’auteur et de publication. La réponse ressemble à ce qui suit :

     ```
     marketingCloudOrgId=0FC4E86B573F99CC7F000101
      reportSuite=aemaem6397618-2018-05-23
      trackingNamespace=aemvideodal
      trackingServer=aemvideodal.d2.sc.omtrdc.net
     ```

   * **Vérification du paramètre prédéfini d’analyses vidéo à l’aide de l’outil de création de rapports vidéo dans Experience Manager**
Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports vidéo]**.

     `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

     Si le message d’erreur suivant s’affiche, la suite de rapports est disponible, mais non renseignée. Cette erreur est normale (et voulue) dans une nouvelle installation, avant que le système ne collecte des données.

   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Pour générer des données de rapport, chargez et publiez une vidéo. Utilisez la fonction **[!UICONTROL Copier l’URL]** et lancez la vidéo au moins une fois.

   Cela peut prendre jusqu’à 12 h avant que les données de rapport soient remplies par l’utilisation de la visionneuse vidéo.

   Si une erreur survient et que la suite de rapports n’est pas configurée correctement, l’avertissement suivant s’affiche.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Cette erreur s’affiche également si le rapport vidéo est exécuté avant la configuration des services de Configuration Dynamic Media (version antérieure à 6.3).

### Dépannage de la configuration de rapport vidéo {#troubleshooting-the-video-reporting-configuration}

* Pendant l’installation, les connexions au serveur API Analytics expirent. Lors de l’installation, la connexion tente d’être établie 20 fois, mais échoue malgré tout. Dans ce cas, le fichier journal enregistre plusieurs erreurs. Recherchez `SiteCatalystReportService`.
* Le fait de ne pas installer le package de paramètres prédéfinis d’analyses en premier peut causer la création d’une nouvelle suite de rapports.
* La mise à niveau d’Experience Manager 6.3 vers Experience Manager 6.4 ou Experience Manager 6.4.1, puis le paramétrage de la configuration de Dynamic Media (version antérieure à 6.3), crée toujours une suite de rapports. Ce problème est connu et sa réparation est prévue pour Experience Manager 6.4.2.

### À propos du paramètre prédéfini d’analyses vidéo {#about-the-video-analytics-preset}

Les paramètres prédéfinis d’analyses vidéo, parfois simplement appelés paramètres prédéfinis d’analyses, sont stockés près des paramètres prédéfinis de la visionneuse dans Dynamic Media. Il s’agit essentiellement de la même chose qu’un paramètre prédéfini de visionneuse, mais avec des informations utilisées pour configurer les rapports AppMeasurement et Video Heartbeat.

Les propriétés du paramètre prédéfini sont les suivantes :

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (non présent dans les anciennes versions d’Experience Manager)

Experience Manager 6.4 et les versions plus récentes enregistrent ce paramètre prédéfini à l’adresse `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`.

## Réplication des paramètres du catalogue {#replicating-catalog-settings}

Publiez vos propres paramètres de catalogue par défaut lors du processus de configuration via le JCR. Pour répliquer les paramètres de catalogue :

1. Dans une fenêtre de terminal, exécutez ce qui suit :

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. Dans Experience Manager, accédez à l’emplacement suivant dans CRXDE Lite (privilèges administrateur requis) :

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Sélectionnez l’onglet **[!UICONTROL Réplication]**.
1. Sélectionnez **[!UICONTROL Répliquer]**.

## Réplication des paramètres prédéfinis de la visionneuse {#replicating-viewer-presets}

Pour diffuser *une ressource avec un paramètre prédéfini de visionneuse, vous devez répliquer/publier* le paramètre prédéfini de la visionneuse. (Tous les paramètres prédéfinis de la visionneuse doivent être activés *et* répliqués pour obtenir l’URL ou le code intégré d’une ressource.
Reportez-vous à la section [Publication des paramètres prédéfinis de la visionneuse](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) pour plus d’informations.

>[!NOTE]
>
Par défaut, le système affiche différents rendus lorsque vous sélectionnez **[!UICONTROL Rendus]** et différents paramètres prédéfinis de la visionneuse lorsque vous sélectionnez **[!UICONTROL Visionneuses]** dans la vue détaillée de la ressource. Vous pouvez augmenter ou diminuer le nombre affiché. Consultez [Augmentation du nombre de paramètres d’image prédéfinis affichés](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Augmentation du nombre de paramètres prédéfinis de visionneuse qui s’affichent](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrage des ressources pour la réplication {#filtering-assets-for-replication}

Dans le cas des déploiements de médias non dynamiques, vous répliquez *toutes* les ressources (à la fois les images et les vidéos) à partir de votre environnement de création Experience Manager et vers le nœud de publication Experience Manager. Ce workflow est nécessaire car les serveurs de publication Experience Manager diffusent également les ressources.

À l’inverse, dans les déploiements Dynamic Media, il n’est pas nécessaire de répliquer les ressources vers les nœuds de publication Experience Manager, puisque ces ressources sont diffusées via le cloud. Un tel workflow de publication hybride permet d’éviter le coût d’un stockage supplémentaire et réduit les temps de traitement pour la réplication des ressources. D’autres contenus, comme les visionneuses Dynamic Media, les pages de site et le contenu statique, restent diffusés depuis les nœuds de publication Experience Manager.

D’autres éléments, qui ne sont pas des ressources, sont également répliqués :

* Configuration de diffusion Dynamic Media : `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Paramètres d’image prédéfinis : `/conf/global/settings/dam/dm/presets/macros`
* Paramètres prédéfinis de la visionneuse : `/conf/global/settings/dam/dm/presets/viewer`

Les filtres vous offrent la possibilité d’*exclure* des ressources de la réplication sur le nœud de publication Experience Manager.

### Utilisation de filtres de ressource par défaut pour la réplication {#using-default-asset-filters-for-replication}

Si vous utilisez Dynamic Media pour (1) les images en exploitation *ou* (2) les images et les vidéos, vous pouvez utiliser les filtres par défaut que nous fournissons en l’état. Les filtres suivants sont activés par défaut :

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtrer</strong></td>
   <td><strong>Type MIME</strong></td>
   <td><strong>Rendus</strong></td>
  </tr>
  <tr>
   <td>Diffusion d’image Dynamic Media</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Commence par <strong>image/</strong></p> <p>Contient <strong>application/</strong> et se termine par <strong>set</strong>.</p> </td>
   <td>Les « filter-images » d’usine (s’applique aux ressources d’images uniques, y compris aux images interactives) et les « filter-sets » (s’applique aux visionneuses à 360°, aux visionneuses de supports variés et aux visionneuses de carrousel) :
    <ul>
     <li>ajoutent des images et des métadonnées PTIFF pour la réplication (tout rendu commençant par <strong>cqdam</strong>) ;</li>
     <li>suppriment de la réplication l’image d’origine et les rendus d’image statiques.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Diffusion vidéo Dynamic Media</td>
   <td>filter-video</td>
   <td>Commence par <strong>video/</strong></td>
   <td>La « filter-video » d’usine :
    <ul>
     <li>comprend des rendus vidéo proxy, des images de miniatures/d’affiche vidéo, des métadonnées (à la fois pour les rendus vidéo et vidéo parents) pour la réplication (tout rendu commençant par <strong>cqdam</strong>) ;</li>
     <li>exclue de la réplication la vidéo d’origine et les rendus de miniatures statiques.<br /> <br /> <strong>Remarque :</strong> les rendus de vidéo en mode proxy ne contiennent pas de données binaires, et ne sont en fait que des propriétés de nœud. Ils n’affectent donc pas la taille du référentiel de l’éditeur.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intégration de Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td>
   <td><p>Commence par <strong>image/</strong></p> <p>Contient <strong>application/</strong> et se termine par <strong>set</strong>.</p> <p>Commence par <strong>video/</strong></p> </td>
   <td><p>Vous configurez l’URI de transport pour qu’il pointe vers votre serveur de publication d’Experience Manager au lieu de l’URL du service de réplication cloud Dynamic Media Adobe. La configuration de ce filtre permet à Dynamic Media Classic de diffuser les ressources à la place de l’instance de publication Experience Manager.</p> <p>Les « filter-images », « filter-sets » et « filter-video » prêts à l’emploi :</p>
    <ul>
     <li>ajoutent des images PTIFF, des rendus vidéo proxy et des métadonnées pour la réplication. Toutefois, dans la mesure où ils n’existent pas dans JCR, ces filtres n’ont aucun effet pour ceux qui exécutent l’intégration de Dynamic Media Classic d’Experience Manager.</li>
     <li>suppriment de la réplication l’image d’origine et les rendus d’image statiques, les vidéos d’origine et les rendus de miniature statiques. À la place, Dynamic Media Classic diffuse des ressources image et vidéo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Les filtres s’appliquent aux types MIME et ne peuvent pas être spécifiques à un chemin.

### Configurez les filtres de ressources pour les déploiements vidéo uniquement. {#setting-up-asset-filters-for-video-only-deployments}

Si vous utilisez Dynamic Media pour la vidéo uniquement, suivez les étapes suivantes pour configurer les filtres de ressource pour la réplication :

1. Dans Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** > **[!UICONTROL Agents sur l’auteur]**.
1. Dans la page Agents sur l’auteur, sélectionnez **[!UICONTROL Agent par défaut (publication)]**.
1. Sélectionnez **[!UICONTROL Modifier]**.
1. Dans la boîte de dialogue **[!UICONTROL Paramètres d’agent]**, sous l’onglet **[!UICONTROL Paramètres]**, cochez l’option **[!UICONTROL Activé]** pour activer l’agent.
1. Sélectionnez **[!UICONTROL OK]**.
1. Dans Experience Manager, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`.
1. Localisez **[!UICONTROL filter-video]**, cliquez dessus avec le bouton droit de la souris et sélectionnez **[!UICONTROL Copier]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/publish`.
1. Localisez `jcr:content`, cliquez dessus avec le bouton droit et sélectionnez **[!UICONTROL Coller]**.

Ces étapes configurent l’instance de publication Experience Manager pour qu’elle fournisse l’image d’affiche et les métadonnées de la vidéo qui sont nécessaires pour la lecture, tandis que la vidéo elle-même est fournie par les Cloud Services Dynamic Media. Le filtre exclut également de la réplication la vidéo originale et les rendus de miniature statiques, qui ne sont pas nécessaires sur l’instance de publication.

### Configuration des filtres de ressource pour les images dans des déploiements hors exploitation {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Si vous utilisez Dynamic Media pour les images dans des déploiements hors exploitation, suivez les étapes suivantes pour configurer les filtres de ressource pour la réplication :

1. Dans Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** > **[!UICONTROL Agents sur l’auteur]**.
1. Dans la page Agents sur l’auteur, sélectionnez **[!UICONTROL Agent par défaut (publication)]**.
1. Sélectionnez **[!UICONTROL Modifier]**.
1. Dans la boîte de dialogue **[!UICONTROL Paramètres d’agent]**, sous l’onglet **[!UICONTROL Paramètres]**, cochez l’option **[!UICONTROL Activé]** pour activer l’agent.
1. Sélectionnez **[!UICONTROL OK]**.
1. Dans Experience Manager, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`.

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Localisez **[!UICONTROL filter-images]**, cliquez dessus avec le bouton droit de la souris et sélectionnez **[!UICONTROL Copier]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/publish`.
1. Localisez `jcr:content`, cliquez avec le bouton droit de la souris, puis accédez à **[!UICONTROL Créer]** > **[!UICONTROL Créer un nœud]**. Saisissez le nom `damRenditionFilters` de type `nt:unstructured`.
1. Localisez `damRenditionFilters`, cliquez dessus avec le bouton droit et sélectionnez **[!UICONTROL Coller]**.

Ces étapes permettent de configurer l’instance de publication d’Experience Manager pour diffuser les images vers votre environnement hors exploitation. Le filtre exclut également de la réplication l’image originale et les rendus statiques, qui ne sont pas nécessaires sur l’instance de publication.

>[!NOTE]
>
S’il existe de nombreux filtres dans un auteur, chaque agent nécessite qu’un autre utilisateur lui soit attribué. Le code Granite impose la règle d’un seul filtre par utilisateur ou par utilisatrice. Prévoyez toujours un utilisateur différent pour chaque filtre configuré.
>
Utilisez-vous plusieurs filtres sur un serveur ? Par exemple, un filtre pour la réplication à publier et un second filtre pour s7delivery. Si c’est le cas, vous devez vous assurer que ces deux filtres ont un **userId** différents qui leur sont affecté dans le nœud `jcr:content`. Voir l’image suivante :

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personnalisation des filtres de ressources pour la réplication (facultatif) {#customizing-asset-filters-for-replication}

1. Dans Experience Manager, sélectionnez le logo Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils**[!UICONTROL  > ]**Général**[!UICONTROL  > ]**CRXDE Lite]**.
1. Dans l’arborescence de gauche, accédez à `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` pour parcourir les filtres.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Pour définir le type MIME du filtre, vous pouvez localiser le type MIME comme suit :

   Dans le rail de gauche, développez `content > dam > <locate_your_asset> >  jcr:content > metadata` puis, dans le tableau, localisez `dc:format`.

   L’illustration ci-dessous est un exemple de chemin d’une ressource vers `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Notez que la valeur `dc:format` de la ressource `Fiji Red.jpg` est `image/jpeg`.

   Pour appliquer ce filtre à toutes les images, quel que soit leur format, définissez la valeur sur `image/*` où `*` est une expression régulière qui est appliquée à toutes les images de n’importe quel format.

   Pour appliquer le filtre uniquement aux images de type JPEG, saisissez la valeur `image/jpeg`.

1. Définissez les rendus à inclure ou à exclure de la réplication.

   Voici des exemples de caractères que vous pouvez utiliser afin de filtrer la réplication :

   | Caractère à utiliser | Filtrage des ressources pour la réplication |
   | --- | --- |
   | `*` | Caractère générique |
   | `+` | Inclure les ressources à répliquer |
   | `-` | Exclure les ressources de la réplication |

   Accédez à `content/dam/<locate your asset>/jcr:content/renditions`.

   L’illustration ci-dessous est un exemple de rendu d’une ressource.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   Dans l’exemple ci-dessus, pour ne répliquer que l’image PTIFF (image TIFF pyramidale), il vous faudrait entrer `+cqdam,*` qui inclut tous les rendus commençant par `cqdam`. Dans cet exemple, ce rendu est `cqdam.pyramid.tiff`.

   Si vous souhaitez uniquement répliquer l’original, vous devez entrer `+original`.

## Configuration des paramètres du serveur d’images Dynamic Media {#configuring-dynamic-media-image-server-settings}

La configuration du serveur d’images Dynamic Media implique la modification du lot Adobe CQ Scene7 ImageServer et du lot Adobe CQ Scene7 PlatformServer.

>[!NOTE]
>
Dynamic Media est opérationnel [dès son activation](#enabling-dynamic-media). Cependant, vous pouvez choisir d’affiner l’installation en configurant le serveur d’images Dynamic Media pour répondre à des conditions ou des exigences particulières.

**Condition préalable** - *Avant* de configurer le serveur d’images Dynamic Media, vérifiez que les bibliothèques Microsoft® Visual C++ sont installées sur votre ordinateur virtuel Windows®. Les bibliothèques sont nécessaires pour exécuter le serveur d’images Dynamic Media. Vous pouvez [télécharger le package redistribuable Microsoft® Visual C++ 2010 (x64) ici](https://www.microsoft.com/fr-fr/download/details.aspx?id=26999).

Pour configurer les paramètres du serveur d’images Dynamic Media :

1. Dans le coin supérieur gauche d’Experience Manager, sélectionnez **[!UICONTROL Adobe Experience Manager]** pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
1. Dans la page de configuration de la Console Web d’Adobe Experience Manager, accédez à **[!UICONTROL OSGi]** > **[!UICONTROL Configuration]** pour répertorier tous les lots en cours d’exécution dans Experience Manager.

   Les serveurs de diffusion Dynamic Media sont répertoriés dans la liste sous les noms suivants :

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. Dans la liste de lots, à droite de Adobe CQ Scene7 ImageServer, appuyez sur l’icône **[!UICONTROL Modifier]**.
1. Dans la boîte de dialogue Adobe CQ Scene7 ImageServer, définissez les valeurs de configuration par défaut suivantes :

   >[!NOTE]
   >
   Normalement, il n’est pas nécessaire de modifier les valeurs par défaut. Si toutefois vous modifiez les valeurs par défaut, vous devrez redémarrer le lot pour que les modifications prennent effet.

   | Propriété | Valeur par défaut | Description |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | Numéro de port à utiliser pour les communications avec le processus ImageServer. Le port disponible par défaut est automatiquement détecté. |
   | `AllowRemoteAccess.name` | *`empty`* | Autorise ou refuse l’accès à distance au processus ImageServer. En cas de refus, le serveur d’images écoute uniquement sur le localhost.<br> Les paramètres par défaut du service Externalizer qui pointent vers le localhost doivent spécifier le domaine ou l’adresse IP de l’instance VM spécifique. La raison est que l’hôte local pointe vers le système parent de la machine virtuelle.<br>Les domaines ou les adresses IP de la machine virtuelle ont donc besoin d’une entrée de fichier hôte pour être résolus. |
   | `MaxRenderRgnPixels` | 16 MP | Taille maximale du rendu, en mégapixels. |
   | `MaxMessageSize` | 16 Mo | Taille maximale du message envoyé, en mégaoctets. |
   | `RandomAccessUrlTimeout` | 20 | Délai d’expiration correspondant au nombre de secondes durant lesquelles le serveur d’images attend le JCR avant de répondre à une requête de plage de mosaïque. |
   | `WorkerThreads` | 10 | Nombre de threads de traitement. |

1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Dans la liste des lots, à droite d’Adobe CQ Scene7 PlatformServer, appuyez sur l’icône **[!UICONTROL Modifier]**.
1. Dans la boîte de dialogue Adobe CQ Scene7 PlatformServer, définissez les valeurs d’option par défaut suivantes :

   >[!NOTE]
   >
   Le serveur d’images Dynamic Media utilise son propre cache sur disque pour mettre les réponses en mémoire cache. Le cache HTTP Experience Manager et le Dispatcher ne peuvent pas être utilisés pour la mise en mémoire cache des réponses provenant du serveur d’images Dynamic Media.

   | Propriété | Valeur par défaut | Description |
   |---|---|---|
   | Cache enabled | Cochée | Indique si le cache de réponse est activé. |
   | Cache roots | cache | Un ou plusieurs chemins d’accès aux dossiers du cache de réponse. Les chemins d’accès relatifs sont résolus par rapport au dossier de lots s7imagerie interne. |
   | Cache Max Size | 200000000 | Taille maximale du cache de réponse, en octets. |
   | Cache Max Entries | 100 000 | Nombre maximal d’entrées autorisées dans le cache. |

### Paramètres du manifeste par défaut {#default-manifest-settings}

Le manifeste par défaut vous permet de configurer les valeurs par défaut qui sont utilisées pour générer les réponses du service de diffusion Dynamic Media. Vous pouvez affiner la qualité (qualité JPEG, résolution, mode de rééchantillonnage), la mise en cache (expiration), et empêcher le rendu d’images trop grandes (defaultpix, defaultthumbpix, maxpix).

La localisation de la configuration du manifeste par défaut est basée sur la valeur par défaut de la **[!UICONTROL Racine de catalogue]** du lot **[!UICONTROL Adobe CQ Scene7 PlatformServer]**. Par défaut, cette valeur est localisée à l’emplacement suivant, sous **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![Configuration du serveur d’images dans CRXDE Lite](assets/configimageservercrxdelite.png)

Vous pouvez modifier les valeurs des propriétés décrites dans le tableau ci-dessous en saisissant de nouvelles valeurs.

Une fois les modifications apportées au manifeste par défaut, dans le coin supérieur gauche de la page, sélectionnez **[!UICONTROL Tout enregistrer]**.

Veillez à sélectionnez l’onglet **[!UICONTROL Contrôle d’accès]** (situé à droite de l’onglet Propriétés), puis définissez les privilèges de contrôle d’accès sur `jcr:read` pour tout le monde, ainsi que pour les utilisateurs de la réplication Dynamic Media.

![Configuration du serveur d’images dans CRXDE Lite et définition de l’onglet Contrôle d’accès](assets/configimageservercrxdeliteaccesscontroltab.png)

Tableau des paramètres du manifeste et leurs valeurs par défaut :

| Propriété | Valeur par défaut | Description |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | Couleur d’arrière-plan par défaut. La valeur RVB est utilisée pour remplir toutes les zones d’une image de réponse qui ne contiennent aucune donnée d’image actuelle. Consultez également la section [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `defaultpix` | `300,300` | Taille d’affichage par défaut. Le serveur oblige les images de réponse à ne pas dépasser cette largeur et cette hauteur si la requête ne spécifie pas explicitement la taille d’affichage à l’aide de wid=, hei=, ou scl=.<br>Spécifiée sous la forme de deux nombres entiers de valeur supérieure ou égale à zéro, séparés par une virgule. Largeur et hauteur en pixels. Vous pouvez définir sur 0 les deux valeurs, ou une seule des deux, pour ne pas les limiter. Ne s’applique pas aux requêtes imbriquées/intégrées.<br>Consultez également la section [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html?lang=fr#image-serving-api) dans l’API du service d’images.<br>Habituellement, cependant, vous utilisez un paramètre de visionneuse ou d’image prédéfini pour fournir la ressource. Defaultpix ne s’applique qu’à une ressource qui n’utilise pas de paramètre de visionneuse ou d’image prédéfini. |
| `defaultthumbpix` | `100,100` | Taille de miniature par défaut. Utilisé à la place d’attribute::DefaultPix pour les requêtes de miniature (`req=tmb`).<br>Le serveur oblige les images de réponse à ne pas dépasser cette largeur et cette hauteur. Cette action est définie sur true si une demande de miniature (`req=tmb`) ne spécifie pas explicitement la taille et ne spécifie pas la taille d’affichage explicitement à l’aide de `wid=`, `hei=`ou `scl=`.<br>Spécifiée sous la forme de deux nombres entiers de valeur supérieure ou égale à zéro, séparés par une virgule. Largeur et hauteur en pixels. Vous pouvez définir sur 0 les deux valeurs, ou une seule des deux, pour ne pas les limiter.<br>Ne s’applique pas aux requêtes imbriquées/intégrées.<br>Consultez également la section [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `expiration` | `36000000` | Durée de vie par défaut du cache. Fournit un intervalle d’expiration par défaut en heures au cas où un enregistrement de catalogue spécifique ne contient pas de valeur catalog::Expiration valide.<br>Nombre réel, supérieur ou égal à zéro. Nombre de millisecondes avant expiration depuis la génération des données de réponse. Définissez la valeur sur zéro pour que l’image de réponse expire immédiatement, ce qui permet de désactiver efficacement la mise en cache de client. Par défaut, cette valeur est définie sur 10 heures, ce qui signifie que si une nouvelle image est publiée, il faut 10 heures pour que l’ancienne image quitte le cache de l’utilisateur ou de l’utilisatrice. Contactez le service clientèle si vous avez besoin que la mémoire cache soit effacée plus rapidement.<br>Consultez également la section [Expiration](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html?lang=fr) dans l’API du service d’images. |
| `jpegquality` | `80` | Attributs de codage JPEG par défaut. Indique l’attribut par défaut des images de réponse au format JPEG.<br>Nombre entier et indicateur, séparés par une virgule. La première valeur est comprise dans la plage 1..100 et définit la qualité. La seconde valeur peut être égale à 0 par défaut, ou à 1 pour désactiver la réduction de la résolution chromatique RVB utilisée par les encodeurs JPEG.<br>Consultez également la section [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `maxpix` | `2000,2000` | Renvoie la limite de taille des images. Largeur et hauteur maximales de l’image de réponse renvoyée au client ou à la cliente.<br>Le serveur renvoie une erreur si une requête provoque la création d’une image de réponse dont la largeur ou la hauteur est plus importante que la valeur d’attribute::MaxPix.<br>Consultez également la section [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `resmode` | `SHARP2` | Mode de rééchantillonnage par défaut. Indique les attributs de rééchantillonnage et d’interpolation par défaut à utiliser pour le redimensionnement des données d’image.<br>Utilisé lorsque `resMode=` n’est pas spécifié dans une requête.<br>Les valeurs autorisées comprennent `BILIN`, `BICUB` ou `SHARP2`.<br>Enum. définie sur 2 pour le mode d’interpolation `bilin`, 3 pour le `bicub` ou 4 pour le `sharp2`. Utilisez `sharp2` pour obtenir de meilleurs résultats.<br>Consultez également la section [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `resolution` | `72` | Résolution d’objet par défaut. Fournit une résolution d’objet par défaut au cas où un enregistrement de catalogue particulier ne contient pas de valeur catalog::Resolution valide.<br>Nombre réel, supérieur à 0. Généralement exprimé en pixels par pouce, mais peut également être exprimé dans d’autres unités, comme les pixels par mètre.<br>Consultez également la section [Résolution](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html?lang=fr#image-serving-api) dans l’API du service d’images. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | Ces valeurs représentent un instantané du temps de lecture de la vidéo et sont transférées à [encoding.com](https://www.encoding.com/). Reportez-vous à la section [À propos des miniatures vidéo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) pour plus d’informations. |

## Configuration de la gestion des couleurs Dynamic Media {#configuring-dynamic-media-color-management}

La gestion des couleurs Dynamic Media vous permet de corriger les couleurs des ressources pour leur prévisualisation.

Avec la correction des couleurs, les ressources ingérées conservent leur espace colorimétrique (RVB, CMJN, gris) et leur profil de couleur intégré dans le rendu pyramidal TIFF généré. Lorsque vous demandez un rendu dynamique, la couleur de l’image est corrigée dans l’espace colorimétrique cible. Vous configurez le profil de couleurs cible dans les paramètres de publication Dynamic Media dans le JCR.

La gestion des couleurs d’Adobe utilise des profils ICC (International Color Consortium), un format défini par l’ICC.

Vous pouvez configurer la gestion des couleurs Dynamic Media et les paramètres d’image prédéfinis à l’aide des sorties RVB, CMJN et Niveaux de gris. Reportez-vous à la section [Configuration des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md).

Les cas d’utilisation avancés peuvent utiliser un modificateur de configuration manuel `icc=` pour sélectionner explicitement un profil de couleurs cible :

* `icc` – [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=fr](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=fr)

* `iccEmbed` – [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=fr](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=fr)

>[!NOTE]
>
L’ensemble standard de profils colorimétriques d’Adobe n’est disponible que si vous avez installé le [Pack de fonctionnalités 12445 de la distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445). Tous les packs de fonctionnalité et de service sont disponibles dans la [distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Le Pack de fonctionnalités 12445 fournit les profils de couleurs d’Adobe.


### Installation du Pack de fonctionnalités 12445 {#installing-feature-pack}

Pour utiliser les fonctionnalités de gestion des couleurs de Dynamic Media, installez le Pack de fonctionnalités 12445.

**Pour installer le Pack de fonctionnalités 12445 :**

1. Accédez à la [distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) et téléchargez `cq-6.3.0-featurepack-12445`.

   Pour plus d’informations sur l’utilisation des packages dans [!DNL Adobe Experience Manager], consultez [Utilisation des packages](/help/sites-administering/package-manager.md).

1. installez le Pack de fonctionnalités.

### Configuration des profils de couleurs par défaut {#configuring-the-default-color-profiles}

Une fois que vous avez installé le pack de fonctionnalités, configurez les profils de couleurs par défaut appropriés pour activer la correction de couleurs lors de l’appel des données d’image RVB ou CMJN.

**Pour configurer les profils de couleurs par défaut :**

1. Dans **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**, accédez à `/conf/global/settings/dam/dm/imageserver/jcr:content`, qui contient les profils de couleur par défaut d’Adobe.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Ajoutez une propriété de correction des couleurs en faisant défiler l’écran vers le bas de l’onglet **[!UICONTROL Propriétés]**. Saisissez manuellement le nom, le type et la valeur de la propriété, qui sont décrits dans les tableaux suivants. Une fois que vous avez entré les valeurs, sélectionnez **[!UICONTROL Ajouter]**, puis **[!UICONTROL Tout enregistrer]** pour les enregistrer.

   Les propriétés de correction des couleurs sont décrites dans le tableau **Propriétés de correction des couleurs**. Les valeurs que vous pouvez attribuer aux propriétés de correction des couleurs se trouvent dans le tableau **Profil colorimétrique**.

   Par exemple, dans **[!UICONTROL Nom]**, ajoutez `iccprofilecmyk`, sélectionnez **[!UICONTROL Type]** `String` puis ajoutez `WebCoated` en tant que **[!UICONTROL Valeur]**. Sélectionnez ensuite **[!UICONTROL Ajouter]** et **[!UICONTROL Tout enregistrer]** pour enregistrer vos valeurs.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **Tableau des propriétés de corrections des couleurs**

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur par défaut</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html?lang=fr">iccprofilergb</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique RVB par défaut.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html?lang=fr">iccprofilecmyk</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique CMJN par défaut.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html?lang=fr">iccprofilegray</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique de niveaux de gris par défaut.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html?lang=fr">iccprofilesrcrgb</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique RGB par défaut utilisé pour les images RGB qui n’ont pas de profil colorimétrique intégré.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html?lang=fr">iccprofilesrccmyk</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique CMJN par défaut utilisé pour les images CMJN qui n’ont pas de profil colorimétrique incorporé.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html?lang=fr">iccprofilesrcgray</a></td>
   <td>Chaîne</td>
   <td>&lt;empty&gt;</td>
   <td>Nom du profil colorimétrique de niveaux de gris par défaut utilisé pour les images CMJN qui n’ont pas de profil colorimétrique incorporé.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html?lang=fr">iccblackpointcompensation</a></td>
   <td>Booléen</td>
   <td>True</td>
   <td>Indique si la compensation du point noir est effectuée lors de la correction des couleurs. Adobe recommande d’activer ce paramètre.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html?lang=fr">iccdither</a></td>
   <td>Booléen</td>
   <td>False</td>
   <td>Indique si le tramage est effectué lors de la correction des couleurs.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html?lang=fr">iccrenderintent</a></td>
   <td>Chaîne</td>
   <td>relative</td>
   <td><p>Indique le mode de rendu. Les valeurs possibles sont : <strong>perception, relative, saturation, absolue. </strong><i></i>Adobe recommande d’utiliser <strong>colorimétrie relative</strong><i></i> comme valeur par défaut.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Les noms des propriétés sont sensibles à la casse et doivent être tous en minuscules.

**Tableau de profil colorimétrique**

Les profils colorimétriques suivants sont installés :

<table>
 <tbody>
  <tr>
   <th><p>Nom</p> </th>
   <th><p>Espace colorimétrique</p> </th>
   <th><p>Description</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RVB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RVB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RVB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMJN</td>
   <td>Coated FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMJN</td>
   <td>Coated FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMJN</td>
   <td>Coated GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RVB</td>
   <td>RGB ColorMatch</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMJN</td>
   <td>Europe ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMJN</td>
   <td>Euro scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMJN</td>
   <td>Euro scale Uncoated v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMJN</td>
   <td>Japan Color 2001 Coated</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMJN</td>
   <td>Japan Color 2002 Newspaper</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMJN</td>
   <td>Japan Color 2001 Uncoated</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMJN</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMJN</td>
   <td>Japan Web Coated (Ad)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMJN</td>
   <td>US Newsprint (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RVB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RVB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RVB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMJN</td>
   <td>Photoshop 4 Default CMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMJN</td>
   <td>Photoshop 5 Default CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMJN</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoated</td>
   <td>CMJN</td>
   <td>U.S. Sheetfed Uncoated v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RVB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRVB</td>
   <td>RVB</td>
   <td>sRVB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>UncoatedFogra29</td>
   <td>CMJN</td>
   <td>Uncoated FOGRA29 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMJN</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMJN</td>
   <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMJN</td>
   <td>Web Coated SWOP 2006 Grade 3 Paper</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMJN</td>
   <td>Web Coated SWOP 2006 Grade 5 Paper</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMJN</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RVB</td>
   <td>Wide Gamut RGB</td>
  </tr>
 </tbody>
</table>

1. Sélectionnez **[!UICONTROL Enregistrer tout]**.

Par exemple, vous pouvez définir **[!UICONTROL iccprofilergb]** sur `sRGB` et **[!UICONTROL iccprofilecmyk]** sur **[!UICONTROL WebCoated]**.

Les conséquences sont les suivantes :

* Active la correction des couleurs pour les images RVB et CMJN.
* Les images RVB qui n’ont pas de profil colorimétrique sont considérées comme se trouvant dans l’espace colorimétrique *sRVB*.
* Les images CMJN qui n’ont pas de profil colorimétrique sont considérées comme se trouvant dans l’espace colorimétrique *WebCoated*.
* Les rendus dynamiques qui renvoient une sortie RVB le font dans l’espace colorimétrique *sRVB*.
* Les rendus dynamiques qui renvoient une sortie CMJN, la renvoient dans l’espace colorimétrique *WebCoated*.

## Diffusion des ressources {#delivering-assets}

Une fois que vous avez terminé toutes les tâches ci-dessus, les ressources Dynamic Media activées sont diffusées depuis le service d’images ou de vidéos. Dans Experience Manager, cela apparaît dans les boîtes de dialogue de **[!UICONTROL copie d’URL d’image]**, **[!UICONTROL copie d’URL de visionneuse]**, **[!UICONTROL code de visionneuse intégré]**, et dans le composant de gestion de contenu web.

Reportez-vous à la section [Diffusion de ressources Dynamic Media](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Action</strong></td>
   <td><strong>Résultat</strong></td>
  </tr>
  <tr>
   <td>Copier l’URL d’une image</td>
   <td><p>La boîte de dialogue Copier l’URL affiche une URL similaire à celle qui suit (l’URL est utilisée à des fins de démonstration uniquement) :</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>où <code>IMAGESERVICEPUBLISHNODE</code> fait référence à l’URL du service d’images.</p> <p>Voir aussi <a href="/help/assets/delivering-dynamic-media-assets.md">Diffusion de ressources Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copier l’URL de la visionneuse</td>
   <td><p>La boîte de dialogue Copier l’URL affiche une URL similaire à celle qui suit (l’URL est utilisée à des fins de démonstration uniquement) :</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>où <code>PUBLISHNODE</code> désigne le nœud de publication standard d’Experience Manager et <code>IMAGESERVICEPUBLISHNODE</code> fait référence à l’URL du service d’images.</p> <p>Voir aussi <a href="/help/assets/delivering-dynamic-media-assets.md">Diffusion de ressources Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copier le code intégré d’une visionneuse</td>
   <td><p>La boîte de dialogue Copier le code affiche un fragment de code similaire à celui qui suit (le code est utilisé à des fins de démonstration uniquement) :</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>où <code>PUBLISHNODE</code> désigne le nœud de publication standard d’Experience Manager et <code>IMAGESERVICEPUBLISHNODE</code> fait référence à l’URL du service d’images.</p> <p>Voir aussi <a href="/help/assets/delivering-dynamic-media-assets.md">Diffusion de ressources Dynamic Media</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Composants WCM Dynamic Media et Interactive Media {#wcm-dynamic-media-and-interactive-media-components}

Les pages WCM qui font référence aux composants Dynamic Media et Interactive Media font référence au service de diffusion.
