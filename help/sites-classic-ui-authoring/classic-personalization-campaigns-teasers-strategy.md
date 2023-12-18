---
title: Teasers et stratégies
description: Les campagnes utilisent souvent les teasers comme mécanisme pour inciter un segment spécifique de la population de visiteurs et de visiteuses à consulter du contenu axé sur leurs intérêts. Un ou plusieurs teasers sont définis pour une campagne spécifique.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: ht
source-wordcount: '1195'
ht-degree: 100%

---

# Teasers et stratégies{#teasers-and-strategies}

Les campagnes utilisent souvent les teasers comme mécanisme pour inciter un segment spécifique de la population de visiteurs et de visiteuses à consulter du contenu axé sur leurs intérêts. Un ou plusieurs teasers sont définis pour une campagne spécifique.

>[!NOTE]
>
>Le composant Teaser est désormais obsolète dans AEM 6.2. Utilisez le [Composant Cible](/help/sites-authoring/content-targeting-touch.md) à la place.

* Les **pages de marque** sont stockées dans la section Campagnes du site Web. Une marque contient les différentes campagnes.
* Les **pages de campagne** sont stockées dans la section Campagnes du site Web. Chaque campagne comporte une page individuelle, sous laquelle sont conservées les définitions de teaser. La page conteneur, ou vue d’ensemble, contient également certaines informations et statistiques concernant les pages de teaser individuelles.

Les teasers AEM sont composés de divers éléments :

* Les **pages de teaser** sont stockées dans une page de campagne appropriée et présentent les définitions des paragraphes de teaser disponibles pour chaque campagne spécifique. Ces définitions sont utilisées lors de l’affichage des paragraphes de teaser, notamment les variations de contenu, le segment à utiliser pour sélectionner une variation et le facteur d’amplification.
* Le **Composant Teaser** est prêt à l’emploi et vous permet de créer une instance de votre paragraphe de teaser spécifique dans une page de contenu. Pour créer votre propre paragraphe de teaser, faites glisser le composant Teaser à partir du sidekick, puis spécifiez votre définition de teaser. **Remarque :** le composant Teaser est obsolète dans AEM 6.2. Utilisez le [composant Cible](/help/sites-authoring/content-targeting-touch.md) à la place.
* Les **Paragraphes de teaser** sont des instances de teaser réelles dans une page de contenu. Elles incitent un segment de visiteurs et de visiteuses à consulter du contenu axé sur leurs intérêts.
* Pages qui contiennent le contenu de la campagne axée sur un segment spécifique de visiteurs et de visiteuses. En règle générale, les paragraphes de teaser conduisent le visiteur ou la visiteuse vers de telles pages.

## Stratégies {#strategies}

Lors de l’ajout d’un paragraphe de teaser à une page, vous devez définir la **stratégie**.

En effet, si plusieurs teasers sont disponibles, la stratégie permet de résoudre leurs segments correspondants. La **Stratégie** spécifie ensuite un critère supplémentaire utilisé pour sélectionner le teaser affiché :

* Le **Score Clickstream** est basé sur les balises et les accès aux balises associées dans le contexte du client du visiteur ou de la visiteuse (indique la fréquence à laquelle un visiteur ou une visiteuse a cliqué sur des pages qui contiennent la balise correspondante). Les taux de fréquence d’accès aux balises définis sur la page du teaser sont comparés.
* **Aléatoire**, pour la sélection « aléatoire » ; emploie le facteur aléatoire généré pour une page. Celui-ci est visible dans le [contexte client](/help/sites-administering/client-context.md).
* **Première** dans la liste des segments résolus. L’ordre est celui des teasers dans la page conteneur de campagne.

Le [facteur d’amplification](/help/sites-administering/campaign-segmentation.md#boost-factor) du segment se répercute également sur la sélection. Il s’agit d’un facteur de pondération ajouté à une définition de segment pour augmenter/diminuer la probabilité relative de sa sélection.

Le workflow et les interrelations des divers critères de sélection sont mieux illustrés par un exemple (une méthode qui peut également être utilisée pour assurer que vos teasers atteignent le public requis).

Si les segments suivants ont déjà été créés et se voient attribuer leur facteur d’amplification respectif :

| Segment | Facteur d’amplification |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

Nous utilisons les définitions de teaser suivantes :

<table>
 <tbody>
  <tr>
   <td>Campagne</td>
   <td>Teaser</td>
   <td>Segments attribués</td>
   <td>Balises attribuées </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Entreprise, Marketing</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Entreprise<br /> </td>
  </tr>
 </tbody>
</table>

Ensuite, si nous appliquons ceci à un visiteur ou à une visiteuse où :

* **S1**, **S2 et **S6** sont résolus avec succès ;

* la balise **marketing** a trois accès ;
* la balise **entreprise** a six accès.

Nous pouvons voir les résultats :

* Succès de la corrsepondance : l’un des segments affectés au teaser est-il résolu avec succès pour le visiteur actuel ou la visiteuse actuelle ?
* Facteur d’amplification : facteur d’amplification le plus élevé de tous les segments applicables
* Score Clickstream : total cumulé de tous les accès aux balises applicables.

qui sont calculés avant d’appliquer la stratégie appropriée :

<table>
 <tbody>
  <tr>
   <td>Campagne</td>
   <td>Teaser</td>
   <td>Segments attribués</td>
   <td>Balises </td>
   <td>Correspondance réussie ?</td>
   <td>Facteur d’amplification résultant</td>
   <td>Score de flux de clics résultant </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Entreprise, Marketing</td>
   <td>Oui</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>Oui</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>Non</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>Oui<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
   <td>Oui</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Entreprise</td>
   <td>Oui</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Ces valeurs sont utilisées pour déterminer les teasers que le visiteur ou la visiteuse verra, en fonction de la **stratégie** appliquée au paragraphe de teaser :

<table>
 <tbody>
  <tr>
   <td>Stratégie</td>
   <td>Teaser résultant</td>
   <td>Commentaires</td>
  </tr>
  <tr>
   <td>Premier</td>
   <td>T5</td>
   <td>Seuls T5 et T6 sont considérés comme si leurs segments étaient tous résolus <i>et</i> comme s’ils avaient le facteur d’amplification le plus élevé. La liste renvoyée est dans l’ordre T5, T6 ; T5 est donc sélectionné et affiché.</td>
  </tr>
  <tr>
   <td>Aléatoire</td>
   <td>T5 ou T6</td>
   <td>Les deux teasers ont des segments qui sont tous résolus et le même facteur d’amplification. Par conséquent, les deux teasers sont affichés en proportion égale.</td>
  </tr>
  <tr>
   <td>Score Clickstream</td>
   <td>T6</td>
   <td><p>Les segments pour T1, T4, T5 et T6 sont tous résolus pour le visiteur ou la visiteuse. Les facteurs d'amplification plus élevés de T5 et T6 excluent alors T1 et T4. Enfin, le score Clickstream supérieur de T6 se voit sélectionné.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si, après les techniques de résolution ci-dessus, plusieurs teasers sont sélectionnables, une sélection interne (aléatoire) sélectionne un seul teaser à afficher.
>
>Par exemple, si la stratégie était Score Clickstream et que T5 avait le même score Clickstream que T6 (c’est-à-dire six au lieu de trois), la sélection interne (aléatoire) serait utilisée pour sélectionner l’un de ces deux types.

Les paragraphes/pages de teaser sont utilisés pour diriger des segments de visiteurs et visiteuses spécifiques vers le contenu qui est centré sur leurs intérêts. Ils peuvent présenter toute une gamme d’options parmi lesquelles le visiteur ou la visiteuse peut effectuer un choix, ou n’afficher qu’un seul paragraphe de teaser basé sur un segment de visiteurs et visiteuses spécifique. Par exemple, le paragraphe de teaser affiché peut dépendre de l’âge du visiteur ou de la visiteuse.

En règle générale, une page de teaser est une action temporaire qui dure pendant une durée spécifique, jusqu’à ce qu’elle soit remplacée par la page de teaser suivante.

Après avoir créé votre marque et votre campagne, vous pouvez créer et configurer votre expérience de teaser.

### Création d’un point de contact pour votre teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>Le composant Teaser est désormais obsolète dans AEM 6.2. Utilisez le [Composant cible](/help/sites-authoring/content-targeting-touch.md) à la place.

1. Accédez à la page de contenu dans laquelle vous souhaitez placer le paragraphe de teaser qui mènera à la page de votre campagne.
1. Ajoutez un composant **Teaser** (disponible dans la section **Personnalisation** du sidekick) à la position requise. Lors de la première création, il indique que le chemin de la campagne n’est pas encore configuré :

   ![chlimage_1](assets/chlimage_1.png)

1. Modifiez le composant de teaser pour ajouter :

   * **Le chemin de la campagne** ;
Chemin d’accès à la page de campagne qui comprend la page de teaser individuelle ; les segments déterminent exactement le teaser affiché.

   * **[Stratégie](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
Méthode utilisée pour la sélection lorsque plusieurs segments sont résolus avec succès.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Cliquez sur **OK** pour enregistrer. Selon les segments que vous avez définis sur le teaser et le profil utilisateur sous lequel vous avez établi la connexion, le contenu approprié s’affiche :

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Placez le pointeur de la souris sur le paragraphe de teaser pour afficher l’icône de point d’interrogation (coin inférieur droit du composant). Cliquez sur ceci pour afficher les segments appliqués et déterminer s’ils sont actuellement résolus.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Vue d’ensemble du teaser {#teaser-overview}

Outre la vue de campagne dans MCM, la page de campagne fournit également des informations sur les teasers qui y sont connectés :

1. Dans la console **Sites web**, ouvrez la page de campagne, par exemple :

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Vous accédez alors à un aperçu de la définition du teaser et des statistiques de visionnage :

   ![chlimage_1-4](assets/chlimage_1-4.png)
