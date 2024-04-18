---
title: Extension AEM Brackets
description: Découvrez comment utiliser l’extension Adobe Experience Manager pour Brackets.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 92%

---

# Extension AEM Brackets{#aem-brackets-extension}

## du commerce électronique {#overview}

L’extension AEM Brackets offre un workflow fluide pour modifier les composants AEM et les bibliothèques clientes. Elle tire parti de la puissance de l’éditeur de code [Brackets](https://brackets.io/) qui donne accès aux fichiers et calques Photoshop depuis l’éditeur de code. La synchronisation simplifiée (aucun Maven ou File Vault requis) grâce à l’extension améliore le rendement des développeurs et permet également aux développeurs de front-end ayant des connaissances AEM limitées de participer à des projets. Cette extension prend également en charge le [langage de modèle HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) qui élimine la complexité des JSP pour faciliter et sécuriser le développement de composants.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Fonctions {#features}

Les principales fonctionnalités de l’extension AEM Brackets son les suivantes :

* La synchronisation automatisée des fichiers modifiés avec l’instance de développement AEM
* La synchronisation bidirectionnelle manuelle des fichiers et des dossiers
* La synchronisation complète des packages de contenu du projet
* Le remplissage du code HTL pour les expressions et les instructions de bloc `data-sly-*`

En outre, Brackets est fourni avec de nombreuses fonctionnalités utiles pour les développeurs et développeuses front-end AEM :

* Prise en charge des fichiers Photoshop pour extraire des informations d’un fichier PSD, comme des calques, des mesures, des couleurs, des polices, du texte, etc.
* Indicateurs de code du PSD, pour facilement réutiliser les informations extraites dans le code.
* Prise en charge de préprocesseurs CSS, comme LESS et SCSS.
* Ainsi que des centaines d’extensions supplémentaires répondant à des besoins plus spécifiques.

## Installation {#installation}

### Brackets {#brackets}

L’extension AEM Brackets prend en charge la version 1.0 de Brackets ou les versions ultérieures.

Téléchargez la dernière version de Brackets sur [Brackets.io](https://brackets.io/).

### Extension {#the-extension}

Pour installer l’extension, procédez comme suit :

1. Ouvrez Brackets. Dans le menu **Fichier**, sélectionnez **Extension Manager...**
1. Saisissez **AEM** dans la barre de recherche et recherchez **Extension AEM Brackets**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Cliquez sur **Installer**.
1. Fermez la boîte de dialogue et Extension Manager une fois l’installation terminée.

## Prise en main {#getting-started}

### Projet de package de contenu {#the-content-package-project}

Une fois l’extension installée, vous pouvez commencer à développer des composants AEM en ouvrant un dossier de package de contenu dans votre système de fichiers avec Brackets.

Le projet doit contenir au minimum :

1. un dossier `jcr_root` (par exemple, `myproject/jcr_root`)

1. un fichier `filter.xml` (par exemple `myproject/META-INF/vault/filter.xml`). Pour plus de détails sur la structure du fichier `filter.xml`, reportez-vous à la [définition du filtre d’espace de travail](https://jackrabbit.apache.org/filevault/filter.html).

Dans le menu **Fichier** de Brackets, choisissez **Ouvrir le dossier...** et choisissez le dossier `jcr_root` ou le dossier du projet parent.

>[!NOTE]
>
>Si vous n’avez pas de votre propre projet avec un module de contenu, vous pouvez essayer la méthode [Exemple HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). Sur GitHub, cliquez sur **Télécharger le fichier ZIP**, extrayez les fichiers localement et, comme indiqué ci-dessus, ouvrez le dossier `jcr_root` dans Brackets. Suivez ensuite les étapes ci-dessous pour configurer les **paramètres du projet** et enfin téléchargez le package entier vers votre instance de développement AEM en **exportant le package de contenu** comme indiqué plus bas dans la section Synchronisation complète des packages de contenu du projet.
>
>Après ces étapes, vous devriez être en mesure d’accéder à l’URL `/content/todo.html` sur votre instance de développement AEM, d’apporter des modifications au code dans Brackets et de voir comment, après une actualisation dans le navigateur Web, les modifications ont été immédiatement synchronisées avec le serveur AEM.

### Paramètres du projet {#project-settings}

Pour synchroniser le contenu avec une instance de développement AEM dans les deux sens, vous devez définir les paramètres du projet. Pour cela, accédez au menu **AEM** et choisissez **Paramètres du projet...**

![chlimage_1-55](assets/chlimage_1-55a.png)

Les paramètres du projet vous permettent de définir les éléments suivants :

1. l’URL du serveur (par exemple `http://localhost:4502`) ;
1. Permet de tolérer les serveurs qui ne possèdent pas de certificat HTTPS valide (ne cochez pas, sauf si nécessaire).
1. le nom d’utilisateur ou d’utilisatrice qui a servi à synchroniser le contenu (par exemple `admin`) ;
1. le mot de passe de l’utilisateur ou de l’utilisatrice (par exemple `admin`).

## Synchronisation du contenu {#synchronizing-content}

L’extension AEM Brackets fournit les types de synchronisation de contenu suivants pour les fichiers et dossiers autorisés par les règles de filtrage définies dans `filter.xml` :

### Synchronisation automatisée des fichiers modifiés {#automated-synchronization-of-changed-files}

Cela synchronise uniquement les modifications de Brackets vers l’instance AEM, jamais l’inverse.

### Synchronisation bidirectionnelle manuelle {#manual-bidirectional-synchronization}

Dans l’Explorateur de projet, ouvrez le menu contextuel en cliquant avec le bouton droit de la souris sur un fichier ou un dossier, et accédez aux options **Exporter vers le serveur** ou **Importer depuis le serveur**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si l’entrée sélectionnée se situe en dehors du dossier `jcr_root`, les entrées du menu contextuel **Exporter vers le serveur** et **Importer depuis le serveur** sont désactivées.

### Synchronisation complète des packages de contenu {#full-content-package-synchronization}

Dans le **AEM** , **Exporter le package de contenu** ou **Importer un module de contenu** Les options vous permettent de synchroniser l’ensemble du projet avec le serveur.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Statut de la synchronisation {#synchronization-status}

L’extension AEM Brackets comporte une icône de notification dans la barre d’outils située à droite de la fenêtre Brackets, qui indique le statut de la dernière synchronisation :

* vert : tous les fichiers ont été synchronisés.
* bleu : une opération de synchronisation est en cours.
* jaune : certains fichiers n’ont pas été synchronisés.
* rouge : aucun fichier n’a été synchronisé.

Cliquez sur l’icône de notification pour ouvrir la boîte de dialogue Rapport sur le statut de la synchronisation qui répertorie les statuts de tous les fichiers synchronisés.

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
