---
title: Configuration des extensions Acrobat Reader DC pour la capture de données
description: Découvrez comment configurer les extensions Acrobat Reader DC pour la capture de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 100%

---

# Configuration des extensions Acrobat Reader DC pour la capture de données {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Si les utilisateurs et utilisatrices de votre installation AEM Forms utilisent la fonctionnalité de capture de données de Content Services (obsolète), il est recommandé de créer un rôle avec un accès en lecture seule pour ces utilisateurs et utilisatrices.

***Remarque ** : Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs et utilisatrices de concevoir, de gérer, de surveiller et d’optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).*

La capture de données requiert que vous attribuiez un rôle utilisateur pour accéder à SampleReaderExtensionsCredential. Vous pouvez affecter le rôle Trust Administrator standard. Cependant, considérez que ce rôle confère des privilèges d’administrateur qui contrôlent les paramètres d’approbation PKI et gèrent les informations d’identification PKI aux utilisateurs et utilisatrices non-administrateurs, ce qui peut compromettre la sécurité de votre installation d’AEM forms dans un environnement de production. Il est recommandé que l’administrateur ou l’administratrice système d’AEM Forms crée un rôle qui accorde uniquement un accès en lecture seule à Trust Store et affecte ce nouveau rôle aux utilisateurs et utilisatrices non-administrateurs qui utilisent la capture de données.

## Création d’un rôle destiné aux utilisateurs qui capturent des données {#create-a-role-for-data-capture-users}

1. Dans la console d’administration, cliquer sur Paramètres > Gestion des utilisateurs ou utilisatrices > Gestion des rôles, puis sur Nouveau rôle.
1. Saisissez le nom du rôle (par exemple Utilisateur ou utilisatrice capturant des données), ainsi qu’une description dans les champs appropriés, puis cliquez sur Suivant.
1. Dans l’écran Autorisations des rôles, cliquer sur Rechercher des autorisations, puis sélectionner Lecture des informations d’identification dans la liste des autorisations disponibles.
1. Cliquez sur OK, puis sur Terminer.

## Affectation du rôle de capture de données {#assign-the-data-capture-role}

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs et utilisatrices > Gestion des rôles, puis sur Rechercher.
1. Cliquez sur le rôle utilisateur de capture de données que vous avez créé.
1. Dans l’onglet Utilisateurs et utilisatrices/groupes de rôle, cliquer sur Rechercher des utilisateurs et utilisatrices/groupes.
1. Dans l’écran Rechercher des utilisateurs, des utilisatrices et des groupes, cliquer sur Rechercher, sélectionner les utilisateurs et utilisatrices nécessitant le rôle utilisateur de capture de données, puis cliquez sur OK.
1. Dans l’écran Modifier le rôle, cliquez sur Enregistrer.
