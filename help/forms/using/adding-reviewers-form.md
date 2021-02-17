---
title: Association de réviseurs d’envoi à un formulaire
seo-title: Association de réviseurs d’envoi à un formulaire
description: Apprenez à associer des réviseurs d’envoi à un formulaire dans AEM Forms. Les réviseurs associés examinent un formulaire envoyé via un portail de formulaires.
seo-description: Apprenez à associer des réviseurs d’envoi à un formulaire dans AEM Forms. Les réviseurs associés examinent un formulaire envoyé via un portail de formulaires.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 76%

---


# Association de réviseurs d’envoi à un formulaire {#associating-submission-reviewers-with-a-form}

Lorsque vous créez un formulaire, vous pouvez spécifier les utilisateurs qui passent en revue les envois du formulaire via le portail de formulaires et qui font part de leur avis. Votre entreprise peut recueillir des avis et retravailler les formulaires envoyés.

AEM Forms vous permet d’associer un groupe de réviseurs à un formulaire. Les utilisateurs ajoutés à un groupe de révision d’un formulaire voient les envois de ce formulaire et fournissent des commentaires.

Les groupes de réviseurs assignés à un formulaire peuvent uniquement analyser les envois du formulaire spécifié.

## Condition requise {#prerequisite}

### Activation de la propriété des groupes de réviseurs d’envoi pour des formulaires adaptatifs à l’aide de l’éditeur de schéma de métadonnées {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Pour associer un groupe de réviseurs à un formulaire, modifiez le schéma de métadonnées des formulaires adaptatifs. Par défaut, vous ne pouvez pas ajouter un groupe de réviseurs à un formulaire envoyé.

Pour modifier le schéma de métadonnées :

1. En mode Création, sous Experience Manager, cliquez sur **Outils** > **Actifs** > **Schémas de métadonnées**.
1. Dans la page Formulaires de schéma, accédez à **Formulaires** > **Formulaires créés dans AEM.**

   L’URL de la page est :

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Sélectionnez **Formulaire adaptatif** et cliquez sur **Modifier**.
1. Dans la page Modifier un formulaire, cliquez sur **Avancé**.
1. Dans l’onglet Avancé, faites glisser et déposez le composant **Texte d’une seule ligne** disponible sous Créer un formulaire.
1. Sélectionnez le composant de texte ajouté pour afficher ses paramètres.

   Sous Paramètres, saisissez `./jcr:content/metadata/form-submission-reviewer-group` dans le champ Associer à la propriété.

   Le champ de groupe de réviseurs d’envoi dans les propriétés avancées de votre formulaire adaptatif est activé avec le nom que vous spécifiez dans le libellé du champ.

## Association de réviseurs d’envoi à un formulaire {#associating-submission-reviewers-with-a-form-1}

Pour associer des réviseurs d’envoi à un formulaire adaptatif, créez un groupe de réviseurs et ajoutez-y des utilisateurs. Ajoutez le groupe de réviseurs créé sous le champ de réviseurs d’envoi de formulaire dans les propriétés avancées du formulaire.
Les groupes d’utilisateurs vous permettent d’associer différents ensembles de réviseurs d’envoi avec des formulaires adaptatifs différents. Cette fonctionnalité évite la révision d’un envoi d’un utilisateur non autorisé.

Avant d’effectuer les étapes suivantes, reportez-vous à la section [Condition préalable](../../forms/using/adding-reviewers-form.md#prerequisite).

Pour créer un groupe et y ajouter des membres, accédez à **Outils** > **Opérations** > **Sécurité** > **Groupes**.
Pour plus d’informations, voir [Administration utilisateur et services](/help/sites-administering/security.md).
Veillez à ajouter le groupe que vous créez en tant que membre du groupe d’utilisateurs prêt à l’emploi : **forms-submission-reviewers**. Ce groupe d’utilisateurs est fourni avec AEM Forms et garantit que les utilisateurs sont ajoutés en tant que réviseurs d’envoi.

Pour associer des groupes d’utilisateurs à un formulaire adaptatif :

1. En mode création, accédez à **Formulaires** > **Formulaires et documents**.
1. Utilisez l&#39;option **Sélectionner **pour sélectionner un formulaire adaptatif, puis cliquez sur **Propriétés de la Vue**.
1. Dans la fenêtre Propriétés du formulaire, cliquez sur **Modifier** puis sur **AVANCE**.
1. Saisissez le groupe dans le champ de groupe de réviseurs d’envoi, puis cliquez sur **Terminé**.

   Le champ de groupe de réviseurs d’envoi s’affiche avec le nom spécifié dans le schéma modifié de métadonnées des formulaires adaptatifs.

>[!NOTE]
>
>Dupliquez les utilisateurs et les formulaires pour assurer leur disponibilité dans l’implémentation à distance d’AEM Forms.
>
>Veillez à ce que tous les utilisateurs soient dupliqués comme membres de révision des groupes d’utilisateurs dans l’implémentation à distance.

