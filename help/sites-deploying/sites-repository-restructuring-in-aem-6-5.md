---
title: Restructuration des référentiels dans AEM 6.5
seo-title: Restructuration des référentiels dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Sites.
seo-description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Mise à niveau
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 80%

---


# Restructuration des référentiels dans AEM 6.5 {#sites-repository-restructuring-in-aem}

Comme décrit sur la page parent [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients qui effectuent la mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer l&#39;effort de travail associé aux modifications du référentiel qui affectent la solution AEM Sites. Certaines modifications nécessitent un effort de travail pendant le processus de mise à niveau AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau ultérieure.

**Avec la mise à niveau vers la version 6.5**

* [Segments ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Avant la mise à niveau future**

* [Bibliothèques clientes Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [De Microsoft Word classique à la conception de pages web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurations de l’émulateur d’appareil mobile](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurations Blueprint de Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurations du déploiement de Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modèle d’e-mail de notification d’événement de page](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Structure de page](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Grille réactive LESS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Conceptions de modèle statique](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Bibliothèques clientes d’intégration Adobe Search and Promote](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Bibliothèques clientes d’intégration Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliothèques clientes WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

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
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Si des segments ContextHub nouveaux ou modifiés doivent être changés dans le contrôle de source plutôt que dans AEM, ils doivent être migrés vers le nouvel emplacement :</p>
    <ol>
     <li>Copiez tous les segments ContextHub nouveaux ou modifiés de l’emplacement précédent vers le nouvel emplacement approprié (/<code>apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Mettez à jour les références aux segments ContextHub de l’emplacement précédent vers les segments ContextHub migrés dans les nouveaux emplacements (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La requête QueryBuilder ci-dessous recherche toutes les références aux segments ContextHub dans les emplacements précédents.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Cette opération peut être exécutée via  <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM interface utilisateur</a> du débogueur QueryBuilder. Notez qu’il s’agit d’une requête transversale. Par conséquent, ne l’exécutez pas en production et vérifiez que les limites de traversée sont ajustées en fonction des besoins.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Les segments ContextHub persistants à l’emplacement précédent s’affichent en lecture seule dans <strong>AEM &gt; Personnalisation &gt; Audiences</strong>.</p> <p>Si les segments ContextHub doivent être modifiables dans AEM, ils doivent être migrés vers le nouvel emplacement (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>). Tout nouveau segment ContentHub créé dans AEM est conservé au nouvel emplacement (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p> <p>Les propriétés de la page AEM Sites permettent uniquement de sélectionner l’emplacement précédent (<code>/etc</code>) ou un nouvel emplacement unique (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>). Les segments ContextHub doivent donc être migrés en conséquence.</p> <p>Tous les segments ContextHub inutilisés des sites de référence AEM peuvent être supprimés et ne pas être migrés vers le nouvel emplacement :</p>
    <ul>
     <li>/etc\/segmentation\/geometrixx/</li>
     <li>/etc\/segmentation\/geometrixx-outdoors</li>
    </ul> <p>Remarque : si ClientContext est en cours d’utilisation, il est recommandé d’effectuer un conversion en ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Avant la mise à niveau ultérieure {#prior-to-upgrade}

### Bibliothèques clientes Adobe Analytics {#adobe-analytics-client-libraries}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit faire référence à la bibliothèque cliente par catégorie et non par chemin :</p>
    <ol>
     <li>Toute référence à la bibliothèque cliente par chemin d’accès à l’emplacement précédent doit être mise à jour pour utiliser l’<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">infrastructure de référencement de la bibliothèque cliente AEM</a>.</li>
     <li>Si l’infrastructure de référencement des bibliothèques clientes AEM ne peut pas être utilisée, le chemin absolu des bibliothèques clientes peut être référencé via la servlet proxy des bibliothèques clientes AEM.
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

### De Microsoft Word classique à la conception de pages web {#classic-microsoft-word-to-web-page-designs}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en une <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans la propriété cq:designPath.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles du répartiteur AEM pour autoriser la diffusion des bibliothèques clientes par le biais de la servlet proxy <code>/etc.clientlibs/</code>.</li>
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
   <td><strong>Conseil de restructuration</strong></td>
   <td>Toute nouvelle configuration d’émulateur d’appareil mobile doit être migrée vers le nouvel emplacement.
    <ol>
     <li>Copiez toute nouvelle configuration d'émulateur de périphérique mobile de l'emplacement précédent vers le nouvel emplacement (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Pour toutes les pages AEM Sites qui dépendent de ces configurations d'émulateur de périphérique mobile, mettez à jour le <span class="code">  de la page.
       <code>
        jcr
       </code>
       Noeud <code>
        :content
       </code></span> : <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = Chaîne[ mobile/groupes/réactif ]</span></li>
     <li>Pour tous les modèles modifiables qui dépendent de ces configurations d'émulateur de périphériques mobiles, mettez à jour les modèles modifiables en pointant le <span class="code">
       <code>
        cq
       </code> :
       <code>
        deviceGroups
       </code></span> au nouvel emplacement.</li>
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

### Configurations Blueprint de Multi-site Manager {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/apps/msm</code> (Configurations du plan directeur client)</p> <p><code>/libs/msm</code> (Configurations du plan directeur prêtes à l'emploi pour les écrans, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les configurations Blueprint de Multi-site Manager nouvelles ou modifiées doivent être migrées vers le nouvel emplacement (<code>/apps</code>).</p>
    <ol>
     <li>Copiez les configurations Blueprint de Multi-site Manager nouvelles ou modifiées de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Supprimez les configurations Blueprint de Multi-site Manager migrées de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Toutes les configurations Blueprint de Multi-site Manager fournies par AEM existent dans le nouvel emplacement de <code>/libs</code>.</p> <p>Le contenu ne fait pas référence aux configurations Blueprint de Multi-site Manager. Par conséquent, il n’y a pas de références de contenu à ajuster.</p> </td>
  </tr>
 </tbody>
</table>

### Configurations du déploiement de Multi-site Manager  {#multi-site-manager-rollout-configurations}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute configuration de déploiement de Multi-site Manager nouvelle ou modifiée doit être migrée vers le nouvel emplacement.</p>
    <ol>
     <li>Copiez les configurations de déploiement de Multi-site Manager nouvelles ou modifiées de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Mettez à jour toutes les références sur AEM pages vers les configurations de déploiement multisite Manager à l'emplacement précédent, afin de pointer vers leurs homologues dans les nouveaux emplacements (<code>/libs</code> ou <code>/apps</code>).</li>
    </ol> <p>Supprimez les configurations de déploiement de Multi-site Manager migrées de l’emplacement précédent.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Si vous ne supprimez pas les configurations de déploiement de Multi-site Manager migrées de l’emplacement précédent, des options de déploiement en double sont affichées pour les auteurs d’AEM.</td>
  </tr>
 </tbody>
</table>

### Modèle d’e-mail de notification d’événement de page  {#page-event-notification-e-mail-template}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Les seuls nouveaux modèles d’e-mail de notification d’événement de page gérés doivent prendre en charge de nouveaux paramètres régionaux.</p> <p>La résolution des modèle d’e-mail d’événement se produit dans l’ordre suivant :</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>Tout modèle de courriel de notification de Événement de page nouveau ou modifié doit être migré vers le nouvel emplacement sous <code>/apps</code> :</p>
    <ol>
     <li>Copiez les modèles d’e-mail de notification d’événement de page nouveaux ou modifiés de l’emplacement précédent vers le nouvel emplacement (<code>/apps</code>).</li>
     <li>Supprimez les modèles d’e-mail de notification d’événement de page migrés de l’emplacement précédent.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Structure de page {#page-scaffolding}

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
      </code>/template-types/échafaudage/échafaudage</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/échafaudage/échafaudage</span></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>Les structures créées à l’emplacement précédent utilisent l’infrastructure existante et ne peuvent pas être migrées vers le nouvel emplacement. Pour s’aligner sur le nouvel emplacement, toute structure existante doit être re-développée à l’aide de l’infrastructure prise en charge.</td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>S/O<br /> </td>
  </tr>
 </tbody>
</table>

### Grille réactive LESS  {#responsive-grid-less}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute référence à l’emplacement précédent dans les fichiers LESS personnalisés doit être mise à jour pour pouvoir être importée à partir du nouvel emplacement.</p>
    <ul>
     <li>Mettez à jour tous les fichiers LESS personnalisés faisant référence à grid_base.less dans l’emplacement précédent pour référencer le nouvel emplacement.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>Si vous référencez un fichier <code>grid_base.less</code> qui n’existe pas, le mode Mise en page de l’éditeur de pages et de modèles ne fonctionne pas et la mise en page est perturbée.</td>
  </tr>
 </tbody>
</table>

### Conceptions de modèle statique {#static-template-designs}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Pour les conceptions gérées dans SCM et qui ne sont pas écrites au moment de l’exécution via les boîtes de dialogue de conception.</p>
    <ol>
     <li>Copiez les conceptions de l’emplacement précédent dans le nouvel emplacement (<code>/apps</code>).</li>
     <li>Convertissez les ressources statiques, CSS et JavaScript dans la conception en une <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">bibliothèque cliente</a> avec <code>allowProxy = true</code>.</li>
     <li>Mettez à jour les références à l’emplacement précédent dans propriétés de <code>cq:designPath</code> via <strong>AEM &gt; Sites &gt; Pages de site personnalisées &gt; Propriétés de page &gt; Onglet avancé &gt; Champ de conception</strong>.</li>
     <li>Mettez à jour les pages faisant référence à l’emplacement précédent pour utiliser la nouvelle catégorie de bibliothèque cliente (cela nécessite la mise à jour du code d’implémentation de la page).</li>
     <li>Mettez à jour les règles du répartiteur AEM afin d’autoriser la diffusion de bibliothèques clientes via la servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Pour les conceptions NON gérées dans SCM et modifiées au moment de l’exécution via les boîtes de dialogue de conception :</p>
    <ul>
     <li>Ne déplacez pas les conceptions activées par l’auteur en dehors de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>L’approche recommandée consiste à créer des sites et des pages AEM Sites à l’aide de modèles modifiables qui utilisent le contenu et les règles de la structure au lieu de conceptions.</td>
  </tr>
 </tbody>
</table>

### Bibliothèques clientes d’intégration Adobe Search and Promote  {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie, et non par le chemin.</p>
    <ol>
     <li>Toute référence à la bibliothèque cliente par chemin d’accès à l’emplacement précédent doit être mise à jour pour utiliser l’<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">infrastructure de référencement des bibliothèques clientes AEM</a>.</li>
     <li>Si l’infrastructure de référencement des bibliothèques clientes AEM ne peut pas être utilisée, le chemin absolu des bibliothèques clientes peut être référencé via la servlet proxy des bibliothèques clientes AEM :</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td><p>La modification de ces bibliothèques clientes n’a jamais été prise en charge.</p> <p>Pour obtenir les catégories des bibliothèques clientes, accédez à chaque nœud cq:ClientLIbraryFolder via CRXDELite et inspectez la propriété des catégories :</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliothèques clientes d’intégration Adobe Target {#adobe-target-integration-client-libraries}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie, et non par le chemin.</p>
    <ol>
     <li>Toute référence à la bibliothèque cliente par chemin d’accès à l’emplacement précédent doit être mise à jour pour utiliser l’<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">infrastructure de référencement des bibliothèques clientes AEM</a>.</li>
     <li>Si l’infrastructure de référencement des bibliothèques clientes AEM ne peut pas être utilisée, le chemin absolu des bibliothèques clientes peut être référencé via la servlet proxy des bibliothèques clientes AEM :</li>
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

### Bibliothèques clientes WCM Foundation {#wcm-foundation-client-libraries}

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
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute utilisation personnalisée de ces bibliothèques clientes doit référencer la bibliothèque cliente par catégorie, et non par le chemin.</p>
    <ol>
     <li>Toute référence à la bibliothèque cliente par chemin d’accès à l’emplacement précédent doit être mise à jour pour utiliser l’<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">infrastructure de référencement des bibliothèques clientes AEM</a>.</li>
     <li>Si l’infrastructure de référencement des bibliothèques clientes AEM ne peut pas être utilisée, le chemin absolu des bibliothèques clientes peut être référencé via la servlet proxy des bibliothèques clientes AEM.</li>
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

