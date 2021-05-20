---
title: Configuration du Cloud Service Adobe Target
seo-title: Configuration du Cloud Service Adobe Target
description: Consultez cette page pour comprendre comment obtenir un ensemble correct d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.
seo-description: Consultez cette page pour comprendre comment obtenir un ensemble correct d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
>Ce document fait partie du guide [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md), point de départ recommandé pour la référence AEM Mobile.

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : Il existe un ensemble d’autorisations adapté aux utilisateurs et aux groupes, la création de services cloud, la configuration de l’application pour l’activité et enfin la génération du contenu.

L’hypothèse à l’avenir est que l’[application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) a été déployée avec succès et accessible via le tableau de bord AEM Mobile.

## Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors` . Dans le cadre de la configuration des utilisateurs et des groupes, il est conseillé d’ajouter le groupe target-activity-group au groupe apps-admins . En ajoutant le groupe target-activity-authors , les utilisateurs pourront voir l’entrée du menu de navigation Personnalisation.

Si vous omettez d’ajouter les utilisateurs ou les groupes auxquels vous souhaitez accéder à la console d’administration de la personnalisation au groupe target-activity-authors , les utilisateurs ne pourront pas voir la console de personnalisation.

## Cloud Services {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : Le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur pour le traitement des requêtes client et le renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json qui est utilisé par le module externe AMS Cordova. Depuis le tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton + .

![chlimage_1-8](assets/chlimage_1-8.png)

Dans l’assistant Ajouter un Cloud Service , sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-9](assets/chlimage_1-9.png)

Dans la liste déroulante Sélectionner une configuration , vous pouvez créer une configuration ou en sélectionner une existante. Pour créer une configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Saisissez un titre pour la configuration Target. Saisissez le code client, l’adresse électronique et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez le support Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

Le service cloud qui est créé est automatiquement associé à l&#39;application mobile via l&#39;assistant. La valeur de la propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud du groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybride-reference-app/jcr:content avec la valeur pointant vers le noeud de structure généré automatiquement situé à l’emplacement /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le noeud de structure possède deux propriétés définies par défaut, le genre et l’âge. La structure n’est utilisée que par AEM prévisualisation et n’a aucun impact sur l’appareil.

Une fois l’assistant terminé, la mosaïque Gérer le Cloud Service contiendra le service cloud Target, mais elle contient un avertissement concernant un compte Mobile Service Adobe manquant.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Pour lier également un compte Mobile Services (AMS) Adobe à l’application, le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations du code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous à l’adresse [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l’application mobile et cliquez sur les paramètres. Localisez le champ Options du SDK Target et placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-11](assets/chlimage_1-11.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord mobile Adobe, les paramètres des paramètres du service sont fournis via le fichier ADBMobileConfig.json .

### Adobe Mobile Service Pourrait Service {#adobe-mobile-service-could-service}

Maintenant qu’AMS a été configuré, il est temps d’associer l’application mobile dans le tableau de bord Mobile Adobe. Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Services et cliquez sur le bouton + .

![chlimage_1-12](assets/chlimage_1-12.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-13](assets/chlimage_1-13.png)

À l’étape de l’assistant Créer ou Sélectionner , sélectionnez la liste déroulante Mobile Service , puis l’entrée Créer une configuration . Indiquez un titre, une société, un nom d’utilisateur et un mot de passe, puis sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs renseignés, cliquez sur le bouton Vérifier . Le processus de vérification passe à AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste d’applications mobiles s’affiche, dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et toute analyse associée à l’application. Une fois le processus terminé, cliquez sur le bouton Terminé dans la fenêtre modale pour revenir au tableau de bord Mobile Adobe.

De retour au tableau de bord mobile, la mosaïque Gérer les Cloud Services contiendra le service cloud AMS. Vous remarquerez également que la mosaïque Analyser les mesures sera remplie avec des rapports de cycle de vie.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestionnaire de synchronisation de contenu de Target {#target-content-sync-handlers}

La diffusion du contenu sur le périphérique de l’utilisateur est générée en effectuant le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cibles, il existe un nouveau gestionnaire de synchronisation de contenu qui traitera les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . L’étape suivante est cruciale pour le rendu des offres sur l’appareil. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation à utiliser pour l’application.

Par exemple, si une activité se trouve à l’emplacement */content/campaigns/hybridref*, copiez ce chemin et collez-le en tant que valeur de la propriété *path* du gestionnaire d’offres mobiles.

Pour l’application de référence hybride, il existe deux gestionnaires mobileappoffers : un pour le développement et un autre pour les productions.

Une fois que le chemin d’accès aux activités a été défini dans la propriété path du gestionnaire mobileappoffers, enregistrez le gestionnaire. Le gestionnaire sera désormais prêt à lancer le rendu des offres pour nos appareils mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec la valeur *publish* définie sur le noeud cq:ContentSyncConfig . Le gestionnaire mobileappoffers fait référence à renderMode et, s’il est défini sur publish, modifie l’ID de mbox qui est créé. Par défaut, les mbox créées par AEM ont une valeur —author ajoutée à l’identifiant mbox. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est intermédiaire via le tableau de bord mobile Adobe, le contenu intermédiaire est considéré comme du contenu prêt pour la production et est rendu via la configuration de synchronisation de contenu non développée. Le rendu de cette manière entraînera la suppression de l’auteur —de tous les identifiants de mbox et prévoit qu’une activité publiée sera disponible sur le serveur Target. Avant de tester le contenu intermédiaire, vérifiez que l’activité a été publiée.

## Création de contenu {#creating-content}

Maintenant que les services cloud ont été créés et que le gestionnaire d’offres mobiles a été configuré, les auteurs de contenu peuvent commencer à générer des expériences ciblées.
