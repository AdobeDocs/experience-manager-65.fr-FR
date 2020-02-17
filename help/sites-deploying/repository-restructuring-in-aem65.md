---
title: Restructuration des référentiels dans AEM 6.5
seo-title: Restructuration des référentiels dans AEM 6.5
description: En savoir plus sur la restructuration du référentiel dans AEM 6.5
seo-description: En savoir plus sur la restructuration du référentiel dans AEM 6.5
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# Restructuration des référentiels dans AEM 6.5 {#repository-restructuring-in-aem}

## Présentation {#introduction}

Avant AEM 6.5, le code client était déployé dans des zones imprévisibles du JCR susceptibles d’être modifiées lors des mises à niveau. C’est pourquoi il était courant que les versions formelles d’AEM (versions majeures, packs de fonctionnalités, Service Packs ou correctifs) écrasent le code, la configuration ou le contenu personnalisé. En outre, il arrivait parfois que les modifications utilisateurs écrasent le contenu ou le code de produit AEM, empêchant le fonctionnement du produit.

Ces conflits ne pouvaient pas toujours être résolus automatiquement. Leur signalement demandait un temps considérable et leur résolution (qui n’était pas toujours simple) nécessitait une intervention humaine. Il est possible d’éviter ces conflits en définissant clairement les hiérarchies applicables au code du produit AEM et au code client.

To that end, beginning in AEM 6.5 and to be continued in future releases, content is being restructured out of `/etc` to other folders in the repository, along with guidelines on what content goes  where,  adhering to the following high-level rules:

* AEM product code will always be placed in `/libs`, which must not be overwritten by custom code
* Custom  code should be placed in `/apps`, `/content`, and `/conf`

This article is organized into three sections, representing the type of content that has been moved out of `/etc`:

1. Configuration
1. Bibliothèques côté client
1. Divers

Chaque section comprend les éléments suivants :

* Un tableau avec les emplacements restructurés et du contenu supplémentaire. Il est prévu, à court terme, de formater les tableaux avec une structure plus aplatie afin d’en améliorer la lisibilité.
* Une stratégie d’extensibilité permettant au code personnalisé d’étendre le code d’application AEM résidant sous `/libs`.

## Compatibilité descendante {#backwards-compatibility}

Dans la plupart des cas, la compatibilité ascendante avec les anciens emplacements est conservée après la mise à niveau vers AEM 6.5. Pour ce faire, les anciens emplacements sont préservés et respectés par le code de produit, en plus des nouveaux emplacements ajoutés. Dans la plupart des cas, la logique conditionnelle permet de vérifier si le dossier hérité existe et de lire le contenu à partir de là au lieu du nouvel emplacement.

Après avoir effectué la mise à niveau vers la version 6.5, les utilisateurs sont invités, selon leur propre calendrier, à supprimer les emplacements précédents, de sorte que le contenu des nouveaux emplacements soit utilisé. Les tableaux ci-dessous contiennent des instructions pour adhérer à la nouvelle structure de contenu par emplacement.

>[!NOTE]
>
>Une instance mise à niveau statique comprend les anciens emplacements de contenu en plus des nouveaux emplacements. Une nouvelle installation développeur ne contient que les nouveaux emplacements.

## Comment lire les tableaux {#how-to-read-the-tables}

Dans chaque section, le tableau se compose des éléments suivants :

* La solution AEM (Sites, Assets, Forms, etc.) pour laquelle ce contenu est pertinent.
* L’ancien emplacement (versions 6.4 et antérieures).
* Le nouvel emplacement 6.5.
* Instructions à suivre pour s’aligner sur la nouvelle structure de contenu. Par exemple, il peut s’avérer nécessaire d’exécuter un script ou de déplacer des fichiers manuellement dans les semaines ou les mois qui suivent une mise à niveau vers la version 6.5.
* La méthode utilisée par AEM pour garantir la rétrocompatibilité des anciens emplacements de contenu pour les clients qui mettent à niveau une version antérieure vers la version AEM 6.5.

## Configuration{#configuration}

The content locations in this section generally refer to content that resides under a `/settings` folder under `/libs`, `/apps`, or `/conf`.

### Stratégie d’extensibilité {#extensibility-strategy}

In general, but with a few exceptions, content under this section can be extended using Apache Sling&#39;s [   Context Aware   Configuration](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) feature.

En bref, la configuration basée sur le contexte permet de superposer plusieurs fois le contenu d’une partie du référentiel par le contenu d’autres parties du référentiel. Par exemple, le contenu `/libs` peut être superposé par le contenu dans `/apps`, qui peut ensuite être superposé par le contenu dans `/conf`. Moreover, content in a global folder under `/conf` can be overlayed by a specific &quot;tenant&quot; or &quot;site&quot; (e.g. `/conf/we-retail/settings`).

En règle générale, la configuration basée sur le contexte est utilisée comme stratégie pour étendre les configurations de fonctionnalités, mais il existe des cas où elle est utilisée par d&#39;autres types de contenu.

Le tableau ci-dessous inclut une colonne supplémentaire nommée &quot;Type de configuration&quot; pour expliquer dans quelle mesure une configuration peut être superposée. Voici quelques informations supplémentaires sur ces types de configuration :

**not context-aware**

* Resources happen to be in context-aware folder structures (like `/libs/settings`) but always referenced via absolute path so context awareness is not in effect.
* Les ressources peuvent se trouver n’importe où. For example, Assets DRM Licenses could be at `/content/my-customer/licenses/creative-commons.html`
* Exemples :

   * Workflow scripts -> `/apps/settings/workflow/scripts/noop.ecma`
   * Licences DRM Ressources -> `/apps/settings/dam/drm/my-license`

**only global**

* Fonctionnalité avec la configuration only global
* As a reference point, take the precedence of settings in this example: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM prend en charge la configuration only global, et non les configurations basées sur le locataire.
* AEM commencera toujours à rechercher les configurations au niveau /conf/global en premier

* Exemples :

   * Lanceurs de workflow -> `/libs/settings/workflow/launcher`
   * Modèles de workflow -> `/conf/global/settings/workflow/models`

**tenant-aware**

* For tenant-aware configurations, see this example for the precedence of configuration paths: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, where we-retail is the tenant name. Les configurations basées sur le locataire prennent également en charge les sous-locataires.

* AEM prend en charge les configurations basées sur le locataire. It respects `cq:conf` property on hierarchy
* Exemples :

   * Modèles modifiables -> `/conf/we-retail/settings/wcm/templates`
   * Configurations du cloud -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>Solution</strong></td>
   <td><strong>Emplacement précédent</strong><br /> </td>
   <td><strong>Nouvel emplacement</strong></td>
   <td><strong>Type de configuration Context-Aware</strong><br /> </td>
   <td><strong>Méthode de compatibilité descendante</strong></td>
   <td><strong>Conditions requises pour s’aligner sur le modèle le plus récent</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>tenant-aware</td>
   <td><p>Services cloud hérités.</p> <p>Conservés lors d’une mise à niveau statique. Le code permettant de les lister et de les lire est toujours présent dans AEM comme solution de secours.</p> </td>
   <td>L’utilitaire de migration différée du contenu peut être déclenché par l’interface de migration de Forms afin d’effectuer une conversion automatique vers le nouveau chemin d’accès.<br /> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>tenant-aware</td>
   <td><p>Services cloud hérités.</p> <p>Conservés sur une configuration mise à niveau statique. Le code permettant de les lister et de les lire est toujours présent dans AEM comme solution de secours.</p> </td>
   <td>L’utilitaire de migration différée du contenu peut être déclenché par l’interface de migration de Forms afin d’effectuer une conversion automatique vers le nouveau chemin d’accès.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>tenant-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>tenant-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>not context-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>tenant-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td><p>Project level customizations need to be cut and pasted under the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</p> <p>Lors de l’exécution du workflow d’assimilation des ressources personnalisé, les références à l’ancien emplacement sous /etc subsistent dans la configuration du processus d’extraction des médias. Parallèlement au déplacement des scripts du dossier /etc vers les emplacements /apps et /conf équivalents, il convient de modifier les arguments du processus d’extraction des médias personnalisé (en définissant des chemins d’accès relatifs au lieu des chemins absolus), afin de tenir compte des modifications.</p> <p>Pour plus d’informations, consultez <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">cette page</a>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>tenant-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>tenant-aware</td>
   <td>Les structures de contenu héritées se voient accorder une priorité plus élevée que les nouvelles structures prêtes à l’emploi.</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>not context-aware</td>
   <td><p>Les Consuming Services ont connaissance de l’emplacement précédent.</p> <p>Les configurations de l’emplacement hérité sont prises en compte.</p> </td>
   <td><br /> Move custom content from <code>/etc/design</code> to <code>/apps/settings/wcm/design</code> for alignment with the new repository structure. Par la suite, pensez à mettre à niveau vos sites afin d’utiliser la fonctionnalité des modèles modifiables, laquelle rend inutiles le mode de conception et donc ce contenu.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>not context-aware</td>
   <td>The components in the old location under <code>/etc/scaffolding</code> will continue to function, but have been deprecated.</td>
   <td>Adobe vous recommande d’utiliser les nouveaux composants de structure (scaffolding) sous le nouvel emplacement.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm pour les configurations de plan d'écrans et de plan de commerce prêtes à l'emploi</p> <p> </p> </td>
   <td>not context-aware</td>
   <td><p>Les Consuming Services ont connaissance de l’emplacement précédent.</p> <p>Les configurations de l’emplacement hérité sont prises en compte.</p> </td>
   <td>Les configurations doivent être copiées sur les nouveaux emplacements.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>tenant-aware</td>
   <td>La fonctionnalité tire parti du Gestionnaire de configuration et prend toujours en charge l’ancien emplacement comme solution de secours.</td>
   <td>
    <ol>
     <li>Déplacer les configurations de <code>/etc</code> vers <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>Ensuite, mettez à jour la référence dans le contenu comme suit :</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/D</td>
   <td><p>Les Consuming Services ont connaissance de l’emplacement précédent.</p> <p>Si des configurations sont détectées dans l’emplacement hérité, elles sont utilisées.</p> </td>
   <td>To align with the new model, configurations need to be created in the new locations, and the old ones under <code>/etc</code> must be deleted.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>tenant-aware</td>
   <td><p>Les segments issus de l’ancien emplacement :</p>
    <ul>
     <li>restent en mode lecture seule dans la console Audiences ;</li>
     <li>sont toujours chargés sur la page (si le chemin d’accès donné est sélectionné dans <strong>Propriétés de page &gt; Personnalisation &gt; Chemin d’accès de segments</strong>) ;</li>
     <li>Peut être utilisé pour le ciblage de contenu.</li>
    </ul> </td>
   <td>Vous pouvez utiliser l’<a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">outil de migration de segments</a> pour effectuer une migration vers le nouvel emplacement.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/A</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>Le code connaît l’emplacement de l’ancien modèle. Les modèles existants continueront à être référencés et lus/écrits à partir de <code>/etc</code>.</p> <p><br /> S’agissant des modèles de courrier électronique, si le client avait déjà défini ses modèles personnalisés à un autre emplacement en configurant le chemin d’accès <strong>Racine des modèles</strong> dans la <strong>Configuration de réponse électronique d’AEM Communities</strong>, aucun changement n’est à signaler.</p> </td>
   <td><p>A <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">migration utility</a> can align to the latest AEM Communities templates model.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>Règles de badge :</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Images de badge :</strong></p> <p>The out of the box images in the old location at <code>/etc/community/badging/images</code> are moved to <code>/libs/community/badging/images </code> </p> <p> </p> <p>Custom images are moved to <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>tenant-aware</td>
   <td><p>Le code connaît les anciens chemins d’attribution de badges.</p> <p><br /> Il vérifie d’abord l’existence de chemins plus anciens<br />. S’il n’en existe pas, il utilise les nouveaux.</p> </td>
   <td><p>Une migration manuelle est requise pour une mise en conformité avec le modèle le plus récent. Pour ce faire, procédez comme suit :</p>
    <ol>
     <li>Créez un compartiment contextuel de site à l’aide de l’explorateur de configuration sous <strong>Outils</strong>.</li>
     <li>Accédez à la racine du site.</li>
     <li>Définissez la propriété <code>cq:conf</code> sur le chemin d’accès du compartiment où vous souhaitez stocker toutes les configurations. Vous pouvez obtenir le même résultat en utilisant <strong>Assistant d’édition de site - Définir l’entrée de configuration cloud</strong>, puis en enregistrant les modifications.</li>
     <li>Move the relevant badging rules and scoring rules from <code>etc/community/*</code> to the site context bucket created in the previous step</li>
     <li>Modifiez les propriétés <code>badgingRules</code> et <code>scoringRules</code> à la racine du site pour qu’elles présentent des références relatives vers les nouveaux emplacements de règles. As an example, if <code>cq:conf</code> is set to <code>/conf/we-retail</code>, the value for <code>badgingRules</code> will be <code>community/badging/rules</code> if rules are now moved to this new bucket</li>
     <li>De même, configurez les références aux règles de notation dans un nœud de règle d’attribution de badges pour qu’elles aient un chemin d’accès relatif.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>tenant-aware</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>Le code connaît les anciens chemins d’attribution de badges.</p> <p><br /> Il vérifie d’abord l’existence de chemins plus anciens<br />. S’il n’en existe pas, il utilise les nouveaux.</p> </td>
   <td><p>Des étapes de migration manuelle doivent être exécutées pour une mise en conformité avec le modèle le plus récent.</p> <p>Elles sont identiques à celles des règles d’attribution de badges ci-dessus.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>not context-aware</td>
   <td><p>Ces configurations ne sont pas rétrocompatibles. Reportez-vous à la colonne « Conditions requises pour une mise en conformité avec le modèle le plus récent » pour connaître la procédure de migration vers les nouveaux emplacements.<br /> </p> <br /> </td>
   <td><p>Une migration manuelle est requise pour une mise en conformité avec le modèle le plus récent. Vous pouvez utiliser le Gestionnaire de configuration Granite pour déplacer les configurations vers le nouvel emplacement sous <code>/apps/settings</code>.</p> <p>Therefore, you need to set the <code>mergeList</code> property to true on the <code>/libs/settings/community/subscriptions</code> node and then add an <code>nt:unstructured</code> child node.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>not context-aware</td>
   <td>Ces configurations ne sont pas rétrocompatibles. Reportez-vous à la colonne « Conditions requises pour une mise en conformité avec le modèle le plus récent » pour connaître la procédure de migration vers les nouveaux emplacements.</td>
   <td><p>Une migration manuelle est requise pour une mise en conformité avec le modèle le plus récent. Vous pouvez utiliser le Gestionnaire de configuration Granite pour déplacer les configurations vers le nouvel emplacement sous <code>/apps/settings</code>.</p> <p>Therefore, you need to set the <code>mergeList</code> property to true on the <code>/libs/settings/community/subscriptions</code> node and then add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>Global</td>
   <td>Ces configurations sont rétrocompatibles. Si les anciens chemins d’accès sont détectés, ils sont utilisés. Dans le cas contraire, les nouveaux chemins d’accès sont prioritaires.</td>
   <td><p>La tâche de migration différée du contenu est disponible sous la forme <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Pour plus d’informations, consultez la <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">documentation de la migration différée</a>.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/D</td>
   <td>Ces configurations sont rétrocompatibles. Si les anciens chemins d’accès sont détectés, ils sont utilisés. Dans le cas contraire, les nouveaux chemins d’accès sont prioritaires.</td>
   <td><p>La tâche de migration différée du contenu est disponible sous la forme <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Watchwords will have to be manually moved from <code>/etc/watchwords</code> to <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>Global</td>
   <td><p>Legacy location is used if present and no configuration exists in <code>/libs</code> or <code>/conf</code>.</p> <p>When editing OOTB workflow models, context-aware overlays must be created under <code>/conf</code> to allow them to be modifiable.</p> <p>Package export needs to include the model in <code>/libs</code> or <code>/conf</code> and the runtime model in <code>/var/workflow/models.</code></p> </td>
   <td><p>Newly created models will be created in the <code>/conf/global/settings</code> location.</p> <p>Any edits in <code>/etc</code> or <code>/libs</code> require you to explicitly create an override in <code>/conf/global/settings</code> before editing can be done. The Edit button has to be selected, and it will cause the override in <code>/conf</code> to be created and editing allowed.</p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>Global</td>
   <td>Legacy location is used if present and no configuration<br /> exists in <code>/libs</code> or <code>/conf</code> locations. De cette manière, les lanceurs personnalisés sont conservés.</td>
   <td><p>Newly created or edited launcher configurations are located in the <code>/conf</code> location.</p> <p>All launchers should be moved from the legacy <code>/etc</code> location to<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>Global</td>
   <td>Legacy location is used if present and no configuration<br /> exists in <code>/libs</code> or <code>/conf</code> locations. De cette manière, les modèles de workflow personnalisés sont conservés.</td>
   <td><p>All workflow models should be moved from the legacy <code>/etc</code> location to <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>not context-aware</td>
   <td><p>S’il est présent, l’emplacement hérité est utilisé à des fins de compatibilité descendante.</p> <p>Auparavant, les modèles prêts à l’emploi devaient être écrasés par le biais d’une modification dans <code>/etc</code>. Now, override should be stored in <code>/conf/global</code>.</p> </td>
   <td>Pour plus d’informations, consultez la documentation des workflows.<br /> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>tenant-aware</td>
   <td>Services cloud hérités. Seront conservés sur une configuration mise à niveau statique. Le code permettant de les lister et de les lire est toujours présent dans le produit comme solution de secours.</td>
   <td><p>In order to move cloud configurations to <code>/conf</code>, you can either:</p>
    <ul>
     <li>Créer des configurations à l’aide de la nouvelle interface utilisateur tactile<br /> ou<br /> </li>
     <li>Copy the configurations from <code>/etc/cloudservices/translation</code> to their respective new location(s)</li>
    </ul> <p>Once this is done, the configurations need to be associated with Sites via <strong>Sites &gt; Properties</strong> in the user interface.</p> <p><em>Remarque : Pour que cela fonctionne, les connecteurs de traduction doivent être compatibles avec AEM 6.5.</em></p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>tenant-aware</td>
   <td>Services cloud hérités. Seront conservés sur une configuration mise à niveau statique. Le code permettant de les lister et de les lire est toujours présent dans le produit comme solution de secours.</td>
   <td><p>In order to move cloud configurations to <code>/conf</code>, you can either:</p>
    <ul>
     <li>Créer des configurations à l’aide de la nouvelle interface utilisateur tactile ou<br /> </li>
     <li>Copy older configurations from <code>/etc/cloudservices/translation</code> to their respective new location(s)</li>
    </ul> <p>Once this is done, the configurations need to be associated with Sites via <strong>Sites &gt; Properties</strong> in the user interface.</p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>tenant-aware</td>
   <td><p>Existing entries under <code>/etc</code> remain in place on upgrading the instance.</p> <p>Si vous accédez à l’interface utilisateur des paramètres de cloud après la mise à niveau, les paramètres de cloud existants sont copiés dans la nouvelle structure de référentiel, tout en conservant le contenu existant à des fins de compatibilité descendante.</p> </td>
   <td><p>Les modèles de contenu sont les mêmes. Seul l’emplacement a été modifié pour s’aligner sur les configurations sensibles au contexte (Context-Aware).</p> <p>La <a href="/help/sites-deploying/lazy-content-migration.md">tâche de migration différée</a> portant sur ces paramètres de cloud effectue les opérations suivantes :</p>
    <ul>
     <li>Copier les paramètres de cloud existants dans <code>/etc/cloudsettings</code> la section <code>/conf/global/settings/cloudsettings</code></li>
     <li>Supprimer tous les enfants de <code>/etc/cloudsettings</code></li>
    </ul> <p>Quelques étapes manuelles doivent toutefois être effectuées après la mise à niveau et avant d’exécuter les tâches de migration différée :</p>
    <ul>
     <li>All references pointing to <code>/etc/cloudsettings/*</code> need to be updated to point to <code>/conf/global</code></li>
    </ul> <p>Avertissement :</p>
    <ul>
     <li>The <code>/etc/cloudsettings</code> container needs to be preserved</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>only global</td>
   <td><p>La configuration cloud pour l’installation Dynamic Media - Scene (mode d’exécution <code>dynamicmedia_scene7</code> 7) reste au même emplacement. Le processus fonctionne en l’état. Si vous devez modifier la valeur de configuration du cloud, deux options s’offrent à vous :</p>
    <ol>
     <li>Mettre à jour la configuration existante au moyen de l’ancienne interface utilisateur de configuration cloud.</li>
     <li>Créer une configuration cloud au moyen de la nouvelle interface utilisateur tactile. Cette interface est prioritaire.</li>
    </ol> </td>
   <td><p>Pour vous aligner sur le modèle le plus récent, vous devez télécharger le script situé à l’adresse suivante :</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>only global</td>
   <td><p>The OOTB viewer presets will only be available in the new location, while the custom viewer preset will still be under <code>/etc</code> until a modification is incurred.</p> <p>Une fois la modification effectuée, ces paramètres prédéfinis seront enregistrés dans le nouvel emplacement par le biais d’une migration différée. Lors de la réception d’une demande, le serveur d’images incorporé regardera à l’emplacement hérité et au nouvel emplacement. Il n’est donc pas nécessaire de modifier l’URL, ni le code intégré.</p> </td>
   <td><p>Les paramètres prédéfinis par défaut de la visionneuse ne seront disponibles que dans le nouvel emplacement. Dans le cas des paramètres prédéfinis personnalisés, vous devez exécuter le script de migration à cet emplacement :</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>Comme c’est le cas pour le scénario de rétrocompatibilité, vous ne devez pas modifier la fonction copyURL ni le code intégré pour qu’il pointe vers <code>/conf</code>. The existing request to <code>/etc</code> will be re-routed under the hood to the correct content from <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>only global</td>
   <td>The macro under <code>/etc</code> is still valid. If modify it, the modified node will be moved to the new location under <code>/conf</code> via a Lazy Migration task.</td>
   <td><p>Vous devez exécuter le script de migration à cet emplacement :</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/D</td>
   <td><p>Le profil vidéo prêt à l’emploi sera supprimé sans mettre à jour la propriété des dossiers de ressources pour qu’elle pointe vers le profil.</p> <p>Le processus de codage intègre un mécanisme de conversion qui transforme l’ancien chemin d’accès pour qu’il pointe vers le nouveau chemin d’accès au profil.</p> </td>
   <td>Aucune modification n’est requise.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>only global</td>
   <td><p>Le profil vidéo personnalisé est conservé en l’état jusqu’à ce que vous le modifiiez.</p> <p>Il est ensuite transféré vers le nouvel emplacement par le biais d’une tâche de migration différée. Ceci est semblable à la vidéo prête à l’emploi prédéfinie lors de la recherche d’encodage. Le processus de codage s’accompagne d’un convertisseur de chemin d’accès intégré qui recherche le profil vidéo dans l’ancien emplacement, puis dans le nouvel emplacement.</p> </td>
   <td><p>Pour vous aligner sur le modèle le plus récent, vous pouvez exécuter le script situé à l’adresse suivante :</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>only global</td>
   <td><p>Cette configuration cloud pour l’installation hybride Dynamic Media (mode d’exécution <code>dynamicmedia</code> ) ) reste au même emplacement. Le processus fonctionne en l’état. Si vous devez modifier la valeur de configuration, deux options s’offrent à vous :</p>
    <ol>
     <li>Mettre à jour une configuration existante au moyen de l’ancienne interface utilisateur de configuration cloud.</li>
     <li>Créer une configuration cloud au moyen de la nouvelle interface utilisateur tactile. Cette interface est prioritaire.</li>
    </ol> </td>
   <td><p>Vous devez exécuter le script de migration pour une mise en conformité avec le modèle le plus récent. Le script est accessible à l’adresse suivante :<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>only global</td>
   <td><p>La configuration cloud pour l’installation DM-Youtube reste au même emplacement. Le processus fonctionne en l’état. Si vous devez modifier la valeur de configuration cloud, deux options s’offrent à vous :</p>
    <ol>
     <li>Mettre à jour une configuration existante au moyen de l’ancienne interface utilisateur de configuration cloud.</li>
     <li>Créer une configuration cloud au moyen de la nouvelle interface utilisateur tactile. Cette interface est prioritaire.</li>
    </ol> </td>
   <td><p>Vous pouvez exécuter un script de migration pour vous aligner sur le modèle le plus récent. Ce script est accessible à l’adresse suivante :<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>only global</td>
   <td>Aucune action requise.</td>
   <td><p>Vous pouvez exécuter un script de migration pour vous aligner sur le modèle le plus récent. Ce script est accessible à l’adresse suivante :<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>only global</td>
   <td>The templates in <code>/etc/notification/email/default/</code> are given precedence over the ones in <code>/libs/settings/notification-templates</code>.</td>
   <td>In order to align to the latest model, you can create new templates under <code>/apps/settings/notification-templates</code> and perform new modifications there.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/D</td>
   <td><p>Les Consuming Services ont connaissance de l’emplacement précédent.</p> <p>Si des configurations sont détectées dans l’emplacement hérité, elles sont utilisées.</p> </td>
   <td>To align with the new model, configurations need to be created in the new locations, and the old ones under <code>/etc</code> must be deleted.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>not context-aware</td>
   <td>Veuillez tenir compte du fait que les langues personnalisées doivent être ajoutées à la liste.<br /> </td>
   <td>Superposez et mettez à jour la nouvelle liste avec des langues supplémentaires, le cas échéant. Alternatively, copying the old list to <code>/apps</code> location would also work.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>only global</td>
   <td>Elles seront conservées sur une configuration mise à niveau statique. Le code permettant de les lister et de les lire est toujours présent dans le produit.</td>
   <td>To persist the changes, copy the XML file from <code>/etc</code> to <code>/libs</code> or <code>/conf</code>. Alternatively,<strong> </strong>remove file from <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## Bibliothèques côté client {#client-side-libraries}

[Les bibliothèques](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) côté client sont du code JavaScript et CSS traité dans le navigateur.

### Stratégie d’extensibilité {#extensibility-strategy-1}

AEM fournit une structure d’extensibilité permettant d’ajouter plusieurs fichiers JavaScript. Tout fichier ayant la même propriété « categories » sera ajouté, ce qui permettra au code personnalisé d’étendre le code AEM résidant sous `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>Solution</strong></td>
   <td><strong>Emplacement précédent</strong><br /> </td>
   <td><strong>Nouvel emplacement</strong></td>
   <td><strong>Méthode de compatibilité descendante</strong></td>
   <td><strong>Conditions requises pour s’aligner sur le modèle le plus récent</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>La clientlib héritée sera conservée sur une instance mise à niveau de manière statique.</p> <p>Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <strong><code>replaces</code></strong> », pour éviter d’être fusionnées avec les anciennes clientlibs.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>Clients hérités qui seront conservés sur une instance mise à niveau par le biais d’une mise à niveau statique.</p> <p>Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <strong><code>replaces</code></strong> », pour éviter d’être fusionnées avec les anciennes clientlibs.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>Clientlibs héritées. Elles seront conservées sur une instance mise à niveau de manière statique. Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <strong><code>replaces</code></strong> », pour éviter d’être fusionnées avec les anciennes clientlibs.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>N’est plus proposé dans le cadre du package par défaut d’AEM 6.5.</td>
   <td><p>Thèmes prêts à l’emploi dans des formulaires adaptatifs.</p> <p>Ils seront conservés sur une configuration mise à niveau statique.</p> </td>
   <td>Il s’agit d’un contenu généré en partie par l’utilisateur. Il sera fourni sous la forme d’un module de contenu de référence avec le nom <code>aem-forms-reference-themes</code>.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>Clientlibs héritées. Elles seront conservées sur une instance mise à niveau de manière statique. Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <strong><code>replaces</code></strong> », pour éviter d’être fusionnées avec les anciennes clientlibs.</td>
   <td>Aucune action requise.<p> </p> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>Clientlibs Analytics et Target héritées qui ne sont pas censées être exploitées directement. </td>
   <td>Effacement effectué après la mise à niveau à l’aide d’un filtre de nettoyage.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>Les clientlibs héritées ont des noms de catégorie différents.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>Il s’agit de clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique. Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <code>replaces</code> », pour éviter d’être fusionnées avec les anciennes clientlibs.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>Il s’agit de clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique.</p> <p>Les nouvelles clientlibs ont les mêmes noms de catégorie.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>Il s’agit de clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique.</p> <p>Les nouvelles clientlibs ont les mêmes noms de catégorie.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>Il s’agit de clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique.</p> <p>Les nouvelles clientlibs ont les mêmes noms de catégorie.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>Il s’agit de clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique.</p> <p>Les nouvelles clientlibs ont les mêmes noms de catégorie.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>Les nouvelles clientlibs ont les mêmes noms de catégorie.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>Clientlibs héritées. Elles seront conservées sur une configuration mise à niveau statique. Les nouvelles clientlibs portent les mêmes noms de catégorie, accompagnés de la propriété « <strong>replaces</strong> », pour éviter d’être fusionnées avec les anciennes clientlibs.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>Sur une mise à niveau statique, le fichier hérité (/etc/clientlibs/wcm/…_) n’est pas supprimé automatiquement. Par conséquent, les références au fichier hérité /etc/clientlibs/wcm/foundation/grid/grid_base.less continuent d’être opérationnelles.</p> <p><em>Notez qu’il s’agit d’un cas extrême dans lequel ce fichier LESS est référencé par un chemin d’accès absolu via des instructions LESS @import, et non par la catégorie clientlib.</em></p> <p>Si l’instruction LESS du client qui fait référence à « grid_base.less » pointe vers un fichier inexistant, le mode Mise en page de modèles modifiables échouera et les éventuelles modifications effectuées avec celui-ci seront ignorées (en d’autres termes, tous les composants occuperont toute la largeur de la page).</p> </td>
   <td>Mettez à jour les références dans le code personnalisé (c’est-à-dire dans tous les fichiers LESS faisant référence au fichier grid_base.less déplacé) pour qu’elles pointent vers le nouvel emplacement et supprimez ensuite l’emplacement hérité.</td>
  </tr>
 </tbody>
</table>

Il s’agit là de tâches de restructuration qui ne sont pas couvertes dans les sections précédentes.

### Stratégie d’extensibilité {#extensibility-strategy-2}

Parcourez chaque ligne du tableau ci-dessous pour en savoir plus sur les modèles d’extensibilité pris en charge. En règle générale, le contenu de cette section n’est pas étendu.

## Divers {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>Solution</strong></td>
   <td><strong>Emplacement précédent</strong><br /> </td>
   <td><strong>Nouvel emplacement</strong></td>
   <td><strong>Méthode de compatibilité descendante</strong></td>
   <td><strong>Conditions requises pour s’aligner sur le modèle le plus récent</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>Modèles prêts à l’emploi AEM Forms Portal hérités. Ces modèles restent dans /etc après une configuration mise à niveau statique.</p> <p>In the template listing, the word<em> "deprecated</em>" will be added to the template title to differentiate them with the newer templates.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>Fichiers d’annotation Correspondence Management hérités. Ces fichiers ne sont pas censés être exploités directement. Ils seront effacés après la mise à niveau à l’aide d’un filtre de nettoyage.</td>
   <td>Effacement de l’emplacement hérité après la mise à niveau à l’aide d’un filtre de nettoyage.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>L’API Tag Manager prend en charge l’emplacement hérité et le nouvel emplacement. Lorsque le composant Factory OSGi de JCR Tag démarre, il détecte s’il s’exécute sur une instance mise à niveau ou une instance héritée, et utilise l’emplacement approprié en conséquence.<br /> </td>
   <td><p>Pour vous aligner correctement sur le nouveau modèle, procédez comme suit :</p>
    <ol>
     <li>Remplacez les références à l’ancien modèle (<code>/etc/tags</code>) par le nouveau (<code>/content/cq:tags</code>) à l’aide de la variable <code>tagID.</code></li>
     <li>Connectez-vous à CRXDE Lite.</li>
     <li>Déplacer les balises de <code>/etc/tags</code> vers <code>/content/cq:tags</code></li>
     <li>Redémarrage du composant OSGi <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Emplacement hérité utilisé dans le cadre du traitement des<br /> workflows en transit. Les nouveaux workflows utilisent le nouvel emplacement sous <code>/var.</code></td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>Existing Workflow Model Steps that reference workflow scripts in the legacy location at <code>/etc/workflow/scripts</code> will continue to point to these scripts after the upgrade, and execute properly.</p> <p>Nous attirons votre attention sur le fait que l’interface utilisateur d’AEM destinée à la création des étapes de workflow (Processus, Divisions, etc.) no longer lists scripts under <code>/etc/workflow/scripts</code> in the drop-down used select to workflow scripts.</p> </td>
   <td><p>Les workflows qui exploitent ces scripts continueront de fonctionner comme prévu si l’étape de workflow associée n’est pas modifiée dans AEM.</p> <p>Cependant, pour bénéficier d’une parfaite rétrocompatibilité, y compris lors de la modification des étapes, une intervention manuelle de l’utilisateur sera nécessaire après la mise à niveau :</p>
    <ul>
     <li>The scripts must be moved from <code>/etc/workflow/scripts</code> to <code>/apps/workflow/scripts.</code></li>
     <li>Any<strong> </strong>references to <code>/etc/workflow/scripts</code> in workflow model steps must be updated to reference the new <code>/apps/workflow/scripts</code> location.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>La page de l’utilitaire Interface utilisateur classique reste au même endroit lors de la mise à niveau.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>Emplacement de stockage temporaire des fichiers ZIP générés pour l’appel de l’opération de téléchargement d’AEM Assets.</p> <p>Aucune mise à jour n’est nécessaire puisque, lorsque le client demande de télécharger la ressource, le fichier est généré dans le nouvel emplacement.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>L’ancien contenu n’est pas transféré et reste utilisable après la mise à niveau.</p> <p>Une tâche de migration différée est fournie pour effectuer la migration vers le nouvel emplacement.</p> </td>
   <td><p>La migration est effectuée par le biais d’une tâche de migration différée : <code>CQ64CommerceMigrationTask.</code></p> <p>La procédure se compose des étapes suivantes :</p>
    <ul>
     <li>Adaptation des références pour qu’elles pointent vers le nouvel emplacement</li>
     <li>Transfert du contenu de l’ancien emplacement vers le nouvel emplacement</li>
     <li><p>Suppression de l’ancien emplacement en vue d’activer l’utilisation du nouvel emplacement à l’échelle du système</p> </li>
    </ul> <p>Les emplacements couverts par la tâche sont les suivants :</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Pour les catalogues plus volumineux, il est conseillé d’exécuter la tâche de migration de commerce en transmettant la propriété du système Java suivante à AEM :</p>
    <ul>
     <li>nom de propriété: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>valeur de propriété: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>Après la migration, AEM doit être redémarré.</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>L’ancien contenu n’est pas transféré et reste utilisable après la mise à niveau.</p> <p>Une tâche de migration différée est fournie pour effectuer la migration vers le nouvel emplacement.</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>L’ancien contenu n’est pas transféré et reste utilisable après la mise à niveau.</p> <p>Une tâche de migration différée est fournie pour effectuer la migration vers le nouvel emplacement.</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>Aucune action requise.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>L’ancien contenu n’est pas transféré et reste utilisable après la mise à niveau.</p> <p>Une tâche de migration différée est fournie pour effectuer la migration vers le nouvel emplacement.</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>L’ancien contenu n’est pas transféré et reste utilisable après la mise à niveau.</p> <p>Une tâche de migration différée est fournie pour effectuer la migration vers le nouvel emplacement.</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>De nouvelles tâches sont créées sous <code>/var/taskmanagement</code></p> <p>Les tâches qui sont présentes à l’emplacement hérité restent visibles dans la boîte de réception AEM.</p> </td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>Les packages AEM créés via AEM Package Manager sont toujours stockés dans <code>/etc/workflow/packages.</code></p> <p>Les autres packages créés via les sites et processus AEM continuent à être stockés dans<code>/var/workflow/packages.</code></p> <p>Packages found in both <code>/etc/workflow/packages</code> and <code>/var/workflow/packages</code> can still be edited via AEM's Package Manager. </p> </td>
   <td><p>Aucune action requise.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>New workflow instances will be created under <code>/var</code> automatically.</td>
   <td>Aucune action requise.</td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Nouvel emplacement pour le contenu de flux Search &amp; Promote.</p> <p>L’ancienne URL fonctionne toujours et la requête est transmise au nouvel emplacement par un ServletFilter.</p> </td>
   <td>Aucune action requise.<br /> <br /> </td>
  </tr>
  <tr>
   <td>Tous</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>Nouvel emplacement pour DTM Web-Hooks.</p> <p>L’ancienne URL fonctionne toujours et la requête est transmise au nouvel emplacement par un ServletFilter.</p> </td>
   <td>Aucune action requise.<br /> <br /> </td>
  </tr>
 </tbody>
</table>

