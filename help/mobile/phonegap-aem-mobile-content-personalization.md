---
title: Personnalisation du contenu AEM Mobile
seo-title: Personnalisation du contenu AEM Mobile
description: Suivez cette page pour en savoir plus sur la fonction de personnalisation du contenu AEM Mobile qui permet aux auteurs AEM de personnaliser le contenu des applications mobiles en exploitant Adobe Target.
seo-description: Suivez cette page pour en savoir plus sur la fonction de personnalisation du contenu AEM Mobile qui permet aux auteurs AEM de personnaliser le contenu des applications mobiles en exploitant Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 3%

---


# Personnalisation du contenu AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>This document is part of the [Getting Started with AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, a recommended starting point for AEM Mobile reference.

La fonction de personnalisation de contenu AEM Mobile permet aux auteurs [](#author) AEM de personnaliser le contenu des applications mobiles en exploitant [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Cela permet la diffusion d’offres ciblées aux utilisateurs d’applications mobiles. Adobe Experience Manager Mobile permet de créer, de cible et de diffuser du contenu qui fournit à l’utilisateur un contenu spécifique à ses goûts.

Comme c&#39;est souvent le cas en AEM, pour que les auteurs puissent commencer à créer ce contenu, les administrateurs et les développeurs doivent d&#39;abord préparer l&#39;environnement.

[aem les administrateurs](#administrator) doivent établir une connexion entre AEM Mobile et le Cloud Service Adobe Target.

En attendant, [les développeurs](#developer) AEM Mobile doivent modifier leurs scripts existants pour faciliter la création de contenu ciblé.

## Pour les administrateurs {#for-administrators}

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent début de générer du contenu ciblé pour les applications mobiles : Il existe un jeu d’autorisations approprié pour les utilisateurs et les groupes, la création de services cloud, la configuration de l’application pour l’activité et enfin la génération du contenu.

Cet article vous guide tout au long du processus de configuration de l’application [de référence hybride](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile pour le ciblage.

L’hypothèse suivante est que l’application de référence hybride AEM Mobile a été déployée avec succès et accessible via le Tableau de bord AEM Mobile.

Avant que les auteurs puissent générer du contenu ciblé au sein d’une application, votre instance AEM doit être [configurée avec l’Cloud Service Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du `target-activity-authors` groupe.

Il est conseillé, dans le cadre de la configuration des utilisateurs et des groupes, d’ajouter le groupe d’activités-cibles au groupe d’administrateurs d’applications. En ajoutant le groupe cible-activités-auteurs, cela permet aux utilisateurs de voir l’entrée du menu de navigation Personnalisation.

>[!NOTE]
>
>Si vous oubliez d’ajouter les utilisateurs ou les groupes auxquels vous souhaitez accéder à la console d’administration de la personnalisation au groupe d’auteurs d’activités-cibles, les utilisateurs ne pourront pas voir la console de personnalisation.

### Cloud Services {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : Le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur de traitement des demandes des clients et de renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services d&#39;Adobe et l&#39;application mobile via le fichier ADBMobileConfig.json qui est utilisé par le plug-in Cordova AMS. A partir du Tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

Dans le Tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton +.

![chlimage_1-38](assets/chlimage_1-38.png)

Dans l’assistant Ajouter Cloud Service, sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-39](assets/chlimage_1-39.png)

Dans la liste déroulante Sélectionner une configuration, vous pouvez créer une nouvelle configuration ou en sélectionner une existante. Pour créer une nouvelle configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Entrez un titre pour la configuration de la Cible. Entrez le code client, le courrier électronique et le mot de passe associés à votre compte de Cible. Si vous ne connaissez pas les valeurs de ces champs, contactez l’assistance Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

>[!NOTE]
>
>Le service cloud qui est créé est automatiquement associé à l’application mobile via l’assistant. La valeur de propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud de groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybrid-reference-app/jcr:content avec la valeur pointant vers le noeud de structure généré automatiquement situé dans /etc/cloudservices/testandtarget/adobe-cible—aem-apps/framework. Le noeud de structure possède deux propriétés définies par défaut, le sexe et l’âge. La structure n&#39;est utilisée que par AEM prévisualisation et n&#39;a aucun impact sur le périphérique.

Une fois l’Assistant terminé, la mosaïque Gérer le Cloud Service contient le service Cloud de Cible, mais contient un avertissement concernant un compte Service mobile d’Adobe manquant.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Il est également nécessaire de lier un compte Adobe Mobile Services (AMS) à l’application. Le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations de code client de la Cible. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous sur [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l’application mobile et cliquez sur les paramètres. Recherchez le champ Options de Cible du SDK, placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-41](assets/chlimage_1-41.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le Tableau de bord Mobile Adobe, les paramètres des paramètres du service sont diffusés via le fichier ADBMobileConfig.json.

### Adobe Mobile Service Cloud Service {#adobe-mobile-service-cloud-service}

Maintenant qu’AMS a été configuré, il est temps d’associer l’application mobile au Tableau de bord mobile Adobe. Dans le Tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton +.

![chlimage_1-42](assets/chlimage_1-42.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-43](assets/chlimage_1-43.png)

A l’étape de l’Assistant Créer ou Sélectionner, sélectionnez la liste déroulante Mobile Service et sélectionnez l’entrée Créer une configuration. Indiquez un titre, une société, un nom d’utilisateur, un mot de passe et sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs remplis, cliquez sur le bouton Vérifier. Le processus de vérification est transmis à AMS et vérifie les informations d’identification du compte. Une fois la validation terminée, une liste d’applications mobiles est renseignée où vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et les analyses associées à l’application. Une fois le processus terminé, cliquez sur le bouton Terminé dans la fenêtre modale pour revenir au Tableau de bord mobile Adobe.

Revenir au Tableau de bord mobile La mosaïque Gérer les Cloud Services contient le service cloud AMS. Vous remarquerez également que le volet Analyser les mesures sera renseigné par des rapports de cycle de vie.

![chlimage_1-44](assets/chlimage_1-44.png)

## Pour les auteurs {#for-authors}

**Condition préalable :** Comme mentionné ci-dessus, les administrateurs doivent configurer la connexion au service Adobe Target pour que les auteurs puissent générer un nouveau contenu ciblé.

Une fois que l’administrateur a configuré les deux services Cloud et que le développeur a configuré le gestionnaire d’applications mobiles, les auteurs de contenu peuvent désormais début générer des expériences ciblées.

La création de contenu ciblé dans une application AEM Mobile suit une procédure similaire à la création de AEM Sites :

Voir ici pour une présentation complète de la [création de contenu ciblé dans AEM](/help/sites-authoring/personalization.md)

## Pour les développeurs {#for-developers}

Les développeurs AEM qui créent des applications mobiles doivent continuer à suivre les schémas couramment utilisés dans l’ensemble de l’AEM lors du développement de composants. Ici, nous allons vous guider à travers les étapes nécessaires pour permettre aux auteurs de contenu de créer du contenu ciblé :

### Gestionnaire de synchronisation de contenu Adobe Target {#adobe-target-contentsync-handlers}

Pour diffuser du contenu sur le périphérique de l’utilisateur, le rendu des offres créées par les auteurs de contenu AEM génère le rendu. Pour gérer le rendu des offres d’cible, il existe un nouveau gestionnaire de synchronisation de contenu qui traitera les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . L’étape suivante est cruciale pour le rendu des offres sur le périphérique. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, si une activité se trouve dans */content/campaigns/hybridref* , copiez ce chemin et collez-le en tant que valeur dans la propriété *path* du gestionnaire mobileappoffers.

>[!NOTE]
>
>Pour l’application de référence hybride, il y a deux gestionnaires mobileappoffers : un pour le développement et un pour les productions.

Une fois que le chemin d’accès aux activités a été défini dans la propriété path du gestionnaire d’applications mobiles, enregistrez le gestionnaire. Le gestionnaire sera maintenant prêt à début les offres de rendu pour nos appareils mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec une valeur de *publication* définie sur le noeud cq:ContentSyncConfig. Le gestionnaire mobileappoffers référence le renderMode et, s’il est défini sur publish, modifie l’identifiant de mbox qui est créé. Par défaut, une valeur —author est ajoutée à l’ID de mbox pour les mbox créées par AEM. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est mis en scène via le Tableau de bord mobile Adobe, le contenu intermédiaire est considéré comme du contenu prêt à l’emploi et rendu via la configuration de synchronisation du contenu non développée. Le rendu de cette manière entraînera la suppression de l’élément —author de tous les identifiants de mbox et la disponibilité d’une activité publiée sur le serveur de Cible. Avant de tester le contenu intermédiaire, vérifiez que l’activité a été publiée.

### Développement d’applications de personnalisation {#personalization-app-development}

#### Composants {#components}

La base d’un contenu est généralement un composant de page qui étend l’un des composants de page de base de l’AEM wcm/foundation/components/page ou foundation/components/page selon que vous utilisez du code HTML ou JSP. La durée de ces étapes sera axée sur l’utilisation du composant wcm/foundation/components/page. La structure de base du composant de page est divisée en plusieurs scripts, chaque script ayant pour objectif spécifique de permettre au développeur d’organiser et de remplacer son code si nécessaire. Les deux scripts présentant un intérêt pour la personnalisation sont head.html et body.html. Ces deux scripts fournissent une zone où le code peut être injecté pour prendre en charge la création Context Hub, Cloud Services et Mobile.

Voici un aperçu des deux scripts Principaux utilisés pour activer le ciblage du contenu.

#### head.html {#head-html}

Pour permettre à l’auteur de cible son contenu, le menu cible doit être ajouté à la page afin que l’auteur puisse changer le contexte du mode d’édition en mode de ciblage. Pour activer cette fonctionnalité, le développeur doit modifier le script head.html afin d’inclure le fragment de code suivant dans la partie supérieure de head.html ou aussi près que possible de l’élément &lt;title>&lt;/title>.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Notez que le script ne doit être inclus que lorsque le mode WCM n’a pas été désactivé de sorte que lorsque le mode WCM est désactivé (voir la section du gestionnaire ContentSync pour plus de détails), le script ne soit pas inclus dans le code d’application final.

Pour permettre aux auteurs de prévisualisation du contenu ciblé, l’éditeur doit être en mesure de localiser la configuration du service Adobe Target cloud. Le bloc de code ci-dessous ajoute deux scripts importants. La première consiste à ajouter la possibilité pour la page de localiser le service cloud de Cible associé et d’envoyer les appels à Adobe Target. La seconde est l’ajout de la catégorie cq.apps.targeting.

La catégorie **cq.apps.targeting** remplace le composant par défaut cq/personalization/component/cible et utilise le composant mobileapps/components/cible qui effectue le rendu des offres spécifiquement pour la consommation d’applications mobiles. Pour en savoir plus, consultez la section Composant de la Cible .

Le code doit être ajouté dans head.html et placé juste avant la fin de l’élément &lt;/head>.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Notez que le bloc de code est encapsulé dans un mode WCM n’étant pas désactivé, l’auteur du contenu ne se lance que pendant la création de contenu. Les scripts du service cloud ne seront pas ajoutés au code d’exécution mobile généré.

#### body.html {#body-html}

Pour permettre à l’auteur du contenu de tester différentes personnalités, le script body.html doit inclure le bloc de code suivant comme premier enfant de l’élément body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

Le dernier bit de code requis se trouve tout en bas de body.html. Ce bit de code recherche le service cloud associé et injecte le code de moteur de ciblage approprié.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Application de référence {#reference-application}

Vous trouverez des exemples de head.html et body.html dans l’application [de référence hybride](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile qui montre au développeur où placer les blocs de script dans les deux scripts.

### Gestionnaires de synchronisation de contenu {#content-sync-handlers}

Lorsque l’auteur du contenu a fini de créer du contenu pour l’application mobile, l’étape suivante consiste à télécharger la source et à créer l’application, ou à préparer le contenu à publier. Il y a un certain nombre d&#39;étapes dans lesquelles le développeur est impliqué pour que cela se produise. Pour faciliter le rendu du contenu, AEM Mobile utilise des gestionnaires de synchronisation de contenu pour générer et assembler le contenu. Un nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation de la personnalisation pour le rendu du contenu ciblé. Le gestionnaire &quot;mobileappoffers&quot; sait comment générer les offres d’cible associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. Par conséquent, la plupart des propriétés sont similaires. Les détails du gestionnaire mobileappoffers possèdent les propriétés suivantes.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>réécrire</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>La propriété rewrite identifie comment les chemins d’accès au contenu doivent être réécrits.</td>
  </tr>
  <tr>
   <td>includePageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>La propriété includePageTypes est facultative. Elle est utilisée par défaut pour les pages dont les types de ressources sont cq/personalization/components/teaserpage et cq/personalization/components/offerproxy. Ces deux types de ressource sont les types de ressource par défaut utilisés lorsque le contenu est ciblé. Si des types de ressources supplémentaires doivent être pris en charge, ils doivent être ajoutés à la liste de includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Emplacement de l’application.</td>
  </tr>
  <tr>
   <td>type</td>
   <td>mobileappoffers</td>
   <td>Nom du gestionnaire qui fait l’objet d’une demande de service mobile.</td>
  </tr>
  <tr>
   <td>sélecteur</td>
   <td>tandt</td>
   <td>Le sélecteur de bande est utilisé pour effectuer le rendu du contenu ciblé. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>répertoire racine dans lequel conserver le contenu rendu.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Si true, les images incluses dans l’offre sont rendues. Si de fausses images sont ignorées.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Si true, toutes les vidéos incluses dans l’offre sont rendues. Si de fausses vidéos sont ignorées.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>Indique la marque de la campagne à laquelle les offres participent. Actuellement, toutes les offres doivent provenir de la même campagne.</td>
  </tr>
  <tr>
   <td>profondeur</td>
   <td>true | false</td>
   <td>Si true effectue le rendu récursif de toutes les pages enfants, si false, ne réapparaît pas. </td>
  </tr>
  <tr>
   <td>extension</td>
   <td>html</td>
   <td>Définit l'extension de la ressource rendue. Définissez cette variable sur html de sorte que les pages aient une extension .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>L’application [de référence](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) hybride AEM Mobile possède la configuration par défaut du gestionnaire de ressources mobileappoffer. La propriété path de l’exemple est vide, car elle dépend de l’emplacement de la campagne. Une fois qu’un auteur Campaign a créé un Campaign, l’administrateur d’applications doit associer le Campaign au gestionnaire en spécifiant la propriété path pour pointer vers le Campaign.

### Composant cible {#target-component}

Pour faciliter le rendu du contenu spécifiquement pour les applications mobiles, AEM Mobile utilise le composant mobileapps/components/cible. Le composant de cible mobile étend le composant cq/personalization/components/cible et remplace le script engine_tnt.jsp. En remplaçant engine_tnt.jsp, cela permet à AEM Mobile de contrôler le code HTML généré pour le cas d’utilisation des applications mobiles. Pour chaque composant ciblé par un auteur de contenu, une mbox associée est créée par le fichier engine_tnt.jsp.

Pour chaque mbox, un attribut de ciblage **** cq est ajouté pour permettre aux développeurs d’applications d’écrire du code personnalisé à consommer et à utiliser comme bon leur semble. L’application [de référence](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) hybride AEM Mobile présente un exemple de directive angulaire qui utilise l’attribut cq-targeting. Le concept de remplacement de contenu, quand et comment il est fait, dépend en grande partie du développeur d&#39;applications mobiles. Il existe un SDK mobile fourni par AEM /etc/clientlibs/mobileapps/js/mobileapps.js qui fournit une API pour appeler le service de ciblage d’Adobe. Il appartient au développeur d’applications de spécifier quand cet appel doit être effectué en fonction de la conception de leur application.

## What&#39;s Next? {#what-s-next}

1. [Expérimenter le développement d’une application AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gérer le contenu d’une application mobile](/help/mobile/phonegap-manage-app-content.md)
1. [Développer une application mobile](/help/mobile/building-app-mobile-phonegap.md)
1. [Suivre les performances d’une application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Offrir une expérience personnalisée dans une application mobile grâce à Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Diffuser des messages importants à l’intention des utilisateurs](/help/mobile/phonegap-push-notifications.md)
