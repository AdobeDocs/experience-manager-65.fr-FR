---
title: Classifications Adobe
seo-title: Adobe Classifications
description: Découvrez Adobe Classifications.
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '600'
ht-degree: 100%

---

# Classifications Adobe{#adobe-classifications}

Adobe Classifications exporte les données de classification dans [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de façon planifiée. L’exportateur est une implémentation de **com.adobe.cq.scheduled.exporter.Exporter**.

Pour configurer cela :

1. Avec la **Navigation**, sélectionnez **Outils**, **Services cloud**, puis **Services cloud hérités**.
1. Faites défiler jusqu’à **Adobe Analytics** et sélectionnez **Afficher les configurations**.
1. Cliquez sur le lien **[+]** situé en regard de votre configuration Adobe Analytics.

1. Dans la boîte de dialogue **Créer une structure** :

   * Spécifiez un **Titre**.
   * Vous pouvez éventuellement spécifier le **Nom**, pour le nœud qui stocke les détails de la structure dans le référentiel.
   * Sélectionnez **Classifications Adobe Analytics**,

   puis cliquez sur **Créer**.

   ![Boîte de dialogue Créer un framework](assets/aa-25.png)

1. La boîte de dialogue **Paramètres des classifications** s’ouvre pour modification.

   ![Boîte de dialogue Paramètres des classifications](assets/aa-classifications-settings.png)

   Les propriétés sont par exemple les suivantes :

   | **Champ** | **Description** |
   |---|---|
   | Activé | Sélectionnez **Oui** pour activer les paramètres d’Adobe Classifications. |
   | Remplacer en cas de conflit | Sélectionnez **Oui** pour remplacer toute collision de données. Par défaut, cette option est définie sur **Non**. |
   | Suppression traitée | Si elle est définie sur **Oui**, supprime les nœuds traités après leur exportation. La valeur par défaut est **Faux**. |
   | Description de la tâche d’exportation | Saisissez une description pour la tâche d’Adobe Classifications. |
   | Message de notification | Saisissez une adresse e-mail qui recevra la notification d’Adobe Classifications. |
   | Suite de rapports | Saisissez la suite de rapports pour laquelle exécuter la tâche d’importation. |
   | Ensemble de données | Saisissez l’ID de relation de l’ensemble de données pour lequel exécuter la tâche d’importation. |
   | Transformateur | Dans le menu déroulant, sélectionnez une mise en œuvre de transformateur. |
   | Source de données | Accédez au chemin du conteneur de données. |
   | Planification de l’exportation | Sélectionnez la planification pour l’exportation. Par défaut, elle a lieu toutes les 30 minutes. |

1. Cliquez sur **OK** pour enregistrer vos paramètres.

## Modification de la taille des pages {#modifying-page-size}

Les enregistrements sont traités par pages. Par défaut, Adobe Classifications crée des pages avec une taille de page de 1 000.

Une page peut présenter une taille maximale de 25 000, par définition dans Adobe Classifications, et peut être modifiée à partir de la console Felix. Pendant l’exportation, Adobe Classifications verrouille le nœud source pour empêcher les modifications simultanées. Le nœud est déverrouillé après l’exportation, en cas d’erreur, ou lorsque la session est fermée.

Pour modifier la taille de page :

1. Accédez à la console OSGi sur **https://&lt;hôte>:&lt;port>/system/console/configMgr** et sélectionnez **Adobe AEM Classifications Exporter**.

   ![aa-26](assets/aa-26.png)

1. Mettez à jour **Export Page Size** (Exporter la taille de page) selon les besoins, puis cliquez sur **Save** (Enregistrer).

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Auparavant, Adobe Classifications était appelé exportateur SAINT.

Un exportateur peut utiliser un transformateur pour transformer les données d’exportation vers un format spécifique. Pour Adobe Classifications, une sous-interface `SAINTTransformer<String[]>` mettant en œuvre l’interface de transformateur est fournie. Cette interface est utilisée pour limiter le type de données à `String[]`, qui est utilisé par l’API SAINT et pour disposer d’une interface de marquage permettant de rechercher ces services à sélectionner.

Dans la mise en œuvre par défaut SAINTDefaultTransformer, les ressources enfants de la source de l’exportateur sont traitées comme des enregistrements avec des noms de propriétés comme clés, et des valeurs de propriétés comme valeurs. La colonne **Clé** est automatiquement ajoutée en tant que première colonne ; sa valeur est le nom du nœud. Les propriétés de nom d’espaces (contenant `:`) sont ignorées.

*Structure de nœud :*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (chaîne)
      * Price = 120.90 (chaîne)
      * Size = M (chaîne)
      * Color = black (chaîne)
      * Color^Code = 101 (chaîne)

**En-tête et enregistrement SAINT :**

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
   <td>transformer</td>
   <td>Nom de classe d’une mise en œuvre SAINTTransformer</td>
  </tr>
  <tr>
   <td>email</td>
   <td>Adresse e-mail des notifications.</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>Les ID des suites de rapports pour lesquelles exécuter la tâche d’importation. </td>
  </tr>
  <tr>
   <td>dataset</td>
   <td>ID de relation de l’ensemble de données pour lequel exécuter la tâche d’importation. </td>
  </tr>
  <tr>
   <td>description</td>
   <td>Description de la tâche. <br /> </td>
  </tr>
  <tr>
   <td>overwrite</td>
   <td>Indicateur pour remplacer les collisions de données. La valeur par défaut est <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>checkdivisions</td>
   <td>Indicateur pour vérifier la compatibilité des suites de rapports. La valeur par défaut est <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Indicateur pour supprimer les nœuds traités après l’exportation. La valeur par défaut est <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatisation de l’exportation d’Adobe Classifications {#automating-adobe-classifications-export}

Vous pouvez créer votre propre workflow, de sorte que toutes les nouvelles importations le lancent afin de créer les données appropriées et structurées dans **/var/export/** pour qu’elles puissent être exportées dans Adobe Classifications.
