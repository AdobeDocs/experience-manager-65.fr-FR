---
title: Prévenir les attaques CSRF
description: Découvrez comment empêcher les attaques CSRF (Cross-site request forgery) et protéger les données utilisateur contre les compromis.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 18%

---

# Prévenir les attaques CSRF {#preventing-csrf-attacks}

## Fonctionnement des attaques CSRF {#how-csrf-attacks-work}

La falsification de requête intersite (CSRF) est une vulnérabilité de site web dans laquelle le navigateur d’un utilisateur valide est utilisé pour envoyer une requête malveillante, par exemple via un iFrame. Étant donné que le navigateur envoie les cookies sur une base de domaine, si l’utilisateur est connecté à une application, les données de l’utilisateur peuvent être compromises.

Supposons, par exemple, que vous soyez connecté à Administration Console dans un navigateur. Vous recevez un message électronique contenant un lien. Cliquez sur le lien pour ouvrir un nouvel onglet dans votre navigateur. La page que vous avez ouverte contient un iFrame masqué qui émet une requête malveillante au serveur Forms à l’aide du cookie de votre session forms authentifiée. Comme User Management reçoit un cookie valide, il transmet la demande.

## Termes liés aux CSRF {#csrf-related-terms}

**Référent :** adresse de la page source à partir de laquelle la requête est envoyée. Par exemple, une page web sur site1.com contient un lien vers site2.com. Un clic sur le lien envoie une requête à site2.com. Le référent de cette requête est site1.com, car la requête provient d’une page dont la source est site1.com.

**URI Placés sur la liste autorisée :** Les URI identifient les ressources sur le serveur Forms qui sont demandées, par exemple /adminui ou /contentspace. Certaines ressources peuvent autoriser des requêtes à entrer dans l’application à partir de sites Web externes. Ces ressources sont considérées comme des URI placés sur la liste autorisée. Le serveur Forms n’effectue jamais de vérification de référent à partir d’URI placés sur la liste autorisée.

**Référent nul :** Lorsque vous ouvrez une nouvelle fenêtre ou un nouvel onglet de navigateur, puis saisissez une adresse et appuyez sur Entrée, le référent est nul. La demande est entièrement nouvelle et ne provient pas d’une page Web parente ; il n’existe donc aucun référent pour la requête. Le serveur Forms peut recevoir un référent null de :

* demandes effectuées sur des points de terminaison SOAP ou REST depuis Acrobat
* lorsqu’un utilisateur final effectue une requête HTTP sur un point d’entrée SOAP ou REST AEM Forms ;
* lorsqu’une nouvelle fenêtre de navigateur est ouverte et que l’URL de toute page de connexion de l’application web d’AEM forms est saisie.

Autoriser un référent null sur les points de terminaison SOAP et REST. Autorisez également un référent null sur toutes les pages de connexion URI telles que /adminui et /contentspace et leurs ressources mappées correspondantes. Par exemple, le servlet mappé pour /contentspace est /contentspace/faces/jsp/login.jsp, qui doit être une exception de référent nulle. Cette exception n’est requise que si vous activez le filtrage par GET pour votre application web. Vos applications peuvent indiquer s’il faut autoriser les référents nuls. Voir « Protection contre les attaques multisites par usurpation de requête (CSRF) » dans [Renforcement et sécurité dʼAEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/HardeningSecurity/index.html).

**Exception de référent autorisé :** L’exception de référent autorisé est une sous-liste de la liste des référents autorisés, à partir de laquelle les requêtes sont bloquées. Les exceptions aux référents autorisés sont spécifiques à une application Web. Si un sous-ensemble des référents autorisés ne doit pas être autorisé à appeler une application web spécifique, vous pouvez placer sur la liste bloquée les référents au moyen des exceptions aux référents autorisés. Les exceptions aux référents autorisés sont spécifiées dans le fichier web.xml de votre application. (voir « Protection contre les attaques multisites par usurpation de requête (CSRF) » dans Renforcement et sécurité dʼAEM Forms sur la page Aide et didacticiels).

## Fonctionnement des référents autorisés {#how-allowed-referers-work}

AEM Forms fournit le filtrage des référents, ce qui peut aider à empêcher les attaques CSRF. Le filtrage des référents fonctionne comme suit :

1. Le serveur Forms vérifie la méthode HTTP utilisée pour l’appel :

   * S’il est POST, le serveur Forms vérifie l’en-tête du référent.
   * S’il est GET, le serveur Forms ignore la vérification du référent, sauf si CSRF_CHECK_GETS est défini sur true, auquel cas il vérifie l’en-tête du référent. La variable CSRF_CHECK_GETS est spécifiée dans le fichier web.xml pour votre application. (Voir « Protection contre les attaques multisites par usurpation de requête (CSRF) » dans le [Guide de renforcement et de sécurité](https://help.adobe.com/fr_FR/livecycle/11.0/HardeningSecurity/index.html).)

1. Le serveur Forms vérifie si l’URI requis est placé sur la liste autorisée :

   * Si cʼest le cas, le serveur transmet la requête.
   * Si l’URI requis n’est pas placé sur la liste autorisée, le serveur récupère le référent de la requête.

1. S’il existe un référent dans la requête, le serveur vérifie s’il s’agit d’un référent autorisé. S’il est autorisé, le serveur recherche une exception de référent :

   * S’il s’agit d’une exception, la requête est bloquée.
   * S’il ne s’agit pas d’une exception, la requête est transmise.

1. S’il n’y a aucun référent dans la requête, le serveur vérifie si un référent null est autorisé.

   * Si un référent null est autorisé, la requête est transmise.
   * Si un référent null n’est pas autorisé, le serveur vérifie si l’URI requis est une exception pour un référent null et traite la requête en conséquence.

## Configuration des référents autorisés {#configure-allowed-referers}

Lorsque vous exécutez Configuration Manager, l’hôte par défaut et l’adresse IP ou le serveur Forms sont ajoutés à la liste des référents autorisés. Vous pouvez modifier cette liste dans Administration Console.

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Configurer les URL de référent autorisées. La liste Référent autorisé s’affiche au bas de la page.
1. Pour ajouter un référent autorisé :

   * Saisissez un nom d’hôte ou une adresse IP dans la zone Référents autorisés . Pour ajouter plusieurs référents autorisés à la fois, saisissez chaque nom d’hôte ou adresse IP sur une nouvelle ligne.
   * Dans les zones Port HTTP et Port HTTPS, spécifiez les ports à autoriser pour le protocole HTTP, HTTPS ou les deux. Si vous laissez ces zones vides, les ports par défaut (port 80 pour HTTP et port 443 pour HTTPS) sont utilisés. Si vous saisissez `0` (zéro) dans les champs, tous les ports sont activés sur ce serveur. Vous pouvez également saisir un numéro de port spécifique pour activer uniquement ce port.
   * Cliquez sur Ajouter.

1. Pour supprimer l’entrée de la liste de référents autorisés, sélectionnez l’élément dans la liste, puis cliquez sur Supprimer.

   Si la liste de référents autorisés est vide, la fonction CSRF cesse de fonctionner et le système n’est plus sécurisé.

1. Après avoir modifié la liste de référents autorisés, redémarrez le serveur AEM Forms.
