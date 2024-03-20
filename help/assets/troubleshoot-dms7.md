---
title: Dépannage de Dynamic Media en mode Scene7
description: Découvrez comment résoudre les problèmes d’installation, de configuration et d’ordre général de Dynamic Media lorsqu’il s’exécute en mode Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 99%

---

# Dépannage de Dynamic Media en mode Scene7{#troubleshooting-dynamic-media-scene-mode}

Le document suivant décrit la résolution des problèmes liés à l’exécution de Dynamic Media en mode **dynamicmedia_scene7**.

## Installation et configuration {#setup-and-configuration}

Vérifiez que Dynamic Media a été installé correctement en procédant comme suit :

* La commande de démarrage contient l’argument de mode d’exécution `-r dynamicmedia_scene7`.
* Tous les packs de correctifs cumulatifs (CFP) Adobe Experience Manager 6.4 ont été installés *avant* tout pack de fonctionnalités Dynamic Media disponible.
* Le pack de fonctionnalités 18912 facultatif est installé.

  Ce pack de fonctionnalités facultatif est utile pour la prise en charge FTP ou si vous effectuez une migration des ressources de Dynamic Media vers Dynamic Media Classic.

* Accédez à l’interface utilisateur des services cloud et vérifiez que le compte fourni s’affiche sous **[!UICONTROL Configurations disponibles]**.
* Assurez-vous que l’agent de réplication `Dynamic Media Asset Activation (scene7)` est activé.

  Cet agent de réplication se trouve sous Agents sur l’instance de création.

## Général (toutes les ressources) {#general-all-assets}

Vous trouverez ci-après quelques astuces et conseils généraux concernant toutes les ressources.

### Propriétés de l’état de synchronisation des ressources {#asset-synchronization-status-properties}

Vous pouvez passer en revue les propriétés de ressource suivantes dans CRXDE Lite pour vérifier que la synchronisation de la ressource depuis Experience Manager vers Dynamic Media s’est déroulée correctement :

| **Propriété** | **Exemple** | **Description** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | Indicateur général indiquant que le nœud est lié à Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** ou texte d’erreur | Statut du téléchargement de la ressource vers Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Doit être renseigné pour générer des URL vers la ressource distante de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **succès** ou **échec :`<error text>`** | Statut de synchronisation des visionneuses (visionneuses à 360°, visionneuses d’images, etc.), des paramètres prédéfinis d’image, des paramètres prédéfinis de visionneuse, des mises à jour de zone cliquable pour une ressource ou des images ayant été modifiées. |

### Journalisation de la synchronisation {#synchronization-logging}

Les erreurs et problèmes de synchronisation sont consignés dans le fichier `error.log` (répertoire de serveur Experience Manager `/crx-quickstart/logs/`). La journalisation est suffisante pour déterminer la cause de la plupart des problèmes. Vous pouvez toutefois augmenter le niveau de journalisation sur DEBUG sur le package `com.adobe.cq.dam.ips` via la console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) pour collecter davantage d’informations.

### Déplacement, copie et suppression {#move-copy-delete}

Avant d’effectuer une opération de déplacement, de copie ou de suppression, procédez comme suit :

* Pour les images et les vidéos, vérifiez qu’il existe une valeur `<object_node>/jcr:content/metadata/dam:scene7ID` avant d’effectuer des opérations de déplacement, de copie ou de suppression.
* Pour les paramètres prédéfinis de visionneuse et d’image, vérifiez qu’il existe une valeur `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` avant d’effectuer des opérations de déplacement, de copie ou de suppression.
* Si la valeur de métadonnées ci-dessus est absente, vous devez charger à nouveau les ressources avant les opérations de déplacement, de copie ou de suppression.

### Gestion de version {#version-control}

Lors du remplacement d’une ressource Dynamic Media (nom et emplacement identiques), vous pouvez conserver les deux ressources ou remplacer et créer une version :

* Si vous conservez les deux, une nouvelle ressource est créée avec un nom unique pour l’URL de ressource publiée. Par exemple, `image.jpg` est la ressource d’origine et `image1.jpg` est la ressource qui vient d’être chargée.

* La création d’une version n’est pas prise en charge dans le cadre de la diffusion en mode Scene7 de Dynamic Media. La nouvelle version remplace la ressource existante lors de la diffusion.

## Images et visionneuses {#images-and-sets}

Si des problèmes surviennent avec les images et les visionneuses, reportez-vous aux conseils de dépannage ci-dessous.

<table>
 <tbody>
  <tr>
   <td><strong>Problème</strong></td>
   <td><strong>Débogage</strong></td>
   <td><strong>Solution</strong></td>
  </tr>
  <tr>
   <td>Impossible d’accéder au bouton Copier l’URL/Incorporer dans l’affichage des détails de la ressource</td>
   <td>
    <ol>
     <li><p>Accédez à CRX/DE :</p>
      <ul>
       <li>Vérifiez si le paramètre prédéfini dans le JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> est défini. Cet emplacement s’applique si vous avez effectué la mise à niveau d’Experience Manager 6.x vers la version 6.4 et si vous avez choisi de ne pas utiliser la migration. Dans le cas contraire, l’emplacement est <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Vérifiez que la ressource dans le JCR présente <code>dam:scene7FileStatus</code><strong> </strong>sous Métadonnées défini sur <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualisez la page ou accédez à une autre page et revenez sur la page (le code JSP de rail latéral doit être recompilé)</p> <p>Si cela ne fonctionne pas :</p>
    <ul>
     <li>Publiez la ressource.</li>
     <li>Rechargez la ressource et publiez-la.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Le sélecteur de ressources dans l’éditeur défini est bloqué dans le chargement perpétuel.</td>
   <td><p>Problème connu à corriger dans la version 6.4</p> </td>
   <td><p>Fermez le sélecteur et rouvrez-le.</p> </td>
  </tr>
  <tr>
   <td>Le bouton <strong>Sélectionner</strong> n’est pas actif après la sélection d’une ressource dans le cadre de la modification d’un ensemble.</td>
   <td><p> </p> <p>Problème connu à corriger dans la version 6.4</p> <p> </p> </td>
   <td><p>Sélectionnez un autre dossier dans le sélecteur de ressources et revenez pour sélectionner la ressource.</p> </td>
  </tr>
  <tr>
   <td>La zone réactive du carrousel se déplace après le basculement entre les diapositives.</td>
   <td><p>Vérifiez que toutes les diapositives ont la même taille.</p> </td>
   <td><p>Utilisez uniquement des images de la même taille pour le carrousel.</p> </td>
  </tr>
  <tr>
   <td>L’image n’est pas prévisualisée avec la visionneuse Dynamic Media.</td>
   <td><p>Vérifiez que la ressource contient <code>dam:scene7File</code> dans les propriétés de métadonnées (CRXDE Lite).</p> </td>
   <td><p>Vérifiez que le traitement de toutes les ressources est terminé.</p> </td>
  </tr>
  <tr>
   <td>La ressource chargée ne s’affiche pas dans le sélecteur de ressources.</td>
   <td><p>Vérifiez que la ressource présente la propriété <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Vérifiez que le traitement de toutes les ressources est terminé.</p> </td>
  </tr>
  <tr>
   <td>La bannière en mode Carte affiche <strong>Nouveau</strong> lorsque le traitement de la ressource n’a pas commencé.</td>
   <td>Vérifiez que la ressource <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> n’a pas été sélectionnée par le workflow.</td>
   <td>Attendez que la ressource soit récupérée par le workflow.</td>
  </tr>
  <tr>
   <td>Les images ou les ensembles n’affichent pas l’URL de la visionneuse ni le code intégré.</td>
   <td>Vérifiez si le paramètre prédéfini de visionneuse a été publié.</td>
   <td><p>Accédez à <strong>Outils</strong> &gt; <strong>Ressources</strong> &gt; <strong>Paramètres prédéfinis de la visionneuse</strong> et publiez le paramètre prédéfini de la visionneuse.</p> </td>
  </tr>
 </tbody>
</table>

## Vidéo {#video}

Si vous êtes confronté à des problèmes au niveau de la vidéo, reportez-vous aux conseils de dépannage ci-dessous.

<table>
 <tbody>
  <tr>
   <td><strong>Problème</strong></td>
   <td><strong>Débogage</strong></td>
   <td><strong>Solution</strong></td>
  </tr>
  <tr>
   <td>Impossible de prévisualiser la vidéo</td>
   <td>
    <ul>
     <li>Vérifiez que le dossier est associé à un profil vidéo (dans le cas d’un format de fichier non pris en charge). Si elle n’est pas prise en charge, seule une image s’affiche.</li>
     <li>Le profil vidéo doit contenir plusieurs paramètres prédéfinis de codage pour générer un ensemble AVS (les codages uniques sont traités comme du contenu vidéo pour les fichiers MP4 ; pour les fichiers non pris en charge, ils sont traités de la même manière que les fichiers non traités).</li>
     <li>Vérifiez que le traitement de la vidéo est terminé en confirmant <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> dans les métadonnées.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Attribuez un profil vidéo au dossier.</li>
     <li>Modifiez le profil vidéo pour inclure plusieurs paramètres prédéfinis de codage.</li>
     <li>Attendez que le traitement de la vidéo soit terminé.</li>
     <li>Avant de recharger la vidéo, assurez-vous que le workflow Vidéo de codage de média dynamique n’est pas en cours d’exécution.<br /> </li>
     <li>Rechargez la vidéo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>La vidéo n’est pas codée.</td>
   <td>
    <ul>
     <li>Vérifiez que le mode d’exécution est <code>dynamicmedia_scene7</code>.</li>
     <li>Vérifiez que le service cloud Dynamic Media est configuré.</li>
     <li>Vérifiez qu’un profil vidéo est associé au dossier de chargement.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Vérifiez votre instance d’Experience Manager avec <code>-r dynamicmedia_scene7</code></li>
     <li>Vérifiez que la configuration Dynamic Media sous Cloud Service est correctement effectuée.</li>
     <li>Vérifiez que le dossier contient un profil vidéo. Vérifiez également le profil vidéo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Le traitement vidéo prend trop de temps.</td>
   <td><p>Pour déterminer si le codage vidéo est toujours en cours ou s’il est à l’état d’échec :</p>
    <ul>
     <li>Vérifiez l’état de la vidéo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Surveillez la vidéo via la console de workflow <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; onglets Instances, Archive, Échecs.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rendu vidéo manquant</td>
   <td><p>Lorsque la vidéo est chargée, mais qu’il n’y a aucun rendu codé :</p>
    <ul>
     <li>Vérifiez qu’un profil vidéo est affecté au dossier.</li>
     <li>Vérifiez que le traitement de la vidéo est terminé en confirmant <code>dam:scene7FileAvs</code> dans les métadonnées.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Attribuez un profil vidéo au dossier.</li>
     <li>Attendez que le traitement de la vidéo soit terminé.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visionneuses {#viewers}

Si vous rencontrez des problèmes avec les visionneuses, reportez-vous aux conseils de dépannage ci-dessous.

### Problème : les paramètres prédéfinis de la visionneuse ne sont pas publiés {#viewers-not-published}

**Débogage**

1. Accédez à la page de diagnostic du gestionnaire d’échantillons : `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Observez les valeurs calculées. Lorsque le fonctionnement est correct, les éléments suivants s’affichent : `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Environ 10 minutes peuvent être nécessaires après la configuration des paramètres cloud de Dynamic Media pour que les ressources de visionneuse se synchronisent.

1. S’il reste des ressources non activées, sélectionnez l’un des boutons **Répertorier toutes les ressources non activées** pour afficher des informations détaillées.

**Solution**

1. Accédez à la liste des paramètres prédéfinis de la visionneuse dans les outils d’administration : `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Sélectionnez tous les paramètres prédéfinis de visionneuse, puis sélectionnez **Publier**.
1. Revenez au gestionnaire d’échantillons et notez que le nombre de ressources non activées est maintenant égal à zéro.

### Problème : le paramètre prédéfini de visionneuse retourne 404 à partir de l’aperçu des détails de ressource ou de la copie d’URL/de code intégré. {#viewer-preset-404}

**Débogage**

Dans CRXDE Lite, procédez comme suit :

1. Accédez au dossier `<sync-folder>/_CSS/_OOTB` dans votre dossier de synchronisation Dynamic Media (par exemple, `/content/dam/_CSS/_OOTB`).
1. Recherchez le nœud de métadonnées de la ressource qui pose problème (par exemple, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Vérifiez que les propriétés `dam:scene7*` sont présentes. Si la ressource a été correctement synchronisée et publiée, `dam:scene7FileStatus` est défini sur **PublishComplete**.
1. Essayez de demander l’illustration directement à partir de Dynamic Media en concaténant les valeurs des propriétés suivantes et des littéraux de chaîne :

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Exemple : `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solution**

Si les exemples de ressources ou l’illustration du paramètre prédéfini de la visionneuse n’ont pas été synchronisés ou publiés, redémarrez le processus de copie ou de synchronisation entier :

1. Accédez à CRXDE Lite.
1. Supprimez `<sync-folder>/_CSS/_OOTB`.
1. Accédez au gestionnaire de packages CRX : `https://localhost:4502/crx/packmgr/`.
1. Recherchez le package de visionneuse dans la liste ; il commence par `cq-dam-scene7-viewers-content`.
1. Sélectionnez **Réinstaller**.
1. Sous Services cloud, accédez à la page Configuration de Dynamic Media, puis ouvrez la boîte de dialogue de configuration correspondant à la configuration S7 de Dynamic Media.
1. N’effectuez aucune modification, sélectionnez **Enregistrer**.
Cette sauvegarde a pour effet de déclencher à nouveau la logique pour créer et synchroniser les exemples de ressources, la feuille CSS du paramètre prédéfini de la visionneuse et l’illustration.

### Problème : l’aperçu de l’image ne se charge pas dans la création des paramètres prédéfinis de la visionneuse. {#image-preview-not-loading}

**Solution**

1. Dans Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans le rail de gauche, accédez au dossier de contenu d’exemple à l’emplacement suivant :

   `/content/dam/_DMSAMPLE`

1. Supprimez le dossier `_DMSAMPLE`.
1. Dans le rail de gauche, accédez au dossier des paramètres prédéfinis à l’emplacement suivant :

   `/conf/global/settings/dam/dm/presets/viewer`

1. Supprimez le dossier `viewer`.
1. Dans le coin supérieur gauche de la page CRXDE Lite, sélectionnez **[!UICONTROL Tout enregistrer]**.
1. Dans le coin supérieur gauche de la page CRXDE Lite, sélectionnez l’icône **Retour à l’accueil**.
1. Recréez une [configuration Dynamic Media dans les services cloud](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
