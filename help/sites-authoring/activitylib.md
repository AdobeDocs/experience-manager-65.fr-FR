---
title: Gestion des activités
seo-title: Managing Activities
description: La console Activités vous permet de créer, d’organiser et de gérer les activités marketing de vos marques.
seo-description: The Activities console enables you to create, organize, and manage the marketing activities of your brands
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
exl-id: f510ca08-977d-45d5-86af-c4b7634b01ba
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1937'
ht-degree: 81%

---

# Gestion des activités{#managing-activities}

La console Activités vous permet de créer, d’organiser et de gérer les [activités](/help/sites-authoring/personalization.md#activities) marketing de vos marques :

* Ajoutez des marques.
* Pour chaque marque, ajoutez et configurez les activités.
* Gérez les activités.

>[!NOTE]
>
>Si vous utilisez Adobe Target comme moteur de ciblage, vous pouvez également [afficher les données de performances de vos activités](#viewing-performance-and-converting-winning-experiences-a-b-test). Si vous utilisez des tests A/B, vous pouvez [convertir les expériences gagnantes](#viewing-performance-and-converting-winning-experiences-a-b-test).

Dans la console Activités, les activités sont organisées par marque. Vous pouvez utiliser des marques et des dossiers pour structurer l’organisation de vos activités. Pour accéder à la console Activités, appuyez/cliquez sur **Personnalisation**, puis sur **Activités**.

Les activités sont disponibles en mode Ciblage pour [créer du contenu ciblé](/help/sites-authoring/content-targeting-touch.md), où vous pouvez également créer des activités. Les activités que vous créez en mode ciblage apparaissent dans la console Activités.

Les activités sont affichées avec un libellé décrivant le type d’activité défini :

* XT : ciblage d’expérience Adobe Target
* A/B : tests A/B Adobe Target
* AEM - Ciblage Adobe Experience Manager (contexthub ou piloté par clientcontext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Les types d’activités disponibles sont déterminés par ce qui suit :
>
>* Si l’option **xt_only** est activée sur le client Adobe Target (clientcode) utilisé sur AEM pour se connecter à Adobe Target, vous pouvez créer **uniquement** des activités XT dans AEM.
>
>* Si la variable **xt_only** options est **not** activée sur le client Adobe Target (clientcode), vous pouvez créer **both** Activités XT et A/B dans AEM.
>
>**Remarque :** L’option **xt_only** est un paramètre appliqué à un certain client Adobe Target (clientcode) et peut uniquement être modifiée directement dans Adobe Target. Vous ne pouvez pas activer ni désactiver cette option dans AEM.

>[!CAUTION]
>
>Sécurisez le nœud de paramètres d’activité **cq:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les personnes utilisatrices normales. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.
>
>Voir [Conditions préalables à l’intégration à Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) pour plus d’informations.

## Création d’une marque à l’aide de la console Activités {#creating-a-brand-using-the-activities-console}

Créez une marque pour laquelle vous souhaitez gérer les activités marketing.

Quand vous créez une marque avec la console Activités, elle apparaît également dans la [console Offres](/help/sites-authoring/offerlib.md) où vous pouvez créer des offres pour les expériences de vos activités.

1. Dans la console Navigation, cliquez sur **Personnalisation**. Cliquez sur **Activités**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. Dans la console Activités, cliquez sur **Créer** then **Créer une marque**.
1. Sélectionnez le modèle de marque et cliquez sur **Suivant**.
1. Saisissez le titre de la marque qui apparaîtra dans les consoles Activités et Offres. Vous pouvez également saisir ou sélectionner une ou plusieurs balises à associer à la marque.
1. Cliquez sur **Créer**. Votre marque apparaît dans la console Activités.

## Ajout/modification d’une activité à l’aide de la console Activités {#adding-editing-an-activity-using-the-activities-console}

Ajoutez une activité ou modifiez une activité existante pour concentrer vos efforts marketing sur des audiences spécifiques. Lorsque vous créez/modifiez une activité, vous spécifiez les informations suivantes :

* **Nom :** nom de l’activité.
* **Moteur de ciblage :** [AEM](/help/sites-authoring/personalization.md#aem) ou [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) comme moteur du contenu ciblé.

* **Sélectionnez une configuration Target :** (Adobe Target uniquement) Configuration du cloud que cette activité doit utiliser pour se connecter à Adobe Target. Cette option s’affiche uniquement lorsque Adobe Target est sélectionné pour le moteur de ciblage.
* **Type d’activité :** test A/B ou ciblage de l’expérience.
* **Objectif :** (facultatif) description de l’activité.
* **Expériences :** correspond aux noms d’audience et aux segments marketing que vous ciblez.
* **Pourcentages de trafic :** si Test A/B est sélectionné, vous pouvez modifier le volume de trafic (en pourcentage) affecté à chaque expérience.
* **Durée :** période d’application de l’activité.
* **Priorité :** priorité relative de l’activité. Lorsque les activités fournissent du contenu pour les mêmes segments d’utilisateurs, l’activité de priorité supérieure est prioritaire.
* **Mesure de l’objectif :** si Adobe Target est sélectionné comme moteur de ciblage, vous pouvez ajouter des mesures de succès à l’activité. Une mesure de succès est requise.

>[!NOTE]
>
>Les nouvelles activités Adobe Target doivent être ***créées*** dans l’éditeur de contenu ciblé et non dans la console **Activités**, car la synchronisation avec Adobe Target échouera.
>
>Vous pouvez toutefois modifier les activités Adobe Target existantes dans la console.

Pour ajouter une activité :

1. Cliquez sur la marque pour laquelle vous créez l’activité, puis sur **Créer** puis **Créer une activité**. Si vous effectuez une modification, sélectionnez l’activité, puis cliquez sur **Modifier**.
1. Indiquez les informations suivantes, puis cliquez sur **Suivant**:

   * Un nom pour l’activité.
   * Le moteur de ciblage à utiliser. ContextHub (AEM) est sélectionné par défaut. Si vous devez utiliser Adobe Target, créez l’activité dans l’éditeur de contenu ciblé.
   * Si vous avez sélectionné Adobe Target comme moteur de ciblage, sélectionnez/modifiez la configuration cloud à utiliser pour vous connecter à Adobe Target. (Veillez à ne pas sélectionner un framework que vous avez créé pour votre configuration cloud.)
   * (Facultatif) L’objectif ou la description de l’activité.
   * Sélectionnez le type d’activité.

1. Ajoutez une ou plusieurs expériences à l’activité. Cliquez sur **Ajouter une expérience**.
1. Si vous utilisez le ciblage AEM ou le ciblage d’expérience Adobe Target :

   1. Cliquez sur **Sélectionner l’audience **et sélectionnez le segment ciblé par votre expérience.
   1. Cliquez sur **Ajouter une expérience**, saisissez un nom, puis cliquez sur **OK**.

   1. Cliquez sur **Suivant**.

   Si vous utilisez des tests A/B Adobe Target :

   1. Cliquez sur le crayon dans la zone audiences pour sélectionner une audience.
   1. Cliquez sur **Ajouter une expérience**, saisissez un nom, puis cliquez sur **OK**.

   1. Saisissez le pourcentage du trafic qui affiche chaque expérience.
   1. Cliquez sur **Suivant**.

1. Pour spécifier le moment où l’activité commence, utilisez le menu déroulant **Démarrer** pour sélectionner l’une des valeurs suivantes :

   * **Après activation :** l’activité commence lorsque la page contenant le contenu ciblé est activée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, cliquez sur l’icône du calendrier, sélectionnez une date et indiquez l’heure de début de l’activité.

1. Pour spécifier le moment où l’activité se termine, utilisez le menu déroulant Fin pour sélectionner l’une des valeurs suivantes :

   * **Lorsqu’elle est désactivée** : l’activité se termine lorsque la page qui contient le contenu ciblé est désactivée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, cliquez sur l’icône du calendrier, sélectionnez une date et indiquez l’heure de fin de l’activité.

1. Pour spécifier une priorité pour l’activité, utilisez le curseur pour sélectionner l’une des options suivantes : **Faible**, **Normale** ou **Élevée**.
1. Si vous utilisez Adobe Target comme moteur de ciblage, sélectionnez ce que vous souhaitez mesurer avec cette activité. Voir [Configuration de l’activité et définition des objectifs](/help/sites-authoring/content-targeting-touch.md) pour plus d’informations sur les mesures de succès disponibles. Sélectionnez au moins un objectif.
1. Cliquez sur **Enregistrer**.

   >[!NOTE]
   >
   >Après avoir créé une activité, vous devez la publier afin qu’elle soit disponible.

## Publication et dépublication des activités {#publishing-and-unpublishing-activities}

Vous devez publier les activités pour les rendre disponibles. À l’inverse, vous pouvez rendre les activités indisponibles en les dépubliant.

>[!NOTE]
>
>Lorsque vous dépubliez une activité, l’état de l’activité ne change que si vous actualisez la page.

Pour publier ou dépublier une activité :

1. Cliquez sur la marque, puis sur la zone contenant l’activité que vous souhaitez publier ou dont vous souhaitez annuler la publication.
1. Cliquez sur l’icône en regard de l’activité ou des activités que vous souhaitez publier ou dont vous souhaitez annuler la publication.

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Pour publier, cliquez sur **Publier**. Pour annuler la publication, cliquez sur **Dépublier**. Votre activité ou vos activités sont publiées ou dépubliées et leur statut change dans la console Activités (une actualisation peut s’avérer nécessaire).

## Activités sur les instances de création et de publication {#activities-on-author-and-publish-instances}

Lors de l’activation d’une activité qui utilise le moteur ciblé Adobe Target, une seconde activité est créée sur l’instance de publication :

* L’activité sur l’instance de création effectue le suivi de l’activité sur l’instance de création et est utile pour simuler l’expérience des visiteurs. Les analyses enregistrées pour cette activité ne reflètent que ce qui se produit sur l’instance de création.
* L’activité sur l’instance de publication reflète l’activité sur le serveur de publication et y répond. Il s’agit de l’activité qui s’exécute sur le site Web public. Seule l’activité de publication est pertinente pour le suivi et l’analyse de l’utilisation du site public réel.

## Affichage des performances et conversion des expériences gagnantes (test A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Vous pouvez voir les performances de n’importe quelle activité Adobe Target (XT ou AB). Si vous utilisez des tests A/B, vous pouvez également convertir l’expérience gagnante, qui devient alors l’expérience par défaut.

Pour afficher les performances des activités et convertir les expériences gagnantes :

1. Dans **Personnalisation**, cliquez sur **Activités** pour accéder au **Activités** console.
1. Cliquez sur la marque pour laquelle vous souhaitez afficher les activités.
1. Sélectionnez l’activité et cliquez sur **Afficher les propriétés** et cliquez sur le bouton **Rapports** et sélectionnez l’activité pour laquelle vous souhaitez afficher les performances/convertir des expériences gagnantes. Les données de performances sont affichées.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Cliquez sur le bouton **Pousser l’expérience gagnante** lien pour transmettre cette expérience comme expérience par défaut.

   La conversion de l’expérience gagnante effectue les opérations suivantes :

   * Elle désactive l’activité en cours.
   * Elle modifie toutes les pages et remplace le contenu ciblé par le contenu de l’expérience gagnante. Le contenu de l’expérience gagnante devient une partie de la page normale **sans** ciblage.

   ![chlimage_1-116](assets/chlimage_1-116.png)

   Une expérience gagnante est l’expérience qui génère le plus d’effet élévateur dans les rapports, en fonction du taux de conversion.

1. Cliquez sur **Oui** pour confirmer que vous souhaitez convertir le gagnant, en désactivant l’expérience actuelle et en la remplaçant par le contenu de l’expérience gagnante.

## Synchronisation des activités avec Adobe Target {#synchronizing-activities-with-adobe-target}

Les activités qui utilisent le moteur de ciblage Adobe Target sont synchronisées avec les campagnes Adobe Target. Une activité est automatiquement synchronisée dans Adobe Target lorsque les conditions suivantes sont remplies :

* L’activité contient au moins une expérience.
* Au moins une expérience contient un segment mappé et une offre.
* Chaque expérience de l’activité doit comporter le même nombre d’offres.

Ces conditions s’appliquent aux activités sur les instances de création et de publication.

Lors de la synchronisation d’une activité, une campagne correspondante est créée dans Adobe Target :

* Les activités sur l’instance de publication portent le même nom que la campagne Adobe Target correspondante.
* Les activités sur l’instance de création correspondent à des campagnes Target du même nom avec le suffixe `_author`.

![chlimage_1-117](assets/chlimage_1-117.png)

Les activités _author sont synchronisées immédiatement lorsque l’activité est modifiée. La synchronisation immédiate permet la simulation des activités avec ClientContext ou ContextHub.

Les activités de publication sont synchronisées lorsque l’activité est publiée sur l’instance de publication AEM.

## Résolution des problèmes de synchronisation d’activité {#troubleshooting-activity-synchronization}

Lorsque AEM synchronise une activité avec Adobe Target, AEM ajoute une propriété appelée `thirdPartyId`. La valeur de cette propriété est basée sur le chemin de l’activité dans le référentiel AEM. Dans Adobe Target, les campagnes ne peuvent avoir la même valeur pour la propriété `thirdPartyId`. Par conséquent, une activité ne se synchronise pas si une campagne existante (d’un autre type A/B ou XT) dans Adobe Target utilise la même valeur pour `thirdPartyId`.

Cette situation peut se produire dans les cas suivants :

1. Une activité est créée et synchronisée avec Adobe Target.
1. Sur une autre instance AEM, une activité est créée sous la même marque et avec le même nom. La synchronisation de cette activité échoue.

Cette situation peut également se produire dans les cas suivants :

1. Une activité est créée et synchronisée avec Adobe Target. L’activité est alors supprimée sur AEM.
1. Une activité est créée sous la même marque et avec le même nom que l’activité supprimée. La synchronisation de cette activité échoue.

Pour éviter des problèmes de synchronisation, utilisez toujours des noms uniques pour les activités. Si une activité ne se synchronise pas, vous pouvez supprimer la campagne dans Adobe Target qui porte le même nom si elle n’est pas utilisée.

>[!NOTE]
>
>Lorsque vous créez une campagne dans Adobe Target, elle affecte la propriété `thirdPartyId t` à chaque campagne. Lorsque vous supprimez la campagne dans Adobe Target, `thirdPartyId` n’est pas supprimé. Vous ne pouvez pas réutiliser la propriété `thirdPartyId` pour des campagnes de différents types (AB, XT) et elle ne peut pas être supprimée manuellement. Pour éviter ce problème, attribuez un nom unique à chaque campagne. Les noms de campagne ne peuvent pas être réutilisés dans différents types de campagne.
>
>Si vous utilisez le même nom dans le même type de campagne, vous remplacerez la campagne existante.
>
>Lors de la synchronisation, si le message d’erreur « Échec de la demande. `thirdPartyId` existe déjà » s’affiche, modifiez le nom de la campagne et resynchronisez-la.
