---
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 61%

---
# Instructions relatives à la contribution à la documentation d’Adobe Experience Manager

## Philosophie de la documentation

Adobe sait que les utilisateurs de Adobe Experience Manager travaillent dans des environnements très concurrentiels, afin de créer des expériences numériques qui les distinguent de leurs concurrents. Par conséquent, il est essentiel que, lorsque Adobe fournit de nouveaux outils avancés dans AEM, ces outils soient complétés par une documentation précise et claire pour permettre au client d’utiliser immédiatement son investissement AEM et maximiser le ROI.

L’objectif de la documentation AEM est de la placer entre les mains des utilisateurs d’AEM dès que possible. Par conséquent, Adobe donne la priorité à une documentation précise et utilisable et s’efforce de la mettre à jour et de l’améliorer continuellement.

## Contributions à la documentation

Afin d’améliorer continuellement la documentation d’AEM, toute la communauté des utilisateurs d’AEM peut apporter sa contribution. Que ce soit par le biais de demandes d’extraction ou de demandes, les améliorations apportées à la documentation peuvent être des corrections, des clarifications, des extensions et des exemples supplémentaires.

## Normes de la documentation

Bien qu’Adobe accueille favorablement les contributions à notre documentation, toute contribution à la documentation d’AEM, sous la forme d’une demande d’extraction ou d’un problème, doit être conforme à nos normes de contribution et de documentation.

Les contributions qui ne satisfont pas à ces normes peuvent être rejetées.

### Cas d’utilisation standard du document.

La documentation d’AEM couvre les cas d’utilisation standard. Les cas d’utilisation au-delà de la portée de l’installation et de l’utilisation standard du produit ne font pas partie de la documentation AEM.

### La documentation ne documente généralement pas les bogues ni leurs solutions.

La documentation d’AEM couvre les cas d’utilisation standard. Pour cette raison, les bogues, les effets causés par les bogues et les solutions aux bogues ne sont généralement pas documentés.

Les exceptions à cette règle concernent les notes de mise à jour qui répertorient les problèmes connus ainsi que les solutions possibles après approbation par l’équipe de gestion des produits AEM.

### Les contributions à la documentation ne sont pas destinées à répondre aux questions techniques.

Toute opinion susceptible d’améliorer la documentation AEM est la bienvenue sous forme de contributions. Toutefois, les commentaires, les demandes et les demandes d’extraction sont destinés uniquement aux *contributions*. Leur finalité n’est pas de répondre à vos questions sur l’utilisation et la mise en œuvre d’AEM ou la résolution de problèmes techniques.

Toute question relative à l’utilisation d’AEM ou à la résolution d’erreurs techniques doit être soumise au moyen du processus d’assistance classique via le [Portail d’assistance d’Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou posée à la [communauté Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=fr).

***Les contributions à la documentation d’AEM ne remplacent pas celles du service clientèle Adobe*** et toute contribution de ce type qui recherche des réponses aux questions liées au support technique sera rejetée.

### Les contributions doivent clairement référencer les pages de documentation concernées.

Si vous créez une demande pour suggérer des améliorations à la documentation, vous devez inclure des liens vers les pages concernées. Si vous créez un problème en utilisant la variable **Modifier cette page** sur une page de documentation, le problème est automatiquement créé avec un lien vers la page.

Cette méthode ne s’applique pas aux requêtes d’extraction qui, par nature, font référence aux pages concernées.

## Directives relatives à la documentation

Nous demandons que toutes les contributions à notre documentation suivent certaines directives de style.

Suivre ces directives facilite la révision et l’intégration rapide de votre contribution dans notre documentation.

### Langue et style

#### Langue

* La documentation AEM est créée et conservée en anglais américain.
* Veillez à ce que les expressions restent le plus simple possible.
* Restez clair et concis.

N’oubliez pas que les lecteurs de la documentation AEM sont internationaux et ne peuvent pas être des locuteurs anglais natifs ou bilingues. Évitez les expressions familières et restez aussi clair et simple que possible.

#### Suivez le guide de style de Microsoft®

[Le guide de style de Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) est un guide de style de documentation gratuit qui se concentre sur la documentation logicielle et AEM documentation suit ce guide dans la mesure du possible.

### Mise en forme

| Élément | Style |
|---|---|
| Élément ou option de l’interface utilisateur | **gras** |
| Nom de fichier, chemin, entrée utilisateur, paramètre-valeurs | `monospaced` |
| Code, ligne de commande | ```Code Block``` |

### Captures d’écran

Les captures d’écran doivent être utilisées de manière judicieuse et uniquement lorsqu’une description textuelle est insuffisante.

N’utilisez pas de marqueurs ni d’autres annotations dans les captures d’écran (comme les cadres rouges, les flèches ou le texte). Ainsi, les captures d’écran sont plus faciles à réutiliser ou à répliquer dans les versions localisées de la documentation.

### Références spécifiques à la version

Dans la mesure du possible, évitez toute référence directe à une version spécifique dans tout le contenu de la documentation. La documentation est ainsi plus flexible et extensible pour les versions ultérieures.

### Utilisation de Day, AEM, CQ, CRX

Le produit doit toujours être référencé par son nom complet **Adobe Experience Manager** pour la première fois dans un article et peut ensuite être appelé **AEM**.

N’utilisez pas Day, Day Software, CQ et CRX, sauf lorsque cela est inévitable, par exemple dans les noms de classe ou en faisant référence à l’historique de l’AEM.