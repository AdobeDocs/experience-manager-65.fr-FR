---
title: Restructuration des référentiels dans AEM 6.5 pour Sites
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Sites.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 100%

---

# Restructuration des référentiels dans AEM 6.5 {#sites-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution AEM Sites. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

**Avec la mise à niveau vers la version 6.5**

* [Segments ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Avant de procéder à la mise à niveau vers une future version**

* [Bibliothèques clientes Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [De Microsoft Word classique à la conception de pages web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurations de l’émulateur d’appareil mobile](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurations de plans directeurs de Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurations du déploiement de Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modèle d’e-mail de notification d’événement de page](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Génération de modèles automatique de pages](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Grille réactive LESS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Conceptions de modèles statiques](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Bibliothèques clientes d’intégration d’Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliothèques clientes de gestion de contenu web de base](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Segments ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Si des segments ContextHub nouveaux ou modifiés sont édités dans le contrôle de source plutôt que dans AEM, ils doivent être migrés vers le nouvel emplacement :</p>
    <ol>
     <li>Copiez les segments ContextHub nouveaux ou modifiés depuis l’emplacement précédent vers le nouvel emplacement approprié (/<code>apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Mettez à jour les références aux segments ContextHub de l’emplacement précédent vers les segments ContextHub migrés dans les nouveaux emplacements client (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La requête QueryBuilder ci-dessous recherche toutes les références aux segments ContextHub dans les emplacements précédents.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Elle peut être exécutée dans l’<a href="/help/sites-developing/querybuilder-api.md" target="_blank">interface utilisateur du débogueur QueryBuilder AEM</a>. Notez qu’il s’agit d’une requête transversale. Par conséquent, ne l’exécutez pas en exploitation et vérifiez que les limites de traversée sont ajustées en fonction des besoins.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Les segments ContextHub persistants à l’emplacement précédent s’affichent en lecture seule dans <strong>AEM &gt; Personnalisation &gt; Audiences</strong>.</p> <p>Si les segments ContextHub doivent être modifiables dans AEM, ils doivent être migrés vers le nouvel emplacement (<code>/conf/global</code> or <code>/conf/&lt;tenant&gt;</code>). Tous les nouveaux segments ContentHub créés dans AEM sont persistants dans le nouvel emplacement (<code>/conf/global</code> or <code>/conf/&lt;tenant&gt;</code>).</p> <p>Les propriétés de la page AEM Sites permettent uniquement la sélection de l’emplacement précédent (<code>/etc</code>) ou d’un nouvel emplacement unique (<code>/apps</code>, <code>/conf/global</code> or <code>/conf/&lt;tenant&gt;</code>). Les segments de ContextHub doivent donc être migrés en conséquence.</p> <p>Tous les segments ContextHub inutilisés des sites de référence AEM peuvent être supprimés et non migrés vers le nouvel emplacement :</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Remarque : si ClientContext est utilisé, il est recommandé de le convertir en ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Avant de procéder à la mise à niveau vers une future version {#prior-to-upgrade}

### Bibliothèques clientes Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie, et non par chemin :</p>
    <ol>
     <li>Toutes les références par chemin d’accès à l’emplacement précédent de la bibliothèque cliente doivent être mises à jour pour utiliser le <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">framework de référencement de la bibliothèque cliente d’AEM</a>.</li>
     <li>Si le framework de référencement de la bibliothèque cliente d’AEM ne peut pas être utilisé, le chemin absolu des bibliothèques clientes peut être référencé via le servlet proxy de bibliothèque cliente d’AEM.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La modification de ces bibliothèques clientes n’a jamais été prise en charge.</p> <p>Pour obtenir les catégories des bibliothèques clientes, accédez à chaque nœud <code>cq:ClientLIbraryFolder</code> via CRXDELite et inspectez la propriété des catégories.</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### De Microsoft Word classique à la conception de pages web {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété cq:designPath.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles du Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception :</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations de l’émulateur d’appareil mobile {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td>Toute nouvelle configuration d’émulateur d’appareil mobile doit être migrée vers le nouvel emplacement.
    <ol>
     <li>Copiez les nouvelles configurations d’émulateur d’appareil mobile de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Pour toutes les pages AEM Sites qui dépendent de ces configurations d’émulateur d’appareil mobile, mettez à jour le nœud de la page <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> : <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Pour les modèles modifiables qui dépendent de ces configurations d’émulateur d’appareil mobile, mettez-les à jour, en faisant pointer <span class="code">
       <code>
        cq
       </code> :
       <code>
        deviceGroups
       </code></span> sur le nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La résolution des configurations d’émulateur d’appareil mobile se produit dans l’ordre suivant :</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Configurations de plans directeurs de Multi-site Manager {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/apps/msm</code> (configurations de plans directeurs clientes)</p> <p><code>/libs/msm</code> (configurations de plans directeurs prêtes à l’emploi pour Screens, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Les configurations de plans directeurs de Multi-site Manager nouvelles ou modifiées doivent être migrées vers le nouvel emplacement (<code>/apps</code>).</p>
    <ol>
     <li>Copiez les configurations de plans directeurs de Multi-site Manager nouvelles ou modifiées de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Supprimez les configurations de plans directeurs de Multi-site Manager migrées de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Toutes les configurations de plans directeurs de Multi-site Manager fournies par AEM existent dans le nouvel emplacement de <code>/libs</code>.</p> <p>Le contenu ne fait pas référence aux configurations de plans directeurs de Multi-site Manager, il n’y a donc pas de références de contenu à ajuster.</p> </td>
  </tr>
 </tbody>
</table>

### Configurations du déploiement de Multi-site Manager {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Toute configuration de déploiement de Multi-site Manager nouvelle ou modifiée doit être migrée vers le nouvel emplacement.</p>
    <ol>
     <li>Copiez les configurations de déploiement de Multi-site Manager nouvelles ou modifiées de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Mettez à jour toutes les références sur les pages AEM vers les configurations de déploiement de Multi-site Manager de l’emplacement précédent, afin qu’elles pointent vers leurs homologues dans les nouveaux emplacements (<code>/libs</code> ou <code>/apps</code>).</li>
    </ol> <p>Supprimez les configurations de déploiement de Multi-site Manager migrées de l’emplacement précédent.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Si vous ne supprimez pas les configurations de déploiement de Multi-site Manager migrées de l’emplacement précédent, les options de déploiement en double seront affichées aux auteurs et autrices d’AEM.</td>
  </tr>
 </tbody>
</table>

### Modèle d’e-mail de notification d’événement de page {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Les seuls nouveaux modèles d’e-mail de notification d’événement de page pris en charge sont ceux qui prennent en charge les nouveaux paramètres régionaux.</p> <p>La résolution du modèle d’e-mail de notification d’événement de page s’effectue dans l’ordre suivant :</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Tout modèle d’e-mail de notification d’événement de page nouveau ou modifié doit être migré vers le nouvel emplacement sous <code>/apps</code> :</p>
    <ol>
     <li>Copiez les modèles d’e-mail de notification d’événement de page nouveaux ou modifiés de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Supprimez les modèles d’e-mail de notification d’événement de page migrés de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Génération de modèles automatique de pages {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td>Les structures créées à l’emplacement précédent utilisent l’infrastructure existante et ne peuvent pas être migrées vers le nouvel emplacement. Pour s’aligner sur le nouvel emplacement, toute génération de modèles automatique existante doit être redéveloppée à l’aide du cadre de génération de modèles automatique pris en charge.</td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Grille réactive LESS {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Toutes les références à l’emplacement précédent dans les fichiers LESS personnalisés doivent être mises à jour pour être importées à partir du nouvel emplacement.</p>
    <ul>
     <li>Mettez à jour tous les fichiers LESS personnalisés faisant référence à grid_base.less dans l’emplacement précédent pour référencer le nouvel emplacement.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Si vous référencez un fichier <code>grid_base.less</code> qui n’existe pas, le mode Mise en page de l’éditeur de pages et de modèles ne fonctionne pas et la mise en page est perturbée.</td>
  </tr>
 </tbody>
</table>

### Conceptions de modèles statiques {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété <code>cq:designPath</code> via <strong>AEM &gt; Sites &gt; Pages de site personnalisées &gt; Propriétés de page &gt; Onglet avancé &gt; Champ de conception</strong>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles du Dispatcher AEM pour autoriser le service des bibliothèques clientes via la servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception :</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>L’approche recommandée consiste à créer des sites et des pages AEM Sites à l’aide de modèles modifiables qui utilisent le contenu et les politiques de la structure au lieu de conceptions.</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Bibliothèques clientes d’intégration d’Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie et non par chemin.</p>
    <ol>
     <li>Toutes les références à la bibliothèque cliente par chemin à l’emplacement précédent doivent être mises à jour pour utiliser le <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">cadre de référencement de la bibliothèque cliente d’AEM</a>.</li>
     <li>Si le cadre de référencement de la bibliothèque cliente d’AEM ne peut pas être utilisé, le chemin absolu des bibliothèques clientes peut être référencé via le servlet proxy de la bibliothèque cliente d’AEM :</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La modification de ces bibliothèques clientes n’a jamais été prise en charge.</p> <p>Pour obtenir les catégories des bibliothèques clientes, accédez à chaque nœud cq:ClientLIbraryFolder via CRXDELite et inspectez la propriété des catégories :</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliothèques clientes de gestion de contenu web de base {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Conseils de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie et non par chemin.</p>
    <ol>
     <li>Toutes les références à la bibliothèque client par chemin à l’emplacement précédent doivent être mises à jour pour utiliser le <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">framework de référencement de la bibliothèque client d’AEM</a>.</li>
     <li>Si le framework de référencement de la bibliothèque cliente d’AEM ne peut pas être utilisé, le chemin absolu des bibliothèques clientes peut être référencé via le servlet proxy de bibliothèque cliente d’AEM.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La modification de ces bibliothèques clientes n’a jamais été prise en charge.</p> <p>Pour obtenir les catégories des bibliothèques clientes, accédez à chaque nœud <code>cq:ClientLIbraryFolder</code> via CRXDELite et inspectez la propriété des catégories :</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
