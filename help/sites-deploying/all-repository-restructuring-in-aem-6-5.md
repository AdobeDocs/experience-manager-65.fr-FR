---
title: Restructuration commune des référentiels dans AEM 6.5
description: Découvrez comment effectuer les modifications nécessaires communes à tous les domaines AEM pour migrer vers la nouvelle structure du référentiel dans AEM 6.5.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 100%

---

# Restructuration des référentiels dans AEM 6.5 {#common-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact potentiel sur toutes les solutions. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

**Avec la mise à niveau vers la version 6.5**

* [Configurations ContextHub](#contexthub-6.5)
* [Instances de workflow](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modèles de workflow](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Lanceurs de workflow](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Scripts de workflow](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Avant de procéder à la mise à niveau vers une future version**

* [Configurations ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Conceptions de services cloud classiques](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Conceptions de tableaux de bord classiques](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Conceptions de rapports classiques](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Conceptions par défaut](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Point d’entrée Javascript Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Point d’entrée Web-Hook Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tâches de la boîte de réception](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurations Blueprint de Multi-Site Manager](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurations du gadget de tableau de bord Projets AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modèle d’e-mail de notification de réplication](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Balises](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Services cloud de traduction](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Langues de traduction](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Règles de traduction](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Bibliothèque cliente du widget de traduction](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console Web d’activation des arborescences](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Services cloud de connecteur de traduction de fournisseur](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modèles d’e-mail de notification de workflow](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Configurations ContextHub {#contexthub-6.5}

Depuis AEM 6.4, il n’existe plus de configuration ContextHub par défaut. Par conséquent, une `cq:contextHubPathproperty` doit être définie au niveau racine du site pour indiquer la configuration à utiliser.

1. Accédez à la racine du site.
1. Ouvrez les propriétés de la page racine et sélectionnez ensuite l’onglet Personnalisation.
1. Dans le champ Chemin d’accès ContextHub, saisissez votre propre chemin d’accès de configuration ContextHub.

Dans la configuration ContextHub, la propriété `sling:resourceType` doit, en outre, être mise à jour, passant de « Relative » à « Absolue ».

1. Ouvrez les propriétés du nœud de configuration ContextHub dans CRX DE Lite, par exemple `/apps/settings/cloudsettings/legacy/contexthub`.
1. Modifiez `sling:resourceType` de `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` en `granite/contexthub/cloudsettings/components/baseconfiguration`.

En d’autres termes, la propriété `sling:resourceType` de la configuration ContextHub doit être relative et non absolue.

### Modèles de workflow {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les modèles de workflow, nouveaux ou modifiés, doivent être migrés vers /conf/global/workflow/models.</p>
    <ol>
     <li>Déployez les modèles de workflow modifiés dans une instance locale de développement AEM 6.5, comme ils existent dans l’emplacement précédent.</li>
     <li>Modifiez le modèle de workflow à l’aide de l’éditeur de modèle de workflow d’AEM sous AEM &gt; Outils &gt; Workflow &gt; Modèles.</li>
     <li>Lors de la migration de modèles de workflow modifiés fournis par AEM
      <ol>
       <li>Une fois l’éditeur de modèle de workflow ouvert, modifiez l’URL de l’adresse du navigateur et remplacez le segment de chemin /libs/settings/workflow/models with /etc/workflow/models.
        <ul>
         <li>Par exemple, modifiez <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> en <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Activez le mode d’édition dans l’éditeur de modèle de workflow qui copiera la définition du modèle de workflow dans /conf/global/workflow/models.</li>
     <li>Sélectionnez le bouton Synchroniser pour synchroniser les modifications apportées au modèle de workflow d’exécution sous /var/workflow/models.</li>
     <li>Exportez le modèle de workflow (/conf/global/workflow/models/&lt;workflow-model&gt;) et le modèle de workflow d’exécution (/var/workflow/models/&lt;workflow-model&gt;), puis intégrez-les dans le projet AEM.
      <ol>
       <li>Par exemple, exportez :
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> et </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution d’un modèle de workflow s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Ainsi, toute personnalisation de modèles de workflow fournis par AEM et conservés à l’emplacement précédent doit être déplacée vers /conf/global/settings/workflow/models. Autrement, elle sera remplacée par la définition du modèle de workflow dans /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Instances de workflow {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Aucune action n’est requise pour s’aligner sur le nouvel emplacement.</p> <p>Les instances de workflow historiques peuvent continuer à résider en toute sécurité à l’emplacement précédent et de nouvelles instances de workflow seront créées dans le nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Toute référence de chemin explicite dans
 le code <code>
     custom
    </code> vers l’emplacement précédent doit également prendre en compte le nouvel emplacement. Il est recommandé de refactoriser ce code pour utiliser les API de workflow AEM.</td>
  </tr>
 </tbody>
</table>

### Lanceurs de workflow {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les lanceurs de workflow nouveaux ou modifiés doivent être migrés vers <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copiez les configurations nouvelles ou modifiées du lanceur de workflow de l’emplacement précédent dans un nouvel emplacement (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution du lanceur de workflow s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Ainsi, toute personnalisation du lanceur de workflow fourni par AEM et conservée à l’emplacement précédent doit être déplacée vers le nouvel emplacement (<code>/conf/global/settings/workflow/launcher</code> si elle doit être conservée), sinon, elle sera remplacée par la définition du lanceur de workflow fourni par AEM dans <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts de workflow {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les scripts de workflow nouveaux ou modifiés doivent être migrés vers le nouvel emplacement et les modèles de workflow de référence mis à jour pour refléter le nouvel emplacement.</p>
    <ol>
     <li>Copiez les scripts de workflow nouveaux ou modifiés de l’emplacement précédent vers le nouvel emplacement.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> doit être conservé dans SCM.</li>
      </ul> </li>
     <li>Mettez à jour les références aux scripts de workflow à l’emplacement précédent dans les modèles de workflow pour pointer vers les nouveaux emplacements.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>AEM 6.4 SP1, à sa publication, permet de différer cette restructuration jusqu’à la mise à niveau vers la version 6.5
     <code>
      upgrade
     </code>.</p> <p>Si vous effectuez une mise à niveau vers AEM 6.4 avant la publication d’AEM 6.4 SP1, cette restructuration doit être effectuée dans le cadre du projet de mise à niveau. Sinon, la modification et l’enregistrement des étapes de workflow référençant des scripts à l’emplacement précédent supprime entièrement la référence du script de workflow de l’étape de workflow. Seuls les scripts de workflow dans de nouveaux emplacements sont disponibles dans la liste déroulante de sélection de script.</p> </td>
  </tr>
 </tbody>
</table>

## Avant de procéder à la mise à niveau vers une future version {#prior-to-upgrade}

### Configurations ContextHub {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute configuration ContextHub nouvelle ou modifiée doit être migrée vers le nouvel emplacement et les pages AEM Sites de référencement doivent être mises à jour pour refléter le nouvel emplacement.</p>
    <ol>
     <li>Copiez les configurations ContextHub nouvelles ou modifiées de l’emplacement précédent vers le nouvel emplacement.</li>
     <li>Associez les configurations d’AEM applicables aux hiérarchies de contenu AEM.
      <ol>
       <li><strong>Hiérarchies de page AEM Sites via AEM Sites &gt; Page &gt; Propriétés de page &gt; Onglet avancé &gt; Configuration cloud</strong>.</li>
      </ol> </li>
     <li>Dissociez les configurations ContextHub héritées migrées des hiérarchies de contenu AEM mentionnées ci-dessus.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Conceptions de services cloud classiques {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles de Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet de proxy /etc.clientlibs/..</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Conceptions de tableaux de bord classiques {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement (/apps).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété
       <code>
       cq
      </code> :
       <code>
       designPath
      </code>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles de Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet de proxy /etc.clientlibs/..</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Conceptions de rapports classiques {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement (/apps).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété
       <code>
       cq
      </code> :
       <code>
       designPath
      </code>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles de Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet de proxy /etc.clientlibs/..</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Conceptions par défaut {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement (/apps).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété
       <code>
       cq
      </code> :
       <code>
       designPath
      </code>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles de Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet de proxy /etc.clientlibs/..</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Point d’entrée Javascript Adobe DTM {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Aucune action n’est requise.</p> <p>L’emplacement public précédent agit comme un point d’entrée proxy pour le nouvel emplacement privé.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Point d’entrée Web-Hook Adobe DTM {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Aucune action n’est requise.</p> <p>L’emplacement public précédent agit comme un point d’entrée proxy pour le nouvel emplacement privé.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Tâches de la boîte de réception {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>Utilisez la <strong>tâche de maintenance de purge de la boîte de réception</strong> pour supprimer les anciennes tâches de l’emplacement précédent en cas de besoin.</td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Aucune action n’est requise pour la migration des tâches vers le nouvel emplacement.</p>
    <ul>
     <li>Les tâches présentes dans l’emplacement précédent restent disponibles et fonctionnent.</li>
     <li>De nouvelles tâches sont créées dans le nouvel emplacement.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurations de plans directeurs de Multi-site Manager {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>Emplacement précédent</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>
    <ol>
     <li>Copiez les configurations personnalisées depuis <code>/etc/blueprints</code> vers <code>/apps/msm</code>.</li>
     <li>Supprimez <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Configurations du gadget de tableau de bord Projets AEM {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les configurations de gadget de tableau de bord Projets AEM nouvelles ou modifiées doivent être migrées vers le nouvel emplacement (<code>/apps</code>).</p>
    <ol>
     <li>Copiez les configurations de gadget de tableau de bord Projets AEM nouvelles ou modifiées de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).
      <ol>
       <li>Ne copiez pas les configurations non modifiées, car elles existent maintenant dans le nouvel emplacement (<code>/libs</code>).</li>
      </ol> </li>
     <li>Mettez à jour les modèles Projets AEM faisant référence à l’emplacement précédent pour qu’ils pointent vers le nouvel emplacement approprié.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Si vous appliquez le package de compatibilité AEM 6.4, vous devez effectuer les activités d’alignement du référentiel au moment de la suppression du package de compatibilité.</td>
  </tr>
 </tbody>
</table>

### Modèle d’e-mail de notification de réplication {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les modèles d’e-mail de notification de réplication nouveaux ou modifiés doivent être migrés vers le nouvel emplacement (<code>/apps</code>).</p>
    <ol>
     <li>Copiez les modèles d’e-mail de notification de réplication nouveaux ou modifiés de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Supprimez les modèles d’e-mail de notification de réplication migrés de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Les seuls nouveaux modèles d’e-mail de notification de réplication pris en charge sont ceux qui prennent en charge les nouveaux paramètres régionaux.</p> <p>La résolution du modèle d’e-mail de notification de réplication s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Balises {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toutes les balises doivent être migrées vers <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copiez toutes les balises de l’emplacement précédent dans le nouvel emplacement.</li>
     <li>Supprimez toutes les balises de l’emplacement précédent.</li>
     <li>Dans la console Web AEM, redémarrez le lot OSGi Tagging Day Communique 5 à l’adresse <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> pour qu’AEM détermine que le nouvel emplacement contient du contenu et qu’il doit être utilisé.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Le redémarrage du bundle OSGi Day Communique Tagging n’enregistrera le nouvel emplacement en tant que racine de balise que si l’emplacement précédent est vide.</p> <p>Les références à l’emplacement précédent continueront à fonctionner après la migration vers le nouvel emplacement pour toutes les fonctionnalités qui utilisent l’API AEM TagManager pour la résolution des balises.</p> <p>Tout code personnalisé qui référence explicitement le chemin d’accès <code>/etc/tags</code> doit être remplacé par <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, ou de préférence réécrit en utilisant l’API Java TagManager, en même temps que cette migration.</p> </td>
  </tr>
 </tbody>
</table>

### Services cloud de traduction {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les nouveaux services cloud de traduction doivent être migrés vers le nouvel emplacement (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ul>
       <li>Recréez manuellement les nouvelles configurations des services cloud de traduction via l’interface utilisateur de création d’AEM dans <strong>Outils &gt; Services cloud &gt; Services cloud de traduction</strong>.<br /> OU </li>
       <li>Copiez les nouvelles configurations de services cloud de traduction de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associez les configurations d’AEM applicables aux hiérarchies de contenu AEM.
      <ol>
       <li>Hiérarchies de page AEM Sites via <strong>AEM Sites &gt; Page &gt; Propriétés de page &gt; Onglet Avancé &gt; Configuration cloud</strong>.</li>
       <li>Hiérarchies de fragments d’expérience AEM via <strong>Fragments d’expérience AEM &gt; Fragment d’expérience &gt; Propriétés &gt; Onglet Services cloud &gt; Configuration cloud</strong>.</li>
       <li>Hiérarchies de dossiers de fragments d’expérience AEM via <strong>Fragments d’expérience AEM &gt; Dossier &gt; Propriétés &gt; Onglet Services cloud &gt; Configuration cloud</strong>.<br /> </li>
       <li>Hiérarchies des dossiers AEM Assets via <strong>AEM Assets &gt; Dossier &gt; Propriétés du dossier &gt; Onglet Services cloud &gt; Configuration</strong>.</li>
       <li>Projets AEM via <strong>Projets AEM &gt; Projet &gt; Propriétés du projet &gt; Onglet avancé &gt; Configuration cloud</strong>.</li>
      </ol> </li>
     <li>Dissociez les anciens services cloud de traduction migrés des hiérarchies de contenu AEM mentionnées ci-dessus.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution des services cloud de traduction s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Les services cloud de traduction migrés doivent être compatibles avec AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Langues de traduction {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les définitions de langue de traduction nouvelles ou modifiées requièrent une migration de toutes les définitions de langue de traduction vers le nouvel emplacement (<code>/apps</code>).</p>
    <ol>
     <li>Si des ajouts ou des modifications ont été apportés aux définitions de langue de traduction, copiez toutes les définitions de langue de traduction dans le nouvel emplacement (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution du chemin de langue de traduction s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Cette résolution ne prend pas en charge une superposition de fusion, ce qui signifie que le chemin résolu doit contenir toutes les langues prises en charge et n’héritera pas des langues prises en charge de résolutions d’ordre supérieur.</p> </td>
  </tr>
 </tbody>
</table>

### Règles de traduction {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Un fichier XML de règles de traduction modifié doit être migré vers le nouvel emplacement (<code>/apps</code> ou <code>/conf/global</code>).</p> <p>1. Copiez le fichier XML de règles de traduction modifié de l’emplacement précédent dans le nouvel emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution XML des règles de traduction de la réplication s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Bibliothèque cliente du widget de traduction {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent vers le nouvel emplacement (/apps).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété
       <code>
       cq
      </code> :
       <code>
       designPath
      </code>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles de Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet de proxy /etc.clientlibs/..</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

### Console Web d’activation des arborescences {#tree-activation-web-console}

| **Emplacement précédent** | `/etc/replication/treeactivation` |
|---|---|
| **Nouveaux emplacements** | `/libs/replication/treeactivation` |
| **Conseils de restructuration** | Aucune action n’est requise. |
| **Remarques** | La console web d’activation de l’arborescence est désormais disponible via **Outils > Déploiement > Réplication > Activer l’arborescence**. |

{style="table-layout:auto"}

### Services cloud de connecteur de traduction de fournisseur {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les nouveaux services cloud de connecteur de traduction de fournisseur doivent être migrés vers le nouvel emplacement (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ul>
       <li>Créez manuellement de nouvelles configurations de services cloud de connecteur de traduction de fournisseur via <strong>l’interface utilisateur de création AEM dans Outils &gt; Services Cloud &gt; Services cloud de traduction</strong>.<br /> OU </li>
       <li>Copiez les nouvelles configurations des services cloud de connecteur de traduction de fournisseur de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>, <code>/conf/global </code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associez les configurations d’AEM applicables aux hiérarchies de contenu AEM.
      <ol>
       <li>Hiérarchies de page AEM Sites via <strong>AEM Sites &gt; Page &gt; Propriétés de page &gt; Onglet Avancé &gt; Configuration cloud</strong>.</li>
       <li>Hiérarchies de fragments d’expérience AEM via <strong>Fragments d’expérience AEM &gt; Fragment d’expérience &gt; Propriétés &gt; Onglet Services cloud &gt; Configuration cloud</strong>.</li>
       <li>Hiérarchies de dossiers de fragments d’expérience AEM via <strong>Fragments d’expérience AEM &gt; Dossier &gt; Propriétés &gt; Onglet Services cloud &gt; Configuration cloud</strong>.</li>
       <li>Hiérarchies des dossiers AEM Assets via <strong>AEM Assets &gt; Dossier &gt; Propriétés du dossier &gt; Onglet Services cloud &gt; Configuration</strong>.</li>
       <li>Projets AEM via <strong>Projets AEM &gt; Projet &gt; Propriétés du projet &gt; Onglet avancé &gt; Configuration cloud</strong>.</li>
      </ol> </li>
     <li>Dissociez les anciens services cloud de traduction migrés des hiérarchies de contenu AEM mentionnées ci-dessus.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution des services cloud de traduction s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Modèles d’e-mail de notification de workflow {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les modèles d’e-mail de notification de workflow modifiés doivent être migrés vers le nouvel emplacement (<code>/conf/global</code>).</p>
    <ol>
     <li>Copiez les modèles d’e-mail de notification de workflow modifiés de l’emplacement précédent vers le nouvel emplacement.</li>
     <li>Supprimez les modèles d’e-mail de notification de workflow migrés de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution du modèle d’e-mail de notification de workflow s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Packages de workflow {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Migrez les packages de workflow existants situés à l’emplacement précédent vers le nouvel emplacement.</p>
    <ol>
     <li>Supprimez les packages de workflow de l’emplacement précédent qui ne sont pas référencés par un autre contenu ou qui ne sont pas nécessaires.</li>
     <li>Déplacez les packages de workflow de l’emplacement précédent qui ne sont pas référencés par un autre contenu, mais qui sont nécessaires dans le nouvel emplacement.</li>
     <li>Laissez les packages de workflow qui sont référencés par un autre contenu à l’emplacement précédent.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Les packages de workflow créés via la console Miscadmin de l’interface utilisateur classique sont conservés à l’emplacement précédent, tandis que tous les autres sont conservés au nouvel emplacement.</p> <p>Les packages de workflow stockés aux emplacements précédents ou nouveaux peuvent être gérés via la console Miscadmin de l’interface utilisateur classique.</p> </td>
  </tr>
 </tbody>
</table>
