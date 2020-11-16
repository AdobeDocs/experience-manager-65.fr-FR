---
title: Restructuration des référentiels pour AEM Communities dans la version 6.4
seo-title: Restructuration des référentiels pour AEM Communities dans la version 6.4
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.4 pour Communities.
seo-description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.4 pour Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 60%

---


# Restructuration des référentiels pour AEM Communities dans la version 6.5 {#repository-restructuring-for-aem-communities-in}

As described on the parent [Repository Restructuring in AEM 6.4](/help/sites-deploying/repository-restructuring.md) page, customers upgrading to AEM 6.5 should use this page to assess the work effort associated with repository changes impacting the AEM Communities Solution. Certaines modifications nécessitent un effort de travail pendant le processus de mise à niveau AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau ultérieure.

**Avec la mise à niveau vers la version 6.5**

* [Modèles de notification par e-mail](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurations des abonnements](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Avant la mise à niveau future**

* [Configurations des badges](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Conceptions des consoles des communautés classiques](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurations des connexions au réseau social Facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurations des options linguistiques](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurations des connexions au réseau social Pinterest](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurations des scores](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurations des connexions au réseau social Twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Divers](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Modèles de notification par e-mail {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Manual migration ia needed if you want to move to new path under "<code>/apps/settings</code>". Vous pouvez utiliser le Gestionnaire de configuration Granite pour effectuer la migration.</p> <p>You can perform the migration by setting the property <code>mergeList</code> to <code>true</code> on the "<code>/libs/settings/community/subscriptions</code>" node and add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des abonnements {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Manual migration ia needed if you want to move to new path under "<code>/apps/settings</code>". Vous pouvez utiliser le Gestionnaire de configuration Granite pour effectuer la migration.</p> <p>You can perform the migration by setting the property <code>mergeList</code> to <code>true</code> on the "<code>/libs/settings/community/subscriptions</code>" node and add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des mots-clés {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>Une tâche de migration différée est disponible pour nettoyer les configurations de Communities.<br /> <p>La Tâche déplace les mots-clés <code>/etc/watchwords</code> vers <code>/conf/global/settings/community/watchwords</code>.</p> <p>If customized watchwords are stored in SCM, then they should be deployed to <code>/apps/settings/...</code> and you must ensure that there is not an overlaying <code>/conf/global/settings/...</code> configuration that would take precedence.</p> <p>Migration task removes <code>/etc</code> locations.</p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

## Avant la mise à niveau future {#prior-to-upgrade}

### Configurations des badges {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><strong>Règles de badge :</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Images de badge :</strong></p> <p>Pour les images par défaut : <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Pour les images personnalisées : <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Une migration manuelle est requise.</p> <p>Si votre instance a personnalisé les règles de badge/score, aucune méthode automatisée ne permet de placer toutes les règles dans un compartiment. Vous avez besoin d’informations de la part du client pour savoir quel compartiment de configuration (global ou spécifique à un site) vous souhaitez utiliser pour votre site.</p> <p>Aucune interface utilisateur n’est disponible pour configurer les badges et les scores d’un site.</p> <p>Pour vous aligner sur la nouvelle structure de référentiel :</p>
    <ol>
     <li>Créez un compartiment contextuel de site à l’aide de l’<strong>explorateur de configuration</strong> sous <strong>Outils</strong></li>
     <li>Accédez à la racine du site</li>
     <li>Définissez <code>cq:confproperty</code> sur le chemin du compartiment où vous souhaitez stocker tous vos paramètres. Le même résultat peut être obtenu par le biais de l’<strong>assistant de modification - Définir l’entrée de configuration du cloud</strong>.</li>
     <li>Move relevant badging rules and scoring rules from <code>/etc/community/*</code> to the site context bucket created in the previous step.</li>
     <li>Ajustez les propriétés des règles de badge et de score à la racine du site pour avoir des références relatives aux nouveaux emplacements de règles.
      <ol>
       <li>For example, if the poperty for <code>cq:conf = /conf/we-retail</code>, then <code>badgingRules [] = community/badging/rules</code> if rules are now moved to this new bucket.</li>
      </ol> </li>
     <li>De même, ajustez les références aux règles de score dans un nœud de règle de badge pour obtenir un chemin relatif.</li>
    </ol> <p> </p> <p>Enfin, nettoyer en supprimant la ressource <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Conceptions des consoles des communautés classiques {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des connexions au réseau social Facebook {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute nouvelle configuration de cloud Facebook doit faire l’objet d’une migration vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement les nouvelles configurations des connexions au réseau social Facebook via l’interface utilisateur de création AEM dans <strong>Outils &gt; Services cloud &gt; Configuration de la connexion au réseau social Facebook</strong>.<br /> ou <br /> </li>
       <li>Copy any new Facebook Cloud Configurations from Previous Location to the appropriate New Location, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Facebook Social Login Configuration by setting the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>Dissociez l’ancien service de cloud Facebook Connect Cloud des racines de site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des options linguistiques {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td>N/A<br /> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des connexions au réseau social Pinterest {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute nouvelle configuration de cloud Pinterest doit faire l’objet d’une migration vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement les nouvelles configurations des connexions au réseau social Pinterest via l’interface utilisateur de création AEM dans <strong> Outils &gt; Services cloud &gt; Configuration de la connexion au réseau social Pinterest</strong>.<br /> ou</li>
       <li>Copy any new Pinterest Cloud Configurations from Previous Location to the appropriate New Location under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Pinterest Social Login Configuration by settings the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>Dissociez l’ancien service de cloud Pinterest Connect Cloud des racines de site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des scores {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>To align with new repository structure, scoring rules can be stored in <code>/apps/settings/</code> or /<code>conf/.../settings</code></p>
    <ol>
     <li>For <code>/apps/settings</code>, this would act as global or default rules managed in SCM.</li>
    </ol> <p>Create context-aware configs in <code>/conf/</code> by using CRXDELite:</p>
    <ol>
     <li>Create the configs in the desired <code>/conf/.../settings</code> location<br /> </li>
     <li>Communities site must have the <code>cq:conf </code>property property set.
      <ol>
       <li>If no <code>cq:conf</code> is set, scoring rules would be directly read from the given path for property '<code>scoringRules</code>' at the site's root node, for example: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Nettoyage : Supprimer la ressource <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des connexions au réseau social Twitter {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Toute nouvelle configuration de cloud Twitter doit faire l’objet d’une migration vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement les nouvelles configurations des connexions au réseau social Twitter via l’interface utilisateur de création d’AEM sous <strong> Outils &gt; Services cloud &gt; Configuration de la connexion au réseau social Twitter</strong>.<br /> ou <br /> </li>
       <li>Copy any new Twitter Cloud Configurations from Previous Location to the appropriate New Location, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Twitter Social Login Configuration by setting the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>Dissociez l’ancien service de cloud Twitter Connect Cloud des racines du site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Divers {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Adobe a fourni un utilitaire de migration à l’adresse suivante :</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td>Les modèles personnalisés existants seront déplacés vers <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

