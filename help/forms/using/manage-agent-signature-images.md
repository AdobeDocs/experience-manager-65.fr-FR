---
title: Gérer les images de signature d’agent
seo-title: Gérer les images de signature d’agent
description: Après la création d’un modèle de lettre, vous pouvez l’utiliser pour créer une correspondance dans AEM Forms en gérant les données, le contenu et les pièces jointes.
seo-description: Après la création d’un modèle de lettre, vous pouvez l’utiliser pour créer une correspondance dans AEM Forms en gérant les données, le contenu et les pièces jointes.
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gérer les images de signature d’agent{#manage-agent-signature-images}

## Présentation {#overview}

Dans Correspondence Management, vous pouvez utiliser une image pour rendre la signature de l’agent dans les lettres. Après avoir configuré l’image de la signature de l’agent lors de la création d’une lettre, vous pouvez rendre l’image de la signature de l’agent dans la lettre comme signature de l’agent expéditeur.

Le DDE agentSignatureImage est un DDE calculé qui représente l’image de la signature de l’agent. L’expression de ce DDE calculé utilise une nouvelle fonction personnalisée qui est exposée par le bloc de création Expression Manager. Cette fonction personnalisée prend agentID et agentFolder comme paramètres d’entrée et récupère le contenu d’image en se basant sur ces paramètres. Le dictionnaire de données système SystemContext donne aux lettres dans Correspondence Management l’accès aux informations dans le contexte système actuel. Le contexte du système contient des informations sur l’utilisateur actuellement connecté, ainsi que sur les paramètres de configuration actifs.

Vous pouvez ajouter des images sous le dossier cmuserroot. Dans [Propriétés de configuration de Correspondence Management](/help/forms/using/cm-configuration-properties.md), à l’aide de la propriété Racine de l’utilisateur de CM, vous pouvez changer le dossier d’où l’image de la signature de l’agent est récupérée.

La valeur du DDE agentFolder est extraite du paramètre de configuration CMUserRoot pour les propriétés de configuration de Correspondence Management. Par défaut, ce paramètre de configuration pointe vers/content/cmUserRoot dans le référentiel CRX. Vous pouvez modifier la valeur de la configuration CMUserRoot dans les Propriétés de configuration.
Vous pouvez également remplacer la fonction personnalisée par défaut de manière à définir votre propre logique pour récupérer l’image de la signature de l’utilisateur.

## Ajouter l’image de la signature de l’agent {#adding-agent-signature-image}

1. Assurez-vous que l’image de la signature de l’agent porte le même nom que le nom d’utilisateur AEM de l’utilisateur. (L’extension n’est pas nécessaire pour le nom de fichier de l’image.)
1. Dans CRX, créez un dossier intitulé `cmUserRoot` dans le dossier de contenu.

   1. Accédez à `https://'[server]:[port]'/crx/de`. Le cas échéant, connectez-vous en tant qu’administrateur.

   1. Cliquez avec le bouton droit sur le dossier **contenu** et sélectionnez **Créer** > **Créer un dossier**.

      ![Créer un dossier](assets/1_createnode_cmuserroot.png)

   1. Dans la boîte de dialogue Créer un dossier, saisissez le nom de dossier`cmUserRoot` . Cliquez sur **Enregistrer tout**.

      >[!NOTE]
      >
      >cmUserRoot correspond à l’emplacement par défaut où AEM recherche l’image de la signature de l’agent. You can, however, change it by editing the CM User Root property in the [Correspondence Management configuration properties](/help/forms/using/cm-configuration-properties.md).

1. Dans l’explorateur de contenu, accédez au dossier cmUserRoot et ajoutez-y l’image de la signature de l’agent.

   1. Accédez à `https://'[server]:[port]'/crx/explorer/index.jsp`. Connectez-vous en tant qu’administrateur, si nécessaire.
   1. Cliquez sur **Explorateur de contenu**. L’explorateur de contenu s’ouvre dans une nouvelle fenêtre.
   1. Dans l’explorateur de contenu, accédez au dossier cmUserRoot et sélectionnez-le. Cliquez avec le bouton droit sur le dossier **cmUserRoot** et sélectionnez **Nouveau nœud**.

      ![Nouveau nœud de cmUserRoot](assets/2_cmuserroot_newnode.png)

      Effectuez les entrées suivantes de la rangée pour le nouveau nœud, puis cliquez sur la coche verte.

      **Nom :** JohnDoe (ou le nom du fichier de signature de votre agent)

      **Type :** nt:file

      Under the `cmUserRoot` folder, a new folder called `JohnDoe` (or the name you have given in the previous step) is created.

   1. Cliquez sur le nouveau dossier que vous avez créé (ici`JohnDoe` ). L’Explorateur de contenu affiche le contenu du dossier en grisé.

   1. Double-click the **jcr:content** property, set its type as **nt:resource**, and then click the green check mark to save the entry.

      Si la propriété n’est pas disponible, vous devez d’abord créer une propriété avec le nom jcr:content.

      ![propriété jcr:content](assets/3_jcrcontentntresource.png)

      Parmi les sous-propriétés de jcr:content se trouve jcr:data en grisé. Double-cliquez sur jcr:data. La propriété devient modifiable et le bouton Choisir un fichier apparaît dans l’entrée. Click **Choose File** and select the image file you want to use as a logo. Le fichier image n’a pas besoin d’extension.

      ![Données JCR](assets/5_jcrdata.png)
   Cliquez sur **Enregistrer tout**.

1. Assurez-vous que le XDP/la mise en page que vous utilisez dans la lettre a un champ d’image en bas à gauche (ou tout autre emplacement de votre choix dans la mise en page où vous souhaitez rendre la signature) afin de rendre l’image de signature.
1. Lors de la création de la correspondance, sous l’onglet Données, sélectionnez un champ d’image pour l’image de la signature en procédant comme suit :

   1. Sélectionnez Système dans le menu contextuel Type de liaison dans le volet de droite.

   1. Sélectionnez le DDE agentSignatureImage dans la liste du volet Eléments de données pour le dictionnaire de données SystemContext.

   1. Enregistrez la lettre.

1. Lorsque la lettre est rendue, vous pouvez voir votre signature dans l’aperçu de lettre dans le champ d’image en fonction de la mise en page.

   ![Image de la signature de l’agent dans la lettre](assets/letterwithsignature.png)

