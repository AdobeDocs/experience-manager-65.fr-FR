---
title: Développement dans CRXDE Lite
description: CRXDE Lite est incorporé dans Adobe Experience Manager (AEM) et permet d’effectuer des tâches de développement standard dans le navigateur.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 100%

---

# Développement dans CRXDE Lite{#developing-with-crxde-lite}

Cette section décrit comment développer votre application Adobe Experience Manager (AEM) à l’aide de CRXDE Lite.

Pour plus d’informations sur les différents environnements de développement disponibles, reportez-vous à la documentation sur la vue d’ensemble.

CRXDE Lite est intégré à CRX/CQ et permet d’effectuer des tâches de développement standard dans le navigateur. En vous connectant à CRXDE Lite, vous pouvez créer un projet, créer et modifier des fichiers (en .jsp et .java, par exemple), des dossiers, des modèles, des composants, des boîtes de dialogue, des nœuds, des propriétés et des bundles.
CRXDE Lite est recommandé lorsque vous ne disposez pas d’accès direct au serveur AEM, lorsque vous développez une application en étendant ou en modifiant les composants prêts à l’emploi et les bundles Java™ ou lorsque vous n’avez pas besoin d’un débogueur dédié, du remplissage de code et de la mise en surbrillance de la syntaxe.

>[!NOTE]
>
>À partir de la version 6.5.5.0 d’AEM, l’accès anonyme de CRXDE Lite n’est plus possible.
>Les utilisateurs sont redirigés vers l’écran de connexion.


>[!NOTE]
>
>Adobe recommande d’utiliser les [outils de développement pour Eclipse d’AEM](/help/sites-developing/aem-eclipse.md) et l’[extension AEM HTL Brackets](/help/sites-developing/aem-brackets.md) pendant le développement du projet.

## Prise en main de CRXDE Lite {#getting-started-with-crxde-lite}

Pour commencer à utiliser CRXDE Lite, procédez comme suit :

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
   <td>Permet de basculer rapidement entre CRXDE Lite, le gestionnaire de modules et le partage de modules.</td>
  </tr>
  <tr>
   <td>Widget de chemin de nœud</td>
   <td><p>Affiche le chemin d’accès au nœud sélectionné.</p> <p>Vous pouvez également l’utiliser pour sauter vers un nœud en entrant le chemin à la main ou en le collant à partir d’un autre endroit et en appuyant sur Entrée.</p> <p>Il permet aussi de rechercher des nœuds par nom de nœud. Entrez le nom du nœud que vous souhaitez rechercher et patientez (ou appuyez sur le symbole de recherche sur le côté droit). Entrez par exemple la chaîne <em>oak</em> dans le widget pour voir comment la recherche fonctionne. Si un ou plusieurs nœuds sont chargés dans le volet de l’explorateur, la liste s’affiche. Vous pouvez sélectionner le chemin et appuyer sur Entrée pour y accéder. La recherche ne fonctionne que pour les nœuds chargés dans l’application cliente CRXDE dans le navigateur. Pour effectuer une recherche dans tout le référentiel, utilisez Outils puis Requête.</p> </td>
  </tr>
  <tr>
   <td>Volet de l’explorateur</td>
   <td><p>Affiche une arborescence de tous les nœuds du référentiel.</p> <p>Cliquez sur un nœud pour afficher ses propriétés dans l’onglet <strong>Propriétés</strong>. Après avoir cliqué sur un nœud, vous pouvez sélectionner une action dans la barre d’outils. Cliquez de nouveau sur le nœud pour le renommer.</p> <p>Filtre de navigation dans l’arborescence (icône en forme de paire de jumelles) : vous permet de filtrer les nœuds du référentiel pour lesquels le nom contient le texte saisi. S’applique uniquement aux nœuds qui ont été chargés localement.<br /> </p> </td>
  </tr>
  <tr>
   <td>Volet de modification</td>
   <td><p>Onglet <strong>Accueil</strong> : vous permet de rechercher du contenu et/ou de la documentation et d’accéder aux ressources des développeurs et développeuses (documentation, blog de développement, base de connaissances) et à l’assistance (page d’accueil et centre d’assistance d’Adobe).<br /> </p> <p>Double-cliquez sur un fichier dans le volet <strong>Explorateur</strong> pour afficher son contenu. Par exemple, un fichier .jsp ou .java. Vous pouvez ensuite le modifier et enregistrer les modifications.</p> <p>Une fois le fichier modifié dans le volet de <strong>modification</strong>, les outils suivants sont disponibles dans la barre d’outils :<br /> </p> - <strong>Afficher dans l’arborescence :</strong> affiche le fichier dans l’arborescence du référentiel.<br /> - <strong>Rechercher/Remplacer...</strong> : permet d’effectuer une recherche ou un remplacement.<br /> <br /> Double-cliquez sur la ligne de statut du volet <strong>Modifier</strong> pour ouvrir la boîte de dialogue <strong>Aller à la ligne</strong> et entrer un numéro de ligne spécifique.<br /> </td>
  </tr>
  <tr>
   <td>Onglet Propriétés<br /> </td>
   <td>Affiche les propriétés du nœud que vous avez sélectionné. Vous pouvez ajouter de nouvelles propriétés ou supprimer celles qui existent déjà.<br /> </td>
  </tr>
  <tr>
   <td>Onglet Contrôle d’accès</td>
   <td><p>Affiche les autorisations en fonction du chemin d’accès, du niveau du référentiel ou du principal.</p> <p>Les autorisations sont classées comme suit.</p> <p>- <strong>Politiques de contrôle d’accès applicables</strong> : les politiques qui peuvent être appliquées à la sélection.</p> <p>- <strong>Politiques de contrôle d’accès locales</strong> : les politiques appliquées localement à la sélection.</p> <p>- <strong>Politiques de contrôle d’accès en vigueur</strong> : les politiques appliquées à la sélection, qui peuvent être définies localement ou héritées des nœuds parents.</p> <p>Remarque. Pour pouvoir voir les informations de contrôle d’accès, l’utilisateur ou l’utilisatrice connecté à CRXDE Lite doit avoir le droit de lire les entrées ACL. Par défaut, l’utilisateur ou utilisatrice anonyme ne peut pas afficher ces informations : connectez-vous en tant qu’administrateur ou administratrice pour voir les informations, par exemple.</p> </td>
  </tr>
  <tr>
   <td>Onglet Réplication</td>
   <td><p>Affiche le statut de la réplication du nœud. Vous pouvez répliquer et supprimer la réplication du nœud.</p> </td>
  </tr>
  <tr>
   <td>Onglet Console<br /> </td>
   <td><p><strong>Journaux de serveur</strong> :</p> <p>Affiche les messages de journaux. Vous pouvez configurer le niveau de journalisation, effacer la console, épingler à la position de défilement sélectionnée et activer/désactiver l’affichage des messages.<br /> </p> <p><strong>Gestion de version</strong> :</p> <p>Affiche les messages de gestion de versions.<br /> </p> </td>
  </tr>
  <tr>
   <td>Onglet Infos sur le build<br /> </td>
   <td>Affiche des informations lorsqu’un lot est en cours de création.<br /> </td>
  </tr>
  <tr>
   <td>Actualiser<br /> </td>
   <td>Actualise la sélection. Les modifications des autres utilisateurs et utilisatrices sont mises à jour dans votre vue du référentiel. Les modifications que vous avez apportées ne sont pas concernées.<br /> </td>
  </tr>
  <tr>
   <td>Enregistrer tout</td>
   <td><p><strong>Enregistrer tout</strong> :<br /> </p> <p>Enregistre toutes les modifications que vous avez apportées. Les modifications non enregistrées sont temporaires jusqu’à ce que vous cliquiez sur Enregistrer. Elles seront perdues si vous quittez la console.</p> <p><strong>Rétablir</strong> :</p> <p>Ignore toutes les modifications que vous avez apportées au nœud sélectionné depuis le dernier enregistrement, puis recharge l’état actuel du référentiel pour le nœud sélectionné.</p> <p><strong>Rétablir tout</strong> :</p> <p>Ignore toutes les modifications que vous avez apportées à l’ensemble du référentiel depuis le dernier enregistrement, puis recharge l’état actuel du référentiel.</p> </td>
  </tr>
  <tr>
   <td>Créer ...<br /> </td>
   <td><p>Menu déroulant permettant de créer les éléments suivants sous le noeud sélectionné :<br /> </p> <p>- <strong>Nœud</strong> : un nœud de type arbitraire<br /> </p> <p>- <strong>Fichier</strong> : nœud nt:file et son sous-nœud nt:resource</p> <p>- <strong>Dossier</strong> : nœud nt:folder</p> <p>- <strong>Modèle</strong> : modèle AEM</p> <p>- <strong>Composant</strong> : composant AEM</p> <p>- <strong>Boîte de dialogue</strong> : boîte de dialogue AEM</p> </td>
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
   <td>Permet d’ajouter des types mixin au type de nœud. Les types mixin sont principalement utilisés pour ajouter des fonctionnalités avancées telles que le contrôle de version, le contrôle d’accès, le référencement et le verrouillage au nœud.</td>
  </tr>
  <tr>
   <td>Outils<br /> </td>
   <td><p>Menu déroulant avec les outils suivants :</p> <p>- <strong>Configuration du serveur</strong> : pour accéder à la console Felix.</p> <p>- <strong>Requête</strong> : pour interroger le référentiel.</p> <p>- <strong>Privilèges</strong> : pour ouvrir la gestion des privilèges, où vous pouvez afficher et ajouter des privilèges.</p> <p>- <strong>Tester le contrôle d’accès</strong> : emplacement où vous pouvez tester l’autorisation pour un certain chemin d’accès et/ou un principal.</p> <p>- <strong>Exporter le type de nœud</strong> : pour exporter les types de nœud dans le système en tant que notation CND.</p> <p>- <strong>Importer le type de nœud</strong> : pour importer les types de nœud en utilisant la notation CND.</p> <p>- <strong>Installer SiteCatalyst Debugger</strong> : instructions pour l’installation d’Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de connexion<br /> </td>
   <td><p>Affiche les utilisateurs et utilisatrices connectés ainsi que l’espace de travail dans lequel ils et elles sont connectés, par exemple, admin@crx.default.</p> <p>Cliquez dessus pour vous connecter ou vous reconnecter en tant qu’utilisateur ou utilisatrice spécifique. Si vous ne spécifiez pas d’espace de travail auquel vous connecter, la connexion est établie sur l’espace de travail par défaut crx.default.</p> <p>Si vous souhaitez parcourir le référentiel en tant qu’utilisateur ou utilisatrice anonyme, utilisez <strong>anonymous</strong> comme identifiant de connexion et n’importe quel mot de passe (par exemple, une espace ou un point).<br /> </p> <p>Si votre autorisation n’est plus valide (par exemple, si elle a expiré), le widget de connexion affiche « <strong>Connexion non autorisée</strong> ». Cliquez dessus pour vous reconnecter.</p> </td>
  </tr>
 </tbody>
</table>

## Création d’un dossier {#creating-a-folder}

Pour créer un dossier avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le dossier dans lequel vous souhaitez créer le nouveau dossier, sélectionnez **Créer**, puis **Créer un dossier**.

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

Les éléments suivants sont alors créés :

* un nœud de type `cq:Template` avec les propriétés du modèle ;

* un nœud enfant de type `cq:PageContent` avec les propriétés de contenu de page.

Vous pouvez ajouter des propriétés à votre modèle. Pour plus d’informations, consultez la section [Création d’une propriété](#creating-a-property).

## Création d’un composant {#creating-a-component}

La fonctionnalité décrite ici n’est disponible que si CQ5 est installé, c’est-à-dire si le type de nœud `cq:Component` est disponible dans le référentiel.

Pour créer un composant avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le dossier dans lequel vous souhaitez créer le composant, sélectionnez **Créer ...**, puis **Créer un composant ...**.

1. Définissez les champs **Libellé**, **Titre**, **Description**, **Super type de ressource** et **Groupe** du composant. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez les propriétés du composant **Est un conteneur**, **Pas de décoration**, **Nom de cellule** et **Chemin d’accès de la boîte de dialogue**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez la propriété de composant **Parents autorisés**. Cliquez sur **Suivant**.

1. Cette étape est facultative : définissez la propriété de composant **Enfant autorisé**. Cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Les éléments suivants sont alors créés :

* un nœud de type `cq:Component`.
* Propriétés du composant
* Un script .jsp de composant

## Création d’une boîte de dialogue {#creating-a-dialog}

Pour créer une boîte de dialogue CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le composant dans lequel vous souhaitez créer la boîte de dialogue, sélectionnez **Créer ...**, puis **Créer une boîte de dialogue ...**.

1. Entrez le **Libellé** et le **Titre**. Cliquez sur **OK**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Une boîte de dialogue est alors créée sous la structure suivante :

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Vous pouvez désormais adapter la boîte de dialogue à vos besoins en modifiant les propriétés ou en créant des nœuds.

Vous pouvez également utiliser l’éditeur de boîte dialogue pour modifier une boîte de dialogue. Un double-clic sur le nœud de la boîte de dialogue dans CRXDE Lite fait apparaître l’éditeur. [Vous trouverez ici](/help/sites-developing/dialog-editor.md) plus d’informations sur l’éditeur de boîte de dialogue.

## Création d’un nœud {#creating-a-node}

Pour créer un nœud avec CRXDE Lite, procédez comme suit :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, cliquez avec le bouton droit sur le nœud où vous souhaitez créer le nœud, sélectionnez **Créer**, puis **Créer un nœud**.
1. Entrez le **Nom** et le **Type**. Cliquez sur **OK**.
1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

Vous pouvez désormais adapter le nœud à vos besoins en modifiant les propriétés ou en créant des nœuds.

>[!NOTE]
>
>La plupart des opérations de modification, y compris la création d’un nœud, conserve toutes les modifications en mémoire et les stocke dans le référentiel au moment de l’enregistrement uniquement (avec le bouton Enregistrer tout). Cependant, certaines opérations telles que le déplacement sont automatiquement conservées.
>
>La validation de l’autorisation du nouveau nœud par le type de nœud du nœud parent est également effectuée par le référentiel JCR lors de l’enregistrement des modifications. Si vous recevez un message d’erreur lors de l’enregistrement d’un nœud, vérifiez si la structure du contenu est valide (par exemple, vous ne pouvez pas créer un nœud `nt:unstructured` en tant qu’enfant du nœud `nt:folder`).

## Création d’une propriété {#creating-a-property}

Pour créer une propriété avec CRXDE Lite :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet de navigation, sélectionnez le nœud dans lequel vous souhaitez ajouter la nouvelle propriété.
1. Dans l’onglet **Propriétés** du volet inférieur, saisissez le **Nom**, le **Type** et la **Valeur**. Cliquez sur **Ajouter**.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

## Créer un script {#creating-a-script}

Pour créer un script :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Dans le volet Explorateur, cliquez avec le bouton droit sur le composant dans lequel vous souhaitez créer le fichier, sélectionnez **Créer**, puis **Créer un fichier ...**.

1. Entrez le **nom** du fichier, y compris son extension. Cliquez sur **OK**.

1. Le nouveau fichier s’ouvre en tant qu’onglet dans le volet de modification.
1. Modifiez le fichier.
1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications.

## Exportation et importation de types de nœuds {#exporting-and-importing-node-types}

Avec CRXDE Lite, vous pouvez importer et/ou exporter des définitions de type de nœud dans la [notation CND (Compact Namespace et Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Pour exporter une définition de type de nœud :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Sélectionnez le nœud requis.
1. Sélectionnez **Outils**, puis **Exporter le type de nœud**.

1. La définition, en notation CND, est affichée dans votre navigateur. Enregistrez les informations si nécessaire.

Pour importer une définition de type de nœud :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Sélectionnez **Outils**, puis **Importer le type de nœud...**.

1. Saisissez la notation CND de la définition dans la zone de texte.
1. Cochez la case **Autoriser la mise à jour** si vous mettez à jour une définition existante.
1. Cliquez sur **Importer**.

## Journalisation {#logging}

CRXDE Lite permet d’afficher le fichier `error.log` qui se trouve sur le système de fichiers à l’emplacement `<crx-install-dir>/crx-quickstart/server/logs` et de le filtrer avec le niveau de journalisation approprié. Procédez comme suit :

1. Ouvrez CRXDE Lite dans un navigateur.
1. Sous l’onglet **Console**, en bas de la fenêtre, dans le menu déroulant à droite, sélectionnez **Journaux du serveur**.

1. Cliquez sur l’icône **Arrêter** pour afficher les messages.

Vous pouvez effectuer les actions suivantes :

* Ajuster les paramètres du journal dans la console Felix en cliquant sur l’icône **Configurations de journalisation**.
* Effacez les messages en cliquant sur l’icône **Pinceau**.
* Épinglez le message à la sélection en cliquant sur l’icône **Épingler**.
* Activer ou désactiver l’affichage des messages en cliquant sur l’icône **Stop**.

## Contrôle d’accès {#access-control}

>[!NOTE]
>
>Consultez [Administration des utilisateurs, des utilisatrices, des groupes et des droits d’accès](/help/sites-administering/user-group-ac-admin.md) pour plus d’informations.
