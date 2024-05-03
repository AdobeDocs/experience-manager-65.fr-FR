---
title: Contrôler les événements
description: Lorsque la fonctionnalité de contrôle est activée, Document Security vous permet de contrôler certains types d’événements. Vous pouvez aisément effectuer des recherches dans la liste des événements et trier celle-ci à l’aide de Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 100%

---

# Contrôler les événements {#monitoring-events}

Lorsque la fonctionnalité de contrôle est activée, Document Security vous permet de contrôler certains types d’événements. Les événements visibles dépendent de votre rôle :

**Utilisateurs :** ils peuvent afficher les événements contrôlés sur leurs documents protégés par une politique, ainsi que sur les documents protégés qu’ils reçoivent et utilisent.

**Coordinateurs de jeux de politiques :** ils peuvent afficher les événements contrôlés, notamment les événements de document et de politique, pour les documents protégés par des politiques issues de leurs jeux de politiques.

**Administrateurs :** ils peuvent afficher les événements contrôlés concernant tous les utilisateurs et documents protégés par une politique. Les administrateurs et administratrices peuvent également suivre d’autres types d’événements, tels que les événements d’utilisateur ou d’utilisatrice, de document, de stratégie et de système.

>[!NOTE]
>
>Les événements qui surviennent sur une copie d’un document protégé par une politique sont également consignés comme des événements concernant le document d’origine protégé.réduisant l’incidence sur les performances de votre environnement AEM forms.

(voir [Options de contrôle des événements](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)).

Un événement d’échec est enregistré si une personne non autorisée tente d’afficher un document ou de se connecter avec un nom d’utilisateur ou un mot de passe incorrect.

>[!NOTE]
>
>Les événements signalant l’échec de l’accès anonyme à des documents peuvent être consignés si l’accès anonyme est supprimé d’une politique. Lorsqu’une personne destinataire autorisée tente d’accéder à un document protégé par la politique modifiée, la première tentative constitue toujours un accès anonyme, mais est invariablement vouée à l’échec.

Si une politique autorise l’accès d’utilisateurs ou d’utilisatrices anonymes et si l’administrateur ou l’administratrice désactive par la suite l’accès anonyme pour Document Security, l’accès anonyme échoue pour les documents protégés par la politique et l’événement n’est pas consigné.

## Activation du contrôle des événements {#enable-event-auditing}

La configuration requise pour contrôler les événements est la suivante :

* Le système, l’administrateur ou l’administratrice doit activer la fonctionnalité de contrôle sur le serveur.

  (voir [Configuration des options de contrôle et de confidentialité des événements](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)).

* Le contrôle doit être activé sur la politique que vous utilisez pour protéger le document. (voir [Création et modification de politiques](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Recherche d’un événement {#search-for-an-event}

Vous pouvez naviguer dans la liste des événements et afficher des descriptions plus détaillées d’événements. Ces descriptions détaillées incluent des informations comme l’ID de l’événement, sa description, son adresse IP, l’entreprise, l’utilisateur ou l’utilisatrice concernée, la date et l’heure de survenue, les activités refusées, ainsi que les événements hors connexion (lorsque des utilisatrices ou des utilisateurs tentent d’utiliser un document sans être connectés à Document Security).

Vous pouvez rechercher des événements dans la page Événements en combinant des critères de recherche et des dates. Les événements pouvant faire l’objet d’une recherche dépendent de votre rôle :

**Utilisateurs :** ils peuvent afficher les événements contrôlés sur leurs documents protégés par une politique, ainsi que sur les documents protégés qu’ils reçoivent et utilisent. Les options de recherche disponibles sont les suivantes :

**Événements me
concernant :** les utilisateurs peuvent rechercher des événements concernant les documents protégés par une politique qu’ils ont créés ou reçus. Par exemple, si un utilisateur ouvre, affiche ou imprime un document qui était protégé par une autre personne, l’utilisateur ne voit que les événements concernant ce document.

**Événements liés à mes documents :** les utilisateurs peuvent rechercher tous les événements relatifs à leurs propres documents protégés par une politique. Les utilisateurs voient les événements générés par chaque personne ayant manipulé leurs documents.

**Coordinateurs de jeux de politiques :** ils peuvent afficher les événements contrôlés (notamment les événements de document et de politique) pour les documents protégés par des politiques issues de leurs jeux de politiques. Voici les options de disponibles :

**Événements de document pour lesquels
je suis coordinateur de jeux de politiques :** les coordinateurs de jeux de politiques qui disposent de l’autorisation d’affichage des événements peuvent rechercher les événements liés aux documents protégés par des politiques issues de leurs jeux de politiques.

**Événements de politique pour lesquels je suis coordinateur de jeux de politiques :** les coordinateurs de jeux de politiques qui disposent de l’autorisation d’affichage des événements peuvent rechercher les événements liés aux politiques issues de leurs jeux de politiques.

**Administrateurs :** ils peuvent afficher les événements contrôlés concernant tous les utilisateurs et documents protégés par une politique. Les administrateurs et administratrices peuvent également assurer le suivi d’autres types. De plus, les administrateurs et administratrices peuvent subdiviser les recherches d’événements par type d’utilisateur ou d’utilisatrice :

**Utilisateurs connus :** utilisateurs se trouvant dans les répertoires sources ou enregistrés en tant qu’utilisateurs externes.

**Utilisateurs anonymes :** utilisateurs non identifiés qui accèdent à un document protégé par une politique autorisant un accès anonyme.

**Utilisateurs système :** événements déclenchés par le serveur, comme la synchronisation d’un répertoire.

1. Dans la page Document Security, cliquez sur Événements.
1. Dans la liste Rechercher, sélectionnez les critères de recherche à utiliser. Selon l’élément sélectionné dans la liste Rechercher, une seconde liste affiche des critères de recherche supplémentaires. Le cas échéant, saisissez votre critère de recherche dans la zone de texte.

   Pour plus d’information sur des types d’événements spécifiques, voir [Options de contrôle des événements](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Dans la liste Utilisateur et utilisatrice, sélectionnez l’utilisateur ou l’utilisatrice ayant déclenché l’événement :

   * Si vous sélectionnez Utilisateur connu ou Utilisatrice connue, une seconde zone de recherche apparaît. Saisissez le nom ou l’adresse e-mail de l’utilisateur ou de l’utilisatrice.
   * Si vous ne connaissez pas ces valeurs, cliquez sur l’icône représentant un carnet d’adresses pour rechercher l’utilisateur ou l’utilisatrice par son nom ou par son adresse e-mail.

1. Dans la liste Date, sélectionnez une option de période. Si vous sélectionnez Dates personnalisées, des zones apparaissent pour vous permettre de saisir la date au format aaaa/mm/jj. Vous pouvez également spécifier la période à l’aide du Sélecteur de date en procédant comme suit :

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
