---
title: Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: Découvrez comment utiliser AEM processus de traduction pour localiser les formulaires adaptatifs et le document d’enregistrement.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 44%

---

# Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

Les formulaires localisés permettent de servir un public plus large dans plusieurs zones géographiques. Le processus de traduction Adobe Experience Manager vous aide à localiser les formulaires adaptatifs et leurs documents d’enregistrement . Vous pouvez utiliser **traduction automatique** ou **traducteurs humains** pour localiser un formulaire adaptatif.

Cet article explique le processus d’utilisation AEM processus de traduction avec des formulaires adaptatifs et des documents d’enregistrement.

## Localisation d’un formulaire adaptatif et d’un document d’enregistrement à l’aide de la traduction automatique {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Le service de traduction automatique traduit immédiatement votre contenu dans un formulaire adaptatif et un document d’enregistrement. AEM Forms est préconfiguré pour utiliser une version d’évaluation de Microsoft Translator pour la traduction automatique. Effectuez les étapes suivantes pour activer la traduction automatique de vos formulaires adaptatifs et documents d’enregistrement :

1. Dans l’interface utilisateur AEM Forms, sélectionnez un formulaire, puis appuyez sur l’option **Ajouter un dictionnaire**.
1. Dans l’écran **Ajouter un dictionnaire au projet de traduction**, sélectionnez l’option **Créer un nouveau projet de traduction** ou **Ajouter à un projet de traduction existant**.
1. Dans le champ **Titre du projet**, indiquez le titre, par exemple `Government Reference Site - German locale.`
1. Dans le champ **Langues cibles**, spécifiez un paramètre régional (par exemple `German(de)`), puis cliquez sur **Terminé**. Vous pouvez spécifier plusieurs paramètres régionaux. Le formulaire est traduit dans tous les paramètres régionaux spécifiés dans la variable **Langues cibles** champ .
1. Dans la boîte de dialogue Dictionnaire ajouté, cliquez sur **Ouvrir des projets**. Dans l’écran Projets , ouvrez le nouveau projet.
1. Cliquez sur le bouton **ellipses** au bas de la **Résumé de traduction** mosaïque. L’écran Résumé de traduction s’affiche.
1. Cliquez sur le bouton **Modifier** en haut de la page **Résumé de traduction** écran. Ouvrez l’onglet **Traduction** et sélectionnez Traduction automatique sur l’écran **Méthode de traduction**. Sélectionnez le **fournisseur de traduction** approprié et la **configuration de cloud**. Cliquez sur l’icône **Terminé** en haut de l’écran.
1. Dans le volet **Tâche de traduction**, cliquez sur l’icône ![aem62forms_downarrow](assets/aem62forms_downarrow.png), puis sur **Démarrer**. L’état de la mosaïque passe à Brouillon. Une fois la traduction terminée, l’état passe à **Prêt pour la révision**. Actualisez la page après quelques minutes et vérifiez l’état.
1. Après le changement d’état en **Prêt pour la révision**, dans la vignette **Tâche de traduction**, ouvrez le formulaire dans une fenêtre de navigateur. Une version localisée du formulaire s’affiche.

   >[!NOTE]
   >
   >* Avant d’ouvrir la version localisée du formulaire dans la fenêtre du navigateur, assurez-vous que les paramètres régionaux du navigateur correspondent à ceux du formulaire. Par exemple, si le formulaire est traduit en allemand(de), définissez les paramètres régionaux du navigateur sur Allemand(de).
   >* Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). comme l’hébreu.

   Avec le formulaire adaptatif, le document d’enregistrement généré automatiquement est également localisé.

   Pour plus d’informations sur les paramètres et la configuration du document d’enregistrement, voir :

[Configuration du modèle de document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Paramètres d’un document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personnalisation des informations de marque du document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) et assurez-vous que les paramètres régionaux du navigateur sont définis dans la même langue que celle dans laquelle vous avez localisé le formulaire adaptatif à l’aide de la langue de la machine. Les paramètres régionaux du navigateur permettent de localiser les informations de marque dans le document d’enregistrement.
1. Pour afficher le document d’enregistrement localisé, appuyez sur Générer l’aperçu. Le document d’enregistrement PDF est généré et ouvert dans un nouvel onglet de votre navigateur.

## Localisation d’un formulaire adaptatif et de son document d’enregistrement à l’aide de la traduction humaine {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

En traduction humaine, le contenu est envoyé à un prestataire de traduction et traduit par des traducteurs professionnels. Une fois la traduction terminée, le contenu traduit est renvoyé et importé dans AEM. Lorsque votre fournisseur de traduction est intégré à AEM, le contenu est automatiquement transféré entre AEM et le fournisseur de traduction.

Pour la traduction, un dictionnaire contenant des fichiers au format XLIFF est partagé avec les traducteurs professionnels. Le dictionnaire contient un fichier XLIFF distinct pour chaque paramètre régional. Chaque fichier XLIFF contient du texte qui sera affiché pour les utilisateurs finaux et des espaces réservés pour le texte localisé correspondant.

Effectuez les étapes suivantes pour localiser un formulaire et son document d’enregistrement à l’aide de traducteurs humains :

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
