---
title: Que sont les fragments de formulaire adaptatif ?
description: Les formulaires adaptatifs fournissent un mécanisme permettant de créer un segment de formulaire, tel qu’un panneau ou un groupe de champs, utilisable dans tout formulaire adaptatif. Vous pouvez également enregistrer un panneau existant en tant que fragment.
topic-tags: author
keywords: Ajouter des fragments de formulaire adaptatif, des fragments de formulaire adaptatif, Créer un fragment de formulaire, Ajouter un fragment à un formulaire adaptatif, Gérer des fragments
feature: Adaptive Forms, Core Components
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 35%

---

# Création et utilisation de fragments de Forms adaptatifs dans un formulaire adaptatif en fonction des composants principaux {#adaptive-form-fragments}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM 6.5 | Cet article |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html?lang=fr) |

Bien que chaque formulaire soit conçu à des fins spécifiques, certains segments sont communs à la plupart des formulaires, comme pour fournir des détails personnels tels que le nom et l’adresse, les détails de famille et les informations sur les revenus. Les personnes qui developpent des formulaire doivent créer ces segments communs à chaque fois qu’un formulaire est créé.

Les formulaires adaptatifs fournissent un mécanisme pratique pour créer un segment de formulaire, comme un panneau ou un groupe de champs, une seule fois et pour les réutiliser dans des formulaires adaptatifs. Ces segments réutilisables et autonomes sont appelés fragments de formulaire adaptatif.

Les fragments de formulaire s’intègrent facilement à plusieurs formulaires, ce qui simplifie la création de formulaires cohérents et d’apparence professionnelle. Les fragments de formulaire assurent la réutilisation, la normalisation et la cohérence de la marque grâce à la fonctionnalité &quot;changer une fois et refléter partout&quot;. Expérimentez une plus grande maintenabilité et une plus grande efficacité, car les mises à jour effectuées à un emplacement donné sont automatiquement propagées à tous les formulaires qui utilisent ces fragments.

Vous pouvez ajouter un fragment plusieurs fois à un document et utiliser les propriétés de liaison de données de ses composants pour le lier à différentes sources de données ou à différents schémas. Par exemple, vous pouvez utiliser le même fragment d’adresse pour les adresses permanentes, de communication et de facturation et le connecter à différents champs d’une source de données ou d’un schéma.

>[!NOTE]
>
> Vous pouvez facilement personnaliser votre expérience de fragment pour les utilisateurs qui utilisent le [Boîte de dialogue de configuration et boîte de dialogue de conception du composant Fragment de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-fragment.html).


## Création d’un fragment de formulaire {#create-a-fragment}

Vous pouvez créer entièrement un fragment de formulaire adaptatif ou enregistrer un panneau dans un formulaire adaptatif existant en tant que fragment. Pour créer un fragment de formulaire :

1. Connectez-vous à votre instance AEM Forms à l’adresse https://[*hostname*]:[*port*]/aem/forms.html.
1. Cliquez sur **Créer > Fragment de formulaire adaptatif**.
1. Indiquez le titre, le nom, la description et les balises du fragment. Assurez-vous de spécifier un nom unique pour le fragment. Si un autre fragment portant le même nom existe, la création du fragment échoue.
1. Sélectionnez un modèle de formulaire. Vous pouvez créer un fragment de formulaire pour le Forms adaptatif basé sur les composants principaux ou le Forms adaptatif basé sur les composants de base.
   * Pour créer un fragment de formulaire pour les formulaires basés sur les composants principaux, sélectionnez un modèle basé sur les composants principaux.
   * Pour créer un fragment de formulaire pour les formulaires basés sur des composants de base, sélectionnez un modèle de composants de base. Par exemple, /libs/fd/af/templateForFragment/defaultFragmentTemplate.

   Lorsque vous créez un fragment de formulaire pour les formulaires basés sur les composants principaux, utilisez l’option Sélectionner le thème de formulaire pour sélectionner un thème basé sur les composants principaux.

1. Cliquez pour ouvrir l’onglet **Modèle de formulaire**, puis dans le menu déroulant **Choisir parmi**, sélectionnez l’un des modèles de fragment suivants :

   ![Affiche le type de modèle dans l’onglet Modèle de formulaire.](assets/create-af-1-1.png)

   * **Aucun** : indique que le fragment doit être créé de zéro sans utiliser de modèle de formulaire.

     >[!NOTE]
     >
     > Dans Adaptive Forms, vous pouvez utiliser plusieurs fois un fragment de formulaire unique (basé sur les composants principaux). Il prend en charge les fragments de formulaire basés sur des schémas et sur des éléments non basés sur des schémas.

   * **Schéma**: indique de créer le fragment à l’aide d’un schéma XML ou JSON téléchargé dans AEM Forms. Vous pouvez charger ou sélectionner dans les schémas XML ou JSON disponibles comme modèle de formulaire pour le fragment. Lorsque vous sélectionnez un schéma XML, vous pouvez également créer un fragment de formulaire adaptatif en sélectionnant un type complexe présent dans le schéma sélectionné à partir de la propriété **[!UICONTROL Type complexe de schéma XML]** menu déroulant. Lorsque vous sélectionnez un schéma JSON, vous pouvez également créer un fragment de formulaire adaptatif en sélectionnant une définition de schéma présente dans le schéma sélectionné à partir du **[!UICONTROL Définitions de schéma JSON]** menu déroulant.
   * **Modèle de données de formulaire**: indique de créer le fragment à l’aide d’un modèle de données de formulaire. Vous pouvez créer un fragment de formulaire adaptatif basé sur un seul objet de modèle de données dans un modèle de données de formulaire. Développez la liste déroulante Définitions de modèle de données de formulaire . Elle répertorie tous les objets de modèle de données dans le modèle de données de formulaire spécifié. Sélectionnez un objet de modèle de données dans la liste.

   ![Modèle de données de formulaire](assets/create-af-3.png)



1. Cliquez sur **Créer** puis cliquez sur **Ouvrir** pour ouvrir le fragment, avec un modèle par défaut, en mode d’édition. En mode d’édition, vous pouvez ajouter n’importe quel composant de formulaire adaptatif au fragment.

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> En outre, si vous avez sélectionné un modèle de schéma XML ou de formulaire XDP comme modèle de formulaire pour votre fragment, un nouvel onglet affichant la hiérarchie des modèles de formulaire apparaît dans l’outil de recherche de contenu. Il vous permet de faire glisser des éléments du modèle de formulaire sur le fragment. Les éléments de modèle de formulaire ajoutés sont convertis en composants de formulaire tout en conservant les propriétés d’origine du modèle XDP ou XSD associé.

Une fois le fragment de formulaire adaptatif basé sur un schéma ou un modèle de données de formulaire créé, les éléments de modèle de données de formulaire ou de schéma apparaissent dans l’onglet Sources de données du navigateur de contenu de l’éditeur de formulaire adaptatif. Vous pouvez faire glisser des éléments de modèle de formulaire sur le fragment. Les éléments de modèle de formulaire ajoutés sont convertis en composants de formulaire tout en conservant les propriétés d’origine du schéma associé.


## Ajout d’un fragment à un formulaire adaptatif {#insert-a-fragment-in-an-adaptive-form}

Pour ajouter un fragment de formulaire adaptatif à un formulaire adaptatif :

1. Ouvrez le formulaire adaptatif en mode d’édition.
1. Ajoutez la variable **fragment de formulaire adaptatif** du formulaire.
1. Cliquez sur le bouton **Ressources** navigateur de contenu dans la barre latérale. Dans l’explorateur de ressources, sous les chemins d’accès, sélectionnez l’option **Fragments de formulaire adaptatif** . Tous les fragments de Forms adaptatif disponibles pour votre formulaire, selon le modèle du formulaire, s’affichent.

   ![sélectionnez l’option Fragments de formulaire adaptatif .](assets/adaptive-forms-fragments.png)

1. Faites glisser un fragment de formulaire adaptatif sur le **fragment de formulaire adaptatif** sur votre formulaire adaptatif.

   >[!NOTE]
   >
   >Le fragment de formulaire adaptatif n’est pas activé pour la création dans le formulaire adaptatif. De plus, vous ne pouvez pas utiliser un fragment basé sur XSD dans un formulaire adaptatif basé sur JSON et inversement.

Le fragment de formulaire adaptatif est ajouté par référence au formulaire adaptatif et reste synchronisé avec le fragment autonome de formulaire adaptatif. Cela signifie que toutes les modifications apportées au fragment de formulaire adaptatif sont répercutées dans toutes les instances où le fragment est incorporé dans le Forms adaptatif.

### Incorporation d’un fragment dans un formulaire adaptatif {#embed-a-fragment-in-adaptive-form}

Vous pouvez choisir d’incorporer un fragment de formulaire adaptatif en cliquant sur le bouton ![Incorporer](assets/Smock_Import_18_N.svg) dans la barre d’outils du panneau du fragment ajouté.

Le fragment inclus n’est plus lié au fragment autonome. Vous pouvez modifier les composants dans le fragment inclus à partir du formulaire adaptatif.

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### Utilisation de fragments dans les fragments {#using-fragments-within-fragments}

Vous pouvez créer des fragments de formulaire adaptatif imbriqués, ce qui signifie que vous pouvez faire glisser un fragment dans un autre fragment et avoir une structure de fragment imbriqué.

### Utilisation d’un fragment de formulaire plusieurs fois dans un formulaire adaptatif {#using-form-fragment-mutiple-times-in-af}

Vous pouvez utiliser plusieurs fois un fragment de formulaire basé sur un schéma et sur aucun modèle dans un formulaire adaptatif pour enregistrer les données de manière unique pour chaque champ de fragment de formulaire. Par exemple, vous pouvez utiliser un fragment de formulaire d’adresse pour collecter les détails des adresses pour les adresses permanentes, les communications et les adresses actives présentes dans un formulaire de demande de prêt.

![utilisation de plusieurs fragments dans un formulaire adaptatif](assets/using-multiple-fragment-af.gif)

## Correspondance automatique des fragments pour la liaison de données {#auto-mapping-of-fragments-for-data-binding}

Lorsque vous créez un fragment de formulaire adaptatif à l’aide d’un modèle de formulaire XFA ou d’un type complexe XSD et que vous le faites glisser vers un formulaire adaptatif, le fragment XFA ou le type complexe XSD est automatiquement remplacé par le fragment de formulaire adaptatif correspondant dont la racine de modèle de fragment est mappée au fragment XFA ou au type complexe XSD.

Vous pouvez modifier la ressource de fragment et ses liaisons dans la boîte de dialogue Modifier le composant.

Vous pouvez également faire glisser et déposer un fragment de formulaire adaptatif lié à partir de la bibliothèque de fragments de formulaire adaptatif dans AEM Content Finder et fournir la référence de liaison correcte à partir de la boîte de dialogue Modifier le composant du panneau Fragment de formulaire adaptatif.

## Gestion des fragments {#manage-fragments}

Vous pouvez effectuer plusieurs opérations sur des fragments de formulaire adaptatif à l’aide de l’interface utilisateur d’AEM Forms.

1. Accédez à `https://[hostname]/aem/forms.html`.

1. Cliquez sur **Sélectionner** dans la barre d’outils de l’interface utilisateur d’AEM Forms et sélectionnez un fragment de formulaire adaptatif. La barre d’outils affiche les opérations suivantes que vous pouvez effectuer sur le fragment de formulaire adaptatif sélectionné.

<table>
 <tbody>
  <tr>
   <td><p><strong>Opération</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modifier</p> </td>
   <td><p>Ouvre le fragment de formulaire adaptatif sélectionné en mode d’édition.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Propriétés</p> </td>
   <td><p>Ouvre le panneau Propriétés. Dans le panneau Propriétés, vous pouvez afficher et modifier les propriétés, générer un aperçu et charger une miniature pour le fragment sélectionné. Pour plus d’informations, consultez la section <a>Gestion des métadonnées</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copier</p> </td>
   <td><p>Copie le fragment sélectionné. Le bouton Coller s’affiche dans la barre d’outils.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Télécharger</p> </td>
   <td><p>Télécharge le fragment sélectionné.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Aperçu</p> </td>
   <td><p>Fournit des options de prévisualisation du fragment en HTML ou un aperçu personnalisé en fusionnant les données d’un fichier XML avec le fragment. Pour plus d’informations, voir <a>Aperçu d’un formulaire</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Démarrage de la révision/Gestion de la révision</p> </td>
   <td><p>Permet de lancer et de gérer la révision du fragment sélectionné. Pour plus d’informations, voir <a>Créer et gérer des révisions</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Ajouter un dictionnaire</p> </td>
   <td><p>Génère un dictionnaire pour localiser le fragment sélectionné. Pour plus d’informations, voir <a>Localisation d’Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publier/Dépublier</p> </td>
   <td><p>Publie/annule la publication du fragment sélectionné.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Supprimer</p> </td>
   <td><p>Supprime le fragment sélectionné.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Points essentiels à respecter lorsque vous utilisez des fragments {#key-points-to-remember-when-working-with-fragments}

* Assurez-vous que le nom du fragment est unique. La création du fragment échoue si un fragment portant le même nom existe déjà.
* Dans un formulaire adaptatif basé sur XDP, si vous enregistrez un panneau en tant que fragment contenant une autre partie du fragment XDP, le fragment obtenu est automatiquement lié au fragment XDP enfant. Si un formulaire adaptatif basé sur un schéma XSD, le fragment obtenu est lié à la racine du schéma.
* Lorsque vous créez un fragment de formulaire adaptatif, un noeud de fragment est créé, similaire au noeud guideContainer pour un formulaire adaptatif, dans CRXDE Lite.
* Un fragment d’un formulaire adaptatif qui utilise un modèle de données de formulaire différent n’est pas pris en charge. Par exemple, un fragment basé sur XDP n’est pas pris en charge dans un formulaire adaptatif basé sur XSD et inversement.
* Les fragments de formulaire adaptatif peuvent être utilisés via l’onglet Fragments de formulaire adaptatif de l’outil de recherche de contenu d’AEM.
* Toute expression, script ou style d’un fragment de formulaire adaptatif autonome est conservé lorsqu’il est inséré par référence ou incorporé dans un formulaire adaptatif.
* Vous ne pouvez pas modifier un fragment de formulaire adaptatif inséré par référence dans un formulaire adaptatif. Pour le modifier, vous modifiez le fragment Formulaire adaptatif autonome ou vous incorporez le fragment dans le formulaire adaptatif.
* Lorsque vous publiez un formulaire adaptatif, vous devez publier les fragments de formulaire adaptatif autonomes insérés par référence dans le formulaire adaptatif.
* Lorsque vous republiez un fragment de formulaire adaptatif mis à jour, les modifications sont répercutées dans les instances publiées du formulaire adaptatif dans lequel le fragment est utilisé.
* Le formulaire adaptatif contenant le composant Vérifier ne prend pas en charge les utilisateurs anonymes. En outre, il n’est pas recommandé d’utiliser le composant Vérifier dans un fragment de formulaire adaptatif.
* (**Mac uniquement**) Pour vous assurer que la fonctionnalité des fragments de formulaire fonctionne parfaitement dans tous les scénarios, ajoutez l’entrée suivante au fichier /private/etc/hosts :
  `127.0.0.1 <Host machine>` **Ordinateur hôte** : ordinateur Apple Mac sur lequel AEM Forms est déployé.

## Fragments de référence {#reference-fragments}

Référencer des fragments de formulaire adaptatif que vous pouvez utiliser pour créer votre formulaire.
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->

## Voir également {#see-also}

* [Créer un formulaire adaptatif basé sur des composants principaux](create-an-adaptive-form-core-components.md)
* [Utiliser l’éditeur de règles pour ajouter un comportement dynamique au formulaire](rule-editor.md)
* [Créer ou personnaliser des thèmes pour les formulaires adaptatifs basés sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Création d’un modèle pour les formulaires adaptatifs basés sur les composants principaux](template-editor.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Exemples de modèles de thèmes et de modèles de données de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=fr)