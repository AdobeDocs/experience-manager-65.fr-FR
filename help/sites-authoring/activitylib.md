---
title: Gestion des activités
seo-title: Gestion des activités
description: 'La console Activités vous permet de créer, d’organiser et de gérer les activités marketing de vos marques :'
seo-description: 'La console Activités vous permet de créer, d’organiser et de gérer les activités marketing de vos marques :'
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
translation-type: tm+mt
source-git-commit: d53e72b198db91d368ddddac768d19b88ee29050

---


# Gestion des activités{#managing-activities}

La console Activités vous permet de créer, d’organiser et de gérer les [activités](/help/sites-authoring/personalization.md#activities) marketing de vos marques :

* Ajoutez des marques.
* Pour chaque marque, ajoutez et configurez les activités.
* Gérez les activités.

>[!NOTE]
>
>Si vous utilisez Adobe Target comme moteur de ciblage, vous pouvez également [consulter les données de performances de vos activités](#viewing-performance-and-converting-winning-experiences-a-b-test). Si vous utilisez les tests A/B, vous pouvez [convertir les gagnants](#viewing-performance-and-converting-winning-experiences-a-b-test).

Dans la console Activités, les activités sont organisées par marque. Vous pouvez utiliser les marques et les dossiers afin de structurer l’organisation de vos activités. Vous accédez à la console Activités en appuyant/cliquant sur **Personnalisation** et en appuyant/cliquant sur **Activités**.

Activities are available in Targeting mode for [authoring targeted content](/help/sites-authoring/content-targeting-touch.md), where you can also create activities. Les activités que vous créez en mode Ciblage apparaissent dans la console Activités.

Les activités sont présentées avec un libellé décrivant le type d’activité défini :

* XT : ciblage d’expérience Adobe Target
* A/B : test A/B Adobe Target
* AEM : ciblage Adobe Experience Manager (via ContextHub ou ClientContext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Les types d’activités disponibles sont déterminés par ce qui suit :

>* Si l’option **xt_only** est activée sur le client Adobe Target (clientcode) utilisé sur AEM pour se connecter à Adobe Target, vous pouvez créer **uniquement** des activités XT dans AEM.
   >
* Si les options **xt_only** **ne sont pas** activées sur le client Adobe Target (clientcode), vous pouvez créer **à la fois** des activités XT et A/B dans AEM.

**Remarque :** L’option **xt_only** est un paramètre appliqué à un certain client Adobe Target (clientcode) et peut uniquement être modifiée directement dans Adobe Target. Vous ne pouvez pas activer ou désactiver cette option dans AEM.

>[!CAUTION]
Vous devez sécuriser le nœud de paramètres d’activité **c:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les utilisateurs normaux. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.
Voir [Préalables à l’intégration à Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) pour plus d’informations.

## Création d’une marque à l’aide de la console Activités {#creating-a-brand-using-the-activities-console}

Créez une marque pour laquelle vous souhaitez gérer les activités marketing.

When you create a brand using the Activities console, it also appears in the [Offers console](/help/sites-authoring/offerlib.md) where you can create offers for the experiences of your activities.

1. Dans la console Navigation, cliquez ou appuyez sur **Personnalisation**. Cliquez ou appuyez sur **Activités**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. Dans la console Activités, cliquez ou appuyez sur **Créer** et ensuite sur **Créer une marque**.
1. Sélectionnez un modèle de marque et cliquez ou appuyez sur **Suivant**.
1. Saisissez le titre de la marque tel qu’il doit apparaître dans les consoles Activités et Offres. Si vous le souhaitez, saisissez ou sélectionnez une ou plusieurs balises à associer à la marque.
1. Cliquez ou appuyez sur **Créer**. Votre marque apparaît dans la console Activités.

## Ajout/modification d’une activité à l’aide de la console Activités {#adding-editing-an-activity-using-the-activities-console}

Ajoutez une activité ou modifiez une activité existante pour concentrer vos efforts marketing sur certaines audiences. Lorsque vous créez/modifiez une activité, vous spécifiez les informations suivantes :

* **Nom :** nom de l’activité.
* **Moteur de ciblage :**[ AEM](/help/sites-authoring/personalization.md#aem) ou [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) comme moteur de recherche de contenu ciblé.

* **Sélectionner une configuration cible :** (Adobe Target uniquement) configuration de cloud que cette activité doit utiliser pour se connecter à Adobe Target. Cette option s’affiche uniquement si Adobe Target est sélectionné comme moteur de ciblage.
* **Type d’activité : **Type d’activité - Test A/B ou ciblage d’expérience
* **Intention :** description de l’activité (facultatif).
* **Expériences :** mappages entre les noms des audiences et les segments marketing que vous ciblez.
* **** Pourcentages de trafic : Si le test A/B est sélectionné, vous pouvez modifier le volume de trafic (en pourcentage) qui va à chaque expérience.
* **Durée :** période pendant laquelle l’activité est appliquée.
* **Priorité :** priorité relative de l’activité. Lorsque les activités fournissent du contenu pour les mêmes segments d’utilisateur, l’activité présentant la priorité la plus élevée est prioritaire.
* **** Mesure d’objectif : Si Adobe Target est sélectionné comme moteur de ciblage, vous pouvez ajouter des mesures de réussite à l’activité. Une mesure de réussite est nécessaire.

>[!NOTE]
Les nouvelles activités Adobe Target doivent être ***créées*** dans l’éditeur de contenu ciblé, et non dans la console **Activités**, sinon la synchronisation avec Adobe Target échouera.
Vous pouvez toutefois modifier les activités existantes d’Adobe Target dans la console.

Pour ajouter une activité :

1. Click or tap the brand for which you are creating the activity, and then click or tap **Create **then** Create Activity. **If editing, select the activity in the Master Area screen and clicking or tapping **Edit Activity**.
1. Fournissez les informations suivantes, puis appuyez ou cliquez sur **Suivant** :

   * Nom de l’activité.
   * Le moteur de ciblage à utiliser. ContextHub (AEM) est sélectionné par défaut. Si vous devez utiliser Adobe Target, créez l’activité dans l’éditeur de contenu ciblé.
   * Si vous avez sélectionné Adobe Target comme moteur de ciblage, sélectionnez/modifiez la configuration de cloud à utiliser pour se connecter à Adobe Target. (Veillez à ne pas sélectionner une structure que vous avez créée pour la configuration de cloud.)
   * L’objectif ou une description de l’activité (facultatif).
   * Sélectionnez le type d’activité.

1. Ajoutez une ou plusieurs expériences à l’activité. Appuyez ou cliquez sur **Ajouter une expérience**.
1. Si vous utilisez le ciblage AEM ou le ciblage d’expérience Adobe Target :

   1. Cliquez ou appuyez sur **Sélectionner l’audience **et sélectionnez le segment ciblé par votre expérience.
   1. Appuyez ou cliquez sur **Ajouter une expérience**, saisissez un nom, puis appuyez ou cliquez sur **OK**. 

   1. Appuyez ou cliquez sur **Suivant**.
   Si vous utilisez le test A/B Adobe Target :

   1. Cliquez ou appuyez sur le crayon dans la zone Audiences pour sélectionner une audience.
   1. Appuyez ou cliquez sur **Ajouter une expérience**, saisissez un nom, puis appuyez ou cliquez sur **OK**. 

   1. Saisissez le pourcentage du trafic qui affiche chaque expérience.
   1. Appuyez ou cliquez sur **Suivant**.


1. Pour indiquer le moment où l’activité commence, utilisez le menu déroulant **Démarrer** pour sélectionner l’une des valeurs suivantes :

   * **Après activation :** l’activité débute lorsque la page contenant le contenu ciblé est activée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, appuyez ou cliquez sur l’icône de calendrier, sélectionnez une date, puis spécifiez l’heure de début de l’activité.

1. Pour indiquer le moment où l’activité se termine, utilisez le menu déroulant Fin pour sélectionner l’une des valeurs suivantes :

   * **Si désactivés** : l’activité s’arrête lorsque la page contenant le contenu ciblé est désactivée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, appuyez ou cliquez sur l’icône de calendrier, sélectionnez une date, puis spécifiez l’heure de fin de l’activité.

1. Pour spécifier la priorité de l’activité, utilisez le curseur pour choisir **Faible**, **Normale** ou **Élevée**.
1. Si vous utilisez Adobe Target comme moteur de ciblage, sélectionnez ce que vous souhaitez mesurer avec cette activité. See [Configuring the Activity and Setting Goals](/help/sites-authoring/content-targeting-touch.md) for more information on the success metrics available. Vous devez sélectionner au moins un objectif.
1. Cliquez ou appuyez sur **Enregistrer**.

   >[!NOTE]
   Après avoir créé une activité, vous devez la modifier de manière à ce qu’elle soit disponible.

## Publication et annulation de la publication des activités {#publishing-and-unpublishing-activities}

Vous devez publier les activités afin de les rendre disponibles. À l’inverse, vous pouvez rendre les activités non disponibles en annulant leur publication.

>[!NOTE]
Lorsque vous annulez la publication d’une activité,

Pour publier des activités ou annuler leur publication :

1. Cliquez ou appuyez sur la marque puis sur la zone contenant l’activité que vous souhaitez publier ou dont vous souhaitez annuler la publication.
1. Appuyez ou cliquez sur l’icône située en regard des activités que vous souhaitez publier ou dont vous souhaitez annuler la publication.

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Pour publier, appuyez ou cliquez sur **Publier**. Pour annuler la publication, appuyez ou cliquez sur **Annuler la publication**. Les activités sont publiées ou leur publication est annulée, et leur état change dans la console Activités (une actualisation peut être nécessaire).

## Activités sur les instances de création et de publication {#activities-on-author-and-publish-instances}

Lorsqu’une activité qui utilise le moteur ciblé Adobe Target est activée, une seconde activité est créée sur l’instance de publication :

* L’activité sur l’instance de création suit l’activité sur l’instance de création et s’avère utile pour simuler l’expérience des visiteurs. Les analyses enregistrées pour cette activité ne reflètent que ce qui se produit sur l’instance de création.
* L’activité sur l’instance de publication reflète l’activité sur le serveur de publication et y réagit. Il s’agit de l’activité qui s’exécute sur le site web public. Seule l’activité de publication est pertinente pour suivre et analyser l’utilisation du site public.

## Affichage des performances et conversion des expériences gagnantes (test A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Vous pouvez afficher les performances de n’importe quelle activité Adobe Target (XT ou A/B). Si vous utilisez les tests A/B, vous pouvez également convertir l’expérience gagnante, qui devient alors l’expérience par défaut.

Pour afficher les performances des activités et convertir les expériences gagnantes :

1. In **Personalization**, click or tap **Activities** to navigate to the **Activities** console.
1. Cliquez ou appuyez sur la marque dont vous souhaitez voir les activités.
1. Select the activity and click or tap **View Properties** and click the **Reports** tab and select the activity that you want to view performance for/convert winning experiences for. Les données de performances sont affichées.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Click or tap the **Push winner** link to push that experience as the default experience.

   La conversion du gagnant effectue les opérations suivantes :

   * Elle désactive l’activité actuelle
   * Elle modifie toutes les pages et remplace le contenu ciblé par le contenu de l’expérience gagnante. The content of the winning experience becomes part of the normal page **without** targeting.
   ![chlimage_1-116](assets/chlimage_1-116.png)

   L’expérience gagnante est celle qui génère la meilleure progression dans les rapports, en fonction des taux de conversion.

1. Cliquez ou appuyez sur **Oui** pour confirmer que vous souhaitez convertir le gagnant, c’est-à-dire désactiver l’expérience actuelle et la remplacer par le contenu de l’expérience gagnante.

## Synchronisation des activités avec Adobe Target {#synchronizing-activities-with-adobe-target}

Les activités qui utilisent le moteur de ciblage Adobe Target sont synchronisées avec les campagnes Adobe Target. Une activité est automatiquement synchronisée avec Adobe Target lorsque les conditions suivantes sont réunies :

* L’activité contient au moins une expérience.
* Au moins une expérience contient un segment mappé et une offre.
* Chaque expérience contenue dans l’activité doit comporter le même nombre d’offres.

Ces conditions s’appliquent aux activités sur les instances de création et de publication.

Lorsqu’une activité est synchronisée, une campagne correspondante est créée dans Adobe Target :

* Les activités sur l’instance de publication portent le même nom que la campagne correspondante d’Adobe Target.
* Activities on the author instance correspond with Target campaigns of the same name with the `_author` suffix.

![chlimage_1-117](assets/chlimage_1-117.png)

Les activités _author sont synchronisées immédiatement lorsque l’activité est modifiée. La synchronisation immédiate permet la simulation des activités avec ClientContext ou ContextHub.

Les activités de publication sont synchronisées lorsque l’activité est publiée sur l’instance de publication AEM.

## Résolution des problèmes de synchronisation d’activité {#troubleshooting-activity-synchronization}

When AEM synchronizes an activity with Adobe Target, AEM includes a property of the activity named `thirdPartyId`. La valeur de cette propriété est basée sur le chemin de l’activité dans le référentiel AEM. Dans Adobe Target, les campagnes ne peuvent avoir la même valeur pour la propriété `thirdPartyId`. Par conséquent, une activité ne se synchronise pas si une campagne existante (d’un autre type A/B ou XT) dans Adobe Target utilise la même valeur pour `thirdPartyId` .

Cette situation peut se produire dans les cas suivants :

1. Une activité est créée et synchronisée avec Adobe Target.
1. Sur une autre instance AEM, une activité est créée sous la même marque avec le même nom. La synchronisation de cette activité échoue à chaque tentative.

Cette situation peut aussi se produire dans les cas suivants :

1. Une activité est créée et synchronisée avec Adobe Target. L’activité est ensuite supprimée sur AEM.
1. Une activité est créée sous la même marque avec le même nom que l’activité supprimée. La synchronisation de cette activité échoue à chaque tentative.

Pour éviter des problèmes de synchronisation, donnez toujours des noms uniques aux activités. Si une activité ne se synchronise pas, vous pouvez supprimer la campagne dans Adobe Target qui porte le même nom si elle n’est pas utilisée.

>[!NOTE]
When you create a campaign in Adobe Target, it assigns a property called `thirdPartyId t`o each campaign. Lorsque vous supprimez la campagne dans Adobe Target, `thirdPartyId` n’est pas supprimé. Vous ne pouvez pas réutiliser la propriété `thirdPartyId` pour des campagnes de différents types (AB, XT) et elle ne peut pas être supprimée manuellement. Pour éviter ce problème, attribuez un nom unique à chaque campagne ; les noms de campagne ne peuvent donc pas être réutilisés dans différents types de campagne.
Si vous utilisez le même nom dans le même type de campagne, vous remplacerez la campagne existante.
Lors de la synchronisation, si le message d’erreur « Échec de la demande. `thirdPartyId` existe déjà » s’affiche, modifiez le nom de la campagne et resynchronisez-la.

