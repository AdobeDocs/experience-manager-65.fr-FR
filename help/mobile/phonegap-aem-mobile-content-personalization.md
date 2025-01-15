---
title: Personnalisation du contenu Adobe Experience Manager Mobile
description: Consultez cette page pour en savoir plus sur la fonctionnalité de personnalisation du contenu mobile d’Adobe Experience Manager (AEM) qui permet aux auteurs AEM de personnaliser le contenu des applications mobiles à l’aide d’Adobe Target.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 1%

---

# Personnalisation du contenu AEM Mobile{#aem-mobile-content-personalization}

{{ue-over-mobile}}

>[!NOTE]
>
>Ce document fait partie du guide [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md), un point de départ recommandé pour la référence à AEM Mobile.

La fonctionnalité de personnalisation de contenu d’AEM Mobile permet aux [auteurs AEM](#author) de personnaliser le contenu des applications mobiles à l’aide d’[Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html). Cela permet de diffuser des offres ciblées aux utilisateurs de l&#39;application mobile. Adobe Experience Manager Mobile permet de créer, de cibler et de diffuser du contenu qui fournira à l’utilisateur un contenu spécifique à ses propres goûts.

Dans AEM, pour que les auteurs puissent commencer à créer ce contenu, les administrateurs et les développeurs doivent d’abord préparer l’environnement.

[Les administrateurs et administratrices AEM](#administrator) doivent établir une connexion entre AEM Mobile et Adobe Target Cloud Service.

En attendant, les [développeurs](#developer) d’AEM Mobile doivent modifier leurs scripts existants pour faciliter la création de contenu ciblée.

## Pour les administrateurs {#for-administrators}

Plusieurs étapes doivent être franchies avant que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : il faut obtenir l’ensemble approprié d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.

Cet article vous guide tout au long du processus de configuration de l’[application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) pour le ciblage.

L’hypothèse pour l’avenir est que l’application de référence hybride AEM Mobile a été déployée avec succès et accessible via le tableau de bord AEM Mobile.

Avant que les auteurs puissent générer du contenu ciblé dans une application, votre instance AEM doit être [configurée avec Adobe Target Cloud Service](/help/mobile/aem-mobile-configuring-cloud-service.md).

### Autorisations {#permissions}

Les utilisateurs et utilisatrices qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors`.

Il est suggéré que, dans le cadre de la configuration des utilisateurs et des groupes, le groupe target-activity-group soit ajouté au groupe apps-admins. L’ajout du groupe target-activity-authors permet aux utilisateurs de voir l’entrée du menu de navigation de Personalization.

>[!NOTE]
>
>L’oubli de l’ajout des utilisateurs ou des groupes auxquels vous souhaitez accorder l’accès à l’Admin Console de personnalisation au groupe target-activity-authors empêche les utilisateurs de voir la console de personnalisation.

### Services cloud {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur permettant de traiter les requêtes des clients et de renvoyer le contenu personnalisé. Le service Adobe Mobile Services assure la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json qui est utilisé par le plug-in AMS Cordova. Depuis le tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

Dans le tableau de bord AEM Mobile, recherchez Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-38](assets/chlimage_1-38.png)

Dans l’assistant Ajouter un Cloud Service , sélectionnez la carte de service cloud « Adobe Target », puis cliquez sur Suivant.

![chlimage_1-39](assets/chlimage_1-39.png)

Dans la liste déroulante Sélectionner une configuration , vous pouvez créer une configuration ou en sélectionner une existante. Pour créer une configuration, sélectionnez Créer une configuration dans la liste déroulante. Saisissez un titre pour la configuration Target. Saisissez le code client, l’adresse e-mail et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez l’assistance technique d’Adobe Target. Cliquez sur le bouton « Vérifier » pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

>[!NOTE]
>
>Le service cloud qui est créé est automatiquement associé à l’application mobile via l’assistant. La valeur de la propriété cq:cloudserviceconfigs est définie sur le nœud jcr:content du nœud du groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybride-reference-app/jcr:content avec la valeur pointant vers le nœud de framework généré automatiquement à l’emplacement /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le nœud de framework possède deux propriétés définies par défaut : le genre et l’âge. Le framework est uniquement utilisé par la prévisualisation AEM et n’a aucun impact sur l’appareil.

Une fois l’assistant terminé, la mosaïque Gérer le Cloud Service contient le service cloud Target. Cependant, il contient un avertissement concernant un compte Adobe Mobile Service manquant.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Il est également nécessaire de lier un compte AMS (Adobe Mobile Services) à l’application. Le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations de code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous sur [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l&#39;application mobile et cliquez sur les paramètres. Recherchez le champ Options de SDK Target et placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-41](assets/chlimage_1-41.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord mobile d’Adobe, les paramètres des paramètres du service seront diffusés via le fichier ADBMobileConfig.json.

### Cloud Service Adobe Mobile Service {#adobe-mobile-service-cloud-service}

Maintenant qu’AMS est configuré, il est temps d’associer l’application mobile dans le tableau de bord mobile d’Adobe. Dans le tableau de bord AEM Mobile, recherchez Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-42](assets/chlimage_1-42.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-43](assets/chlimage_1-43.png)

À l’étape de l’assistant Créer ou Sélectionner , sélectionnez le menu déroulant Service mobile et sélectionnez l’entrée Créer une configuration . Indiquez un titre, une société, un nom d’utilisateur et un mot de passe, puis sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs remplis, cliquez sur **Vérifier**. Le processus de vérification va dans AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste d’applications mobiles est renseignée dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur **Envoyer** pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et toute analyse associée à l’application. Une fois le processus terminé, cliquez sur **Terminé** pour revenir au tableau de bord mobile d’Adobe.

Pour revenir au tableau de bord mobile, la mosaïque Gérer les Cloud Service contient le service cloud AMS. En outre, la mosaïque Analyser les mesures est remplie de rapports de cycle de vie.

![chlimage_1-44](assets/chlimage_1-44.png)

## Pour les auteurs {#for-authors}

**Condition préalable :** comme mentionné ci-dessus, les administrateurs doivent configurer la connexion au service Adobe Target avant que les auteurs puissent générer du nouveau contenu ciblé.

Une fois que l’administrateur a configuré les deux services cloud et que le développeur a configuré le gestionnaire d’offres mobiles, les auteurs de contenu peuvent commencer à générer des expériences ciblées.

La création de contenu ciblé dans une application AEM Mobile suit une procédure similaire à la création d’AEM Sites :

Consultez ici un aperçu complet de la [création de contenu ciblé dans AEM](/help/sites-authoring/personalization.md)

## Pour les développeurs {#for-developers}

Les développeurs et développeuses AEM qui créent des applications mobiles doivent continuer à suivre les schémas couramment utilisés dans AEM lors du développement de composants. Ici, Adobe vous guide tout au long des étapes nécessaires pour permettre aux auteurs de contenu de créer du contenu ciblé :

### Gestionnaires de synchronisation de contenu Adobe Target {#adobe-target-contentsync-handlers}

Pour diffuser du contenu sur l’appareil de l’utilisateur, le contenu est généré en effectuant le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cibles, un nouveau gestionnaire de synchronisation de contenu traite les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). L’étape suivante est cruciale pour le rendu des offres sur l’appareil. Le gestionnaire mobileappoffers comporte une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, s’il existe une activité sous */content/campaigns/hybridref*, copiez ce chemin et collez-le en tant que valeur dans la propriété *path* du gestionnaire mobileappoffers.

>[!NOTE]
>
>Pour l’application de référence hybride, il existe deux gestionnaires d’offres mobiles, l’un pour le développement et l’autre pour les productions.

Une fois que le chemin d’accès des activités est défini dans la propriété de chemin du gestionnaire mobileappoffers, enregistrez le gestionnaire. Le gestionnaire est maintenant prêt à commencer le rendu des offres pour les appareils mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec une valeur de *publish* définie sur le nœud cq:ContentSyncConfig. Le gestionnaire mobileappoffers référence renderMode et, s’il est défini sur publish, modifie l’identifiant de mbox qui est créé. Par défaut, les mbox créées par AEM sont dotées de la valeur —author ajoutée à l’identifiant de mbox. Cela identifie que l&#39;activité n&#39;a pas été publiée et doit utiliser la campagne dépubliée pour les résolutions d&#39;offre.

Lorsque le contenu est évalué via le tableau de bord mobile d’Adobe, le contenu évalué est considéré comme du contenu prêt pour la production et est rendu via la configuration de synchronisation de contenu hors développement. Avec un rendu de cette manière, —author sera supprimé de tous les identifiants de mbox et une activité publiée sera disponible sur le serveur Target. Avant de tester le contenu évalué, assurez-vous que l’activité est déjà publiée.

### Développement d’applications Personalization {#personalization-app-development}

#### Composants {#components}

La base de tout contenu est généralement un composant de page qui étend l’un des composants de page AEM de base wcm/foundation/components/page ou foundation/components/page selon que vous utilisez HTL ou JSP. La durée de ces étapes est axée sur l’utilisation du composant wcm/foundation/components/page. La structure de base du composant de page est divisée en plusieurs scripts, chaque script fournissant l’objectif spécifique de permettre au développeur ou à la développeuse d’organiser et de remplacer leur code si nécessaire. Les deux scripts qui intéressent Personalization sont head.html et body.html. Ces deux scripts fournissent une zone où du code peut être injecté pour prendre en charge la création ContextHub, de Cloud Service et Mobile.

Voici un aperçu des deux principaux scripts utilisés pour activer le ciblage du contenu.

#### head.html {#head-html}

Pour permettre à l’auteur de cibler son contenu, le menu cible doit être ajouté à la page afin que l’auteur puisse passer du mode d’édition au mode de ciblage. Pour activer cette fonctionnalité, le développeur doit modifier le script head.html afin d’inclure le fragment de code suivant près du haut du fichier head.html ou aussi près que possible de l’élément &lt;title>&lt;/title>.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>N’incluez le script que lorsque le mode de gestion de contenu Web est désactivé, de sorte que lorsque ce dernier est désactivé (voir la section relative au gestionnaire de synchronisation de contenu pour plus de détails), le script n’est pas inclus dans le code d’application final.

Pour permettre aux auteurs de prévisualiser le contenu ciblé, l’éditeur doit pouvoir localiser la configuration du service cloud d’Adobe Target. Le bloc de code ci-dessous ajoute deux scripts importants. La première permettant à la page de localiser le service cloud Target associé et d’effectuer les appels vers Adobe Target. La seconde est l’ajout de la catégorie de ciblage cq.apps.target .

La catégorie **cq.apps.targeting** remplace le composant cq/personalization/component/target par défaut et utilise le composant mobileapps/components/target qui effectue le rendu des offres spécifiquement pour la consommation d’applications mobiles. Vous trouverez plus d’informations à ce sujet dans la section Composant Target .

Le code doit être ajouté dans head.html et placé juste avant la fin de l’élément &lt;/head>.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Le bloc de code est encapsulé dans un mode de gestion de contenu web qui n’est pas désactivé et qui n’entre donc en jeu que lorsque l’auteur de contenu travaille à la création de contenu. Les scripts de service cloud ne sont pas ajoutés au code d’exécution mobile généré.

#### body.html {#body-html}

Pour permettre à l’auteur de contenu de tester différentes personnes, le script body.html doit inclure le bloc de code suivant en tant que premier enfant de l’élément de corps.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

Le dernier bit de code requis se trouve au bas de body.html. Ce bit de code recherche le service cloud associé et injecte le code du moteur de ciblage approprié.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Application de référence {#reference-application}

Vous trouverez des exemples de head.html et body.html dans l’[Application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) indiquant au développeur ou à la développeuse où placer les blocs de script dans les deux scripts.

### Gestionnaires de synchronisation de contenu {#content-sync-handlers}

Lorsque l’auteur du contenu a terminé de créer du contenu pour l’application mobile, l’étape suivante consiste à télécharger la source et à créer l’application, ou à préparer le contenu à publier. Pour ce faire, le développeur doit suivre plusieurs étapes. Pour faciliter le rendu du contenu, AEM Mobile utilise des gestionnaires de synchronisation de contenu pour effectuer le rendu et le package du contenu. Un nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation Personalization afin de générer du contenu ciblé. Le gestionnaire « mobileappoffers » sait comment effectuer le rendu des offres cibles associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. De ce fait, de nombreuses propriétés sont similaires. Les détails du gestionnaire mobileappOffers possèdent les propriétés suivantes.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>réécrire</td>
   <td>+ relativeParentPath<p> - « / »</p> </td>
   <td>La propriété rewrite identifie comment les chemins d’accès dans le contenu doivent être réécrits.</td>
  </tr>
  <tr>
   <td>includePageTypes</td>
   <td><p>« cq/personalization/components/teaserpage »,</p> <p>« cq/personalization/components/offerproxy »</p> </td>
   <td>La propriété includePageTypes est facultative, et correspond par défaut aux pages qui ont les types de ressources cq/personalization/components/teaserpage et cq/personalization/components/offerproxy. Ces deux types de ressources sont les types de ressources par défaut utilisés lorsque le contenu est ciblé. Si d’autres types de ressources doivent être pris en charge, ajoutez-les à la liste des includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Emplacement de l’application.</td>
  </tr>
  <tr>
   <td>Type</td>
   <td>mobileappooffer</td>
   <td>Nom du gestionnaire mobileappoffers.</td>
  </tr>
  <tr>
   <td>sélecteur</td>
   <td>tandt</td>
   <td>Le sélecteur Tandt est utilisé pour effectuer le rendu du contenu ciblé. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>Répertoire racine dans lequel conserver le contenu rendu.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>vrai | faux</td>
   <td>Si la valeur est true, toutes les images incluses dans l’offre sont rendues. Si la valeur est false, les images sont ignorées.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>vrai | faux</td>
   <td>Si la valeur est true, toutes les vidéos incluses dans l’offre seront rendues. Si la valeur est false, les vidéos sont ignorées.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;marque&gt;</td>
   <td>Indique la marque de la campagne à laquelle les offres participent. Actuellement, toutes les offres doivent provenir de la même campagne.</td>
  </tr>
  <tr>
   <td>profondeur</td>
   <td>vrai | faux</td>
   <td>Si la valeur est true, le rendu de toutes les pages enfants est récursif, si la valeur est false, il ne l’est pas. </td>
  </tr>
  <tr>
   <td>Extension</td>
   <td>html</td>
   <td>Définit l’extension de la ressource en cours de rendu. Définissez-le sur html de sorte que les pages aient une extension .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>L&#39;application de référence hybride [AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) possède la configuration par défaut du gestionnaire mobileappoffer. La propriété path dans l’exemple est vide, car elle dépend de l’emplacement de la campagne. Une fois qu’un auteur Campaign a créé une campagne, l’administrateur des applications doit associer la campagne au gestionnaire en spécifiant la propriété de chemin d’accès pour pointer vers la campagne.

### Composant cible {#target-component}

Pour faciliter le rendu du contenu destiné spécifiquement aux applications mobiles, AEM Mobile utilise le composant mobileapps/components/target. Le composant cible mobile étend le composant cq/personalization/components/target et remplace le script engine_tnt.jsp. En remplaçant le fichier engine_tnt.jsp, AEM Mobile peut contrôler l’HTML généré pour le cas d’utilisation des applications mobiles. Pour chaque composant ciblé par un auteur de contenu, une mbox associée est créée par le fichier engine_tnt.jsp.

Pour chaque mbox, un attribut **cq-targeting** est ajouté, ce qui permet aux développeurs d’applications d’écrire du code personnalisé pour consommer et utiliser comme ils le souhaitent. L’application de référence hybride [AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) contient un exemple de directive d’Angular qui utilise l’attribut cq-targeting. Le concept de remplacement de contenu, quand et comment il est effectué, dépend du développeur ou de la développeuse d’applications mobiles. Il existe un SDK mobile fourni par l’intermédiaire d’AEM /etc/clientlibs/mobileapps/js/mobileapps.js qui fournit une API pour appeler le service de ciblage d’Adobe. Il appartient au développeur ou à la développeuse d’applications de spécifier le moment où cet appel doit être effectué en fonction de la conception de leur application.

## Quelle est la suite ? {#what-s-next}

1. [Démarrer mon expérience d’application AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gérer le contenu de mon application](/help/mobile/phonegap-manage-app-content.md)
1. [Créer mon application](/help/mobile/building-app-mobile-phonegap.md)
1. [Suivre les performances de mon application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Offrir une expérience d’application personnalisée avec Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Envoyer des messages importants à mes utilisateurs](/help/mobile/phonegap-push-notifications.md)
