---
title: Développement dans CRXDE Lite
seo-title: Developing with CRXDE Lite
description: CRXDE Lite est intégré à AEM et permet d’effectuer des tâches de développement standard dans le navigateur.
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2134'
ht-degree: 100%

---

# Développement dans CRXDE Lite{#developing-with-crxde-lite}

Cette section explique comment développer votre application AEM à l’aide de CRXDE Lite.

Reportez-vous à la documentation de présentation pour plus d’informations sur les différents environnements de développement disponibles.

CRXDE Lite est intégré à CRX/CQ et permet d’effectuer des tâches de développement standard dans le navigateur. En vous connectant à CRXDE Lite, vous pouvez créer un projet, créer et modifier des fichiers (en .jsp et .java, par exemple), des dossiers, des modèles, des composants, des boîtes de dialogue, des nœuds, des propriétés et des bundles.
CRXDE Lite est recommandé si vous ne disposez pas d’un accès direct au serveur AEM, lorsque vous développez une application en étendant ou en modifiant les composants prêts à l’emploi et les bundles Java ou lorsque vous n’avez pas besoin d’un débogueur dédié, de la complétion de code et de la mise en surbrillance de la syntaxe.

>[!NOTE]
>
>À partir de la version 6.5.5.0 d’AEM, l’accès anonyme de CRXDE Lite n’est plus possible.
>Les utilisateurs sont redirigés vers l’écran de connexion.


>[!NOTE]
>
>Il est recommandé d’utiliser [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) et [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) pendant le développement du projet.

## Prise en main de CRXDE Lite {#getting-started-with-crxde-lite}

Pour commencer avec CRXDE Lite, procédez comme suit :

1. Installez AEM.
1. Dans votre navigateur, entrez `https://<host>:<port>/crx/de`. Par défaut, le paramètre est `https://localhost:4502/crx/de`.
1. Entrez votre **nom d’utilisateur** et votre **mot de passe**. Par défaut, il s’agit de `admin` et `admin`.

1. Cliquez sur **OK**.

L’interface utilisateur de CRXDE Lite est la suivante dans votre navigateur :

![chlimage_1-18](assets/crx-interface.jpg)

Vous pouvez désormais utiliser CRXDE Lite pour développer votre application.

## Présentation de l’interface utilisateur {#overview-of-the-user-interface}

CRXDE Lite offre les fonctionnalités suivantes :

<table>
 <tbody>
  <tr>
   <td>Barre de commutation supérieure</td>
   <td>Vous permet de basculer rapidement entre CRXDE Lite, le gestionnaire de modules et le partage de modules.</td>
  </tr>
  <tr>
   <td>Widget de chemin de nœud</td>
   <td><p>Affiche le chemin d’accès au nœud actuellement sélectionné.</p> <p>Vous pouvez également l’utiliser pour sauter vers un nœud, en entrant le chemin à la main ou en le collant à partir d’un autre endroit et en appuyant sur Entrée.</p> <p>Il permet aussi de rechercher des nœuds par nom de nœud. Entrez le nom du nœud que vous souhaitez rechercher et patientez (ou appuyez sur le symbole de recherche sur le côté droit). Entrez par exemple la chaîne <em>oak</em> dans le widget pour voir comment la recherche fonctionne. Si un ou plusieurs nœuds sont chargés dans le volet de l’explorateur, la liste s’affiche et vous pouvez sélectionner le chemin et appuyer sur Entrée pour y accéder. Notez que la recherche ne fonctionne que pour les nœuds actuellement chargés dans l’application cliente CRXDE dans le navigateur. Pour effectuer une recherche dans tout le référentiel, utilisez Outils, puis Requête.</p> </td>
  </tr>
  <tr>
   <td>Volet de l’explorateur</td>
   <td><p>Affiche une arborescence de tous les nœuds du référentiel.</p> <p>Cliquez sur un nœud pour afficher ses propriétés dans l’onglet <strong>Propriétés</strong>. Après avoir cliqué sur un nœud, vous pouvez sélectionner une action dans la barre d’outils. Cliquez à nouveau sur le nœud pour le renommer.</p> <p>Filtre de navigation dans l’arborescence (icône en forme de paire de jumelles) : vous permet de filtrer les nœuds du référentiel pour lesquels le nom contient le texte saisi. S’applique uniquement aux nœuds qui ont été chargés localement.<br /> </p> </td>
  </tr>
  <tr>
   <td>Volet de modification</td>
   <td><p>Onglet <strong>Accueil</strong> : permet de rechercher du contenu et/ou de la documentation et d’accéder aux ressources de développeurs (documentation, blog, base de connaissances) et au support (page d’accueil Adobe et centre de support).<br /> </p> <p>Double-cliquez sur un fichier dans le volet de <strong>l’explorateur</strong> pour afficher son contenu, par exemple un fichier .jsp ou un fichier .java. Vous pouvez ensuite le modifier et enregistrer les modifications.</p> <p>Une fois le fichier modifié dans le volet <strong>Modifier</strong>, les outils suivants sont disponibles dans la barre d’outils : <br /> </p> - <strong>Afficher dans l’arborescence :</strong> affiche le fichier dans l’arborescence du référentiel.<br />- <strong>Recherche/Remplacement ...</strong> : recherche ou remplacement.<br /><br />Double-cliquez sur la ligne d’état du volet <strong>Modifier</strong> pour ouvrir la boîte de dialogue <strong>Aller à la ligne</strong> et entrer un numéro de ligne spécifique à laquelle accéder.<br /> </td>
  </tr>
  <tr>
   <td>Onglet Propriétés<br /> </td>
   <td>Affiche les propriétés du nœud que vous avez sélectionné. Vous pouvez ajouter de nouvelles propriétés ou supprimer celles qui existent déjà.<br /> </td>
  </tr>
  <tr>
   <td>Onglet Contrôle d’accès</td>
   <td><p>Afficher les autorisations en fonction du chemin actuel, du niveau du référentiel ou du chemin principal.</p> <p>Les autorisations sont décomposées en</p> <p>- <strong>Politiques de contrôle d’accès applicables</strong> : politiques qui peuvent être appliquées à la sélection en cours.</p> <p>- <strong>Stratégies de contrôle d’accès local</strong> : stratégies actuelles appliquées localement à la sélection en cours.</p> <p>- <strong>Stratégies de contrôle d’accès en vigueur</strong> : les stratégies actuelles appliquées à la sélection en cours peuvent être définies localement ou héritées des nœuds parents.</p> <p>Remarque. Pour pouvoir voir les informations de contrôle d’accès, l’utilisateur connecté à CRXDE Lite doit avoir le droit de lire les entrées ACL. Par défaut, l’utilisateur anonyme ne peut pas voir cette information - veuillez vous connecter sous admin par ex., pour voir les informations.</p> </td>
  </tr>
  <tr>
   <td>Onglet Réplication</td>
   <td><p>Affiche l’état de la réplication du nœud actif. Vous pouvez répliquer et supprimer la réplication du nœud actif.</p> </td>
  </tr>
  <tr>
   <td>Onglet Console<br /> </td>
   <td><p><strong>Journaux de serveur</strong> :</p> <p>Affiche les messages de journaux. Vous pouvez configurer le niveau de journalisation, effacer la console, épingler à la position de défilement sélectionnée et activer/désactiver l’affichage des messages.<br /> </p> <p><strong>Gestion de version</strong> :</p> <p>Affiche les messages de gestion des versions.<br /> </p> </td>
  </tr>
  <tr>
   <td>Onglet Infos sur le build<br /> </td>
   <td>Affiche des informations lors de la création d’un bundle.<br /> </td>
  </tr>
  <tr>
   <td>Actualiser<br /> </td>
   <td>Actualise la sélection actuelle. Les modifications des autres utilisateurs sont mises à jour dans votre vue du référentiel. Les modifications que vous avez apportées ne sont pas concernées.<br /> </td>
  </tr>
  <tr>
   <td>Enregistrer tout</td>
   <td><p><strong>Enregistrer tout</strong> : <br /> </p> <p>Enregistre tous les changements que vous avez apportés. Tant que vous ne cliquez pas sur Enregistrer, les modifications sont temporaires. Elles seront perdues lorsque vous quitterez la console.</p> <p><strong>Rétablir</strong> :</p> <p>Ignore toutes les modifications que vous avez apportées au nœud sélectionné depuis le dernier enregistrement, puis recharge l’état actuel du référentiel pour le nœud sélectionné.</p> <p><strong>Tout rétablir</strong> :</p> <p>Ignore toutes les modifications que vous avez apportées au référentiel entier depuis le dernier enregistrement, puis recharge l’état actuel du référentiel.</p> </td>
  </tr>
  <tr>
   <td>Créer ...<br /> </td>
   <td><p>Menu déroulant permettant de créer les éléments suivants sous le nœud sélectionné :<br /> </p> <p>- <strong>Nœud</strong> : nœud avec un type de nœud arbitraire<br /> </p> <p>- <strong>Fichier</strong> : nœud nt:file et son sous-nœud nt:resource</p> <p>- <strong>Dossier</strong> : nœud nt:folder</p> <p>- <strong>Modèle</strong> : modèle AEM</p> <p>- <strong>Composant</strong> : composant AEM</p> <p>- <strong>Boîte de dialogue</strong> : boîte de dialogue AEM</p> </td>
  </tr>
  <tr>
   <td>Supprimer<br /> </td>
   <td>Supprime le nœud sélectionné.<br /> </td>
  </tr>
  <tr>
   <td>Copier</td>
   <td>Copie le nœud sélectionné.<br /> </td>
  </tr>
  <tr>
   <td>Coller<br /> </td>
   <td>Colle le nœud copié sous le nœud sélectionné.<br /> </td>
  </tr>
  <tr>
   <td>Déplacer ...<br /> </td>
   <td>Déplace le nœud sélectionné vers le nœud défini dans la boîte de dialogue.</td>
  </tr>
  <tr>
   <td>Renommer ...<br /> </td>
   <td>Renomme le nœud sélectionné.<br /> </td>
  </tr>
  <tr>
   <td>Mixins ...<br /> </td>
   <td>Permet d’ajouter des types mixin au type de nœud. Les types mixin sont principalement utilisés pour ajouter des fonctionnalités avancées telles que la gestion des versions, le contrôle d’accès, le référencement et le verrouillage du nœud.</td>
  </tr>
  <tr>
   <td>Outils<br /> </td>
   <td><p>Menu déroulant avec les outils suivants :</p> <p>- <strong>Config serveur ...</strong> : pour accéder à la console Felix.</p> <p>- <strong>Requête ...</strong> : pour interroger le référentiel.</p> <p>- <strong>Privilèges ...</strong> : pour ouvrir la gestion des privilèges, laquelle permet d’afficher et d’ajouter des privilèges.</p> <p>- <strong>Test du contrôle d’accès ...</strong> : emplacement où vous pouvez tester l’autorisation pour certains chemins et/ou le chemin principal.</p> <p>- <strong>Exporter le type de nœud</strong> : pour exporter les types de nœud dans le système en tant que notation cnd.</p> <p>- <strong>Importer le type de nœud ...</strong> : pour importer les types de nœud en utilisant la notation cnd.</p> <p>- <strong>Installer le débogueur SiteCatalyst ...</strong> : instructions sur l’installation de Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de connexion<br /> </td>
   <td><p>Affiche les utilisateurs actuellement connectés et l’espace de travail auquel ils sont connectés, par exemple, admin@crx.default.</p> <p>Cliquez dessus pour vous connecter ou vous reconnecter en tant qu’utilisateur spécifique. Si vous ne spécifiez pas d’espace de travail auquel vous connecter, vous serez connecté à l’espace de travail par défaut, crx.default.</p> <p>Si vous souhaitez parcourir le référentiel en tant qu’utilisateur anonyme, utilisez <strong>anonymous</strong> comme nom de connexion et n’importe quel mot de passe (par exemple, un espace ou un point).<br /> </p> <p>Si votre autorisation n’est plus valide (par exemple, elle a expiré), le widget de connexion affiche « <strong>Connexion - Non autorisée ...</strong> ». Cliquez dessus pour vous reconnecter.</p> </td>
  </tr>
 </tbody>
</table>

## Création d’un dossier {#creating-a-folder}

Pour créer un dossier avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le dossier sous lequel vous souhaitez créer le nouveau dossier, sélectionnez **Créer...**, puis **Créer un dossier...**.

1. Entrez le **nom** du dossier et cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

## Création d’un modèle {#creating-a-template}

Pour créer un modèle avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le dossier dans lequel vous souhaitez créer le modèle, sélectionnez **Créer ...**, puis **Créer un modèle ...**.

1. Définissez les champs **Libellé**, **Titre**, **Description**, **Type de ressource** et **Classement** du modèle. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez **Chemins autorisés**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez les **Parents autorisés**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez les **Enfants autorisés**. Cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Cela crée :

* un nœud de type `cq:Template` avec les propriétés du modèle ;

* un nœud enfant de type `cq:PageContent` avec les propriétés de contenu de page.

Vous pouvez ajouter des propriétés à votre modèle : reportez-vous à la section [Création d’une propriété](#creating-a-property).

## Création d’un composant {#creating-a-component}

La fonctionnalité décrite ici n’est disponible que si CQ5 est installé, c’est-à-dire si le type de nœud `cq:Component` est disponible dans le référentiel.

Pour créer un composant avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le dossier dans lequel vous souhaitez créer le composant, sélectionnez **Créer ...**, puis **Créer un composant ...**.

1. Définissez les champs **Libellé**, **Titre**, **Description**, **Super type ressource** et **Groupe** du modèle. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez les propriétés du composant **Est conteneur**, **Pas de décoration**, **Nom de cellule** et **Chemin de la boîte de dialogue**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez la propriété de composant **Parents autorisés**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez la propriété de composant **Enfant autorisé**. Cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Cela crée :

* un nœud de type `cq:Component`.
* Les propriétés du composant
* Un script .jsp de composant

## Création d’une boîte de dialogue {#creating-a-dialog}

Pour créer une boîte de dialogue avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le composant dans lequel vous souhaitez créer la boîte de dialogue, sélectionnez **Créer ...**, puis **Créer une boîte de dialogue ...**.

1. Entrez le **Libellé** et le **Titre**. Cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Il crée une boîte de dialogue avec la structure suivante :

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Vous pouvez désormais adapter la boîte de dialogue à vos besoins en modifiant les propriétés ou en ajoutant de nouveaux nœuds.

Vous pouvez également utiliser l’éditeur de boîte dialogue pour modifier une boîte de dialogue. Un double-clic sur le nœud dialog dans CRXDE Lite fait apparaître l’éditeur. Plus d’informations sur l’éditeur de boîte de dialogue sont disponibles [ici](/help/sites-developing/dialog-editor.md).

## Création d’un nœud {#creating-a-node}

Pour créer un nœud avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le nœud où vous souhaitez créer le nouveau nœud, sélectionnez **Créer ...**, puis **Créer un nœud ...**.
1. Entrez le **Nom** et le **Type**. Cliquez sur **OK**.
1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Vous pouvez désormais adapter le nœud à vos besoins en modifiant les propriétés ou en ajoutant de nouveaux nœuds.

>[!NOTE]
>
>La plupart des opérations de modification, y compris Créer un nœud, conserve toutes les modifications en mémoire et les stocke dans le référentiel lors de l’enregistrement uniquement (avec le bouton Enregistrer tout). Cependant, certaines opérations telles que le déplacement sont automatiquement conservées.
>
>La validation du nœud nouvellement créé qui est ou non autorisé par le type de nœud du nœud parent est également effectuée par le référentiel JCR en premier, lors de l’enregistrement des modifications. Si vous recevez un message d’erreur lors de l’enregistrement d’un nœud, vérifiez si la structure du contenu est valide (par exemple, vous ne pouvez pas créer un nœud `nt:unstructured` en tant qu’enfant du nœud `nt:folder`).

## Création d’une propriété {#creating-a-property}

Pour créer une propriété avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, sélectionnez le nœud dans lequel vous souhaitez ajouter la nouvelle propriété.
1. Dans l’onglet **Propriétés** du volet inférieur, entrez le **Nom**, le **Type** et la **Valeur**. Cliquez sur **Ajouter**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

## Création d’un script {#creating-a-script}

Pour créer un script :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le composant dans lequel vous souhaitez créer le script, sélectionnez **Créer ...**, puis **Créer un fichier ...**.

1. Entrez le **nom** du fichier, y compris son extension. Cliquez sur **OK**.

1. Le nouveau fichier s’ouvre en tant qu’onglet dans le volet de modification.
1. Modifiez le fichier.
1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications.

## Exportation et importation de types de nœuds {#exporting-and-importing-node-types}

[Avec CRXDE Lite, vous pouvez importer et exporter des définitions de type de nœud dans la notation CND (Compact Namespace et Node Type Definition).](https://jackrabbit.apache.org/jcr/node-type-notation.html)

Pour exporter une définition de type de nœud :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Sélectionnez le nœud en question.
1. Sélectionnez **Outils**, puis **Exporter le type de nœud**.

1. La définition, en notation cnd, est affichée dans votre navigateur. Enregistrez les informations si nécessaire.

Pour importer une définition de type de nœud :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Sélectionnez **Outils**, puis **Importer le type de nœud...**.

1. Entrez la notation CND pour la définition dans la zone de texte.
1. Cochez **Autoriser la mise à jour** si vous mettez à jour une définition existante.
1. Cliquez sur **Importer**.

## Journalisation {#logging}

CRXDE Lite permet d’afficher le fichier `error.log` qui se trouve sur le système de fichiers sous `<crx-install-dir>/crx-quickstart/server/logs` et de filtrer selon le niveau de journalisation approprié. Procédez comme suit :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans l’onglet **Console** en bas de la fenêtre, dans le menu déroulant à droite, sélectionnez **Journaux de serveur**.

1. Cliquez sur l’icône **Stop** pour afficher les messages.

Vous pouvez :

* Ajuster les paramètres du journal dans la console Felix en cliquant sur l’icône **Configurations de journalisation**.
* Effacer les messages en cliquant sur l’icône **Pinceau**.
* Épingler le message à la sélection en cours en cliquant sur l’icône **Épingler**.
* Activer ou désactiver l’affichage des messages en cliquant sur l’icône **Stop**.

## Contrôle d’accès {#access-control}

>[!NOTE]
>
>Consultez [Administration des utilisateurs, groupes et droits d’accès](/help/sites-administering/user-group-ac-admin.md) pour plus d’informations.
