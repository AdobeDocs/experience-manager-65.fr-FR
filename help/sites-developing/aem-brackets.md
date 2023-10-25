---
title: Extension AEM Brackets
seo-title: AEM Brackets Extension
description: Découvrez comment utiliser l’extension Adobe Experience Manager pour Brackets.
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 67%

---

# Extension AEM Brackets{#aem-brackets-extension}

## du commerce électronique {#overview}

L’extension AEM Brackets offre un workflow fluide pour modifier les composants AEM et les bibliothèques clientes. Elle tire parti de la puissance de l’éditeur de code [Brackets](https://brackets.io/) qui donne accès aux fichiers et calques Photoshop depuis l’éditeur de code. La synchronisation simplifiée (aucun Maven ou File Vault requis) grâce à l’extension améliore le rendement des développeurs et permet également aux développeurs de front-end ayant des connaissances AEM limitées de participer à des projets. Cette extension prend également en charge le [langage de modèle HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) qui élimine la complexité des JSP pour faciliter et sécuriser le développement de composants.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Fonctions {#features}

Les principales fonctionnalités de l’extension AEM Brackets sont les suivantes :

* La synchronisation automatisée des fichiers modifiés avec l’instance de développement AEM
* La synchronisation bidirectionnelle manuelle des fichiers et des dossiers
* La synchronisation complète des packages de contenu du projet
* Le remplissage du code HTL pour les expressions et les instructions de bloc `data-sly-*`

En outre, Brackets s’accompagne de nombreuses fonctionnalités utiles pour les développeurs de polices AEM :

* Prise en charge des fichiers Photoshop pour extraire des informations d’un fichier de PSD, comme des calques, des mesures, des couleurs, des polices, du texte, etc.
* Conseils sur le code du PSD, pour réutiliser facilement ces informations extraites dans le code.
* Prise en charge de préprocesseurs CSS, comme LESS et SCSS.
* Et des centaines d’extensions supplémentaires qui répondent à des besoins plus spécifiques.

## Installation {#installation}

### Brackets {#brackets}

L’extension AEM Brackets prend en charge Brackets version 1.0 ou ultérieure.

Téléchargez la dernière version de Brackets sur [Brackets.io](https://brackets.io/).

### L’extension {#the-extension}

Pour installer l’extension, procédez comme suit :

1. Ouvrez Brackets. Dans le menu **Fichier**, sélectionnez **Extension Manager...**
1. Entrée **AEM** dans la barre de recherche et recherchez **Extension AEM Brackets**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Cliquez sur **Installer**.
1. Fermez la boîte de dialogue et l’Extension Manager une fois l’installation terminée.

## Prise en main {#getting-started}

### Le projet Content-Package {#the-content-package-project}

Une fois l’extension installée, vous pouvez commencer à développer AEM composants en ouvrant un dossier content-package à partir de votre système de fichiers avec Brackets.

Le projet doit contenir au moins :

1. a `jcr_root` Dossier (par exemple, `myproject/jcr_root`)

1. a `filter.xml` (par exemple, `myproject/META-INF/vault/filter.xml`) ; pour plus d’informations sur la structure de la variable `filter.xml` veuillez consulter le fichier [Définition du filtre Workspace](https://jackrabbit.apache.org/filevault/filter.html).

Dans le menu **Fichier** de Brackets, choisissez **Ouvrir le dossier...** et choisissez le dossier `jcr_root` ou le dossier du projet parent.

>[!NOTE]
>
>Si votre projet n’a pas de package de contenu, vous pouvez essayer d’appliquer l’[exemple HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). Sur GitHub, cliquez sur **Télécharger le fichier ZIP**, extrayez les fichiers localement et, comme indiqué ci-dessus, ouvrez le dossier `jcr_root` dans Brackets. Suivez ensuite les étapes ci-dessous pour configurer les **paramètres du projet** et enfin téléchargez le package entier vers votre instance de développement AEM en **exportant le package de contenu** comme indiqué plus bas dans la section Synchronisation complète des packages de contenu du projet.
>
>Après ces étapes, vous devriez être en mesure d’accéder à l’URL `/content/todo.html` sur votre instance de développement AEM, d’apporter des modifications au code dans Brackets et de voir comment, après une actualisation dans le navigateur Web, les modifications ont été immédiatement synchronisées avec le serveur AEM.

### Paramètres du projet {#project-settings}

Pour synchroniser le contenu avec une instance de développement AEM dans les deux sens, vous devez définir les paramètres du projet. Pour cela, accédez au menu **AEM** et choisissez **Paramètres du projet...**

![chlimage_1-55](assets/chlimage_1-55a.png)

Les paramètres du projet permettent de définir :

1. L’URL du serveur (par exemple, `http://localhost:4502`)
1. s’il faut accepter les serveurs sans certificat HTTPS valide (ne pas cocher, sauf si nécessaire) ;
1. Nom d’utilisateur utilisé pour synchroniser le contenu (par exemple : `admin`)
1. Le mot de passe de l’utilisateur (par exemple : `admin`)

## Synchronisation du contenu {#synchronizing-content}

L’extension AEM Brackets fournit les types de synchronisation de contenu suivants pour les fichiers et dossiers autorisés par les règles de filtrage définies dans `filter.xml` :

### Synchronisation Automatisée Des Fichiers Modifiés {#automated-synchronization-of-changed-files}

Cela synchronise uniquement les modifications de Brackets vers l’instance AEM, mais jamais l’inverse.

### Synchronisation bidirectionnelle manuelle {#manual-bidirectional-synchronization}

Dans l’Explorateur de projet, ouvrez le menu contextuel en cliquant avec le bouton droit de la souris sur un fichier ou un dossier, et accédez aux options **Exporter vers le serveur** ou **Importer depuis le serveur**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si l’entrée sélectionnée se situe en dehors du dossier `jcr_root`, les entrées du menu contextuel **Exporter vers le serveur** et **Importer depuis le serveur** sont désactivées.

### Synchronisation complète des packages de contenu {#full-content-package-synchronization}

Dans le menu **AEM**, les options **Exporter le package de contenu** ou **Importer le package de contenu** permettent de synchroniser l’ensemble du projet avec le serveur.

![chlimage_1-57](assets/chlimage_1-57a.png)

### État de synchronisation {#synchronization-status}

L’extension AEM Brackets comporte une icône de notification dans la barre d’outils située à droite de la fenêtre Brackets, qui indique l’état de la dernière synchronisation :

* vert : tous les fichiers ont été synchronisés avec succès
* blue : une opération de synchronisation est en cours
* jaune : certains fichiers n’ont pas été synchronisés
* rouge : aucun des fichiers n’a été synchronisé

Cliquez sur l’icône de notification pour ouvrir la boîte de dialogue Rapport d’état de synchronisation qui répertorie tous les états de chaque fichier synchronisé.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Seul le contenu marqué comme inclus par les règles de filtrage de `filter.xml` est synchronisé, quelle que soit la méthode de synchronisation appliquée.
>
>De plus, les fichiers `.vltignore` sont pris en charge pour exclure le contenu de la synchronisation bidirectionnelle avec le référentiel.

## Modification du code HTL {#editing-htl-code}

L’extension AEM Brackets propose également une fonction de remplissage automatique pour faciliter l’écriture d’attributs et d’expressions HTL.

### Remplissage automatique des attributs {#attribute-auto-completion}

1. Dans un attribut HTML, tapez `sly`. L’attribut est automatiquement rempli sur `data-sly-`.
1. Sélectionnez l’attribut HTL dans la liste déroulante.

### Remplissage automatique des expressions {#expression-auto-completion}

Dans une expression `${}`, les noms communs des variables sont remplis automatiquement.

## Informations supplémentaires {#more-information}

L’extension AEM Brackets est un projet open source, hébergé sur GitHub par l’entreprise [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), sous licence Apache, version 2.0 :

* Référentiel de code : [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension ](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licence Apache, version 2.0 : [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L’éditeur de code Brackets est également un projet open source, hébergé sur GitHub par l’entreprise [Adobe Systems Incorporated](https://github.com/adobe) :

* Référentiel de code : [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

N’hésitez pas à apporter votre contribution !
