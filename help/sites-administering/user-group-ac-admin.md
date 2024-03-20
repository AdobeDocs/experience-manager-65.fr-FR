---
title: Administration des utilisateurs, des utilisatrices, des groupes et des droits d’accès
description: Découvrez l’administration des utilisateurs, des utilisatrices, des groupes et des droits d’accès dans Adobe Experience Manager.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 5808b8f9-9b37-4970-b5c1-4d33404d3a8b
feature: Security
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3073'
ht-degree: 100%

---

# Administration des utilisateurs, des utilisatrices, des groupes et des droits d’accès{#user-group-and-access-rights-administration}

Plusieurs thèmes sont associés à l’activation de l’accès à un référentiel CRX :

* [Droits d’accès](#how-access-rights-are-evaluated) : concepts se rapportant à leur définition et à leur évaluation
* [Administration des utilisateurs et utilisatrices](#user-administration) : gestion des comptes individuels utilisés pour l’accès
* [Administration des groupes](#group-administration) : simplifiez la gestion des utilisateurs en formant des groupes
* [Gestion des droits d’accès](#access-right-management) : définition des politiques qui contrôlent comment ces utilisateurs et ces groupes peuvent accéder à des ressources

Les éléments de base sont les suivants :

**Comptes utilisateur** : CRX authentifie l’accès en identifiant et en vérifiant un utilisateur ou une utilisatrice (par l’intermédiaire de cette personne ou d’une autre application) en fonction des détails contenus dans le compte utilisateur.

Dans CRX, chaque compte utilisateur est un nœud dans l’espace de travail. Un compte d’utilisateur CRX possède les propriétés suivantes :

* Il représente un utilisateur ou une utilisatrice de CRX.
* Il contient un nom d’utilisateur et un mot de passe.
* Il s’applique à cet espace de travail.
* Il ne peut pas avoir de sous-utilisateurs ou sous-utilisatrices. Pour les droits d’accès hiérarchiques, vous devez utiliser les groupes.

* Vous pouvez spécifier des droits d’accès pour le compte utilisateur.

  Toutefois, pour simplifier la gestion, Adobe recommande (dans la plupart des cas) d’attribuer des droits d’accès aux comptes de groupe. L’affectation de droits d’accès à chaque personne devient rapidement difficile à gérer (à l’exception de certains utilisateurs ou utilisatrices système lorsqu’il n’y a qu’une ou deux instances).

**Comptes de groupe** : les comptes de groupe sont des ensembles d’utilisateurs et utilisatrices et/ou d’autres groupes. Ils sont utilisés pour simplifier la gestion, car toute modification des droits d’accès affectés à un groupe est appliquée automatiquement à tous les utilisateurs de ce groupe. Un utilisateur ou une utilisatrice n’a pas l’obligation d’appartenir à un groupe, mais il ou elle appartient souvent à plusieurs groupes.

Dans CRX, un groupe possède les propriétés suivantes :

* Il représente un groupe d’utilisateurs avec des droits d’accès communs. Par exemple, les auteurs et autrices, ou les développeurs et développeuses.
* Il s’applique à cet espace de travail.
* Il peut contenir des membres, qui peuvent être des utilisateurs ou utilisatrices individuel(le)s ou d’autres groupes.
* Il est possible de hiérarchiser les groupes grâce aux relations des membres. Vous ne pouvez pas placer un groupe directement sous un autre groupe dans le référentiel.
* Vous pouvez définir les droits d’accès pour les membres du groupe.

**Droits d’accès** : CRX utilise des droits d’accès pour contrôler l’accès à des zones spécifiques du référentiel.

Cette opération est effectuée en affectant des autorisations pour autoriser ou refuser l’accès à une ressource (nœud ou chemin d’accès) dans le référentiel. Lorsque différentes autorisations peuvent être affectées, les droits d’accès doivent être évalués afin de déterminer la combinaison qui s’applique à la demande actuelle.

CRX permet de configurer les droits d’accès pour des comptes utilisateur et des comptes de groupe. Les mêmes principes de base d’évaluation sont alors appliqués aux deux.

## Évaluation des droits d’accès {#how-access-rights-are-evaluated}

>[!NOTE]
>
>CRX implémente le [contrôle d’accès tel que défini par JSR-283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>L’installation standard du référentiel CRX est configurée de manière à utiliser des listes de contrôle d’accès dépendant des ressources. Il s’agit d’une implémentation possible du contrôle d’accès JSR-283 et de l’une des implémentations présentes avec Jackrabbit.

### Sujets et entités {#subjects-and-principals}

CRX utilise deux concepts clés lors de l’évaluation des droits d’accès :

* Un **principal de sécurité** est une entité qui transfère des droits d’accès. Les entités incluent :

   * Un compte d’utilisateur
   * Un compte de groupe

     Si un compte utilisateur appartient à un ou à plusieurs groupes, il est également associé à chacun de ces principaux du groupe.

* Un **objet** est utilisé pour représenter la source de la demande.

   Il est utilisé pour centraliser les droits d’accès applicables pour cette demande. Ceux-ci proviennent de :

   * le principal de sécurité de l’utilisateur ;

     Les droits affectés directement au compte d’utilisateur

   * tous les principaux de sécurité des groupes associés à cet utilisateur.

     Tous les droits sont affectés aux groupes auxquels appartient l’utilisateur ou l’utilisatrice.

  Le résultat est ensuite utilisé pour autoriser ou refuser l’accès à la ressource demandée.

#### Compilation de la liste des droits d’accès pour un sujet {#compiling-the-list-of-access-rights-for-a-subject}

Dans CRX, le sujet dépend de :

* l’utilisateur ou utilisatrice principal(e) ;
* toutes les entités de groupe associées à cet utilisateur ou utilisatrice.

La liste des droits d’accès applicables au sujet est établie à partir :

* des droits affectés directement au compte d’utilisateur ;
* et de tous les droits affectés aux groupes auxquels appartient l’utilisateur.

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* CRX ne prend en compte aucune hiérarchie d’utilisateurs ou utilisatrices lors de la compilation de la liste.
>* CRX n’utilise une hiérarchie des groupes que lorsque vous incluez un groupe comme membre d’un autre groupe. Il n’existe pas d’héritage automatique des autorisations de groupe.
>* L’ordre dans lequel vous définissez les groupes n’a aucune incidence sur les droits d’accès.
>

### Résolution des demandes et des droits d’accès {#resolving-request-and-access-rights}

Lorsque CRX gère la demande, il compare la demande d’accès du sujet à la liste de contrôle d’accès sur le nœud du référentiel :

Ainsi, si Linda demande de mettre à jour le nœud `/features` dans la structure de référentiel suivante :

![chlimage_1-57](assets/chlimage_1-57.png)

### Ordre de priorité {#order-of-precedence}

Les droits d’accès dans CRX sont évalués comme suit :

* Les entités d’utilisateur ou d’utilisatrice ont toujours la priorité sur les entités de groupe, indépendamment de :

   * leur ordre dans la liste de contrôle d’accès ;
   * leur position dans la hiérarchie des nœuds.

* Pour un principal donné, il existe (au plus) 1 entrée de refus et 1 entrée d’autorisation sur un nœud donné. La mise en œuvre efface toujours les entrées redondantes et s’assure que les mêmes autorisations ne figurent pas à la fois dans les entrées d’autorisation et de refus.

>[!NOTE]
>
>Ce processus d’évaluation est adapté au contrôle d’accès dépendant des ressources d’une installation CRX standard.

En prenant deux exemples dans lesquels l’utilisateur `aUser` est membre du `aGroup` :

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

Dans le cas ci-dessus :

* `aUser` ne dispose pas d’une autorisation en écriture sur `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

Dans ce cas :

* `aUser` ne dispose pas d’une autorisation en écriture sur `grandChildNode`.
* La deuxième entrée de contrôle d’accès pour `aUser` est redondante.

Les droits d’accès provenant de plusieurs entités de groupe sont évalués en fonction de leur ordre, à la fois dans la hiérarchie et dans une seule liste de contrôle d’accès.

### Bonnes pratiques {#best-practices}

Le tableau ci-dessous contient des recommandations et bonnes pratiques :

<table>
 <tbody>
  <tr>
   <td>Recommandation...</td>
   <td>Raison...</td>
  </tr>
  <tr>
   <td><i>Utilisez des groupes</i></td>
   <td><p>Évitez d’affecter des droits d’accès utilisateur par utilisateur. Il existe plusieurs raisons à cela :</p>
    <ul>
     <li>Comme il y a beaucoup plus d’utilisateurs que de groupes, les groupes simplifient la structure.</li>
     <li>Les groupes offrent une vue d’ensemble de tous les comptes.</li>
     <li>L’héritage est plus simple avec les groupes.</li>
     <li>Les utilisateurs vont et viennent. Les groupes sont créés à long terme.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>Soyez positif</i></td>
   <td><p>Utilisez toujours des instructions Autoriser pour spécifier les droits d’accès du principal du groupe (dans la mesure du possible). Évitez d’utiliser une instruction Refuser.</p> <p>Les principaux de groupe sont évalués dans l’ordre, dans la hiérarchie et dans la liste de contrôle d’accès unique.</p> </td>
  </tr>
  <tr>
   <td><i>Restez simple</i></td>
   <td><p>Il est important d’investir du temps et de réfléchir à la configuration d’une nouvelle installation.</p> <p>L’application d’une structure claire simplifie la gestion et l’administration au jour le jour, ce qui garantit que vos collègues actuels et leurs successeurs peuvent comprendre facilement ce qui est mis en œuvre.</p> </td>
  </tr>
  <tr>
   <td><i>Testez</i></td>
   <td>Utilisez une installation de test pour vous exercer et vous assurer que vous comprenez les relations entre les différents utilisateurs et groupes.</td>
  </tr>
  <tr>
   <td><i>Utilisateurs/groupes par défaut</i></td>
   <td>Mettez toujours à jour les utilisateurs et les groupes par défaut immédiatement après l’installation afin d’éviter tout problème de sécurité.</td>
  </tr>
 </tbody>
</table>

## Administration des utilisateurs {#user-administration}

Une boîte de dialogue standard est utilisée pour l’**administration des utilisateurs**.

Vous devez être connecté(e) à l’espace de travail approprié, puis vous pouvez accéder à la boîte de dialogue à partir :

* du lien **Administration des utilisateurs** sur la console principale de CRX ;
* du menu **Sécurité** de l’Explorateur CRX.

![chlimage_1-58](assets/chlimage_1-58.png)

**Propriétés**

* **UserID**

  Le nom abrégé du compte est utilisé lors de l’accès à CRX.

* **Principal Name**

  Nom entier du compte.

* **Password**

  Nécessaire lors de l’accès à CRX avec ce compte.

* **ntlmhash**

  Affecté automatiquement pour chaque nouveau compte et mis à jour lorsque le mot de passe est modifié.

* Vous pouvez ajouter de nouvelles propriétés en définissant un nom, un type et une valeur. Cliquez sur Enregistrer (symbole de coche verte) pour chaque nouvelle propriété.

**Appartenance à un groupe**

Tous les groupes auxquels appartient le compte s’affichent. La colonne Hérité indique l’appartenance héritée en raison de l’appartenance à un autre groupe.

Si vous cliquez sur un ID de groupe (le cas échéant), l’[Administration des groupes](#group-administration) s’affiche pour ce groupe.

**Emprunteurs d’identité**

La fonction Emprunter l’identité permet à un utilisateur ou une utilisatrice de travailler sous le nom d’un(e) autre.

Cela signifie qu’un compte d’utilisateur peut spécifier d’autres comptes (utilisateur, utilisatrice ou groupe) compatibles avec son compte. En d’autres termes, si la personne B est autorisée à emprunter l’identité de la personne A, la personne B peut agir à l’aide des détails du compte utilisateur (dont l’ID, le nom et les droits d’accès) de la personne A.

Cela permet aux comptes d’emprunteur d’identité d’effectuer des tâches comme s’ils utilisaient le compte qu’ils empruntaient. Par exemple, lors d’une absence ou pour partager une charge excessive à court terme.

Si un compte emprunte l’identité d’un autre compte, il est très difficile de s’en rendre compte. Les fichiers journaux ne contiennent pas d’informations sur le fait que l’emprunt de l’identité s’est produit lors des événements. Ainsi, si la personne B emprunte l’identité de la personne A, tous les événements peuvent sembler avoir été effectués personnellement par la personne A.

### Création d’un compte d’utilisateur {#creating-a-user-account}

1. Ouvrez la boîte de dialogue **Administration des utilisateurs**.
1. Cliquez sur **Créer un utilisateur**.
1. Vous pouvez ensuite saisir les Propriétés :

   * **UserID** utilisé comme nom de compte
   * **Password** nécessaire lors de la connexion
   * **Principal Name** pour fournir un nom textuel entier
   * **Intermediate Path** qui peut être utilisé pour former une arborescence

1. Cliquez sur Enregistrer (symbole de coche verte).
1. La boîte de dialogue est développée afin que vous puissiez :

   1. Configurez les **propriétés**.
   1. afficher l’**appartenance à un groupe** ;
   1. définir les **emprunteurs d’identité**.

>[!NOTE]
>
>Une perte de performances peut parfois être constatée lors de l’enregistrement de nouveaux utilisateurs ou de nouvelles utilisatrices dans des installations comportant un grand nombre :
>
>* d’utilisateurs ;
>* de groupes comportant de nombreux membres.
>

### Mise à jour d’un compte d’utilisateur {#updating-a-user-account}

1. Avec la boîte de dialogue **Administration des utilisateurs**, ouvrez la vue Liste de tous les comptes.
1. Parcourez la structure de l’arborescence.
1. Cliquez sur le compte requis pour l’ouvrir et le modifier.
1. Effectuez une modification, puis cliquez sur Enregistrer (symbole de coche verte) pour cette entrée.
1. Cliquez sur **Fermer** pour terminer, ou sur **Liste...** pour revenir à la liste de tous les comptes d’utilisateurs.

### Suppression d’un compte d’utilisateur {#removing-a-user-account}

1. Avec la boîte de dialogue **Administration des utilisateurs**, ouvrez la vue Liste de tous les comptes.
1. Parcourez la structure de l’arborescence.
1. Sélectionnez le compte requis et cliquez sur **Supprimer un utilisateur**. Le compte est immédiatement supprimé.

>[!NOTE]
>
>Cette action supprime le nœud de cette entité du référentiel.
>
>Les entrées de droit d’accès ne sont pas supprimées. Cela permet de s’assurer de l’intégrité de l’historique.

### Définition des propriétés {#defining-properties}

Vous pouvez définir des **propriétés** pour les comptes nouveaux ou existants :

1. Ouvrez la boîte de dialogue **Administration des utilisateurs** pour le compte approprié.
1. Définissez un nom de **Propriété**.
1. Sélectionnez le **type** dans la liste déroulante.
1. Définissez la **Valeur**.
1. Cliquez sur Enregistrer (symbole de coche verte) pour la nouvelle propriété.

Les propriétés existantes peuvent être supprimées avec le symbole de la corbeille.

À l’exception du mot de passe, les propriétés ne peuvent pas être modifiées. Elles doivent être supprimées et recréées.

#### Modification du mot de passe {#changing-the-password}

Le **mot de passe** est une propriété spéciale qui peut être modifiée en cliquant sur le lien **Modifier le mot de passe**.

Vous pouvez également modifier le mot de passe de votre propre compte d’utilisateur à partir du menu **Sécurité** dans l’Explorateur CRX.

### Définition d’un emprunteur d’identité {#defining-an-impersonator}

Vous pouvez définir des emprunteurs d’identité pour les comptes nouveaux ou existants :

1. Ouvrez la boîte de dialogue **Administration des utilisateurs** pour le compte approprié.
1. Indiquez le compte autorisé à emprunter l’identité de ce compte.

   Vous pouvez utiliser Parcourir... pour sélectionner un compte existant.

1. Cliquez sur Enregistrer (symbole de coche verte) pour la nouvelle propriété.

## Administration des groupes {#group-administration}

Une boîte de dialogue standard est utilisée pour l’**administration des groupes**.

Vous devez être connecté(e) à l’espace de travail approprié, puis vous pouvez accéder à la boîte de dialogue à partir :

* du lien **Administration des groupes** sur la console principale de CRX ;
* du menu **Sécurité** de l’Explorateur CRX.

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**Propriétés**

* **GroupID**

  Nom abrégé du compte de groupe.

* **Principal Name**

  Nom textuel entier pour le compte de groupe.

* Vous pouvez ajouter de nouvelles propriétés en définissant un nom, un type et une valeur. Cliquez sur Enregistrer (symbole de coche verte) pour chaque nouvelle propriété.

* **Members**

  Vous pouvez ajouter des utilisateurs, ou d’autres groupes, en tant que membres de ce groupe.

**Appartenance à un groupe**

Tous les groupes auxquels appartient le compte s’affichent. La colonne Hérité indique l’appartenance héritée en raison de l’appartenance à un autre groupe.

Cliquer sur un ID de groupe ouvre la boîte de dialogue correspondante.

**Membres**

Répertorie tous les comptes (utilisateurs, utilisatrices et/ou groupes) qui sont membres du groupe actuel.

La colonne **Hérité** indique l’appartenance héritée en raison de l’appartenance à un autre groupe.

>[!NOTE]
>
>Lorsque le rôle Propriétaire, Éditeur ou Observateur est attribué à un utilisateur sur n’importe quel dossier de ressources, un nouveau groupe est créé. Le nom du groupe utilise le format `mac-default-<foldername>` pour chaque dossier sur lequel les rôles sont définis.

### Création d’un compte de groupe {#creating-a-group-account}

1. Ouvrez la boîte de dialogue **Administration des groupes**.
1. Cliquez sur **Créer un groupe**.
1. Vous pouvez ensuite saisir les Propriétés :

   * **Principal Name** pour fournir un nom textuel entier
   * **Intermediate Path** qui peut être utilisé pour former une arborescence

1. Cliquez sur Enregistrer (symbole de coche verte).
1. La boîte de dialogue est développée afin que vous puissiez :

   1. Configurez les **propriétés**.
   1. afficher l’**appartenance à un groupe** ;
   1. Gérez les **membres**.

### Mise à jour d’un compte de groupe {#updating-a-group-account}

1. Avec la boîte de dialogue **Administration des groupes**, ouvrez la vue Liste de tous les comptes.
1. Parcourez la structure de l’arborescence.
1. Cliquez sur le compte requis pour l’ouvrir et le modifier.
1. Effectuez une modification, puis cliquez sur Enregistrer (symbole de coche verte) pour cette entrée.
1. Cliquez sur **Fermer** pour terminer, ou **Liste...** pour revenir à la liste de tous les comptes de groupe.

### Suppression d’un compte de groupe {#removing-a-group-account}

1. Avec la boîte de dialogue **Administration des groupes**, ouvrez la vue Liste de tous les comptes.
1. Parcourez la structure de l’arborescence.
1. Sélectionnez le compte requis et cliquez sur **Supprimer le groupe**. Le compte est immédiatement supprimé.

>[!NOTE]
>
>Cette action supprime le nœud de cette entité du référentiel.
>
>Les entrées de droit d’accès ne sont pas supprimées. Cela permet de s’assurer de l’intégrité de l’historique.

### Définition des propriétés {#defining-properties-1}

Vous pouvez définir des propriétés pour les comptes nouveaux ou existants :

1. Ouvrez la boîte de dialogue **Administration des groupes** pour le compte approprié.
1. Définissez un nom de **Propriété**.
1. Sélectionnez le **type** dans la liste déroulante.
1. Définissez la **valeur**.
1. Cliquez sur Enregistrer (symbole de coche verte) pour la nouvelle propriété.

Les propriétés existantes peuvent être supprimées avec le symbole de la corbeille.

### Membres {#members}

Vous pouvez ajouter des membres au groupe actuel :

1. Ouvrez la boîte de dialogue **Administration des groupes** pour le compte approprié.
1. Vous pouvez :

   * saisir le nom du membre requis (compte utilisateur ou de groupe) ;
   * ou utiliser **Parcourir...** pour rechercher et sélectionner l’entité (compte utilisateur ou de groupe) à ajouter.

1. Cliquez sur Enregistrer (symbole de coche verte) pour la nouvelle propriété.

Vous pouvez également supprimer un membre existant avec le symbole de la corbeille.

## Gestion des droits d’accès {#access-right-management}

Grâce à l’onglet **Contrôle d’accès** de CRXDE Lite, vous pouvez définir des politiques de contrôle d’accès et affecter les autorisations associées.

Par exemple, pour **Chemin d’accès actuel**, sélectionnez la ressource requise dans le volet de gauche, l’onglet Contrôle d’accès dans le volet inférieur droit :

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

Les politiques sont classées en fonction des éléments suivants :

* **Politiques de contrôle d’accès applicables**

  Ces politiques peuvent être appliquées.

   Ce sont les politiques disponibles pour créer une politique locale. Une fois que vous avez sélectionné et ajouté une politique applicable, elle devient une politique locale.

* **Politiques de contrôle d’accès locales**

  Il s’agit des politiques de contrôle d’accès que vous avez appliquées. Vous pouvez les mettre à jour, les trier ou les supprimer.

  La politique locale remplace toutes les politiques héritées du parent.

* **Politiques de contrôle d’accès actuelles**

  Ce sont les politiques de contrôle d’accès désormais en vigueur pour toutes les demandes d’accès. Elles affichent les politiques agrégées dérivées des politiques locales et des politiques héritées du parent.

### Sélection d’une politique {#policy-selection}

Les politiques peuvent être sélectionnées pour les éléments suivants :

* **Chemin d’accès actuel**

  Comme dans l’exemple ci-dessus, sélectionnez une ressource dans le référentiel. Les politiques de ce « chemin d’accès actuel » s’affichent.

* **Référentiel**

  Sélectionne le contrôle d’accès au niveau du référentiel. Par exemple, lors de la définition de l’autorisation `jcr:namespaceManagement`, qui n’est appropriée que pour le référentiel, et non pour le nœud.

* **Principal de sécurité**

  Principal de sécurité enregistré dans le référentiel.

  Vous pouvez saisir le nom du **principal de sécurité** ou cliquer sur l’icône à droite du champ pour ouvrir la boîte de dialogue **Sélectionner un principal de sécurité**.

  Cela permet de **rechercher** une **personne** ou un **groupe**. Sélectionnez le principal de sécurité nécessaire dans la liste qui s’affiche, puis cliquez sur **OK** pour reprendre la valeur dans la boîte de dialogue précédente.

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>Pour simplifier la gestion, Adobe vous recommande d’attribuer des droits d’accès aux comptes de groupe, et non à des comptes utilisateurs individuels.
>
>Il est plus facile de gérer quelques groupes que de nombreux comptes d’utilisateurs.

### Autorisations {#privileges}

Les autorisations ci-dessous peuvent être sélectionnées lors de l’ajout d’une entrée de contrôle d’accès (pour plus d’informations, voir [API de sécurité](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html)) :

<table>
 <tbody>
  <tr>
   <th><strong>Nom de l’autorisation</strong></th>
   <th><strong>Qui contrôle l’autorisation pour...</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>Récupérer un nœud et lire ses propriétés et leurs valeurs</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>Il s’agit d’une autorisation agrégée spécifique à Jackrabbit de jcr:write et jcr:nodeTypeManagement.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>Il s’agit d’une autorisation agrégée qui contient tous les autres privilèges prédéfinis.</td>
  </tr>
  <tr>
   <td><strong>Avancé</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>Effectuer la réplication d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>Créer les nœuds enfants d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>Effectuer des opérations de cycle de vie sur un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>Verrouiller et déverrouiller un nœud ; actualiser un verrou</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>Modifier les politiques de contrôle d’accès d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>Créer, modifier et supprimer les propriétés d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>Enregistrer, annuler l’enregistrement et modifier les définitions d’espace de noms</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>Importer des définitions de type de nœud dans le référentiel</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>Ajouter et supprimer des types de nœuds mixin et modifier le type de nœud principal d’un nœud Cela inclut également les appels de Node.addNode et les méthodes d’importation XML, dans lesquels le type mixin ou principal du nouveau nœud est spécifié explicitement.</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>Lire la politique de contrôle d’accès d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>Supprimer les nœuds enfants d’un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>Supprimer un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>Effectuer des opérations de gestion de la rétention sur un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>Exécuter des opérations de contrôle de version sur un nœud</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>Créer et supprimer des espaces de travail via l’API JCR</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>Il s’agit d’une autorisation agrégée qui contient :<br /> - jcr:modifyProperties<br /> - jcr:addChildNodes<br /> - jcr:removeNode<br /> - jcr:removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>Enregistrer une nouvelle autorisation</td>
  </tr>
 </tbody>
</table>

### Enregistrement de nouvelles autorisations {#registering-new-privileges}

Vous pouvez également enregistrer de nouvelles autorisations :

1. Dans la barre d’outils, sélectionnez **Outils**, puis **Autorisations** pour afficher les autorisations actuellement enregistrées.

   ![ac_privileges](assets/ac_privileges.png)

1. Utilisez l’icône d’**enregistrement d’autorisation** (**+**) pour définir une autorisation :

   ![ac_privilegeregister](assets/ac_privilegeregister.png)

1. Cliquez sur **OK** pour enregistrer. L’autorisation peut maintenant être sélectionnée.

### Ajout d’une entrée de contrôle d’accès {#adding-an-access-control-entry}

1. Sélectionnez votre ressource et ouvrez l’onglet **Contrôle d’accès**.

1. Pour ajouter une **politique de contrôle d’accès locale**, cliquez sur l’icône **+** à droite de la liste **Politique de contrôle d’accès applicable** :

   ![crx_accesscontrol_applicable](assets/crx_accesscontrol_applicable.png)

1. Une nouvelle entrée s’affiche sous **Politiques de contrôle d’accès locales :**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. Cliquez sur l’icône **+** pour ajouter une entrée :

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >Actuellement, une solution de contournement est nécessaire pour spécifier une chaîne vide.
   >
   >Pour cela, vous devez utiliser `""`.

1. Définissez votre politique de contrôle d’accès et cliquez sur **OK** pour l’enregistrer. Votre nouvelle politique :

   * est répertoriée sous **Politiques de contrôle d’accès locales** ;
   * les modifications sont répercutées dans les **politiques de contrôle d’accès actuelles**.

CRX valide votre sélection ; pour un principal donné, il existe (au plus) une entrée de refus et une entrée d’autorisation sur un nœud donné. La mise en œuvre efface toujours les entrées redondantes et s’assure que les mêmes autorisations ne figurent pas à la fois dans les entrées d’autorisation et de refus.

### Ordre des politiques de contrôle d’accès locales {#ordering-local-access-control-policies}

L’ordre dans la liste indique l’ordre dans lequel les politiques sont appliquées.

1. Dans le tableau **Politiques de contrôle d’accès locales**, sélectionnez l’entrée souhaitée et faites-la glisser vers la nouvelle position dans le tableau.

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. Les modifications sont affichées dans les tableaux pour les **politiques de contrôle d’accès locales** et **actuelles**.

### Suppression d’une politique de contrôle d’accès {#removing-an-access-control-policy}

1. Dans le tableau **Politiques de contrôle d’accès locales**, cliquez sur l’icône rouge (-) à droite de l’entrée.
1. L’entrée est supprimée dans les tableaux des **politiques de contrôle d’accès locales** et **actuelles**.

### Test d’une politique de contrôle d’accès {#testing-an-access-control-policy}

1. Dans la barre d’outils de CRXDE Lite, sélectionnez **Outils**, puis **Tester le contrôle d’accès**.
1. Une nouvelle boîte de dialogue s’affiche dans le volet supérieur droit. Sélectionnez le **chemin d’accès** et/ou le **principal de sécurité** à tester.
1. Cliquez sur **Test** pour afficher les résultats de votre sélection :

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
