---
title: Connexion à Microsoft Translator
description: Découvrez comment connecter AEM à Microsoft Translator pour automatiser votre processus de traduction.
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3bb516289dbff4fb3b94685b9e25360e7717776e
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 76%

---

# Connexion à Microsoft Translator {#connecting-to-microsoft-translator}

AEM fournit un connecteur intégré pour [Microsoft Translator](https://www.microsoft.com/fr-fr/translator/business/) afin de traduire le contenu de pages ou de ressources. Après obtention d’une licence Microsoft pour utiliser Microsoft Translator, configurez le connecteur en suivant les instructions de cette page.

| Propriété | Description |
|---|---|
| Libellé de traduction | Nom d’affichage du service de traduction |
| Attribution de traduction | (Facultatif) Pour le contenu créé par l’utilisateur ou l’utilisatrice, l’attribution qui apparaît à côté du texte traduit, par exemple `Translations by Microsoft`. |
| ID d’espace de travail | (Facultatif) ID de votre moteur Microsoft Translator personnalisé à utiliser |
| Clé d’abonnement | Votre clé d’abonnement Microsoft pour Microsoft Translator |

La procédure suivante crée une configuration Microsoft Translator.

1. Dans le [panneau de navigation](/help/sites-authoring/basic-handling.md#first-steps), cliquez sur **Outils** -> **Services cloud** -> **Services cloud de traduction**.
1. Accédez à l’emplacement où vous souhaitez créer la configuration. Normalement, il s’agit de la racine de votre site, mais il peut s’agir aussi d’une configuration globale par défaut.
1. Cliquez sur le bouton **Créer**.
1. Définissez votre configuration.
   1. Sélectionnez **Microsoft Translator** dans la liste déroulante.
   1. Indiquez un titre pour votre configuration. Le titre identifie la configuration dans la console Services cloud, ainsi que dans les listes déroulantes de propriétés de la page.
   1. Éventuellement, saisissez un nom à utiliser pour le nœud du référentiel qui stocke la configuration.

   ![Créer une configuration de traduction](assets/create-translation-config.png)

1. Cliquez sur **Créer**.
1. Dans la fenêtre **Modifier la configuration**, indiquez les valeurs du service de traduction décrit dans le tableau précédent.

   ![Modifier la configuration de traduction](assets/msft-config-ui.png)

1. Cliquez sur **Connexion** pour vérifier la connexion.
1. Cliquez sur **Enregistrer et fermer**.

## Publication des configurations du service de traducteur {#publishing-the-translator-service-configurations}

La dernière étape consiste à publier les configurations de Microsoft Translator pour prendre en charge le contenu traduit publié à l’aide de l’action [publication d’une arborescence](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree).
