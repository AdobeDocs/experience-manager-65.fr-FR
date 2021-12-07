---
title: Configuration de Experience Manager Assets pour Adobe Asset Link
description: Configurez Experience Manager Assets à utiliser avec l’extension Adobe Asset Link pour les applications Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
source-git-commit: e91fa04d87c7ecacf3ad8a148227948eafe15b1e
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 5%

---


# Configuration de Experience Manager Assets pour Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/fr/creativecloud/business/enterprise/adobe-asset-link.html) simplifie la collaboration entre les créatifs et les marketeurs dans le processus de création de contenu. Il connecte Adobe Experience Manager Assets aux applications de bureau Creative Cloud Adobe InDesign, Adobe Photoshop et Adobe Illustrator. Le panneau Adobe Asset Link permet aux créatifs d’accéder au contenu stocké dans AEM Assets et de le modifier sans quitter les applications de création qui leur sont les plus familières.

Pour configurer Experience Manager Assets à utiliser avec Asset Link, implémentez les tâches suivantes. Utilisez le compte administrateur de Experience Manager pour effectuer la configuration :

1. Installez les modules selon les besoins. Les détails se trouvent dans [conditions préalables](#prerequisites).

1. Configurez Experience Manager [manuellement](#manual-configuration) ou en utilisant un [package](#configure-using-package).

1. Pour mapper des utilisateurs sous licence de Creative Cloud à des utilisateurs de Experience Manager, gérez [contrôle d’accès utilisateur](#user-access).

1. Créer [index de requête personnalisé](#create-custom-index), configurez [Rendus FPO](/help/assets/configure-fpo-renditions.md) pour InDesign, configurez [Intégration d’Adobe Stock](/help/assets/aem-assets-adobe-stock.md)et configurez [recherche visuelle ou par analogie](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Conditions préalables et prise en charge de différentes fonctionnalités {#prerequisites}

Assurez-vous d’installer le Service Pack et le package appropriés si nécessaire. Voir les conditions requises suivantes pour chaque version de Experience Manager et pour connaître les fonctionnalités spécifiques.

| Fonctionnalité Ressources | Version du Experience Manager et configuration requise pour la prise en charge |
|--- |--- |
| Asset Link fonctionne par défaut. | Experience Manager 6.5 et 6.5.2 ou version ultérieure. </br> Experience Manager 6.4.4 et 6.4.6 ou version ultérieure. </br> Adobe recommande d’installer la dernière version [Service Pack Experience Manager (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) avant d’utiliser AAL. |
| Asset Link fonctionne après l’installation d’un module | Pour Experience Manager 6.4.0 - 6.4.3, installez . [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) module. |
| Intégration d’Adobe Stock | Experience Manager 6.4.2 ou version ultérieure |
| Recherche visuelle ou par analogie | Experience Manager 6.5.0 ou version ultérieure |


## Configuration de Experience Manager à l’aide du package de configuration {#configure-using-package}

Adobe recommande d’installer [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) package de configuration pour automatiser la plupart des tâches de configuration, suivi de quelques tâches manuelles. Vous pouvez également [configurer manuellement](#manual-configuration).

>[!CAUTION]
>
>Si votre instance de Experience Manager est configurée pour la connexion utilisateur avec des comptes Adobe IMS, n’utilisez pas le package de configuration. Au lieu de cela, [configuration manuelle](#manual-configuration) votre instance de Experience Manager.

1. Pour ouvrir Package Manager, dans l’interface web de Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Partage de modules]**. Installer `adobe-asset-link-config` module.

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**. Localiser **[!UICONTROL Adobe du fournisseur IMS OAuth Granite]** et cliquez pour la modifier.

   Définissez les propriétés suivantes et enregistrez les modifications.

   * [!UICONTROL Mappages de groupe]: Laissez vide, sauf si vous le souhaitez. Pour plus d’informations, voir [Mappage de groupe](#group-mapping).
   * [!UICONTROL Organisation]: Saisissez l’ID d’organisation que vous utilisez dans Adobe Admin Console. Pour plus d’informations sur les ID d’organisation, voir [Création d’un groupe d’utilisateurs](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. Localiser **[!UICONTROL Gestionnaire d’authentification du porteur Adobe Granite]** et cliquez pour la modifier.

   Ajouter **[!UICONTROL InDesignAem2]** Les identifiants du client pour la variable **[!UICONTROL ID de client OAuth autorisés]** configuration .


## Configuration manuelle du Experience Manager {#manual-configuration}

Configurez manuellement Experience Manager si vous choisissez de ne pas utiliser de package de configuration ou si votre déploiement de Experience Manager est configuré pour prendre en charge la connexion utilisateur avec des comptes Adobe IMS.

Pour configurer manuellement Experience Manager :

1. Pour accéder à Configuration Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**. Sélectionner **[!UICONTROL OSGi]** > **[!UICONTROL Configuration]** dans le menu supérieur.

1. Recherchez la variable **[!UICONTROL Adobe du fournisseur IMS OAuth Granite]** et cliquez pour la modifier.

   Définissez la configuration suivante, puis cliquez sur **[!UICONTROL Enregistrer]**.

   * [!UICONTROL Point de terminaison d’autorisation]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Point de terminaison du jeton]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Point de terminaison de profil]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL de validation]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organisation]: Défini sur l’ID d’organisation dans la variable [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Mappages de groupe]: Laissez vide, sauf si vous avez une casse spéciale. Pour plus d’informations, voir [Mappage de groupe](#group-mapping).

1. Localiser **[!UICONTROL Gestionnaire d’authentification du porteur Adobe Granite]** et cliquez pour la modifier.

   Ajoutez les ID client suivants au **[!UICONTROL ID de client OAuth autorisés]** propriété de configuration : `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Pour ajouter chaque `Client ID`, cliquez sur `+`. Cliquez sur **[!UICONTROL Enregistrer]** après l’ajout de tous les identifiants.

1. Dans **[!UICONTROL Adobe de l’application OAuth Granite et du fournisseur]** , inspecter les **[!UICONTROL Gestionnaire d’authentification OAuth Adobe]** instances. Si vous localisez une instance avec l’événement `Config ID` valeur de `ims`, utilisez-le pour les instructions de cette procédure. Sinon, cliquez sur `+` pour créer une instance de configuration. Définissez les valeurs de propriété suivantes, puis cliquez sur **[!UICONTROL Enregistrer]**.

   * [!UICONTROL ID client]: Ne pas modifier
   * [!UICONTROL Secret du client]: Ne pas modifier
   * [!UICONTROL ID de configuration]: ` ims`
   * [!UICONTROL Portée]: `AdobeID, OpenID, read_organizations` (d’autres valeurs peuvent également se trouver dans la configuration)
   * [!UICONTROL Identifiant du fournisseur]: ` ims`
   * [!UICONTROL Création d’utilisateurs]: ` Checked`
   * [!UICONTROL Propriété de l’ID utilisateur]: `Email` pour la configuration nouvellement créée. Sinon, ne modifiez pas.

1. Recherchez la variable **[!UICONTROL Gestionnaire de synchronisation par défaut Apache Jackrabbit Oak]** avec la méthode **[!UICONTROL Nom du gestionnaire de synchronisation]** `ims` et cliquez pour le modifier.

   Définissez les propriétés de configuration suivantes, puis cliquez sur **[!UICONTROL Enregistrer]**.

   * [!UICONTROL Délai d’expiration de l’utilisateur et expiration de l’appartenance de l’utilisateur]: Temps en minutes suivant &quot;m&quot; sans espace. Par exemple : `15m` pendant 15 minutes. Pour plus d’informations, voir [Mappage de groupe](#group-mapping).
   * [!UICONTROL Abonnement automatique des utilisateurs]: Ne pas modifier
   * [!UICONTROL Appartenance dynamique de l’utilisateur]: ` Deslect`

1. Recherchez la variable **[!UICONTROL Gestionnaire d’authentification OAuth Adobe]** et cliquez pour la modifier. Sans apporter de modifications, cliquez sur **[!UICONTROL Enregistrer]**.

1. Pour ajuster la priorité relative du gestionnaire d’authentification du porteur, dans CRXDE, accédez à `/apps/system/config`. Localiser `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` et ouvrez sa configuration. À la fin, ajoutez `service.ranking=I"-10"`. Enregistrez les modifications.

   >[!NOTE]
   >
   >Chaque requête authentifiée avec un jeton porteur entraîne la surcharge de trois appels à Adobe IMS, la synchronisation des utilisateurs et la création d’un jeton de connexion dans Experience Manager. Pour surmonter cette surcharge, Adobe Asset Link capture le jeton de connexion renvoyé dans la réponse de Experience Manager et l’envoie avec les requêtes suivantes. Pour que ce processus fonctionne, la priorité relative du gestionnaire d’authentification du porteur doit être ajustée.

1. (Facultatif) Si les utilisateurs du Experience Manager ont des noms de domaine en majuscules ou en minuscules dans leurs ID de courrier électronique, sélectionnez **[!UICONTROL Modification de la casse d’un utilisateur verrouillé]** in **[!UICONTROL Adobe les configurations de la plateforme ACP Granite]** dans la console web de Experience Manager.

## Configuration supplémentaire après la migration vers les profils professionnels {#configure-migration-activity}

Les utilisateurs d’Adobe Asset Link peuvent se connecter à Experience Manager pour autoriser la connexion IMS à partir de l’organisation principale de Creative Cloud pour entreprise (CCE). Experience Manager utilise les ID client pour identifier l’organisation IMS autorisée. Après la migration vers les profils professionnels, il est nécessaire de configurer l’identifiant du client et la clé secrète pour l’organisation IMS en Experience Manager pour le gestionnaire d’authentification du porteur. Pour plus d’informations sur les profils professionnels, voir [introduction des profils d’Adobe](https://helpx.adobe.com/fr/enterprise/kb/introducing-adobe-profiles.html).

Une configuration supplémentaire n’est requise que si vous utilisez différentes organisations Adobe IMS pour Experience Manager et Creative Cloud pour Enterprise (CCE) et qu’une relation de confiance de domaine est établie entre ces deux organisations.

>[!NOTE]
>
>* Le correctif pour les profils professionnels est fourni dans Experience Manager 6.5.11.0.
>* La configuration existante continue de fonctionner si vous utilisez la même organisation Adobe IMS avec Experience Manager et CCE.



**Prérequis**

1. Une instance de Experience Manager en cours d’exécution avec l’authentification du porteur configurée pour AAL.
1. Installez le package suivant (Service Pack 11) sur votre instance Experience Manager 6.5.

   [Téléchargement de Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contact [!UICONTROL Assistance clientèle] pour obtenir l’identifiant du client et la clé secrète pour l’authentification du porteur de votre organisation IMS.

Voici les configurations supplémentaires requises après la migration vers les profils métier :

1. Dans **[!UICONTROL Adobe du fournisseur de configuration IMS OAuth Granite]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), définit :

   * ID de configuration OAuth (`oauth.configmanager.ims.configid`) : `ims` (Vérifier une fois, il se peut que vous l’ayez déjà configuré)

   * Entité propriétaire IMS (`ims.owningEntity`) : Votre identifiant de l’organisation IMS

   ![Identifiant de configuration IMS](assets/bearer-authentication1.png)

1. Ouvrir **[!UICONTROL Gestionnaire d’authentification du porteur]** et ajoutez l’identifiant client obtenu à partir de [!UICONTROL Assistance clientèle] à la liste de **[!UICONTROL ID de client OAuth autorisés]**.

   ![Ajouter un ID de client](assets/add-clientid-bearer-auth.png)

1. Ouvrir **[!UICONTROL Adobe de l’application OAuth Granite et du fournisseur]** et ajoutez le **[!UICONTROL ID client]** et **[!UICONTROL Secret du client]** (Clé secrète) obtenue auprès du service clientèle.

   Assurez-vous que la variable **[!UICONTROL ID de configuration]** Champ (`oauth.config.id`) contient la même valeur que celle fournie dans **[!UICONTROL ID de configuration OAuth]** Champ (`oauth.configmanager.ims.configid`) ci-dessus.

   ![Vérification de l’ID client](assets/clientid-secretkey.png)

1. Ouvrir **[!UICONTROL Préprocesseur de jeton d’échange de cluster Adobe IMS]** Configuration et définissez-la sur `enable`.

## Gestion du contrôle d’accès des utilisateurs {#user-access}

Cette section décrit comment gérer les utilisateurs et leur accès au référentiel du Experience Manager.

### Mappage de groupe {#group-mapping}

Le mappage de groupes détermine la manière dont les groupes en Experience Manager correspondent aux groupes dans Adobe IMS. Il joue un rôle important dans la manière dont les utilisateurs Adobe Asset Link se voient accorder l’autorisation d’accéder à Experience Manager Assets.

Lorsqu’il est utilisé avec Adobe Asset Link, Experience Manager délègue des fonctions de gestion des utilisateurs à Adobe IMS. Il crée automatiquement des utilisateurs et des groupes qui correspondent aux utilisateurs et aux groupes dans Adobe IMS. En outre, il synchronise les utilisateurs, les groupes et l’appartenance à un groupe dans Experience Manager pour qu’ils correspondent à ceux d’Adobe IMS.

Supposons, par exemple, que les utilisateurs d’Adobe Asset Link soient membres du groupe Adobe IMS assetlink-users. Dans ce cas, un groupe synchronisé nommé assetlink-users est créé en Experience Manager lorsqu’un utilisateur de ce groupe Adobe IMS se connecte pour la première fois à Adobe Asset Link. Chaque nouvel utilisateur du groupe Adobe IMS est ajouté à ce groupe correspondant dans Experience Manager lorsqu’il se connecte pour la première fois à Experience Manager via Adobe Asset Link.

Les groupes en Experience Manager qui correspondent aux groupes et sont synchronisés avec les groupes dans Adobe IMS peuvent se voir accorder l’accès directement ou en les faisant appartenir à un autre groupe. Voici un exemple de gestion des autorisations.

![exemples de groupes](assets/group-examples.png)

Les règles suivantes s’appliquent aux mappages de groupes en Experience Manager :

* Assurez-vous que la variable **[!UICONTROL Mappages de groupe]** dans **[!UICONTROL Adobe du fournisseur IMS OAuth Granite]** La configuration est vide.
* L’appartenance à un groupe d’utilisateurs Asset Link d’Adobe est évaluée lorsque l’utilisateur s’authentifie et la période dans **[!UICONTROL Délai d’expiration de l’utilisateur]** dans **[!UICONTROL Gestionnaire de synchronisation par défaut Apache Jackrabbit Oak]** a expiré. Actuellement, les utilisateurs peuvent être ajoutés et supprimés des groupes dans Experience Manager pour se synchroniser avec ce qui se trouve dans Adobe IMS.
* Évitez les conflits de nom de groupe. Assurez-vous que les noms utilisés pour les groupes créés dans Adobe IMS (pour gérer les utilisateurs) sont différents de tous les noms des groupes système de Experience Manager.

   Par exemple, assurez-vous qu’elles sont différentes de la variable `dam-users` et les groupes créés par l’administrateur du Experience Manager.

   Un groupe Adobe IMS dont le nom est en conflit avec le nom d’un groupe système de Experience Manager ou créé manuellement n’est pas utilisé pour contrôler les autorisations utilisateur.
* Si un utilisateur Adobe IMS se connecte à une instance de Experience Manager, sur laquelle le nom de l’utilisateur entre en conflit avec un utilisateur Experience Manager créé précédemment, l’utilisateur Adobe IMS se voit attribuer un autre nom, avec des numéros ajoutés, pour le rendre unique.

**Configuration du contrôle d’accès pour la première fois**

Les utilisateurs qui se connectent via Adobe Asset Link ne peuvent afficher et interagir avec les ressources qu’après avoir obtenu l’autorisation requise. Le [Mappage de groupe](#group-mapping) La section ci-dessus explique comment les groupes d’utilisateurs sont créés dans Experience Manager, qui correspondent aux groupes d’utilisateurs de votre entreprise et sont synchronisés avec eux dans Adobe IMS. Il est recommandé que les administrateurs du Experience Manager utilisent ces groupes pour gérer le contrôle d’accès pour les utilisateurs d’Adobe Asset Link.

Pour chaque groupe de Experience Manager synchronisé avec un groupe Adobe IMS (utilisé pour gérer le contrôle d’accès des utilisateurs) :

1. Assurez-vous que le groupe comporte un membre qui peut être utilisé pour une connexion initiale à partir d’Adobe Asset Link.
1. Utilisez cet utilisateur pour vous connecter à Adobe Asset Link et vous connecter à Experience Manager. Cette connexion devrait échouer.
1. Dans Experience Manager, localisez le groupe correspondant au groupe dans Adobe IMS et accordez-lui le contrôle d’accès souhaité. Par exemple, le nouveau groupe est devenu membre du groupe dam-users .
1. Fermez Adobe Asset Link et redémarrez l’application du Creative Cloud.
1. Pour vérifier que l’utilisateur dispose de l’accès attendu, rouvrez Adobe Asset Link.

Une fois ces étapes effectuées, d’autres utilisateurs du même groupe peuvent se connecter au Experience Manager avec Adobe Asset Link lors de leur première tentative. Ils disposent automatiquement des mêmes autorisations que les autres utilisateurs du groupe.

## Gestion des utilisateurs Experience Manager pour Adobe Asset Link {#manage-users}

Les utilisateurs d’Adobe Asset Link peuvent se connecter à Experience Manager lorsqu’ils sont connectés à leur application de Creative Cloud. Cette authentification utilise la technologie Adobe IMS et crée des informations utilisateur en Experience Manager, si elles n’existent pas. Il est courant que les clients d’entreprise Experience Manager gèrent leurs utilisateurs avec un fournisseur d’identité externe intégré à Experience Manager. Les fournisseurs d’identité incluent Adobe IMS et d’autres produits qui utilisent les protocoles SAML et LDAP. Vous pouvez également créer et gérer des utilisateurs localement dans Experience Manager.

Les utilisateurs qui se connectent à Experience Manager à partir d’Adobe Asset Link n’ont aucun conflit avec les informations d’utilisateur existantes stockées dans Experience Manager à partir de la connexion directe précédente, si :

* Tous les noms d’utilisateur utilisés pour la connexion directe à Experience Manager diffèrent des noms d’utilisateur utilisés dans Adobe IMS pour la connexion du Creative Cloud.
* Adobe IMS est utilisé comme fournisseur d’identité pour la connexion directe au Experience Manager.
* Les utilisateurs se connectent au Experience Manager à partir d’Adobe Asset Link avant de se connecter au Experience Manager direct avec le même compte.


D’un autre côté, les informations utilisateur créées suite à la connexion directe au Experience Manager doivent être mises à jour pour fonctionner avec Adobe Asset Link, dans les scénarios suivants :

* Le même nom d’utilisateur, tel que l’adresse électronique de l’utilisateur, est utilisé à la fois pour le compte dans Creative Cloud, qui utilise Adobe IMS, et pour le compte dans un fournisseur d’identité externe autre qu’Adobe IMS.
* Le même nom d’utilisateur est utilisé pour : le compte en Creative Cloud et un compte de Experience Manager local.
* Les comptes de Creative Cloud dans Adobe IMS sont des Federated ID, qui sont servis par le même fournisseur d’identité externe intégré à Experience Manager pour la connexion directe.

Les utilisateurs créés par le biais de ces scénarios ne disposent pas d’une propriété requise pour les utilisateurs, qui sont synchronisés avec Adobe IMS.

Pour mettre à jour ces utilisateurs en Experience Manager afin qu’ils travaillent avec Adobe Asset Link :

1. Dans la console web du Experience Manager, recherchez **[!UICONTROL Apache Jackrabbit Oak External Principal Configuration]** et cliquez pour la modifier. Désélectionnez l’option **[!UICONTROL Protection des identités externes]** puis cliquez sur **[!UICONTROL Enregistrer]**.
1. Pour accéder à l’interface de gestion des utilisateurs dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**. Sélectionnez l’utilisateur que vous souhaitez mettre à jour, puis notez la fin du chemin d’URL de votre navigateur pour cet utilisateur, en commençant par `/home/users`. Vous pouvez également rechercher le nom d’utilisateur dans CRXDE. Exemple de chemin d’accès utilisateur : `/home/users/x/xTac082TDh-guJzzG7WM`.
1. Dans CRXDE, accédez au chemin d’accès de l’utilisateur, sélectionnez le noeud utilisateur et affichez les propriétés du noeud en sélectionnant l’option **[!UICONTROL Propriétés]** dans la zone inférieure centrale. Ce noeud a une propriété `jcr:primaryType` valeur de propriété de `rep:User`.
1. Au bas de la **[!UICONTROL Propriétés]** zone de tabulation, saisissez une `Name` valeur de `rep:externalId`, `Type` valeur de `String`, et a `Value` valeur de `rep:authorizableId`;`ims`où `rep:authorizableId` est la valeur de la variable `rep:authorizableId` du noeud. (Un point-virgule est utilisé sans espaces pour séparer la variable `rep:authorizableId` de `ims`.)
1. Cliquez sur le bouton **[!UICONTROL Ajouter]** à droite de votre nouvelle entrée, puis cliquez sur **[!UICONTROL Enregistrer tout]**.
1. Répétez les étapes 2 à 5 pour tous les autres utilisateurs que vous souhaitez mettre à niveau afin de travailler avec Adobe Asset Link.
1. Dans la console web du Experience Manager, recherchez **[!UICONTROL Apache Jackrabbit Oak External Principal Configuration]** et cliquez pour la modifier. Désélectionnez l’option **[!UICONTROL Protection des identités externes]** puis cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Si les services ne sont pas restaurés en quelques minutes, redémarrez Experience Manager pour permettre des authentifications réussies.

Après cette modification, un utilisateur Experience Manager mis à jour peut se connecter à Adobe Asset Link et continuer à utiliser la méthode de connexion directe à Experience Manager utilisée avant la mise à jour. Une fois l’authentification réussie avec Adobe IMS, les informations de profil utilisateur du Experience Manager sont synchronisées avec le profil utilisateur dans Adobe IMS.

Il existe une méthode par laquelle une migration en masse de plusieurs utilisateurs de Experience Manager peut être effectuée pour leur permettre de travailler avec Adobe Asset Link. Pour plus d’informations et d’aide sur l’activation de cette option, contactez l’assistance Adobe.

Au lieu des étapes, dans certains cas, un utilisateur de lien de ressource d’Adobe peut bénéficier d’un accès rapide à Experience Manager. Dans ce cas, les informations sur l’utilisateur préexistantes sont trouvées et supprimées avec Experience Manager User Management ou CRXDE du Experience Manager avant leur connexion à Adobe Asset Link. Les informations sur les nouveaux utilisateurs sont créées dans Experience Manager après la connexion. Utilisez cette approche uniquement si vous êtes certain qu’aucune donnée importante n’est ajoutée en tant qu’enfant du noeud utilisateur. Ces données supplémentaires sont tout noeud enfant du noeud utilisateur autre que `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`, et `rep:policy/*` noeuds.

## Processus de démarrage automatique pour traiter les ressources de manière conditionnelle {#auto-start-workflow}

Dans Experience Manager 6.4 et Experience Manager 6.5, les administrateurs peuvent configurer des workflows pour exécuter et traiter automatiquement les ressources en fonction de conditions prédéfinies.

La configuration est utile pour les utilisateurs et les spécialistes du marketing du secteur, par exemple pour créer un workflow personnalisé sur quelques dossiers spécifiques. Disons que toutes les ressources de la séance photo d’une agence peuvent être filigrane ou que toutes les ressources téléchargées par un programme de travail indépendant peuvent être traitées pour créer des rendus spécifiques.

Pour plus d’informations et pour la configuration du Experience Manager, voir [exécution automatique du workflow sur les ressources](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Création d’un index personnalisé dans les versions Experience Manager 6.4.x {#create-custom-index}

Experience Manager contient des index utilisés pour l’interrogation. Créez l’index personnalisé suivant pour la version spécifiée. Experience Manager 6.5.0 contient cet index par défaut. Adobe Asset Link nécessite cet index pour déterminer les ressources qu’un utilisateur a extraites.

1. Dans CRXDE, recherchez `/oak:index` noeud . Créez un noeud nommé `cqDrivelock` et définissez ses `Type` to `oak:QueryIndexDefinition`.

1. Ajoutez les propriétés suivantes au nouveau noeud et enregistrez les modifications :

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configuration de la recherche visuelle ou par analogie {#configure-visual-similarity-search}

La fonctionnalité de recherche visuelle vous permet de rechercher des ressources visuellement similaires dans le référentiel AEM Assets à l’aide du panneau Adobe Asset Link . La fonctionnalité est disponible dans la version 6.5.0 ou ultérieure et seules les ressources indexées sont recherchées. Pour plus d’informations, voir [comment configurer la recherche visuelle](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Génération de rendus pour placement uniquement pour Adobe InDesign {#fpo-renditions}

Experience Manager fournit des rendus utilisés uniquement pour placement (FPO). Ces rendus FPO ont une taille de fichier réduite, mais présentent les mêmes proportions. Si un rendu FPO n’est pas disponible pour une ressource, Adobe InDesign utilise la ressource d’origine à la place. Ce mécanisme de secours garantit que le workflow créatif se poursuit sans interruption. Pour plus d’informations, voir [générer des rendus FPO ;](/help/assets/configure-fpo-renditions.md).


## Intégration à Adobe Stock {#adobe-stock-integration}

Les organisations intègrent leurs comptes Adobe Stock à Experience Manager Assets. Il permet aux marketeurs de mettre à disposition des photos, des vecteurs, des illustrations, des vidéos, des modèles et des ressources 3D de haute qualité et libres de droits pour leurs projets de création et de marketing. Les professionnels de la création peuvent utiliser ces ressources à l’aide du panneau Asset Link.

Pour procéder à l’intégration avec Adobe Stock, reportez-vous à la section [Ressources Adobe Stock dans Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Experience Manager 6.4.2 ou version ultérieure est requis pour l’intégration à Adobe Stock.


## Résolution des problèmes liés aux Experience Manager {#troubleshoot}


Si vous rencontrez des problèmes lors de la configuration ou de l’utilisation d’Adobe Asset Link, essayez les méthodes suivantes :

* Assurez-vous que votre déploiement respecte les conditions préalables. Plus précisément, assurez-vous que les Feature Packs ou packages appropriés sont installés.
* Contactez le partenaire ou l’intégrateur système de votre entreprise.
* Si les utilisateurs de votre Creative Cloud ne peuvent pas vérifier dans les ressources extraites, vérifiez la casse des noms de domaine dans les ID d’email. Pour résoudre ce problème, voir [configuration manuelle](#manual-configuration).
* Pour plus d’informations, voir [dépannage d’Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [À propos d’Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Utilisation de Asset Link dans l’appli de bureau Creative Cloud et gestion des ressources](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configuration d’Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).






