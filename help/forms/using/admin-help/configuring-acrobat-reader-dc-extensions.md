---
title: Configuration des extensions Acrobat Reader DC pour la capture de données
description: Découvrez comment configurer les extensions Acrobat Reader DC pour la capture de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 3%

---

# Configuration des extensions Acrobat Reader DC pour la capture de données {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Si les utilisateurs de votre installation AEM forms utilisent la fonctionnalité de capture de données de Content Services (obsolète), il est recommandé de créer un rôle avec un accès en lecture seule pour ces utilisateurs.

***Remarque **: Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) prend fin le 12/31/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).*

La capture de données requiert que vous attribuiez un rôle utilisateur pour accéder à SampleReaderExtensionsCredential. Vous pouvez affecter le rôle Trust Administrator standard. Cependant, considérez que ce rôle confère des privilèges d’administrateur généraux non administrateurs aux utilisateurs qui contrôlent les paramètres d’approbation PKI et gèrent les informations d’identification PKI, ce qui peut compromettre la sécurité de votre installation d’AEM forms dans un environnement de production. Il est recommandé que l’administrateur système d’AEM forms crée un rôle qui accorde uniquement un accès en lecture seule à Trust Store et affecte ce nouveau rôle aux utilisateurs non-administrateurs qui utilisent la capture de données.

## Création d’un rôle pour les utilisateurs de la capture de données {#create-a-role-for-data-capture-users}

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nouveau rôle.
1. Saisissez le nom du rôle (par exemple, Utilisateur de capture de données) et une description dans les champs appropriés, puis cliquez sur Suivant.
1. Dans l’écran Autorisations des rôles, cliquez sur Rechercher des autorisations, puis sélectionnez Lecture des informations d’identification dans la liste des autorisations disponibles.
1. Cliquez sur OK, puis sur Terminer.

## Attribution du rôle de capture de données {#assign-the-data-capture-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Rechercher.
1. Cliquez sur le rôle utilisateur de capture de données que vous avez créé.
1. Dans l’onglet Utilisateurs/groupes de rôle, cliquez sur Rechercher des utilisateurs/groupes.
1. Dans l’écran Rechercher des utilisateurs et des groupes, cliquez sur Rechercher, sélectionnez les utilisateurs nécessitant le rôle d’utilisateur de capture de données, puis cliquez sur OK.
1. Dans l’écran Modifier le rôle, cliquez sur Enregistrer.
