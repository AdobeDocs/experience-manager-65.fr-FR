---
title: Administration et sécurité des utilisateurs
description: Découvrez l’administration et la sécurité des utilisateurs et des utilisatrices dans AEM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 100%

---

# Administration et sécurité des utilisateurs{#user-administration-and-security}

Ce chapitre décrit comment configurer et gérer l’autorisation utilisateur ainsi que la théorie du fonctionnement de l’authentification et de l’autorisation dans AEM.

## Utilisateurs, utilisatrices et groupes dans AEM {#users-and-groups-in-aem}

Cette section aborde plus en détail les différentes entités et les concepts associés afin de vous aider à configurer un concept de gestion des utilisateurs et des utilisatrices facile à gérer.

### Utilisateurs {#users}

Les utilisateurs et les utilisatrices se connectent à AEM avec leur compte. Chaque compte d’utilisateur est unique et contient les détails de base du compte ainsi que les privilèges qui lui sont attribués.

Les utilisateurs et les utilisatrices sont souvent membres de groupes, ce qui simplifie l’attribution de ces autorisations et/ou privilèges.

### Groupes {#groups}

Les groupes sont des ensembles d’utilisateurs ou d’autres groupes, ou les deux. Ces collections sont toutes appelées membres d’un groupe.

Le principal objectif des groupes est de simplifier le processus de maintenance en réduisant le nombre d’entités à mettre à jour : une modification apportée à un groupe est appliquée à tous les membres du groupe. Les groupes reflètent souvent :

* un rôle au sein de l’application ; par exemple une personne autorisée à naviguer dans le contenu ou à contribuer au contenu.
* votre propre organisation ; vous pouvez étendre les rôles afin de différencier les contributeurs de différents services lorsqu’ils sont limités à différentes branches dans l’arborescence de contenu.

Par conséquent, les groupes tendent à rester stables, alors que les utilisateurs et utilisatrices vont et viennent plus fréquemment.

Grâce à une planification et une structure propre, l’utilisation de groupes peut refléter votre structure, ce qui vous donne une vue d’ensemble clair et un mécanisme efficace pour les mises à jour.

### Utilisateurs, utiliatrices et groupes intégrés {#built-in-users-and-groups}

La gestion de contenu web AEM installe plusieurs utilisateurs, utilisatrices et groupes. Ces collections s’affichent lorsque vous accédez pour la première fois à la console de sécurité après l’installation.

Les tableaux suivants répertorient chaque élément avec :

* une brève description ;
* des recommandations quant aux modifications nécessaires.

*Modifiez tous les mots de passe par défaut* (si vous ne supprimez pas le compte lui-même dans certains cas).

<table>
 <tbody>
  <tr>
   <td>ID de l’utilisateur</td>
   <td>Type</td>
   <td>Description</td>
   <td>Recommandation</td>
  </tr>
  <tr>
   <td><p>administrateur</p> <p>Mot de passe par défaut : admin</p> </td>
   <td>Utilisateur</td>
   <td><p>Compte d’administration système avec droits d’accès complets.</p> <p>Ce compte est utilisé pour la connexion entre la gestion de contenu web AEM et CRX.</p> <p>Si vous supprimez ce compte par erreur, il sera recréé lors du redémarrage du référentiel (dans la configuration par défaut).</p> <p>Le compte administrateur est une exigence de la plateforme AEM. Par conséquent, ce compte ne peut pas être supprimé.</p> </td>
   <td><p>Adobe vous recommande de modifier le mot de passe par défaut de ce compte d’utilisateur.</p> <p>De préférence lors de l’installation, bien que vous puissiez le faire par la suite.</p> <p>Remarque : ne confondez pas ce compte avec le compte administrateur du moteur de servlet CQ.</p> </td>
  </tr>
  <tr>
   <td><p>anonyme</p> <p> </p> </td>
   <td>Utilisateur</td>
   <td><p>Détient les droits par défaut pour l’accès non authentifié à une instance. Par défaut, ce compte contient les droits d’accès minimum.</p> <p>Si vous supprimez ce compte par erreur, il sera recréé lors du redémarrage. Il ne peut pas être supprimé définitivement, mais il peut être désactivé.</p> </td>
   <td>Évitez de supprimer ou de désactiver ce compte, car cela aurait une incidence négative sur le fonctionnement des instances de création. Si vous devez le supprimer pour des raisons de sécurité, assurez-vous d’abord de tester correctement les effets qu’il a sur vos systèmes.</td>
  </tr>
  <tr>
   <td><p>auteur </p> <p>Mot de passe par défaut : author</p> </td>
   <td>Utilisateur</td>
   <td><p>Compte de création autorisé à écrire dans /content. Comprend les privilèges de contributeur et de surfeur.</p> <p>Peut être utilisé comme webmaster, car il a accès à l’ensemble de l’arborescence /content.</p> <p>Ce compte n’est pas un utilisateur intégré, mais un autre utilisateur de démonstration de Geometrixx.</p> </td>
   <td><p>Adobe recommande de supprimer complètement le compte ou de modifier le mot de passe par défaut.</p> <p>De préférence lors de l’installation, bien que vous puissiez le faire par la suite.</p> </td>
  </tr>
  <tr>
   <td>administrateurs</td>
   <td>Groupe</td>
   <td><p>Groupe donnant des droits d’administrateur à tous ses membres. Seule l’administration est autorisée à modifier ce groupe.</p> <p>Dispose de droits d’accès complets.</p> </td>
   <td>Même si vous définissez un paramètre « deny-everyone » sur un nœud, l’administration peut y accéder.</td>
  </tr>
  <tr>
   <td>auteurs de contenu</td>
   <td>Groupe</td>
   <td><p>Groupe responsable de la modification du contenu. Nécessite des autorisations de lecture, de modification, de création et de suppression.</p> </td>
   <td>Vous pouvez créer vos propres groupes 'auteurs de contenu' avec des droits d’accès spécifiques au projet, à condition d’ajouter des autorisations de lecture, de modification, de création et de suppression.</td>
  </tr>
  <tr>
   <td>contributeur</td>
   <td>Groupe</td>
   <td><p>Privilèges de base qui permettent à l’utilisateur ouà l’utilisatrice d’écrire du contenu (fonctionnalité uniquement).</p> <p>N’attribue aucun privilège sur l’arborescence /content. Ils doivent être attribués aux groupes ou aux utilisateurs et utilisatrices de manière individuelle.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>utilisateurs DAM</td>
   <td>Groupe</td>
   <td>Groupe de référence prêt à l’emploi pour un utilisateur AEM Assets standard. Les membres de ce groupe disposent des droits appropriés pour activer le chargement/partage de ressources et de collections.</td>
   <td> </td>
  </tr>
  <tr>
   <td>tout le monde</td>
   <td>Groupe</td>
   <td><p>Chaque utilisateur et utilisatrice d’AEM est membre du groupe Tout le monde, même si vous ne pouvez pas voir le groupe ou la relation d’appartenance dans tous les outils.</p> <p>Ce groupe peut être considéré comme les droits par défaut, car il peut être utilisé pour appliquer des autorisations à tout le monde, même aux utilisateurs et utilisatrices qui seront créés ultérieurement.</p> </td>
   <td><p>Ne modifiez et ne supprimez pas ce groupe.</p> <p>La modification de ce compte a des répercussions en matière de sécurité.</p> </td>
  </tr>
  <tr>
   <td>admininistration balises</td>
   <td>Groupe</td>
   <td>Groupe autorisé à modifier des balises.</td>
   <td> </td>
  </tr>
  <tr>
   <td>administrateurs-utilisateurs</td>
   <td>Groupe</td>
   <td>Autorise l’administration des utilisateurs, c’est-à-dire le droit de créer des utilisateurs et des groupes.</td>
   <td> </td>
  </tr>
  <tr>
   <td>éditeurs de workflow</td>
   <td>Groupe</td>
   <td>Groupe autorisé à créer et modifier des modèles de workflow.</td>
   <td> </td>
  </tr>
  <tr>
   <td>utilisateurs de workflow</td>
   <td>Groupe</td>
   <td><p>Un utilisateur ou une utilisatrice participant à un workflow doit être membre du groupe utilisateurs de workflow. Donne à l’utilisateur ou à l’utilisatrice un accès complet à : /etc/workflow/instances afin que l’instance de workflow puisse être mise à jour.</p> <p>Le groupe est inclus dans l’installation standard, mais vous devez y ajouter manuellement les utilisateurs et les utilisatrices.</p> </td>
  </tr>
 </tbody>
</table>

## Autorisations dans AEM {#permissions-in-aem}

AEM utilise des listes de contrôle d’accès pour déterminer quelles sont les actions qu’un utilisateur ou un groupe peut effectuer et où.

### Autorisations et listes de contrôle d’accès {#permissions-and-acls}

Les autorisations définissent les personnes autorisées à effectuer des actions sur une ressource. Les autorisations sont le résultat d’évaluations de [contrôle d’accès](#access-control-lists-and-how-they-are-evaluated).

Vous pouvez modifier les autorisations accordées ou refusées à un utilisateur donné en cochant ou décochant les cases correspondant à chaque [action](security.md#actions) dans AEM. Une coche indique que l’action est autorisée. L’absence de coche indique que l’action est refusée.

L’emplacement de la coche dans la grille indique également les autorisations dont disposent les utilisateurs et utilisatrices à tel ou tel emplacement dans AEM (c’est-à-dire les chemins d’accès).

### Actions {#actions}

Les actions peuvent être effectuées sur une page (ressource). Pour chaque page dans la hiérarchie, vous pouvez spécifier quelle action l’utilisateur est autorisé à effectuer sur cette page. Les [autorisations](#permissions-and-acls) vous permettent d’autoriser ou de refuser une action.

<table>
 <tbody>
  <tr>
   <td><strong>Action </strong></td>
   <td><strong>Description </strong></td>
  </tr>
  <tr>
   <td>Lecture</td>
   <td>L’utilisateur est autorisé à lire la page et les pages enfants.</td>
  </tr>
  <tr>
   <td>Modification</td>
   <td><p>L’utilisateur peut :</p>
    <ul>
     <li>modifier le contenu existant sur la page et sur les pages enfants ;</li>
     <li>créer de nouveaux paragraphes sur la page ou une page enfant.</li>
    </ul> <p>Au niveau de JCR, les utilisateurs et utilisatrices peuvent modifier une ressource en modifiant les propriétés, le verrouillage, le contrôle de version, les modifications du type de nœud, et disposer d’une autorisation d’écriture complète sur les nœuds définissant un noeud enfant jcr:content. Par exemple, cq:Page, nt:file, cq:Asset.</p> </td>
  </tr>
  <tr>
   <td>Création</td>
   <td><p>L’utilisateur peut :</p>
    <ul>
     <li>créer une page ou une page enfant.</li>
    </ul> <p>Si l’action <strong>modifier</strong> est refusée, les sous-arborescences en dessous du nœud jcr:content sont spécifiquement exclues, car la création du nœud jcr:content et de ses nœuds enfants est considérée comme une modification de page. Cette règle s’applique uniquement aux nœuds définissant un nœud enfant jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Suppression</td>
   <td><p>L’utilisateur peut :</p>
    <ul>
     <li>supprimer des paragraphes existants de la page ou de toute page enfant ;</li>
     <li>supprimer une page ou une page enfant.</li>
    </ul> <p>Si l’action <strong>modifier</strong> est refusée, les sous-arborescences en dessous du nœud jcr:content sont exclues, car la suppression du nœud jcr:content et de ses nœuds enfants est considérée comme une modification de page. Cette règle s’applique uniquement aux nœuds définissant un nœud enfant jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Lecture de l’ACL</td>
   <td>L’utilisateur peut lire la liste de contrôle d’accès de la page ou des pages enfants.</td>
  </tr>
  <tr>
   <td>Modification de l’ACL</td>
   <td>L’utilisateur peut modifier la liste de contrôle d’accès de la page ou de toutes les pages enfants.</td>
  </tr>
  <tr>
   <td>Réplication</td>
   <td>L’utilisateur peut répliquer du contenu dans un autre environnement (l’environnement de publication, par exemple). L’autorisation est également appliquée à toutes les pages enfants.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM génère automatiquement des groupes d’utilisateurs pour l’affectation de rôle (Propriétaire, Éditeur, Observateur) dans les [collections](/help/assets/manage-collections.md). Cependant, ajouter manuellement des listes de contrôle d’accès pour ces groupes peut introduire des vulnérabilités en matière de sécurité dans AEM. Adobe recommande d’éviter d’ajouter des listes de contrôle d’accès manuellement.

### Listes de contrôle d’accès et méthode d’évaluation {#access-control-lists-and-how-they-are-evaluated}

La gestion de contenu web AEM utilise des listes de contrôle d’accès (ACL) pour organiser les autorisations appliquées aux différentes pages.

Les listes de contrôle d’accès sont composées d’autorisations spécifiques et sont utilisées pour déterminer l’ordre dans lequel ces autorisations s’appliquent. La liste est établie selon la hiérarchie des pages concernées. Cette liste est ensuite analysée de bas en haut jusqu’à trouver la première autorisation appropriée à appliquer à une page.

>[!NOTE]
>
>Des listes de contrôle d’accès sont fournies avec les échantillons. Il est recommandé d’examiner et de déterminer ce qui convient à vos applications. Pour passer en revue les listes de contrôle d’accès incluses, accédez à **CRXDE** et sélectionnez l’onglet **Contrôle d’accès** pour les nœuds suivants :
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>Votre application personnalisée peut définir l’accès pour d’autres relations, telles que :
>
>* `*/social/relationships/friend/*`
>* ou `*/social/relationships/pending-following/*`.
>
>Lorsque vous créez des listes de contrôle d’accès spécifiques aux communautés, les membres rejoignant ces communautés peuvent se voir accorder des autorisations supplémentaires. Par exemple, lorsque des utilisateurs et des utilisatrices rejoignent les communautés à l’adresse `/content/we-retail/us/en/community`

### États des autorisations {#permission-states}

>[!NOTE]
>
>Pour les utilisateurs et utilisatrices de CQ 5.3 :
>
>Contrairement aux versions précédentes de CQ, il ne faut plus accorder les autorisations **créer** et **supprimer** si l’utilisateur ou l’utilisatrice doit uniquement modifier les pages. Au lieu de cela, accordez l’action **modifier** uniquement si vous souhaitez que les utilisateurs et utilisatrices puissent créer, modifier ou supprimer des composants sur des pages existantes.
>
>Pour des raisons de rétrocompatibilité, les tests des actions ne prennent pas en compte le traitement spécial des nœuds définissant **jcr:content**.

| **Action** | **Description** |
|---|---|
| Autoriser (coche) | La gestion de contenu web d’AEM permet à l’utilisateur d’effectuer l’action sur cette page ou sur n’importe quelle page enfant. |
| Refuser (aucune coche) | La gestion de contenu web d’AEM ne permet pas à l’utilisateur d’effectuer l’action sur cette page ou sur n’importe quelle page enfant. |

Les autorisations s’appliquent également aux pages enfants.

Si une autorisation n’est pas héritée du nœud parent, mais dispose d’au moins une entrée locale pour lui, les symboles suivants sont ajoutés à la case à cocher. Une entrée locale est une entrée créée dans l’interface CRX 2.2 (les listes de contrôle d’accès avec caractères génériques ne peuvent actuellement être créées que dans CRX).

Pour une action sur un chemin d’accès donné :

<table>
 <tbody>
  <tr>
   <td>* (astérisque)</td>
   <td>Il existe au moins une entrée locale (active ou inactive). Ces listes de contrôle d’accès avec caractères génériques sont définies dans CRX.</td>
  </tr>
  <tr>
   <td>! (point d’exclamation)</td>
   <td>Au moins une entrée n’a actuellement aucun effet.</td>
  </tr>
 </tbody>
</table>

Lorsque vous placez le pointeur de la souris sur l’astérisque ou le point d’exclamation, une info-bulle affiche plus de détails à propos des entrées déclarées. L’info-bulle est divisée en deux parties :

<table>
 <tbody>
  <tr>
   <td>Partie supérieure</td>
   <td><p>Répertorie les entrées actives.</p> </td>
  </tr>
  <tr>
   <td>Partie inférieure</td>
   <td>Répertorie les entrées non actives susceptibles d’avoir un effet à un autre endroit de l’arborescence (comme indiqué par un attribut spécial associé à l’entrée de contrôle d’accès correspondante qui limite la portée de l’entrée). Sinon, il s’agit d’une entrée dont l’effet a été révoqué par une autre entrée définie dans le chemin d’accès donné ou au niveau d’un nœud ancêtre.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>Si aucune autorisation n’est définie pour une page, toutes les actions sont refusées.

Voici des recommandations pour la gestion des listes de contrôle d’accès :

* N’affectez pas d’autorisations directement aux utilisateurs. Attribuez-les uniquement à des groupes.

  Cela simplifie la gestion, dans la mesure où le nombre de groupes est beaucoup plus petit que le nombre d’utilisateurs et d’utilisatrices, et également plus stable.

* Si vous souhaitez qu’un groupe/utilisateur puisse uniquement modifier les pages, ne lui affectez pas de droits de création ou de refus. Accordez-leur uniquement des droits de modification et de lecture.
* Utilisez l’autorisation Refuser avec modération. Dans la mesure du possible, utilisez uniquement l’action Autoriser.

  L’utilisation de l’autorisation Autoriser peut avoir des effets inattendus si les autorisations sont appliquées dans un ordre différent de l’ordre prévu. Si un utilisateur ou une utilisatrice est membre de plusieurs groupes, les instructions Refuser d’un groupe peuvent annuler l’instruction Autoriser d’un autre groupe ou vice versa. Il est difficile de garder une vue d’ensemble dans ce genre de situation qui peut facilement donner des résultats imprévus, alors que les attributions Autoriser ne provoquent pas de tels conflits.

  Adobe vous recommande d’utiliser Autoriser plutôt que Refuser. Consultez les [bonnes pratiques](#best-practices).

Avant de modifier l’une des autorisations, assurez-vous de comprendre son fonctionnement et ses interactions. Consultez la documentation CRX qui explique comment la gestion de contenu web AEM [évalue les droits d’accès](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated), ainsi que des exemples sur la configuration des listes de contrôle d’accès.

### Autorisations {#permissions}

Les autorisations permettent aux utilisateurs, aux utilisatrices et aux groupes d’accéder aux fonctionnalités AEM sur les pages AEM.

Vous passez en revue les autorisations par chemin d’accès en développant ou en réduisant les nœuds et vous pouvez suivre l’héritage des autorisations jusqu’au nœud racine.

Vous autorisez ou refusez les autorisations en cochant ou en décochant les cases appropriées.

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### Affichage des informations détaillées sur les autorisations {#viewing-detailed-permission-information}

Outre la vue Grille, AEM fournit une vue détaillée des autorisations pour un utilisateur/groupe sélectionné dans un chemin d’accès donné. La vue détaillée fournit des informations supplémentaires.

Outre l’affichage des informations, vous pouvez également inclure ou exclure l’utilisateur ou le groupe actuel d’un groupe. Consultez la section [Ajout d’utilisateurs ou de groupes lors de l’ajout d’autorisations](#adding-users-or-groups-while-adding-permissions). Les modifications apportées ici sont immédiatement répercutées dans la portion supérieure de la vue détaillée.

Pour accéder à la vue détaillée, dans l’onglet **Autorisations**, cliquez sur **Détails** pour le groupe ou l’utilisateur et le chemin d’accès.

![permissiondetails](assets/permissiondetails.png)

Les détails sont scindés en deux parties :

<table>
 <tbody>
  <tr>
   <td>Partie supérieure</td>
   <td><p>Répète les informations affichées dans la grille de l’arborescence. Pour chaque action, une icône indique si l’action est autorisée ou refusée :</p>
    <ul>
     <li>aucune icône = aucune entrée déclarée</li>
     <li>(coche) = action déclarée (autoriser)</li>
     <li>(-) = action déclarée (refus)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Partie inférieure</td>
   <td><p>Affiche la grille des utilisateurs et des groupes qui correspondent aux critères suivants :</p>
    <ul>
     <li>Déclare une entrée pour le chemin d’accès ET</li>
     <li>Est celui qui reçoit l’ID autorisable OU est un groupe</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Emprunt de l’identité d’un utilisateur {#impersonating-another-user}

La [fonctionnalité Emprunter l’identité](/help/sites-authoring/user-properties.md#user-settings) permet à un utilisateur ou une utilisatrice de travailler pour le compte de quelqu’un d’autre.

Cela signifie qu’un compte d’utilisateur peut spécifier d’autres comptes pouvant fonctionner avec son compte. Par exemple, si l’utilisateur ou utilisatrice B est autorisé(e) à emprunter l’identité de l’utilisateur ou utilisatrice A, l’utilisateur ou utilisatrice B peut agir en utilisant les détails complets du compte de l’utilisateur ou de l’utilisatrice A.

Cette fonctionnalité permet aux comptes d’emprunteur d’identité d’effectuer des tâches comme s’ils utilisaient le compte qu’ils empruntent. Par exemple, en cas d’absence ou pour partager une lourde charge de travail temporaire.

>[!NOTE]
>
>Pour que l’emprunt d’identité fonctionne pour les utilisateurs et utilisatrices qui ne sont pas dministrateurs ou administratrices, l’emprunteur (dans le cas ci-dessus l’utilisateur ou utilisatrice B) doit disposer des autorisations de lecture dans le chemin `/home/users`.
>
>Voir [Autorisations dans AEM](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>Si un compte emprunte l’identité d’un autre compte, il est très difficile de s’en rendre compte. Une entrée est créée dans le journal d’audit lorsque l’emprunt commence et se termine, mais les autres fichiers journaux (par exemple, le journal des accès) ne détiennent aucune information sur l’emprunt au niveau des événements. Ainsi, si l’utilisateur ou utilisatrice B emprunte l’identité de l’utilisateur ou utilisatrice A, tous les événements semblent avoir été effectués par l’utilisateur ou utilisatrice A.

>[!CAUTION]
>
>Le verrouillage d’une page peut être réalisé lorsque vous empruntez l’identité d’un utilisateur. Toutefois, une page verrouillée de cette manière peut uniquement être déverrouillée par l’utilisateur dont l’identité a été empruntée ou par un utilisateur disposant des droits d’administration.
>
>Les pages ne peuvent pas être déverrouillées en empruntant l’identité de l’utilisateur ou de l’utilisatrice qui les a verrouillées.

### Bonnes pratiques {#best-practices}

Ce qui suit décrit les bonnes pratiques lorsque vous travaillez avec des autorisations et des droits d’accès :

| Règle | Raison |
|--- |--- |
| *Utilisation de groupes* | Évitez d’affecter des droits d’accès utilisateur par utilisateur. Il existe plusieurs raisons à cela :<ul><li>Comme il y a beaucoup plus d’utilisateurs que de groupes, les groupes simplifient la structure.</li><li>Les groupes offrent une vue d’ensemble de tous les comptes.</li> <li>L’héritage est plus simple avec les groupes.</li><li>Les utilisateurs vont et viennent. Les groupes sont à long terme.</li></ul> |
| *Soyez positif* | Utilisez toujours l’instruction Autoriser pour spécifier les droits du groupe (chaque fois que possible). Évitez d’utiliser une instruction Refuser. Les groupes sont évalués dans l’ordre, et l’ordre peut être défini différemment par utilisateur. En d’autres termes : il se peut que vous ayez peu de contrôle sur l’ordre dans lequel les instructions sont mises en œuvre et évaluées. Si vous utilisez uniquement des instructions Autoriser, l’ordre n’a pas d’importance. |
| *Restez simple* | Il est important d’investir du temps et de réfléchir à la configuration d’une nouvelle installation. L’application d’une structure claire simplifie la gestion et l’administration au jour le jour, ce qui garantit que vos collègues actuels et leurs successeurs peuvent comprendre facilement ce qui est mis en œuvre. |
| *Testez* | Utilisez une installation de test pour vous exercer et vous assurer que vous comprenez les relations entre les différents utilisateurs et groupes. |
| *Utilisateurs et groupes par défaut* | Mettez toujours à jour les utilisateurs et les groupes par défaut immédiatement après l’installation afin d’éviter tout problème de sécurité. |

## Gestion des utilisateurs et des groupes {#managing-users-and-groups}

Les utilisateurs et utilisatrices incluent des personnes qui utilisent le système et des systèmes étrangers qui adressent des demandes au système.

Un groupe est un ensemble d’utilisateurs et utilisatrices.

Les deux peuvent être configurés à l’aide de la fonctionnalité d’administration des utilisateurs et utilisatrices de la console de sécurité.

### Accès à l’administration des utilisateurs et utilisatrices à l’aide de la console de sécurité {#accessing-user-administration-with-the-security-console}

Vous pouvez accéder à tous les utilisateurs, groupes et autorisations associées à l’aide de la console de sécurité. Toutes les procédures décrites dans cette section sont exécutées dans cette fenêtre.

Pour accéder à la sécurité de la gestion de contenu web AEM, effectuez l’une des opérations suivantes :

* Dans l’écran d’accueil ou à différents emplacements d’AEM, cliquez sur l’icône de sécurité :

![Onglet Sécurité WCM AEM](do-not-localize/wcmtoolbar.png)

* Accédez directement à `https://<server>:<port>/useradmin`. Assurez-vous de vous connecter à AEM avec des droits d’administration.

La fenêtre suivante s’affiche :

![cqsecuritypage](assets/cqsecuritypage.png)

L’arborescence de gauche répertorie tous les utilisateurs et groupes actuellement dans le système. Vous pouvez sélectionner les colonnes à afficher, trier le contenu des colonnes et même modifier l’ordre d’affichage des colonnes en faisant glisser l’en-tête de colonne vers une nouvelle position.

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

Les onglets permettent d’accéder à diverses configurations :

<!-- ??? in table below. -->

| Tabulation | Description |
|--- |--- |
| Zone de filtrage | Mécanisme de filtrage des utilisateurs, des utilisatrices ou des groupes répertoriés, ou des trois. Consultez la section [Gestion des utilisateurs et des groupes](#filtering-users-and-groups). |
| Masquer les utilisateurs | Bouton (bascule) qui masque tous les utilisateurs et utilisatrices répertoriés, et affiche uniquement les groupes. Consultez la section [Dissimulation des utilisateurs et des groupes](#hiding-users-and-groups). |
| Masquer les groupes | Bouton bascule qui masque tous les groupes répertoriés, et affiche uniquement les utilisateurs et utilisatrices. Consultez la section [Dissimulation des utilisateurs et des groupes](#hiding-users-and-groups). |
| Modifier | Un menu vous permettant de créer et de supprimer ainsi que d’activer et de désactiver des utilisateurs ou des groupes. Consultez les sections [Création d’utilisateurs et de groupes](#creating-users-and-groups) et [Suppression d’utilisateurs et de groupes](#deleting-users-and-groups). |
| Propriétés | Répertorie les informations sur l’utilisateur ou le groupe pouvant inclure des informations d’e-mail, une description et un nom. Vous permet également de modifier le mot de passe d’un utilisateur ou d’une utilisatrice. Consultez les sections [Création d’utilisateurs et de groupes](#creating-users-and-groups), [Modification des propriétés d’utilisateur et de groupe](#modifying-user-and-group-properties) et [Modification d’un mot de passe utilisateur](#changing-a-user-password). |
| Groupes | Répertorie tous les groupes auxquels l’utilisateur ou le groupe sélectionné appartient. Vous pouvez affecter l’utilisateur ou le groupe sélectionné à d’autres groupes ou les supprimer des groupes. Consultez la section [Groupes](#adding-users-or-groups-to-a-group). |
| Membres | Disponible uniquement pour les groupes. Répertorie les membres d’un groupe spécifique. Consultez la section [Membres](#members-adding-users-or-groups-to-a-group). |
| Autorisations | Vous pouvez attribuer des autorisations à un utilisateur ou à un groupe. Permet de contrôler les éléments suivants :<ul><li>Les autorisations liées à des pages ou des nœuds spécifiques. Consultez la section [Définition des autorisations](#setting-permissions). </li><li>Les autorisations liées à la création et la suppression de pages et à la modification de hiérarchie. ??? vous permet d’[allouer des privilèges](#settingprivileges), par exemple la modification de hiérarchie, qui permet de créer et supprimer des pages.</li><li>Les autorisations liées aux [droits de réplication](#setting-replication-privileges) (généralement de l’auteur à la publication) selon un chemin d’accès.</li></ul> |
| Emprunteurs d’identité | Permet à un autre utilisateur d’emprunter l’identité d’un compte. Utile lorsque vous avez besoin qu’un utilisateur agisse au nom d’un autre utilisateur. Consultez la section [Emprunt d’identités utilisateurs](#impersonating-another-user). |
| Préférences | Permet de définir les [préférences d’un groupe ou d’un utilisateur](#setting-user-and-group-preferences). Par exemple, les préférences de langue. |

### Filtrage des utilisateurs, des utilisatrices et des groupes {#filtering-users-and-groups}

Vous pouvez filtrer la liste en entrant une expression de filtre, qui masque tous les utilisateurs et les groupes qui ne correspondent pas à l’expression. Vous pouvez également masquer des utilisateurs et des groupes à l’aide des boutons [Masquer les utilisateurs et Masquer les groupes](#hiding-users-and-groups).

Pour filtrer les utilisateurs, les utilisatrices ou les groupes :

1. Dans l’arborescence de gauche, tapez votre expression de filtre dans l’espace fourni. Par exemple, la saisie de **admin** affiche tous les utilisateurs, les utilisatrices et groupes contenant cette chaîne.
1. Cliquez sur la loupe pour filtrer la liste.

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. Cliquez sur le **x** lorsque vous souhaitez supprimer tous les filtres.

### Masquage des utilisateurs, des utilisatrices et des groupes {#hiding-users-and-groups}

Le masquage des utilisateurs ou des groupes est une autre façon de filtrer la liste de tous les utilisateurs et groupes à l’intérieur d’un système. Il existe deux mécanismes. Cliquer sur Masquer les utilisateurs masque tous les utilisateurs de la vue et cliquer sur Masquer Groupes masque tous les groupes de la vue (vous ne pouvez pas masquer des utilisateurs et des groupes en même temps). Pour filtrer la liste à l’aide d’une expression de filtre, voir [Filtrage des utilisateurs et des groupes](#filtering-users-and-groups).

Pour masquer les utilisateurs, les utilisatrices et les groupes :

1. Dans la console **Sécurité**, cliquez sur **Masquer les utilisateurs** ou **Masquer Groupes**. Le bouton sélectionné est mis en surbrillance.

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. Pour que les utilisateurs ou les groupes réapparaissent, cliquez de nouveau sur le bouton correspondant.

### Création d’utilisateurs et de groupes {#creating-users-and-groups}

Pour créer un utilisateur, une utilisatrice ou un groupe :

1. Dans l’arborescence de la console **Sécurité**, cliquez sur **Modifier**, puis sur **Créer un utilisateur** ou **Créer un groupe**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. Saisissez les informations requises, selon que vous créez un utilisateur, une utilisatrice ou un groupe.

   * Si vous sélectionnez **Créer un utilisateur**, entrez l’ID de connexion, le prénom et le nom, l’adresse électronique et un mot de passe. Par défaut, AEM crée un chemin d’accès en fonction de la première lettre du nom de famille, mais vous pouvez choisir un autre chemin d’accès.

   ![createuserdialog](assets/createuserdialog.png)

   * Si vous sélectionnez **Créer un groupe**, entrez un ID de groupe et une description facultative.

   ![creategroupdialog](assets/creategroupdialog.png)

1. Cliquez sur **Créer**. L’utilisateur, l’utilisatrice ou le groupe que vous avez créé apparaît dans l’arborescence.

### Suppression d’utilisateurs, d’utilisatrices et de groupes {#deleting-users-and-groups}

Pour supprimer un utilisateur, une utilisatrice ou un groupe :

1. Dans la console **Sécurité**, sélectionnez l’utilisateur ou le groupe que vous souhaitez supprimer. Si vous souhaitez supprimer plusieurs éléments, utilisez la combinaison Maj+clic ou Ctrl+clic pour les sélectionner.
1. Cliquez sur **Modifier**, puis sélectionnez Supprimer. La gestion de contenu web AEM vous demande si vous souhaitez supprimer l’utilisateur, l’utilisatrice ou le groupe.
1. Cliquez sur **OK** pour confirmer ou sur Annuler.

### Modification des propriétés des utilisateurs, des utilisatrices et des groupes {#modifying-user-and-group-properties}

Pour modifier les propriétés des, des utilisatrices et des groupes :

1. Dans la console **Sécurité**, double-cliquez sur le nom de l’utilisateur ou du groupe que vous souhaitez modifier.

1. Cliquez sur l’onglet **Propriétés**, effectuez les modifications requises, puis cliquez sur **Enregistrer**.

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>Le chemin d’accès de l’utilisateur s’affiche en bas des propriétés d’utilisateur. Il ne peut pas être modifié.

### Modification d’un mot de passe d’utilisateur {#changing-a-user-password}

Utilisez la procédure suivante pour modifier le mot de passe d’un utilisateur.

>[!NOTE]
>
>Vous ne pouvez pas utiliser la console Sécurité pour modifier le mot de passe de l’administrateur. Pour modifier le mot de passe du compte d’administrateur, utilisez la [console Utilisateurs](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) fournie par les Opérations Granite.
>
>Si vous utilisez AEM Forms on JEE, n’utilisez pas les instructions ci-dessous pour modifier le mot de passe. Utilisez plutôt l’Admin Console d’AEM Forms sur JEE (/adminui) pour modifier le mot de passe.

1. Dans la console **Sécurité**, double-cliquez sur le nom de l’utilisateur dont vous souhaitez modifier le mot de passe.
1. Cliquez sur l’onglet **Propriétés** (s’il n’est pas déjà actif).
1. Cliquez sur **Définir le mot de passe**. La fenêtre Définir le mot de passe s’ouvre et vous pouvez y modifier votre mot de passe.

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. Saisissez le nouveau mot de passe deux fois ; comme ils ne s’affichent pas en clair, cette action sert de confirmation. S’ils ne correspondent pas, le système affiche une erreur.
1. Cliquez sur **Définir** pour activer le nouveau mot de passe du compte.

### Ajout d’utilisateurs, d’utilisatrices ou de groupes à un groupe {#adding-users-or-groups-to-a-group}

AEM propose trois manières d’ajouter des utilisateurs, des utilisatrices ou des groupes à un groupe existant :

* Lorsque vous vous trouvez dans le groupe, vous pouvez ajouter des membres (utilisateurs, utilisatrices ou groupes).
* Lorsque vous vous trouvez dans le membre, vous pouvez ajouter des membres à des groupes.
* Lorsque vous travaillez sur des autorisations, vous pouvez ajouter des membres à des groupes.

### Groupes – Ajout d’utilisateurs, d’utilisatrices ou de groupes à un groupe {#groups-adding-users-or-groups-to-a-group}

L’onglet **Groupes** indique à quels groupes le compte actuel appartient. Vous pouvez l’utiliser pour ajouter le compte sélectionné à un groupe :

1. Double-cliquez sur le nom du compte (utilisateur, utilisatrice ou groupe) que vous souhaitez affecter à un groupe.
1. Cliquez sur l’onglet **Groupes**. Une liste des groupes auxquels le compte appartient déjà s’affiche.
1. Dans l’arborescence, cliquez sur le nom du groupe que vous souhaitez ajouter au compte et faites-le glisser vers le volet **Groupes**. (Si vous souhaitez ajouter plusieurs utilisateurs ou utilisatrices, utilisez la combinaison Maj+clic ou Ctrl+clic sur ces noms et faites-les glisser.)

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Membres – Ajout d’utilisateurs, d’utilisatrices ou de groupes à un groupe {#members-adding-users-or-groups-to-a-group}

L’onglet **Membres** fonctionne uniquement pour les groupes et indique quels utilisateurs et groupes appartiennent au groupe actuel. Vous pouvez l’utiliser pour ajouter des comptes à un groupe :

1. Double-cliquez sur le nom du groupe auquel vous souhaitez ajouter des membres.
1. Cliquez sur l’onglet **Membres**. Une liste des membres appartenant déjà à ce groupe s’affiche.
1. Dans l’arborescence, cliquez sur le nom du membre que vous souhaitez ajouter au groupe et faites-le glisser vers le volet **Membres**. (Si vous souhaitez ajouter plusieurs utilisateurs ou utilisatrices, utilisez la combinaison Maj+clic ou Ctrl+clic sur ces noms et faites-les glisser.)

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Ajout d’utilisateurs ou de groupes lors de l’ajout d’autorisations {#adding-users-or-groups-while-adding-permissions}

Pour ajouter des membres à un groupe dans un chemin d’accès spécifique, procédez comme suit :

1. Double-cliquez sur le nom du groupe ou de l’utilisateur auquel vous souhaitez ajouter des utilisateurs.

1. Cliquez sur l’onglet **Autorisations**.

1. Accédez au chemin d’accès auquel vous souhaitez ajouter des autorisations et cliquez sur **Détails**. La partie inférieure de la fenêtre des détails indique qui dispose d’autorisations pour cette page.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Dans la colonne **Membre**, cochez les cases des membres qui doivent disposer d’autorisations au niveau de ce chemin d’accès. Décochez les cases des membres dont vous souhaitez supprimer les autorisations. Un triangle rouge apparaît dans la cellule que vous avez modifiée.
1. Cliquez sur **OK** pour enregistrer vos modifications.

### Suppression d’utilisateurs ou de groupes dans des groupes {#removing-users-or-groups-from-groups}

AEM propose trois manières de supprimer des utilisateurs, des utilisatrices ou des groupes d’un groupe :

* Lorsque vous vous trouvez dans le profil du groupe, vous pouvez supprimer des membres (utilisateurs, utilisatrices ou groupes).
* Lorsque vous vous trouvez dans le profil du membre, vous pouvez supprimer des membres des groupes.
* Lorsque vous travaillez sur des autorisations, vous pouvez supprimer des membres des groupes.

### Groupes - Suppression d’utilisateurs ou de groupes dans des groupes {#groups-removing-users-or-groups-from-groups}

Pour supprimer un compte d’utilisateur ou de groupe d’un groupe, procédez comme suit :

1. Double-cliquez sur le nom du groupe ou du compte d’utilisateur que vous souhaitez supprimer d’un groupe.
1. Cliquez sur l’onglet **Groupes**. Vous voyez à quels groupes le compte sélectionné appartient.
1. Dans le volet **Groupes**, cliquez sur le nom de l’utilisateur ou du groupe que vous souhaitez supprimer du groupe et cliquez sur **Supprimer**. (Si vous souhaitez supprimer plusieurs comptes, utilisez la combinaison Maj+clic ou Ctrl+clic sur ces noms et cliquez sur **Supprimer**.)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Membres - Suppression d’utilisateurs ou de groupes dans des groupes {#members-removing-users-or-groups-from-groups}

Pour supprimer des comptes d’un groupe, procédez comme suit :

1. Double-cliquez sur le nom du groupe dont vous souhaitez supprimer des membres.
1. Cliquez sur l’onglet **Membres**. Une liste des membres appartenant déjà à ce groupe s’affiche.
1. Dans le volet **Membres**, cliquez sur le nom du membre que vous souhaitez supprimer du groupe et cliquez sur **Supprimer**. (Si vous souhaitez supprimer plusieurs utilisateurs ou utilisatrices, utilisez la combinaison Maj+clic ou Ctrl+clic sur ces noms et cliquez sur **Supprimer**.)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Suppression d’utilisateurs ou de groupes lors de l’ajout d’autorisations {#removing-users-or-groups-while-adding-permissions}

Pour supprimer des membres d’un groupe dans un chemin d’accès spécifique, procédez comme suit :

1. Double-cliquez sur le nom du groupe ou de l’utilisateur dont vous souhaitez supprimer des utilisateurs.

1. Cliquez sur l’onglet **Autorisations**.

1. Accédez au chemin d’accès dont vous souhaitez supprimer les autorisations et cliquez sur **Détails**. La partie inférieure de la fenêtre des détails indique qui dispose d’autorisations pour cette page.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Dans la colonne **Membre**, cochez les cases des membres qui doivent disposer d’autorisations au niveau de ce chemin d’accès. Décochez les cases des membres dont vous souhaitez supprimer les autorisations. Un triangle rouge apparaît dans la cellule que vous avez modifiée.
1. Cliquez sur **OK** pour enregistrer vos modifications.

### Synchronisation des utilisateurs {#user-synchronization}

Lorsque le déploiement consiste en une [ferme de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), les utilisateurs, utilisatrices et les groupes doivent être synchronisés sur tous les nœuds de publication.

Pour en savoir plus sur la synchronisation des utilisateurs et utilisatrices, et son activation, voir [Synchronisation des utilisateurs](/help/sites-administering/sync.md).

## Gestion des autorisations {#managing-permissions}

>[!NOTE]
>
>Adobe a introduit une nouvelle vue principale basée sur l’interface utilisateur tactile pour la gestion des autorisations. Pour plus d’informations sur son utilisation, consultez [cette page](/help/sites-administering/touch-ui-principal-view.md).

Cette section décrit comment définir des autorisations, y compris des autorisations de réplication.

### Définition des autorisations {#setting-permissions}

Les autorisations permettent aux utilisateurs d’effectuer certaines opérations sur les ressources dans certains chemins d’accès. Elle offre également la possibilité de créer ou de supprimer des pages.

Pour ajouter, modifier ou supprimer des autorisations, procédez comme suit :

1. Dans la console **Sécurité**, double-cliquez sur le nom de l’utilisateur ou du groupe pour lequel vous souhaitez définir des autorisations ou [rechercher des nœuds](#searching-for-nodes).

1. Cliquez sur l’onglet **Autorisations**.

   ![cquserpermissions](assets/cquserpermissions.png)

1. Dans la grille d’arborescence, cochez une case pour autoriser l’utilisateur ou le groupe sélectionné à effectuer une action ou décochez une case pour interdire à l’utilisateur ou au groupe sélectionné d’effectuer une action. Pour plus d’informations, cliquez sur **Détails**.

1. Lorsque vous avez terminé, cliquez sur **Enregistrer**.

### Définition des droits de réplication {#setting-replication-privileges}

Le droit de réplication correspond au droit de publier du contenu, et peut être octroyé à des groupes, des utilisateurs et des utilisatrices.

>[!NOTE]
>
>* Tous les droits de réplication appliqués à un groupe s’appliquent à tous les utilisateurs et utilisatrices de ce groupe.
>* Les droits de réplication d’un utilisateur ou d’une utilisatrice remplacent les droits de réplication d’un groupe.
>* Les droits de réplication Autoriser ont une priorité supérieure aux droits de réplication Refuser. Consultez la section [Autorisations dans AEM](#permissions-in-aem) pour plus d’informations.
>

Pour définir les droits de réplication :

1. Sélectionnez l’utilisateur, l’utilisatrice ou le groupe dans la liste, double-cliquez pour l’ouvrir, puis cliquez sur **Autorisations**.
1. Dans la grille, accédez au chemin d’accès où vous souhaitez que l’utilisateur possède des autorisations de réplication ou [recherchez des nœuds](#searching-for-nodes).

1. Dans la colonne **Répliquer** du chemin d’accès sélectionné, cochez une case pour ajouter l’autorisation de réplication à cet utilisateur ou ce groupe ou décochez la case pour supprimer l’autorisation de réplication. AEM affiche un triangle rouge aux emplacements où vous avez apporté des modifications qui n’ont pas encore été enregistrées.

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Recherche de nœuds {#searching-for-nodes}

Lors de l’ajout ou de la suppression d’autorisations, vous pouvez parcourir ou rechercher le nœud.

Il existe deux types de recherche de chemin d’accès :

* Recherche de chemin d’accès – Si la chaîne de recherche commence par une « / », elle recherche les sous-nœuds directs du chemin d’accès donné :

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

Dans la zone de recherche, vous pouvez effectuer les opérations suivantes :

| Action | Effets |
|--- |--- |
| Touche fléchée à droite | Sélectionne un sous-nœud dans le résultat de la recherche. |
| Touche fléchée vers le bas | Redémarre la recherche. |
| Touche Entrée (Retour) | Sélectionne un sous-nœud et le charge dans la grille d’arborescence. |

* Recherche en texte intégral - Si la chaîne de recherche ne commence pas par le caractère « / », une recherche en texte intégral est effectuée sur tous les nœuds du chemin d’accès « /content ».

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

Pour effectuer une recherche sur les chemins d’accès ou le texte intégral, procédez comme suit :

1. Dans la console Sécurité, sélectionnez un utilisateur ou un groupe, puis cliquez sur l’onglet **Autorisations**.

1. Dans la zone de recherche, saisissez le terme à rechercher.

### Emprunt d’identités d’utilisateurs et d’utilisatrices {#impersonating-users}

Vous pouvez spécifier un ou plusieurs utilisateurs autorisés à emprunter l’identité de l’utilisateur actuel. Cela signifie qu’ils peuvent faire basculer les paramètres de leur compte vers ceux de l’utilisateur actuel ou utilisatrice actuelle et agir pour le compte de cet utilisateur ou de cette utilisatrice.

Utilisez cette fonction avec précaution, car elle peut autoriser des utilisateurs à exécuter des actions que leur propre compte d’utilisateur ne leur autorise pas. Lors de l’emprunt de l’identité d’un utilisateur ou d’une utilisatrice, les utilisateurs et les utilisatrices sont informés qu’ils ne sont pas connectés en tant qu’eux-mêmes.

Il existe différents scénarios dans lesquels vous pouvez utiliser cette fonctionnalité, notamment :

* Si vous êtes absent du bureau, vous pouvez laisser une autre personne emprunter votre identité en votre absence. Grâce à cette fonctionnalité, vous pouvez vous assurer que quelqu’un dispose de vos droits d’accès et que vous n’avez pas besoin de modifier un profil utilisateur ni de fournir votre mot de passe.
* Vous pouvez utiliser cette fonction à des fins de débogage. Par exemple, pour voir à quoi ressemble le site web pour un utilisateur disposant de droits d’accès restreints. En outre, si un utilisateur ou une utilisatrice se plaint de problèmes techniques, vous pouvez emprunter l’identité de cet utilisateur ou de cette utilisatrice pour diagnostiquer et résoudre le problème.

Pour emprunter l’identité d’un utilisateur existant ou d’une utilisatrice existante :

1. Dans l’arborescence, sélectionnez le nom de la personne à laquelle vous souhaitez affecter d’autres utilisateurs dont emprunter l’identité. Double-cliquez pour l’ouvrir.
1. Cliquez sur l’onglet **Emprunteurs d’identité**.
1. Cliquez sur l’utilisateur ou l’utilisatrice qui doit pouvoir emprunter l’identité de l’utilisateur ou de l’utilisatrice sélectionné. Faites glisser l’utilisateur ou l’utilisatrice (l’emprunteur d’identité) de la liste vers le volet Emprunter l’identité. Le nom apparaît dans la liste.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Cliquez sur **Enregistrer**.

### Définition des préférences d’utilisateur, d’utilisatrice et de groupe {#setting-user-and-group-preferences}

Pour définir les préférences de l’utilisateur, de l’utilisatrice et du groupe, notamment la langue, la gestion des fenêtres et les préférences de la barre d’outils :

1. Sélectionnez l’utilisateur, l’utilisatrice ou le groupe dont vous souhaitez modifier les préférences dans l’arborescence de gauche. Pour sélectionner plusieurs utilisateurs, utilisatrices ou groupes, utilisez les combinaisons Ctrl+clic ou Maj+clic sur vos sélections.
1. Cliquez sur l’onglet **Préférences**.

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. Apportez les modifications nécessaires aux préférences du groupe ou de l’utilisateur ou utilisatrice, puis cliquez sur **Enregistrer**.

### Configuration des utilisateurs et utilisatrices ou des administrateurs et administratrices pour avoir le droit de gérer d’autres utilisateurs ou utilisatrices {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

Pour attribuer à des utilisateurs ou administrateurs l’autorisation de supprimer/activer/désactiver d’autres utilisateurs :

1. Ajoutez au groupe d’administrateurs ou d’administratrices l’utilisateur ou l’utilisatrice qui doit recevoir le droit de gérer d’autres utilisateurs et utilisatrices et enregistrez vos modifications.

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. Dans l’onglet **Autorisations** de l’utilisateur, accédez au caractère « / » et, dans la colonne Répliquer, cochez la case pour autoriser la réplication au niveau de « / » et cliquez sur **Enregistrer**.

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   L’utilisateur ou utilisatrice sélectionné peut désormais désactiver, activer, supprimer et créer des utilisateurs et utilisatrices.

### Extension des privilèges au niveau d’un projet {#extending-privileges-on-a-project-level}

Si vous prévoyez d’implémenter des privilèges spécifiques à une application, les informations suivantes vous expliquent comment implémenter un privilège personnalisé et l’appliquer dans CQ :

L’autorisation de modification de la hiérarchie est couverte par une combinaison d’autorisations jcr. L’autorisation de réplication est nommée **crx:replicate** et est stockée/évaluée avec d’autres autorisations dans le référentiel jcr. Il n’est toutefois pas appliqué au niveau jcr.

La définition et l’enregistrement d’autorisations personnalisées font officiellement partie de l’[API Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/privilege.html) depuis la version 2.4 (voir aussi [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)). Des explications plus détaillées de ces usages sont offertes dans Gestion du contrôle d’accès JCR tel que défini dans le [JSR 283](https://jcp.org/en/jsr/detail?id=283) (section 16). En outre, l’API Jackrabbit définit quelques extensions.

Le mécanisme d’enregistrement des autorisations est reflété dans l’interface utilisateur sous **Configuration du référentiel**.

L’enregistrement de nouveaux privilèges (personnalisés) est lui-même protégé par un privilège intégré qui doit être accordé au niveau du référentiel. Dans JCR : charger « null » comme paramètre « absPath » dans l’API ac mgt, voir le jsr 333 pour plus de détails. Par défaut, le membre **admin** et tous les membres du groupe d’administrateurs disposent de cette autorisation.

>[!NOTE]
>
>Bien que l’implémentation se charge de valider et d’évaluer les autorisations personnalisées, elle ne peut les appliquer que si ces autorisations sont des agrégats d’autorisations intégrées.
