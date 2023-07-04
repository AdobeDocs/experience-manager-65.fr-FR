---
title: Affichage principal de la gestion des autorisations
seo-title: Principal View for Permissions Management
description: Découvrez la nouvelle interface de l’interface utilisateur tactile qui facilite la gestion des autorisations.
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: 7803f1df1e05dc838cb458026f8dbd27de9cb924
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 40%

---

# Affichage principal de la gestion des autorisations{#principal-view-for-permissions-management}

## Présentation {#overview}

AEM 6.5 introduit la gestion des autorisations pour les utilisateurs et pour les groupes. La fonctionnalité principale reste la même que celle de l’interface utilisateur classique, mais celle-ci est plus efficace et conviviale.

## Utilisation {#how-to-use}

### Accès à l’interface utilisateur {#accessing-the-ui}

La nouvelle gestion des autorisations basée sur l’interface utilisateur est accessible via la carte Autorisations sous Sécurité , comme illustré ci-dessous :

![Interface utilisateur de gestion des autorisations](assets/screen_shot_2019-03-17at63333pm.png)

Le nouvel affichage facilite la consultation de l’ensemble des privilèges et restrictions pour un principal donné pour tous les chemins d’accès pour lesquels les autorisations ont été accordées explicitement. Cela supprime la nécessité d’accéder à

CRXDE pour gérer les privilèges et les restrictions avancés. L’affichage a été fusionné. La vue est définie par défaut sur Groupe &quot;tout le monde&quot;.

![Vue du groupe &quot;tout le monde&quot;](assets/unu-1.png)

Il existe un filtre qui permet à l’utilisateur de sélectionner le type d’entités à examiner. **Utilisateurs**, **Groupes** ou **Tous** et rechercher n’importe quelle entité&#x200B;**.**

![Recherche de types d’entités principales](assets/image2019-3-20_23-52-51.png)

### Affichage des autorisations pour un entité de sécurité {#viewing-permissions-for-a-principal}

Le cadre de gauche permet aux utilisateurs de faire défiler l’écran vers le bas pour trouver l’entité principale ou rechercher un Groupe ou un Utilisateur en fonction du filtre sélectionné, comme illustré ci-dessous :

![Affichage des autorisations pour un entité de sécurité](assets/doi-1.png)

Cliquez sur le nom pour afficher les autorisations attribuées sur la droite. Le volet Autorisations affiche la liste des entrées de contrôle d’accès sur des chemins spécifiques, ainsi que les restrictions configurées.

![Afficher la liste ACL](assets/trei-1.png)

### Ajout d’une nouvelle entrée de contrôle d’accès pour une entité de sécurité {#adding-new-access-control-entry-for-a-principal}

De nouvelles autorisations peuvent être ajoutées en ajoutant une nouvelle entrée de contrôle d’accès en cliquant sur le bouton Ajouter ACE .

![Ajout d’une liste de contrôle d’accès pour un principal](assets/patru.png)

La fenêtre ci-dessous apparaît alors. L’étape suivante consiste à choisir le chemin d’accès pour lequel l’autorisation doit être configurée.

![Configuration du chemin d’accès aux autorisations](assets/cinci-1.png)

Sur cet exemple, nous sélectionnons un chemin pour lequel configurer une autorisation pour les **dam-users** :

![Exemple de configuration pour dam-users](assets/sase-1.png)

Une fois le chemin sélectionné, le workflow revient sur l’écran depuis lequel un ou plusieurs privilèges peuvent être sélectionnés parmi les espaces de noms disponibles (comme `jcr`, `rep` ou `crx`), comme indiqué ci-dessous.

Vous pouvez ajouter des privilèges en effectuant une recherche à partir du champ de texte, puis en effectuant une sélection dans la liste.

>[!NOTE]
>
>Pour obtenir la liste complète des privilèges et descriptions, reportez-vous à la section [cette page](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![Permission de recherche d’un chemin donné](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Une fois la liste des privilèges sélectionnée, l’utilisateur peut choisir le Type d’autorisation : Refuser ou autoriser, comme illustré ci-dessous.

![Sélectionner l’autorisation](assets/screen_shot_2019-03-17at63938pm.png) ![Sélectionner l’autorisation](assets/screen_shot_2019-03-17at63947pm.png)

### Utilisation des restrictions {#using-restrictions}

Outre la liste des privilèges et le type d’autorisation sur un chemin donné, cet écran permet également d’ajouter des restrictions pour un contrôle d’accès affiné, comme illustré ci-dessous :

![Ajout de restrictions](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Pour plus d’informations sur la signification de chaque restriction, consultez la [Documentation Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

Vous pouvez ajouter des restrictions comme illustré ci-dessous en choisissant le type de restriction, en entrant la valeur et en appuyant sur la variable **+** icône .

![Ajouter le type de restriction](assets/sapte-1.png) ![Ajouter le type de restriction](assets/opt-1.png)

La nouvelle entrée de contrôle d’accès est reflétée dans la liste de contrôle d’accès, comme illustré ci-dessous. Notez que `jcr:write` est une autorisation agrégée qui inclut `jcr:removeNode`, qui a été ajouté précédemment, mais qui n’apparaît pas ci-dessous, car il se trouve sous `jcr:write`.

### Modification des ACE {#editing-aces}

Les entrées de contrôle d’accès peuvent être modifiées en sélectionnant une entité et en choisissant l’entrée de contrôle d’accès que vous souhaitez modifier.

Par exemple, ici, nous pouvons modifier l’entrée ci-dessous pour **dam-users** en cliquant sur l’icône en forme de crayon à droite :

![Ajouter une restriction](assets/image2019-3-21_0-35-39.png)

Les entrées de contrôle d’accès configurées présélectionnées apparaissent sur l’écran de modification. Il est possible de les supprimer en cliquant sur la croix située en regard de celles-ci ou d’ajouter de nouvelles autorisations pour le chemin donné, comme illustré ci-dessous.

![Modifier l’entrée](assets/noua-1.png)

Ici, nous ajoutons l’autorisation `addChildNodes` pour les **dam-users** sur le chemin donné.

![Ajout d’un privilège](assets/image2019-3-21_0-45-35.png)

Les modifications peuvent être enregistrées en cliquant sur le bouton **Enregistrer** en haut à droite, et les modifications seront répercutées dans les nouvelles autorisations pour **dam-users** comme illustré ci-dessous :

![Enregistrez les modifications](assets/zece-1.png)

### Suppression des ACE {#deleting-aces}

Vous pouvez supprimer des entrées de contrôle d’accès pour supprimer l’ensemble des autorisations accordées à un principal sur un chemin spécifique. L’icône X en regard de ACE peut être utilisée pour la supprimer, comme illustré ci-dessous :

![Suppression d’ACE](assets/image2019-3-21_0-53-19.png) ![Suppression d’ACE](assets/unspe.png)

### Combinaisons de privilèges de l’interface utilisateur classique {#classic-ui-privilege-combinations}

Notez que la nouvelle interface utilisateur des autorisations utilise explicitement l’ensemble de base de privilèges au lieu de combinaisons prédéfinies qui ne reflétaient pas vraiment les privilèges sous-jacents exacts qui ont été accordés.

Ceci entraînait une certaine confusion quant à la configuration exacte. Le tableau suivant répertorie le mappage entre les combinaisons de privilèges de l’interface utilisateur classique et les privilèges réels qui les constituent :

<table>
 <tbody>
  <tr>
   <th>Combinaisons de privilèges de l’interface utilisateur classique</th>
   <th>Privilège de l’interface utilisateur Autorisations</th>
  </tr>
  <tr>
   <td>Lecture</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modification</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Créer</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Supprimer</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Lecture de l’ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Modification de l’ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Réplication</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
