---
title: Classifications Adobe
description: Découvrez comment utiliser les classifications Adobe pour exporter des données de classification vers Adobe Analytics.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 100%

---

# Classifications Adobe{#adobe-classifications}

Adobe Classifications exporte les données de classification dans [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de façon planifiée. L’exportateur est une implémentation de **com.adobe.cq.scheduled.Export.Exporter**.

Pour le configurer, procédez comme suit :

1. Avec la **Navigation**, sélectionnez **Outils**, **Services cloud**, puis **Services cloud hérités**.
1. Faites défiler jusqu’à **Adobe Analytics** et sélectionnez **Afficher les configurations**.
1. Cliquez sur le lien **[+]** situé en regard de votre configuration Adobe Analytics.

1. Dans la boîte de dialogue **Créer un framework** :

   * Spécifiez un **Titre**.
   * Il est possible de spécifier le **Nom** pour le nœud qui stocke les détails du framework dans le référentiel.
   * Sélectionnez **Classifications Adobe Analytics**,

   puis cliquez sur **Créer**.

   ![Boîte de dialogue Créer un framework](assets/aa-25.png)

1. La boîte de dialogue **Paramètres des classifications** s’ouvre pour modification.

   ![Boîte de dialogue Paramètres des classifications](assets/aa-classifications-settings.png)

   Les propriétés sont par exemple les suivantes :

   | **Champ** | **Description** |
   |---|---|
   | Activé | Sélectionnez **Oui** pour activer les paramètres des classifications Adobe. |
   | Remplacer en cas de conflit | Sélectionnez **Oui** pour remplacer toute collision de données. Par défaut, cette option est définie sur **Non**. |
   | Suppression traitée | Si cette option est définie sur **Oui**, elle supprime les nœuds traités après avoir été exportés. La valeur par défaut est **False**. |
   | Description de la tâche d’exportation | Saisissez une description pour la tâche des classifications Adobe. |
   | Message de notification | Saisissez une adresse e-mail qui recevra la notification d’Adobe Classifications. |
   | Suite de rapports | Saisissez la suite de rapports pour laquelle exécuter la tâche d’importation. |
   | Ensemble de données | Saisissez l’identifiant de relation du jeu de données pour lequel exécuter la tâche d’importation. |
   | Transformateur | Dans le menu déroulant, sélectionnez une implémentation de transformateur. |
   | Source de données | Accédez au chemin d’accès du conteneur de données. |
   | Planification de l’exportation | Sélectionnez le planning pour l’exportation. La valeur par défaut est toutes les 30 minutes. |

1. Cliquez sur **OK** pour enregistrer vos paramètres.

## Modification du format de page {#modifying-page-size}

Les enregistrements sont traités par pages. Par défaut, Adobe Classifications crée des pages avec une taille de page de 1 000.

Une page peut présenter une taille maximale de 25 000, par définition dans Adobe Classifications, et peut être modifiée à partir de la console Felix. Pendant l’exportation, Adobe Classifications verrouille le nœud source pour empêcher les modifications simultanées. Le nœud est déverrouillé après l’exportation, en cas d’erreur ou lorsque la session est fermée.

Pour modifier le format de page :

1. Accédez à la console OSGi sur **https://&lt;hôte>:&lt;port>/system/console/configMgr** et sélectionnez **Adobe AEM Classifications Exporter**.

   ![aa-26](assets/aa-26.png)

1. Mettez à jour la **taille de page d’exportation** selon les besoins, puis cliquez sur **Enregistrer**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Les classifications Adobe étaient auparavant connues sous le nom d’exportateur SAINT.

Un exportateur peut utiliser un transformateur pour transformer les données d’exportation vers un format spécifique. Pour Adobe Classifications, une sous-interface `SAINTTransformer<String[]>` mettant en œuvre l’interface de transformateur est fournie. Cette interface est utilisée pour limiter le type de données à `String[]`, qui est utilisé par l’API SAINT et pour disposer d’une interface de marquage permettant de rechercher ces services à sélectionner.

Dans la mise en œuvre par défaut SAINTDefaultTransformer, les ressources enfants de la source de l’exportateur sont traitées comme des enregistrements avec des noms de propriétés comme clés, et des valeurs de propriétés comme valeurs. La colonne **Clé** est automatiquement ajoutée en tant que première colonne ; sa valeur est le nom du nœud. Les propriétés d’espace de noms (contenant `:`) sont ignorées.

*Structure de nœud :*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Produit = Mon nom de produit (chaîne)
      * Prix = 120,90 (chaîne)
      * Taille = M (chaîne)
      * Couleur = noir (chaîne)
      * Code couleur = 101 (chaîne)

**En-tête et enregistrement de SAINT :**

| **Clé** | **Produit** | **Prix** | **Taille** | **Couleur** | **Code Couleur** |
|---|---|---|---|---|---|
| 1 | Mon nom de produit | 120,90 | M | noir | 101 |

Les propriétés sont par exemple les suivantes :

<table>
 <tbody>
  <tr>
   <td><strong>Chemin de la propriété</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>transformateur</td>
   <td>Nom de classe d’une implémentation SAINTTransformer.</td>
  </tr>
  <tr>
   <td>email</td>
   <td>Adresse e-mail de notification.</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>Identifiants des suites de rapports pour lesquelles exécuter la tâche d’importation. </td>
  </tr>
  <tr>
   <td>dataset</td>
   <td>Identifiant de relation du jeu de données pour lequel exécuter la tâche d’importation. </td>
  </tr>
  <tr>
   <td>description</td>
   <td>Description de la tâche. <br /> </td>
  </tr>
  <tr>
   <td>overwrite</td>
   <td>Indicateur pour remplacer les collisions de données. La valeur par défaut est <strong>False</strong>.</td>
  </tr>
  <tr>
   <td>checkdivisions</td>
   <td>Indicateur pour vérifier la compatibilité des suites de rapports. La valeur par défaut est <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Indicateur pour supprimer les nœuds traités après l’exportation. Par défaut : <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatisation de l’export des classifications Adobe {#automating-adobe-classifications-export}

Vous pouvez créer votre propre workflow, de sorte que tout nouvel import lance le workflow pour créer les données appropriées et correctement structurées dans **/var/export/**, afin qu’il puisse être exporté vers les classifications Adobe.
