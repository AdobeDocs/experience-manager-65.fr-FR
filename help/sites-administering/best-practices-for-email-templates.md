---
title: Bonnes pratiques relatives aux modèles d’e-mail
description: Découvrez les bonnes pratiques pour créer des modèles d’email dans AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 47%

---

# Bonnes pratiques relatives aux modèles d’e-mail {#best-practices-for-email-templates}

>[!CAUTION]
>
>Cet article s’applique aux composants Foundation obsolètes basés sur AEM composants de messagerie électronique.
>
>Les utilisateurs sont encouragés à utiliser les [Composants principaux : composants de messagerie électronique.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

Ce document décrit certaines des bonnes pratiques concernant la conception d’emails, ce qui se traduit par un modèle de campagne email bien développé.

La campagne de démonstration disponible dans AEM observe toutes ces meilleures pratiques. La manière dont les bonnes pratiques sont mises en oeuvre dans la campagne de démonstration est décrite pour chaque bonne pratique.

Utilisez ces bonnes pratiques lors de la création de votre propre newsletter.

>[!NOTE]
>
>Tout le contenu d’une campagne doit être créé sous une page `master` de type `cq/personalization/components/ambitpage`.
>
>Par exemple, si la structure de campagne planifiée ressemble à
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Assurez-vous qu’il réside sous un `master` page
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Lors de la création d’un modèle de courrier électronique pour Adobe Campaign, vous devez inclure la propriété . **acMapping** avec la valeur **mapRecipient** dans le **jcr:content** du modèle. Dans le cas contraire, vous ne pouvez pas sélectionner le modèle Adobe Campaign dans **Propriétés de la page** de Experience Manager (le champ est désactivé).

## Composant Modèle/page {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Bonne pratique</strong></td>
   <td><strong>Mise en œuvre</strong></td>
  </tr>
  <tr>
   <td><p>Spécifiez le type de document afin d’assurer un rendu cohérent.</p> <p>Ajoutez DOCTYPE au début (HTML ou XHTML).</p> </td>
   <td><p>Configurable en modifiant la conception de la propriété <i>cq:doctype</i> dans <i>« /etc/designs/default/jcr:content/campaign_newsletterpage »</i></p> <p>La valeur par défaut est « XHTML » :</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Peut être remplacé par « HTML_5 » :</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Spécifiez la définition des caractères afin d’assurer le rendu correct des caractères spéciaux.</p> <p>Ajoutez la déclaration CHARSET (par exemple, iso-8859-15, UTF-8) à &lt;head&gt;</p> </td>
   <td><p>Définie sur UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codez toute la structure à l’aide de la fonction &lt;table&gt;élément. Pour des mises en page plus compliquées, vous devez imbriquer les tableaux pour créer des structures complexes.</p> <p>L’e-mail doit présenter un aspect correct, même sans CSS.</p> </td>
   <td><p>Les tableaux sont utilisés dans tout le modèle pour structurer le contenu. Actuellement, il est possible d’utiliser un maximum de quatre tableaux imbriqués (1 tableau de base + max. 3 niveaux d’imbrication).</p> <p>Les balises &lt;div&gt; ne sont utilisées qu’en mode création pour garantir la modification correcte des composants.</p> </td>
  </tr>
  <tr>
   <td>Utilisez des attributs d’élément (par exemple, cellpadding, valign et width) pour définir les dimensions de table. Cette méthode force une structure de modèle de boîte.</td>
   <td><p>Toutes les tables contiennent les attributs nécessaires, tels que <i>border</i>, <i>cellpadding</i>, <i>cellspacing</i>, et <i>width</i>.</p> <p>Pour que le positionnement des éléments dans les tableaux soit harmonisé, toutes les cellules des tableaux doive avoir l’attribut <i>valign="top"</i> défini.</p> </td>
  </tr>
  <tr>
   <td><p>Prenez en compte, si possible, de la convivialité des appareils mobiles. Utilisez les requêtes multimédias pour augmenter la taille du texte sur les petits écrans et fournir des zones actives de la taille d’une vignette pour les liens.</p> <p>Rendez un e-mail interactif si la conception l’autorise.</p> </td>
   <td>Même si les styles CSS sont utilisés pour illustrer le design de démonstration, les requêtes multimédias sont utilisées pour proposer une version conviviale pour les appareils mobiles.</td>
  </tr>
  <tr>
   <td>Les styles CSS intégrés sont un meilleur choix que l’insertion de tous les styles CSS au début.</td>
   <td><p>Pour mieux démontrer la structure de HTML sous-jacente et faciliter la personnalisation de la structure de newsletter, seules certaines définitions CSS ont été insérées.</p> <p>Les styles de base et les variations de modèle ont été extraits dans un bloc de style dans l’élément &lt;head&gt; de la page. Lors de l’envoi final de la newsletter, ces définitions CSS sont insérées dans le HTML. Un mécanisme de mise en ligne automatique est prévu, mais actuellement pas disponible.</p> </td>
  </tr>
  <tr>
   <td>Restez simple avec votre CSS. Évitez les déclarations de style composées, le code court, les propriétés de mise en page CSS, les sélecteurs complexes et les pseudo-éléments.</td>
   <td>Même si les styles CSS sont utilisés pour illustrer le design de démonstration, les recommandations CSS sont observées.</td>
  </tr>
  <tr>
   <td>Les e-mails doivent présenter une largeur maximale de 600 à 800 pixels. Ce dimensionnement les rend plus performants dans la taille du volet d’aperçu fournie par de nombreux clients.</td>
   <td>Le <i>width</i> du tableau de contenu est limité à 600 pixels dans la conception de démonstration.</td>
  </tr>
 </tbody>
</table>

### Images {#images}

/libs/mcm/campaign/components/image

| **Bonne pratique** | **Mise en œuvre** |
|---|---|
| Ajoutez des attributs *alt* aux images. | L’attribut *alt* a été défini comme obligatoire pour le composant d’image. |
| Utilisez le format *jpg* au lieu du format *png* pour les images. | Les images sont toujours diffusées en tant que JPG par le composant d’image. |
| Utilisez l’élément `<img>` au lieu des images d’arrière-plan dans un tableau. | Aucune donnée d’image d’arrière-plan n’est utilisée dans les modèles. |
| Ajoutez l’attribut style=&quot;bloc d’affichage&quot; dans les images. Cela leur permet de bien s&#39;afficher sur Gmail. | Toutes les images contiennent par défaut l’attribut *style=&quot;display block&quot;*. |

### Texte et liens {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Bonne pratique</strong></td>
   <td><strong>Mise en œuvre</strong></td>
  </tr>
  <tr>
   <td>Utilisez du code html &lt;font&gt; plutôt que du style dans CSS (famille de polices).</td>
   <td>L’éditeur de texte enrichi (par exemple, dans le composant textimage) prend désormais en charge le choix et l’application de familles de polices et de tailles de police aux textes sélectionnés. Ils sont rendus sous la forme de balises.</td>
  </tr>
  <tr>
   <td>Utilisez des polices de base interplateformes, telles que <i>Arial®, Verdana, Géorgie</i>, et <i>Times New Roman®</i>.</td>
   <td><p>Dépend de la conception de la newsletter.</p> <p>Pour la conception de démonstration, la police "Helvetica®" est utilisée, mais elle revient à une police sans-serif générique, si elle n’est pas présente.</p> </td>
  </tr>
 </tbody>
</table>

### Générique {#generic}

| **Bonne pratique** | **Mise en œuvre** |
|---|---|
| Utilisez le validateur W3C pour corriger le code du HTML. Assurez-vous que toutes les balises ouvertes sont correctement fermées. | Le code doit être validé. Pour le Doctype de transition XHTML uniquement, l’attribut xmlns manquant pour `<html>` élément est manquant. |
| Évitez d’utiliser JavaScript ou Flash : ces technologies ne sont souvent pas prises en charge par les clients de messagerie. | JavaScript ou Flash n’est pas utilisé dans le modèle de newsletter. |
| Ajoutez une version en texte brut pour l’envoi multipartie. | Un nouveau widget a été intégré aux propriétés de la page pour extraire facilement une version en texte brut du contenu de la page. Vous pouvez l’utiliser comme point de départ pour la version finale en texte brut. |

## Modèles et exemples de newsletter Campaign {#campaign-newsletter-templates-and-examples}

AEM est fourni avec des modèles et des composants clé en main vous permettant de créer des newsletters de campagne. Vous pouvez utiliser ces modèles et composants pour créer vos newsletters personnalisées.

### Modèles {#templates}

Pour offrir une base solide et élargir la variété des possibilités de flux de contenu, trois types de modèles légèrement différents sont disponibles d’usine. Vous pouvez facilement utiliser ces trois types pour créer une newsletter personnalisée.

Tous ont une **header**, un **pied de page**, et a **corps** . Sous la section de corps, chaque modèle diffère en **conception de colonne** (une, deux ou trois colonnes).

![](assets/chlimage_1-69.png)

### Composants {#components}

[Sept composants sont actuellement disponibles dans les modèles de campagne](/help/sites-authoring/adobe-campaign-components.md). Ces composants sont tous basés sur le langage de balisage d’Adobe. **HTL**.

| **Nom du composant** | **Chemin du composant** |
|---|---|
| En-tête | /libs/mcm/campaign/components/heading |
| Image | /libs/mcm/campaign/components/image |
| Texte et personnalisation | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Lien | /libs/mcm/campaign/components/reference |
| Modèle d’image Dynamic Media Classic (anciennement Scene7) | /libs/mcm/campaign/s7image |
| Référence ciblée | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Ces composants sont optimisés pour le contenu de courrier électronique. En d’autres termes, ils respectent les meilleures pratiques décrites dans ce document. L’utilisation d’autres composants prêts à l’emploi enfreint généralement ces règles.

Ces composants sont décrits en détail à la section [Composants Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
