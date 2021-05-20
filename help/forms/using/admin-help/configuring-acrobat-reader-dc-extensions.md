---
title: Configuration des extensions d’Acrobat Reader DC pour la capture de données
seo-title: Configuration des extensions d’Acrobat Reader DC pour la capture de données
description: Découvrez comment configurer des extensions d’Acrobat Reader DC pour la capture de données.
seo-description: Découvrez comment configurer des extensions d’Acrobat Reader DC pour la capture de données.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 98%

---

# Configuration des extensions d’Acrobat Reader DC pour la capture de données {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Si les utilisateurs de votre installation AEM Forms utilisent la fonctionnalité de capture des données de Content Services (obsolète), nous vous recommandons de créer un rôle avec un accès en lecture seule pour ces utilisateurs.

***Remarque ** : Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Pour en savoir plus sur la configuration de Content Services (obsolète), voir [Administration de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

La capture des données nécessite d’affecter un rôle utilisateur pour l’accès à SampleReaderExtensionsCredential. Vous pouvez affecter le rôle Trust Administrator standard mais n’oubliez pas que ce rôle confère à des utilisateurs type, non administrateurs, de puissants privilèges d’administrateur capables de contrôler les paramètres d’approbation PKI et de gérer les informations d’identification PKI. Cela peut compromettre la sécurité de votre installation AEM Forms dans un environnement de production. Il est recommandé que l’administrateur système AEM Forms crée un nouveau rôle qui accorde un accès en lecture seule uniquement à Trust Store et affecte ce nouveau rôle à des utilisateurs non administrateurs utilisant la capture des données.

## Création d’un rôle destiné aux utilisateurs qui capturent des données {#create-a-role-for-data-capture-users}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nouveau rôle.
1. Saisissez le nom du rôle (par exemple Utilisateur capturant des données), ainsi qu’une description dans les champs appropriés, puis cliquez sur Suivant.
1. Dans l’écran Droits des rôles, cliquez sur Rechercher des droits, puis sélectionnez Lecture des informations d’identification dans la liste des autorisations disponibles.
1. Cliquez sur OK, puis sur Terminer.

## Affectation du rôle de capture de données  {#assign-the-data-capture-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Rechercher.
1. Cliquez sur le rôle d’utilisateur de la capture des données que vous venez de créer.
1. Dans l’onglet Utilisateurs/groupes de rôle, cliquez sur Rechercher des utilisateurs/groupes.
1. Dans l’écran Rechercher des utilisateurs et des groupes, cliquez sur Rechercher, sélectionnez les utilisateurs nécessitant un rôle de capture de données, puis cliquez sur OK.
1. Dans l’écran Modifier le rôle, cliquez sur Enregistrer.
