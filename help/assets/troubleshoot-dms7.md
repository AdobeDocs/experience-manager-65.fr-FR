---
title: Dépannage de Dynamic Media – mode Scene7
description: Dépannage de Dynamic Media en mode d’exécution Scene7.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Dépannage de Dynamic Media – mode Scene7{#troubleshooting-dynamic-media-scene-mode}

Le document suivant décrit la résolution des problèmes affectant Dynamic Media en mode d’exécution **dynamicmedia_scene7**.

## Installation et configuration {#setup-and-configuration}

Assurez-vous que Dynamic Media a été correctement configuré en procédant comme suit :

* Start up command contains the `-r dynamicmedia_scene7` runmode argument.
* Tous les packs de correctifs cumulatifs (CFP) AEM 6.4 ont été installés *avant* tout Feature Pack Dynamic Media disponible.
* Le Feature Pack 18912 facultatif est installé.

   Ce Feature Pack facultatif est utile pour la prise en charge FTP ou si vous effectuez une migration des ressources de Dynamic Media vers Dynamic Media Classic (Scene7).

* Accédez à l’interface utilisateur des services cloud et vérifiez que le compte fourni s’affiche sous **[!UICONTROL Configurations disponibles]**.
* Ensure that the `Dynamic Media Asset Activation (scene7)` replication agent is enabled.

   Cet agent de réplication est accessible sous Agents dans l’instance d’auteur.

## Général (toutes les ressources) {#general-all-assets}

Vous trouverez ci-après quelques astuces et conseils généraux concernant toutes les ressources.

### Propriétés de l’état de synchronisation des ressources {#asset-synchronization-status-properties}

Vous pouvez passer en revue les propriétés de ressource suivantes dans CRXDE Lite pour vérifier que la synchronisation de la ressource depuis AEM vers Dynamic Media s’est déroulée correctement :

| **Propriété** | **Exemple** | **Description** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicateur général indiquant que le nœud est lié à Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **Publication terminée** ou texte d’erreur | Statut du téléchargement de la ressource vers Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Doit être renseigné pour générer des URL vers la ressource distante de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **succès** ou **échec :`<error text>`** | Statut de synchronisation des visionneuses (visionneuses à 360°, visionneuses d’images, etc.), des paramètres prédéfinis d’image, des paramètres prédéfinis de visionneuse, des mises à jour de zone cliquable pour une ressource ou des images ayant été modifiées. |

### Journalisation de la synchronisation {#synchronization-logging}

Synchronization errors and issues are logged in `error.log` (AEM server directory `/crx-quickstart/logs/`). Sufficient logging is available to determine the root cause of most issues, however you can increase the logging to DEBUG on the `com.adobe.cq.dam.ips` package through the Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) to gather more information.

### Déplacement, copie et suppression {#move-copy-delete}

Avant d’effectuer une opération de déplacement, de copie ou de suppression, procédez comme suit :

* Pour les images et les vidéos, vérifiez qu’une `<object_node>/jcr:content/metadata/dam:scene7ID` valeur existe avant d’effectuer des opérations de déplacement, de copie ou de suppression.
* Pour les paramètres prédéfinis d’image et de visionneuse, vérifiez qu’une `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` valeur existe avant d’effectuer des opérations de déplacement, de copie ou de suppression.
* Si la valeur de métadonnées ci-dessus est absente, vous devez transférer à nouveau les ressources avant les opérations de déplacement, de copie ou de suppression.

### Gestion de version {#version-control}

Lors du remplacement d’une ressource Dynamic Media (nom et emplacement identiques), vous avez la possibilité de conserver les deux ressources ou de remplacer/créer une version :

* Le fait de conserver ces deux éléments crée un nouveau fichier avec un nom unique pour l’URL du fichier publié. Par exemple, `image.jpg` est la ressource d’origine et `image1.jpg` la ressource nouvellement téléchargée.

* La création d’une version n’est pas prise en charge dans le cadre de la diffusion en mode Scene7 de Dynamic Media. La nouvelle version remplace la ressource existante lors de la diffusion.

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
   <td>Impossible d’accéder au bouton Copier le code intégré/l’URL dans la vue détaillée de la ressource</td>
   <td>
    <ol>
     <li><p>Accédez à CRX/DE :</p>
      <ul>
       <li>Vérifiez si le paramètre prédéfini dans le JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> est défini. Remarque : Cet emplacement s’applique si vous avez effectué la mise à niveau d’AEM 6.x vers la version 6.4 et avez choisi de ne pas utiliser la migration. Sinon, la situation est <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Check to make sure that the asset in the JCR has <code>dam:scene7FileStatus</code><strong> </strong>under Metadata shows as <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualisez la page/accédez à une autre page et revenez sur la page (le code JSP de rail latéral doit être recompilé)</p> <p>Si cela ne fonctionne pas :</p>
    <ul>
     <li>Publiez la ressource.</li>
     <li>Rechargez la ressource et publiez-la.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Le sélecteur de ressources dans l’éditeur de visionneuse est bloqué dans un chargement perpétuel.</td>
   <td><p>Problème connu à corriger dans la version 6.4</p> </td>
   <td><p>Fermez le sélecteur et rouvrez-le.</p> </td>
  </tr>
  <tr>
   <td>Le bouton <strong>Sélectionner</strong> n’est pas actif après sélection d’une ressource dans le cadre de la modification de ressource.</td>
   <td><p> </p> <p>Problème connu à corriger dans la version 6.4</p> <p> </p> </td>
   <td><p>Cliquez sur un autre dossier dans le sélecteur de ressources et revenez pour sélectionner la ressource.</p> </td>
  </tr>
  <tr>
   <td>La zone réactive de carrousel se déplace après un basculement entre des diapositives.</td>
   <td><p>Vérifiez que toutes les diapositives ont la même taille.</p> </td>
   <td><p>Utilisez uniquement des images de taille identique pour le carrousel.</p> </td>
  </tr>
  <tr>
   <td>L’aperçu de l’image ne s’affiche pas avec la visionneuse Dynamic Media.</td>
   <td><p>Check that the asset contains <code>dam:scene7File</code> in the Metadata properties (CRXDE Lite)</p> </td>
   <td><p>Vérifiez que le traitement de toutes les ressources est terminé.</p> </td>
  </tr>
  <tr>
   <td>La ressource téléchargée n’apparaît pas dans le sélecteur de ressources.</td>
   <td><p>Check asset has property <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Vérifiez que le traitement de toutes les ressources est terminé.</p> </td>
  </tr>
  <tr>
   <td>La bannière en mode Carte affiche <strong>Nouveau</strong> lorsque la ressource n’a pas commencé le traitement.</td>
   <td>Check asset <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> it was not picked up by the workflow.</td>
   <td>Attendez que la ressource soit sélectionnée par le workflow.</td>
  </tr>
  <tr>
   <td>Les images ou les visionneuses n’affichent pas l’URL ou le code intégré de la visionneuse.</td>
   <td>Vérifiez que le paramètre prédéfini de visionneuse a été publié.</td>
   <td><p>Go to <strong>Tools</strong> &gt; <strong>Assets</strong> &gt; <strong>Viewer Presets</strong> and publish the viewer preset.</p> </td>
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
   <td>L’aperçu de la vidéo ne peut pas être affiché.</td>
   <td>
    <ul>
     <li>Vérifiez que le dossier est associé à un profil vidéo (dans le cas d’un format de fichier non pris en charge). En l’absence de prise en charge, seule une image est affichée.</li>
     <li>Le profil vidéo doit contenir plusieurs paramètres prédéfinis de codage pour générer un ensemble AVS (les codages uniques sont considérés comme du contenu vidéo pour les fichiers MP4 ; dans le cas des fichiers non pris en charge, ils sont considérés comme étant non traités).</li>
     <li>Check that the video has finished processing by confirming <code>dam:scene7FileAvs</code> of <code>dam:scene7File</code> in metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Attribuez un profil vidéo au dossier.</li>
     <li>Modifiez le profil vidéo de sorte qu’il inclue plusieurs paramètres de codage prédéfinis.</li>
     <li>Attendez que le traitement de la vidéo soit terminé.</li>
     <li>Rechargez la vidéo et assurez-vous que le workflow Vidéo de codage de média dynamique n’est pas en cours d’exécution.<br /> </li>
     <li>Rechargez la vidéo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>La vidéo n’est pas codée.</td>
   <td>
    <ul>
     <li>Check that the runmode is <code>dynamicmedia_scene7</code>.</li>
     <li>Vérifiez que le service cloud Dynamic Media est configuré.</li>
     <li>Vérifiez qu’un profil vidéo est associé au dossier de transfert.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Vérifiez votre instance AEM avec <code>-r dynamicmedia_scene7</code></li>
     <li>Vérifiez que la configuration de Dynamic Media sous Services Cloud est correctement effectuée.</li>
     <li>Vérifiez que le dossier contient un profil vidéo. Vérifiez également le profil vidéo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Le traitement vidéo prend trop de temps.</td>
   <td><p>Pour déterminer si le codage vidéo est toujours en cours ou s’il est passé à l’état d’échec :</p>
    <ul>
     <li>Vérifiez l’état de la vidéo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitor the video from the workflow console <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Instances, Archive, Failures tabs.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Absence de rendu vidéo</td>
   <td><p>Lorsque la vidéo est téléchargée, mais qu’il n’y a aucun rendu codé :</p>
    <ul>
     <li>Vérifiez qu’un profil vidéo est attribué au dossier.</li>
     <li>Check that the video has finished processing by confirming <code>dam:scene7FileAvs</code> in metadata.</li>
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

<table>
 <tbody>
  <tr>
   <td><strong>Problème</strong></td>
   <td><strong>Débogage</strong></td>
   <td><strong>Solution</strong></td>
  </tr>
  <tr>
   <td>Les paramètres prédéfinis de la visionneuse ne sont pas publiés.</td>
   <td><p>Accédez à l’exemple de page de diagnostic du gestionnaire : <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Observez les valeurs calculées. Dans le cadre d’un fonctionnement correct, vous devriez voir :</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Remarque</strong> : Environ 10 minutes peuvent être nécessaires après la configuration des paramètres cloud de Dynamic Media pour que les ressources de visionneuse se synchronisent.</p> <p>S’il reste des ressources non activées, cliquez sur l’un des boutons <strong>Répertorier toutes les ressources non activées</strong> pour afficher des informations détaillées.</p> </td>
   <td>
    <ol>
     <li>Accédez à la liste des paramètres prédéfinis de la visionneuse dans les outils d’administration : <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Sélectionnez tous les paramètres prédéfinis de visionneuse, puis cliquez sur <strong>Publier</strong>.</li>
     <li>Revenez au gestionnaire d’échantillons et notez que le nombre de ressources non activées est maintenant égal à zéro.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Le paramètre prédéfini de visionneuse retourne 404 à partir de l’aperçu des détails de ressource ou de la copie d’URL/de code intégré.</td>
   <td><p>Dans CRXDE Lite, procédez comme suit :</p>
    <ol>
     <li>Accédez au <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> dossier du dossier de synchronisation de Contenu multimédia dynamique (par exemple, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Recherchez le noeud de métadonnées de la ressource problématique (par exemple, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Check for the presence of <code>dam:scene7*</code> properties. If the asset was successfully synced and published you see the <code>dam:scene7FileStatus</code> set is to <strong>PublishComplete</strong>.</li>
     <li>Essayez de demander l’illustration directement à partir de Dynamic Media en concaténant les valeurs des propriétés suivantes et des littéraux de chaîne.
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Exemple: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Si les exemples de ressources ou l’illustration du paramètre prédéfini de la visionneuse n’ont pas été synchronisés ou publiés, redémarrez le processus de copie/synchronisation entier :</p>
    <ol>
     <li>Accédez à CRXDE Lite.
      <ul>
       <li>Supprimer <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Navigate to the CRX package manager: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Recherchez le module de visionneuse dans la liste (il commence par <code>cq-dam-scene7-viewers-content</code>).</li>
       <li>Cliquez sur <strong>Réinstaller</strong>.</li>
      </ol> </li>
     <li>Sous Services Cloud, accédez à la page Configuration Dynamic Media, puis ouvrez la boîte de dialogue de configuration correspondant à la configuration S7 de Dynamic Media.
      <ul>
       <li>N’effectuez aucune modification, cliquez sur <strong>Enregistrer</strong>. Cela a pour effet de déclencher à nouveau la logique pour créer et synchroniser les exemples de ressources, la feuille CSS du paramètre prédéfini de la visionneuse et l’illustration.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

