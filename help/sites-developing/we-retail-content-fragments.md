---
title: Test des fragments de contenu dans We.Retail
description: Test des fragments de contenu dans We.Retail
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 70%

---

# Test des fragments de contenu dans We.Retail{#trying-out-content-fragments-in-we-retail}

Les fragments de contenu vous permettent de créer du contenu neutre pour les canaux, ainsi que des variantes (éventuellement spécifiques aux canaux). **We.Retail** (comme disponible dans une instance prête à l’emploi de Adobe Experience Manager) fournit le fragment **Le surf arctique à Lofoten** comme exemple de base. Cela illustre que :

* Les fragments de contenu Adobe Experience Manager (AEM) sont [créés et gérés en tant que ressources indépendantes de la page](/help/assets/content-fragments/content-fragments.md). Ils vous permettent de créer du contenu neutre pour les canaux, ainsi que des variantes (éventuellement spécifiques aux canaux).

   * Consultez la section [Emplacement des ressources de Fragment de contenu dans We.Retail](#where-to-find-content-fragments-in-we-retail).

* Vous pouvez ensuite [utiliser ces fragments et leurs variantes lors de la création](/help/sites-authoring/content-fragments.md) de vos pages de contenu.

   * Consultez la section [Où les fragments de contenu sont-ils utilisés dans We.Retail](#where-content-fragments-are-used-in-we-retail).

Pour obtenir la documentation complète sur la création, la gestion, l’utilisation et le développement de fragments de contenu :

* Consultez la section [Informations supplémentaires](#further-information).

>[!NOTE]
>
>Les **fragments de contenu** et les **[fragments d’expérience](/help/sites-authoring/experience-fragments.md)** représentent deux fonctions distinctes d’AEM :
>
>* **Fragments de contenu** sont du contenu éditorial, principalement du texte et des images associées. Il s’agit de contenu pur, sans conception ni mise en page.
>* Les **fragments d’expérience** désignent un contenu parfaitement mis en page : un fragment de page web.
>
>Les fragments d’expérience peuvent être composés de contenu sous la forme de fragments de contenu, mais pas l’inverse.

## Emplacement des fragments de contenu dans We.Retail {#where-to-find-content-fragments-in-we-retail}

We.Retail comprend plusieurs échantillons de fragments de contenu ; accédez à **Ressources**, **Fichiers**, **We.Retail**, **Anglais**, **Expériences**.

Vous y trouverez notamment **Arctic Surfing in Lofoten**, un fragment avec des ressources visuelles associées :

* Navigation par le biais de **Ressources**, **Fichiers**, **We.Retail**, **Anglais**, **Expériences**, **Le surf arctique à Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Vous pouvez sélectionner et modifier le fragment **Arctic Surfing in Lofoten** :

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Ici, vous pouvez [modification et gestion](/help/assets/content-fragments/content-fragments.md) votre fragment à l’aide des onglets (panneau de gauche) :

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variations](/help/assets/content-fragments/content-fragments-variations.md)**, y compris [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) 
* **[Contenu associé](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Métadonnées](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Emplacement d’utilisation des fragments de contenu dans We.Retail {#where-content-fragments-are-used-in-we-retail}

Illustration [création de page avec un fragment de contenu](/help/sites-authoring/content-fragments.md) plusieurs exemples de pages sont proposés sous, par exemple :

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Le fragment de contenu **Arctic Surfing in Lofoten**, par exemple, est référencé sur la page Sites :

* Accédez à **Sites**, **We.Retail**, **Gabarits de langue**, **Anglais**, **Expérience**. Ouvrez ensuite le fragment **Arctic Surfing in Lofoten** en vue de le modifier :

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Informations supplémentaires {#further-information}

Pour plus d’informations, voir :

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)

   * Découvrez comment créer, modifier et gérer vos ressources de fragment de contenu.

* [Création de page à partir de fragments de contenu](/help/sites-authoring/content-fragments.md)

   * Utilisez votre fragment de contenu lors de la création d’une page.

* [Développement de composants AEM pour les fragments de contenu](/help/sites-developing/components-content-fragments.md)

   * Une présentation des composants pour les fragments de contenu.

* [Développement et extension de fragments de contenu](/help/sites-developing/customizing-content-fragments.md)

   * Les informations de cette section vous aident à développer et à étendre des fragments de contenu.
