---
title: Création de formulaires Adobe Campaign dans AEM
description: AEM vous permet de créer et d’utiliser sur votre site web des formulaires qui interagissent avec Adobe Campaign. Vous pouvez insérer des champs spécifiques dans vos formulaires et les mapper à la base de données d’Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 90%

---

# Création de formulaires Adobe Campaign dans AEM{#creating-adobe-campaign-forms-in-aem}

AEM vous permet de créer et d’utiliser sur votre site web des formulaires qui interagissent avec Adobe Campaign. Vous pouvez insérer des champs spécifiques dans vos formulaires et les mapper à la base de données d’Adobe Campaign.

Vous pouvez gérer les nouveaux abonnements aux contacts, les désabonnements et les données de profil utilisateur, tout en intégrant leurs données dans votre base de données d’Adobe Campaign.

Pour utiliser des formulaires d’Adobe Campaign dans AEM, suivez les étapes décrites dans ce document :

1. Rendez un modèle disponible.
1. Créez un formulaire.
1. Modifiez le contenu du formulaire.

Trois types de formulaires, spécifiques à Adobe Campaign, sont disponibles par défaut :

* Enregistrement d’un profil
* Abonnement à un service
* Désabonnement d’un service

Ces formulaires définissent un paramètre d’URL qui accepte la clé primaire chiffrée d’un profil d’Adobe Campaign. En fonction de ce paramètre d’URL, le formulaire met à jour les données du profil d’Adobe Campaign associé.

Bien que la création de ces formulaires se fasse indépendamment, dans un cas d’utilisation classique, vous générez un lien personnalisé vers une page de formulaire dans le contenu de la newsletter, de sorte que les destinataires puissent ouvrir le lien et ajuster les données de leur profil (désabonnement, abonnement ou mise à jour de leur profil).

Le formulaire est automatiquement mis à jour en fonction de l’utilisateur ou de l’utilisatrice. Pour plus d’informations, reportez-vous à la rubrique [Modification du contenu d’un formulaire](#editing-form-content).

## Rendre un modèle disponible {#making-a-template-available}

Avant de pouvoir créer des formulaires spécifiques à Adobe Campaign, vous devez rendre les différents modèles disponibles dans votre application AEM.

Pour ce faire, consultez la [Documentation relative aux modèles](/help/sites-developing/page-templates-static.md#templateavailability).

Tout d’abord, vérifiez que la connexion entre les instances de création et de publication et Adobe Campaign est bonne. Voir [Intégration à Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Intégration à Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Vérifiez que la propriété **acMapping** sur le nœud **jcr:content** de la page est définie sur **mapRecipient** ou **profile**, lorsque vous utilisez respectivement Adobe Campaign 6.1.x ou Adobe Campaign Standard.
>

### Création d’un formulaire {#creating-a-form}

1. Démarrez dans siteadmin.
1. Parcourez l’arborescence jusqu’à atteindre l’emplacement où vous souhaitez créer le formulaire dans le site Web sélectionné.
1. Sélectionnez **Nouveau** > **Nouvelle page…**.
1. Sélectionnez le modèle **Profil Adobe Campaign (AC 6.1)** ou **Profil Adobe Campaign (ACS)** et saisissez les propriétés de la page.

   >[!NOTE]
   >
   >Si le modèle n’est pas disponible, reportez-vous au [Mettre un modèle à disposition](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) .

1. Cliquez sur **Créer** pour créer le formulaire.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Vous pouvez alors [modifier et configurer le contenu de votre formulaire](#editing-form-content).

## Modifier le contenu d’un formulaire {#editing-form-content}

Les formulaires dédiés à Adobe Campaign comportent des composants spécifiques. Ces composants disposent d’une option permettant de lier chaque champ du formulaire à un champ de la base de données Adobe Campaign.

>[!NOTE]
>
>Si le modèle désiré n’est pas disponible, consultez [Rendre un modèle disponible](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Cette section présente uniquement les liens spécifiques à Adobe Campaign. Pour plus d’informations sur l’utilisation des formulaires dans Adobe Experience Manager, consultez [Composants en mode création](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Accédez au formulaire que vous souhaitez modifier.
1. Dans la boîte à outils, sélectionnez **Page** > **Propriétés de page…** et accédez ensuite à l’onglet **Services cloud** de la fenêtre pop-up.
1. Ajoutez le service Adobe Campaign en cliquant sur **Ajouter un service**, puis en sélectionnant la configuration correspondant à votre instance Adobe Campaign dans la liste déroulante du service. Cette configuration est effectuée lors de la configuration de la connexion entre les différentes instances. Pour plus d’informations, consultez [Connexion d’AEM à Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Le cas échéant, déverrouillez la configuration en cliquant sur l’icône en forme de cadenas pour pouvoir ajouter le service Adobe Campaign.

1. Accédez aux paramètres généraux du formulaire à l’aide du bouton **Modifier** situé au début du formulaire. La variable **Formulaire** vous permet de sélectionner une page de remerciement vers laquelle l’utilisateur sera redirigé après avoir validé le formulaire.

   La variable **Avancé** form permet de sélectionner le type de formulaire. Le champ **Options de publication** vous donne le choix entre trois types de formulaires Adobe Campaign :

   * **Adobe Campaign : Enregistrement d’un profil** : permet de créer ou de mettre à jour un ou une destinataire dans Adobe Campaign (valeur par défaut).
   * **Adobe Campaign : Abonnement aux services** : permet de gérer les abonnements d’un ou d’une destinataire dans Adobe Campaign.
   * **Adobe Campaign : Désabonnement des services** : permet d’annuler les abonnements d’un ou d’une destinataire dans Adobe Campaign.

   Le champ **Configuration de l’action** vous permet de spécifier si vous voulez créer le profil cible dans la base de données Adobe Campaign, s’il n’existe pas encore. Pour ce faire, cochez l’option **Créer un utilisateur s’il n’existe pas**.

1. Ajoutez les composants sélectionnés en les faisant glisser depuis la boîte à outils et en les déposant dans le formulaire. Pour plus d’informations sur les composants spécifiques à Adobe Campaign disponibles, reportez-vous à la rubrique [Composants de formulaires d’Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Paramétrez les champs ajoutés en double-cliquant dessus. L’onglet **Adobe Campaign** vous permet de lier le champ à un champ dans le tableau de destinataires Adobe Campaign. Vous pouvez également indiquer si le champ fait partie de la clé de réconciliation qui permet aux destinataires qui sont déjà présents dans la base de données Adobe Campaign d’être reconnus.

   >[!CAUTION]
   >
   >Le **Nom de l’élément** doit être différent pour chaque champ de formulaire. Modifiez-le si nécessaire.
   >
   >Chaque formulaire doit contenir un **Clé de Principal chiffrée** pour gérer correctement les destinataires dans la base de données Adobe Campaign.

1. Activez la page en choisissant **Page** > **Activer la page** dans la boîte à outils. La page est activée sur votre site. Vous pouvez l’afficher en accédant à votre instance de publication AEM. Les données de la base de données d’Adobe Campaign sont mises à jour une fois qu’un formulaire est validé.

## Tester un formulaire {#testing-a-form}

Après avoir créé un formulaire et en avoir modifié le contenu, vous pouvez le tester manuellement pour vérifier s’il fonctionne comme prévu.

>[!NOTE]
>
>Vous devez disposer d’un composant **Clé primaire chiffrée** (EPK) sur chaque formulaire. Dans Composants, sélectionnez Adobe Campaign afin que seuls ces composants soient visibles.
>
>Bien que dans le cadre de cette procédure vous deviez saisir manuellement le numéro EPK, en pratique, les utilisateurs et utilisatrices reçoivent un lien vers cette page (que l’action voulue soit le désabonnement, l’abonnement ou la mise à jour du profil) dans une newsletter. En fonction de l’utilisateur ou de l’utilisatrice, l’EPK se met automatiquement à jour.
>
>Pour créer ce lien, vous utilisez la variable **Identifiant de ressource principale** (Adobe Campaign Standard) ou l’**identifiant chiffré** (Adobe Campaign 6.1) (par exemple, dans un composant **Texte et personnalisation (Campaign)**), qui est lié à l’EPK dans Adobe Campaign.

Pour ce faire, vous devez obtenir manuellement l’EPK d’un profil Adobe Campaign, puis l’ajouter à l’URL :

1. Pour obtenir la clé primaire chiffrée (EPK) d’un profil Adobe Campaign :

   * Dans Adobe Campaign Standard, accédez à **Profils et audiences** > **Profils**, qui répertorie les profils existants. Assurez-vous que le tableau contient le champ **Identifiant de ressource principale** dans l’une de ses colonnes (cela peut être configuré en cliquant/appuyant sur **Configurer la liste**). Copiez l’identifiant de ressource principale du profil souhaité.
   * Dans Adobe Campaign 6.11, accédez à **Profils et cibles** > **Destinataires** où les profils existants sont répertoriés. Assurez-vous que le tableau contient le champ **Identifiant chiffré** dans l’une de ses colonnes (cela peut être configuré en cliquant avec le bouton droit sur une entrée et en choisissant **Configurer la liste…**). Copiez l’identifiant chiffré du profil souhaité.

1. Dans AEM, ouvrez la page du formulaire sur l’instance de publication et ajoutez l’EPK de l’étape 1 comme paramètre d’URL. Utilisez le même nom que celui précédemment défini dans le composant lors de la création du formulaire (par exemple, `?epk=...`).
1. Le formulaire peut maintenant être utilisé pour modifier les données et abonnements associés au profil Adobe Campaign lié. Après avoir modifié certains champs et envoyé le formulaire, vous pouvez vérifier dans Adobe Campaign que les données appropriées ont été mises à jour.

Les données de la base de données d’Adobe Campaign sont mises à jour une fois qu’un formulaire est validé.
