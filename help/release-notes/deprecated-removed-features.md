---
title: Fonctionnalités obsolètes et supprimées
description: Notes de mise à jour dédiées aux fonctionnalités obsolètes et supprimées dans Adobe Experience Manager 6.5.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 33fab976729baa09fdfd3725542f9e6bc7f37eeb

---


# Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe étudie constamment les fonctionnalités du produit de façon à les réinventer au fil du temps ou à remplacer les fonctions plus anciennes par des variantes plus modernes, pour améliorer la valeur client globale, le tout en faisant toujours attention à la compatibilité ascendante.

Pour communiquer la suppression/le remplacement imminent de fonctionnalités d’AEM, les règles suivantes s’appliquent :

1. L’annonce de la suppression arrive en premier. Bien qu&#39;abandonnées, les capacités sont toujours disponibles, mais elles ne seront pas améliorées.
1. La suppression des fonctionnalités obsolètes se produit au plus tôt dans la version majeure suivante. La date de suppression sera annoncée.

Ce processus donne aux clients au moins un cycle de version afin d’adapter leur implémentation à une nouvelle version ou produit de remplacement d’une fonctionnalité obsolète, avant que la suppression ne soit effective.

## Fonctionnalités obsolètes {#deprecated-features}

Cette section répertorie les fonctionnalités qui ont été signalées comme étant obsolètes dans AEM 6.5. En général, les fonctionnalités qui seront supprimées dans une prochaine version sont d’abord annoncées comme obsolètes, et une solution de remplacement est fourni.

Il est conseillé aux clients de réfléchir à leur utilisation de la fonctionnalité dans leur déploiement actuel et de prévoir la modification de leur mise en œuvre de façon à utiliser l’alternative proposée.

<table>
 <tbody>
  <tr>
   <td><b>Zone</b></td>
   <td><b>Fonctionnalité</b></td>
   <td><b>Remplacement</b></td>
  </tr>
  <tr>
   <td>Intégration de Creative Cloud</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">Le partage</a> de dossiers AEM vers Creative Cloud a été introduit dans AEM 6.2 pour permettre aux utilisateurs créatifs d’accéder aux ressources d’AEM, de sorte qu’ils puissent les ouvrir dans les applications CC et télécharger de nouveaux fichiers ou enregistrer des modifications dans AEM. Adobe Asset Link, nouvelle fonctionnalité proposée dans l’application Creative Cloud, offre une expérience utilisateur améliorée et un accès plus puissant aux ressources d’AEM directement à partir de Photoshop, InDesign et Illustrator.</p> <p>Adobe n’envisage pas d’apporter d’autres améliorations à l’intégration du partage de dossiers d’AEM à Creative Cloud. Bien que cette fonctionnalité soit incluse dans AEM, il est vivement conseillé aux clients d’utiliser des solutions de remplacement.</p> </td>
   <td>Il est conseillé aux clients de passer aux nouvelles fonctionnalités d’intégration de Creative Cloud, notamment Adobe Asset Link ou l’application de bureau AEM. Review <a href="/help/assets/aem-cc-integration-best-practices.md">AEM and Creative Cloud Integration Best Practices</a> for more details.</td>
  </tr>
  <tr>
   <td>Ressources</td>
   <td>
    <ol>
     <li>AssetDownloadServlet est désactivé par défaut pour les instances de publication. Pour plus de détails, voir la <a href="/help/sites-administering/security-checklist.md">Liste de contrôle de sécurité AEM</a>.</li>
     <li>Si un utilisateur n’a pas les autorisations suffisantes (en lecture et écriture) sur /content/dam/collections, il ne peut pas créer de collection.</li>
    </ol> </td>
   <td>
    <ol>
     <li>Configuration décrite dans la <a href="/help/sites-administering/security-checklist.md">Liste de contrôle de sécurité AEM</a>.</li>
     <li>Respectez la configuration du contrôle d’accès de l’utilisateur et assurez-vous que les autorisations sont appropriées.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>L’intégration à Adobe Search &amp; Promote est obsolète.</p> <p>Adobe ne prévoit pas d’apporter d’autres améliorations à l’intégration Search &amp; Promote. Notez que l’intégration Search &amp; Promote reste entièrement prise en charge tout en étant obsolète.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM Tag Manager</td>
   <td>L’intégration avec DTM (Dynamic Tag Manager) est obsolète.</td>
   <td>Passez à Adobe Experience Platform Launch en tant que gestionnaire de balises</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Lorsque vous ajoutez la possibilité pour AEM de se connecter au service Adobe Target à l’aide de l’API Standard d’Adobe Target basée sur Adobe I/O (API Rest) dans AEM 6.5, la méthode utilisant l’API Target Classic (XML) est obsolète.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">Reconfigurez l’intégration pour utiliser la nouvelle API.</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>L’utilisation de l’intégration basée sur mbox.js avec Adobe Target dans AEM est obsolète.</td>
   <td>Passez à at.js 1.x.</td>
  </tr>
  <tr>
   <td>Commerce</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> a été fourni en 2018 sous la forme d’un ensemble de microservices permettant l’intégration entre AEM et les moteurs de commerce.</p> <p>Après l’acquisition de Magento par Adobe à la mi-2018, Adobe a décidé de modifier son approche pour deux raisons : </p> <p><strong>1.</strong> Magento possède son propre jeu d’API de commerce (REST et GraphQL) et il n’est pas recommandé de gérer deux jeux d’API. </p> <p><strong>2.</strong> Les tendances du marché ont indiqué que les clients se dirigeaient vers GraphQL, parce que c'est une façon plus efficace d'interroger des données. En 2019, Adobe a publié la nouvelle structure d’intégration commerciale en utilisant les API GraphQL de Magento comme source de vérité.</p> <p>Adobe n’envisage pas d’investir davantage dans CIF REST. Il est vivement conseillé aux clients d’utiliser la solution de remplacement.</p> </td>
   <td><p>Pour les intégrations AEM-Magento, passez à l’archétype <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">CIF</a>AEM et aux composants principaux <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF.</a></p> <p>Pour plus d’informations, consultez Intégration <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEM et Magento à l’aide de Commerce Integration Framework</a> .</p> <p>Le soutien aux intégrations tierces (autres que Magento) avec la nouvelle approche est sur notre feuille de route.</p> </td>
  </tr>
  <tr>
   <td>Composants (AEM Sites)</td>
   <td><p>Adobe ne prévoit pas d’apporter d’autres améliorations à la plupart des composants de base (Foundation) stockés dans /libs/foundation/components.</p> <p>Recherchez les propriétés <strong>cq:deprecated</strong> et <strong>cq:deprecatedReason</strong> dans le dossier des composants.</p> <p>AEM 6.5 inclut les composants Foundation, et les clients qui effectuent une mise à niveau depuis des versions antérieures peuvent continuer à les utiliser en l’état. En outre, les éléments de base restent entièrement pris en charge tout en étant abandonnés. </p> </td>
   <td>Adobe recommande aux clients d’utiliser les composants principaux pour les prochains projets. Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>Composants (AEM Sites)</td>
   <td>Les composants de l’importateur de conception /libs/wcm/designimporter/components ont été marqués comme obsolètes depuis la version 6.5. Adobe ne prévoit pas d’apporter d’autres améliorations à cette implémentation de l’importateur de conception.</td>
   <td>Adobe prévoit de fournir une autre implémentation du cas d’utilisation dans les prochaines versions.</td>
  </tr>
  <tr>
   <td>Composants (AEM Forms)</td>
   <td><p>L’étape Signature permet aux utilisateurs de vérifier et de signer un formulaire adaptatif. Dans les versions précédentes, l’étape de signature pouvait utiliser les composants Adobe Sign et Scribble Signature comme champs de signature. Dans AEM Forms 6.5, l’expérience de signature tactile de l’étape de signature est obsolète.</p> </td>
   <td>
    <ul>
     <li>Si vous avez effectué une nouvelle installation :
      <ul>
       <li>Utilisez l’expérience de signature basée sur Adobe Sign dans une étape Signature d’un formulaire adaptatif.</li>
       <li>Utilisez le composant Scribble Signature autonome dans un formulaire adaptatif, une communication interactive et des formulaires HTML5.</li>
      </ul> </li>
     <li>Si vous avez effectué la mise à niveau d’une version précédente vers AEM Forms 6.5 :<br />
      <ul>
       <li>Continuez à utiliser l’expérience de signature tactile de l’étape de signature avec les formulaires qui utilisent déjà cette fonctionnalité.<br /> </li>
       <li>Utilisez le composant Scribble Signature autonome ou l’expérience de signature basée sur Adobe Sign au sein d’une étape Signature lorsque vous créez un formulaire. </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Structure de déchargement Granite</p> <p>Adobe n’envisage pas d’apporter d’autres améliorations à la structure de déchargement ajoutée à la version 5.6.1 pour externaliser le traitement des ressources. </p> </td>
   <td>Adobe travaille sur une structure de déchargement native pour le cloud de nouvelle génération.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Hobbes.js</p> <p>Adobe ne prévoit pas d’apporter d’autres améliorations à la structure de test de l’interface utilisateur de hobbes.js.</p> </td>
   <td>Adobe recommande aux clients d’utiliser l’automatisation du sélénium.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Bibliothèque cliente de l’interface utilisateur jQuery</p> <p>Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente de l’interface utilisateur qui est fournie dans le cadre de la distribution (Quickstart)</p> </td>
   <td>Adobe recommande aux clients qui ont encore besoin de l’interface utilisateur jQuery pour leur code de l’ajouter à leur base de code de projet.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Bibliothèque cliente jQuery Animation (granite.jquery.animation)</p> <p>Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente jQuery Animation fournie avec la distribution (Quickstart).</p> </td>
   <td>Adobe recommande aux clients qui ont encore besoin d’animations jQuery pour leur code de l’ajouter à leur base de code de projet.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Bibliothèque cliente Handlebars</p> <p>Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Handlebar fournie avec la distribution (Quickstart).</p> </td>
   <td>Adobe recommande aux clients qui ont encore besoin de barres de poignées pour leur code de l’ajouter dans leur base de code de projet.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Bibliothèque cliente Lawnchair</p> <p>Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Lawnchair fournie avec la distribution (Quickstart).</p> </td>
   <td>Adobe recommande aux clients qui ont encore besoin de Lawnchair pour leur code de l’ajouter dans leur base de code de projet.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Bibliothèque cliente Granite.Sling.js</p> <p>Adobe ne prévoit pas d’améliorer la bibliothèque cliente Granite.Sling.js fournie avec la distribution (Quickstart).</p> </td>
   <td>Adobe recommande aux clients qui comptent sur la capacité de la bibliothèque de reformater leur code pour ne plus l’utiliser.</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td>Utilisation de YUI pour compresser/réduire les bibliothèques clientes JavaScript. Adobe ne prévoit pas de mettre à jour la bibliothèque YUI. Jusqu’à AEM 6.4, l’interface utilisateur YUI était par défaut en mesure de réduire JavaScript avec l’option permettant de passer au compilateur de fermeture Google (GCC). À partir d’AEM 6.5, GCC est l’option par défaut.</td>
   <td>Adobe recommande aux clients effectuant la mise à niveau vers AEM 6.5 de passer à GCC pour leur implémentation</td>
  </tr>
  <tr>
   <td>Développeurs</td>
   <td><p>Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite</p> <p>Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart).</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Forms</td>
   <td><p>Intégration d'AEM Forms avec AEM Mobile&lt; est obsolète </p> </td>
   <td>Aucun remplacement. </td>
  </tr>
 </tbody>
</table>

## Fonctionnalités supprimées {#removed-features}

Cette section les fonctionnalités et fonctionnalités qui ont été supprimées d’AEM 6.5. Les versions précédentes présentaient ces fonctionnalités comme obsolètes.

| Zone | Fonctionnalité | Remplacement |
|--- |--- |--- |
| Carte des  Analytics  | Version du  de mappage de  incluse dans AEM. | En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM. Utilisez le module externe [ActivityMap fourni par Adobe Analytics](https://docs.adobe.complugin /content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Intégrations | L’intégration ExactTarget a été supprimée de la distribution par défaut (Quickstart) et n’est plus disponible. | Aucun remplacement. |
| Intégrations | L’intégration de l’API Salesforce Force a été supprimée de la distribution par défaut (Quickstart) et constitue désormais un package supplémentaire à installer à partir de PackageShare. | La fonctionnalité est toujours disponible. |
| Forms | La prise en charge du service de passerelle d’Adobe Central Migration n’est plus assurée, car le produit Adobe Central n’est plus pris en charge. | Aucun remplacement. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Aucun remplacement. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Aucun remplacement. |
| Forms | La mise à niveau à sauce unique de LiveCycle ES4 SP1 vers AEM Forms 6.5 sur JEE n’est pas disponible | Reportez-vous à la page Chemins [de mise à niveau](../forms/using/upgrade.md) disponibles dans la documentation de mise à niveau d’AEM Forms. |
| Forms | Suppression de la prise en charge de la mise en grappe basée sur UPD d’AEM Forms sur JEE | Vous pouvez uniquement utiliser la mise en grappe basée sur TCP dans AEM Forms sur JEE. Si vous mettez à niveau un serveur de multidiffusion UDP d’une version précédente vers AEM Forms 5.5 sur JEE, effectuez des configurations manuelles pour passer à la mise en grappe de jeux basée sur TCP. Pour obtenir des instructions détaillées, voir [Mise à niveau vers AEM Forms 6.5 sur JEE](../forms/using/upgrade-forms-jee.md) |
| Développeurs | Firebug Lite a été supprimé de la distribution par défaut (Quickstart). | Utilisez les consoles de développement intégrées au navigateur. |
| Développeurs | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Aucun remplacement. |
| Ressources | La fonction de déchargement Ressources a été supprimée d’AEM 6.5. | Aucun remplacement. |
| Cache | `system/console/slingjsp` n’est plus disponible dans AEM 6.5. | Classes et cache Légèrement sont stockés sous le lot Apache Sling Commons FileSystem ClassLoader. Vous pouvez vérifier le numéro de lot dans la console Web AEM et supprimer le dossier de cache directement du système de fichiers (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Annonce préalable à la prochaine version {#pre-announcement-for-next-release}

Cette section vise à annoncer les modifications à venir dans la prochaine version, qui ne sont pas obsolètes, mais qui auront une incidence sur les clients. Elles sont fournies à des fins de planification.

| Zone | Fonctionnalité | Annonce |
|--- |--- |--- |
| Foundation | Structure de l’interface utilisateur | Adobe prévoit de rendre obsolète les composants de l’interface utilisateur Coral 2 en 2019. L’interface utilisateur Coral 3 a été introduite avec AEM 6.2, et AEM 6.5 est entièrement basé sur Coral 3. Adobe recommande à ses clients et partenaires qui ont créé des interfaces utilisateur personnalisées avec Coral 2 de les restructurer avec Coral 3. Adobe fournit un outil permettant de convertir les boîtes de dialogue Coral 2 en Coral 3 - [En savoir plus](/help/sites-developing/dialog-conversion.md). |
