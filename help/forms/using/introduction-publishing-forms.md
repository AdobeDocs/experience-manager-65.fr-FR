---
title: Présentation de la publication de formulaires sur un portail
seo-title: Présentation de la publication de formulaires sur un portail
description: AEM Forms fournit des composants que vous pouvez utiliser pour créer votre portail de formulaires. Cet article présente les composants de portail de formulaires disponibles.
seo-description: AEM Forms fournit des composants que vous pouvez utiliser pour créer votre portail de formulaires. Cet article présente les composants de portail de formulaires disponibles.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 62%

---

# Présentation de la publication de formulaires sur un portail{#introduction-to-publishing-forms-on-a-portal}

## Présentation des composants du portail AEM Forms {#aem-forms-portal-components-overview}

Dans les scénarios typiques de déploiement de portail basés sur l’utilisation de formulaires, le développement des formulaires et le développement du portail sont deux activités bien distinctes. Tandis que les créateurs de formulaires créent des formulaires et les stockent dans un référentiel, les développeurs Web créent une application Web permettant de répertorier les formulaires et de gérer leurs envois. Les formulaires sont copiés sur la plateforme Web car il n’existe aucune communication entre le référentiel des formulaires et l’application Web.

Ces scénarios entraînent généralement des problèmes de gestion et des retards de production. Par exemple, lorsqu’une nouvelle version d’un formulaire est disponible dans le référentiel, vous devez remplacer le formulaire sur la plateforme Web, modifier l’application Web, puis déployer à nouveau le formulaire sur le site public. Le redéploiement de l’application Web risque d’entraîner un temps d’arrêt au niveau du serveur. En règle générale, les temps d’arrêt de serveur sont dus à une activité planifiée et, par conséquent, les modifications ne peuvent pas être transférées au site public instantanément.

AEM Forms fournit des composants de portail qui réduisent les surcharges de gestion et les délais de production. Les composants permettent aux développeurs Web de créer et de personnaliser un portail de formulaires sur les sites Web créés à l’aide d’Adobe Experience Manager (AEM).

![Portail AEM Forms](assets/aem-forms-portal.png)

Les composants de portail de formulaires vous permettent d’ajouter les fonctionnalités suivantes :

* Création d’une liste de formulaires dans des mises en page personnalisées Mises en page de vues Liste, Carte et Panneau prêtes à l’emploi. Vous pouvez créer vos propres mises en page personnalisées.
* Possibilité d’afficher les métadonnées et les actions personnalisées lorsque vous les répertoriez.
* Création d’une liste des formulaires publiés par l’interface utilisateur d’AEM Forms sur l’instance de publication où sont utilisés les composants de portail de formulaires.
* Possibilité pour les utilisateurs finaux d’afficher les formulaires aux formats HTML et PDF.
* Utilisation d’un profil HTML personnalisé pour le rendu des formulaires.
* Activation de la recherche de formulaires en fonction de différents critères, tels que les propriétés, les métadonnées et les balises du formulaire.
* Envoi de données de formulaire vers une servlet.
* Utilisation de feuilles CSS pour la personnalisation de l’apparence du portail.
* Création de liens vers des formulaires.
* Création d’une liste de brouillons et d’envois associés au formulaire adaptatif créé par l’utilisateur final.

## Composants disponibles du portail AEM Forms {#available-aem-forms-portal-components}

AEM Forms fournit les composants de portail suivants prêts à l’emploi, regroupés sous les groupes de composants **Services de document** et **Prédicats de services de document** :

### Search &amp; Lister {#search-amp-lister}

Le composant Search &amp; Lister (Recherche et énumérateur) permet de répertorier les formulaires du référentiel de formulaires sur la page de portail et propose des options de configuration pour répertorier les formulaires selon des critères spécifiés. Il permet également de spécifier des critères de recherche pour permettre aux utilisateurs du portail d’effectuer des recherches dans la liste des formulaires.

### Brouillons et soumissions {#drafts-amp-submissions}

Alors que le composant Search &amp; Lister affiche les formulaires rendus publics par l’auteur de formulaires, le composant Drafts &amp; Submissions (Brouillon et envoi) affiche les formulaires enregistrés sous forme de brouillons en vue de leur achèvement ultérieur et les formulaires envoyés. Ce composant offre un environnement personnalisé à tout utilisateur connecté.

### Lien {#link}

Le composant Link (Lien) vous permet de créer un lien vers un formulaire depuis n’importe quel emplacement de la page. Cela peut être le cas, par exemple, si vous proposez un programme de formation et que vous voulez que vos utilisateurs envoient un formulaire pour s’inscrire à la formation. Vous avez indiqué les détails du programme sur votre site Web. Sous les détails, vous souhaitez fournir un lien vers le formulaire d’inscription. Le composant Link vous permet de créer ce lien.

## Workflow du portail Forms {#forms-portal-workflow}

Forms Portal vous permet de répertorier les formulaires du référentiel de formulaires sur votre page de portail. Il permet également de spécifier des critères de recherche pour permettre aux utilisateurs du portail d’effectuer des recherches dans la liste des formulaires. Vous pouvez également utiliser le composant Drafts &amp; Submissions pour afficher les formulaires enregistrés en tant que brouillon en vue de les remplir ultérieurement et les formulaires envoyés. Vous devez effectuer un certain ensemble d’opérations avant que ces fonctionnalités ne soient disponibles sur une page Sites. Effectuez les étapes de la séquence répertoriée pour rendre les composants et les fonctionnalités respectives disponibles sur une page de sites :

1. **Activez les composants** du portail Forms : Les composants Forms Portal prêts à l’emploi ne sont pas disponibles. [Activez les composants à partir du ](/help/forms/using/enabling-forms-portal-components.md) sidekick d’AEM pour une page AEM Sites.
1. **Répertorier les formulaires sur une page (créer une page de portail de formulaires) :** vous pouvez répertorier les formulaires sur les pages AEM Sites et non AEM Site. La liste contient les formulaires disponibles sur l’instance de publication. Un utilisateur peut ouvrir des formulaires et commencer à les remplir. Chaque fois qu’un utilisateur ouvre un formulaire, une nouvelle instance du formulaire est créée :

   1. **Répertorier les formulaires sur une page** AEM Sites : Ajoutez le composant  **[Search &amp;](../../forms/using/creating-form-portal-page.md)** Listercomponent à la page et configurez le panneau  **[Liste](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** dans lequel répertorier les formulaires sur une page. Ajoutez et configurez le composant **Panneau de recherche** au composant **Search &amp; Lister** pour ajouter également la fonctionnalité de recherche à la page. La page avec le composant Forms Portal est appelée [page Forms Portal](../../forms/using/creating-form-portal-page.md).

   1. **Lister des formulaires sur une page non-AEM Sites :**  utilisez les  [API de recherche du portail de ](/help/forms/using/listing-forms-webpage-using-apis.md) formulaires pour interroger, récupérer et répertorier des formulaires sur des pages non-AEM Sites.

1. **Répertorier les formulaires préliminaires et envoyés sur une page** du portail de formulaires : Ajoutez et configurez le composant Drafts &amp; Submissions (Brouillons et envois) sur la page Forms Portal. Le composant dresse la liste de tous les formulaires qui sont à l’état de brouillon et des formulaires déjà envoyés.

   Pour activer l’affichage d’un formulaire adaptatif envoyé dans l’onglet des envois, définissez **Action d’envoi** sur **[Action d’envoi du portail Forms](configuring-submit-actions.md).** Vous pouvez également activer l’option d’envoi du portail Forms. Chaque fois qu’un utilisateur envoie le formulaire, celui-ci est ajouté à l’onglet des envois.

1. **Configurez le stockage des données de formulaires sous forme de brouillons et envoyés :**  par défaut, les données de brouillons et d’envois sont stockées dans le référentiel AEM. Dans un environnement de production, il est recommandé de ne pas stocker des données de formulaire de brouillon ou envoyées dans le référentiel AEM. [Configurez le composant Forms Portal pour enregistrer les données à un emplacement](../../forms/using/draft-submission-component.md#customizing-the-storage) sécurisé.
1. **(Facultatif) Personnalisation des composants Forms Portal :** [personnalisez les ](../../forms/using/customizing-templates-forms-portal-components.md) modèles de page Forms Portal pour donner un aspect distinctif aux composants.
1. **(Facultatif) Ajout de métadonnées personnalisées aux formulaires :** [ajoutez des métadonnées personnalisées aux ](../../forms/using/customizing-templates-forms-portal-components.md) formulaires afin d’améliorer l’expérience de liste et de recherche.
1. **Publier la page Forms Portal :** votre page Forms Portal est maintenant prête. Publiez la page.

## Articles connexes {#related-articles}

* [Activation des composants de Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* [Page du portail de formulaires](../../forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Drafts &amp; Submissions](../../forms/using/draft-submission-component.md)
* [Personnalisation du stockage des brouillons et des formulaires envoyés](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](../../forms/using/introduction-publishing-forms.md)
