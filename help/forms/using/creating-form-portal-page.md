---
title: Création d’une page de portail de formulaires
seo-title: Création d’une page de portail de formulaires
description: Forms Portal fournit aux développeurs Web des composants pour la création et la personnalisation d’un portail de formulaires sur les sites Web créés à l’aide d’Adobe Experience Manager (AEM).
seo-description: Forms Portal fournit aux développeurs Web des composants pour la création et la personnalisation d’un portail de formulaires sur les sites Web créés à l’aide d’Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Portail Formulaires
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Création d’une page de portail de formulaires{#creating-a-forms-portal-page}

Les composants de Forms Portal fournissent aux développeurs Web des composants pour la création et la personnalisation d’un portail de formulaires sur les sites Web créés à l’aide d’Adobe Experience Manager (AEM). Pour une présentation rapide de Forms Portal, consultez [Présentation de la publication de formulaires sur un portail](../../forms/using/introduction-publishing-forms.md).

## Conditions préalables {#prerequisites}

Les composants de Forms Portal ne peuvent pas être utilisés par défaut. Assurez-vous que les catégories de composants de Forms Portal suivantes sont activées tel qu’indiqué dans [Activation des composants d’un portail de formulaires](/help/forms/using/enabling-forms-portal-components.md).

**Document** ServicesInclut les composants Search &amp; Lister, Link, Drafts and Submissions.

**Prédicats de services de document** : comprend les composants des attributs Date, Texte complet, Propriétés et Balises. Ces composants sont utilisés pour configurer la recherche dans le composant Search &amp; Lister.

Une fois qu’elles sont activées sur une page de sites AEM, ces catégories de composants peuvent être utilisées dans l’explorateur de composants.

![Composants d’AEM Forms Portal dans l’explorateur de composants](assets/component-categories.png)

Catégories de composants de Forms Portal

## Composant Search &amp; Lister {#search-amp-lister-component}

Le composant Search &amp; Lister, disponible dans la catégorie des composants Document Services, est utilisé pour répertorier les formulaires sur une page et pour implémenter la recherche dans les formulaires répertoriés. Ce composant comporte deux volets :

* Le volet Liste, où les formulaires sont répertoriés
* Le volet Recherche, où ajouter la fonction de recherche

Vous pouvez faire glisser et déposer le composant Search &amp; Lister depuis la catégorie de composants Document Services dans l’explorateur de composants sur la page. Une fois ajouté, le composant se présente comme suit.

![Composant Search &amp; Lister dans une page](assets/fp-grid-viw.png)

Composant Search &amp; Lister dans une page avec la disposition Grille

### Zone de liste {#list-pane}

La zone de liste contient vos formulaires répertoriés. Le composant Search &amp; Lister fournit différentes options de configuration à utiliser pour contrôler l’affichage de formulaires dans le volet Liste.

Pour configurer le volet Liste, appuyez sur le composant Search and Lister, puis sur ![settings_icon](assets/settings_icon.png). La boîte de dialogue **[!UICONTROL Modifier le composant]** s’ouvre.

![Volet Liste en mode d’édition](assets/edit-list.png)

Volet Liste en mode d’édition

La boîte de dialogue **Modifier** comprend plusieurs onglets fournissant des options de configuration décrites dans le tableau ci-dessous. Lorsque vous avez terminé, appuyez sur **OK** pour enregistrer la configuration.

<table>
 <tbody>
  <tr>
   <th>Onglet</th>
   <th>Configuration</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Dossiers des actifs</strong></code></td>
   <td>Ajouter un élément</td>
   <td>Configure les dossiers dans lesquels des actifs sont téléchargés à l’aide de l’interface utilisateur d’AEM Forms. Par défaut, tous les actifs téléchargés sont répertoriés. Pour en savoir plus sur l’interface utilisateur d’AEM Forms, consultez <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Présentation de la gestion des formulaires</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Affichage</strong></code></p> </td>
   <td>Texte du titre</td>
   <td>Titre du composant Search &amp; Lister. Le titre par défaut est <strong>Forms Portal.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de mise en page</td>
   <td>Mise en page des actifs. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Désactiver la recherche avancée</td>
   <td>Lorsque cette option est activée, l’icône de recherche avancée est masquée.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Désactiver la recherche de texte</td>
   <td>Lorsque cette option est activée, la barre de recherche en texte intégral est masquée.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Résultat</strong></code></td>
   <td>Nombre de résultats par page</td>
   <td>Configure le nombre maximal de formulaires à afficher sur une page.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Texte des résultats</td>
   <td><p>Configure le texte des résultats (par exemple, 1-12 sur 601 <strong>Résultats</strong>). La valeur par défaut est <strong>Résultats</strong>.</p> <p>Par exemple, si vous spécifiez <strong>Forms </strong>dans ce champ et qu’il y a un total de 601 formulaires, le texte du résultat devient 1-12 sur 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texte de la page</td>
   <td><p>Configure le texte de la page (par exemple, <strong>Page </strong>1 de 51). La valeur par défaut est <strong>Page</strong>.</p> <p>Par exemple, si vous spécifiez <strong>Formulaire de demande </strong>dans ce champ et qu'il y a 51 pages, le texte de la page devient <strong>Formulaire de demande </strong>1 sur 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texte de</td>
   <td><p>Remplace le mot <strong>de</strong> par le texte spécifié (Page 1 <strong>de </strong>51). La valeur par défaut est <strong>de</strong>.</p> <p>Par exemple, si vous spécifiez <strong>sur </strong>dans ce champ, le texte devient Page 1 <strong>sur </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Lien de formulaire</strong></code></td>
   <td>Type de rendu</td>
   <td>Contrôle la liste des formulaires en fonction du type de rendu spécifié. Les options disponibles sont les suivantes : PDF et HTML. Par exemple, si vous sélectionnez uniquement HTML comme type de rendu, les formulaires PDF sont exclus du filtre.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Profil HTML</td>
   <td>Configure le profil HTML à utiliser pour le rendu. Tous les profils disponibles sont répertoriés dans la liste déroulante.</td>
  </tr>
  <tr>
   <td> </td>
   <td>URL d’envoi</td>
   <td><p>Configure un servlet vers lequel les données de formulaire sont envoyées.</p> <p><strong>Remarque :</strong> <em>la valeur URL d’envoi d’un formulaire peut être spécifiée à divers emplacements et l’ordre de priorité s’établit comme suit :</em></p>
    <ol>
     <li><em>La valeur Submit URL intégrée dans le formulaire (dans le bouton d’envoi) a la priorité la plus élevée.</em></li>
     <li><em>Dans l’ordre des priorités, la valeur Submit URL mentionnée dans l’interface utilisateur d’AEM Forms arrive en deuxième position.</em></li>
     <li><em>La valeur Submit URL mentionnée dans Forms Portal a la priorité la plus faible.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Info-bulle HTML Render Action</td>
   <td>Configure le texte de l’info-bulle qui s’affiche lorsque le pointeur de la souris survole <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> l’icône HTML5.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Info-bulle PDF Render Action</td>
   <td>Configure le texte de l’info-bulle qui s’affiche lorsque le pointeur de la souris survole <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> l’icône PDF.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Style</strong></code></td>
   <td>Type de style</td>
   <td>Permet de spécifier <strong>Aucun style, Style par défaut</strong> ou <strong>Style personnalisé </strong>pour répertorier les formulaires.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Chemin d’accès au style personnalisé</td>
   <td>Si vous avez sélectionné l’option Personnalisé dans Type de style, accédez à la feuille CSS personnalisée pour en spécifier le chemin ou sélectionnez Par défaut.</td>
  </tr>
 </tbody>
</table>

### Zone de recherche {#search-pane}

La zone de recherche vous permet d’ajouter les composants Date Predicate (attribut de date), Full Text Predicate (attribut de texte intégral) et Tags predicate (attribut d’étiquette) dans la catégorie Document Services Predicates du sidekick d’AEM. Ces composants implémentent la fonction de recherche pour permettre aux utilisateurs d’effectuer une recherche dans les formulaires répertoriés.

**Conseil :** *vous pouvez contrôler la liste des formulaires affichée sur votre portail de formulaires en fonction d’un paramètre prédéfini et masquer la fonctionnalité de recherche pour les utilisateurs finaux. Pour contrôler la liste des formulaires, utilisez les attributs pour appliquer des filtres de recherche. Vous pouvez également spécifier les valeurs de filtre par défaut et désactiver la recherche dans l&#39;onglet Affichage de la boîte de dialogue Modifier le composant.*

![Zone de recherche avec les attributs Date, Texte complet, Propriétés et Balises](assets/search-with-predicates.png)

Zone de recherche avec les attributs Date, Texte complet, Propriétés et Balises

#### Prédicat de la date {#date-predicate}

Une fois ajouté, l’attribut de date permet d’effectuer une recherche dans les formulaires répertoriés en fonction de leur date de modification.

Pour configurer l’attribut de date :

1. Appuyez sur le composant, puis sur ![settings_icon](assets/settings_icon.png). La boîte de dialogue Edit (Modification du composant) s’ouvre.
1. Indiquez les informations suivantes :

   * **Type** : la seule option disponible est **Date de la dernière modification**.

   * **Texte** : libellé ou légende pour l’attribut de date. La valeur par défaut est **Date de la dernière modification**.

   * **Libellé Date de début** : libellé ou légende correspondant au champ de date de début.
   * **Libellé Date de fin** : libellé ou légende correspondant au champ de date de fin.
   * **Masquer** : permet d’appliquer le filtre de date par défaut permettant de répertorier les formulaires. 

1. Appuyez sur **OK**

#### Prédicat de texte intégral {#full-text-predicate}

L’attribut de texte complet permet d’effectuer une recherche de texte intégral dans les données de formulaire, telles que le nom et la description. Les utilisateurs peuvent effectuer des recherches dans n’importe quelle chaîne de texte pour renvoyer les formulaires dont le nom ou la description contient ce texte.

Pour configurer l’attribut de texte complet, procédez comme suit :

1. Appuyez sur le composant, puis sur ![settings_icon](assets/settings_icon.png). La boîte de dialogue Edit (Modification du composant) s’ouvre.
1. Indiquez le titre dans le champ **Titre principal**.
1. Appuyer sur **Ok**

#### Prédicat de propriétés {#properties-predicate}

L’attribut de propriétés permet d’effectuer une recherche dans les propriétés de formulaire, telles que le titre, l’auteur et la description.

Pour configurer l’attribut de propriétés, procédez comme suit :

1. Appuyez sur le composant, puis sur ![settings_icon](assets/settings_icon.png). La boîte de dialogue Edit (Modification du composant) s’ouvre.
1. Dans l’onglet Général, spécifiez le libellé du critère de recherche. La valeur par défaut est **Propriétés**.

1. Dans l’onglet Options, cliquez sur **Ajouter un élément.**
1. Sélectionnez une propriété dans la liste déroulante et spécifiez un libellé de recherche pour la propriété dans le champ situé sous la liste déroulante.
1. Répétez l’étape 4 pour ajouter d’autres propriétés. Vous pouvez également indiquer une valeur de filtre par défaut pour répertorier les formulaires basés sur les critères spécifiés et masquer la propriété pour les recherches effectuées par les utilisateurs finaux. Cochez la case Hide (Masquer) d’une propriété et spécifiez la valeur de filtre par défaut.
Par exemple, si vous souhaitez afficher les formulaires dont le titre contient le mot « voyage », sélectionnez Masquer à côté de la propriété de titre. En outre, indiquez Voyage dans la zone de texte de valeur de filtre par défaut.

1. Appuyez sur **OK**

#### Prédicat de balises {#tags-predicate}

L’attribut de balises permet d’effectuer une recherche de formulaires construits à partir de balises définies dans Forms Manager.

Pour configurer l’attribut de balises, procédez comme suit :

1. Appuyez sur le composant, puis sur ![settings_icon](assets/settings_icon.png). La boîte de dialogue Edit (Modification du composant) s’ouvre.
1. Cliquez sur la flèche vers le bas située en regard du champ Balises.
1. Sélectionnez les balises appropriées
1. Appuyez sur **OK**

Les balises sélectionnées s’affichent dans le volet Recherche avec des cases à cocher. Les utilisateurs peuvent affiner leur recherche en fonction des balises.

## Répertorier les formulaires sur une page {#list-forms-on-a-page-br}

Pour répertorier les formulaires sur une page, ajoutez le composant **[!UICONTROL Search &amp; Lister]** à la page et configurer le **[!UICONTROL volet Liste]**. Pour permettre aux utilisateurs de rechercher des formulaires avec les attributs de date, de texte et de balises, ajoutez un composant **[!UICONTROL Volet Recherche]**.

Pour lier un formulaire depuis n’importe quel point de la page, utilisez le composant Link. Pour plus d’informations sur le composant Link, voir [Incorporation du composant Link dans une page](../../forms/using/embedding-link-component-page.md).

Pour répertorier les formulaires qui sont à l’état Brouillon et ceux qui ont déjà été envoyés, utilisez le composant **[!UICONTROL Drafts &amp; Submissions]**. Pour en savoir plus, consultez la section [Personnalisation du composant Drafts &amp; Submission](../../forms/using/draft-submission-component.md).

## Compatibilité avec les périphériques mobiles {#mobile-device-friendliness}

Le composant Search &amp; Lister de Forms Portal est compatible avec les périphériques mobiles et s’adapte en conséquence. Les trois vues par défaut : La grille, la carte, les mises en page du panneau en fonction du périphérique sur lequel le site est ouvert, à condition que la page Web s’adapte également. Search &amp; Lister n’est qu’un simple composant et ne contrôle pas le style au niveau de la page.

L’image suivante montre le composant Search &amp; Lister lorsqu’il est ouvert sur un périphérique mobile :

![Capture d’écran du composant Search &amp; Lister](assets/search_lister.png)

Composant Search &amp; Lister

## Personnalisation d’une page Forms Portal {#customizing-a-forms-portal-page-br}

Vous pouvez personnaliser une page du portail de formulaires pour donner un aspect spécifique à la page. Vous pouvez également ajouter des métadonnées pour améliorer l’expérience de recherche, pour modifier la disposition de la page, ou encore ajouter des styles CSS personnalisés. Pour plus d’informations, voir [Personnalisation des modèles pour les composants Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

L’interface utilisateur d’AEM Forms vous permet d’ajouter des métadonnées personnalisées aux formulaires. Les métadonnées personnalisées se révèlent particulièrement utiles pour mettre à la disposition des utilisateurs un environnement permettant de répertorier et de rechercher des formulaires. Pour plus d’informations sur les métadonnées personnalisées, voir [Personnalisation des modèles pour les composants Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

Forms Portal propose des actions de rendu prêtes à l’emploi. Vous pouvez personnaliser Forms Portal afin d’ajouter d’autres actions. Pour en savoir plus, consultez [Ajout d’une action personnalisée sur des éléments de liste de formulaire.](../../forms/using/add-custom-action-form-lister.md)

## Articles connexes

* [Activation des composants du portail de formulaires](/help/forms/using/enabling-forms-portal-components.md)
* [Créer une page du portail de formulaires](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Drafts and Submissions](/help/forms/using/draft-submission-component.md)
* [Personnalisation de l’enregistrement des brouillons et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
