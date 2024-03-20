---
title: Exemple d’intégration d’un composant brouillons et envois à une base de données
description: Référencez l’implémentation des services de données et de métadonnées personnalisés pour intégrer le composant brouillons et envois à une base de données.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 49%

---

# Exemple d’intégration d’un composant brouillons &amp; envois à la base de données {#sample-for-integrating-drafts-submissions-component-with-database}

## Aperçu de l’exemple {#sample-overview}

Le composant brouillons et envois du portail AEM Forms permet aux utilisateurs d’enregistrer leurs formulaires en tant que brouillons et de les envoyer ultérieurement à partir de n’importe quel périphérique. En outre, les utilisateurs peuvent afficher leurs formulaires envoyés sur le portail. Pour activer cette fonctionnalité, AEM Forms fournit des services de données et de métadonnées pour stocker les données renseignées par un utilisateur dans le formulaire et les métadonnées de formulaire associées aux brouillons et aux formulaires envoyés. Ces données sont stockées dans le référentiel CRX, par défaut. Cependant, lorsque les utilisateurs interagissent avec les formulaires via AEM instance de publication, qui se trouve généralement en dehors du pare-feu de l’entreprise, les entreprises peuvent vouloir personnaliser le stockage des données pour qu’il soit plus sécurisé et fiable.

L’exemple présenté dans ce document est une implémentation de référence des services de données et de métadonnées personnalisés pour intégrer le composant brouillons et envois à une base de données. La base de données utilisée dans l’exemple d’implémentation est : **MySQL 5.6.24**. Cependant, vous pouvez intégrer le composant brouillons et envois à n’importe quelle base de données de votre choix.

>[!NOTE]
>
>* Les exemples et configurations décrits dans ce document sont conformes à MySQL 5.6.24 et vous devez les remplacer de manière appropriée pour votre système de base de données.
>* Vérifiez que vous avez installé la dernière version du module complémentaire AEM Forms. Pour obtenir la liste des packages disponibles, voir la section [Versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) article.
>* L’exemple de package fonctionne uniquement avec les actions d’envoi de formulaires adaptatifs.

## Installer et configurer l’exemple {#set-up-and-configure-the-sample}

Effectuez les étapes suivantes, sur toutes les instances d’auteur et de publication, pour installer et configurer l’exemple :

1. Téléchargez le package suivant **aem-fp-db-integration-sample-pkg-6.1.2.zip** vers votre système de fichiers.

   Exemple de package pour l&#39;intégration à une base de données

[Obtenir le fichier](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Accédez au gestionnaire de package AEM à l’adresse https://[*host*]:[*port*]/crx/packmgr/.
1. Cliquez sur **[!UICONTROL Upload Package]** (Télécharger le package).

1. Parcourez l’arborescence pour sélectionner le package **aem-fp-db-integration-sample-pkg-6.1.2.zip** et cliquez sur **[!UICONTROL OK]**.
1. Cliquez sur **[!UICONTROL Installer]** en regard du module pour installer le module.
1. Accédez à la page de **[!UICONTROL configuration de la console web AEM]**
à l’adresse https://[*host*]:[*port*]/system/console/configMgr.
1. Cliquez pour ouvrir **[!UICONTROL Forms Portal Draft and Submission Configuration]** (Configuration des brouillons et des envois du portail Forms) en mode d’édition.

1. Spécifiez les valeurs des propriétés comme décrit dans le tableau suivant :

   | **Propriété** | **Description** | **Valeur** |
   |---|---|---|
   | Service de données de brouillon du portail Formulaires | Identifiant du service de données de brouillon | formsportal.sampledataservice |
   | Service de métadonnées de brouillon du portail Formulaires | Identifiant du service de métadonnées de brouillon | formsportal.samplemetadataservice |
   | Service de données d’envoi du portail Formulaires | Identifiant du service de données d’envoi | formsportal.sampledataservice |
   | Service de métadonnées d’envoi du portail Formulaires | Identifiant du service de métadonnées d’envoi | formsportal.samplemetadataservice |
   | Service de données de signature en attente du portail Formulaires | Identificateur du service de données de signature en attente | formsportal.sampledataservice |
   | Service de métadonnées de signature en attente du portail Formulaires | Identificateur du service de métadonnées de signature en attente | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Les services sont résolus par leurs noms indiqués comme valeur de la clé `aem.formsportal.impl.prop` comme suit : 

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   Vous pouvez modifier les noms des tableaux de données et de métadonnées.

   Pour donner un nom différent au tableau de métadonnées :

   * Dans la configuration de la console web, recherchez et cliquez sur Exemple de mise en oeuvre du service de métadonnées Forms Portal. Vous pouvez modifier les valeurs de la source de données, du nom de la table des métadonnées/métadonnées supplémentaires.

   Pour attribuer un nom différent au tableau de données :

   * Dans la configuration de la console web, recherchez et cliquez sur Exemple de mise en oeuvre du service de données du portail Forms. Vous pouvez modifier les valeurs de la source de données et du nom du tableau de données.

   >[!NOTE]
   >
   >Si vous modifiez les noms du tableau, renseignez-les dans la configuration du portail Formulaires.

1. Laissez les autres configurations inchangées et cliquez sur **[!UICONTROL Save]** (Enregistrer).

1. La connexion à la base de données peut être effectuée via la source de données mise en pool de la connexion Apache Sling.
1. Pour la connexion Apache Sling, recherchez et cliquez pour ouvrir **[!UICONTROL Source de données en pool de la connexion Apache Sling]** en mode d’édition dans la configuration de la console web. Spécifiez les valeurs des propriétés comme décrit dans le tableau suivant :

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Valeur</strong></td>
  </tr>
  <tr>
   <td>Nom de la source de données</td>
   <td><p>Un nom de source de données pour filtrer les pilotes du pool de la source de données</p> <p><strong>Remarque : </strong><em>L’exemple d’implémentation utilise FormsPortal comme nom de la source de données.</em></p> </td>
  </tr>
  <tr>
   <td>Classe de pilote JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI de connexion JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>Nom d’utilisateur</td>
   <td>Nom d’utilisateur pour l’authentification et l’exécution d’actions sur les tables de base de données</td>
  </tr>
  <tr>
   <td>Mot de passe</td>
   <td>Mot de passe associé au nom d’utilisateur</td>
  </tr>
  <tr>
   <td>Isolation des transactions</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>Nombre max. de connexions actives</td>
   <td>1 000</td>
  </tr>
  <tr>
   <td>Nombre max. de connexions inactives</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Nombre min. de connexions inactives</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Taille initiale</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Attente max.</td>
   <td>100 000</td>
  </tr>
  <tr>
   <td>Test lors de l’emprunt</td>
   <td>Cochée</td>
  </tr>
  <tr>
   <td>Test en mode inactif</td>
   <td>Cochée</td>
  </tr>
  <tr>
   <td>Requête de validation</td>
   <td>Exemples de valeurs : SELECT 1(mysql), select 1 from dual (oracle), SELECT 1 (MS Sql Server) (validationQuery).</td>
  </tr>
  <tr>
   <td>Délai d’expiration des requêtes de validation</td>
   <td>10 000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Le pilote JDBC pour MySQL n’est pas fourni avec l’exemple. Assurez-vous que vous avez fourni les informations requises pour configurer le pool de connexions JDBC.
>* Pointez vos instances de création et de publication pour utiliser la même base de données. La valeur du champ URI de connexion JDBC doit être identique pour toutes les instances d’auteur et de publication.

1. Laissez les autres configurations inchangées et cliquez sur **[!UICONTROL Save]** (Enregistrer).

1. Si vous disposez déjà d’un tableau dans le schéma de base de données, passez à l’étape suivante.

   Dans le cas contraire, si vous ne disposez pas déjà d’un tableau dans le schéma de base de données, exécutez les instructions SQL suivantes pour créer des tableaux distincts pour les données, les métadonnées et les métadonnées supplémentaires dans le schéma de base de données :

   >[!NOTE]
   >
   >Vous n’avez pas besoin de bases de données différentes pour les instances de création et de publication. Utilisez la même base de données sur toutes les instances d’auteur et de publication.

   **Instruction SQL pour le tableau de données**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instruction SQL pour le tableau de métadonnées**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instruction SQL pour le tableau de métadonnées supplémentaires**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instruction SQL pour la table des commentaires**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. Si vous disposez déjà des tables (données, métadonnées et métadonnées supplémentaires) dans le schéma de base de données, exécutez les modifications de requête de tableau suivantes :

   **Instruction SQL pour la modification du tableau de données**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instruction SQL pour la modification du tableau de métadonnées**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >La requête d’ajout des métadonnées ALTER TABLE échoue si vous l’avez déjà effectuée et la colonne markedforDeletion est présente dans le tableau.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instruction SQL pour la modification du tableau additionalmetadatatable**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

L’exemple d’implémentation est maintenant configuré. Vous pouvez l’utiliser pour répertorier vos brouillons et envois tout en stockant toutes les données et métadonnées dans une base de données. Voyons maintenant comment les services de données et de métadonnées sont configurés dans l’exemple.

## Installer le fichier mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Effectuez les étapes suivantes, sur toutes les instances d’auteur et de publication, pour installer le fichier mysql-connector-java-5.1.39-bin.jar :

1. Accédez à `https://'[server]:[port]'/system/console/depfinder` et recherchez le package com.mysql.jdbc.
1. Dans la colonne Exported by (Exporté par), vérifiez si le package est exporté par un groupe.

   Continuez si le package n’est pas exporté par un groupe.

1. Accédez à `https://'[server]:[port]'/system/console/bundles` et cliquez sur **[!UICONTROL Install/Update]** (Installer/Mettre à jour).
1. Cliquez sur **[!UICONTROL Choose File]** (Choisir un fichier) et accédez au chemin permettant de sélectionner le fichier mysql-connector-java-5.1.39-bin.jar. Cochez également les cases **[!UICONTROL Start Bundle]** (Démarrer le groupe) et **[!UICONTROL Refresh Packages]** (Actualiser les packages).
1. Cliquez sur **[!UICONTROL Install (Installer) ou Update]** (Mettre à jour). Une fois cette opération effectuée, redémarrez le serveur.
1. (*Windows uniquement*) Désactivez le pare-feu système pour votre système d’exploitation.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande &quot;Ctrl + C&quot; pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

## Exemple de code pour le service de données et de métadonnées de portail de formulaires {#sample-code-for-forms-portal-data-and-metadata-service}

Le fichier zip suivant contient `FormsPortalSampleDataServiceImpl` et `FormsPortalSampleMetadataServiceImpl` (classes d’implémentation) pour les interfaces de service de données et de métadonnées. En outre, il contient toutes les classes requises pour la compilation des classes d’implémentation mentionnées ci-dessus.

[Obtenir le fichier](assets/sample_package.zip)

## Vérification de la longueur du nom de fichier  {#verify-length-of-the-file-name}

L’implémentation de la base de données de Forms Portal utilise un tableau de métadonnées supplémentaire. Le tableau comporte une clé primaire composite basée sur les colonnes Clé et Identifiant du tableau. MySQL autorise les clés primaires jusqu’à 255 caractères. Vous pouvez utiliser le script de validation côté client suivant pour vérifier la longueur du nom de fichier joint au widget de fichier. La validation est exécutée lorsqu’un fichier est joint. Le script fourni dans la procédure suivante affiche un message lorsque le nom de fichier est supérieur à 150 (extension comprise). Vous pouvez modifier le script pour vérifier un nombre différent de caractères.

Effectuez les étapes suivantes pour créer [une bibliothèque cliente](/help/sites-developing/clientlibs.md) et utilisez le script :

1. Connectez-vous à CRXDE et accédez à /etc/clientlibs/
1. Création d’un noeud de type **cq:ClientLibraryFolder** et indiquez le nom du noeud. Par exemple, `validation`.

   Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Cliquez avec le bouton droit sur le nœud, cliquez sur **[!UICONTROL Créer un nouveau fichier]** et créez un fichier avec l’extension .txt. Par exemple, `js.txt` Ajoutez le code suivant au fichier .txt nouvellement créé et cliquez sur **[!UICONTROL Enregistrer tout]**.

   ```javascript
   #base=util
    util.js
   ```

   Dans le code ci-dessus, `util` est le nom du dossier et`util.js` est le nom du fichier dans le dossier `util`. Le dossier `util` et le fichier `util.js` sont créés dans les étapes suivantes.

1. Cliquez avec le bouton droit sur le nœud `cq:ClientLibraryFolder` créé à l’étape 2 et sélectionnez Créer > Créer un dossier. Créez un dossier nommé `util`. Cliquez sur **[!UICONTROL Enregistrer tout]**. Cliquez avec le bouton droit sur le dossier `util` et sélectionnez Créer > Créer un fichier. Créez un fichier nommé `util.js`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Ajoutez le code suivant au fichier util.js et cliquez sur **[!UICONTROL Enregistrer tout]**. Le code valide la longueur du nom de fichier.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >Le script est destiné au composant de widget de pièce jointe prêt à l’emploi. Si vous avez personnalisé le widget de pièce jointe prêt à l’emploi, modifiez le script ci-dessus pour incorporer les modifications respectives.

1. Ajoutez la propriété suivante au dossier créé à l’étape 2, puis cliquez sur **[!UICONTROL Enregistrer tout]**.

   * **[!UICONTROL Nom :]** categories

   * **[!UICONTROL Type :]** Chaîne

   * **[!UICONTROL Valeur :]** fp.validation

   * **[!UICONTROL Option multiple :]** Activé 

1. Accédez à `/libs/fd/af/runtime/clientlibs/guideRuntime` et ajoutez la valeur `fp.validation` à la propriété embed.

1. Accédez à /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA et ajoutez la valeur `fp.validation` à la propriété embed.

   >[!NOTE]
   >
   >Si vous utilisez des bibliothèques client personnalisées au lieu des bibliothèques client guideRuntime et guideRuntimeWithXfa, utilisez le nom de catégorie pour intégrer la bibliothèque client créée dans cette procédure à vos bibliothèques personnalisées chargées lors de l’exécution.

1. Cliquez sur **[!UICONTROL Enregistrer tout.]** Désormais, lorsque le nom de fichier contient plus de 150 caractères (extension comprise), un message s’affiche.
