---
title: Restructuration du référentiel Dynamic Media dans Adobe Experience Manager 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans Experience Manager 6.5 pour Dynamic Media.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 100%

---

# Restructuration du référentiel Dynamic Media dans Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers Experience Manager 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la Dynamic Media. Certaines modifications demandent du travail lors du processus de mise à niveau vers Experience Manager 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers la version future.

**Avant la mise à niveau ultérieure**

* [Configurations personnalisées du codage vidéo adaptatif](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configuration du cloud Dynamic Media (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configuration du service cloud Dynamic Media (version hybride de DM)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - Configuration du service cloud YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Divers](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Avant la mise à niveau ultérieure {#prior-to-upgrade}

### Configurations personnalisées du codage vidéo adaptatif  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Vous pouvez exécuter le script de migration suivant pour migrer vers le nouvel emplacement :</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Vous pouvez également modifier la configuration dans l’interface utilisateur d’Experience Manager. Les modifications seront enregistrées au nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configuration du cloud Dynamic Media (DMS7) {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Le client peut exécuter un script de migration à cet emplacement :<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Redémarrez le lot OSGi Dynamic Media.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Configuration du service cloud Dynamic Media (version hybride de DM) {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Vous pouvez exécuter le script de migration suivant pour vous aligner sur le modèle le plus récent :</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - Configuration du service cloud YouTube  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>1. Dépubliez toutes les vidéos de YouTube.<br /> 2. Créez la configuration YouTube à l’aide de la nouvelle TouchUI (à partir de <code>/conf</code>), y compris en copiant toutes les chaînes de l’ancien emplacement.<br /> 3. Publiez toutes les vidéos sur YouTube.</p> <p>Ce workflow génère de nouvelles URL YouTube. Si vous n’annulez pas la publication avant de créer une configuration YouTube TouchUI, plusieurs URL YouTube seront répertoriées sous Propriétés, car les chaînes recréées seront publiées si l’occasion se présente. Cela signifie que des URL inutiles seront répertoriées sous Propriétés.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Divers {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Le client peut exécuter le script de migration ci-dessous.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Vous pouvez également modifier la configuration dans l’interface utilisateur d’Experience Manager. Les modifications seront enregistrées au nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Le client peut exécuter le script de migration ci-dessous.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>
