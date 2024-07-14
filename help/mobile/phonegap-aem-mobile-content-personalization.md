---
title: Personnalisation du contenu Adobe Experience Manager Mobile
description: Consultez cette page pour en savoir plus sur la fonction de personnalisation de contenu mobile Adobe Experience Manager (AEM) qui permet aux auteurs AEM de personnaliser le contenu des applications mobiles à l’aide d’Adobe Target.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 2%

---

# Personnalisation du contenu AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Ce document fait partie du guide [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md), un point de départ recommandé pour la référence AEM Mobile.

La fonction de personnalisation du contenu AEM Mobile permet à [AEM auteurs](#author) de personnaliser le contenu des applications mobiles à l’aide de [Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html). Cela permet la diffusion d’offres ciblées aux utilisateurs d’applications mobiles. Adobe Experience Manager Mobile permet de créer, de cibler et de diffuser du contenu qui fournira à l’utilisateur du contenu spécifique à ses goûts.

Dans AEM, pour que les auteurs puissent commencer à créer ce contenu, les administrateurs et les développeurs doivent d’abord préparer l’environnement.

[AEM administrateurs](#administrator) sont nécessaires pour établir une connexion entre AEM Mobile et le Cloud Service Adobe Target.

Pendant ce temps, les [développeurs](#developer) d’AEM Mobile doivent modifier leurs scripts existants pour faciliter la création de contenu ciblé.

## Pour les administrateurs {#for-administrators}

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : il existe un ensemble approprié d’autorisations pour les utilisateurs et les groupes, la création de services cloud, la configuration de l’application pour l’activité et enfin la génération du contenu.

Cet article vous guide tout au long du processus utilisé pour configurer l’ [application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) pour le ciblage.

L’hypothèse à l’avenir est que l’application de référence hybride AEM Mobile a été déployée avec succès et accessible via le tableau de bord AEM Mobile.

Avant que les auteurs puissent générer du contenu ciblé dans une application, votre instance AEM doit être [ configurée avec le Cloud Service Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors`.

Dans le cadre de la configuration des utilisateurs et des groupes, il est conseillé d’ajouter le groupe target-activity-group au groupe apps-admins . En ajoutant le groupe target-activity-authors, les utilisateurs peuvent ainsi voir l’entrée du menu de navigation de Personalization.

>[!NOTE]
>
>L’oubli de l’ajout des utilisateurs ou des groupes auxquels vous souhaitez accéder à l’Admin Console de personnalisation au groupe target-activity-authors empêche les utilisateurs de voir la console de personnalisation.

### Services cloud {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur pour le traitement des requêtes client et le renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json qui est utilisé par le module externe AMS Cordova. Depuis le tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-38](assets/chlimage_1-38.png)

Dans l’assistant Ajouter un Cloud Service, sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-39](assets/chlimage_1-39.png)

Dans la liste déroulante Sélectionner une configuration , vous pouvez créer une configuration ou en sélectionner une existante. Pour créer une configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Saisissez un titre pour la configuration Target. Saisissez le code client, l’adresse électronique et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez le support Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les identifiants. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

>[!NOTE]
>
>Le service cloud qui est créé est automatiquement associé à l&#39;application mobile via l&#39;assistant. La valeur de la propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud du groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybride-reference-app/jcr:content avec la valeur pointant vers le noeud de structure généré automatiquement à l’emplacement /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le noeud de structure possède deux propriétés définies par défaut, le genre et l’âge. La structure n’est utilisée que par AEM prévisualisation et n’a aucun impact sur l’appareil.

Une fois l’assistant terminé, la mosaïque Gérer le Cloud Service contient le service cloud Target. Il contient toutefois un avertissement concernant un compte Mobile Service Adobe manquant.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Pour lier également un compte Mobile Services (AMS) Adobe à l’application, le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations du code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous à l&#39;adresse [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l&#39;application mobile et cliquez sur les paramètres. Localisez le champ Options du SDK Target et placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-41](assets/chlimage_1-41.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord mobile Adobe, les paramètres des paramètres du service sont fournis via le fichier ADBMobileConfig.json .

### Adobe du Cloud Service Mobile Service {#adobe-mobile-service-cloud-service}

Maintenant qu’AMS est configuré, il est temps d’associer l’application mobile dans le tableau de bord Mobile Adobe. Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-42](assets/chlimage_1-42.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-43](assets/chlimage_1-43.png)

À l’étape de l’assistant Créer ou Sélectionner , sélectionnez la liste déroulante Mobile Service , puis l’entrée Créer une configuration . Indiquez un titre, une société, un nom d’utilisateur et un mot de passe, puis sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs renseignés, cliquez sur **Vérifier**. Le processus de vérification passe à AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste d’applications mobiles est renseignée dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur **Submit** pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et toute analyse associée à l’application. Une fois le processus terminé, cliquez sur **Terminé** pour revenir au tableau de bord Mobile Adobe.

Pour revenir au tableau de bord mobile, la mosaïque Gérer les Cloud Service contient le service cloud AMS. En outre, la mosaïque Analyser les mesures est remplie avec des rapports de cycle de vie.

![chlimage_1-44](assets/chlimage_1-44.png)

## Pour les auteurs {#for-authors}

**Condition préalable requise :** Comme mentionné ci-dessus, les administrateurs doivent configurer la connexion au service Adobe Target pour que les auteurs puissent générer un nouveau contenu ciblé.

Une fois que l’administrateur a configuré les deux services cloud et que le développeur a configuré le gestionnaire d’offres mobiles, les auteurs de contenu peuvent commencer à générer des expériences ciblées.

La création de contenu ciblé dans une application AEM Mobile suit une procédure similaire à celle de la création d’AEM Sites :

Cliquez ici pour une présentation complète de la [création de contenu ciblé dans AEM](/help/sites-authoring/personalization.md)

## Pour les développeurs {#for-developers}

AEM développeurs qui créent des applications mobiles doivent continuer à suivre les modèles couramment utilisés dans AEM lors du développement de composants. Adobe vous guide tout au long des étapes nécessaires pour permettre aux auteurs de contenu de créer du contenu ciblé :

### Gestionnaires de synchronisation de contenu Adobe Target {#adobe-target-contentsync-handlers}

Pour diffuser du contenu sur l’appareil de l’utilisateur, le contenu est généré par le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cibles, il existe un nouveau gestionnaire de synchronisation de contenu qui traite les offres. En utilisant l’application de référence hybride comme exemple, le module de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . L’étape suivante est cruciale pour le rendu des offres sur l’appareil. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, si une activité se trouve à l’emplacement */content/campaigns/hybridref*, copiez ce chemin et collez-le en tant que valeur de la propriété *path* du gestionnaire mobileappoffers.

>[!NOTE]
>
>Pour l’application de référence hybride, il existe deux gestionnaires mobileappoffers : un pour le développement et un autre pour les productions.

Une fois le chemin d’accès aux activités défini dans la propriété path du gestionnaire mobileappoffers, enregistrez le gestionnaire. Le gestionnaire est maintenant prêt à lancer le rendu des offres pour les périphériques mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire de ressources mobiles est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec une valeur *publish* définie sur le noeud cq:ContentSyncConfig . Le gestionnaire mobileappoffers fait référence à renderMode et, s’il est défini sur publish, modifie l’ID de mbox qui est créé. Par défaut, les mbox créées par AEM ont une valeur —author ajoutée à l’identifiant mbox. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est intermédiaire via le tableau de bord mobile Adobe, le contenu intermédiaire est considéré comme du contenu prêt pour la production et est rendu via la configuration de synchronisation de contenu non développée. Le rendu de cette manière entraînera la suppression de l’auteur —de tous les identifiants de mbox et prévoit qu’une activité publiée sera disponible sur le serveur Target. Avant de tester le contenu intermédiaire, vérifiez que l’activité est déjà publiée.

### Développement d’applications Personalization {#personalization-app-development}

#### Composants {#components}

La base de tout contenu est généralement un composant de page qui étend l’un des composants de page de base AEM wcm/foundation/components/page ou foundation/components/page selon que vous utilisez HTL ou JSP. La durée de ces étapes se concentre sur l’utilisation du composant wcm/foundation/components/page . La structure de base du composant de page est divisée en plusieurs scripts, chaque script fournissant l’objectif spécifique de permettre au développeur d’organiser et de remplacer son code si nécessaire. Les deux scripts intéressants pour Personalization sont head.html et body.html. Ces deux scripts fournissent une zone dans laquelle le code peut être injecté pour prendre en charge la création ContextHub, Cloud Service et Mobile.

Voici un aperçu des deux scripts principaux utilisés pour activer le ciblage du contenu.

#### head.html {#head-html}

Pour permettre à l’auteur de cibler son contenu, le menu cible doit être ajouté à la page afin que l’auteur puisse passer du mode d’édition au mode de ciblage. Pour activer cette fonction, le développeur doit modifier le script head.html afin d’inclure le fragment de code suivant près du haut de head.html ou aussi près que possible de l’élément &lt;title>&lt;/title> .

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>N’incluez le script que lorsque le mode WCM est désactivé, de sorte que lorsque le mode WCM est désactivé (voir la section du gestionnaire ContentSync pour plus de détails), le script n’est pas inclus dans le code d’application final.

Pour permettre aux auteurs de prévisualiser le contenu ciblé, l’éditeur doit être en mesure de localiser la configuration du service cloud Adobe Target. Le bloc de code ci-dessous ajoute deux scripts importants. Le premier ajout de la possibilité pour la page de localiser le service cloud Target associé et d’envoyer les appels à Adobe Target. Le second est l’ajout de la catégorie cq.apps.targeting .

La catégorie **cq.apps.targeting** remplace le composant cq/personalization/component/target par défaut et utilise le composant mobileapps/components/target qui effectue le rendu des offres spécifiquement pour la consommation d’applications mobiles. Pour plus d’informations à ce sujet, consultez la section Composant cible .

Le code doit être ajouté dans head.html et placé juste avant la fin de l’élément &lt;/head> .

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Le bloc de code n’est pas encapsulé dans un mode WCM. Il n’est donc pas désactivé. Il entre donc en jeu que lorsque l’auteur du contenu travaille à la création de contenu. Les scripts du service cloud ne sont pas ajoutés au code d’exécution mobile généré.

#### body.html {#body-html}

Pour permettre à l’auteur de contenu de tester différentes personas, le script body.html doit inclure le bloc de code suivant comme premier enfant de l’élément de corps.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

La dernière partie de code requise se trouve au bas de body.html. Ce code recherche le service cloud associé et injecte le code du moteur de ciblage approprié.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Application de référence {#reference-application}

Vous trouverez des exemples head.html et body.html dans l’ [ application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) qui indique au développeur où placer les blocs de script dans les deux scripts.

### Gestionnaires de synchronisation de contenu {#content-sync-handlers}

Lorsque l’auteur du contenu a fini de créer du contenu pour l’application mobile, l’étape suivante consiste à télécharger la source et à créer l’application, ou à préparer le contenu à publier. Pour ce faire, le développeur doit suivre plusieurs étapes. Pour faciliter le rendu du contenu, AEM Mobile utilise des gestionnaires de synchronisation de contenu pour générer et empaqueter le contenu. Un nouveau gestionnaire de synchronisation de contenu a été ajouté pour le cas d’utilisation de Personalization afin de rendre le contenu ciblé. Le gestionnaire &quot;mobileappoffers&quot; sait comment effectuer le rendu des offres cibles associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. Par conséquent, de nombreuses propriétés sont similaires. Les détails du gestionnaire de mobileappoffers possèdent les propriétés suivantes.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>rewrite</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>La propriété rewrite identifie la manière dont les chemins d’accès dans le contenu doivent être réécrits.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offer"</p> </td>
   <td>La propriété includePageTypes est facultative. Par défaut, elle concerne les pages qui comportent des types de ressources cq/personalization/components/teaserpage et cq/personalization/components/offerproxy. Ces deux types de ressources sont les types de ressources par défaut utilisés lorsque le contenu est ciblé. Si des types de ressources supplémentaires doivent être pris en charge, ajoutez-les à la liste des includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Emplacement de l’application.</td>
  </tr>
  <tr>
   <td>Type</td>
   <td>mobileappoffers</td>
   <td>Nom du gestionnaire en cours de mobileappoffers.</td>
  </tr>
  <tr>
   <td>sélecteur</td>
   <td>tandt</td>
   <td>Le sélecteur de tandt est utilisé pour effectuer le rendu du contenu ciblé. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>Répertoire racine dans lequel conserver le contenu rendu.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Si la valeur est définie sur true, les images incluses dans l’offre sont rendues. Si la valeur est false, les images sont ignorées.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Si la valeur est définie sur true, les vidéos incluses dans l’offre sont affichées. Si la valeur est false, les vidéos sont ignorées.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;marque&gt;</td>
   <td>Identifie la marque de l'opération à laquelle participent les offres. Actuellement, toutes les offres doivent provenir de la même campagne.</td>
  </tr>
  <tr>
   <td>profondeur</td>
   <td>true | false</td>
   <td>Si la valeur est définie sur true de manière récursive, toutes les pages enfants sont générées, si la valeur est définie sur false, elles ne sont pas récurrentes. </td>
  </tr>
  <tr>
   <td>Extension</td>
   <td>html</td>
   <td>Définit l’extension de la ressource en cours de rendu. Définissez cette variable sur html de sorte que les pages disposent d’une extension .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>L’ [application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) possède la configuration par défaut du gestionnaire d’offres mobiles. La propriété path de l’exemple est vide, car elle dépend de l’emplacement de la campagne. Une fois qu’un auteur de campagne a créé une campagne, l’administrateur d’applications doit associer la campagne au gestionnaire en spécifiant la propriété de chemin d’accès vers la campagne.

### Composant cible {#target-component}

Pour faciliter le rendu du contenu spécifiquement pour les applications mobiles, AEM Mobile utilise le composant mobileapps/components/target . Le composant cible mobile étend le composant cq/personalization/components/target et remplace le script engine_tnt.jsp. En remplaçant le fichier engine_tnt.jsp, AEM Mobile peut contrôler l’HTML généré pour le cas d’utilisation des applications mobiles. Pour chaque composant ciblé par un auteur de contenu, une mbox associée est créée par engine_tnt.jsp.

Pour chaque mbox, un attribut **cq-targeting** est ajouté pour permettre aux développeurs d’applications d’écrire du code personnalisé à utiliser comme bon leur semble. L’ [application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) comporte un exemple de directive d’Angular qui utilise l’attribut cq-targeting . Le concept de remplacement du contenu, le moment et la manière dont il est effectué, dépend du développeur de l’application mobile. Un SDK Mobile est fourni via AEM /etc/clientlibs/mobileapps/js/mobileapps.js qui fournit une API pour appeler le service de ciblage d’Adobe. Il appartient au développeur de l’application de spécifier le moment où cet appel doit être effectué en fonction de la conception de son application.

## Et après ? {#what-s-next}

1. [Démarrer l’expérience de l’application AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gérer le contenu de mon application](/help/mobile/phonegap-manage-app-content.md)
1. [Créer mon application](/help/mobile/building-app-mobile-phonegap.md)
1. [Suivi des performances de mon application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Proposer une expérience d’application personnalisée avec Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Envoyer des messages importants à mes utilisateurs](/help/mobile/phonegap-push-notifications.md)
