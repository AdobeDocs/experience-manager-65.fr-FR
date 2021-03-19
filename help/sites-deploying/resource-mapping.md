---
title: Mappage de ressource
seo-title: Mappage de ressource
description: Découvrez comment définir des redirections, des URL Vanity et les hôtes virtuels pour AEM à l’aide du mappage de ressource.
seo-description: Découvrez comment définir des redirections, des URL Vanity et les hôtes virtuels pour AEM à l’aide du mappage de ressource.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuration
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 66%

---


# Mappage de ressources{#resource-mapping}

Le mappage de ressource permet de définir des redirections, des URL Vanity et des hôtes virtuels pour AEM.

Par exemple, vous pouvez utiliser ces mappages pour :

* Ajoutez un préfixe `/content` à toutes les requêtes afin que la structure interne soit masquée des visiteurs vers votre site Web.
* Définissez une redirection de sorte que toutes les requêtes envoyées à la page `/content/en/gateway` de votre site Web soient redirigées vers `https://gbiv.com/`.

Un mappage HTTP possible préfixe toutes les requêtes à `localhost:4503` avec `/content`. Un mappage de ce type peut être utilisé pour masquer la structure interne vis-à-vis des visiteurs du site web, car il rend :

`localhost:4503/content/we-retail/en/products.html`

accessible à l’aide de :

`localhost:4503/we-retail/en/products.html`

car le mappage ajoute automatiquement le préfixe `/content` à `/we-retail/en/products.html`.

>[!CAUTION]
>
>Les URL Vanity ne prennent pas en charge les modèles regex.

>[!NOTE]
>
>Voir la documentation Sling et les sections [Mappages pour la résolution de ressource](https://sling.apache.org/site/resources.html) et [Ressources](https://sling.apache.org/site/mappings-for-resource-resolution.html) pour plus d’informations.

## Affichage des définitions du mappage {#viewing-mapping-definitions}

Les mappages forment deux listes que le résolveur de ressources JCR analyse (du haut vers le bas) pour trouver une correspondance.

Ces listes peuvent être visualisées (avec les informations de configuration) sous l&#39;option **JCR ResourceResolver** de la console Felix ; par exemple, `https://<*host*>:<*port*>/system/console/jcrresolver` :

* Configuration indique la configuration actuelle (telle que définie pour [le résolveur de ressource Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)). 

* Test de configuration. Cela permet de saisir une URL ou un chemin d’accès vers la ressource. Cliquez sur **Résoudre** ou **Mapper** pour confirmer la façon dont le système transforme l’entrée.

* **Resolver Map Entries (Entrées de mappage du résolveur)** La liste des entrées utilisées par les méthodes ResourceResolver.resolve pour mapper les URL aux ressources. 

* **Mapping Map Entries (Entrées de mappage)** La liste des entrées utilisées par les méthodes ResourceResolver.map pour mapper les chemins d’accès des ressources aux URL.

Les deux listes affichent différentes entrées, y compris celles définies par défaut par les applications. Cela vise souvent à simplifier les URL pour l’utilisateur. 

Les listes associe **un modèle**, une expression régulière correspondant à la demande, avec **un remplacement** qui définit la redirection à appliquer.

Par exemple :

**Modèle** `^[^/]+/[^/]+/welcome$`

déclenche :

**Remplacement** `/libs/cq/core/content/welcome.html`.

pour rediriger une requête :

`https://localhost:4503/welcome` ``

vers:

`https://localhost:4503/libs/cq/core/content/welcome.html`

De nouvelles définitions de mappage sont créées dans le référentiel.

>[!NOTE]
>
>Il existe de nombreuses ressources qui permettent d&#39;expliquer comment définir les expressions ordinaires ; par exemple [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Création des définitions de mappage dans AEM {#creating-mapping-definitions-in-aem}

Dans une installation d’AEM standard, vous pouvez trouver le dossier :

`/etc/map/http`

Il s’agit de la structure utilisée lors de la définition des mappages pour le protocole HTTP. D&#39;autres dossiers ( `sling:Folder`) peuvent être créés sous `/etc/map` pour tout autre protocole que vous souhaitez mapper.

#### Configuration d’une redirection interne vers /content {#configuring-an-internal-redirect-to-content}

Pour créer le mappage qui préfixe toute requête à https://localhost:4503/ avec `/content` :

1. A l’aide de CRXDE, accédez à `/etc/map/http`.

1. Créez un nœud :

   * **Type** `sling:Mapping` ce type de nœud est conçu pour de tels mappages, même si son utilisation n’est pas obligatoire.

   * **Nom** `localhost_any`

1. Cliquez sur **Enregistrer tout**.
1. **Ajoutez** les propriétés suivantes à ce nœud :

   * **Nom** `sling:match`

      * **Type** `String`

      * **Valeur** `localhost.4503/`
   * **Nom** `sling:internalRedirect`

      * **Type** `String`

      * **Valeur** `/content/`


1. Cliquez sur **Enregistrer tout**.

Cela permettra de traiter une demande telle que :
`localhost:4503/geometrixx/en/products.html`
comme si :
`localhost:4503/content/geometrixx/en/products.html`
avait été demandé.

>[!NOTE]
>
>Voir [Ressources](https://sling.apache.org/site/mappings-for-resource-resolution.html) dans la documentation Sling pour plus d’informations sur les propriétés sling disponibles et leur configuration.

>[!NOTE]
>
>Vous pouvez utiliser `/etc/map.publish` pour conserver les configurations de l’environnement de publication. Ils doivent ensuite être répliqués et le nouvel emplacement ( `/etc/map.publish`) configuré pour l&#39;**emplacement de mappage** de l&#39;[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) de l&#39;environnement de publication.

