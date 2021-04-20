---
title: Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement
seo-title: Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement
description: Découvrez comment utiliser les processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement.
seo-description: Découvrez comment utiliser les processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 84%

---


# Utilisation du processus de traduction AEM pour localiser les formulaires adaptatifs et le document d’enregistrement {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Les formulaires localisés permettent de servir un public plus large dans plusieurs zones géographiques. Le processus de traduction Adobe Experience Manager vous aide à localiser des formulaires adaptatifs et leurs documents d’enregistrement. Vous pouvez faire appel à la **traduction automatique** ou à des **traducteurs humains** pour localiser un formulaire adaptatif.

Cet article décrit le processus d’utilisation du processus de traduction AEM avec des formulaires adaptatifs et des documents d’enregistrement.

## Localisation d’un formulaire adaptatif et d’un document d’enregistrement à l’aide de la traduction automatique {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Le service de traduction automatique traduit directement le contenu de vos formulaires adaptatifs et document d’enregistrement. AEM Forms est préconfiguré pour utiliser une version d’évaluation de Microsoft Translator pour la traduction automatique. Procédez comme suit pour activer la traduction automatique pour les formulaires adaptatifs et le document d’enregistrement :

1. Sur l’interface utilisateur AEM Forms, sélectionnez un formulaire, puis appuyez sur l’option **Ajouter un dictionnaire**.
1. Dans l’écran **Ajouter un dictionnaire au projet de traduction**, sélectionnez l’option **Créer un nouveau projet de traduction** ou **Ajouter à un projet de traduction existant**.
1. Dans le champ **Titre du projet**, indiquez le titre. Par exemple, `Government Reference Site - German locale.`
1. Dans le champ **Langues de la Cible**, spécifiez un paramètre régional (par exemple, `German(de)`), puis cliquez sur **Terminé**. Vous pouvez spécifier plusieurs paramètres régionaux. Le formulaire est traduit dans tous les paramètres régionaux spécifiés dans le champ **Langues cibles**.
1. Dans la boîte de dialogue Dictionnaire ajouté, cliquez sur **Ouvrir des projets**. Dans l’écran Projets, ouvrez le nouveau projet.
1. Cliquez sur les **points de suspension** situés au bas du volet **Résumé de traduction**. L’écran Résumé de traduction apparaît.
1. Cliquez sur l’icône **Modifier** en haut de l’écran **Résumé de traduction**. Ouvrez l’onglet **Traduction** et sélectionnez Traduction automatique sur l’écran **Méthode de traduction.** Sélectionnez le **fournisseur de traduction** approprié et la **configuration de cloud**. Cliquez sur l’icône **Terminé** en haut de l’écran.
1. Dans la mosaïque **Tâche de traduction**, cliquez sur l’icône ![flèche de téléchargement ](assets/aem62forms_downarrow.png) d’aem62forms, puis sur **Début**. Le statut du volet passe à Brouillon. À la fin de la traduction, le statut passe à **Prêt pour la révision**. Actualisez la page après quelques minutes et vérifiez l’état.
1. Une fois l’état défini sur **Prêt pour révision** sur la mosaïque **Tâche de traduction**, ouvrez le formulaire dans une fenêtre de navigateur. Une version localisée du formulaire s’affiche.

   >[!NOTE]
   >
   >* Avant d’ouvrir la version localisée du formulaire dans la fenêtre du navigateur, assurez-vous que les paramètres régionaux du navigateur permettent d’afficher le formulaire. Par exemple, si le formulaire est traduit en Allemand(de), définissez les paramètres régionaux du navigateur sur Allemand(de).
   >* Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). Par exemple, hébreu.


   Avec le formulaire adaptatif, le document d’enregistrement généré automatiquement est également localisé.

   Pour plus d&#39;informations sur les paramètres et la configuration du Document d&#39;enregistrement, voir :

   [Configuration du modèle de document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Paramètres des documents d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personnalisez les informations de marque du document d’enregistrement](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) et assurez-vous que les paramètres régionaux du navigateur correspondent à la langue dans laquelle vous avez localisé le formulaire adaptatif à l’aide de la langue de la machine. Les paramètres régionaux du navigateur permettent de localiser les informations de marque dans le document d’enregistrement.
1. Pour afficher le document d’enregistrement localisé, appuyez sur Générer l’aperçu. Le document d’enregistrement PDF est généré et ouvert dans un nouvel onglet de votre navigateur.

## Localisation d’un formulaire adaptatif et de son document d’enregistrement à l’aide de la traduction humaine {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Avec la traduction humaine, le contenu est envoyé à un prestataire de traduction et traduit par des traducteurs professionnels. Une fois la traduction terminée, le contenu traduit est renvoyé et importé dans AEM. Lorsque votre fournisseur de traduction est intégré à AEM, le contenu est automatiquement transféré entre AEM et le fournisseur de traduction.

Pour la traduction, un dictionnaire contenant les fichiers au format XLIFF est partagé avec les traducteurs professionnels. Le dictionnaire contient un fichier XLIFF distinct pour chaque langue. Chaque fichier XLIFF contient du texte visible par les utilisateurs finaux, ainsi que des espaces réservés pour le texte localisé correspondant.

Effectuez les étapes suivantes pour localiser un formulaire et son document d’enregistrement à l’aide de traducteurs humains :

1. [Connectez AEM à votre fournisseur de service de traduction](/help/sites-administering/tc-tic.md) et [créez des configurations de structure d’intégration de traduction](/help/sites-administering/tc-tic.md).

1. [Associer les pages de votre gabarit de langue](/help/sites-administering/tc-tic.md) au service de traduction et aux configurations de structure.

1. [Identifiez le type de ](/help/sites-administering/tc-rules.md) contenu à traduire.

1. [Préparez le contenu à traduire](/help/sites-administering/tc-prep.md) en créant le gabarit de langue et les pages racine des copies de langue.

1. [Créez des ](/help/sites-administering/tc-manage.md) projets de traduction pour rassembler le contenu à traduire et préparer le processus de traduction.

1. Utiliser les projets de translation pour [gérer le processus de traduction du contenu](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). Par exemple, hébreu.

>



