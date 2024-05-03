---
title: Ajout d’informations issues de données utilisateur aux métadonnées d’envoi de formulaire
description: Découvrez comment ajouter des informations aux métadonnées d’un formulaire envoyé avec des données fournies par l’utilisateur.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms, Foundation Components
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
exl-id: 5ca850e3-30f0-4384-b615-356dc3c2ad0d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 100%

---

# Ajout d’informations issues de données utilisateur aux métadonnées d’envoi de formulaire{#adding-information-from-user-data-to-form-submission-metadata}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

Vous pouvez utiliser des valeurs saisies dans un élément de votre formulaire pour calculer les champs de métadonnées d’un brouillon ou d’un envoi de formulaire. Les métadonnées vous permettent de filtrer le contenu en fonction des données utilisateur. Par exemple, un utilisateur ou une utilisatrice saisit John Doe dans le champ de nom de votre formulaire. Vous pouvez utiliser ces informations pour calculer les métadonnées susceptibles de classer cet envoi sous les initiales JD.

Pour calculer les champs de métadonnées avec des valeurs saisies par l’utilisateur, ajoutez les éléments de votre formulaire aux métadonnées. Lorsqu’un utilisateur entre une valeur dans cet élément, un script utilise la valeur pour calculer les informations. Ces informations sont ajoutées dans les métadonnées. Lorsque vous ajoutez un élément sous la forme d’un champ de métadonnées, vous fournissez la clé correspondante. La clé est ajoutée en tant que champ dans les métadonnées et les informations calculées sont enregistrées en fonction de celle-ci.

Par exemple, une compagnie d’assurance maladie publie un formulaire. Dans ce formulaire, un champ capture l’âge des utilisateurs finaux. Le client ou la cliente souhaite vérifier tous les envois dans une tranche d’âge spécifique, après qu’un certain nombre d’utilisateurs et utilisatrices ont envoyé le formulaire. Plutôt que de parcourir toutes les données qui deviennent complexes à mesure que le nombre de formulaires augmente, des métadonnées supplémentaires aident le client ou la cliente. La personne ayant créé le formulaire peut configurer quelles propriétés/données remplies par l’utilisateur final ou l’utilisatrice finale sont stockées au niveau supérieur afin de faciliter la recherche. Les métadonnées supplémentaires sont des informations renseignées par l’utilisateur ou l’utilisatrice et stockées au niveau supérieur du nœud de métadonnées, tel que l’auteur ou l’autrice les a configurées.

Prenons un autre exemple de formulaire qui capture l’ID de l’e-mail et le numéro de téléphone. Lorsqu’un utilisateur visite ce formulaire de manière anonyme et abandonne le formulaire, l’auteur peut configurer le formulaire afin que l’ID d’adresse électronique et le numéro de téléphone soient automatiquement enregistrés. Ce formulaire est enregistré automatiquement et le numéro de téléphone et l’ID d’adresse électronique sont stockés dans le nœud de métadonnées du brouillon. Le tableau de bord de gestion des prospects représente un cas d’utilisation de cette configuration.

## Ajout d’éléments de formulaire aux métadonnées {#adding-form-elements-to-metadata}

Effectuez les étapes suivantes pour ajouter un élément aux métadonnées :

1. Ouvrez votre formulaire adaptatif en mode d’édition.\
   Pour ouvrir le formulaire en mode d’édition, dans Forms Manager, sélectionnez le formulaire, puis sélectionnez **Ouvrir**.
1. En mode d’édition, sélectionnez un composant, sélectionnez ![field-level](assets/field-level.png) > **Conteneur de formulaires adaptatifs**, puis sélectionnez ![cmppr](assets/cmppr.png).
1. Dans la barre latérale, cliquez sur **Métadonnées**.
1. Dans la section Métadonnées, cliquez sur **Ajouter**.
1. Utilisez le champ Valeur de l’onglet Métadonnées pour ajouter des scripts. Les scripts que vous ajoutez collectent des données à partir d’éléments sur le formulaire et calculent les valeurs qui sont ajoutées aux métadonnées.

   Par exemple, la valeur **true** est enregistrée dans les métadonnées si l’âge entré est supérieur à 21, et la valeur **false** est enregistrée s’il est inférieur à 21. Vous entrez le script suivant dans l’onglet Métadonnées :

   `(agebox.value >= 21) ? true : false`

   ![Script de métadonnées](assets/add-element-metadata.png)

   Script entré dans l’onglet Métadonnées

1. Cliquez sur **OK**.

Une fois qu’un utilisateur a saisi des données dans l’élément sélectionné comme champ de métadonnées, les informations calculées sont enregistrées dans les métadonnées. Vous pouvez afficher les métadonnées dans le référentiel que vous avez configuré pour stocker les métadonnées.

## Affichage des métadonnées d’envoi de formulaire mises à jour : {#seeing-updated-form-nbsp-submission-metadata}

Pour l’exemple ci-dessus, les métadonnées sont stockées dans le référentiel CRX. Les métadonnées présentent l’aspect suivant :

![Métadonnées](assets/metadata_entry_new.png)

Si vous ajoutez un élément de case à cocher dans les métadonnées, les valeurs sélectionnées sont stockées sous forme de chaîne séparée par des virgules. Par exemple, vous ajoutez un composant de case à cocher dans votre formulaire, puis indiquez son nom : `checkbox1`. Dans les propriétés du composant de case à cocher, vous ajoutez les éléments Permis de conduire, Numéro de sécurité sociale et Passeport pour les valeurs 0, 1 et 2.

![Stockage de plusieurs valeurs à partir d’une case à cocher](assets/checkbox-metadata.png)

Vous sélectionnez le conteneur de formulaires adaptatifs et dans les propriétés du formulaire vous ajoutez une clé de métadonnées `cb1` qui stocke `checkbox1.value`, puis vous publiez le formulaire. Lorsqu’un client ou une cliente remplit le formulaire, il sélectionne les options Passeport et Numéro de sécurité sociale dans le champ de case à cocher. Les valeurs 1 et 2 sont stockées sous la forme 1, 2 dans le champ cb1 des métadonnées d’envoi.

![Entrée de métadonnées pour plusieurs valeurs sélectionnées dans un champ de case à cocher](assets/metadata-entry.png)

>[!NOTE]
>
>L’exemple ci-dessus est fourni uniquement à des fins d’apprentissage. Veillez à rechercher des métadonnées à l’emplacement correct, tel que configuré dans votre implémentation AEM Forms.
