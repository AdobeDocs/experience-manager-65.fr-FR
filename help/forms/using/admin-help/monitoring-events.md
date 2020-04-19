---
title: Contrôle des événements
seo-title: Contrôle des événements
description: Lorsque la fonctionnalité de contrôle est activée, Document Security vous permet de contrôler certains types d’événements. Vous pouvez aisément effectuer des recherches dans la liste des événements et trier celle-ci à l’aide de la sécurité des documents.
seo-description: Lorsque la fonctionnalité de contrôle est activée, Document Security vous permet de contrôler certains types d’événements. Vous pouvez aisément effectuer des recherches dans la liste des événements et trier celle-ci à l’aide de la sécurité des documents.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Contrôle des événements {#monitoring-events}

Lorsque la fonctionnalité de contrôle est activée, Document Security vous permet de contrôler certains types d’événements. Les événements visibles dépendent de votre rôle :

**Utilisateurs :** Peut  des  contrôlés pour leurs protégés par une politique et pour tout autre protégé qu&#39;ils reçoivent et utilisent.

**Coordinateurs de jeux de stratégies :** Peut  les  de contrôlés, y compris les de lapolitique et lespolitiques, pour les programmes qui sont protégés par des stratégies de leurs jeux de stratégies.

**Administrateurs :** Peut  les  de contrôlés qui sont liés à tous les utilisateurs et à tous les protégés par une stratégie. Les administrateurs peuvent également suivre d’autres types d’événements, tels que les événements d’utilisateur, de document, de stratégie et de système.

>[!NOTE]
>
>les événements qui surviennent sur une copie d’un document protégé par une stratégie sont également consignés comme des événements concernant le document d’origine protégé

(voir [Options de contrôle des événements](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)).

Un événement d’échec est enregistré si un utilisateur non autorisé tente d’afficher un document ou d’ouvrir une session avec un nom d’utilisateur ou un mot de passe incorrect.

>[!NOTE]
>
>les événements signalant l’échec de l’accès anonyme à des documents peuvent être consignés si l’accès anonyme est supprimé d’une stratégie. Lorsqu’un destinataire autorisé tente d’accéder à un document protégé par la stratégie modifiée, la première tentative constitue toujours un accès anonyme, mais est invariablement vouée à l’échec.

Si une stratégie autorise l’accès d’utilisateurs anonymes et si l’administrateur désactive par la suite l’accès anonyme pour Document Security, l’accès anonyme échoue pour les documents protégés par la stratégie et l’événement n’est pas consigné.

## Activation du contrôle des événements {#enable-event-auditing}

La configuration requise pour contrôler les événements est la suivante :

* Le système ou l’administrateur doit activer la fonctionnalité de contrôle sur le serveur

   (voir [Configuration des options de contrôle et de confidentialité des événements](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)).

* Le contrôle doit être activé sur la stratégie que vous utilisez pour protéger le document (voir [Création et modification de stratégies](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Recherche d’un événement {#search-for-an-event}

Vous pouvez naviguer dans la liste des événements et afficher des descriptions plus détaillées sur des événements. Ces descriptions détaillées incluent des informations comme l’ID de l’événement, sa description, son adresse IP, l’entreprise, l’utilisateur concerné, la date et l’heure de survenue, les activités refusées, ainsi que les événements hors connexion (lorsque des utilisateurs tentent d’utiliser un document sans être connectés à Document Security).

Vous pouvez rechercher des événements dans la page Evénements en combinant des critères de recherche et des dates. Les événements pouvant faire l’objet d’une recherche dépendent de votre rôle :

**Utilisateurs :** Peut  des  contrôlés pour leurs protégés par une politique et pour tout autre protégé qu&#39;ils reçoivent et utilisent. Les options de recherche disponibles sont les suivantes :

**m&#39;a raconté :** Les utilisateurs peuvent rechercher des  pour tout protégé par une stratégie  qu’ils ont créé ou reçu. Par exemple, si un utilisateur ouvre, affiche ou imprime un document qui était protégé par une autre personne, l’utilisateur ne voit que les événements concernant ce document.

**en rapport avec mon  :** Les utilisateurs peuvent trouver tous les  qui sont liés à leur propre protégé par une stratégie. Les utilisateurs voient les événements générés par chaque personne ayant manipulé leurs documents.

**Coordinateurs de jeux de stratégies :** Peut  les  de contrôlés, y compris les de lapolitique et lespolitiques, pour les programmes qui sont protégés par des stratégies de leurs jeux de stratégies. Voici les options de disponibles :

**où je suis coordinateur de jeux de stratégies :** Les coordinateurs de jeux de stratégies qui disposent de l’autorisation   peuvent trouver des qui sont liées aux protégés par des stratégies issues de leurs jeux de stratégies.

**de stratégies  où je suis coordinateur de jeux de stratégies :** Les coordinateurs de jeux de stratégies qui disposent de l’autorisation   peuvent trouver des liées aux stratégies issues de leurs jeux de stratégies.

**Administrateurs :** Peut  les  de contrôlés qui sont liés à tous les utilisateurs et à tous les protégés par une stratégie. Les administrateurs peuvent également assurer le suivi d’autres types. De plus, les administrateurs peuvent subdiviser les recherches d’événements par type d’utilisateur :

**Utilisateurs connus :** Les utilisateurs se trouvent dans les répertoires source ou sont enregistrés en tant qu’utilisateurs externes.

**Utilisateurs anonymes :**  les qui accèdent à un  protégé par une stratégie autorisant l’accès anonyme.

**Utilisateurs système :**  initié par le serveur, telle qu’une synchronisation d’annuaires.

1. Dans la page Document Security, cliquez sur Événements.
1. Dans la liste Rechercher, sélectionnez les critères de recherche à utiliser. Selon l’élément sélectionné dans la liste Rechercher, une seconde liste affiche des critères de recherche supplémentaires. Le cas échéant, saisissez votre critère de recherche dans la zone de texte.

   Pour plus d’information sur des types d’événements spécifiques, voir [Options de contrôle des événements](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Dans la liste Utilisateur, sélectionnez l’utilisateur ayant déclenché l’événement :

   * Si vous sélectionnez Utilisateur connu, une seconde zone de recherche apparaît. Saisissez le nom ou l’adresse électronique de l’utilisateur.
   * Si vous ne connaissez pas ces valeurs, cliquez sur l’icône représentant un carnet d’adresses pour rechercher l’utilisateur par son nom ou par son adresse électronique.

1. Dans la liste Date, sélectionnez une option de plage de dates. Si vous sélectionnez Dates personnalisées, des zones apparaissent pour vous permettre de saisir la date au format aaaa/mm/jj. Vous pouvez également spécifier la plage de dates à l’aide du Sélecteur de date en procédant comme suit :

   * Cliquez sur le calendrier pour ouvrir le Sélecteur de date.
   * Utilisez les flèches pour sélectionner l’année et le mois.
   * Cliquez sur un jour du mois dans le calendrier.
   * Cliquez sur OK pour fermer le Sélecteur de date.

1. Dans la liste Afficher, sélectionnez le nombre de résultats de recherche à afficher par page.
1. Cliquez sur Rechercher.

   Tous les événements d’échec apparaissent en surbrillance dans la liste avec une icône de refus.

1. Pour afficher les détails d’un événement, cliquez sur la description de l’événement dans la liste.

## Tri de la liste des événements {#sort-the-event-list}

Pour faciliter la recherche d’événements, triez la liste par en-tête de colonne. Le triangle situé à côté de l’en-tête de colonne indique la colonne triée. Lorsque le triangle est dirigé vers le haut, l’ordre de tri est croissant et lorsqu’il est dirigé vers le bas, l’ordre de tri est décroissant.

1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur l’en-tête de colonne.

