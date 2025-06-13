---
title: Mode de développement
description: Le mode de développement ouvre un panneau latéral avec plusieurs onglets qui procurent au développeur ou à la développeuse des informations sur la page en cours.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 99%

---

# Mode de développement{#developer-mode}

Lors de la modification de pages dans Adobe Experience Manager (AEM), plusieurs [modes](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) sont disponibles, y compris le mode de développement. Le mode de développement ouvre un panneau latéral avec plusieurs onglets qui procurent des informations techniques sur la page en cours. Les trois onglets sont les suivants :

* **[Composants](#components)**, pour visualiser les informations de structure et de performances.
* **[Tests](#tests)**, pour exécuter des tests et analyser les résultats.
* **[Erreurs](#errors)**, pour afficher les problèmes rencontrés.

Ils aident les développeurs à :

* découvrir la composition des pages ;
* déboguer en vérifiant la nature des événements, ainsi que leur emplacement et le moment où ils surviennent, afin de résoudre des problèmes ;
* Test : l’application se comporte-t-elle comme prévu ?

>[!CAUTION]
>
>Le mode Développeur :
>
>* n’est disponible que dans l’interface utilisateur tactile (lors de la modification de pages) ;
>* n’est pas disponible sur les appareils mobiles ou les petites fenêtres sur les ordinateurs de bureau (en raison de l’espace restreint),
>
>   * ce qui se produit lorsque la largeur est inférieure à 1 024 px ;
>* n’est disponible que pour les utilisateurs qui sont membres du groupe `administrators`.

>[!CAUTION]
>
>Le mode Développeur n’est disponible que sur une instance de création standard qui n’utilise pas le mode d’exécution nosamplecontent.
>
>Si nécessaire, il peut être configuré pour être utilisé comme suit :
>
>* sur une instance de création à l’aide du mode d’exécution nosamplecontent ;
>* sur une instance de publication.
>
>Il doit être désactivé à nouveau après utilisation.

>[!NOTE]
>
>Voir :
>
>* l’article de la base de connaissances [Résolution des problèmes liés à l’IU tactile d’AEM](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-16935) pour découvrir d’autres conseils et outils.
>* Session AEM Gems concernant le [mode Développeur d’AEM 6.0](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-developer-mode.html?lang=fr).
>

## Ouvrir le mode Développeur {#opening-developer-mode}

Le mode Développeur est implémenté sous la forme d’un panneau latéral dans l’éditeur de page. Pour ouvrir le panneau, sélectionnez **Développeur** dans le sélecteur de mode au niveau de la barre d’outils de l’éditeur de page :

![chlimage_1-11](assets/chlimage_1-11.png)

Le panneau est divisé en deux onglets :

* **[Composants](/help/sites-developing/developer-mode.md#components)** : il présente une arborescence de composants, similaire à l’[arborescence de contenu](/help/sites-authoring/author-environment-tools.md#content-tree) pour les auteurs.

* **[Erreurs](/help/sites-developing/developer-mode.md#errors)** : lorsque des problèmes se produisent, les détails sont affichés pour chaque composant.

### Composants {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

Il présente une arborescence de composants qui :

* décrit la chaîne de composants et de modèles rendus sur la page (SLY, JSP, etc.) ; L’arborescence peut être développée pour afficher le contexte dans la hiérarchie.
* affiche le temps de calcul côté serveur nécessaire au rendu du composant ;
* permet de développer l’arborescence et de sélectionner des composants spécifiques dans l’arborescence. La sélection permet d’accéder aux détails du composant, par exemple :

   * le chemin du référentiel ;
   * les liens vers les scripts (accessibles dans CRXDE Lite)

* Les composants sélectionnés (dans le flux de contenu, indiqués par une bordure bleue) sont mis en surbrillance dans l’arborescence de contenu (et inversement).

Cela peut vous aider à :

* déterminer et comparer le temps de rendu par composant ;
* visualiser et comprendre la hiérarchie ;
* comprendre, puis améliorer, le temps de chargement de la page en recherchant les composants lents.

Chaque entrée de composant peut afficher (par exemple) :

![chlimage_1-13](assets/chlimage_1-13.png)

* **Afficher les détails** : lien vers une liste qui affiche :

   * tous les scripts de composants utilisés pour le rendu du composant ;
   * le chemin du contenu de référentiel pour ce composant spécifique.

  ![chlimage_1-14](assets/chlimage_1-14.png)

* **Modifier le script** : un lien qui :

   * ouvre le script de composant dans CRXDE Lite.

* Le développement d’une entrée de composant (flèche) peut également afficher :

   * la hiérarchie au sein du composant sélectionné ;
   * les temps de rendu pour le composant sélectionné de manière isolée, tous les composants individuels imbriqués qu’il contient, ainsi que le total combiné.

  ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>Certains liens pointent sur des scripts sous `/libs`. Toutefois, ils servent uniquement de référence, vous **ne devez rien** modifier sous `/libs`, car toutes les modifications que vous apportez risquent d’être perdues. Cela est dû au fait que cette branche est exposée aux modifications à chaque mise à niveau ou application d’un correctif ou pack de fonctionnalités. Apportez les modifications requises sous `/apps`. Voir [Recouvrements et remplacements](/help/sites-developing/overlays.md).

### Erreurs {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

L’onglet **Erreurs** devrait toujours rester vide (comme ci-dessus), mais lorsque des problèmes surviennent, les informations suivantes sont affichées pour chaque composant :

* Un avertissement s’affiche si le composant écrit une entrée dans le journal d’erreurs, avec les détails de l’erreur et des liens directs vers le code correspondant dans CRXDE Lite.
* Un avertissement s’affiche si le composant ouvre une session d’administrateur.

Par exemple, dans une situation où une méthode non définie est appelée, l’erreur résultante s’affiche dans l’onglet **Erreurs** :

![chlimage_1-17](assets/chlimage_1-17.png)

L’entrée du composant dans l’arborescence de l’onglet Composants est également marquée avec un indicateur lorsqu’une erreur se produit.

### Tests {#tests}

>[!CAUTION]
>
>Dans AEM 6.2, les fonctionnalités de test du mode de développement ont été réimplémentées en tant qu’application autonome Outils.
>
>Pour en savoir plus, consultez [Test de l’IU](/help/sites-developing/hobbes.md).
