---
title: Accès WebDAV
description: Découvrez comment accéder à Adobe Experience Manager à l’aide de WebDAV.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 99%

---

# Accès WebDAV{#webdav-access}

Pour vous connecter à AEM via WebDAV avec KDE :

Dans AEM, la prise en charge de WebDAV permet d’afficher et de modifier le contenu du référentiel. La connexion par le biais de WebDAV permet d’accéder directement au référentiel de contenu depuis votre ordinateur de bureau. Les fichiers texte et PDF ajoutés au référentiel par le biais de la connexion WebDAV sont automatiquement indexés en texte intégral et peuvent être recherchés avec les interfaces de recherche standard et via les API Java™ standard.

## Général {#general}

[Les instructions détaillées par système d’exploitation](/help/sites-administering/webdav-access.md#connecting-via-webdav) sont incluses dans ce document. Toutefois, pour se connecter à votre référentiel à l’aide du protocole WebDAV, vous devez pointer votre client WebDAV vers l’emplacement suivant :

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Cette adresse URL, lors d’une connexion au niveau du système d’exploitation, permet à WebDAV d’accéder à l’espace de travail par défaut (`crx.default`). Si cette approche est plus simple pour l’utilisateur, elle n’offre toutefois pas la flexibilité supplémentaire de spécifier des noms d’espace de travail, ce qui peut être effectué à l’aide d’[adresses URL WebDAV](/help/sites-administering/webdav-access.md#webdav-urls) supplémentaires.

AEM affiche le contenu du référentiel comme suit :

* Un nœud du type `nt:folder` s’affiche sous la forme d’un dossier. Les nœuds situés sous le nœud `nt:folder` s’affichent comme contenu du dossier.

* Un nœud du type `nt:file` s’affiche sous la forme d’un fichier. Les nœuds situés sous le nœud `nt:file` ne sont pas répertoriés, mais ils constituent le contenu du fichier.

Lorsque vous utilisez WebDAV pour créer et modifier des dossiers et des fichiers, AEM crée et modifie les nœuds `nt:folder` et `nt:file` nécessaires. Si vous prévoyez d’utiliser WebDAV pour importer et exporter du contenu, utilisez, autant que possible, les types de nœuds `nt:file` et `nt:folder`.

>[!NOTE]
>
>Avant de configurer WebDAV, vérifiez les [exigences techniques](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL WebDAV {#webdav-urls}

L’URL du serveur WebDAV présente la structure suivante :

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Description</strong></td>
   <td>Hôte et port sur lequel AEM s’exécute</td>
   <td>Chemin d’accès vers l’application web du référentiel AEM</td>
   <td>Chemin vers lequel le servlet WebDAV est mappé</td>
   <td>Nom de l’espace de travail</td>
  </tr>
 </tbody>
</table>

Si vous modifiez l’élément d’espace de travail dans le chemin d’accès, vous pouvez mapper des espaces de travail autres que l’espace de travail par défaut (`crx.default`). Par exemple, pour mapper un espace de travail appelé `staging`, utilisez l’adresse URL suivante :

```xml
http://localhost:4502/crx/repository/staging
```

## Connexion par le biais de WebDAV {#connecting-via-webdav}

[Comme mentionné ci-dessus](/help/sites-administering/webdav-access.md#general), pour se connecter au référentiel à l’aide du protocole WebDAV, vous pointez le client WebDAV vers l’emplacement de votre référentiel. Toutefois, selon le système d’exploitation, les étapes de connexion de votre client diffèrent et il peut y avoir une configuration requise du système d’exploitation.

Des instructions sur la connexion des systèmes d’exploitation suivants sont disponibles :

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Pour connecter correctement un système Microsoft® Windows 7 (et version ultérieure) à une instance d’AEM qui n’est pas sécurisée avec SSL, l’option d’établissement d’une authentification de base par un réseau non sécurisé doit être activée explicitement dans Windows. Cette capacité nécessite une modification du registre Windows du WebClient.

Une fois le registre mis à jour, l’instance d’AEM peut être mappée en tant que lecteur.

#### Configuration de Windows 7 et version ultérieure {#windows-and-greater-configuration}

Pour mettre à jour le registre afin d’autoriser une authentification de base sur un réseau non sécurisé :

1. Localisez la sous-clé de registre suivante :

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Définissez la sous-clé d’entrée de registre `BasicAuthLevel` sur une valeur égale ou supérieure à `2`.

   Si elle n’est pas présente, ajoutez la sous-clé.

1. Redémarrez le système pour que la modification du registre prenne effet.

>[!NOTE]
>
>Adobe vous recommande de créer un utilisateur ou une utilisatrice Windows avec les mêmes informations d’identification que l’utilisateur ou l’utilisatrice du référentiel, faute de quoi vous risquez de rencontrer des conflits d’autorisations.

#### Configuration de Windows 8 {#windows-configuration}

Sous Windows 8, vous devez également modifier l’entrée de registre [comme indiqué pour Windows 7 et version ultérieure](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Toutefois, avant d’effectuer cette tâche, l’Expérience utilisateur doit être activée pour afficher l’entrée de registre.

Pour ce faire, ouvrez **Server Manager**, puis **Fonctionnalités**, **Ajouter des fonctionnalités** et enfin, **Expérience utilisateur**.

Après le redémarrage, l’entrée de registre décrite pour Windows 7 et versions ultérieures est disponible. Modifiez-la comme décrit pour Windows 7 et versions ultérieures.

#### Se connecter sous Windows {#connecting-in-windows}

Pour vous connecter à AEM via WebDAV dans un environnement Windows :

1. Ouvrez l’**Explorateur Windows** ou l’**Explorateur de fichiers**, puis cliquez sur **Ordinateur** ou **Ce PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Pour démarrer l’assistant, cliquez sur **Mapper un lecteur réseau**.
1. Saisissez les informations du mappage :

   * **Lecteur** : choissisez n’importe quelle lettre disponible.
   * **Dossier** : `http://localhost:4502`
   * Cochez **Se connecter à l’aide d’informations d’identification différentes**.

   Cliquez sur Terminer.

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Si AEM se trouve sur un autre port, utilisez ce numéro de port au lieu du port 4502. De même, si vous n’exécutez pas le référentiel de contenu sur votre ordinateur local, remplacez `localhost` par le nom ou l’adresse IP du serveur correspondant.

1. Entrez le nom d’utilisateur `admin` et le mot de passe `admin`. Adobe recommande d’utiliser le compte administrateur préconfiguré pour le test.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. L’assistant se ferme. Le lecteur qui vient d’être mappé est ouvert dans l’Explorateur Windows ou dans l’Explorateur de fichiers.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows a désormais mappé AEM comme lecteur via WebDAV et vous pouvez l’utiliser comme n’importe quel autre lecteur.

### macOS {#macos}

Aucune étape de configuration n’est nécessaire pour se connecter par le biais de WebDAV sous Mac OS. Vous pouvez vous connecter au serveur WebDAV.

1. Dans le **Finder**, cliquez sur **Aller** puis sur **Se connecter au serveur** ou appuyez sur **Commande+k**.
1. Dans la fenêtre **Se connecter au serveur**, saisissez l’emplacement d’AEM :

   * `http://localhost:4502`

   >[!NOTE]
   >
   >Si AEM se trouve sur un autre port, utilisez ce numéro de port au lieu du port 4502. De même, si vous n’exécutez pas le référentiel de contenu sur votre ordinateur local, remplacez `localhost` par le nom ou l’adresse IP du serveur correspondant.

1. Lorsque vous êtes invité à vous authentifier, saisissez le nom d’utilisateur `admin` et le mot de passe `admin`. Adobe recommande d’utiliser le compte administrateur préconfiguré pour le test.

macOS est maintenant connecté à AEM via WebDAV et vous pouvez l’utiliser comme n’importe quel autre dossier de votre Mac.

### Linux® {#linux}

La connexion via WebDAV sous Linux® ne nécessite aucune configuration, mais implique quelques étapes pour établir la connexion, qui varient selon votre environnement de bureau.

#### GNOME {#gnome}

Pour vous connecter à AEM via WebDAV avec GNOME :

1. Dans Nautilus (explorateur de fichiers), sélectionnez **Emplacements** et sélectionnez **Se connecter au serveur**.
1. Dans la fenêtre **Se connecter à un serveur**, sélectionnez le type de service WebDAV (HTTP).

1. Dans **Serveur**, saisissez `http://localhost:4502/crx/repository/crx.default`.

   >[!NOTE]
   >
   >Si AEM se trouve sur un autre port, utilisez ce numéro de port au lieu du port 4502. De même, si vous n’exécutez pas le référentiel de contenu sur votre ordinateur local, remplacez `localhost` par le nom ou l’adresse IP du serveur correspondant.

1. Sous **Dossier**, saisissez `/dav`.
1. Saisissez le nom d’utilisateur `admin`. Adobe recommande d’utiliser le compte administrateur préconfiguré pour le test.
1. Ne renseignez pas le port et saisissez un nom pour la connexion.
1. Cliquez sur **Connecter**. AEM vous invite à saisir votre mot de passe.
1. Saisissez le mot de passe `admin` et cliquez sur **Connecter**.

GNOME a maintenant monté AEM sous la forme d’un volume, que vous pouvez utiliser comme n’importe quel autre volume.

#### KDE {#kde}

1. Ouvrez l’assistant Dossier réseau.
1. Sélectionnez **WebFolder** (webdav), puis cliquez sur Suivant.
1. Sous **Nom**, saisissez un nom de connexion.
1. Dans **Utilisateur**, saisissez `admin.` Adobe vous recommande d’utiliser le compte administrateur préconfiguré.
1. Dans **Serveur**, saisissez `http://localhost:4502/crx/repository/crx.default`.

   >[!NOTE]
   >
   >Si AEM se trouve sur un autre port, utilisez ce numéro de port au lieu du port 4502. De même, si vous n’exécutez pas le référentiel de contenu sur votre ordinateur local, remplacez `localhost` par le nom ou l’adresse IP du serveur correspondant.

1. Sous **Dossier**, saisissez `dav`.

1. Cliquez sur **Enregistrer et connecter**.
1. Lorsque vous êtes invité à saisir votre mot de passe, saisissez `admin` et cliquez sur **Connecter**.

KDE a maintenant monté AEM sous la forme d’un volume, que vous pouvez utiliser comme n’importe quel autre volume.
