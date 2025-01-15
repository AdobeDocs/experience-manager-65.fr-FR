---
title: Configuration d’Adobe Target Cloud Service
description: Consultez cette page pour découvrir comment obtenir un jeu d’autorisations approprié pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Configuration d’Adobe Target Cloud Service {#configuring-adobe-target-cloud-service}

{{ue-over-mobile}}

>[!NOTE]
>
>Ce document fait partie du guide [Prise en main de Adobe Experience Manager (AEM) Mobile](/help/mobile/getting-started-aem-mobile.md), un point de départ recommandé pour la référence à AEM Mobile.

Plusieurs étapes doivent être franchies avant que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : il faut obtenir l’ensemble approprié d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.

À l’avenir, nous partons du principe que l’[application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) a été déployée avec succès et accessible au moyen du tableau de bord AEM Mobile.

## Autorisations {#permissions}

Les utilisateurs et utilisatrices qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors`. Il est suggéré que, dans le cadre de la configuration des utilisateurs et des groupes, le groupe target-activity-group soit ajouté au groupe apps-admins. L’ajout du groupe target-activity-authors permet aux utilisateurs de voir l’entrée du menu de navigation de Personalization.

L’oubli de l’ajout des utilisateurs ou des groupes auxquels vous souhaitez accorder l’accès à l’Admin Console de personnalisation au groupe target-activity-authors empêche les utilisateurs de voir la console de personnalisation.

## Services cloud {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur permettant de traiter les requêtes des clients et de renvoyer le contenu personnalisé. Le service Adobe Mobile Services assure la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json qui est utilisé par le plug-in AMS Cordova. Depuis le tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

## Adobe Target Cloud Service {#adobe-target-cloud-service}

Dans le tableau de bord AEM Mobile, recherchez Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-8](assets/chlimage_1-8.png)

Dans l’assistant Ajouter un Cloud Service , sélectionnez la carte de service cloud « Adobe Target », puis cliquez sur Suivant.

![chlimage_1-9](assets/chlimage_1-9.png)

Dans la liste déroulante Sélectionner une configuration , vous pouvez créer une configuration ou en sélectionner une existante. Pour créer une configuration, sélectionnez Créer une configuration dans la liste déroulante. Saisissez un titre pour la configuration Target. Saisissez le code client, l’adresse e-mail et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez l’assistance technique d’Adobe Target. Cliquez sur le bouton « Vérifier » pour valider les informations d’identification. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

Le service cloud qui est créé est automatiquement associé à l’application mobile via l’assistant. La valeur de la propriété cq:cloudserviceconfigs est définie sur le nœud jcr:content du nœud du groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybride-reference-app/jcr:content avec la valeur pointant vers le nœud de framework généré automatiquement qui se trouve dans /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le nœud de framework possède deux propriétés définies par défaut : le genre et l’âge. Le framework est uniquement utilisé par la prévisualisation AEM et n’a aucun impact sur l’appareil.

Une fois l’assistant terminé, la mosaïque Gérer le Cloud Service contient le service cloud Target, mais elle contient un avertissement concernant un compte Adobe Mobile Service manquant.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Il est également nécessaire de lier un compte AMS (Adobe Mobile Services) à l’application. Le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations de code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous sur [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l&#39;application mobile, puis cliquez sur les paramètres. Recherchez le champ Options de SDK Target et placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-11](assets/chlimage_1-11.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord mobile d’Adobe, les paramètres des paramètres du service seront diffusés via le fichier ADBMobileConfig.json.

### Adobe Mobile Service Pourrait Servir {#adobe-mobile-service-could-service}

Maintenant qu’AMS est configuré, il est temps d’associer l’application mobile dans le tableau de bord mobile d’Adobe. Dans le tableau de bord AEM Mobile, recherchez Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-12](assets/chlimage_1-12.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-13](assets/chlimage_1-13.png)

À l’étape de l’assistant Créer ou Sélectionner , sélectionnez le menu déroulant Service mobile et sélectionnez l’entrée Créer une configuration . Indiquez un titre, une société, un nom d’utilisateur et un mot de passe, puis sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs remplis, cliquez sur **Vérifier**. Le processus de vérification va dans AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste d’applications mobiles est renseignée dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et toute analyse associée à l’application. Une fois le processus terminé, cliquez sur **Terminé** dans la boîte de dialogue modale pour revenir au tableau de bord mobile d’Adobe.

Pour revenir au tableau de bord mobile, la mosaïque Gérer les Cloud Service contient le service cloud AMS. En outre, la mosaïque Analyser les mesures est remplie de rapports de cycle de vie.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestionnaires de synchronisation de contenu Target {#target-content-sync-handlers}

Pour diffuser du contenu sur l’appareil de l’utilisateur, le contenu est généré en effectuant le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cibles, un nouveau gestionnaire de synchronisation de contenu traite les offres. En utilisant l’application de référence hybride comme exemple, le package de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). L’étape suivante est cruciale pour le rendu des offres sur l’appareil. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation utilisée pour l’application.

Par exemple, s’il existe une activité sous */content/campaigns/hybridref*, copiez ce chemin et collez-le en tant que valeur dans la propriété *path* du gestionnaire mobileappoffers.

Pour l’application de référence hybride, il existe deux gestionnaires d’offres mobiles, l’un pour le développement et l’autre pour les productions.

Une fois que le chemin d’accès des activités est défini dans la propriété de chemin du gestionnaire mobileappoffers, enregistrez le gestionnaire. Le gestionnaire est maintenant prêt à commencer le rendu des offres pour les appareils mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire mobileappoffers est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec une valeur de *publish* définie sur le nœud cq:ContentSyncConfig. Le gestionnaire mobileappoffers référence renderMode et, s’il est défini sur publish, modifie l’identifiant de mbox qui est créé. Par défaut, les mbox créées par AEM sont dotées de la valeur —author ajoutée à l’identifiant de mbox. Cela identifie que l&#39;activité n&#39;a pas été publiée et doit utiliser la campagne dépubliée pour les résolutions d&#39;offre.

Lorsque le contenu est évalué via le tableau de bord mobile d’Adobe, le contenu évalué est considéré comme du contenu prêt pour la production et est rendu via la configuration de synchronisation de contenu hors développement. Avec ce rendu, —author est supprimé de tous les identifiants de mbox et une activité publiée est disponible sur le serveur Target. Avant de tester le contenu évalué, assurez-vous que l’activité est publiée.

## Création de contenu {#creating-content}

Maintenant que les services cloud ont été créés et que le gestionnaire d’offres mobiles a été configuré, les auteurs de contenu peuvent commencer à générer des expériences ciblées.
