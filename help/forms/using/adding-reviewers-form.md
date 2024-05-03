---
title: Association de réviseurs d’envoi à un formulaire
description: Apprenez à associer des réviseurs d’envoi à un formulaire dans AEM Forms. Les réviseurs associés examinent un formulaire envoyé via un portail de formulaires.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 100%

---

# Association de réviseurs d’envoi à un formulaire {#associating-submission-reviewers-with-a-form}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

Lorsque vous créez un formulaire, vous pouvez spécifier les utilisateurs et utilisatrices qui passent en revue les envois du formulaire via le portail Formulaires et qui font part de leurs commentaires. Votre entreprise peut recueillir des commentaires et retravailler les formulaires envoyés.

AEM Forms vous permet d’associer un groupe de réviseurs et réviseuses à un formulaire. Les utilisateurs ajoutés à un groupe de révision d’un formulaire examinent les envois du formulaire en question et font part de leurs commentaires.

Les groupes de réviseurs assignés à un formulaire peuvent uniquement analyser les envois du formulaire spécifié.

## Prérequis {#prerequisite}

### Activer la propriété des groupes de réviseurs et réviseuses d’envois pour des formulaires adaptatifs à l’aide de l’éditeur de schéma de métadonnées {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Pour associer un groupe de réviseurs et réviseuses à un formulaire, modifiez le schéma de métadonnées des formulaires adaptatifs. Par défaut, vous ne pouvez pas ajouter un groupe de réviseurs à un formulaire envoyé.

Pour modifier le schéma de métadonnées :

1. En mode création, sous Experience Manager, cliquez sur **Outils** > **Ressources** > **Schémas de métadonnées**.
1. Dans la page Formulaires du schéma, accédez à **Formulaires** > **Formulaires créés dans AEM.**

   L’URL de la page est la suivante :

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Sélectionnez **Formulaire adaptatif**, puis cliquez sur **Modifier**.
1. Dans la page Modifier un formulaire, cliquez sur **Avancé**.
1. Dans l’onglet Avancé, effectuez un glisser-déposer du composant **Une seule ligne de texte** disponible sous Générer un formulaire.
1. Sélectionnez le composant de texte ajouté pour afficher ses paramètres.

   Sous Paramètres, saisissez `./jcr:content/metadata/form-submission-reviewer-group` dans le champ Associer à la propriété.

   Le champ de groupe de réviseurs d’envoi dans les propriétés avancées de votre formulaire adaptatif est activé avec le nom que vous spécifiez dans le libellé du champ.

## Association de réviseurs d’envoi à un formulaire {#associating-submission-reviewers-with-a-form-1}

Pour associer des réviseurs et réviseuses d’envoi à un formulaire adaptatif, créez un groupe de réviseurs et réviseuses et ajoutez-y des personnes. Ajoutez le groupe de réviseurs créé sous le champ de réviseurs d’envoi de formulaire dans les propriétés avancées du formulaire.
Les groupes d’utilisateurs vous permettent d’associer différents ensembles de réviseurs d’envoi avec des formulaires adaptatifs différents. Cette fonctionnalité évite la révision d’un envoi d’un utilisateur non autorisé.

Avant d’effectuer les étapes suivantes, reportez-vous à la section [Prérequis](../../forms/using/adding-reviewers-form.md#prerequisite).

Pour créer un groupe et y ajouter des membres, accédez à **Outils** > **Opérations** > **Sécurité** > **Groupes**.
Pour plus d’informations, reportez-vous à la section [Administration utilisateur et services](/help/sites-administering/security.md).
Veillez à ajouter le groupe que vous avez créé en tant que membre du groupe d’utilisateurs prêt à l’emploi : **réviseurs-envoi-formulaires**. Ce groupe d’utilisateurs est fourni avec AEM Forms et garantit que les utilisateurs sont ajoutés en tant que réviseurs d’envoi.

Pour associer des groupes d’utilisateurs et d’utilisatrices à un formulaire adaptatif :

1. En mode création, accédez à **Formulaires** > **Formulaires et documents**.
1. Utilisez l’option **Sélectionner** pour choisir un formulaire adaptatif, puis cliquez sur **Afficher les propriétés**.
1. Dans la fenêtre Propriétés du formulaire, cliquez sur **Modifier** puis sur **AVANCÉ**.
1. Saisissez le groupe dans le champ de groupe de réviseurs d’envoi, puis cliquez sur **Terminé**.

   Le champ de groupe de réviseurs d’envoi s’affiche avec le nom spécifié dans le schéma modifié de métadonnées des formulaires adaptatifs.

>[!NOTE]
>
>Répliquez les utilisateurs ou utilisatrices et les formulaires pour garantir leur disponibilité dans l’implémentation distante d’AEM Forms.
>
>Veillez à ce que tous les utilisateurs soient répliqués comme membres de révision des groupes d’utilisateurs dans l’implémentation distante.
