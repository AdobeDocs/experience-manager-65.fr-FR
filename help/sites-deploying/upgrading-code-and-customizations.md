---
title: Mettre à jour le code et les personnalisations
seo-title: Upgrading Code and Customizations
description: Découvrez la mise à niveau du code personnalisé dans AEM.
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: ht
source-wordcount: '2115'
ht-degree: 100%

---

# Mettre à jour le code et les personnalisations{#upgrading-code-and-customizations}

Lors de la planification d’une mise à niveau, les aspects suivants d’une mise en œuvre doivent être étudiés et abordés.

* [Mise à niveau de la base de code](#upgrade-code-base)
* [Alignement avec la structure de référentiel de la version 6.5](#align-repository-structure)
* [Personnalisations d’AEM](#aem-customizations)
* [Procédure de test](#testing-procedure)

## Présentation {#overview}

1. **Détecteur de motifs** : exécutez le détecteur de motifs comme décrit dans la planification de la mise à niveau et présenté en détail dans [cette page](/help/sites-deploying/pattern-detector.md). Vous obtenez un rapport du détecteur de motifs qui contient plus de détails sur les zones à traiter en plus des API/lots indisponibles dans la version cible d’AEM. Le rapport du détecteur de motifs vous donne une indication des incompatibilités éventuelles de votre code. S’il n’y a aucune incompatibilité, votre déploiement est déjà compatible avec la version 6.5. Vous pouvez toujours choisir d’effectuer un nouveau développement pour utiliser la fonctionnalité 6.5, mais vous n’en avez pas besoin pour conserver la compatibilité. Si des incompatibilités sont signalées, vous pouvez choisir d’effectuer une exécution en mode de compatibilité et de différer le développement pour les nouvelles fonctionnalités de la version 6.5 ou pour la compatibilité. Vous pouvez également décider de procéder au développement après la mise à niveau, puis passer à l’étape 2. Pour en savoir plus, consultez la [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md).

1. **Développement de la base de code pour la version 6.5**- Créez une branche ou un référentiel dédié à la base de code pour la version cible. Utilisez les informations de la compatibilité avant la mise à niveau pour prévoir les zones de code à mettre à jour.
1. **Compilation avec 6.5 Uber jar** : mettez à jour les POM de la base de code pour pointer vers 6.5 Uber jar et compilez le code par rapport à cette opération.
1. **Mise à jour de la personnalisation d’AEM***- *Toutes les personnalisations ou les extensions dans AEM doivent être mises à jour/validées pour fonctionner dans la version 6.5 et être ajoutées à la base de code 6.5. Comprend des formulaires de recherche d’interface utilisateur, des personnalisations de ressources, tout élément utilisant /mnt/overlay.

1. **Déploiement vers l’environnement 6.5** - Une instance AEM 6.5 nette (auteur + publication) doit être conservée dans un environnement Dev/QA. La base de code à jour et un échantillon représentatif de contenu (de l’exploitation actuelle) doivent être déployés.
1. **Validation du contrôle qualité et correction des bogues** - Le contrôle qualité doit valider l’application sur les instances d’auteur et de publication de la version 6.5. Tous les problèmes détectés doivent être corrigés et intégrés dans la base de code 6.5. Répétez le cycle de développement jusqu’à ce que tous les bugs soient corrigés.

Avant de procéder à une mise à niveau, vous devez disposer d’une base de code d’application stable qui a été soigneusement testée par rapport à la version cible d’AEM. En fonction des observations effectuées dans les tests, il peut être possible d’optimiser le code personnalisé. Par exemple, il peut être possible de refactoriser le code pour éviter de parcourir le référentiel, d’indexer de manière personnalisée pour optimiser la recherche ou d’utiliser ded noeuds non ordonnés dans JCR, entre autres.

Outre la mise à niveau facultative de votre base de code et de vos personnalisations pour qu’elles fonctionnent avec la nouvelle version d’AEM, la version 6.5 permet de gérer plus efficacement vos personnalisations à l’aide de la fonctionnalité de compatibilité descendante, comme décrit dans [cette page](/help/sites-deploying/backward-compatibility.md).

Comme mentionné ci-dessus et illustré dans le diagramme ci-dessous, en exécutant le [Détecteur de motifs](/help/sites-deploying/pattern-detector.md) dans la première étape, vous pouvez évaluer la complexité globale de la mise à niveau. Il peut également vous aider à décider si vous souhaitez exécuter le mode de compatibilité ou mettre à jour vos personnalisations pour utiliser toutes les nouvelles fonctionnalités d’AEM 6.5. Pour en savoir plus, consultez la page [Compatibilité descendante dans AEM 6.5.](/help/sites-deploying/backward-compatibility.md)
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Mise à niveau de la base de code {#upgrade-code-base}

### Création d’une branche spécifique pour la version 6.5 du code dans le contrôle de version  {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Tout le code et toutes les configurations nécessaires pour votre mise en oeuvre d’AEM doivent être gérés à l’aide d’une forme de gestion de versions. Une branche dédiée à la gestion de versions doit être créée pour gérer les modifications nécessaires pour la base de code dans la version cible d’AEM. Les tests itératifs de la base de code par rapport à la version cible d’AEM et les correctifs de bugs ultérieurs sont gérés dans cette branche.

### Mise à jour de la version AEM Uber Jar {#update-the-aem-uber-jar-version}

AEM Uber jar inclut toutes les API d’AEM en tant que dépendance unique dans le fichier `pom.xml` de votre projet Maven. Il est toujours recommandé d’inclure Uber Jar en tant que dépendance unique au lieu d’inclure les dépendances d’API d’AEM individuelles. Lors de la mise à niveau de la base de code, modifiez la version du fichier Uber Jar pour qu’elle pointe vers la version cible d’AEM. Si votre projet a été développé sur une version d’AEM antérieure à l’existence d’Uber Jar, supprimez toutes les dépendances d’API d’AEM individuelles. Remplacez-les par une seule inclusion du fichier Uber Jar pour la version cible d’AEM. Recompilez la base de code par rapport à la nouvelle version du fichier Uber Jar. Mettez à jour les API ou méthodes obsolètes afin qu’elles soient compatibles avec la version cible d’AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Suppression progressive de l’utilisation du résolveur de ressources d’administration {#phase-out-use-of-administrative-resource-resolver}

L’utilisation d’une session d’administration via `SlingRepository.loginAdministrative()` et `ResourceResolverFactory.getAdministrativeResourceResolver()` était très courante dans les bases de code avant AEM 6.0. Ces méthodes sont désormais déconseillées pour des raisons de sécurité, car elles offrent un niveau d’accès trop large. [Ces méthodes seront supprimées des prochaines versions de Sling.](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Il est vivement recommandé de refactoriser tout code pour utiliser les utilisateurs et utilisatrices du service à la place. Vous trouverez ici des informations supplémentaires sur les utilisateurs et utilisatrices de service et sur la manière de [supprimer progressivement les sessions d’administration](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Requêtes et index Oak {#queries-and-oak-indexes}

Toute utilisation de requêtes dans la base de code doit être minutieusement testée dans le cadre de la mise à niveau de la base de code. Pour les clients effectuant une mise à niveau à partir de Jackrabbit 2 (versions d’AEM antérieures à la version 6.0), ce test est particulièrement important, car Oak n’indexe pas le contenu automatiquement et vous devez créer des index personnalisés. Si vous effectuez une mise à niveau à partir d’une version 6.x d’AEM, les définitions d’index Oak prêtes à l’emploi peuvent avoir changé et peuvent avoir un impact sur les requêtes existantes.

Les outils suivants sont disponibles pour l’analyse et l’inspection des performances des requêtes :

* [Outils d’index AEM](/help/sites-deploying/queries-and-indexing.md)

* [Outils de diagnostic des opérations - Performance des requêtes](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Création dans l’interface utilisateur classique {#classic-ui-authoring}

La création de l’IU classique est toujours disponible dans AEM 6.5, mais elle sera bientôt obsolète. Vous trouverez plus d’informations[ ici](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Si votre application s’exécute dans l’environnement de création de l’interface utilisateur classique, il est recommandé de passer à AEM 6.5 et de continuer à utiliser l’interface utilisateur classique. La migration vers l’interface utilisateur optimisée pour les écrans tactiles peut ensuite être prévue en tant que projet distinct à effectuer sur plusieurs cycles de développement. Pour utiliser l’interface utilisateur classique dans AEM 6.5, plusieurs configurations OSGi doivent être intégrées à la base de code. Pour plus d’informations sur la configuration, cliquez [ici](/help/sites-administering/enable-classic-ui.md).

## Alignement avec la structure de référentiel de la version 6.5 {#align-repository-structure}

Pour faciliter les mises à niveau et s’assurer que les configurations ne soient pas remplacées au cours de celles-ci, le référentiel est restructuré dans la version 6.4 afin de séparer le contenu de la configuration.

Plusieurs paramètres doivent donc être déplacés afin de ne plus résider sous `/etc`, comme c’était auparavant le cas. Pour consulter l’ensemble des problèmes de restructuration de référentiel qui doivent être étudiés et résolus dans la mise à jour d’AEM 6.4, voir [Restructuration de référentiel dans AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personnalisations d’AEM  {#aem-customizations}

Toutes les personnalisations de l’environnement de création AEM dans la version source d’AEM doivent être identifiées. Une fois identifiées, il est recommandé de stocker chaque personnalisation dans la gestion de versions ou, au minimum, de les sauvegarder dans un package de contenu. Toutes les personnalisations doivent être déployées et validées dans le cadre d’un contrôle qualité ou un environnement d’évaluation exécutant la version cible d’AEM avant une mise à niveau d’exploitation.

### Recouvrements en général {#overlays-in-general}

Il est courant d’étendre les fonctionnalités d’AEM prêtes à l’emploi en recouvrant des nœuds et/ou des fichiers sous /libs avec des nœuds supplémentaires sous /apps. Ces recouvrements doivent faire l’objet d’un suivi dans le cadre de la gestion de versions et d’un test par rapport à la version cible d’AEM. Si un fichier (JS, JSP, HTL, par exemple) est superposé, Adobe vous recommande de laisser un commentaire sur les fonctionnalités qui ont été améliorées pour simplifier les tests de régression sur la version cible d’AEM. Vous trouverez plus d’informations sur les recouvrements en général [ici](/help/sites-developing/overlays.md). Vous trouverez ci-dessous des instructions relatives à des recouvrements d’AEM spécifiques.

### Mettre à niveau les formulaires de recherche personnalisés {#upgrading-custom-search-forms}

Les facettes de recherche personnalisées nécessitent quelques ajustements manuels après la mise à niveau pour fonctionner correctement. Pour en savoir plus, consultez la section [Mise à niveau des formulaires de recherche personnalisée](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personnalisations de l’interface utilisateur Assets {#assets-ui-customizations}

>[!NOTE]
>
>Cette procédure n’est requise que pour les mises à niveau à partir de versions antérieures à AEM 6.2.

Les instances qui ont des déploiements d’Assets personnalisés doivent être préparées pour la mise à niveau. Cette action est nécessaire pour s’assurer que tout le contenu personnalisé est compatible avec la nouvelle structure de nœuds de la version 6.4.

Vous pouvez préparer les personnalisations de l’interface utilisateur d’Assets en procédant comme suit :

1. Sur l’instance qui doit être mise à niveau, ouvrez CRXDE Lite en accédant à *https://server:port/crx/de/index.jsp*.

1. Accédez au nœud suivant :

   * `/apps/dam/content`

1. Renommez le nœud de contenu **content_backup** en cliquant avec le bouton droit sur le volet de l’explorateur dans la partie gauche de la fenêtre, et en choisissant **Renommer**.

1. Une fois que le nœud a été renommé, créez un nœud de contenu sous `/apps/dam` nommé **content** et définissez son type de nœud sur **sling:Folder**.

1. Déplacez tous les nœuds enfants de **content_backup** vers le nœud de contenu que vous venez de créer en cliquant avec le bouton droit sur chaque nœud enfant dans le volet de l’explorateur et en sélectionnant **Déplacer**.

1. Supprimez le nœud **content_backup**.

1. Les nœuds mis à jour sous `/apps/dam` avec le type de nœud correct `sling:Folder` doivent idéalement être enregistrés dans le contrôle de version et déployés avec la base de code ou au moins être sauvegardés en tant que packages de contenu.

### Génération d’identifiants pour les ressources existantes {#generating-asset-ids-for-existing-assets}

Pour générer des identifiants pour les ressources existantes, mettez à niveau les ressources en même temps que l’instance AEM pour exécuter la version 6.5d’AEM. Cela requiert l’activation de la [fonctionnalité Assets Insights](/help/assets/asset-insights.md). Pour plus de détails, consultez la section [Ajout d’un code intégré](/help/assets/use-page-tracker.md#add-embed-code).

Pour mettre à niveau les ressources, configurez le package d’identifiants de ressources associé dans la console JMX. En fonction du nombre de ressources dans le référentiel, `migrateAllAssets` peut prendre beaucoup de temps. Selon les tests internes d’Adobe, cela peut prendre environ une heure pour 125 000 ressources sur TarMK.

![1487758945977](assets/1487758945977.png)

Si vous avez besoin de plusieurs identifiants de ressources pour un sous-ensemble de vos ressources totales, utilisez l’API `migrateAssetsAtPath`.

Pour tout autre objectif, utilisez l’API `migrateAllAssets()`

### Personnalisations de script InDesign {#indesign-script-customizations}

Adobe recommande de placer les scripts personnalisés à l’emplacement `/apps/settings/dam/indesign/scripts`. Vous trouverez plus d’informations sur les personnalisations des scripts d’InDesign [ici](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Récupérer des configurations ContextHub {#recovering-contexthub-configurations}

Les configurations ContextHub sont affectées par la mise à niveau. Des instructions sur la façon de récupérer les configurations ContextHub existantes sont disponibles [ici](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personnalisations des workflows {#workflow-customizations}

Il est courant de modifier les workflows prêts à l’emploi pour ajouter ou supprimer des fonctionnalités inutiles. Un workflow qui est souvent personnalisé est le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]. Tous les workflows nécessitant une implémentation personnalisée doivent être enregistrés et stockés dans le contrôle de version, car ils risquent d’être remplacés lors de la mise à niveau.

### Modèles modifiables {#editable-templates}

>[!NOTE]
>
>Cette procédure est requise uniquement pour les mises à niveau de Sites à l’aide de modèles modifiables à partir d’AEM 6.2.

La structure des modèles modifiables a changé entre AEM 6.2 et 6.3. Si vous effectuez une mise à niveau à partir de la version 6.2 ou antérieure et si le contenu de votre site est créé à l’aide de modèles modifiables, vous devez utiliser l’[Outil de nettoyage des noeuds réactifs](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). L’outil est destiné à être exécuté **après** une mise à niveau pour nettoyer le contenu. Exécutez-le sur les niveaux de création et de publication.

### Modifications de l’implémentation des groupes d’utilisateurs fermés {#cug-implementation-changes}

L’implémentation des groupes d’utilisateurs fermés a considérablement changé pour répondre aux limites de performances et d’évolutivité des versions précédentes d’AEM. La version précédente des groupes d’utilisateurs fermés a été abandonnée dans la version 6.3 et la nouvelle implémentation n’est prise en charge que dans l’interface utilisateur tactile. Si vous effectuez une mise à niveau à partir de la version 6.2 ou antérieure, vous trouverez les instructions de migration vers la nouvelle implémentation [ici](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procédure de test {#testing-procedure}

Un plan de test complet doit être préparé pour tester les mises à niveau. Le test de la base de code et de l’application mises à niveau doit d’abord être effectué dans les environnements inférieurs. Tous les bugs détectés doivent être corrigés itérativement jusqu’à ce que la base de code soit stable, après quoi les environnements de niveau supérieur doivent être mis à niveau.

### Test de la procédure de mise à niveau {#testing-the-upgrade-procedure}

La procédure de mise à niveau décrite ici doit être testée sur les environnements de développement et d’assurance qualité, comme indiqué dans votre runbook personnalisé (voir [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md)). La procédure de mise à niveau doit être répétée jusqu’à ce que toutes les étapes soient documentées dans le runbook de mise à niveau et que le processus de mise à niveau soit fluide.

### Zones de test de l’implémentation  {#implementation-test-areas-}

Vous trouverez ci-dessous les zones critiques de toute implémentation d’AEM qui doivent être couvertes par votre plan de test une fois l’environnement mis à niveau et la base de code mise à niveau déployée.

<table>
 <tbody>
  <tr>
   <td><strong>Zone de test fonctionnelle</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Sites publiés</td>
   <td>Test de l’implémentation d’AEM et du code associé au niveau de la publication<br /> par le biais du Dispatcher. Le test doit inclure des critères pour les mises à jour de page et<br /> l’invalidation du cache.</td>
  </tr>
  <tr>
   <td>Création</td>
   <td>Test de l’implémentation d’AEM et du code associé au niveau de création. Ce test doit inclure la page, la création de composants et les boîtes de dialogue.</td>
  </tr>
  <tr>
   <td>Intégrations aux solutions Experience Cloud</td>
   <td>Validation des intégrations avec des produits tels qu’Analytics, DTM et Target.</td>
  </tr>
  <tr>
   <td>Intégrations à des systèmes tiers</td>
   <td>Validez toutes les intégrations tierces sur les niveaux de création et de publication.</td>
  </tr>
  <tr>
   <td>Authentification, sécurité et autorisations</td>
   <td>Tous les mécanismes d’authentification tels que LDAP/SAML doivent être validés.<br /> Les autorisations et les groupes doivent être testés sur les niveaux de création et de publication.<br />.</td>
  </tr>
  <tr>
   <td>Requêtes</td>
   <td>Les index et requêtes personnalisés doivent être testés avec les performances des requêtes.</td>
  </tr>
  <tr>
   <td>Personnalisations de l’interface utilisateur</td>
   <td>Toutes les extensions ou personnalisations de l’interface utilisateur d’AEM dans l’environnement de création.</td>
  </tr>
  <tr>
   <td>Workflows</td>
   <td>Workflow et fonctionnalités personnalisés ou prêts à l’emploi.</td>
  </tr>
  <tr>
   <td>Test de performance</td>
   <td>Les tests de chargement doivent être effectués sur les niveaux de création et de publication qui simulent des scénarios en situation réelle.</td>
  </tr>
 </tbody>
</table>

### Documentation du plan de test et des résultats {#document-test-plan-and-results}

Vous devez créer un plan de tests qui couvre les zones de tests d’implémentation décrites ci-dessus. Souvent, il est logique de séparer le plan de test par les listes de tâches de création et de publication. Ce plan de test doit être exécuté sur les environnements de développement, d’assurance qualité et d’évaluation avant la mise à niveau des environnements de production. Les résultats de test et les mesures de performances doivent être enregistrés dans des environnements inférieurs afin de fournir une comparaison lors de la mise à niveau des environnements d’évaluation et de production.
