---
title: Composant Drafts & Submissions
description: Le composant Drafts & Submissions dresse la liste de tous les formulaires qui sont à l’état de brouillon et des formulaires déjà envoyés. Vous pouvez personnaliser l’apparence et le style du composant.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '744'
ht-degree: 100%

---

# Composant Drafts &amp; Submissions{#drafts-and-submissions-component}

Le composant Drafts &amp; Submissions dresse la liste de tous les formulaires qui sont à l’état de brouillon et des formulaires déjà envoyés. Le composant dispose de sections distinctes (onglets) pour les brouillons et les formulaires envoyés. Les personnes peuvent afficher leurs brouillons et leurs formulaires envoyés uniquement.

## Configuration du composant {#configuring-the-component}

Le composant Drafts &amp; Submissions comporte deux onglets : Brouillons et envois.

Pour autoriser un envoi de formulaire adaptatif à apparaître dans l’onglet des envois, définissez **Action d’envoi** sur **[Action d’envoi du Portail Formulaires](../../forms/using/configuring-submit-actions.md). Sinon,** activez l’option Action d’envoi du Portail Formulaires. Lorsqu’un utilisateur envoie le formulaire, ce formulaire est ajouté à l’onglet des envois.

La fonctionnalité de brouillon est activée immédiatement. Lorsqu’une personne clique sur **Enregistrer** sur un formulaire adaptatif, le formulaire est ajouté à l’onglet Brouillons.

Effectuez les étapes suivantes pour ajouter et configurer le composant Drafts &amp; Submissions :

1. Faites glisser le composant **Drafts &amp; Submissions** sous la catégorie Document Services dans l’explorateur de composants de votre page.
1. Sélectionnez le composant, puis sélectionnez ![settings_icon](assets/settings_icon.png) pour ouvrir la boîte de dialogue Modifier du composant.

   ![Composant Drafts &amp; Submissions](assets/drafts-submissions-edit.png)

1. Dans la boîte de dialogue Modifier, spécifiez les détails suivants et sélectionnez **Terminé** pour enregistrer les paramètres.

<table>
 <tbody>
  <tr>
   <th>Tabulation</th>
   <th>Configuration</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>Général</td>
   <td>Nombre total de résultats</td>
   <td>Spécifie le nombre maximal de résultats à afficher. Si le nombre de résultats dépasse la limite du nombre total de résultats, un lien <strong>Plus</strong> s’affiche au bas du composant. Pour afficher tous les formulaires, cliquez sur <strong>Plus. </strong> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Type de style</td>
   <td>Indique le style du composant. Vous pouvez spécifier <strong>Aucun Style</strong>, <strong>Style par défaut</strong> ou <strong>Style personnalisé</strong> pour répertorier les formulaires. Pour l’option Style personnalisé, vous pouvez spécifier le chemin du fichier CSS personnalisé dans le champ <strong>Chemin d’accès au style personnalisé</strong><strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Chemin d’accès au style personnalisé</td>
   <td>Si vous sélectionnez l’option <strong>Style personnalisé</strong> dans le champ <strong>Type de style</strong>, utilisez le champ <strong>Chemin d’accès au style personnalisé</strong> pour spécifier le chemin du fichier CSS personnalisé. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Options d’affichage</td>
   <td><p>Spécifie les onglets à afficher. Vous pouvez choisir d’afficher des brouillons de formulaires, des formulaires envoyés, ou les deux. </p> <p><strong>Remarque</strong> :<em> Pour les <strong>Options d’affichage</strong>, si vous sélectionnez une option autre que <strong>Les deux</strong>, l’option du champ <strong>Tabulation par défaut</strong> n’est pas utilisée.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Onglet par défaut</td>
   <td>Spécifie l’onglet à afficher au chargement de la page du portail Formulaires. Vous pouvez choisir entre <strong>l’onglet Brouillons de formulaires</strong> et <strong>l’onglet Formulaires envoyés</strong>.</td>
  </tr>
  <tr>
   <td>Configuration de l’onglet Brouillons de formulaires</td>
   <td>Titre personnalisé</td>
   <td>Spécifie le titre de l’onglet <strong>Brouillons de formulaires</strong>. La valeur par défaut est <strong>Brouillons de formulaires.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de disposition</td>
   <td>Spécifie la disposition à utiliser pour la liste Brouillons de formulaires.</td>
  </tr>
  <tr>
   <td>Configuration de l’onglet Formulaires envoyés</td>
   <td>Titre personnalisé </td>
   <td>Spécifie le titre de l’onglet <strong>Formulaires envoyés</strong>. La valeur par défaut est <strong>Formulaires envoyés.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de mise en page</td>
   <td>Spécifie l’affichage à utiliser pour la liste Formulaires<strong> </strong>envoyés. </td>
  </tr>
 </tbody>
</table>

## Personnaliser l’espace de stockage {#customizing-the-storage}

Lorsque vous utilisez l’action d’envoi Forms Portal ou activez les données de stockage dans l’option de portail de formulaires dans un formulaire adaptatif, les données du formulaire sont stockées dans le référentiel AEM. Dans un environnement de production, il est recommandé de ne pas stocker des données de formulaire de brouillon ou envoyées dans le référentiel AEM. Au contraire, vous devez intégrer le composant de brouillons et d’envoi à un stockage sécurisé comme la base de données d’entreprise pour stocker des brouillons et des données de formulaires envoyés.

Le portail Formulaires vous permet de stocker des données dans un référentiel AEM local ou distant, ou encore dans une base de données. AEM Forms vous permet de personnaliser l’implémentation du stockage des données utilisateur pour les brouillons et les envois. Vous pouvez remplacer les méthodes par défaut pour spécifier la manière dont les données de brouillon et d’envoi sont stockées dans un espace de stockage de votre choix. Vous pouvez, par exemple, stocker les données dans un entrepôt de données implémenté au sein de votre entreprise.

Le portail Formulaires fournit des services prêts à l’emploi (API) pour stocker des données sur le référentiel crx d’instances de publication AEM Forms locales et distantes. Vous pouvez remplacer les implémentations par défaut, décrites dans l’artickle [Configurer les services de stockage pour les brouillons et les envois](/help/forms/using/configuring-draft-submission-storage.md), par des implémentations personnalisées. Pour plus d’informations sur les méthodes requises dans le cadre d’une implémentation personnalisée visant à stocker du contenu dans un emplacement sécurisé, consultez la section [Personnaliser les services de données de brouillons et d’envois](/help/forms/using/custom-draft-submission-data-services.md) et [Stockage personnalisé des composant brouillons et envois.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentation d’AEM Forms fournit un [Exemple d’intégration d’un composant brouillons et envois à la base de données](integrate-draft-submission-database.md). Vous pouvez utiliser l’exemple d’implémentation pour développer votre propre implémentation personnalisée.

## Articles connexes

* [Activer des composants du portail Formulaires](/help/forms/using/enabling-forms-portal-components.md)
* [Créer une page du portail Formulaires](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Brouillons et Envois](/help/forms/using/draft-submission-component.md)
* [Personnaliser le stockage des brouillons de formulaires et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
