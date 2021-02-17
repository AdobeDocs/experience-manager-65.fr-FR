---
title: Configuration manuelle de l’intégration à Adobe Target
seo-title: Configuration manuelle de l’intégration à Adobe Target
description: Découvrez comment configurer manuellement l’intégration à Adobe Target.
seo-description: Découvrez comment configurer manuellement l’intégration à Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 74%

---


# Configuration manuelle de l’intégration à Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Vous pouvez modifier les configurations de l’assistant de souscription que vous avez effectuées lors de l’utilisation de l’assistant, ou vous pouvez intégrer AEM manuellement à Adobe Target sans utiliser l’assistant.

## Modification des configurations de l’assistant de souscription {#modifying-the-opt-in-wizard-configurations}

L&#39;[Assistant d&#39;inclusion](/help/sites-administering/opt-in.md) que [intègre AEM à Adobe Target](/help/sites-administering/target.md) crée automatiquement une configuration de cloud de Cibles nommée Configuration de Cible activée. L’assistant crée également une structure Target pour la configuration de cloud appelée Structure Target mise en service. Vous pouvez modifier les propriétés de la configuration de cloud et de la structure si nécessaire.

Vous pouvez également configurer Adobe Target afin de l’utiliser en tant que source de création de rapports lors du ciblage du contenu en définissant la configuration d’A4T Analytics Cloud.

Pour localiser la configuration du cloud et la structure, accédez à **Cloud Services** par **Outils** > **Déploiement** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Sous Adobe Target, cliquez ou appuyez sur **Afficher les configurations**.

### Propriétés de configuration de Target mise en service {#provisioned-target-configuration-properties}

Les valeurs de propriétés suivantes sont utilisées dans la configuration de cloud de la configuration Target mise en service créée par l’assistant de souscription :

* **Code client :** comme indiqué dans l’assistant d’ouverture de session.
* **Courrier électronique :** comme indiqué dans l’assistant d’ouverture de session.
* **Mot de passe :** tel que saisi dans l’assistant d’ouverture de session.
* **Type d’API:** REST
* **Synchroniser Les Segments À Partir D’Adobe Target:** Sélectionné.

* **bibliothèque cliente :** mbox.js.
* **Utilisez la gestion dynamique des balises pour diffuser la bibliothèque cliente :** Non sélectionné. Sélectionnez cette option si vous [utilisez la gestion dynamique des balises](/help/sites-administering/dtm.md) ou un autre système de gestion des balises pour héberger le fichier mbox.js ou AT.js. Adobe vous recommande d’utiliser la gestion dynamique des balises plutôt qu’AEM pour livrer la bibliothèque.

* **mbox.js personnalisé :** Aucun spécifié pour que le fichier mbox.js par défaut soit utilisé. Spécifiez un fichier mbox.js personnalisé selon vos besoins. S’affiche uniquement si vous avez sélectionné mbox.js.
* **Custom AT.js :** aucune valeur spécifiée pour que le fichier AT.js par défaut soit utilisé. Spécifiez un fichier AT.js personnalisé selon vos besoins.  S’affiche uniquement si vous avez sélectionné AT.js.

>[!NOTE]
>
>Dans AEM 6.3, vous pouvez sélectionner le fichier de bibliothèque de Cibles, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), qui est une nouvelle bibliothèque d’implémentation pour Adobe Target conçue pour les implémentations Web classiques et les applications d’une seule page.
>
>AT.js propose plusieurs améliorations par rapport à la bibliothèque mbox.js :
>
>* Temps de chargement des pages améliorés pour les mises en œuvre web
>* Sécurité renforcée
>* Meilleures options de mise en œuvre pour les applications d’une seule page
>* AT.js contient les composants qui étaient inclus dans target.js. Il n’y a donc plus d’appel à target.js.


### Propriétés de structure de Target mise en service {#provisioned-target-framework-properties}

La structure de Target mise en service créée par l’assistant de souscription est configurée pour envoyer des données contextuelles à partir du magasin de données de profil. Les éléments de données du magasin relatifs à l’âge et au sexe sont envoyés à Target par défaut. Votre solution requiert probablement l’envoi de paramètres supplémentaires.

![chlimage_1-158](assets/chlimage_1-158.png)

Vous pouvez configurer la structure pour envoyer des informations contextuelles vers Target comme décrit dans [Ajout d’une structure de Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Définition de la configuration d’A4T Analytics Cloud  {#configuring-a-t-analytics-cloud-configuration}

Vous pouvez configurer Adobe Target pour utiliser Adobe Analytics en tant que source de création de rapports lors du ciblage du contenu.

Pour ce faire, vous devez spécifier la configuration de cloud d’A4T pour connecter votre configuration de cloud Adobe Target de la façon suivante :

1. Accédez à **Cloud Services** par le **logo de l&#39;AEM** > **Outils** > **Déploiement** > **Cloud Services**.
1. Dans la section **Adobe Target**, cliquez sur **Configurer maintenant**.
1. Reconnectez-vous à votre configuration Adobe Target.
1. Dans le menu déroulant **Configuration d’A4T Analytics Cloud**, sélectionnez la structure.

   >[!NOTE]
   >
   >Seules les fonctionnalités d’analyse qui sont activées pour A4T sont disponibles.
   >
   >En configurant A4T avec AEM, vous risquez de voir une entrée de référence de configuration manquante. Pour pouvoir sélectionner la structure d’analyse, procédez comme suit :
   >
   >1. Accédez à **Outils** > **Général** > **CRXDE Lite**.
   1. Accédez à **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Définissez la propriété **disable** sur **false**.
   1. Appuyez ou cliquez sur **Tout enregistrer**.


   ![chlimage_1-159](assets/chlimage_1-159.png)

   Cliquez sur **OK**. Lorsque vous ciblez le contenu avec Adobe Target, vous pouvez [choisir la source de rapport](/help/sites-authoring/content-targeting-touch.md).

## Intégration manuelle à Adobe Target  {#manually-integrating-with-adobe-target}

Intégrez manuellement à Adobe Target au lieu d’utiliser l’assistant de souscription.

>[!NOTE]
Le fichier de bibliothèque de Cibles [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html) est une nouvelle bibliothèque d’implémentation pour Adobe Target, conçue pour les implémentations Web classiques et les applications d’une seule page. Adobe recommande d’utiliser AT.js, au lieu de mbox.js, comme bibliothèque cliente.
AT.js propose plusieurs améliorations par rapport à la bibliothèque mbox.js :
* Temps de chargement des pages améliorés pour les mises en œuvre web
* Sécurité renforcée
* Meilleures options de mise en œuvre pour les applications d’une seule page
* AT.js contient les composants qui étaient inclus dans target.js. Il n’y a donc plus d’appel à target.js.

Vous pouvez sélectionner AT.js ou mbox.js dans le menu déroulant **Bibliothèque cliente**.

### Création d’une configuration de cloud Target  {#creating-a-target-cloud-configuration}

Pour permettre à AEM d’interagir avec Adobe Target, créez une configuration de cloud Target. Pour créer la configuration, vous fournissez le code client et les informations d’identification d’utilisateur Adobe Target.

Vous créez la configuration de cloud Target une seule fois, car vous pouvez l’associer à plusieurs campagnes AEM. Si vous avez plusieurs codes client Adobe Target, créez une configuration pour chaque code client.

Vous pouvez configurer la configuration de cloud pour synchroniser les segments depuis Adobe Target. Si vous activez la synchronisation, les segments sont importés en arrière-plan à partir de Target dès que la configuration de cloud est enregistrée.

Utilisez la procédure suivante pour créer une configuration de cloud Target dans AEM :

1. Accédez à **Cloud Services** par le **logo de l&#39;AEM** > **Outils** > **Déploiement** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   La **page de présentation de Adobe Marketing Cloud** s&#39;affiche.

1. Dans la section **Adobe Target**, cliquez sur **Configurer maintenant**.
1. Dans la boîte de dialogue **Créer une configuration** :

   1. Attribuez à la configuration un **Titre**.
   1. Sélectionnez le modèle **Configuration Adobe Target**.
   1. Cliquez sur **Créer**.

   La boîte de dialogue de modification s’ouvre.

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   En configurant A4T avec AEM, vous risquez de voir une entrée de référence de configuration manquante. Pour pouvoir sélectionner la structure d’analyse, procédez comme suit :
   1. Accédez à **Outils** > **Général** > **CRXDE Lite**.
   1. Accédez à **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Définissez la propriété **disable** sur **false**.
   1. Appuyez ou cliquez sur **Tout enregistrer**.


1. Dans la boîte de dialogue, saisissez les valeurs pour ces propriétés.

   * **Code client** : code client du compte Target.
   * **Courrier électronique** : l’e-mail du compte Target.
   * **Mot de passe** : mot de passe du compte Target.
   * **Type d’API** : REST ou XML.
   * **Configuration d’A4T Analytics Cloud** : sélectionnez la configuration de cloud Analytics utilisée pour les objectifs et les mesures des activités de Target. Vous avez besoin de cette option si vous utilisez Adobe Analytics en tant que source de création de rapports lors du ciblage de contenu. Si vous ne voyez pas la configuration de votre cloud, consultez la note dans [Configuration de A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).

   * **Utiliser un ciblage précis :** cette case à cocher est sélectionnée par défaut. Si cette option est sélectionnée, la configuration du service cloud attend le chargement du contexte avant de charger le contenu. Voir la remarque qui suit.
   * **Synchroniser les segments à partir d’Adobe Target :** sélectionnez cette option pour télécharger les segments définis dans la Cible afin de les utiliser dans AEM. Vous devez sélectionner cette option lorsque la propriété Type d’API est REST, car les segments incorporés ne sont pas pris en charge, et vous devez toujours utiliser les segments de Target. (Notez que le terme « segment » d’AEM équivaut à « audience » dans Target.)
   * **Bibliothèque cliente :** indiquez si vous souhaitez utiliser la bibliothèque cliente mbox.js ou AT.js.
   * **Utilisez la gestion dynamique des balises pour diffuser la bibliothèque**  client : sélectionnez cette option pour utiliser AT.js ou mbox.js de la gestion dynamique des balises ou un autre système de gestion des balises. Vous devez [configurer l’intégration de la gestion dynamique des balises](/help/sites-administering/dtm.md) pour utiliser cette option. Adobe vous recommande d’utiliser la gestion dynamique des balises plutôt qu’AEM pour livrer la bibliothèque.
   * **Fichier mbox.js personnalisé** : laissez ce champ vierge si vous avez coché la case Gestion dynamique des balises ou pour utiliser le fichier mbox.js par défaut. Vous pouvez également télécharger votre fichier mbox.js personnalisé. S’affiche uniquement si vous avez sélectionné mbox.js.
   * **AT.js personnalisé** : laissez ce champ vierge si vous avez coché la case Gestion dynamique des balises ou pour utiliser le fichier AT.js par défaut. Vous pouvez également télécharger votre fichier AT.js personnalisé.  S’affiche uniquement si vous avez sélectionné AT.js.

   >[!NOTE]
   Par défaut, lorsque vous souscrivez à l’assistant de configuration Adobe Target, le ciblage précis est activé.
   Le ciblage précis implique que cette configuration du service cloud attend le chargement du contexte avant de charger le contenu. Par conséquent, en termes de performances, le ciblage précis peut entraîner un délai de quelques millisecondes avant le chargement du contenu.
   Le ciblage précis est toujours activé sur l’instance de création. Toutefois, sur l’instance de publication, vous pouvez choisir de le désactiver en désactivant la coche en regard de Ciblage précis dans la configuration du service cloud (**http://localhost:4502/etc/cloudservices.html**). Vous pouvez également toujours activer et désactiver le ciblage précis pour chaque composant, quel que soit le paramètre dans la configuration du service cloud.
   Si vous avez ***déjà*** créé les composants ciblés et si vous modifiez ce paramètre, vos modifications n’affectent pas ces composants. Vous devez effectuer toutes les modifications directement sur ces composants.

1. Cliquez sur **Se connecter à Target** pour lancer la connexion à Target. Si la connexion réussit, le message **Connexion réussie** s’affiche. Cliquez sur **OK** dans le message et **OK** dans la boîte de dialogue.

   Si vous ne parvenez pas à vous connecter à Target, voir la section [Dépannage](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Ajout d’une structure Target  {#adding-a-target-framework}

Une fois que vous avez configuré la configuration de cloud Target, ajoutez une structure Target. La structure identifie les paramètres par défaut qui sont envoyés à Adobe Target à partir des composants [ClientContext](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md). Target utilise les paramètres pour déterminer les segments qui s’appliquent au contexte actuel.

Vous pouvez créer des structures multiples pour une même configuration Target. Les structures multiples s’avèrent utiles lorsque vous devez envoyer un jeu de paramètres différent à Target pour différentes sections de votre site web. Créez une structure pour chaque jeu de paramètres que vous avez besoin d’envoyer. Associez chaque section de votre site web à la structure appropriée. Notez qu’une page web peut utiliser uniquement une structure à la fois.

1. Dans la page de configuration de votre Cible, cliquez sur **+** (signe plus) en regard de Cadres disponibles.
1. Dans la boîte de dialogue Créer un cadre, spécifiez un **titre**, sélectionnez le **cadre Adobe Target**, puis cliquez sur **Créer**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   La page de structure s’ouvre. Sidekick fournit des composants qui représentent les informations provenant du [contexte client](/help/sites-administering/client-context.md) ou [ContextHub](/help/sites-developing/ch-configuring.md) que vous pouvez mapper.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Faites glisser le composant ClientContext représentant les données que vous souhaitez utiliser pour mettre en correspondance avec la cible de dépôt. Vous pouvez également faire glisser le composant **Boutique ContextHub** vers la structure.

   >[!NOTE]
   Lors de la mise en correspondance, les paramètres sont transmis à un mbox via des chaînes simples. Vous ne pouvez pas mettre en correspondance des tableaux à partir de ContextHub.

   Par exemple, pour utiliser **Données de Profil** sur les visiteurs de votre site pour contrôler votre campagne de Cible, faites glisser le composant **Données de Profil** sur la page. Les variables de données de profil disponibles pour le mappage aux paramètres de Cible s’affichent.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Sélectionnez les variables que vous souhaitez rendre visibles au système Adobe Target en cochant la case **Partager** dans les colonnes appropriées.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   La synchronisation des paramètres est unidirectionnelle uniquement, d’AEM à Adobe Target.

La structure est créée. Pour répliquer la structure sur l’instance de publication, utilisez l’option **Activer le cadre** dans le sidekick.

### Association des activités à la configuration de cloud Target  {#associating-activities-with-the-target-cloud-configuration}

Associez vos [AEM activités](/help/sites-authoring/activitylib.md) à votre configuration de cloud de Cibles afin que vous puissiez mettre en miroir les activités dans [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Les types d’activités disponibles sont déterminés par ce qui suit :
* Si l’option **xt_only** est activée sur le client Adobe Target (clientcode) utilisé sur AEM pour se connecter à Adobe Target, vous pouvez créer **uniquement** des activités XT dans AEM.

* Si les options **xt_only** **ne sont pas** activées sur le client Adobe Target (clientcode), vous pouvez créer **à la fois** des activités XT et A/B dans AEM.

**Remarque :** L’option **xt_only** est un paramètre appliqué à un certain client Adobe Target (clientcode) et peut uniquement être modifiée directement dans Adobe Target. Vous ne pouvez pas activer ou désactiver cette option dans AEM.

### Association de la structure Target à votre site  {#associating-the-target-framework-with-your-site}

Après avoir créé une structure Target dans AEM, associez vos pages web à la structure. Les composants ciblés sur les pages envoient les données définies par la structure vers Adobe Target pour le suivi. (voir [Ciblage de contenu](/help/sites-authoring/content-targeting-touch.md)). 

Lorsque vous associez une page à la structure, les pages enfants héritent de l’association.

1. Dans la console **Sites**, accédez au site que vous souhaitez configurer.
1. En utilisant [actions rapides](/help/sites-authoring/basic-handling.md#quick-actions) ou [mode de sélection](/help/sites-authoring/basic-handling.md), sélectionnez **Propriétés de la Vue.**
1. Sélectionnez l’onglet **Services cloud**.
1. Appuyez/cliquez sur **Modifier**.
1. Appuyez/cliquez sur **Ajouter la configuration** sous **Configurations du service cloud** et sélectionnez **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Sélectionnez la structure souhaitée sous **Référence de configuration**.

   >[!NOTE]
   Veillez à sélectionner la **structure** que vous avez créée et non la configuration cloud Target dans laquelle elle a été créée.

1. Appuyez/cliquez sur **Terminé.**
1. Activez la page racine du site web pour la répliquer sur le serveur de publication. (Voir [Publication de pages](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Si la structure que vous avez jointe à la page n’était pas encore activée, un assistant s’ouvre pour vous permettre de la publier.

## Dépannage des problèmes de connexion à Target  {#troubleshooting-target-connection-problems}

Effectuez les tâches suivantes pour résoudre les problèmes qui se produisent lors de la connexion à Target :

* Assurez-vous que les informations d’identification de l’utilisateur fournies sont correctes.
* Assurez-vous que l’instance AEM peut se connecter au serveur Target. Par exemple, assurez-vous que les règles de pare-feu ne bloquent pas les connexions AEM sortantes, ou qu’AEM est configuré pour utiliser les proxys nécessaires.
* Recherchez des messages utiles dans le journal d’erreurs d’AEM. Le fichier error.log situé dans le répertoire **crx-quickstart/logs** où AEM est installé.
* Lors de la modification de l’activité dans Adobe Target, l’URL pointe sur localhost. Pour contourner ce problème, définissez l’externaliseur AEM sur l’URL adéquate.

