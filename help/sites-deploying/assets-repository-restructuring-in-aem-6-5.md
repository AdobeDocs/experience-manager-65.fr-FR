---
title: Restructuration des référentiels d’Assets dans AEM 6.5
seo-title: Restructuration des référentiels d’Assets dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Assets.
seo-description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 53%

---


# Restructuration des référentiels d’Assets dans AEM 6.5 {#assets-repository-restructuring-in-aem}

As described on the parent [Repository Restructuring in AEM 6.5](/help/sites-deploying/repository-restructuring.md) page, customers upgrading to AEM 6.5 should use this page to assess the work effort associated with repository changes impacting the AEM Assets Solution. Certaines modifications nécessitent un effort de travail pendant le processus de mise à niveau AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau ultérieure.

**Avec la mise à niveau vers la version 6.5**

* [Divers](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Avant la mise à niveau future**

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
   <td><p>Si du code personnalisé dépend de cet emplacement (par exemple, le code repose explicitement sur ce chemin), il doit être mis à jour pour utiliser le nouvel emplacement avant de procéder à la mise à niveau. Idéalement, les API Java sont utilisées lorsqu’elles sont disponibles pour limiter les dépendances sur un chemin spécifique dans JCR.</p> <p>Emplacement temporaire pour contenir le fichier zip à télécharger par le client. Il n’est pas nécessaire d’effectuer une mise à jour, car lorsque le client demande de télécharger la ressource, il génère un fichier au nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## Avant la mise à niveau future {#prior-to-upgrade}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Si les modèles d’e-mail ont été modifiés par le client, effectuez les actions suivantes afin de vous aligner sur la nouvelle structure de référentiel :</p>
    <ol>
     <li>Le modèle de <code>/libs/settings/dam/notification</code> courrier électronique doit être copié de <strong><code>/etc/notification/email/default</code></strong> vers <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <strong><code>/etc/dam/notification/email/default</code></strong> after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc/notification/email/default</code></strong>, the folder can be removed as the original e-mail template exists under <strong><code>/libs/settings/notification/email/default</code></strong> as part of AEM 4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception, effectuez les actions suivantes pour vous aligner sur le dernier modèle :</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement sous <code>/apps</code>.</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en une <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété <code>cq:designPath</code> via <strong>AEM &gt; Administrateur DAM &gt; Page de partage des actifs &gt; Propriétés de la page &gt; Onglet avancé &gt; Champ de conception</strong>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente. Cela nécessite la mise à jour du code d’implémentation de la page.</li>
     <li>Update the Dispatcher rules to allow serving of Client Libraries via the <code>/etc.clientlibs/</code> proxy servlet.</li>
    </ol> <p>Pour les conceptions qui ne sont pas gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception, ne déplacez pas les conceptions activées par l’auteur en-dehors de <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Si les modèles d’e-mail (<strong>downloadasset</strong><strong> ou transientworkflowcompleted</strong>) ont été modifiés, suivez la procédure ci-dessous pour vous aligner sur la nouvelle structure :</p>
    <ol>
     <li>The updated e-mail template should be copied from <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> to <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <code>/etc/dam/workflow/notification/email/downloadasset </code>after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc</code></strong>, the folder can be removed as the orginal e-mail template exists under <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> as part of AEM 6.4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> is technically supported for look-up (takes precedence before /apps via usual Sling CAConfig lookup, but after <code>/etc</code>) the template could be placed in <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Cependant, cela n’est pas recommandé car il n’y a pas d’IU d’exécution pour faciliter la modification du modèle d’e-mail.</td>
  </tr>
 </tbody>
</table>

### Exemple de licences DRM {#example-drm-licenses}

| **Emplacement précédent** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nouveaux emplacements** | `/libs/settings/dam/drm` |
| **Conseil de restructuration** | N/A |
| **Notes** | N/A |

### Modèle de notification par e-mail de lien de partage {#link-share-e-mail-notification-template}

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
     <li>The updated e-mail template should be copied from <strong><code>/etc/dam/adhocassetshare</code></strong> to <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <strong><code>/etc/dam/adhocassetshare</code></strong> after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc</code></strong>, the folder can be removed as the original e-mail template exists under <strong><code>/libs/settings/dam/adhocassetshare</code></strong> as part of AEM 6.4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> is technically supported for look-up (it takes precedence before <code>/apps</code> via usual Sling CAConfig lookup, but after <code>/etc</code>), the template can be placed in <code>/conf/global/settings/dam/adhocassetshare</code>. Toutefois, cette méthode n’est pas recommandée car il n’existe pas d’interface utilisateur d’exécution pour faciliter la modification du modèle de courrier électronique.</td>
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
     <li>Copier tous les scripts personnalisés ou modifiés de <strong><code>/etc/dam/indesign/scripts</code></strong> vers <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>Only copy new or modified scripts as unmodified scripts provided by AEM will be available via <strong><code>/libs/settings</code></strong> in AEM 6.5</li>
      </ol> </li>
     <li>Recherchez tous les modèles de workflow qui utilisent l’étape de workflow Processus d’extraction de médias et
      <ol>
       <li>For each instance of the Workflow Step, update the paths in config to point explicitly at the proper scripts under<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> or <strong><code>/libs/settings/dam/indesign/scripts</code></strong> as appropriate.</li>
      </ol> </li>
     <li>Supprimez<strong><code>/etc/dam/indesign/scripts</code></strong> complètement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>It is recommended customized scripts be stored under <code>/apps</code>, since that is the location where code should be stored.</td>
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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Project level customizations need to be cut and pasted under equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</p> <p>Pour vous aligner sur la structure de référentiel AEM 6.4 :</p>
    <ol>
     <li>Copier toutes les configurations vidéo modifiées de <code>/etc/dam/video</code> vers <code>/apps/settings/dam/video</code></li>
     <li>Remove <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Configurations des paramètres prédéfinis de la visionneuse {#viewer-preset-configurations}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les paramètres prédéfinis prêts à l’emploi de la visionneuse ne seront disponibles que dans le nouvel emplacement.</p> <p>Pour les paramètres prédéfinis personnalisés de la visionneuse :</p>
    <ul>
     <li>you will have to run a migration script to move the node from <code>/etc</code> to <code>/conf</code>. The script is located at <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>ou vous pouvez modifier la configuration pour qu’ils soient enregistrés automatiquement au nouvel emplacement.</li>
    </ul> <p>Note that you do not have to adjust their copyURL/embed code to point to <code>/conf</code>. The existing request to <code>/etc</code> will be re-routed to the correct content from <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A</td>
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
   <td><p>Adjust any references to point to the new resources under <code>/libs</code> using the <code>/etc.clientlibs/</code> allow proxy prefix.</p> <p>Enfin, supprimez les dossiers des clientlibs migrés de <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

