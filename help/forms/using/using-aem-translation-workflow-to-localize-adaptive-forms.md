---
title: Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement
description: Découvrez comment utiliser les workflows de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement.
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms, Foundation Components
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 100%

---

# Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

Les formulaires localisés permettent de servir un public plus large dans plusieurs zones géographiques. Le workflow de traduction Adobe Experience Manager vous permet de localiser des formulaires adaptatifs et leurs documents d’enregistrement. Vous pouvez faire appel à la **traduction automatique** ou à des **traducteurs humains** pour localiser un formulaire adaptatif.

Cet article décrit la procédure d’utilisation du workflow de traduction AEM avec des formulaires adaptatifs et des documents d’enregistrement.

## Localisation d’un formulaire adaptatif et d’un document d’enregistrement à l’aide de la traduction automatique {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Le service de traduction automatique traduit directement le contenu de vos formulaires adaptatifs et documents d’enregistrement. AEM Forms est préconfiguré pour utiliser une version d’évaluation de Microsoft Translator pour la traduction automatique. Pour activer la traduction automatique pour les formulaires adaptatifs et le document d’enregistrement, procédez comme suit :

1. Dans l’interface utilisateur AEM Forms, sélectionnez un formulaire, puis l’option **Ajouter un dictionnaire**.
1. Dans l’écran **Ajouter un dictionnaire au projet de traduction**, sélectionnez l’option **Créer un nouveau projet de traduction** ou **Ajouter à un projet de traduction existant**.
1. Dans le champ **Titre du projet**, indiquez le titre, par exemple `Government Reference Site - German locale.`
1. Dans le champ **Langues cibles**, spécifiez un paramètre régional (par exemple `German(de)`), puis cliquez sur **Terminé**. Vous pouvez spécifier plusieurs paramètres régionaux. Le formulaire est traduit dans tous les paramètres régionaux spécifiés dans le champ **Langues cibles**.
1. Dans la boîte de dialogue Dictionnaire ajouté, cliquez sur **Ouvrir des projets**. Sur l’écran Projets, ouvrez le nouveau projet.
1. Cliquez sur les **points de suspension** en bas de la mosaïque **Résumé de traduction**. L’écran Résumé de traduction s’affiche.
1. Cliquez sur l’icône **Modifier** en haut de l’écran **Résumé de traduction**. Ouvrez l’onglet **Traduction** et sélectionnez Traduction automatique sur l’écran **Méthode de traduction**. Sélectionnez le **fournisseur de traduction** approprié et la **configuration de cloud**. Cliquez sur l’icône **Terminé** en haut de l’écran.
1. Dans le volet **Tâche de traduction**, cliquez sur l’icône ![aem62forms_downarrow](assets/aem62forms_downarrow.png), puis sur **Démarrer**. Le statut de la mosaïque passe à Brouillon. Une fois la traduction terminée, le statut passe à **Prêt pour la révision**. Actualisez la page après quelques minutes et vérifiez le statut.
1. Après le changement d’état en **Prêt pour la révision**, dans la vignette **Tâche de traduction**, ouvrez le formulaire dans une fenêtre de navigateur. Une version localisée du formulaire s’affiche.

   >[!NOTE]
   >
   >* Avant d’ouvrir la version localisée du formulaire dans la fenêtre du navigateur, assurez-vous que les paramètres régionaux du navigateur correspondent à ceux du formulaire. Par exemple, si le formulaire est traduit en Allemand(de), définissez les paramètres régionaux du navigateur sur Allemand(de).
   >* Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). comme l’hébreu.

   Avec le formulaire adaptatif, le document d’enregistrement généré automatiquement est également localisé.

   Pour plus d’informations sur les paramètres et la configuration du document d’enregistrement, voir :

[Configuration du modèle de document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Paramètres d’un document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personnalisez les informations de marque du document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) et assurez-vous que les paramètres régionaux du navigateur correspondent à la langue dans laquelle vous avez localisé le formulaire adaptatif à l’aide de la traduction automatique. Les paramètres régionaux du navigateur permettent de localiser les informations de marque dans le document d’enregistrement.
1. Pour afficher le document d’enregistrement localisé, sélectionnez Générer l’aperçu. Le document d’enregistrement PDF est généré et ouvert dans un nouvel onglet de votre navigateur.

## Localiser un formulaire adaptatif et son document d’enregistrement à l’aide de la traduction humaine {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Avec la traduction humaine, le contenu est envoyé à un prestataire de traduction et traduit par des traducteurs et des traductrices professionnels. Une fois la traduction terminée, le contenu traduit est renvoyé et importé dans AEM. Lorsque votre fournisseur de traduction est intégré à AEM, le contenu est automatiquement transféré entre AEM et le fournisseur de traduction.

Pour la traduction, un dictionnaire contenant les fichiers au format XLIFF est partagé avec les traducteurs et les traductrices professionnels. Le dictionnaire contient un fichier XLIFF distinct pour chaque langue. Chaque fichier XLIFF contient du texte visible par les utilisateurs finaux, ainsi que des espaces réservés pour le texte localisé correspondant.

Pour localiser un formulaire et son document d’enregistrement à l’aide de traducteurs et traductrices humains, procédez comme suit :

1. [Connectez AEM à votre fournisseur de service de traduction](/help/sites-administering/tc-tic.md) et [créez des configurations de structure d’intégration de traduction](/help/sites-administering/tc-tic.md).

1. [Associer les pages de votre gabarit de langue](/help/sites-administering/tc-tic.md) au service de traduction et aux configurations de structure.

1. [Identifier le type de contenu](/help/sites-administering/tc-rules.md) à traduire.

1. [Préparez le contenu à traduire](/help/sites-administering/tc-prep.md) en créant le gabarit de langue et les pages racine des copies de langue.

1. [Créez des projets de traduction](/help/sites-administering/tc-manage.md) pour collecter le contenu à traduire et préparer le processus de traduction.

1. Utiliser les projets de translation pour [gérer le processus de traduction du contenu](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). comme l’hébreu.
>
