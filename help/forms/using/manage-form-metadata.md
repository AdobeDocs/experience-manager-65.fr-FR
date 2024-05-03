---
title: Gérer les métadonnées de formulaire
description: Les métadonnées permettent de catégoriser et d’organiser plus facilement les ressources. Les utilisateurs peuvent ainsi retrouver aisément une ressource spécifique.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 100%

---

# Gérer les métadonnées de formulaire{#manage-form-metadata}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/manage-form-metadata.html?lang=fr) |
| AEM 6.5 | Cet article |

## Présentation  {#overview-nbsp}

Les métadonnées permettent de catégoriser et d’organiser plus facilement les ressources. Les utilisateurs peuvent ainsi retrouver aisément une ressource spécifique.

Par défaut, AEM Forms fournit un ensemble défini de métadonnées pour chaque type de ressource. En plus des métadonnées par défaut, vous pouvez ajouter des métadonnées personnalisées à chaque type de ressources. AEM Forms permet également de créer, gérer et d’échanger efficacement toutes ces métadonnées pour vos formulaires.

Si vous êtes développeur ou développeuse, ou propriétaire d’un site, vous pouvez personnaliser Portail Formulaires, l’interface utilisateur d’AEM Forms pour refléter les métadonnées que vous utilisez dans votre entreprise. Pour plus d’informations sur Forms Portal, reportez-vous à la section [Présentation de la publication de formulaires sur un portail](../../forms/using/introduction-publishing-forms.md).

## Métadonnées dans AEM Forms {#metadata-in-aem-forms}

Dans AEM Forms, la liste des propriétés de métadonnées associées à une ressource dépend du type de cette dernière. En outre, si vous ajoutez une propriété de métadonnées personnalisée, celle-ci est ajoutée pour toutes les ressources du même type.

### Types de ressources {#asset-types}

Les types de ressources suivants sont pris en charge dans les AEM Forms :

* Modèles de formulaire (formulaires XFA)
* Formulaires PDF
* Document (PDF plats)
* Formulaires adaptatifs
* Ressources
* XFS

#### Liste exhaustive des métadonnées {#extensive-list-of-metadata}

Vous trouverez ci-dessous une liste exhaustive des propriétés de métadonnées prises en charge dans AEM Forms :

<table>
 <tbody> 
  <tr> 
   <td><strong>Nom de la propriété</strong></td> 
   <td><strong>Type de ressource</strong></td> 
   <td><strong>Description</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titre</td> 
   <td>Tous sauf la ressource</td> 
   <td>Nom d’affichage du formulaire.<br /> </td> 
  </tr> 
  <tr> 
   <td>Description</td> 
   <td>Tous sauf la ressource</td> 
   <td>Description du formulaire. L’utilisateur ou utilisatrice peut spécifier cette valeur.<br /> </td> 
  </tr> 
  <tr> 
   <td>Type</td> 
   <td>Tous</td> 
   <td><p>Valeur en lecture seule spécifiant le type de ressource. Elle peut avoir l’une des valeurs suivantes :</p> 
    <ul> 
     <li>Modèle de formulaire</li> 
     <li>Formulaire PDF, formulaire PDF (Acroform) ou formulaire PDF (signé)</li> 
     <li>Document, document (signé)</li> 
     <li>Formulaire adaptatif</li> 
     <li>Ressource</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Créé</td> 
   <td>Tous</td> 
   <td>Valeur en lecture seule indiquant la date de création de la ressource.</td> 
  </tr> 
  <tr> 
   <td>Date de la dernière modification</td> 
   <td>Tous</td> 
   <td>Valeur en lecture seule indiquant l’heure de la dernière modification de la ressource.</td> 
  </tr> 
  <tr> 
   <td>Création</td> 
   <td>Tous sauf la ressource</td> 
   <td><p>Valeur en lecture seule qui est automatiquement calculée en fonction du type de formulaire.</p> 
    <ul> 
     <li>PDF/Modèle de formulaire/Document – extrait du fichier binaire téléchargé.</li> 
     <li>Formulaire adaptatif : utilisateur connecté au moment de la création du formulaire.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>État</td> 
   <td>Tous sauf la ressource</td> 
   <td><p> Valeur en lecture seule qui définit l’un des états suivants d’un formulaire :</p> 
    <ul> 
     <li>Aucune valeur : si un formulaire n’a jamais été publié.</li> 
     <li>Publié : lorsqu’un formulaire est publié.</li> 
     <li>Modifié : lorsqu’un formulaire a été modifié après avoir été publié une fois.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Date de dernière publication</td> 
   <td>Tous sauf la ressource</td> 
   <td>Valeur en lecture seule indiquant la date de dernière publication du formulaire.</td> 
  </tr> 
  <tr> 
   <td>Heure d’activation/de désactivation de la publication</td> 
   <td>Tous sauf la ressource</td> 
   <td><p>Heure à laquelle la publication/l’annulation de publication automatique du formulaire est planifiée. L’utilisateur ou utilisatrice définit cette valeur lors de la modification des métadonnées.</p> 
    <ul> 
     <li>L’heure d’activation et de désactivation de la publication doit être postérieure à la date actuelle. </li> 
     <li>La date d’annulation de la publication doit être antérieure à celle de la publication. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Envoyer l’URL</td> 
   <td><p>Modèle de formulaire</p> <p>Formulaire PDF</p> </td> 
   <td><p>Pour configurer une URL spécifiée par l’utilisateur ou utilisatrice afin d’envoyer des données de formulaire à un servlet.</p> <p>L’URL d’envoi peut être configurée à l’aide de l’une des méthodes suivantes, citées par ordre de priorité :</p> 
    <ul> 
     <li>Spécifiez une URL d’envoi directement dans un modèle de formulaire à l’aide du bouton Envoyer via HTTP lors de la création d’un formulaire XFA dans AEM Forms Designer.</li> 
     <li>Dans l’interface utilisateur AEM Forms, sélectionnez un formulaire et spécifiez une URL d’envoi lors de la modification des propriétés de métadonnées.</li> 
     <li>Dans le portail Formulaires, modifiez le composant Recherche et énumérateur et spécifiez une URL d’envoi dans l’onglet Lien de formulaire.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Profil de rendu de HTML</td> 
   <td>Modèle de formulaire</td> 
   <td>Profil de rendu de HTML utilisé lors du rendu d’un modèle de formulaire au format HTML.</td> 
  </tr> 
  <tr> 
   <td>Format de rendu</td> 
   <td><p>Modèle de formulaire</p> <p>Formulaire adaptatif</p> </td> 
   <td><p>Cette option permet à l’utilisateur ou utilisatrice de spécifier le format de rendu du formulaire lors de la publication des formulaires :</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Les deux</li> 
    </ul> <p>Cette option sert à limiter uniquement le format de rendu des formulaires sur le Portail Formulaires où ils sont visibles par l’utilisateur final ou l’utilisatrice finale.</p> </td> 
  </tr> 
  <tr> 
   <td>Balises</td> 
   <td>Tous sauf la ressource</td> 
   <td>Étiquettes associées au formulaire pour faciliter la recherche.</td> 
  </tr> 
  <tr> 
   <td>Références</td> 
   <td><p>Formulaire adaptatif</p> <p>Modèle de formulaire</p> <p>Ressource</p> </td> 
   <td><p>Liste des ressources (autres formulaires ou ressources) auxquelles ce formulaire est associé. Ces ressources peuvent appartenir à deux catégories :</p> 
    <ul> 
     <li>Fait référence : ressources auxquelles le formulaire actuel fait référence.</li> 
     <li>Référencée par : ressources qui font référence à la ressource actuelle.</li> 
    </ul> <p>Ces ressources sont affichées sous forme de liens et leurs métadonnées sont accessibles en cliquant dessus.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Sélection du modèle de formulaire (XDP/XSD)</td> 
   <td>Formulaire adaptatif</td> 
   <td><p>Indique quel modèle de formulaire est utilisé lors de la création du formulaire adaptatif. Cette propriété peut avoir les valeurs suivantes :</p> 
    <ul> 
     <li>Modèle de formulaire : un modèle de formulaire est sélectionné parmi ceux existant dans le référentiel. Cette valeur peut être mise à jour.</li> 
     <li>Schéma XML : un fichier XSD est chargé. Cette valeur peut être mise à jour.</li> 
     <li>Aucune</li> 
    </ul> 
    <div>
      Un modèle de formulaire sélectionné peut être mis à jour, mais pas supprimé. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Affichage des métadonnées de formulaire {#view-form-metadata}

Les ressources ont des valeurs de propriété existantes, qui peuvent être affichées en mode lecture seule. Ces métadonnées sont générées au moment du chargement ou de la création du formulaire.

1. Accédez à l’emplacement de la ressource pour laquelle vous souhaitez afficher les métadonnées.

1. Ouvrez la page de propriétés à l’aide de l’une des méthodes suivantes :

   1. Cliquez sur l’icône Afficher les propriétés ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) à partir des actions rapides.

      >[!NOTE]
      >
      >Les actions rapides sont les éléments d’action qui s’affichent sur une vignette lorsque vous pointez dessus.

   1. Sélectionnez le formulaire, puis cliquez sur l’icône Afficher les propriétés ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) qui s’affiche dans la barre d’outils.
   1. Accédez à la page des détails du formulaire en cliquant sur la vignette de celui-ci lorsque vous n’êtes pas en mode de sélection. Cliquez ensuite sur l’icône représentant un œil ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) en haut à droite, puis sur Propriétés dans la liste en dessous.

1. La page de propriétés qui s’ouvre affiche un schéma contenant uniquement les propriétés de métadonnées comportant des valeurs.

   La page Propriétés comporte une barre d’outils contenant deux icônes d’action :

   * Modifier : ![aem6forms_edit](assets/aem6forms_edit.png) permet de modifier des valeurs de propriété des métadonnées.
   * Afficher : ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) permet d’accéder à la page Détails du formulaire, qui ouvre le formulaire en mode Prévisualisation.

   La section du contenu est divisée en deux parties :

   * Le panneau de gauche contient une vignette du formulaire.
   * Le panneau de droite contient les propriétés de métadonnées en mode lecture seule, réparties dans différents onglets.

## Ajout/mise à jour de valeurs de métadonnées de formulaire {#add-update-form-metadata-values}

Vous pouvez modifier les valeurs des propriétés de métadonnées existantes ou ajouter de nouvelles valeurs à un champ de propriété de métadonnées existant (par exemple, lorsqu’un champ de métadonnées est vide).

### Mise à jour des valeurs de propriétés de métadonnées {#update-metadata-property-values}

1. Suivez la procédure décrite dans la section précédente pour ouvrir la page de propriétés dans laquelle peuvent être affichées les métadonnées existantes du formulaire sélectionné.

1. Dans la barre d’outils, cliquez sur l’icône Modifier ![aem6forms_edit](assets/aem6forms_edit.png) pour passer du mode lecture seule à celui de lecture/écriture.

1. La page de propriétés qui s’affiche contient un schéma comportant un mélange de champs d’entrée modifiables et de texte statique.

1. Les propriétés affichées sous forme de texte statique sont celles que vous ne pouvez pas modifier.

1. Vous pouvez accéder à d’autres onglets pour rechercher des champs d’entrée pour les propriétés de métadonnées placées sous ceux-ci.

   Cette page contient une barre d’outils dotée de deux icônes d’action différentes de celles du mode d’affichage :

   * Annuler : ![aem6forms_close](assets/aem6forms_close.svg_w24.png) permet d’annuler les modifications apportées jusqu’à présent aux valeurs de propriété des métadonnées.
   * Terminé : ![aem6forms_check](assets/aem6forms_check.png) permet d’enregistrer toutes les modifications apportées jusqu’à présent aux valeurs de propriété des métadonnées.

   Ces deux actions redirigent l’utilisateur dans le mode lecture seule de la page de propriétés contenant les valeurs mises à jour.

### Mise à jour de la vignette du formulaire {#update-the-form-thumbnail}

Dans la page de propriétés, le panneau de gauche affiche la vignette du formulaire. Par défaut, la vignette affichée est celle qui a été générée au moment de la création du formulaire (formulaire adaptatif) ou du chargement du formulaire.

Pour tous les types de formulaires, vous avez la possibilité de télécharger une image en cliquant sur **[!UICONTROL Télécharger l’image]** et en accédant à un fichier image dans le répertoire local. L’image sélectionnée remplace la vignette par défaut.

Pour les formulaires adaptatifs, les utilisateurs et utilisatrices ont également la possibilité de générer une vignette en tant qu’instantané de l’aperçu du formulaire adaptatif actuel. Comme AEM Forms prend également en charge la création de formulaires adaptatifs, l’aperçu d’un formulaire adaptatif peut être modifié chaque fois que vous changez ce dernier. Cette possibilité de générer une vignette permet d’obtenir une vignette mise à jour du formulaire adaptatif selon le statut de l’aperçu actuel. Cliquez sur **[!UICONTROL Générer l’aperçu]** pour effectuer cette action.

>[!NOTE]
>
>* Utilisez une image carrée pour la vignette. Lorsque vous utilisez une image qui n’est pas carrée et affichez la miniature dans une vue Liste, la miniature apparaît tronquée.
>* Une fois qu’une nouvelle image est téléchargée ou générée, la vignette est remplacée par celle-ci et l’image précédente ne peut pas être rétablie.
>

## Ajout de métadonnées personnalisées {#add-custom-metadata}

Outre les métadonnées prêtes à l’emploi, AEM Forms prend en charge de nouvelles métadonnées personnalisées.

Un outil (l’éditeur de schéma de métadonnées) est proposé pour définir le schéma de la mise en page des métadonnées, c’est-à-dire la mise en page des élément de la page de **[!UICONTROL propriétés]** d’un formulaire. L’éditeur de schéma de métadonnées permet d’ajouter ou de modifier un schéma personnalisé pour vos ressources.

AEM Forms exposent les schémas de métadonnées des types de formulaires pris en charge dans cet outil. Vous pouvez ainsi accéder à ces schémas et utiliser les fonctionnalités de l’éditeur de schéma de métadonnées pour ajouter des propriétés personnalisées.

### Navigation dans l’éditeur de schéma de métadonnées {#navigate-the-metadata-schema-editor}

1. Accédez à **[!UICONTROL Outils > Ressources > Schémas de métadonnées]**.

1. Cliquez sur **[!UICONTROL formulaires]** dans les formulaires de schéma répertoriés.

1. Dans la liste qui s’affiche, cliquez sur le type de ressource auquel vous souhaitez ajouter des métadonnées personnalisées.

   >[!NOTE]
   >
   >Ces schémas contiennent des propriétés de métadonnées prêtes à l’emploi qui ne doivent pas être modifiées (en cochant des cases ou en cliquant sur Modifier dans la barre d’outils) pour éviter tout problème fonctionnel.

1. Lorsque vous cliquez sur n’importe quel type de ressource, une liste contenant l’option `extendedmetadata` s’affiche. Modifiez ce schéma.

1. Cochez la case en regard de l’option `extendedmetadata`, puis cliquez sur l’icône Modifier ![aem6forms_edit](assets/aem6forms_edit.png) qui s’affiche dans la barre d’outils.

1. AEM Forms ouvre l’éditeur de schéma de métadonnées/le créateur de formulaires du type de ressource sélectionné (dans ce cas présent, du formulaire adaptatif).

   ![Editeur de schéma de métadonnées pour le type de formulaire adaptatif](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Éditeur de métadonnées

   1. Le panneau de gauche contient des sections à onglets où se trouvent les champs. Le panneau de droite affiche tous les composants d’IU disponibles et les propriétés du champ sélectionné dans le panneau de gauche.

   1. La section verrouillée n’est pas modifiable et contient les champs de toutes les propriétés de métadonnées prêtes à l’emploi.

   1. Vous pouvez ajouter d’autres onglets en cliquant sur le symbole +.

   1. Vous pouvez ajouter un champ personnalisé de type souhaité en faisant glisser le composant de champ de la section **[!UICONTROL Créateur de formulaires]** jusqu’à la page de schéma.
   1. Les caractéristiques de ce champ peuvent être affichées sous la section **[!UICONTROL Paramètres]** en cliquant dessus.

### Ajout d’une propriété de métadonnées personnalisée dans l’éditeur de schéma {#add-custom-metadata-property-in-schema-editor}

1. Accédez à l’onglet (nouveau ou existant) auquel vous souhaitez ajouter la propriété personnalisée.

1. Faites glisser un composant du type souhaité de la section **[!UICONTROL Créer le formulaire]** du panneau de gauche jusqu’à l’emplacement souhaité.

   >[!NOTE]
   >
   >Vous ne pouvez pas déplacer les sections verrouillées. Vous pouvez toutefois placer votre composant dans un des espaces vides.

1. Cliquez sur un composant que vous venez de déplacer. Dans l’onglet Paramètres qui s’affiche dans le panneau de droite, renseignez les champs suivants :

   1. Indiquez un libellé de champ à utiliser comme nom d’affichage au-dessus du champ placé dans le schéma (par exemple : Service)
   1. Sous le champ Associer à la propriété, vous pouvez voir une valeur préremplie **./jcr:content/metadata/default&#39;**. Remplacez « **default** » par le nom de propriété de votre choix, qui sera utilisé pour stocker la propriété dans le référentiel crx (par exemple, &#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >Ne modifiez pas le préfixe « ./jcr:content/metadata/ » car il définit le chemin où la propriété est stockée.
      >
      >En outre, le nom de la propriété doit être unique pour éviter d’écrire des valeurs pour plusieurs propriétés au même emplacement dans le référentiel. Il est donc recommandé de modifier la valeur « default ».

   1. Remplissez les autres paramètres en fonction des besoins. Sélectionnez par exemple l’option Obligatoire si vous souhaitez que le champ soit obligatoire.
   1. Pour supprimer un champ que vous avez ajouté, sélectionnez-le, puis cliquez sur l’icône Supprimer ![delete-1](assets/delete-1.png).

1. Si nécessaire, suivez les étapes 1 à 3 pour ajouter une autre propriété.
1. Cliquez sur **Terminé** lorsque vous avez apporté toutes les modifications.

   Vous venez d’ajouter une propriété de métadonnées personnalisée.

Tous les formulaires adaptatifs d’AEM Forms contiennent maintenant cette autre propriété de métadonnées. Vous pouvez la modifier dans la page de propriétés.
