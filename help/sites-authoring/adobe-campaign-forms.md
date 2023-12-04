---
title: Créer des formulaires Adobe Campaign dans Adobe Experience Manager
description: Adobe Experience Manager vous permet de créer et d’utiliser des formulaires qui interagissent avec Adobe Campaign sur votre site web.
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 93%

---

# Création de formulaires Adobe Campaign dans AEM {#creating-adobe-campaign-forms-in-aem}

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

Pour ce faire, consultez la [Documentation relative aux modèles](/help/sites-developing/templates.md#template-availability).

## Création d’un formulaire {#creating-a-form}

Tout d’abord, vérifiez que la connexion entre les instances de création et de publication et Adobe Campaign est bonne. Voir [Intégration à Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Intégration à Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Vérifiez que la propriété **acMapping** sur le nœud **jcr:content** de la page est définie sur **mapRecipient** ou **profile**, lorsque vous utilisez Adobe Campaign Classic ou Adobe Campaign Standard, respectivement.
>

1. Dans AEM, dans Sites, accédez à l’emplacement où vous souhaitez créer une page.
1. Créez une page et sélectionnez **Profil Adobe Campaign Classic** ou **Profil Adobe Campaign Standard** et cliquez sur **Suivant**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si le modèle désiré n’est pas disponible, consultez [Disponibilité des modèles](/help/sites-developing/templates.md#template-availability).

1. Dans le champ **Nom**, ajoutez le nom de la page. Il doit s’agir d’un nom JCR valide.
1. Dans le champ **Titre**, saisissez un titre, puis cliquez sur **Créer**.
1. Ouvrez la page, puis sélectionnez **Ouvrir les propriétés**, ajoutez la configuration Adobe Campaign aux services cloud et cliquez sur la coche pour enregistrer vos modifications.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Sur la page, dans le composant **Début du formulaire**, sélectionnez le type de formulaire : **Abonnement, Désabonnement,** ou **Enregistrement d’un profil**. Vous pouvez uniquement disposer d’un type par formulaire. Vous pouvez désormais [modifier le contenu du formulaire](#editing-form-content).

## Modifier le contenu d’un formulaire {#editing-form-content}

Les formulaires dédiés à Adobe Campaign comportent des composants spécifiques. Ces composants disposent d’une option permettant de lier chaque champ du formulaire à un champ de la base de données Adobe Campaign.

>[!NOTE]
>
>Si le modèle désiré n’est pas disponible, consultez [Rendre un modèle disponible](/help/sites-authoring/adobe-campaign.md).

Cette section présente uniquement les liens spécifiques à Adobe Campaign. Pour plus d’informations sur l’utilisation des formulaires dans Adobe Experience Manager, consultez [Composants en mode création](/help/sites-authoring/default-components-foundation.md).

1. Sélectionnez **Ouvrir les propriétés**, ajoutez la configuration Adobe Campaign aux services cloud et cliquez sur la coche pour enregistrer vos modifications.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Sur la page, dans le composant **Début du formulaire**, cliquez sur l’icône Configuration.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Cliquez sur l’onglet **Avancé** et choisissez le type de formulaire **S’abonner, Se désabonner** ou **Enregistrer le profil** et cliquez sur **OK.** Vous pouvez uniquement disposer d’un type par formulaire.

   * **Adobe Campaign : Enregistrement d’un profil** : permet de créer ou de mettre à jour un ou une destinataire dans Adobe Campaign (valeur par défaut).
   * **Adobe Campaign : Abonnement aux services** : permet de gérer les abonnements d’un ou d’une destinataire dans Adobe Campaign.
   * **Adobe Campaign : Désabonnement des services** : permet d’annuler les abonnements d’un ou d’une destinataire dans Adobe Campaign.

1. Vous devez disposer d’un composant **Clé primaire chiffrée** (EPK) sur chaque formulaire. Ce composant définit le paramètre d’URL utilisé pour accepter la clé primaire chiffrée d’un profil Adobe Campaign. Dans Composants, sélectionnez Adobe Campaign afin que seuls ces composants soient visibles.
1. Faire glisser le composant **Clé de Principal chiffrée** dans le formulaire (n’importe où) et cliquez sur l’icône **Configuration** Icône Dans l’onglet **Adobe Campaign**, indiquez le nom du paramètre d’URL. Cliquez sur la coche pour enregistrer vos modifications.

   Les liens générés vers ce formulaire doivent utiliser ce paramètre d’URL et lui attribuer la clé primaire chiffrée d’un profil Adobe Campaign. La clé primaire chiffrée doit être correctement encodée en URL (pourcentage).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Ajoutez au formulaire autant de composants que vous le souhaitez, tels qu’un champ de texte, un champ de date, un champ de case à cocher, un champ d’option, etc. Pour plus d’informations sur chaque composant, veuillez consulter [Composants de formulaire Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
1. Cliquez sur l’icône Configuration pour ouvrir le composant. Par exemple, dans le composant **Champ de texte (Campaign)**, changez le titre et le texte.

   Cliquez sur **Adobe Campaign** pour mapper le champ de formulaire à une variable de métadonnées Adobe Campaign. Lorsque vous soumettez le formulaire, le champ mappé est mis à jour dans Adobe Campaign. Seuls les champs avec les types correspondants sont disponibles dans le sélecteur de variables (par exemple, les variables de chaîne pour les champs de texte).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Vous pouvez ajouter ou supprimer des champs qui sont affichés dans le tableau Destinataire en suivant les instructions ici :[https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Cliquez sur **Publier la page**. La page est activée sur votre site. Vous pouvez l’afficher en accédant à votre instance de publication AEM. Vous pouvez également [tester un formulaire](#testing-a-form).

   >[!CAUTION]
   >
   >Vous devez fournir des autorisations de lecture à l’utilisateur ou à l’utilisatrice anonyme sur le service cloud pour utiliser les formulaires sur l’instance de publication. Toutefois, gardez en tête les problèmes de sécurité potentiels liés à l’octroi d’autorisations de lecture à l’utilisateur ou à l’utilisatrice anonyme et assurez-vous de les limiter, par exemple en configurant le Dispatcher.

## Tester un formulaire {#testing-a-form}

Après avoir créé un formulaire et en avoir modifié le contenu, vous pouvez le tester manuellement pour vérifier s’il fonctionne comme prévu.

>[!NOTE]
>
>Vous devez disposer d’un composant **Clé primaire chiffrée** (EPK) sur chaque formulaire. Dans Composants, sélectionnez Adobe Campaign afin que seuls ces composants soient visibles.
>
>Bien que dans le cadre de cette procédure vous deviez saisir manuellement le numéro EPK, en pratique, les utilisateurs et utilisatrices reçoivent un lien vers cette page (que l’action voulue soit le désabonnement, l’abonnement ou la mise à jour du profil) dans une newsletter. En fonction de l’utilisateur ou de l’utilisatrice, l’EPK se met automatiquement à jour.
>
>Pour créer ce lien, utilisez la variable **Identifiant de ressource principale** (Adobe Campaign Standard) ou l’**identifiant chiffré** (Adobe Campaign Classic) (par exemple, dans un composant **Texte et personnalisation (Campaign)**), lié à l’EPK dans Adobe Campaign.

Pour ce faire, vous devez obtenir manuellement l’EPK d’un profil Adobe Campaign, puis l’ajouter à l’URL :

1. Pour obtenir la clé primaire chiffrée (EPK) d’un profil Adobe Campaign :

   * Dans Adobe Campaign Standard, accédez à **Profils et audiences** > **Profils**, qui répertorie les profils existants. Assurez-vous que le tableau contient le champ **Identifiant de ressource principale** dans l’une de ses colonnes (cela peut être configuré en cliquant/appuyant sur **Configurer la liste**). Copiez l’identifiant de ressource principale du profil souhaité.
   * Dans Adobe Campaign Classic, accédez à **Profils et cibles** > **Destinataires** où les profils existants sont répertoriés. Assurez-vous que le tableau contient le champ **Identifiant chiffré** dans l’une de ses colonnes (cela peut être configuré en cliquant avec le bouton droit sur une entrée et en choisissant **Configurer la liste…**). Copiez l’identifiant chiffré du profil souhaité.

1. Dans AEM, ouvrez la page du formulaire sur l’instance de publication et ajoutez l’EPK de l’étape 1 comme paramètre d’URL. Utilisez le même nom que celui précédemment défini dans le composant lors de la création du formulaire (par exemple, `?epk=...`).
1. Le formulaire peut maintenant être utilisé pour modifier les données et abonnements associés au profil Adobe Campaign lié. Après avoir modifié certains champs et envoyé le formulaire, vous pouvez vérifier dans Adobe Campaign que les données appropriées ont été mises à jour.

Les données de la base de données d’Adobe Campaign sont mises à jour une fois qu’un formulaire est validé.
