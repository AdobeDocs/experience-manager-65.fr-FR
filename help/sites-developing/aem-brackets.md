---
title: Extension AEM Brackets
seo-title: Extension AEM Brackets
description: 'null'
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 55%

---


# Extension AEM Brackets{#aem-brackets-extension}

## Présentation {#overview}

L’extension AEM Brackets offre un workflow fluide pour modifier les composants AEM et les bibliothèques clientes. Elle tire parti de la puissance de l’éditeur de code [Brackets](https://brackets.io/) qui donne accès aux fichiers et calques Photoshop depuis l’éditeur de code. La synchronisation simplifiée (aucun Maven ou File Vault requis) grâce à l’extension améliore le rendement des développeurs et permet également aux développeurs de front-end ayant des connaissances AEM limitées de participer à des projets. This extension also provides some support for the [HTML Template Language (HTL)](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html), which takes away the complexity of JSP to make component development easier and more secure.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Fonctionnalités {#features}

Les principales fonctionnalités de l’extension AEM Brackets sont les suivantes :

* Synchronisation automatisée des fichiers modifiés vers l’instance de développement AEM.
* Synchronisation bidirectionnelle manuelle des fichiers et des dossiers.
* Synchronisation complète des packages de contenu du projet.
* HTL code completion for expressions and `data-sly-*` block statements.

En outre, Brackets propose de nombreuses fonctionnalités utiles pour les développeurs de front-end AEM :

* Prise en charge des fichiers Photoshop pour extraire les informations d’un fichier PSD, comme des calques, des mesures, des couleurs, des polices, du texte, etc.
* Conseils relatifs au code du fichier PSD pour réutiliser facilement cette information extraite dans le code.
* Prise en charge du préprocesseur CSS, comme LESS et SCSS.
* Et des centaines d’extensions supplémentaires qui répondent à des besoins plus précis.

## Installation {#installation}

### Brackets {#brackets}

L’extension AEM Brackets prend en charge les versions 1.0 ou ultérieures.

Download the latest Brackets version from [brackets.io](https://brackets.io/).

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

1. un `jcr_root` dossier (ex. `myproject/jcr_root`)

1. a `filter.xml` file (e.g. `myproject/META-INF/vault/filter.xml`); for more details about the structure of the `filter.xml` file please see the [Workspace Filter definition](https://jackrabbit.apache.org/filevault/filter.html).

Dans le menu **Fichier** de Brackets, choisissez **Ouvrir le dossier...** et choisissez le dossier `jcr_root` ou le dossier du projet parent.

>[!NOTE]
>
>If you don&#39;t have of your own a project with a content-package, you can try the [HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). On GitHub, click **Download ZIP**, extract the files locally, and as instructed above, open the `jcr_root` folder in Brackets. Then follow the steps below to setup the **Project Settings**, and finally upload the whole package to your AEM development instance by doing an **Export Content Package** as instructed further down in the Full Content-Package Synchronization section.
>
>After these steps, you should be able to access the `/content/todo.html` URL on your AEM development instance and you can start doing modifications to the code in Brackets and see how, after doing a refresh in the web browser, the changes were immediately synchronized to the AEM server.

### Paramètres du projet {#project-settings}

Pour synchroniser le contenu avec une instance de développement AEM dans les deux sens, vous devez définir les paramètres du projet. This can be done by going to the **AEM** menu and choosing **Project Settings…**

![chlimage_1-55](assets/chlimage_1-55a.png)

Les paramètres du projet permettent de définir :

1. The server URL (e.g. `http://localhost:4502`)
1. Permet de tolérer les serveurs ne disposant pas d&#39;un certificat HTTPS valide (ne cochez pas cette case, sauf si nécessaire).
1. Le nom d’utilisateur qui a servi à synchroniser le contenu (par exemple `admin`)
1. The user&#39;s password (e.g. `admin`)

## Synchronisation du contenu {#synchronizing-content}

The AEM Brackets Extension provides following types of content synchronization for files and folders that are allowed by the filtering rules defined in `filter.xml`:

### Synchronisation automatisée des fichiers modifiés {#automated-synchronization-of-changed-files}

Ne synchronise que les changements de Brackets vers l’instance d’AEM, mais jamais l’inverse.

### Synchronisation bidirectionnelle manuelle {#manual-bidirectional-synchronization}

In the Project Explorer, open the contextual menu by right-clicking on any file or folder, and the **Export to Server** or **Import from Server** options can be accessed.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>If the selected entry is outside of the `jcr_root` folder, the **Export to Server** and **Import from Server** contextual menu entries are disabled.

### Synchronisation complète des modules de contenu {#full-content-package-synchronization}

In the **AEM** menu, the **Export Content Package** or **Import Content Package** options allow to synchronize the whole project with the server.

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
>Additionally, `.vltignore` files are supported for excluding content from synchronizing to and from the repository.

## Modification du code HTL {#editing-htl-code}

L’extension AEM Brackets propose également une fonction de remplissage automatique pour faciliter l’écriture d’attributs et d’expressions HTL.

### Remplissage automatique des attributs {#attribute-auto-completion}

1. Dans un attribut HTML, tapez `sly`. L’attribut est automatiquement rempli sur `data-sly-`.
1. Sélectionnez l’attribut HTL dans la liste déroulante.

### Remplissage automatique des expressions {#expression-auto-completion}

Within an expression `${}`, common variable names are auto-completed.

## Informations supplémentaires {#more-information}

L’extension AEM Brackets est un projet open source, hébergé sur GitHub par l’entreprise [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), sous licence Apache, version 2.0 :

* Référentiel de code : [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension ](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License, version 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

The Brackets code editor is also an open-source project, hosted on GitHub by the [Adobe Systems Incorporated](https://github.com/adobe) organization:

* Code repository: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

N’hésitez pas à apporter votre contribution !
