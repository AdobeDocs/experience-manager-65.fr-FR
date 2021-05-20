---
title: AEM - FAQ sur l’intégration de Commerce à l’aide de Commerce Integration Framework
description: AEM - FAQ sur l’intégration de Commerce à l’aide de Commerce Integration Framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45,aece1190-9530-4060-9b08-022da7068987
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 47%

---

# AEM - FAQ sur l’intégration de Commerce à l’aide de Commerce Integration Framework

## 1. CIF GraphQL est-il utilisé uniquement pour le commerce ou sera-t-il disponible pour interroger du contenu créé sur AEM JCR ?

Adobe a adopté les API GraphQL de Magento comme API commerciales officielles pour toutes les données liées au commerce. Par conséquent, AEM utilise GraphQL pour échanger des données commerciales avec Magento et tout moteur de commerce via I/O Runtime. Cette API GraphQL est indépendante de AEM API GraphQL pour accéder aux fragments de contenu.

## 2. Les ressources de produit (images) peuvent-elles être stockées et référencées à partir d’AEM via l’administrateur Adobe Commerce (Magento) ? Comment les ressources issues de Dynamic Media peuvent-elles être utilisées ?

Aucune intégration officielle AEM Assets - Magento n’est disponible. Un connecteur partenaire est disponible sur le [marketplace](https://marketplace.magento.com/bounteous-dam.html).

Vous pouvez également, à titre de solution, stocker des ressources de produit (images) dans AEM Assets, mais vous devrez stocker manuellement les URL de ressources dans Magento. Dynamic Media fait désormais partie d’AEM Assets et fonctionnera de la même manière.

## 3. L’emplacement de déploiement de la solution commerciale est-il important ? (Sur site ou dans le cloud)

Non, l’emplacement de déploiement de votre solution commerciale n’a pas d’importance. Le CIF et le storefront AEM fonctionneront indépendamment du modèle de déploiement. Cependant, si la solution est déployée avec l’architecture de référence E2E recommandée, les tests E2E peuvent s’exécuter par rapport aux indicateurs de performance clés (KPI) de performance qui représentent un profil client d’entreprise type. Vous obtiendrez ainsi des informations supplémentaires qui pourront être utilisées comme référence.

## 4. Comment les pages de catalogues ou de produits sont-elles créées dans AEM ? Comment persistent-elles dans AEM ?

Les pages de catalogues et de produits sont créées et mises en cache dynamiquement dans AEM en fonction de modèles de pages de catalogues et de produits génériques. Aucune donnée de produit ou de catalogue n’est importée et stockée dans AEM.

## 5. Lorsque vous mettez à jour les données de produit dans votre solution commerciale, s’agit-il d’une notification push en temps réel vers AEM ? Ou s’agit-il d’un traitement par lots ?

Le module complémentaire CIF utilisé avec AEM permet aux données de passer de la solution commerciale à AEM à la demande. Par conséquent, il ne s’agit pas d’un traitement push en temps réel ou par lots lorsqu’une mise à jour est disponible dans votre solution commerciale.

## 6. Quelle taille de catalogue AEM-elle avec la prise en charge de CIF ?

Cela dépend de quelques aspects supplémentaires que vous devez prendre en compte. Quel est le taux de cache de vos pages et données de catalogue ? Combien de demandes simultanées attendez-vous aux heures de pointe ? Quelle est l’évolutivité des API de vos solutions commerciales ?

## 7. Comment PIM opère-t-il dans ce framework ?

Les données PIM sont exposées à AEM et aux clients par le biais de requêtes GraphQL. Nous vous recommandons d’intégrer PIM au moteur de commerce (Magento ou autre) afin que les données PIM puissent ensuite être récupérées à partir du moteur de commerce.

## 8. Mettez-vous également en cache les données de tarification et autres données par l’intermédiaire du Dispatcher ? Cela provoque-t-il un problème fréquent d’invalidation du cache ?

Les données dynamiques telles que le prix ou l’inventaire ne sont pas mises en cache dans le Dispatcher. Les données dynamiques sont récupérées côté client avec des composants web directement via les API GraphQL. Seules les données statiques (telles que les données de produit ou de catégorie) sont mises en cache dans le Dispatcher. Si les données de produit sont modifiées, le cache doit être invalidé.

## 9. Comment l’invalidation du cache pour AEM Dispatcher fonctionne-t-elle avec AEM et le commerce ?

Nous vous recommandons de configurer l’invalidation de cache TTL pour les pages mises en cache dans le Dispatcher. Pour les informations dynamiques telles que le prix ou l’inventaire, il est recommandé d’effectuer le rendu de la date côté client. Pour plus d’informations sur l’invalidation de cache TTL, reportez-vous à [AEM Dispatcher](https://helpx.adobe.com/fr/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10. Y a-t-il une recommandation sur la recherche unifiée dans le contenu AEM avec Commerce ?

Une mise en œuvre de référence de recherche de produit est fournie, mais aucune recherche unifiée avec du contenu. Cette fonctionnalité est généralement très spécifique au client et mieux résolue au niveau du projet.

## 11. Comment la recherche fonctionne-t-elle avec AEM et le commerce à l’aide de CIF ?

CIF fournit des composants de barre de recherche et de résultats de recherche. Le composant Barre de recherche envoie une requête GraphQL avec le terme de recherche à la solution de commerce, puis renvoie une liste de produits qui inclut le nom, le prix, le SLUG du produit, etc. Le composant de résultats de recherche affiche ensuite les résultats de la recherche dans une vue de galerie sur une page de résultats de recherche créée dans AEM. La recherche prend en charge la recherche de texte intégral de base. Nous utilisons la clé SLUG/url pour établir une référence au PDP.

## 12. Comment les données de produit peuvent-elles être utilisées dans MSM ou les traductions ?

Les données produit sont généralement déjà traduites dans PIM ou Magento. L’intégration AEM – Magento prend en charge la connexion à plusieurs magasins et vues de magasin Magento. Dans une configuration MSM, généralement un site AEM est lié à une vue de magasin Magento.

## 13. Existe-t-il un moyen d’améliorer les données de produit avec le texte commercial ? Où effectuer cette opération ? Dans AEM ou dans la solution commerciale ?

Nous vous recommandons de gérer les données et le contenu liés au marketing dans AEM. Décorez les données de produit de votre solution commerciale avec des attributs supplémentaires à l’aide de fragments de contenu ou créez et liez des fragments d’expérience pour le contenu non structuré avec vos produits.

## 14. Comment pouvons-nous garantir la conformité PCI lors de l’utilisation d’AEM pour toute la couche de présentation ?

Nous vous recommandons d’utiliser des méthodes de paiement abstraites. Le client du navigateur est ainsi en communication directe avec le fournisseur de passerelle de paiement, de sorte que ni l’Adobe ni les solutions commerciales ne contiennent ni ne transmettent de données de détenteur de carte. Cette approche nécessite uniquement une conformité PCI de niveau 3. Cependant, il existe d’autres aspects à considérer pour assurer une conformité PCI entière, tels que la façon dont les employés interagissent avec le système et les données. Pour plus d’informations sur la conformité PCI Magento, consultez <https://magento.com/pci-compliance>

## 15. Si j’utilise des versions de cloud d’AEM et de Magento, cette solution conjointe est-elle conforme PCI ?

Oui, le questionnaire d’auto-évaluation D et l’attestation de conformité sont disponibles sur demande.

## 16. Comment puis-je demander une licence d’évaluation d’I/O Runtime ?

Vous pouvez demander une licence d’évaluation pour utiliser I/O Runtime [ici](https://adobeio.typeform.com/to/obqgRm).
