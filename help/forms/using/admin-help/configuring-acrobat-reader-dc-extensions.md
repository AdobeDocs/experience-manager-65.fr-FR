---
title: Configurer les extensions Acrobat Reader DC pour la capture de données
description: Découvrez comment configurer les extensions Acrobat Reader DC pour la capture de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%
---
# Configurer les extensions Acrobat Reader DC pour la capture de données {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Si les utilisateurs et utilisatrices de votre installation AEM Forms utilisent la fonctionnalité de capture de données de Content Services (Obsolète), il est recommandé de créer un rôle avec un accès en lecture seule pour ces utilisateurs et utilisatrices.

***Remarque ** : Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs et utilisatrices de concevoir, de gérer, de surveiller et d’optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).*

La capture de données requiert que vous attribuiez un rôle utilisateur pour accéder à SampleReaderExtensionsCredential. Vous pouvez affecter le rôle Trust Administrator standard. Cependant, considérez que ce rôle confère des privilèges d’administrateur ou d’administratrice qui contrôlent les paramètres d’approbation PKI et gèrent les informations d’identification PKI aux utilisateurs et utilisatrices non-administrateurs, ce qui peut compromettre la sécurité de votre installation d’AEM Forms dans un environnement de production. Il est recommandé que l’administrateur ou l’administratrice système d’AEM Forms crée un rôle qui accorde uniquement un accès en lecture seule à Trust Store et affecte ce nouveau rôle aux utilisateurs et utilisatrices non-administrateurs qui utilisent la capture de données.

## Création d’un rôle destiné aux utilisateurs qui capturent des données {#create-a-role-for-data-capture-users}

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs ou utilisatrices > Gestion des rôles, puis sur Nouveau rôle.
1. Saisissez le nom du rôle (par exemple Utilisateur ou utilisatrice capturant des données), ainsi qu’une description dans les champs appropriés, puis cliquez sur Suivant.
1. Dans l’écran Autorisations des rôles, cliquer sur Rechercher des autorisations, puis sélectionner Lecture des informations d’identification dans la liste des autorisations disponibles.
1. Cliquez sur OK, puis sur Terminer.

## Affectation du rôle de capture de données {#assign-the-data-capture-role}

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs et utilisatrices > Gestion des rôles, puis sur Rechercher.
1. Cliquez sur le rôle utilisateur de capture de données que vous avez créé.
1. Dans l’onglet Utilisateurs et utilisatrices/groupes de rôle, cliquer sur Rechercher des utilisateurs et utilisatrices/groupes.
1. Dans l’écran Rechercher des utilisateurs, des utilisatrices et des groupes, cliquez sur Rechercher, sélectionnez les utilisateurs et utilisatrices nécessitant le rôle utilisateur de capture de données, puis cliquez sur OK.
1. Dans l’écran Modifier le rôle, cliquez sur Enregistrer.
