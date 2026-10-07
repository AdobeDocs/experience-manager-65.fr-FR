---
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 3%
---
# Recommandations pour la contribution à la documentation de Adobe Experience Manager

## Philosophie de la documentation

Adobe sait que les utilisateurs de Adobe Experience Manager travaillent dans des environnements hautement compétitifs et s’efforcent de créer des expériences digitales qui les distinguent de leurs concurrents. Lorsqu’Adobe fournit de nouveaux outils avancés dans AEM, il est essentiel qu’ils soient complétés par une documentation précise et claire pour permettre au client d’utiliser immédiatement son investissement AEM et maximiser le retour sur investissement.

L’objectif de la documentation d’AEM est de la mettre entre les mains des utilisateurs d’AEM dès que possible. Par conséquent, Adobe donne la priorité à une documentation précise et utilisable et s’efforce de la mettre à jour et de l’améliorer continuellement.

## Contributions à la documentation

Dans le but d’améliorer continuellement la documentation d’AEM, l’ensemble de la communauté des utilisateurs d’AEM est invitée à contribuer à la documentation. Que ce soit par le biais de demandes ou de problèmes d’extraction, les améliorations apportées à la documentation peuvent être des corrections, des clarifications, des extensions et des exemples supplémentaires.

## Normes de documentation

Bien qu’Adobe accueille favorablement les contributions à notre documentation, toute contribution à la documentation d’AEM, que ce soit sous la forme d’une demande d’extraction ou d’un problème, doit être conforme à nos normes de contribution et de documentation.

Les contributions qui ne répondent pas à ces normes peuvent être refusées.

### Documentez les cas d’utilisation standard.

La documentation d’AEM couvre les cas d’utilisation standard. Les cas d’utilisation ne relevant pas de l’installation et de l’utilisation standard du produit ne font pas partie de la documentation d’AEM.

### La documentation ne documente généralement pas les bogues ou leurs solutions.

La documentation d’AEM couvre les cas d’utilisation standard. Pour cette raison, les bogues, les effets causés par les bogues et les solutions de contournement des bogues ne sont généralement pas documentés.

Les exceptions à cette règle s’appliquent aux notes de mise à jour dans lesquelles les problèmes connus peuvent être répertoriés avec les solutions possibles qui ont été approuvées par la gestion des produits AEM.

### Les contributions à la documentation ne sont pas destinées à répondre à des questions techniques.

Toutes les idées que vous pourriez avoir pour améliorer la documentation d’AEM sont les bienvenues en tant que contributions. Toutefois, les commentaires, les problèmes et les demandes d’extraction sont destinés uniquement aux *contributions*. Ils ne sont pas destinés à être utilisés pour répondre à vos questions sur l’utilisation d’AEM, la mise en œuvre de votre projet AEM ou la résolution de problèmes techniques.

Toute question relative à l’utilisation d’AEM ou à la résolution d’erreurs techniques doit être soumise au moyen du processus d’assistance classique via le portail d’assistance [Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=fr#support) ou posée à la communauté [Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***Les contributions à la documentation d’AEM ne remplacent pas celles du service clientèle d’Adobe*** et toute contribution de ce type visant à obtenir des réponses à des questions d’assistance sera refusée.

### Les contributions doivent clairement faire référence aux pages de documentation concernées.

Si vous créez un problème afin de suggérer des améliorations à la documentation, vous devez inclure des liens vers les pages affectées. Si vous créez un problème à l’aide du lien **Modifier cette page** sur une page de documentation, le problème est automatiquement créé avec un lien vers la page.

Cela ne s’applique pas aux demandes d’extraction, car les demandes d’extraction, par leur nature, font référence aux pages affectées.

## Instructions de documentation

Nous demandons que toute contribution à notre documentation respecte certaines directives de style.

Le respect de ces instructions facilite la révision de votre contribution et, par conséquent, l’intégration à notre documentation est plus rapide.

### Langue et style

#### Langue

* La documentation d’AEM est rédigée et conservée en anglais (États-Unis).
* Veillez à ce que les phrases soient aussi simples que possible.
* Gardez le langage clair et concis.

Souvenez-vous que les lecteurs de la documentation d’AEM sont internationaux et ne peuvent pas être des locuteurs anglais natifs ou bilingues. Évitez les termes familiers et veillez à ce qu&#39;ils soient aussi clairs et simples que possible.

#### Suivez le manuel de style de ®.

Le [Manuel de style de Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) est un guide de style de documentation disponible gratuitement qui se concentre sur la documentation logicielle et la documentation AEM suit ce guide dans la mesure du possible.

### Mise en forme

| Élément | Style |
|---|---|
| Élément ou option de l’interface utilisateur | **gras** |
| Nom de fichier, chemin, entrée utilisateur, valeurs de paramètre | `monospaced` |
| Code, ligne de commande | ```Code Block``` |

### Copies d’écran

Les captures d’écran doivent être utilisées de manière judicieuse et uniquement lorsqu’une description textuelle est insuffisante.

N’utilisez pas de marqueurs ou d’autres annotations dans les captures d’écran (comme les cadres rouges, les flèches ou le texte). Ainsi, les captures d’écran sont plus faciles à réutiliser ou à répliquer dans les versions localisées de la documentation.

### Références spécifiques à la version

Dans la mesure du possible, évitez toute référence directe à une version spécifique dans le contenu de la documentation. Cela rend la documentation plus flexible et extensible pour les versions ultérieures.

### Utilisation de Day, AEM, CQ, CRX

Le produit doit toujours être désigné par son nom complet **&#x200B;**&#x200B;pour la première fois dans un article et peut ensuite être appelé **AEM**.

N’utilisez pas Day, Day Software, CQ et CRX sauf si cela est inévitable, comme dans les noms de classe ou en référence à l’historique d’AEM.