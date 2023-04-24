---
title: Mettre à jour le code et les personnalisations
seo-title: Upgrading Code and Customizations
description: En savoir plus sur la mise à niveau du code personnalisé dans AEM.
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
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 21%

---

# Mettre à jour le code et les personnalisations{#upgrading-code-and-customizations}

Lors de la planification d’une mise à niveau, les aspects suivants d’une mise en oeuvre doivent être étudiés et abordés.

* [Mise à niveau de la base de code](#upgrade-code-base)
* [Alignement avec la structure de référentiel de la version 6.5](#align-repository-structure)
* [Personnalisations d’AEM](#aem-customizations)
* [Procédure de test](#testing-procedure)

## Présentation {#overview}

1. **Outil de détection des motifs** - Exécutez le détecteur de motifs comme décrit dans la planification de la mise à niveau et décrit en détail [cette page](/help/sites-deploying/pattern-detector.md). Vous obtenez un rapport de détecteur de motifs qui contient plus de détails sur les zones à traiter en plus des API/bundles indisponibles dans la version cible d’AEM. Le rapport Détection des motifs vous donne une indication des incompatibilités éventuelles de votre code. S’il n’en existe aucun, votre déploiement est déjà compatible avec la version 6.5. Vous pouvez toujours choisir d’effectuer un nouveau développement pour utiliser la fonctionnalité 6.5, mais vous n’en avez pas besoin uniquement pour maintenir la compatibilité. Si des incompatibilités sont signalées, vous pouvez choisir de lancer en mode de compatibilité et différer le développement de nouvelles fonctionnalités ou de la compatibilité de la version 6.5. Vous pouvez également décider de procéder au développement après la mise à niveau, puis passer à l’étape 2. Voir [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md) pour plus d’informations.

1. **Développement de la base de code pour la version 6.5**- Créez une branche ou un référentiel dédié à la base de code pour la version cible. Utilisez les informations de la compatibilité avant la mise à niveau pour prévoir les zones de code à mettre à jour.
1. **Compilation avec 6.5 Uber jar **- Mettez à jour les POM de la base de code pour pointer vers 6.5 Uber jar et compilez le code par rapport à cette dernière.
1. **Mise à jour de la personnalisation d’AEM***- *Toutes les personnalisations ou les extensions dans AEM doivent être mises à jour/validées pour fonctionner dans la version 6.5 et être ajoutées à la base de code 6.5. Comprend des formulaires de recherche d’interface utilisateur, des personnalisations de ressources, tout élément utilisant /mnt/overlay.

1. **Déploiement vers l’environnement 6.5** - Une instance AEM 6.5 nette (auteur + publication) doit être conservée dans un environnement Dev/QA. La base de code à jour et un échantillon représentatif de contenu (de l’exploitation actuelle) doivent être déployés.
1. **Validation du contrôle qualité et correction des bogues** - Le contrôle qualité doit valider l’application sur les instances d’auteur et de publication de la version 6.5. Tous les problèmes détectés doivent être corrigés et intégrés dans la base de code 6.5. Répétez Dev-Cycle si nécessaire jusqu’à ce que tous les bogues soient corrigés.

Avant de procéder à une mise à niveau, vous devez disposer d’une base de code d’application stable qui a été soigneusement testée par rapport à la version cible d’AEM. En fonction des observations effectuées dans les tests, il peut y avoir des moyens d’optimiser le code personnalisé. Par exemple, cela peut inclure la refactorisation du code pour éviter de parcourir le référentiel, l’indexation personnalisée pour optimiser la recherche ou l’utilisation de noeuds non ordonnés dans JCR, entre autres.

Outre la mise à niveau facultative de votre base de code et de vos personnalisations pour qu’elles fonctionnent avec la nouvelle version d’AEM, la version 6.5 permet de gérer plus efficacement vos personnalisations à l’aide de la fonctionnalité de compatibilité descendante, comme décrit dans la section [cette page](/help/sites-deploying/backward-compatibility.md).

Comme mentionné ci-dessus et illustré dans le diagramme ci-dessous, l’exécution de la fonction [Outil de détection des motifs](/help/sites-deploying/pattern-detector.md) dans la première étape, vous pouvez évaluer la complexité globale de la mise à niveau. Il peut également vous aider à décider si vous souhaitez exécuter le mode de compatibilité ou mettre à jour vos personnalisations pour utiliser toutes les nouvelles fonctionnalités d’AEM 6.5. Voir [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md) pour plus d’informations.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Mise à niveau de la base de code {#upgrade-code-base}

### Création d’une branche spécifique pour la version 6.5 du code dans le contrôle de version  {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Tous le code et toutes les configurations requis pour votre mise en oeuvre AEM doivent être gérés à l’aide d’une forme de contrôle de version. Une branche dédiée au contrôle de version doit être créée pour gérer les modifications nécessaires pour la base de code dans la version cible d’AEM. Les tests itératifs de la base de code par rapport à la version cible de AEM et les correctifs de bogues ultérieurs sont gérés dans cette branche.

### Mise à jour de la version AEM Uber Jar {#update-the-aem-uber-jar-version}

AEM Uber jar inclut toutes les API d’AEM en tant que dépendance unique dans le fichier `pom.xml` de votre projet Maven. Il est toujours recommandé d’inclure Uber Jar en tant que dépendance unique au lieu d’inclure les dépendances d’API d’AEM individuelles. Lors de la mise à niveau de la base de code, modifiez la version du fichier Uber Jar pour qu’elle pointe vers la version cible d’AEM. Si votre projet a été développé sur une version d’AEM avant l’existence d’Uber Jar, supprimez toutes les dépendances d’API d’AEM individuelles. Remplacez-les par une seule inclusion du fichier Uber Jar pour la version cible d’AEM. Recompilez la base de code par rapport à la nouvelle version du fichier Uber Jar. Mettez à jour les API ou méthodes obsolètes afin qu’elles soient compatibles avec la version cible d’AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Suppression de l’utilisation du résolveur de ressources d’administration {#phase-out-use-of-administrative-resource-resolver}

Utilisation d’une session d’administration via `SlingRepository.loginAdministrative()` et `ResourceResolverFactory.getAdministrativeResourceResolver()` était courante dans les bases de code avant AEM 6.0. Ces méthodes ont été abandonnées pour des raisons de sécurité, car elles offrent un niveau d’accès trop large. [Dans les futures versions de Sling, ces méthodes vont être supprimées.](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Il est vivement recommandé de refactoriser tout code pour utiliser les utilisateurs du service à la place. Informations supplémentaires sur les utilisateurs de services et [Découvrez comment supprimer progressivement les sessions administratives ici](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Requêtes et index Oak {#queries-and-oak-indexes}

Toute utilisation de requêtes dans la base de code doit être minutieusement testée dans le cadre de la mise à niveau de la base de code. Pour les clients effectuant une mise à niveau à partir de Jackrabbit 2 (versions d’AEM antérieures à la version 6.0), ce test est particulièrement important, car Oak n’indexe pas le contenu automatiquement et des index personnalisés doivent être créés. Si vous effectuez une mise à niveau à partir d’une version 6.x d’AEM, les définitions d’index Oak prêtes à l’emploi peuvent avoir changé et peuvent affecter les requêtes existantes.

Les outils suivants sont disponibles pour l’analyse et l’inspection des performances des requêtes :

* [Outils d’index AEM](/help/sites-deploying/queries-and-indexing.md)

* [Outils de diagnostic des opérations - Performance des requêtes](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Création d’interfaces utilisateur classiques {#classic-ui-authoring}

La création de l’IU classique est toujours disponible dans AEM 6.5, mais elle sera bientôt obsolète. Vous trouverez plus d’informations[ ici](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Si votre application s’exécute dans l’environnement de création de l’interface utilisateur classique, il est recommandé d’effectuer la mise à niveau vers AEM 6.5 et de continuer à utiliser l’interface utilisateur classique. La migration vers l’interface utilisateur tactile peut ensuite être planifiée en tant que projet distinct pour s’achever sur plusieurs cycles de développement. Pour utiliser l’interface utilisateur classique dans AEM 6.5, plusieurs configurations OSGi doivent être validées dans la base de code. Vous trouverez plus d’informations sur la procédure de configuration. [here](/help/sites-administering/enable-classic-ui.md).

## Alignement avec la structure de référentiel de la version 6.5 {#align-repository-structure}

Pour faciliter les mises à niveau et s’assurer que les configurations ne soient pas remplacées au cours de celles-ci, le référentiel est restructuré dans la version 6.4 afin de séparer le contenu de la configuration.

Par conséquent, plusieurs paramètres doivent être déplacés pour ne plus résider sous . `/etc` comme par le passé. Pour consulter l’ensemble des préoccupations relatives à la restructuration du référentiel qui doivent être examinées et prises en compte dans la mise à jour vers AEM 6.4, voir [Restructuration des référentiels dans AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personnalisations d’AEM  {#aem-customizations}

Toutes les personnalisations de l’environnement de création AEM dans la version source d’AEM doivent être identifiées. Une fois identifiées, il est recommandé de stocker chaque personnalisation dans le contrôle de version ou au minimum sauvegardée dans un package de contenu. Toutes les personnalisations doivent être déployées et validées dans un environnement d’assurance qualité ou d’évaluation exécutant la version cible d’AEM avant une mise à niveau de production.

### Superpositions en général {#overlays-in-general}

Il est courant d’étendre AEM fonctionnalité prête à l’emploi en superposant des noeuds et/ou des fichiers sous /libs avec des noeuds supplémentaires sous /apps. Ces recouvrements doivent être suivis dans le contrôle de version et testés par rapport à la version cible d’AEM. Si un fichier (JS, JSP, HTL, par exemple) est superposé, Adobe vous recommande de laisser un commentaire sur les fonctionnalités qui ont été améliorées pour simplifier les tests de régression sur la version cible d’AEM. Vous trouverez plus d’informations sur les superpositions en général [here](/help/sites-developing/overlays.md). Vous trouverez ci-dessous des instructions relatives à des incrustations d’AEM spécifiques.

### Mettre à niveau les formulaires de recherche personnalisés {#upgrading-custom-search-forms}

Les facettes de recherche personnalisées nécessitent quelques ajustements manuels après la mise à niveau pour fonctionner correctement. Pour en savoir plus, consultez la section [Mise à niveau des formulaires de recherche personnalisée](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personnalisations de l’interface utilisateur d’Assets {#assets-ui-customizations}

>[!NOTE]
>
>Cette procédure n’est requise que pour les mises à niveau de versions antérieures à AEM 6.2.

Les instances qui ont des déploiements de ressources personnalisés doivent être préparées pour la mise à niveau. Cette action est nécessaire pour s’assurer que tout le contenu personnalisé est compatible avec la nouvelle structure de noeuds de la version 6.4.

Vous pouvez préparer les personnalisations de l’interface utilisateur d’Assets en procédant comme suit :

1. Sur l’instance en cours de mise à niveau, ouvrez le CRXDE Lite en accédant à *https://server:port/crx/de/index.jsp*

1. Accédez au nœud suivant :

   * `/apps/dam/content`

1. Renommez le noeud de contenu en **content_backup** en cliquant avec le bouton droit sur le volet d’exploration dans la partie gauche de la fenêtre, et en choisissant **Renommer**.

1. Une fois le noeud renommé, créez un noeud nommé content sous `/apps/dam` named **content** et définissez son type de noeud sur **sling:Folder**.

1. Déplacer tous les noeuds enfants de **content_backup** au noeud de contenu nouvellement créé en cliquant avec le bouton droit de la souris sur chaque noeud enfant dans le volet de l’explorateur et en sélectionnant **Déplacer**.

1. Supprimez la variable **content_backup** noeud .

1. Les nœuds mis à jour sous `/apps/dam` avec le type de nœud correct `sling:Folder` doivent idéalement être enregistrés dans le contrôle de version et déployés avec la base de code ou au moins être sauvegardés en tant que packages de contenu.

### Génération d’identifiants pour les ressources existantes {#generating-asset-ids-for-existing-assets}

Pour générer des identifiants de ressources pour les ressources existantes, mettez à niveau les ressources lorsque vous mettez à niveau votre instance AEM pour exécuter AEM 6.5. Cette étape est nécessaire pour activer la variable [Fonctionnalité Statistiques sur les ressources](/help/assets/asset-insights.md). Pour plus de détails, consultez la section [Ajout d’un code intégré](/help/assets/use-page-tracker.md#add-embed-code).

Pour mettre à niveau les ressources, configurez le package d’identifiants de ressources associé dans la console JMX. En fonction du nombre de ressources dans le référentiel, `migrateAllAssets` peut prendre beaucoup de temps. Les tests internes d’Adobe estiment à environ une heure les ressources 125000 sur TarMK.

![1487758945977](assets/1487758945977.png)

Si vous avez besoin de plusieurs identifiants de ressources pour un sous-ensemble de vos ressources totales, utilisez l’API `migrateAssetsAtPath`.

Pour tout autre objectif, utilisez l’API `migrateAllAssets()`

### Personnalisations de script InDesign {#indesign-script-customizations}

Adobe recommande de placer les scripts personnalisés à l’emplacement `/apps/settings/dam/indesign/scripts`. Vous trouverez plus d’informations sur les personnalisations des scripts d’InDesign [here](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Récupération des configurations ContextHub {#recovering-contexthub-configurations}

Les configurations ContextHub sont affectées par la mise à niveau. Des instructions sur la façon de récupérer les configurations ContextHub existantes sont disponibles [ici](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personnalisations des workflows {#workflow-customizations}

Il est courant de modifier les workflows prêts à l’emploi pour ajouter ou supprimer des fonctionnalités inutiles. Un workflow qui est souvent personnalisé est le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]. Tous les workflows nécessitant une implémentation personnalisée doivent être enregistrés et stockés dans le contrôle de version, car ils risquent d’être remplacés lors de la mise à niveau.

### Modèles modifiables {#editable-templates}

>[!NOTE]
>
>Cette procédure est requise uniquement pour les mises à niveau de Sites à l’aide de modèles modifiables à partir d’AEM 6.2.

La structure des modèles modifiables a changé entre AEM 6.2 et 6.3. Si vous effectuez une mise à niveau à partir de la version 6.2 ou antérieure et si le contenu de votre site est créé à l’aide de modèles modifiables, vous devez utiliser la variable [Outil de nettoyage des noeuds réactifs](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). L’outil est destiné à être exécuté. **after** une mise à niveau pour nettoyer le contenu. Exécutez-le sur les niveaux Auteur et Publication.

### Modifications de l’implémentation des CUG {#cug-implementation-changes}

L’implémentation des groupes d’utilisateurs fermés a considérablement changé pour répondre aux limites de performances et d’évolutivité des versions précédentes d’AEM. La version précédente du CUG a été abandonnée dans la version 6.3 et la nouvelle mise en oeuvre n’est prise en charge que dans l’interface utilisateur tactile. Si vous effectuez une mise à niveau à partir de la version 6.2 ou antérieure, vous trouverez des instructions pour migrer vers la nouvelle mise en oeuvre de CUG. [here](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procédure de test {#testing-procedure}

Un plan de test complet doit être préparé pour tester les mises à niveau. Le test de la base de code et de l’application mise à niveau doit d’abord être effectué dans les environnements inférieurs. Tous les bogues détectés doivent être corrigés itérativement jusqu’à ce que la base de code soit stable, mais les environnements de niveau supérieur doivent être mis à niveau.

### Test de la procédure de mise à niveau {#testing-the-upgrade-procedure}

La procédure de mise à niveau décrite ici doit être testée sur les environnements de développement et d’assurance qualité, comme indiqué dans votre runbook personnalisé (voir [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md)). La procédure de mise à niveau doit être répétée jusqu’à ce que toutes les étapes soient documentées dans le runbook de mise à niveau et que le processus de mise à niveau soit fluide.

### Zones de test d’implémentation  {#implementation-test-areas-}

Vous trouverez ci-dessous les zones critiques de toute implémentation d’AEM qui doit être couverte par votre plan de test une fois l’environnement mis à niveau et la base de code mise à niveau déployée.

<table>
 <tbody>
  <tr>
   <td><strong>Zone de test fonctionnelle</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Sites publiés</td>
   <td>Test de l’implémentation AEM et du code associé au niveau de publication<br /> par le biais de Dispatcher. Doit inclure des critères pour les mises à jour de page et<br /> invalidation du cache.</td>
  </tr>
  <tr>
   <td>Création</td>
   <td>Test de l’implémentation AEM et du code associé sur le niveau Auteur. Doit inclure la page, la création de composants et les boîtes de dialogue.</td>
  </tr>
  <tr>
   <td>Intégrations avec des solutions Experience Cloud</td>
   <td>Validation des intégrations avec des produits tels qu’Analytics, DTM et Target.</td>
  </tr>
  <tr>
   <td>Intégrations à des systèmes tiers</td>
   <td>Validez toutes les intégrations tierces sur les niveaux Auteur et Publication.</td>
  </tr>
  <tr>
   <td>Authentification, sécurité et autorisations</td>
   <td>Tous les mécanismes d’authentification tels que LDAP/SAML doivent être validés.<br /> Les autorisations et les groupes doivent être testés sur les instances de création et de publication.<br /> niveaux.</td>
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
   <td>Processus et fonctionnalités personnalisés et/ou prêts à l’emploi.</td>
  </tr>
  <tr>
   <td>Test de performance</td>
   <td>Les tests de chargement doivent être effectués sur les niveaux Auteur et Publication qui simulent des scénarios du monde réel.</td>
  </tr>
 </tbody>
</table>

### Plan et résultats de test du document {#document-test-plan-and-results}

Vous devez créer un plan de tests qui couvre les zones de tests d’implémentation décrites ci-dessus. Souvent, il est logique de séparer le plan de test par les listes de tâches Auteur et Publier . Ce plan de test doit être exécuté sur les environnements de développement, d’assurance qualité et d’évaluation avant la mise à niveau des environnements de production. Les résultats de test et les mesures de performances doivent être capturés dans des environnements inférieurs afin de fournir une comparaison lors de la mise à niveau des environnements d’évaluation et de production.
