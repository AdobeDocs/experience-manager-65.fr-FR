---
title: Configuration du Cloud Service Adobe Target
description: Consultez cette page pour comprendre comment obtenir un ensemble correct d’autorisations pour les utilisateurs et les groupes, créer des services cloud, configurer l’application pour l’activité et enfin générer le contenu.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 3%

---

# Configuration du Cloud Service Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Ce document fait partie du guide [Prise en main de Adobe Experience Manager (AEM) Mobile](/help/mobile/getting-started-aem-mobile.md), un point de départ recommandé pour la référence AEM Mobile.

Plusieurs étapes doivent être réunies pour que les auteurs de contenu puissent commencer à générer du contenu ciblé pour les applications mobiles : il existe un ensemble approprié d’autorisations pour les utilisateurs et les groupes, la création de services cloud, la configuration de l’application pour l’activité et enfin la génération du contenu.

L’hypothèse à l’avenir est que l’[ application de référence hybride AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) a été déployée avec succès et accessible par le biais du tableau de bord AEM Mobile.

## Autorisations {#permissions}

Les utilisateurs qui doivent accéder à la console de personnalisation doivent faire partie du groupe `target-activity-authors`. Dans le cadre de la configuration des utilisateurs et des groupes, il est conseillé d’ajouter le groupe target-activity-group au groupe apps-admins . En ajoutant le groupe target-activity-authors, les utilisateurs peuvent ainsi voir l’entrée du menu de navigation de Personalization.

L’oubli de l’ajout des utilisateurs ou des groupes auxquels vous souhaitez accéder à l’Admin Console de personnalisation au groupe target-activity-authors empêche les utilisateurs de voir la console de personnalisation.

## Services cloud {#cloud-services}

Pour que le contenu ciblé fonctionne pour les applications mobiles, deux services doivent être configurés : le service Adobe Target et le service Adobe Mobile Services. Le service Adobe Target fournit le moteur pour le traitement des requêtes client et le renvoi du contenu personnalisé. Le service Adobe Mobile Services fournit la connexion entre les services Adobe et l’application mobile via le fichier ADBMobileConfig.json qui est utilisé par le module externe AMS Cordova. Depuis le tableau de bord AEM Mobile, vous pouvez configurer votre application en ajoutant les deux services.

## Adobe Target Cloud Service {#adobe-target-cloud-service}

Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-8](assets/chlimage_1-8.png)

Dans l’assistant Ajouter un Cloud Service, sélectionnez la carte de service cloud &quot;Adobe Target&quot; et cliquez sur Suivant.

![chlimage_1-9](assets/chlimage_1-9.png)

Dans la liste déroulante Sélectionner une configuration , vous pouvez créer une configuration ou en sélectionner une existante. Pour créer une configuration, sélectionnez &quot;Créer une configuration&quot; dans la liste déroulante. Saisissez un titre pour la configuration Target. Saisissez le code client, l’adresse électronique et le mot de passe associés à votre compte Target. Si vous ne connaissez pas les valeurs de ces champs, contactez le support Adobe Target. Cliquez sur le bouton &quot;Vérifier&quot; pour valider les identifiants. Une fois la vérification effectuée, cliquez sur le bouton Envoyer pour créer le service cloud.

Le service cloud qui est créé est automatiquement associé à l&#39;application mobile via l&#39;assistant. La valeur de la propriété cq:cloudserviceconfigs est définie sur le noeud jcr:content du noeud du groupe d’applications. Pour l’exemple d’application hybride, il est défini sur /content/mobileapps/hybride-reference-app/jcr:content , la valeur pointant vers le noeud de structure généré automatiquement se trouvant dans /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Le noeud de structure possède deux propriétés définies par défaut, le genre et l’âge. La structure n’est utilisée que par AEM prévisualisation et n’a aucun impact sur l’appareil.

Une fois l’assistant terminé, la mosaïque Gérer le Cloud Service contient le service cloud Target, mais elle contient un avertissement concernant un compte Mobile Service Adobe manquant.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Pour lier également un compte Mobile Services (AMS) Adobe à l’application, le service AMS fournit le fichier ADBMobileConfig.json requis qui contient les informations du code client Target. Avant de créer une association avec le compte AMS, le compte AMS doit être modifié par un utilisateur disposant d’autorisations sur AMS.

### Code client {#client-code}

Pour vous connecter aux services AMS, rendez-vous à l&#39;adresse [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), sélectionnez l&#39;application mobile et cliquez sur les paramètres. Localisez le champ Options du SDK Target et placez le code client dans le champ, puis cliquez sur Enregistrer.

![chlimage_1-11](assets/chlimage_1-11.png)

Maintenant que le code client a été associé à l’application mobile, lorsque le service cloud AMS est configuré via le tableau de bord mobile Adobe, les paramètres des paramètres du service sont fournis via le fichier ADBMobileConfig.json .

### Service Adobe Mobile Service Pourrait {#adobe-mobile-service-could-service}

Maintenant qu’AMS est configuré, il est temps d’associer l’application mobile dans le tableau de bord Mobile Adobe. Dans le tableau de bord AEM Mobile, recherchez l’option Gérer les Cloud Service et cliquez sur le bouton + .

![chlimage_1-12](assets/chlimage_1-12.png)

Sélectionnez la carte Adobe Mobile Services et cliquez sur Suivant.

![chlimage_1-13](assets/chlimage_1-13.png)

À l’étape de l’assistant Créer ou Sélectionner , sélectionnez la liste déroulante Mobile Service , puis l’entrée Créer une configuration . Indiquez un titre, une société, un nom d’utilisateur et un mot de passe, puis sélectionnez le centre de données approprié. Si vous ne connaissez pas ces valeurs, contactez votre administrateur Adobe Mobile Service pour les obtenir. Une fois tous les champs renseignés, cliquez sur **Vérifier**. Le processus de vérification passe à AMS et vérifie les informations d’identification du compte. Une fois la validation réussie, une liste d’applications mobiles s’affiche, dans laquelle vous sélectionnez l’application mobile associée dans la liste déroulante. Cliquez sur le bouton Envoyer pour terminer l’assistant. Le processus peut prendre un certain temps pour obtenir les données de configuration et toute analyse associée à l’application. Une fois le processus terminé, cliquez sur **Terminé** dans la fenêtre modale pour revenir au tableau de bord mobile Adobe.

Pour revenir au tableau de bord mobile, la mosaïque Gérer les Cloud Service contient le service cloud AMS. En outre, la mosaïque Analyser les mesures est remplie avec des rapports de cycle de vie.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestionnaires de synchronisation de contenu de Target {#target-content-sync-handlers}

Pour diffuser du contenu sur l’appareil de l’utilisateur, le contenu est généré par le rendu des offres créées par les auteurs de contenu AEM. Pour gérer le rendu des offres cibles, il existe un nouveau gestionnaire de synchronisation de contenu qui traite les offres. En utilisant l’application de référence hybride comme exemple, le module de contenu en (anglais) contient ContentSyncConfig avec un gestionnaire [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . L’étape suivante est cruciale pour le rendu des offres sur l’appareil. Le gestionnaire mobileappoffers possède une propriété path qui identifie le chemin d’accès à l’activité de personnalisation utilisée pour l’application.

Par exemple, si une activité se trouve à l’emplacement */content/campaigns/hybridref*, copiez ce chemin et collez-le en tant que valeur de la propriété *path* du gestionnaire mobileappoffers.

Pour l’application de référence hybride, il existe deux gestionnaires mobileappoffers : un pour le développement et un autre pour les productions.

Une fois le chemin d’accès aux activités défini dans la propriété path du gestionnaire mobileappoffers, enregistrez le gestionnaire. Le gestionnaire est maintenant prêt à lancer le rendu des offres pour les périphériques mobiles.

### Mode de rendu {#render-mode}

Le gestionnaire de ressources mobiles est configuré différemment pour les configurations de publication et de développement. Pour les configurations de publication, il existe une propriété appelée *renderMode* avec une valeur *publish* définie sur le noeud cq:ContentSyncConfig . Le gestionnaire mobileappoffers fait référence à renderMode et, s’il est défini sur publish, modifie l’ID de mbox qui est créé. Par défaut, les mbox créées par AEM ont une valeur —author ajoutée à l’identifiant mbox. Ceci identifie que l’activité n’a pas été publiée et doit utiliser la campagne non publiée pour les résolutions d’offre.

Lorsque le contenu est intermédiaire via le tableau de bord mobile Adobe, le contenu intermédiaire est considéré comme du contenu prêt pour la production et est rendu via la configuration de synchronisation de contenu non développée. Le rendu de cette manière entraîne la suppression de —author de tous les identifiants mbox et prévoit qu’une activité publiée soit disponible sur le serveur Target. Avant de tester le contenu intermédiaire, vérifiez que l’activité est publiée.

## Création de contenu {#creating-content}

Maintenant que les services cloud ont été créés et que le gestionnaire d’offres mobiles a été configuré, les auteurs de contenu peuvent commencer à générer des expériences ciblées.
