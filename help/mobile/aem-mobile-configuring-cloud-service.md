---
title: Configuration de l’Cloud Service Adobe Target
seo-title: Configuration de l’Cloud Service Adobe Target
description: Suivez cette page pour comprendre comment obtenir le bon ensemble d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et générer enfin le contenu.
seo-description: Suivez cette page pour comprendre comment obtenir le bon ensemble d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et générer enfin le contenu.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 2%

---


# Configuration du Cloud Service Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Ce document fait partie du [Guide de prise en main de AEM Mobile](/help/mobile/getting-started-aem-mobile.md), point de départ recommandé pour la référence à AEM Mobile.

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent début de générer du contenu ciblé pour les applications mobiles : Il existe un jeu d’autorisations approprié pour les utilisateurs et les groupes, la création de services cloud, la configuration de l’application pour l’activité et enfin la génération du contenu.

L&#39;hypothèse suivante est que l&#39;application de référence hybride [AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) a été déployée avec succès et accessible via le Tableau de bord AEM Mobile.

## Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors`. Il est conseillé, dans le cadre de la configuration des utilisateurs et des groupes, d’ajouter le groupe d’activités-cibles au groupe d’administrateurs d’applications. En ajoutant le groupe cible-activités-auteurs, cela permet aux utilisateurs de voir l’entrée du menu de navigation Personnalisation.

Si vous oubliez d’ajouter les utilisateurs ou les groupes auxquels vous souhaitez avoir accès à la console d’administration de la personnalisation au groupe d’auteurs d’activités-cibles, les utilisateurs ne pourront pas voir la console de personnalisation.

## Cloud Services {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : Le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur de traitement des demandes des clients et de renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services d&#39;Adobe et l&#39;application mobile via le fichier ADBMobileConfig.json qui est utilisé par le plug-in Cordova AMS. A partir du Tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

Dans le Tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton +.

![chlimage_1-8](assets/chlimage_1-8.png)

Dans l’assistant Ajouter Cloud Service, sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-9](assets/chlimage_1-9.png)

Dans la liste déroulante Sélectionner une configuration, vous pouvez créer une nouvelle configuration ou en sélectionner une existante. Pour créer une nouvelle configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Entrez un titre pour la configuration de la Cible. Entrez le code client, le courrier électronique et le mot de passe associés à votre compte de Cible. Si vous ne connaissez pas les valeurs de ces champs, contactez l’assistance Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

Le service cloud qui est créé est automatiquement associé à l’application mobile via l’assistant. La valeur de propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud de groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybrid-reference-app/jcr:content avec la valeur pointant vers le noeud de structure généré automatiquement situé dans /etc/cloudservices/testandtarget/adobe-cible—aem-apps/framework. Le noeud de structure possède deux propriétés définies par défaut, le sexe et l’âge. La structure n&#39;est utilisée que par AEM prévisualisation et n&#39;a aucun impact sur le périphérique.

Une fois l’Assistant terminé, la mosaïque Gérer le Cloud Service contient le service Cloud de Cible, mais contient un avertissement concernant un compte Service mobile d’Adobe manquant.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Il est également nécessaire de lier un compte Adobe Mobile Services (AMS) à l’application. Le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations de code client de la Cible. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, visitez [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l’application mobile et cliquez sur les paramètres. Recherchez le champ Options de Cible du SDK, placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-11](assets/chlimage_1-11.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le Tableau de bord Mobile Adobe, les paramètres des paramètres du service sont diffusés via le fichier ADBMobileConfig.json.

### Adobe Mobile Service Pourrait Service {#adobe-mobile-service-could-service}

Maintenant qu’AMS a été configuré, il est temps d’associer l’application mobile au Tableau de bord mobile Adobe. Dans le Tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton +.

![chlimage_1-12](assets/chlimage_1-12.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-13](assets/chlimage_1-13.png)

A l’étape de l’Assistant Créer ou Sélectionner, sélectionnez la liste déroulante Mobile Service et sélectionnez l’entrée Créer une configuration. Indiquez un titre, une société, un nom d’utilisateur, un mot de passe et sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs remplis, cliquez sur le bouton Vérifier. Le processus de vérification est transmis à AMS et vérifie les informations d’identification du compte. Une fois la validation terminée, une liste d’applications mobiles est renseignée où vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et les analyses associées à l’application. Une fois le processus terminé, cliquez sur le bouton Terminé dans la fenêtre modale pour revenir au Tableau de bord mobile Adobe.

Revenir au Tableau de bord mobile La mosaïque Gérer les Cloud Services contient le service cloud AMS. Vous remarquerez également que le volet Analyser les mesures sera renseigné par des rapports de cycle de vie.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestionnaire de synchronisation du contenu de la cible {#target-content-sync-handlers}

Pour diffuser du contenu sur le périphérique de l’utilisateur, le rendu des offres créées par les auteurs de contenu AEM génère le rendu. Pour gérer le rendu des offres d’cible, il existe un nouveau gestionnaire de synchronisation de contenu qui traitera les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). L’étape suivante est cruciale pour le rendu des offres sur le périphérique. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, si une activité se trouve à l’emplacement */content/campaigns/hybridref*, copiez ce chemin d’accès et collez-le en tant que valeur dans la propriété *path* du gestionnaire d’applications mobiles.

Pour l’application de référence hybride, il y a deux gestionnaires mobileappoffers : un pour le développement et un pour les productions.

Une fois que le chemin d’accès aux activités a été défini dans la propriété path du gestionnaire d’applications mobiles, enregistrez le gestionnaire. Le gestionnaire sera maintenant prêt à début les offres de rendu pour nos appareils mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec la valeur *publish* définie sur le noeud cq:ContentSyncConfig. Le gestionnaire mobileappoffers référence le renderMode et, s’il est défini sur publish, modifie l’identifiant de mbox qui est créé. Par défaut, une valeur —author est ajoutée à l’ID de mbox pour les mbox créées par AEM. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est mis en scène via le Tableau de bord mobile Adobe, le contenu intermédiaire est considéré comme du contenu prêt à l’emploi et rendu via la configuration de synchronisation du contenu non développée. Le rendu de cette manière entraînera la suppression de l’élément —author de tous les identifiants de mbox et la disponibilité d’une activité publiée sur le serveur de Cible. Avant de tester le contenu intermédiaire, vérifiez que l’activité a été publiée.

## Création de contenu {#creating-content}

Maintenant que les services Cloud ont été créés et que le gestionnaire d’applications mobiles a été configuré, les auteurs de contenu peuvent désormais début générer des expériences ciblées.
