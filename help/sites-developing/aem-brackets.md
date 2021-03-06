---
title: Extension AEM Brackets
seo-title: Extension AEM Brackets
description: Extension AEM Brackets
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 55%

---

# Extension AEM Brackets{#aem-brackets-extension}

## Présentation {#overview}

L’extension AEM Brackets offre un workflow fluide pour modifier les composants AEM et les bibliothèques clientes. Elle tire parti de la puissance de l’éditeur de code [Brackets](https://brackets.io/) qui donne accès aux fichiers et calques Photoshop depuis l’éditeur de code. La synchronisation simplifiée (aucun Maven ou File Vault requis) grâce à l’extension améliore le rendement des développeurs et permet également aux développeurs de front-end ayant des connaissances AEM limitées de participer à des projets. Cette extension fournit également une prise en charge du [langage HTL (HTML Template Language)](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html), qui élimine la complexité de JSP pour faciliter et sécuriser le développement de composants.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Fonctions {#features}

Les principales fonctionnalités de l’extension AEM Brackets sont les suivantes :

* Synchronisation automatisée des fichiers modifiés vers l’instance de développement AEM.
* Synchronisation bidirectionnelle manuelle des fichiers et des dossiers.
* Synchronisation complète des packages de contenu du projet.
* Remplissage du code HTL pour les expressions et les instructions de bloc `data-sly-*`.

En outre, Brackets propose de nombreuses fonctionnalités utiles pour les développeurs de front-end AEM :

* Prise en charge des fichiers Photoshop pour extraire les informations d’un fichier PSD, comme des calques, des mesures, des couleurs, des polices, du texte, etc.
* Conseils relatifs au code du fichier PSD pour réutiliser facilement cette information extraite dans le code.
* Prise en charge du préprocesseur CSS, comme LESS et SCSS.
* Et des centaines d’extensions supplémentaires qui répondent à des besoins plus précis.

## Installation {#installation}

### Brackets {#brackets}

L’extension AEM Brackets prend en charge les versions 1.0 ou ultérieures.

Téléchargez la dernière version de Brackets à partir de [crochets.io](https://brackets.io/).

### L’extension {#the-extension}

Pour installer l’extension, procédez comme suit :

1. Ouvrez Brackets. Dans le menu **Fichier**, sélectionnez **Extension Manager...**
1. Entrez **AEM** dans la barre de recherche et recherchez l’**extension AEM Brackets**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Cliquez sur **Installer**.
1. Fermez la boîte de dialogue et Extension Manager, une fois l’installation terminée.

## Prise en main {#getting-started}

### Le projet de modules de contenu {#the-content-package-project}

Une fois l’extension installée, vous pouvez commencer à développer des composants AEM en ouvrant un dossier de modules de contenu à partir de votre système de fichiers avec Brackets.

Le projet doit contenir au moins :

1. un dossier `jcr_root` (par ex. `myproject/jcr_root`)

1. un fichier `filter.xml` (par ex. `myproject/META-INF/vault/filter.xml`); pour plus d’informations sur la structure du fichier `filter.xml`, consultez la [Définition du filtre d’espace de travail](https://jackrabbit.apache.org/filevault/filter.html).

Dans le menu **Fichier** de Brackets, choisissez **Ouvrir le dossier...** et choisissez le dossier `jcr_root` ou le dossier du projet parent.

>[!NOTE]
>
>Si vous ne disposez pas de votre propre projet avec un module de contenu, vous pouvez essayer l’ [exemple HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). Sur GitHub, cliquez sur **Télécharger ZIP**, extrayez les fichiers localement, puis, comme indiqué ci-dessus, ouvrez le dossier `jcr_root` dans Brackets. Suivez ensuite les étapes ci-dessous pour configurer les **paramètres du projet**, puis téléchargez enfin l’ensemble du module vers votre instance de développement AEM en effectuant une **exportation du module de contenu** comme indiqué plus bas dans la section Synchronisation complète des modules de contenu .
>
>Après ces étapes, vous devriez pouvoir accéder à l’URL `/content/todo.html` sur votre instance de développement AEM et vous pouvez commencer à apporter des modifications au code dans Brackets et voir comment, après une actualisation dans le navigateur web, les modifications ont été immédiatement synchronisées avec le serveur AEM.

### Paramètres du projet {#project-settings}

Pour synchroniser le contenu avec une instance de développement AEM dans les deux sens, vous devez définir les paramètres du projet. Pour ce faire, accédez au menu **AEM** et sélectionnez **Paramètres du projet..**.

![chlimage_1-55](assets/chlimage_1-55a.png)

Les paramètres du projet permettent de définir :

1. L’URL du serveur (par ex. `http://localhost:4502`)
1. Permet de tolérer les serveurs qui ne possèdent pas de certificat HTTPS valide (ne cochez pas, sauf si nécessaire).
1. Le nom d’utilisateur qui a servi à synchroniser le contenu (par exemple `admin`)
1. Mot de passe de l’utilisateur (par exemple, `admin`)

## Synchronisation du contenu {#synchronizing-content}

L’extension AEM Brackets fournit les types suivants de synchronisation de contenu pour les fichiers et dossiers autorisés par les règles de filtrage définies dans `filter.xml` :

### Synchronisation automatisée des fichiers modifiés {#automated-synchronization-of-changed-files}

Ne synchronise que les changements de Brackets vers l’instance d’AEM, mais jamais l’inverse.

### Synchronisation bidirectionnelle manuelle {#manual-bidirectional-synchronization}

Dans l’Explorateur de projets, ouvrez le menu contextuel en cliquant avec le bouton droit de la souris sur un fichier ou un dossier, et vous accédez aux options **Exporter vers le serveur** ou **Importer depuis le serveur**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si l’entrée sélectionnée se trouve en dehors du dossier `jcr_root` , les entrées du menu contextuel **Exporter vers le serveur** et **Importer depuis le serveur** sont désactivées.

### Synchronisation complète des modules de contenu {#full-content-package-synchronization}

Dans le menu **AEM**, les options **Exporter le module de contenu** ou **Importer le module de contenu** permettent de synchroniser l’ensemble du projet avec le serveur.

![chlimage_1-57](assets/chlimage_1-57a.png)

### État de la synchronisation {#synchronization-status}

L’extension AEM Brackets comporte une icône de notification dans la barre d’outils à droite de la fenêtre Brackets, qui indique l’état de la dernière synchronisation :

* vert - tous les fichiers ont été synchronisés avec succès
* bleu - une opération de synchronisation est en cours
* jaune - certains fichiers n’ont pas été synchronisés
* rouge - aucun des fichiers n’a été synchronisé

En cliquant sur l’icône de notification, vous ouvrez la boîte de dialogue du rapport d’état de la synchronisation qui répertorie tous les états de chaque fichier synchronisé.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Seul le contenu marqué comme inclus par les règles de filtrage de `filter.xml` est synchronisé, quelle que soit la méthode de synchronisation appliquée.
>
>En outre, les fichiers `.vltignore` sont pris en charge pour exclure le contenu de la synchronisation vers et depuis le référentiel.

## Modification du code HTL {#editing-htl-code}

L’extension AEM Brackets propose également une fonction de remplissage automatique pour faciliter l’écriture d’attributs et d’expressions HTL.

### Remplissage automatique des attributs {#attribute-auto-completion}

1. Dans un attribut HTML, tapez `sly`. L’attribut est automatiquement rempli sur `data-sly-`.
1. Sélectionnez l’attribut HTL dans la liste déroulante.

### Remplissage automatique des expressions  {#expression-auto-completion}

Dans une expression `${}`, les noms de variable courants sont renseignés automatiquement.

## Informations supplémentaires {#more-information}

L’extension AEM Brackets est un projet open source, hébergé sur GitHub par l’entreprise [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), sous licence Apache, version 2.0 :

* Référentiel de code : [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension ](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licence Apache, version 2.0 : [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L’éditeur de code Brackets est également un projet open source, hébergé sur GitHub par l’organisation [Adobe Systems Incorporated](https://github.com/adobe) :

* Référentiel de code : [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

N’hésitez pas à apporter votre contribution !
