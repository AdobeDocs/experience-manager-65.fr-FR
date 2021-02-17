---
title: Prévention des attaques CSRF
seo-title: Prévention des attaques CSRF
description: Apprenez à prévenir les attaques multisites par usurpation de requête (CSRF) et à éviter que les données utilisateur ne soient compromises.
seo-description: Apprenez à prévenir les attaques multisites par usurpation de requête (CSRF) et à éviter que les données utilisateur ne soient compromises.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 81%

---


# Prévention des attaques CSRF {#preventing-csrf-attacks}

## Fonctionnement des attaques CSRF {#how-csrf-attacks-work}

Une attaque multisite par usurpation de requête ou CRSF (Cross-site request forgery) consiste à utiliser le navigateur d’un utilisateur valide pour envoyer une requête malveillante via un élément iframe, par exemple. Le navigateur envoyant les cookies sur la base de domaines, si l’utilisateur est connecté à une application, ses données peuvent être corrompues.

Imaginons, par exemple, un scénario où vous êtes connecté à Administration Console dans un navigateur. Vous recevez un message électronique contenant un lien. Vous cliquez sur le lien qui vient ouvrir un nouvel onglet dans votre navigateur. La page que vous avez ouverte contient un iFrame masqué qui envoie une requête malveillante au serveur Forms à l’aide du cookie de votre session AEM forms authentifiée. Comme User Management reçoit un cookie valide, il transmet la requête.

## Termes associés aux attaques CSRF {#csrf-related-terms}

**Référent :** adresse de la page source à partir de laquelle une demande arrive. Par exemple, une page Web de site1.com contient un lien vers site2.com. En cliquant sur ce lien, une requête est envoyée à site2.com. Le référent de la requête est donc site1.com, la requête ayant été envoyée à partir d’une page provenant de site1.com.

**URIs Placés sur la liste autorisée:** URIs identifient les ressources du serveur Forms qui sont demandées, par exemple /adminui ou /contentspace. Certaines ressources peuvent autoriser des requêtes à entrer dans l’application à partir de sites Web externes. Ces ressources sont considérées comme des URI placés sur la liste autorisée. Le serveur Forms n’effectue jamais de vérification du référent à partir d’URI placés sur la liste autorisée.

**Référent nul :** lorsque vous ouvrez une nouvelle fenêtre ou un nouvel onglet du navigateur, puis que vous tapez une adresse et appuyez sur Entrée, le référent est nul. La requête est totalement nouvelle et ne provient d’aucune page Web parente ; il n’existe donc aucun référent pour la requête. La valeur d’un référent reçu par le serveur Forms peut être NULL dans plusieurs cas :

* lorsqu’une requête est effectuée sur un point de fin SOAP ou REST à partir d’Acrobat ;
* lorsqu’un utilisateur final effectue une requête HTTP sur un point de fin SOAP ou REST AEM Forms ;
* lorsque vous ouvrez une nouvelle fenêtre de navigation et que l’URL de la page de connexion d’une application Web AEM forms est déjà saisie.

Autorisez la valeur de référent NULL sur les points de fin SOAP et REST. Autorisez également la valeur de référent NULL sur toutes les pages de connexion URI telles que /adminui et /contentspace, ainsi que leurs ressources mappées correspondantes. Par exemple, la servlet mappée pour /contentspace est /contentspace/faces/jsp/login.jsp ; sa valeur de référent doit pouvoir être NULL. Cette exception est obligatoire uniquement si vous activez le filtrage GET pour votre application Web. Vos applications peuvent indiquer s’il convient d’autoriser des référents de valeur NULL Voir &quot;Protection contre les attaques multisites par usurpation de requête&quot; dans [Renforcement et sécurité des formulaires AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Exception de référent autorisé : l’exception de référent** autorisé est une sous-liste de la liste des référents autorisés, à partir de laquelle les requêtes sont bloquées. Les exceptions aux référents autorisés sont spécifiques à une application Web. Si un sous-ensemble des référents autorisés ne doit pas être autorisé à appeler une application Web particulière, vous pouvez placer sur la liste bloquée les référents au moyen d’exceptions aux référents autorisés. Les exceptions aux référents autorisés peuvent être spécifiées dans le fichier web.xml de votre application (consultez la section Protection contre les attaques multisite par usurpation de requête dans Renforcement et sécurité d’AEM Forms sur la page Aide et didacticiels).

## Fonctionnement des référents autorisés {#how-allowed-referers-work}

AEM forms offre une option de filtrage des référents aidant à prévenir les attaques CSRF. Le filtrage des référents fonctionne de la manière suivante :

1. Le serveur Forms vérifie la méthode HTTP utilisée pour l’appel :

   * S’il s’agit d’une méthode POST, le serveur Forms vérifie l’en-tête référent.
   * S’il s’agit d’une méthode GET, le serveur Forms ignore la vérification du référent, à moins que la variable CRSF_CHECK_GETS ne soit définie sur true. Dans ce cas, il vérifie l’en-tête du référent. La variable CSRF_CHECK_GETS peut être spécifiée dans le fichier web.xml de votre application (voir Protection contre les attaques multisites par usurpation de requête dans le [Guide de renforcement et de sécurité](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)).

1. Le serveur Forms vérifie si l’URI requis est placé sur la liste autorisée :

   * Si l’URI est placé sur la liste autorisée, le serveur transmet la requête.
   * Si l’URI requis n’est pas placé sur la liste autorisée, le serveur récupère le référent de la requête.

1. S’il existe un référent pour la requête, le serveur vérifie s’il s’agit d’un référent autorisé. Si le référent est autorisé, le serveur vérifie qu’il ne fait pas partie des exceptions aux référents autorisés :

   * S’il s’agit d’une exception, la requête est bloquée.
   * S’il ne fait pas partie des exceptions, la requête est transmise.

1. S’il n’existe aucun référent pour la requête, le serveur vérifie que les référents de valeur NULL sont autorisés.

   * Si les référents de valeur NULL sont autorisés, la requête est transmise.
   * Si ce n’est pas le cas, le serveur vérifie que l’URI requis fait partie des exceptions aux référents de valeur NULL et traite la requête en fonction.

## Configuration des référents autorisés  {#configure-allowed-referers}

Lorsque vous exécutez Configuration Manager, l’hôte par défaut et l’adresse IP ou le serveur Forms sont ajoutés à la liste de référents autorisés. Vous pouvez modifier cette liste dans Administration Console.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les URL des référents autorisés. La liste de référents autorisés s’affiche en bas de la page.
1. Pour ajouter un référent autorisé :

   * Saisissez un nom d’hôte ou une adresse IP dans le champ Référents autorisés. Pour ajouter plusieurs référents autorisés en même temps, saisissez chaque nom d’hôte ou adresse IP dans une nouvelle ligne.
   * Dans les champs Port HTTP et Port HTTPS, indiquez les ports à autoriser pour le protocole HTTP ou HTTPS ou pour les deux. Si vous laissez ces zones vides, les ports par défaut (le port 80 pour le protocole HTTP et le port 443 pour le protocole HTTPS) sont utilisés. Si vous saisissez `0` (zéro) dans les champs, tous les ports sont activés sur ce serveur. Vous pouvez également saisir un numéro de port spécifique pour activer uniquement ce port.
   * Cliquez sur Ajouter.

1. Pour supprimer une entrée de la liste de référents autorisés, sélectionnez l’élément dans la liste puis cliquez sur Supprimer.

   Si la liste de référents autorisés est vide, la fonction CSRF est désactivée et le système n’est donc plus sécurisé.

1. Après avoir modifié la liste de référents autorisés, redémarrez le serveur AEM forms.

