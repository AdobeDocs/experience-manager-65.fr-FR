---
title: Intégration d’AEM et de Commerce à l’aide de Commerce Integration Framework – FAQ
description: Intégration d’AEM et de Commerce à l’aide de Commerce Integration Framework – FAQ
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 80%

---

# Intégration d’AEM et de Commerce à l’aide de Commerce Integration Framework – FAQ

## &#x200B;1. CIF GraphQL est-il utilisé uniquement pour le commerce ou est-il disponible pour interroger du contenu créé sur AEM JCR ?

Adobe a adopté les API GraphQL d’Adobe Commerce en tant qu’API commerciales officielles pour toutes les données liées au commerce. Par conséquent, AEM utilise GraphQL pour échanger des données commerciales avec Adobe Commerce et tout moteur de commerce via I/O Runtime. Cette API GraphQL est indépendante de l’API GraphQL AEM pour accéder aux fragments de contenu.

## &#x200B;2. Les ressources de produit (images) peuvent-elles être stockées et référencées à partir d’AEM via l’administration Adobe Commerce ? Comment les ressources issues de Dynamic Media peuvent-elles être utilisées ?

Aucune intégration officielle AEM Assets - Adobe Commerce n’est disponible. Un connecteur partenaire est disponible sur la [marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

Pour pallier ce problème, vous pouvez stocker les ressources de produit (images) dans AEM Assets, mais vous devrez stocker manuellement les URL de ressources dans Adobe Commerce. Dynamic Media fait partie d’AEM Assets et fonctionne de la même manière.

## &#x200B;3. L’emplacement de déploiement de la solution de commerce a-t-il une importance ? (Sur site ou dans le cloud)

Non, l’emplacement de déploiement de votre solution de commerce n’a pas d’importance. Le CIF et le storefront AEM fonctionneront indépendamment du modèle de déploiement. Cependant, si la solution est déployée avec l’architecture de référence de bout en bout recommandée, les tests de bout en bout peuvent s’exécuter par rapport aux KPI qui représentent un profil client d’entreprise type. Ce processus permet d’obtenir des informations supplémentaires qui pourront être utilisées comme référence.

## &#x200B;4. Comment les pages de catalogue ou de produits sont-elles créées dans AEM ? Comment persistent-elles dans AEM ?

Les pages de catalogues et de produits sont créées et mises en cache dynamiquement dans AEM en fonction de modèles de pages de catalogues et produits génériques. Aucune donnée de produit ni de catalogue n’est importée et stockée dans AEM.

## &#x200B;5. La mise à jour des données de produit dans votre solution de commerce correspond-elle à un transfert Push en temps réel vers AEM ? Ou s’agit-il d’un traitement par lots ?

Le module complémentaire CIF utilisé avec AEM permet aux données de transiter de la solution de commerce à AEM, et ce, à la demande. Par conséquent, ce workflow nest pas un transfert de notifications push en temps réel ni un traitement par lots dans le cas d’une mise à jour dans votre solution de commerce.

## &#x200B;6. Quelle taille de catalogue AEM avec CIF prend-il en charge ?

La prise en charge de la taille du catalogue dépend de quelques aspects supplémentaires que vous devez prendre en compte. Quel est le ratio de cache de vos pages et données de catalogue ? Combien de demandes simultanées attendez-vous aux heures de pointe ? Quelle est l’évolutivité des API de vos solutions de commerce ?

## &#x200B;7. Comment PIM entre-t-il dans ce framework ?

Les données PIM sont exposées à AEM et aux clients et aux clientes par le biais de requêtes GraphQL. Nous recommandons d’intégrer PIM au moteur de commerce (Adobe Commerce ou autres) afin que les données PIM puissent être récupérées à partir de ce dernier.

## &#x200B;8. Mettez-vous également en cache les prix et d’autres données via Dispatcher ? Cela provoque-t-il un problème fréquent d’invalidation du cache ?

Les données dynamiques telles que le prix ou l’inventaire ne sont pas mises en cache dans le Dispatcher. Les données dynamiques sont récupérées côté client avec des composants web directement via les API GraphQL. Seules les données statiques (telles que les données de produit ou de catégorie) sont mises en cache dans le Dispatcher. Si les données relatives au produit changent, l’invalidation du cache est nécessaire.

## &#x200B;9. Comment l’invalidation du cache pour AEM Dispatcher fonctionne-t-elle avec AEM et commerce ?

Nous vous recommandons de configurer l’invalidation de cache TTL pour les pages mises en cache dans le Dispatcher. Pour les informations dynamiques telles que le prix ou l’inventaire, il est recommandé d’effectuer le rendu de la date côté client. Pour plus d’informations sur l’invalidation de cache TTL, consultez [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=fr).

## &#x200B;10. Existe-t-il des recommandations sur la recherche unifiée dans le contenu AEM avec Commerce ?

Une mise en œuvre de référence de recherche de produit est fournie, mais aucune recherche unifiée avec du contenu. Cette fonctionnalité est spécifique au client ou à la cliente et est mieux résolue au niveau d’un projet spécifique.

## &#x200B;11. Comment la recherche fonctionne-t-elle avec AEM et Commerce à l’aide de CIF ?

CIF fournit des composants de barre de recherche et de résultats de recherche. Le composant barre de recherche envoie une requête GraphQL avec le terme de recherche à la solution de commerce, puis renvoie une liste de produits qui inclut le nom, le prix, le SLUG, etc. Le composant de résultats de recherche affiche ensuite les résultats de la recherche dans une vue de galerie sur une page de résultats de recherche créée dans AEM. La recherche prend en charge la recherche de texte intégral de base. Utilisez la clé SLUG/url pour établir une référence au PDP.

## &#x200B;12. Comment les données de produit peuvent-elles être utilisées dans MSM ou les traductions ?

Les données de produit sont déjà traduites dans PIM ou dans Adobe Commerce. L’intégration AEM - Adobe Commerce prend en charge la connexion à plusieurs magasins et vues de magasin Adobe Commerce. Dans une configuration MSM, un site AEM est généralement lié à une vue de magasin Adobe Commerce.

## &#x200B;13. Existe-t-il un moyen d’améliorer les données de produit avec le texte commercial ? Si c’est le cas, où est-ce effectué ? Dans AEM ou dans la solution de commerce ?

Adobe recommande de gérer les données et le contenu liés au marketing dans AEM. Décorez les données de produit de votre solution commerciale avec des attributs supplémentaires à l’aide de fragments de contenu ou créez et liez des fragments d’expérience pour le contenu non structuré avec vos produits.

## &#x200B;14. Comment une entreprise garantit-elle la conformité PCI lors de l’utilisation d’AEM pour l’ensemble de la couche de présentation ?

Adobe recommande d’utiliser des modes de paiement abstraits. Le client ou la cliente du navigateur est ainsi en communication directe avec le fournisseur de la passerelle de paiement, de sorte qu’Adobe ne détient ni ne transmet les données du ou de la titulaire de la carte, pas plus que les solutions de commerce. Cette approche nécessite uniquement une conformité PCI de niveau 3. Cependant, il existe d’autres aspects à considérer pour assurer une conformité PCI entière, tels que la façon dont les employé(e)s interagissent avec le système et les données. Pour plus d’informations sur la conformité PCI d’Adobe Commerce, reportez-vous à la section [Exigences de conformité PCI](https://business.adobe.com/fr/products/magento/pci-compliance.html).

## &#x200B;15. Si j’utilise des versions cloud d’AEM et d’Adobe Commerce, cette solution conjointe est-elle conforme PCI ?

Oui, le questionnaire d’auto-évaluation D et l’attestation de conformité sont disponibles sur demande.

## &#x200B;16. Comment puis-je demander une licence d’évaluation d’I/O Runtime ?

Voir la section [Obtenir l’accès](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/) pour plus d’informations sur la demande d’une licence d’évaluation pour utiliser I/O Runtime.
