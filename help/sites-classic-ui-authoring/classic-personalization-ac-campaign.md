---
title: Utiliser Adobe Campaign 6.1 et Adobe Campaign Standard
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: Vous pouvez créer le contenu d’un e-mail dans AEM et le traiter dans les e-mails Adobe Campaign.
seo-description: You can create email content in AEM and process it in Adobe Campaign emails.
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 52%

---

# Utiliser Adobe Campaign 6.1 et Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Vous pouvez créer le contenu d’un courrier électronique dans AEM et le traiter dans les courriers électroniques Adobe Campaign. À cet effet, vous devez suivrez cette procédure :

1. Créez une newsletter dans AEM à partir d’un modèle spécifique à Adobe Campaign.
1. Sélectionner [un service Adobe Campaign ;](#selectingtheadobecampaigncloudservice) avant de modifier le contenu pour accéder à toutes les fonctionnalités.
1. Modifiez le contenu.
1. Validez le contenu.

Le contenu peut ensuite être synchronisé avec une diffusion dans Adobe Campaign. Des instructions détaillées sont présentées dans ce document.

>[!NOTE]
>
>Avant de pouvoir utiliser cette fonctionnalité, vous devez configurer AEM pour l’intégration à [Adobe Campaign](/help/sites-administering/campaignonpremise.md) ou [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Envoi de contenu d’email via Adobe Campaign {#sending-email-content-via-adobe-campaign}

Après avoir configuré AEM et Adobe Campaign, vous pouvez créer le contenu de diffusion email directement dans AEM, puis le traiter dans Adobe Campaign.

Lorsque vous créez du contenu Adobe Campaign dans AEM, vous devez effectuer une liaison à un service Adobe Campaign avant de modifier le contenu pour accéder à toutes les fonctionnalités.

Deux cas sont possibles :

* Le contenu peut être synchronisé avec une diffusion depuis Adobe Campaign. Vous pouvez ainsi utiliser AEM contenu dans une diffusion.
* (Adobe Campaign on premise uniquement) Le contenu peut être envoyé directement à Adobe Campaign, qui génère automatiquement une nouvelle diffusion email. Ce mode présente des limites.

Des instructions détaillées sont présentées dans ce document.

### Créer du contenu d’e-mail {#creating-new-email-content}

>[!NOTE]
>
>Lorsque vous ajoutez des modèles d’e-mail, veillez à les ajouter sous **/content/campaigns** pour qu’ils soient disponibles.
>

1. Dans AEM, sélectionnez le dossier **Sites web**, puis cherchez dans l’explorateur l’emplacement où sont gérées vos campagnes par e-mail. Dans l’exemple ci-dessous, le nœud concerné est **Sites web** > **Campagnes** > **Geometrixx Outdoors** > **Campagnes par e-mail**.

   >[!NOTE]
   >
   >[Les exemples d’e-mails ne sont disponibles que dans Geometrixx](/help/sites-developing/we-retail.md#weretail). Téléchargez un exemple de contenu Geometrixx à partir du partage de packages.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Pour créer du contenu à diffuser par e-mail, sélectionnez **Nouveau** > **Nouvelle page**.
1. Sélectionnez l’un des modèles disponibles spécifiques à Adobe Campaign, puis renseignez les propriétés générales de la page. Trois modèles sont disponibles par défaut :

   * **Adobe Campaign Email (AC 6.1)** : permet d’ajouter du contenu à un modèle prédéfini avant de l’envoyer vers Adobe Campaign 6.1 pour diffusion.
   * **Adobe Campaign Email (ACS)** : permet d’ajouter du contenu à un modèle prédéfini avant de l’envoyer vers Adobe Campaign Standard pour diffusion.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Cliquez sur **Créer** pour créer un e-mail ou la newsletter.

### Sélection du service cloud et du modèle Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Pour l’intégrer à Adobe Campaign, vous devez ajouter un service cloud Adobe Campaign à la page. Cela vous permet d’accéder à la personnalisation et à d’autres informations Adobe Campaign.

En outre, vous devrez peut-être également sélectionner le modèle Adobe Campaign, modifier l’objet et ajouter du contenu en texte brut pour les utilisateurs qui ne verront pas l’email par HTML.

1. Sélectionnez l’onglet **Page** dans le sidekick, puis sélectionnez **Propriétés de la page.**
1. Sous l’onglet **Services cloud** dans la fenêtre pop-up, sélectionnez **Ajouter un service** pour ajouter le service Adobe Campaign et cliquez sur **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Sélectionnez la configuration qui correspond à votre instance Adobe Campaign dans la liste déroulante, puis cliquez sur **OK**.

   >[!NOTE]
   >
   >Veillez à appuyer/cliquer sur **OK** ou **Appliquer** après avoir ajouté le service cloud. Cela active la variable **Adobe Campaign** pour fonctionner correctement.

1. Si vous souhaitez appliquer un modèle de diffusion par e-mail spécifique (à partir d’Adobe Campaign), autre que le modèle d’**e-mail** par défaut, sélectionnez de nouveau **Propriétés de la page**. Sous l’onglet **Adobe Campaign**, entrez le nom interne du modèle de diffusion par e-mail dans l’instance Adobe Campaign associée.

   Dans Adobe Campaign Standard, le modèle est **Diffusion avec contenu AEM**. Dans Adobe Campaign 6.1, le modèle est **Diffusion Email avec contenu AEM**.

   Lorsque vous sélectionnez le modèle, AEM active automatiquement les composants **Newsletter Adobe Campaign**.

### Editer le contenu d&#39;un email {#editing-email-content}

Vous pouvez modifier le contenu d’un email dans l’interface utilisateur classique ou dans l’interface utilisateur optimisée pour les écrans tactiles.

1. Entrez l’objet et la version du texte du e-mail en sélectionnant **Propriétés de la page** > **E-mail** à partir de la palette.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Modifiez le contenu d’un email en ajoutant les éléments que vous souhaitez parmi ceux disponibles dans le sidekick. Pour ce faire, faites-les glisser et déposez-les. Cliquez deux fois ensuite sur l’élément à modifier.

   Vous pouvez par exemple ajouter du texte contenant des champs de personnalisation.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Pour une description des composants disponibles pour les campagnes par newsletter et par e-mail, reportez-vous à la section [Composants Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Insérer une personnalisation {#inserting-personalization}

Lorsque vous éditez votre contenu, vous pouvez insérer :

* Des champs de contexte Adobe Campaign. Il s’agit de champs que vous pouvez insérer dans votre texte qui s’adaptera en fonction des données du destinataire (prénom, nom ou toute donnée de la dimension cible, par exemple).
* Des blocs de personnalisation Adobe Campaign. Ce sont des blocs de contenu prédéfini, qui ne sont pas liés aux données du destinataire, comme le logo d’une marque ou un lien vers une page miroir.

Voir [Composants Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) pour une description complète des composants de Campaign.

>[!NOTE]
>
>* Uniquement les champs d&#39;Adobe Campaign **Profils** la dimension de ciblage est prise en compte.
>* Lorsque vous affichez des propriétés à partir de l’onglet **Sites**, vous n’avez pas accès aux champs de contexte Adobe Campaign. Vous pouvez y accéder directement à partir de l’e-mail en cours de modification.
>

1. Insérez un nouveau composant **Newsletter** > **Texte et personnalisation (Campaign)**.
1. Ouvrez le composant en double-cliquant dessus. La variable **Modifier** dispose d’une fonctionnalité permettant d’insérer les éléments de personnalisation.

   >[!NOTE]
   >
   >Les champs de contexte disponibles correspondent au **Profils** dimension de ciblage dans Adobe Campaign.
   >
   >Reportez-vous à la section [Liaison d’une page AEM à un e-mail Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Sélectionnez **Contexte client** dans le sidekick pour tester les champs de personnalisation à l’aide des données figurant dans les profils de persona.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Une fenêtre s’affiche et vous permet de sélectionner le personnage de votre choix. Les champs de personnalisation sont remplacés automatiquement par les données du profil sélectionné.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Aperçu d’une newsletter {#previewing-a-newsletter}

Vous pouvez prévisualiser l’aspect de la newsletter et prévisualiser la personnalisation.

1. Ouvrez la newsletter pour laquelle vous souhaitez afficher un aperçu et cliquez sur Aperçu (la loupe) pour réduire le sidekick.
1. Cliquez sur l’une des icônes de client de messagerie pour découvrir comment se présente votre newsletter dans les différents clients de messagerie.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Développez le sidekick pour recommencer la modification.

### Valider le contenu dans AEM {#approving-content-in-aem}

Une fois le contenu terminé, vous pouvez lancer le processus de validation. Accédez à l’onglet **Workflow** de la palette et sélectionnez le workflow **Approuver pour Adobe Campaign**.

Ce workflow prêt à l’emploi comporte deux étapes : révision, puis approbation ou révision puis rejet. Néanmoins, ce workflow peut être étendu et adapté à une procédure plus complexe.

![chlimage_1-182](assets/chlimage_1-182.png)

Pour approuver le contenu pour Adobe Campaign, appliquez le workflow en sélectionnant **Workflow** dans le sidekick et en sélectionnant **Approuver pour Adobe Campaign** et cliquez sur **Démarrer le workflow**. Parcourez les étapes et approuvez le contenu. Vous pouvez également rejeter le contenu en sélectionnant **Rejeter** au lieu d’**Approuver** dans la dernière étape du workflow.

![chlimage_1-183](assets/chlimage_1-183.png)

Une fois le contenu approuvé, il apparaît comme approuvé dans Adobe Campaign. L&#39;email peut alors être envoyé.

Dans Adobe Campaign Standard :

![chlimage_1-184](assets/chlimage_1-184.png)

Dans Adobe Campaign 6.1 :

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>Le contenu non validé peut être synchronisé avec une diffusion dans Adobe Campaign mais la diffusion ne peut pas être exécutée. Seul le contenu validé peut être envoyé via les diffusions Campaign.

## Liaison d’AEM avec Adobe Campaign Standard et Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Pour plus d’informations, consultez [Liaison d’AEM à Adobe Campaign Standard et à Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) sous [Utilisation d’Adobe Campaign 6.1 et d’Adobe Campaign Standard](/help/sites-authoring/campaign.md) dans la documentation de création standard.
