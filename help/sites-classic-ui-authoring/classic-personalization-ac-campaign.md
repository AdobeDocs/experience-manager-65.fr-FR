---
title: Utiliser Adobe Campaign 6.1 et Adobe Campaign Standard
description: Vous pouvez créer le contenu d’un e-mail dans AEM et le traiter dans les e-mails Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 100%

---

# Utiliser Adobe Campaign 6.1 et Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Vous pouvez créer le contenu d’un courrier électronique dans AEM et le traiter dans les courriers électroniques Adobe Campaign. À cet effet, vous devez suivrez cette procédure :

1. Créez une newsletter dans AEM à partir d’un modèle spécifique à Adobe Campaign.
1. Sélectionnez [un service Adobe Campaign](#selectingtheadobecampaigncloudservice) avant de modifier le contenu pour accéder à toutes les fonctionnalités.
1. Modifiez le contenu.
1. Validez le contenu.

Le contenu peut ensuite être synchronisé avec une diffusion dans Adobe Campaign. Ce document contient des instructions détaillées.

>[!NOTE]
>
>Avant de pouvoir utiliser cette fonctionnalité, vous devez configurer AEM pour l’intégrer à [Adobe Campaign](/help/sites-administering/campaignonpremise.md) ou à [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Envoi de contenu d’e-mail via Adobe Campaign {#sending-email-content-via-adobe-campaign}

Après avoir configuré AEM et Adobe Campaign, vous pouvez créer le contenu de la diffusion par e-mail directement dans AEM, puis le traiter dans Adobe Campaign.

Lorsque vous créez du contenu Adobe Campaign dans AEM, vous devez effectuer une liaison à un service Adobe Campaign avant de modifier le contenu pour accéder à toutes les fonctionnalités.

Deux cas sont possibles :

* Le contenu peut être synchronisé avec une diffusion depuis Adobe Campaign. Vous pouvez ainsi utiliser le contenu AEM dans une diffusion.
* (Adobe Campaign On-Premise uniquement) Le contenu peut être envoyé directement vers Adobe Campaign, qui génère automatiquement une nouvelle diffusion par e-mail. Ce mode présente des limites.

Ce document contient des instructions détaillées.

### Créer du contenu d’e-mail {#creating-new-email-content}

>[!NOTE]
>
>Lorsque vous ajoutez des modèles d’e-mail, veillez à les ajouter sous **/content/campaigns** pour qu’ils soient disponibles.
>

1. Dans AEM, sélectionnez le dossier **Sites web**, puis cherchez dans l’explorateur l’emplacement où sont gérées vos campagnes par e-mail. Dans l’exemple ci-dessous, le nœud concerné est **Sites web** > **Campagnes** > **Geometrixx Outdoors** > **Campagnes par e-mail**.

   >[!NOTE]
   >
   >[Les exemples d’e-mails ne sont disponibles que dans Geometrixx](/help/sites-developing/we-retail.md#weretail). Téléchargez un exemple de contenu Geometrixx à partir du partage de modules.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Pour créer du contenu à diffuser par e-mail, sélectionnez **Nouveau** > **Nouvelle page**.
1. Sélectionnez l’un des modèles disponibles, spécifiques à Adobe Campaign, puis renseignez les propriétés générales de la page. Trois modèles sont disponibles par défaut :

   * **Adobe Campaign Email (AC 6.1)** : permet d’ajouter du contenu à un modèle prédéfini avant de l’envoyer vers Adobe Campaign 6.1 pour diffusion.
   * **Adobe Campaign Email (ACS)** : permet d’ajouter du contenu à un modèle prédéfini avant de l’envoyer vers Adobe Campaign Standard pour diffusion.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Cliquez sur **Créer** pour créer un e-mail ou la newsletter.

### Sélectionner le service cloud et le modèle Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Pour une intégration à Adobe Campaign, vous devez ajouter un service cloud Adobe Campaign à la page. Cela vous permet d’accéder à la personnalisation et à d’autres informations Adobe Campaign.

En outre, vous devrez peut-être également sélectionner le modèle Adobe Campaign, modifier l’objet et ajouter du contenu en texte brut pour les utilisateurs et utilisatrices qui ne verront pas l’e-mail en HTML.

1. Sélectionnez l’onglet **Page** dans le sidekick, puis sélectionnez **Propriétés de la page.**
1. Sous l’onglet **Services cloud** dans la fenêtre pop-up, sélectionnez **Ajouter un service** pour ajouter le service Adobe Campaign et cliquez sur **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Sélectionnez la configuration qui correspond à votre instance Adobe Campaign dans la liste déroulante, puis cliquez sur **OK**.

   >[!NOTE]
   >
   >Veillez à cliquer sur **OK** ou sur **Appliquer** après avoir ajouté le service cloud. Cela permet à l’onglet **Adobe Campaign** de fonctionner correctement.

1. Si vous souhaitez appliquer un modèle de diffusion par e-mail spécifique (à partir d’Adobe Campaign), autre que le modèle d’**e-mail** par défaut, sélectionnez de nouveau **Propriétés de la page**. Sous l’onglet **Adobe Campaign**, entrez le nom interne du modèle de diffusion par e-mail dans l’instance Adobe Campaign associée.

   Dans Adobe Campaign Standard, le modèle est **Diffusion avec contenu AEM**. Dans Adobe Campaign 6.1, le modèle est **Diffusion e-mail avec contenu AEM**.

   Lorsque vous sélectionnez le modèle, AEM active automatiquement les composants **Newsletter Adobe Campaign**.

### Modification du contenu de l’e-mail {#editing-email-content}

Vous pouvez modifier le contenu d’un e-mail dans l’interface utilisateur classique ou dans l’interface utilisateur optimisée pour les écrans tactiles.

1. Entrez l’objet et la version du texte du e-mail en sélectionnant **Propriétés de la page** > **E-mail** à partir de la palette.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Modifiez le contenu d’un e-mail en ajoutant les éléments que vous souhaitez parmi ceux disponibles dans le sidekick. Pour ce faire, faites-les glisser et déposez-les. Double-cliquez ensuite sur l’élément à modifier.

   Vous pouvez par exemple ajouter du texte contenant des champs de personnalisation.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Pour une description des composants disponibles pour les campagnes par newsletter et par e-mail, reportez-vous à la section [Composants Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Insertion d’une personnalisation {#inserting-personalization}

Lorsque vous éditez votre contenu, vous pouvez insérer :

* Des champs de contexte Adobe Campaign. Ce sont des champs que vous pouvez insérer dans votre texte, qui seront adaptés en fonction des données du ou de la destinataire (par exemple, prénom, nom de famille ou données de dimension cible).
* Des blocs de personnalisation Adobe Campaign. Ces blocs de contenu prédéfini ne sont pas liés aux données de la personne destinataire, tels que le logo d’une marque ou un lien vers une page miroir.

Consultez [Composants d’Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) pour une description complète des composants de Campaign.

>[!NOTE]
>
>* Seuls les champs de la dimension de ciblage **Profils** d’Adobe Campaign sont pris en compte.
>* Lorsque vous affichez des propriétés à partir de l’onglet **Sites**, vous n’avez pas accès aux champs de contexte Adobe Campaign. Vous pouvez y accéder directement à partir de l’e-mail en cours de modification.
>

1. Insérez un nouveau composant **Newsletter** > **Texte et personnalisation (Campaign)**.
1. Ouvrez le composant en double-cliquant dessus. La fenêtre **Modifier** dispose d’une fonctionnalité qui vous permet d’insérer des éléments de personnalisation.

   >[!NOTE]
   >
   >Les champs de contexte disponibles correspondent à la dimension de ciblage **Profils** dans Adobe Campaign.
   >
   >Reportez-vous à la section [Liaison d’une page AEM à un e-mail Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Sélectionnez **Contexte client** dans le sidekick pour tester les champs de personnalisation à l’aide des données figurant dans les profils de persona.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Une fenêtre s’affiche et vous permet de sélectionner la personne de votre choix. Les champs de personnalisation sont remplacés automatiquement par les données du profil sélectionné.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Prévisualisation d’une newsletter {#previewing-a-newsletter}

Vous pouvez prévisualiser l’apparence de la newsletter et prévisualiser la personnalisation.

1. Ouvrez la newsletter pour laquelle vous souhaitez afficher un aperçu et cliquez sur Aperçu (la loupe) pour réduire le sidekick.
1. Cliquez sur l’une des icônes de client de messagerie pour découvrir comment se présente votre newsletter dans les différents clients de messagerie.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Développez le sidekick pour recommencer la modification.

### Approbation du contenu dans AEM {#approving-content-in-aem}

Une fois le contenu terminé, vous pouvez lancer le processus d’approbation. Accédez à l’onglet **Workflow** de la palette et sélectionnez le workflow **Approuver pour Adobe Campaign**.

Ce workflow prêt à l’emploi comporte deux étapes : révision, puis approbation ou révision puis rejet. Néanmoins, ce workflow peut être étendu et adapté à une procédure plus complexe.

![chlimage_1-182](assets/chlimage_1-182.png)

Pour approuver le contenu pour Adobe Campaign, appliquez le workflow en sélectionnant **Workflow** dans le sidekick et en sélectionnant **Approuver pour Adobe Campaign** et cliquez sur **Démarrer le workflow**. Parcourez les étapes et approuvez le contenu. Vous pouvez également rejeter le contenu en sélectionnant **Rejeter** au lieu d’**Approuver** dans la dernière étape du workflow.

![chlimage_1-183](assets/chlimage_1-183.png)

Une fois le contenu approuvé, il apparaît comme approuvé dans Adobe Campaign. L’e-mail peut alors être envoyé.

Dans Adobe Campaign Standard :

![chlimage_1-184](assets/chlimage_1-184.png)

Dans Adobe Campaign 6.1 :

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>Le contenu non approuvé peut être synchronisé avec une diffusion dans Adobe Campaign, mais la diffusion ne peut pas être exécutée. Seul le contenu approuvé peut être envoyé via les diffusions Campaign.

## Liaison d’AEM avec Adobe Campaign Standard et Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Pour plus d’informations, consultez [Liaison d’AEM à Adobe Campaign Standard et à Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) sous [Utilisation d’Adobe Campaign 6.1 et d’Adobe Campaign Standard](/help/sites-authoring/campaign.md) dans la documentation de création standard.
