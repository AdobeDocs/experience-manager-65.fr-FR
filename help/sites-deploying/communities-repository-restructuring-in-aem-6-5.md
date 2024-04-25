---
title: Restructurer les référentiels pour AEM Communities dans la version 6.4
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.4 pour Communities.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 100%

---

# Restructuration des référentiels pour AEM Communities dans la version 6.5 {#repository-restructuring-for-aem-communities-in}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers AEM 6.4 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution AEM Communities. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

**Avec la mise à niveau vers la version 6.5**

* [Modèles de notification par e-mail](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurations des abonnements](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Avant de procéder à la mise à niveau vers une future version**

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
   <td><p>Une migration manuelle est requise pour déplacer les configurations vers le nouvel emplacement sous « <code>/apps/settings</code> ». Vous pouvez utiliser le Gestionnaire de configuration Granite pour effectuer la migration.</p> <p>Vous pouvez effectuer la migration en définissant la propriété <code>mergeList</code> sur <code>true</code> sur le nœud « <code>/libs/settings/community/subscriptions</code> » et en ajoutant un nœud enfant <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
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
   <td><p>Une migration manuelle est requise pour déplacer les configurations vers le nouvel emplacement sous « <code>/apps/settings</code> ». Vous pouvez utiliser le Gestionnaire de configuration Granite pour effectuer la migration.</p> <p>Vous pouvez effectuer la migration en définissant la propriété <code>mergeList</code> sur <code>true</code> sur le nœud « <code>/libs/settings/community/subscriptions</code> » et en ajoutant un nœud enfant <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations des signaux {#watchwords-configurations}

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
   <td>Une tâche de migration différée est disponible pour nettoyer les configurations de Communities.<br /> <p>La tâche déplace les mots-clés depuis <code>/etc/watchwords</code> vers <code>/conf/global/settings/community/watchwords</code>.</p> <p>Si des mots-clés personnalisés sont stockés dans SCM, ils doivent être déployés sur <code>/apps/settings/...</code>. Vous devez en outre vérifier qu’aucune configuration de recouvrement <code>/conf/global/settings/...</code> prioritaire n’existe.</p> <p>La tâche de migration supprime les emplacements <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

## Avant de procéder à la mise à niveau vers une future version {#prior-to-upgrade}

### Configurations des badges {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><strong>Règles de badge :</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Images de badge :</strong></p> <p>Pour les images par défaut : <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Pour les images personnalisées : <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>La migration manuelle est requise.</p> <p>Si votre instance a personnalisé les règles de badge/score, aucune méthode automatisée ne permet de placer toutes les règles dans un compartiment. Nécessite des entrées clientes sur le compartiment conf (global ou spécifique au site) à utiliser pour votre site.</p> <p>Aucune interface utilisateur n’est disponible pour configurer le badge et la notation d’un site.</p> <p>Pour aligner la structure du nouveau référentiel :</p>
    <ol>
     <li>Créez un compartiment contextuel de site à l’aide de la variable <strong>Explorateur de configuration</strong> dans <strong>Outils</strong>.</li>
     <li>Accédez à la racine du site.</li>
     <li>Définissez <code>cq:confproperty</code> sur le chemin du compartiment où vous souhaitez stocker tous vos paramètres. Le même résultat peut être obtenu par le biais de l’<strong>assistant de modification - Définir l’entrée de configuration du cloud</strong>.</li>
     <li>Déplacez les règles de badge et de score appropriées depuis <code>/etc/community/*</code> vers le compartiment contextuel de site créé à l’étape précédente.</li>
     <li>Ajustez les propriétés des règles de badge et de score à la racine du site pour avoir des références relatives aux nouveaux emplacements de règles.
      <ol>
       <li>Par exemple, si la propriété est définie pour <code>cq:conf = /conf/we-retail</code>, alors <code>badgingRules [] = community/badging/rules</code> si les règles sont maintenant déplacées vers ce nouveau compartiment.</li>
      </ol> </li>
     <li>De même, ajustez les références aux règles de score dans un nœud de règle de badge pour obtenir un chemin relatif.</li>
    </ol> <p> </p> <p>Enfin, effectuez un nettoyage en supprimant la ressource <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Conceptions des consoles classiques de Communities {#classic-communities-console-designs}

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
   <td>S/O</td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
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
   <td><p>Toute nouvelle configuration du cloud Facebook doit être migrée vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement de nouvelles configurations de connexion sociale à Facebook via l’interface utilisateur de création d’AEM en suivant le chemin <strong>Outils &gt; Cloud Services &gt; Configurations des connexions au réseau social Facebook</strong>.<br /> ou <br /> </li>
       <li>Copiez toute nouvelle configuration de cloud Facebook depuis l’emplacement précédent dans le nouvel emplacement approprié, sous <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Mettez à jour n’importe quelle racine de site AEM Communities pour faire référence à la nouvelle configuration de connexion au réseau social Facebook en définissant la propriété <code>[cq:Page]/jcr:content@cq:conf</code> sur le chemin absolu dans le nouvel emplacement.</li>
     <li>Dissociez l’ancien service de cloud Facebook Connect des racines de site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
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
   <td><strong>Remarques</strong></td>
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
   <td><p>Toute nouvelle configuration du cloud Pinterest doit être migrée vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement les nouvelles configurations des connexions au réseau social Pinterest via l’interface utilisateur de création AEM dans <strong>Outils &gt; Services cloud &gt; Configuration de la connexion au réseau social Pinterest</strong>.<br /> ou</li>
       <li>Copiez toute nouvelle configuration de cloud Pinterest depuis l’emplacement précédent vers le nouvel emplacement approprié sous <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Mettez à jour toute racine de site AEM Communities pour faire référence à la nouvelle configuration de connexion du réseau social Pinterest en définissant la propriété <code>[cq:Page]/jcr:content@cq:conf</code> sur le chemin absolu dans le nouvel emplacement.</li>
     <li>Dissociez l’ancien service de cloud Pinterest Connect des racines de site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
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
   <td><p>Pour s’aligner sur la nouvelle structure de référentiel, les règles de score peuvent être stockées dans <code>/apps/settings/</code> ou /<code>conf/.../settings</code></p>
    <ol>
     <li>Pour <code>/apps/settings</code>, cela agit comme règles globales ou par défaut gérées dans SCM.</li>
    </ol> <p>Créez des configurations selon le contexte dans <code>/conf/</code> à l’aide de CRXDELite :</p>
    <ol>
     <li>Créez des configurations à l’<code>/conf/.../settings</code>emplacement<br /> souhaité. </li>
     <li>La propriété <code>cq:conf </code> doit être définie pour le site Communities.
      <ol>
       <li>Si aucune propriété <code>cq:conf</code> n’est définie, les règles de score sont directement lues à partir du chemin donné pour la propriété ’<code>scoringRules</code>’ au nœud racine du site, par exemple : <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Nettoyage : supprime la ressource. <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
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
   <td><p>Toute nouvelle configuration du cloud Twitter doit être migrée vers le nouvel emplacement.</p>
    <ol>
     <li>Migrez les configurations existantes de l’emplacement précédent vers le nouvel emplacement.
      <ol>
       <li>Recréez manuellement les nouvelles configurations des connexions au réseau social Twitter via l’interface utilisateur de création d’AEM sous <strong>Outils &gt; Services cloud &gt; Configuration de la connexion au réseau social Twitter</strong>.<br /> ou <br /> </li>
       <li>Copiez toute nouvelle configuration de cloud Twitter de l’emplacement précédent dans le nouvel emplacement approprié, sous <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Mettez à jour toute racine de site AEM Communities pour faire référence à la nouvelle configuration de connexion du réseau social Twitter en définissant la propriété <code>[cq:Page]/jcr:content@cq:conf</code> sur le chemin absolu dans le nouvel emplacement.</li>
     <li>Dissociez l’ancien service de cloud Twitter Connect des racines du site AEM Communities mises à jour pour faire référence au nouvel emplacement.</li>
    </ol> </td>
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
   <td><strong>Remarques</strong></td>
   <td>Les modèles personnalisés existants sont déplacés vers <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
