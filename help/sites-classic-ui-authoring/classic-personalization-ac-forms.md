---
title: Création de formulaires Adobe Campaign dans AEM
seo-title: Création de formulaires Adobe Campaign dans AEM
description: AEM vous permet de créer et d’utiliser des formulaires qui interagissent avec Adobe Campaign sur votre site web. Vous pouvez insérer des champs spécifiques dans vos formulaires et les mapper à la base de données Adobe Campaign.
seo-description: AEM vous permet de créer et d’utiliser des formulaires qui interagissent avec Adobe Campaign sur votre site web. Vous pouvez insérer des champs spécifiques dans vos formulaires et les mapper à la base de données Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 63%

---


# Création de formulaires Adobe Campaign dans AEM{#creating-adobe-campaign-forms-in-aem}

AEM vous permet de créer et d’utiliser des formulaires qui interagissent avec Adobe Campaign sur votre site web. Vous pouvez insérer des champs spécifiques dans vos formulaires et les mapper à la base de données Adobe Campaign.

Vous pouvez également gérer les nouveaux abonnements des contacts, les désabonnements et les données de profil utilisateur, tout en intégrant leurs données dans votre base de données Adobe Campaign.

Pour utiliser des formulaires Adobe Campaign dans AEM, suivez les étapes décrites dans ce document :

1. Rendre un modèle disponible.
1. Créer un formulaire.
1. Modifier le contenu du formulaire.

Trois types de formulaires, spécifiques à Adobe Campaign, sont disponibles par défaut :

* Enregistrement d’un profil
* Abonnement à un service
* Désabonnement d’un service

Ces formulaires définissent un paramètre d’URL qui accepte la clé primaire chiffrée d’un profil Adobe Campaign. Selon ce paramètre d’URL, le formulaire met à jour les données du profil Adobe Campaign associé.

Même si vous créez ces formulaires individuellement, dans un cas d’utilisation standard, vous générez un lien personnalisé sur une page de formulaire à l’intérieur du contenu de la newsletter, afin que les destinataires puissent ouvrir le lien et modifier les données de leur profil (qu’il s’agisse pour eux de se désabonner, de s’abonner ou de mettre à jour leur profil).

Le formulaire est mis à jour automatiquement en fonction de l’utilisateur. Voir [Modification du contenu d’un formulaire](#editing-form-content) pour plus d’informations.

## Rendre un modèle disponible {#making-a-template-available}

Avant de pouvoir créer des formulaires spécifiques à Adobe Campaign, vous devez rendre les différents modèles disponibles dans votre application AEM.

Pour ce faire, consultez la [documentation sur les modèles](/help/sites-developing/page-templates-static.md#templateavailability).

Tout d’abord, vérifiez la connexion entre les instances de création et de publication et assurez-vous qu’Adobe Campaign est en cours d’exécution. Voir [Intégration à Adobe Campaign standard](/help/sites-administering/campaignstandard.md) ou [Intégration à Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Vérifiez que la propriété **acMapping** sur le nœud **jcr:content** de la page est définie sur **mapRecipient** ou **profile**, lorsque vous utilisez Adobe Campaign 6.1.x ou Adobe Campaign standard, respectivement.


### Création d’un formulaire {#creating-a-form}

1. Commencez dans siteadmin.
1. Parcourez l’arborescence jusqu’à atteindre l’emplacement où vous souhaitez créer le formulaire dans le site web sélectionné.
1. Sélectionnez **Nouvelle** > **Nouvelle page...**.
1. Sélectionnez le modèle **Profil Adobe Campaign (AC 6.1)** ou **Profil Adobe Campaign (ACS)** et saisissez les propriétés de la page.

   >[!NOTE]
   >
   >Si le modèle n’est pas disponible, consultez la section [Mise à disposition d’un modèle](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

1. Cliquez sur **Créer** pour créer le formulaire.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Vous pouvez ensuite [modifier et configurer le contenu de votre formulaire](#editing-form-content). 

## Modification du contenu d’un formulaire  {#editing-form-content}

Les formulaires dédiés à Adobe Campaign présentent des composants spécifiques. Ces composants disposent d’une option pour vous permettre de lier chaque champ du formulaire à un champ dans la base de données Adobe Campaign.

>[!NOTE]
>
>Si le modèle souhaité n’est pas disponible, voir [Mise à disposition d’un modèle](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Cette section présente uniquement les liens spécifiques à Adobe Campaign. Pour plus d’informations sur une présentation plus générale de l’utilisation des formulaires dans Adobe Experience Manager, voir [Composants du mode éditeur](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Accédez au formulaire que vous souhaitez modifier.
1. Dans la boîte à outils, sélectionnez **Page** > **Propriétés de la page...** puis accédez à l&#39;onglet **Cloud Services** de la fenêtre contextuelle.
1. Ajoutez le service Adobe Campaign en cliquant sur **Ajouter le service**, puis en sélectionnant la configuration qui correspond à votre instance Adobe Campaign dans la liste déroulante du service. Cette configuration est effectuée lors de la configuration de la connexion entre les différentes instances. Pour plus d’informations, voir [Connexion de l’AEM à Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Le cas échéant, déverrouillez la configuration en cliquant sur l’icône en forme de cadenas pour pouvoir ajouter le service Adobe Campaign.

1. Accédez aux paramètres généraux du formulaire à l’aide du bouton **Modifier** situé en début du formulaire. L&#39;onglet **Formulaire** vous permet de sélectionner une page de remerciement à laquelle l&#39;utilisateur sera redirigé après avoir validé le formulaire.

   Le formulaire **Advanced** vous permet de sélectionner le type de formulaire. Le champ **Options de publication** vous donne le choix entre trois types de formulaires Adobe Campaign :

   * **Adobe Campaign : enregistrer le profil** : vous permet de créer ou de mettre à jour un destinataire dans Adobe Campaign (valeur par défaut).
   * **Adobe Campaign : s’abonner aux services** : vous permet de gérer les abonnements d’un destinataire dans Adobe Campaign.
   * **Adobe Campaign : se désabonner des services** : vous permet d’annuler les abonnements d’un destinataire dans Adobe Campaign.

   Le champ **Configuration de l&#39;action** vous permet de spécifier si vous souhaitez ou non créer le profil de destinataire dans la base de données Adobe Campaign s&#39;il n&#39;existe pas encore. Pour ce faire, cochez l’option **Créer un utilisateur s’il n’existe pas**.

1. Ajoutez vos composants sélectionnés en les faisant glisser depuis la boîte à outils et en les plaçant dans le formulaire. Pour plus d’informations sur les éléments spécifiques d’Adobe Campaign disponibles, voir [Composants de formulaire Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configurez les champs ajoutés en cliquant deux fois dessus. L’onglet **Adobe Campaign** permet de lier le champ à un champ de la table destinataire Adobe Campaign. Vous pouvez également indiquer si le champ fait partie de la clé de réconciliation qui permet aux destinataires qui sont déjà présents dans la base de données Adobe Campaign d’être reconnus.

   >[!CAUTION]
   >
   >Le **nom de l’élément** doit être différent pour chaque champ de formulaire. Modifiez-le si nécessaire.
   >
   >Chaque formulaire doit contenir un composant **Clé de Principal chiffrée** afin de gérer correctement les destinataires dans la base de données Adobe Campaign.

1. Activez la page en sélectionnant **Page** > **Activer la page** dans la boîte à outils. La page est activée sur votre site. Vous pouvez l’afficher en accédant à votre instance de publication AEM. Les données de la base de données Adobe Campaign sont mises à jour une fois qu’un formulaire est validé.

## Test d’un formulaire  {#testing-a-form}

Une fois que vous avez créé un formulaire et modifié son contenu, il est conseillé de tester manuellement que le formulaire fonctionne comme prévu.

>[!NOTE]
>
>Vous devez disposer d’un composant **Clé de Principal chiffrée** sur chaque formulaire. Dans Composants, sélectionnez Adobe Campaign afin que seuls ces composants soient visibles.
>
>Même si dans cette procédure vous saisissez le numéro d’EPK manuellement, dans la pratique, les utilisateurs recevront un lien vers cette page (pour se désabonner, s’abonner ou mettre à jour leur profil) dans une newsletter. En fonction de l’utilisateur, l’EPK est mis à jour automatiquement.
>
>Pour créer ce lien, vous utilisez la variable **Identificateur de ressource principale**(Adobe Campaign Standard) ou **Identificateur chiffré** (Adobe Campaign 6.1) (par exemple, dans un composant **Texte et personnalisation (Campaign)**), qui pointe vers le epk dans Adobe Campaign.

Pour ce faire, vous devez obtenir manuellement l’EPK d’un profil Adobe Campaign et ensuite l’ajouter à l’URL :

1. Pour obtenir la clé primaire chiffrée (EPK) d’un profil Adobe Campaign :

   * Dans Adobe Campaign Standard - Accédez à **Profils et Audiences** > **Profils**, qui liste les profils existants. Assurez-vous que le tableau affiche le champ **Identifiant de ressource principale** dans une colonne (Vous pouvez le configurer en cliquant/appuyant sur **Configurer la liste**). Copiez l’identifiant de ressource principale du profil souhaité.
   * Dans Adobe Campaign 6.11, accédez à **Profils et Cibles** > **Destinataires**, qui liste les profils existants. Assurez-vous que le tableau affiche le champ **Identificateur chiffré** dans une colonne (Vous pouvez le configurer en cliquant avec le bouton droit sur une entrée et en sélectionnant **Configurer la liste...**). Copiez l’identifiant chiffré du profil souhaité.

1. Dans AEM, ouvrez la page de formulaire sur l’instance de publication et ajoutez l’EPK de l’étape 1 en tant que paramètre d’URL : utilisez le même nom que celui que vous avez précédemment défini dans le composant EPK lors de la création du formulaire (par exemple : `?epk=...`)
1. Le formulaire peut maintenant être utilisé pour modifier les données et les abonnements associés au profil Adobe Campaign lié. Après avoir modifié certains champs et envoyé le formulaire, vous pouvez vérifier dans Adobe Campaign que les données ont été mises à jour.

Les données de la base de données Adobe Campaign sont mises à jour une fois qu’un formulaire est validé.
