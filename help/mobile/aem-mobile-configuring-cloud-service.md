---
title: Configuration du service Adobe Target Cloud
seo-title: Configuration du service Adobe Target Cloud
description: Suivez cette page pour comprendre comment obtenir le bon jeu d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et générer le contenu.
seo-description: Suivez cette page pour comprendre comment obtenir le bon jeu d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et générer le contenu.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration du service Adobe Target Cloud {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>This document is part of the [Getting Started with AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, a recommended starting point for AEM Mobile reference.

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : Il obtient le bon jeu d’autorisations pour les utilisateurs et les groupes, crée des services cloud, configure l’application pour l’activité et génère enfin le contenu.

L&#39;hypothèse suivante est que l&#39;application [de référence hybride](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile a été correctement déployée et accessible via le tableau de bord AEM Mobile.

## Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du `target-activity-authors` groupe. Il est conseillé, dans le cadre de la configuration des utilisateurs et des groupes, d’ajouter le groupe target-activity-group au groupe apps-admins. L’ajout du groupe target-activity-authors permet aux utilisateurs de voir l’entrée du menu de navigation Personnalisation.

Si vous oubliez d’ajouter les utilisateurs ou les groupes que vous souhaitez avoir accès à la console d’administration de la personnalisation au groupe target-activity-authors, les utilisateurs ne pourront pas voir la console de personnalisation.

## Services cloud {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : Le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur de traitement des demandes client et de renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json, qui est utilisé par le plug-in Cordova AMS. Le tableau de bord AEM Mobile vous permet de configurer votre application en ajoutant les deux services.

## Service Adobe Target Cloud {#adobe-target-cloud-service}

Dans le tableau de bord AEM Mobile, recherchez la section Gérer les services Cloud et cliquez sur le bouton +.

![chlimage_1-8](assets/chlimage_1-8.png)

Dans l’assistant d’ajout de services cloud, sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-9](assets/chlimage_1-9.png)

Dans la liste déroulante Sélectionner une configuration, vous pouvez créer une nouvelle configuration ou sélectionner une configuration existante. Pour créer une nouvelle configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Entrez un titre pour la configuration de Target. Entrez le code client, le courrier électronique et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez le support technique d’Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

Le service cloud qui est créé est automatiquement associé à l’application mobile via l’assistant. La valeur de propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud de groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybrid-reference-app/jcr:content avec la valeur pointant vers le noeud de structure généré automatiquement situé dans /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le noeud framework possède deux propriétés définies par défaut, le sexe et l’âge. La structure est utilisée uniquement par la prévisualisation AEM et n’a aucun impact sur le périphérique.

Une fois l’assistant terminé, le volet Gérer le service Cloud contient le service cloud Target. Toutefois, il contient un avertissement concernant un compte Adobe Mobile Service manquant.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Il est également nécessaire de lier un compte Adobe Mobile Services (AMS) à l’application. Le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations de code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous sur [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l’application mobile et cliquez sur les paramètres. Recherchez le champ Options de cible du SDK, placez le code client dans le champ et cliquez sur Enregistrer.

![chlimage_1-11](assets/chlimage_1-11.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord Adobe Mobile, les paramètres du service sont diffusés via le fichier ADBMobileConfig.json.

### Adobe Mobile Service Pourrait Service {#adobe-mobile-service-could-service}

Maintenant qu’AMS a été configuré, il est temps d’associer l’application mobile au tableau de bord Adobe Mobile. Dans le tableau de bord AEM Mobile, recherchez la section Gérer les services Cloud et cliquez sur le bouton +.

![chlimage_1-12](assets/chlimage_1-12.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-13](assets/chlimage_1-13.png)

A l’étape de l’assistant Créer ou Sélectionner, sélectionnez la liste déroulante Service mobile et sélectionnez l’entrée Créer une configuration. Indiquez un titre, une société, un nom d’utilisateur, un mot de passe et sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs remplis, cliquez sur le bouton Vérifier. Le processus de vérification s’adresse à AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste des applications mobiles est renseignée dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et les analyses associées à l’application. Une fois le processus terminé, cliquez sur le bouton Terminé du mode modal pour revenir au tableau de bord Adobe Mobile.

Revenir au tableau de bord Mobile La mosaïque Gérer les services Cloud contient le service cloud AMS. Vous noterez également que le volet Analyser les mesures sera rempli de rapports de cycle de vie.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestionnaire de synchronisation de contenu Target {#target-content-sync-handlers}

La diffusion de contenu sur le contenu du périphérique de l’utilisateur est générée par le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cible, il existe un nouveau gestionnaire de synchronisation du contenu qui traitera les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . L’étape suivante est cruciale pour le rendu des offres sur le périphérique. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, si une activité se trouve dans */content/campaigns/hybridref* , copiez ce chemin et collez-le comme valeur dans la propriété *path* du gestionnaire mobileappoffers.

Pour l’application de référence hybride, il existe deux gestionnaires mobileappoffers : un pour le développement et un pour les productions.

Une fois que le chemin d’accès aux activités a été défini dans la propriété path du gestionnaire mobileapffers, enregistrez le gestionnaire. Le gestionnaire sera maintenant prêt à commencer à générer des offres pour nos périphériques mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec la valeur de *publish* définie sur le noeud cq:ContentSyncConfig. Le gestionnaire mobileappoffers fait référence à renderMode et, s’il est défini pour la publication, modifie l’ID de mbox qui est créé. Par défaut, une valeur —author est ajoutée à l’ID de mbox pour les mbox créées par AEM. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est mis en scène via Adobe Mobile Dashboard, le contenu mis en scène est considéré comme du contenu prêt à l’emploi et rendu via la configuration de synchronisation de contenu non développée. Le rendu de cette manière entraînera la suppression de l’auteur —author de tous les ID de mbox et prévoit qu’une activité publiée sera disponible sur le serveur Target. Avant de tester le contenu intermédiaire, vérifiez que l’activité a été publiée.

## Création de contenu {#creating-content}

Maintenant que les services cloud ont été créés et que le gestionnaire mobileappoffers a été configuré, les auteurs de contenu peuvent commencer à générer des expériences ciblées.
