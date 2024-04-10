---
title: Restructuration des référentiels d’Assets dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans Adobe Experience Manager (AEM) 6.5 pour Assets.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 100%

---

# Restructuration des référentiels d’Assets dans AEM 6.5 {#assets-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients et clientes effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution AEM Assets. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

**Avec la mise à niveau vers la version 6.5**

* [Divers](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Avant la future mise à niveau**

* [Modèle de notification par e-mail d’événement de ressource/collection](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Conceptions classiques de partage de ressources](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Modèle de notification par e-mail de téléchargement de ressource](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Exemple de licences DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Modèle de notification par e-mail de lien de partage](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [Scripts de workflow InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configurations de transcodage vidéo](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Divers](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Divers {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Si du code personnalisé dépend de cet emplacement (c’est-à-dire que le code s’appuie explicitement sur ce chemin), le code doit être mis à jour pour utiliser le nouvel emplacement avant la mise à niveau. Idéalement, les API Java™ sont utilisées lorsqu’elles sont disponibles pour réduire les dépendances sur un chemin spécifique dans le JCR.</p> <p>Emplacement temporaire pour contenir un fichier compressé à télécharger par le client. Il n’est pas nécessaire d’effectuer une mise à jour, car lorsque le client demande de télécharger la ressource, il génère un fichier au nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

## Avant la future mise à niveau {#prior-to-upgrade}

### Modèle de notification par e-mail d’événement de ressource/collection {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Si les modèles d’e-mail ont été modifiés par le client ou la cliente, effectuez les actions suivantes afin de vous aligner sur la nouvelle structure de référentiel :</p>
    <ol>
     <li>Le modèle d’e-mail <code>/libs/settings/dam/notification</code> doit être copié à partir de <strong><code>/etc/notification/email/default</code></strong> vers <strong><code>/apps/settings/notification/email/default</code></strong>.
      <ol>
       <li>Étant donné que la destination se trouve dans <strong> <code>/apps</code></strong>, cette modification doit être conservée dans SCM.</li>
      </ol> </li>
     <li>Supprimez le dossier <strong><code>/etc/dam/notification/email/default</code></strong> après le déplacement des modèles d’e-mail qu’il contient.<br />
      <ol>
       <li>Si aucune mise à jour n’a été apportée au modèle d’e-mail sous <strong>/<code>/etc/notification/email/default</code></strong>, le dossier peut être supprimé car le modèle d’e-mail d’origine existe sous <strong><code>/libs/settings/notification/email/default</code></strong> dans le cadre de l’installation d’AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Conceptions classiques de partage de ressources {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception, effectuez les actions suivantes pour vous aligner sur le dernier modèle :</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement sous <code>/apps</code>.</li>
     <li>Convertissez tous les fichiers CSS, JavaScipt et les ressources statiques dans la conception en une <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété <code>cq:designPath</code> via <strong>AEM &gt; Administrateur de gestion des ressources numériques &gt; Page de partage des ressources &gt; Propriétés de la page &gt; Onglet avancé &gt; Champ de conception</strong>.</li>
     <li>Pour utiliser la nouvelle catégorie Bibliothèque cliente, mettez à jour toutes les pages faisant référence à l’emplacement précédent. Cela nécessite de mettre à jour du code d’implémentation de la page.</li>
     <li>Mettez à jour les règles de Dispatcher afin de pouvoir autoriser le service des bibliothèques clientes via le servlet de proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Pour les conceptions qui ne sont pas gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception, ne déplacez pas les conceptions activées par le créateur ou la créatrice en dehors de <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Modèle de notification par e-mail de téléchargement de ressource {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Si les modèles d’e-mail (<strong>downloadasset</strong> ou <strong>transientworkflowcompleted</strong>) ont été modifiés, suivez la procédure ci-dessous pour vous aligner sur la nouvelle structure :</p>
    <ol>
     <li>Le modèle d’e-mail mis à jour doit être copié depuis <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> dans <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>.
      <ol>
       <li>Étant donné que la destination se trouve dans <strong><code>/apps</code></strong>, cette modification doit être conservée dans SCM.</li>
      </ol> </li>
     <li>Supprimez le dossier <code>/etc/dam/workflow/notification/email/downloadasset </code> après le déplacement des modèles d’e-mail qu’il contient.<br />
      <ol>
       <li>Si aucune mise à jour n’a été apportée au modèle d’e-mail sous <strong>/<code>/etc</code></strong>, le dossier peut être supprimé car le modèle d’e-mail d’origine existe sous <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> dans le cadre de l’installation d’AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Bien que <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> soit pris en charge techniquement pour la recherche (il est prioritaire par rapport à /apps via la recherche habituelle Sling CAConfig, mais passe après <code>/etc</code>), le modèle peut être placé dans <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Cependant, cela n’est pas recommandé car il n’y a pas d’interface utilisateur d’exécution pour faciliter la modification du modèle d’e-mail.</td>
  </tr>
 </tbody>
</table>

### Exemple de licences DRM {#example-drm-licenses}

| **Emplacement précédent** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nouveaux emplacements** | `/libs/settings/dam/drm` |
| **Conseils de restructuration** | S/O |
| **Remarques** | S/O |

### Modèle de notification par e-mail de partage de lien {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Si le modèle d’e-mail a été modifié par le client, alignez-le sur la nouvelle structure de référentiel :</p>
    <ol>
     <li>Le modèle d’e-mail mis à jour doit être copié depuis <strong><code>/etc/dam/adhocassetshare</code></strong> dans <strong><code>/apps/settings/dam/adhocassetshare</code></strong>.
      <ol>
       <li>Étant donné que la destination se trouve dans <strong><code>/apps</code></strong>, cette modification doit être conservée dans SCM.</li>
      </ol> </li>
     <li>Supprimez le dossier <strong><code>/etc/dam/adhocassetshare</code></strong> après le déplacement des modèles d’e-mail qu’il contient.<br />
      <ol>
       <li>Si aucune mise à jour n’a été apportée au modèle d’e-mail sous <strong>/<code>/etc</code></strong>, le dossier peut être supprimé car le modèle d’e-mail d’origine existe sous <strong><code>/libs/settings/dam/adhocassetshare</code></strong> dans le cadre de l’installation d’AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Bien que <code>/conf/global/settings/dam/adhocassetshare</code> soit techniquement pris en charge pour la recherche (il est prioritaire par rapport à <code>/apps</code> dans la recherche habituelle Sling CAConfig, mais passe après <code>/etc</code>), le modèle peut être placé dans <code>/conf/global/settings/dam/adhocassetshare</code>. Cependant, cela n’est pas recommandé car il n’y a pas d’IU d’exécution pour faciliter la modification du modèle d’e-mail.</td>
  </tr>
 </tbody>
</table>

### Scripts de workflow InDesign {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Pour s’aligner sur la nouvelle structure de référentiel :</p>
    <ol>
     <li>Copiez tous les scripts personnalisés ou modifiés depuis <strong><code>/etc/dam/indesign/scripts</code></strong> vers <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />.
      <ol>
       <li>Copiez uniquement les scripts nouveaux ou modifiés, car les scripts non modifiés fournis par AEM seront disponibles via <strong><code>/libs/settings</code></strong> dans AEM 6.5.</li>
      </ol> </li>
     <li>Recherchez tous les modèles de workflow qui utilisent l’étape de workflow Processus d’extraction de médias et
      <ol>
       <li>pour chaque instance de l’étape du workflow, mettez à jour les chemins de config pour qu’ils pointent explicitement vers les scripts appropriés sous <strong>/<code>/apps/settings/dam/indesign/scripts</code></strong> ou <strong><code>/libs/settings/dam/indesign/scripts</code></strong>, selon vos besoins.</li>
      </ol> </li>
     <li>Supprimez <strong> <code>/etc/dam/indesign/scripts</code></strong> entièrement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Il est recommandé de stocker les scripts personnalisés sous <code>/apps</code>, car il s’agit de l’emplacement où le code doit être stocké.</td>
  </tr>
 </tbody>
</table>

### Configurations de transcodage vidéo {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Les personnalisations au niveau du projet doivent être coupées et collées dans des chemins <code>/apps</code> ou <code>/conf</code> équivalents.</p> <p>Pour vous aligner sur la structure de référentiel AEM 6.4 :</p>
    <ol>
     <li>Copiez toutes les configurations vidéo modifiées depuis <code>/etc/dam/video</code> vers <code>/apps/settings/dam/video</code></li>
     <li>Supprimez <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Configuration des paramètres prédéfinis de la visionneuse {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Le paramètre prédéfini de visionneuse prêt à l’emploi n’est disponible que dans le nouvel emplacement.</p> <p>Pour le paramètre prédéfini de visionneuse personnalisé :</p>
    <ul>
     <li>Exécutez un script de migration afin de pouvoir déplacer le nœud de <code>/etc</code> vers <code>/conf</code>. Le script se trouve à l’adresse <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em>.</li>
     <li>Vous pouvez également modifier la configuration. L’enregistrement est automatiquement effectué au nouvel emplacement.</li>
    </ul> <p>Vous n’avez pas besoin d’ajuster le code copyURL/embed pour pointer vers <code>/conf</code>. La requête existante vers <code>/etc</code> sera réacheminée vers le contenu correct à partir de <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Divers {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Ajustez les références pour pointer vers les nouvelles ressources sous <code>/libs</code> à l’aide de <code>/etc.clientlibs/</code>.</p> <p>Enfin, procédez à un nettoyage en supprimant les dossiers des clientlibs migrés depuis <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
