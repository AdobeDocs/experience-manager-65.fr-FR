---
title: Présentation d’AEM Forms
description: Utilisez ce guide d’AEM 6.5 pour créer, gérer, publier et mettre à jour des formulaires numériques. Trouvez de l’aide sur l’installation, la mise à niveau et la configuration, et découvrez comment créer des formulaires adaptatifs.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: e5533b4f-93b7-4ea9-a01d-fdf9528652c8
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 31%

---

# Présentation d’AEM Forms{#introduction-to-aem-forms}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=fr) |
| AEM 6.5 | Cet article |

Pour plus d’informations sur les dernières fonctionnalités et améliorations d’AEM Forms, voir [Nouveautés d’AEM Forms](../../forms/using/whats-new.md).

## À propos d’AEM Forms {#about-aem-forms}

Adobe Experience Manager (AEM) offre une solution conviviale pour créer, gérer, publier et mettre à jour des formulaires numériques complexes tout en s’intégrant aux processus principaux, aux règles métier et aux données.

AEM Forms associe des outils de création, de gestion et de publication à des fonctionnalités de gestion des correspondances, de sécurité des documents et d’analytique intégré pour offrir un environnement complet et convivial. Conçu pour fonctionner sur des canaux Web et mobiles, AEM Forms peut être efficacement intégré à vos processus métier, ce qui réduit les processus papier et les erreurs tout en améliorant l’efficacité.

Dans les grandes entreprises, les formulaires sont souvent créés et réutilisés en les copiant dans un système de gestion de contenu. La mise à jour d’une base de données volumineuse de formulaires et leur découverte peuvent représenter un défi considérable. AEM fournit un portail Forms personnalisable qui permet aux clients de rechercher et d’accéder aux formulaires dont ils ont besoin sur les canaux web et mobiles.

AEM Forms offre des outils de gestion de formulaires qui vous permettent non seulement de gérer les formulaires adaptatifs, mais aussi les formulaires XFA, les formulaires PDF et les actifs associés. Pour plus d’informations, voir [Présentation de la gestion des formulaires](../../forms/using/introduction-managing-forms.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=fr), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

![Fonctionnalités d’AEM forms](do-not-localize/4th-draft.gif)

### Fonctionnalités essentielles {#key-capabilities}

En résumé, AEM Forms offre des fonctionnalités puissantes de gestion de formulaires, comme celles qui suivent, qui réduisent les processus manuels et augmentent la satisfaction des clients.

* Portail Forms centralisé pour la conception et le déploiement de formulaires dynamiques, notamment les formulaires adaptatifs, PDF, HTML5 et
* Interface utilisateur graphique conviviale pour permettre aux utilisateurs professionnels d’importer, gérer, prévisualiser et publier facilement des formulaires
* Répertoire de formulaires réactifs avec de puissantes fonctionnalités de recherche utilisant des mots-clés, des balises et des métadonnées
* Détection dynamique de l’appareil et de l’emplacement d’un utilisateur pour un rendu approprié du formulaire sur les canaux web et mobiles
* Intégration à Adobe Analytics pour mesurer efficacement les mesures d’utilisation des formulaires
* Intégration aux services Adobe Document Cloud eSign ou saisie tactile pour signer électroniquement des documents contenant des informations confidentielles
* Publication automatisée de formulaires et possibilité de diffuser des communications opportunes, personnalisées et cohérentes par plusieurs canaux

## AEM types de formulaires {#aem-form-types}

AEM Forms vous permet d’étendre les formulaires nouveaux et existants pour créer :

* HTML et PDF forms pixels parfaits et paginés qui ressemblent presque à du papier, ou
* formulaires adaptatifs qui s’affichent automatiquement pour le périphérique et le navigateur d’un utilisateur.

**PDF forms**

Les PDF forms peuvent être remplis hors ligne, enregistrés localement et les données de formulaire envoyées lors de votre prochaine mise en ligne. Vous pouvez utiliser des codes à barres 2D pour capturer des données de formulaire et des signatures numériques pour valider l’authenticité des utilisateurs.

**Formulaires HTML**

Les formulaires basés sur un navigateur HTML5 peuvent être affichés sur des périphériques mobiles et des navigateurs de bureau. Vous pouvez signer électroniquement des HTMLS à l’aide des services de saisie tactile ou eSign.

**Formulaires adaptatifs**

Les formulaires adaptatifs peuvent s’adapter dynamiquement aux réponses des utilisateurs en ajoutant ou en supprimant des champs ou des sections selon les besoins. AEM vous permet de réutiliser des modèles de formulaires XML d’Adobe pour créer des formulaires adaptatifs.

### Fonctionnalités prises en charge {#supported-features}

Tous les types de formulaires prennent en charge les fonctionnalités suivantes :

* Disposition dynamique
* Validation des champs de formulaire
* Aide contextuelle
* Traitement des données XML et des scripts
* Conception et vérification de l’accessibilité
* Possibilité d’enregistrer des formulaires côté serveur
* Prise en charge des pièces jointes
* Intégration à HTML Workspace pour la capture de données

## Collecte de données hors ligne {#offline-data-collection}

Une fois les données de formulaire envoyées, Adobe Experience Manager les associe aux systèmes, aux règles de fonctionnement et aux personnes requises.

AEM Forms fournit Forms Workspace, une application mobile qui étend vos processus métier numériques aux appareils mobiles. Avec Forms Workspace, vous pouvez collecter et enregistrer des données même hors ligne. Forms Workspace utilise les fonctionnalités de votre périphérique mobile et vous permet de capturer des photos, des vidéos et de collecter des données, telles que des horodatages et d’autres informations. La prochaine fois que vous vous connecterez à un réseau, vous pouvez synchroniser les données collectées.

La capture des données hors ligne et la synchronisation de celles-ci lors de votre prochaine mise en ligne s’avèrent particulièrement utiles pour les personnes sur le terrain. Cela améliore la productivité et réduit les erreurs.

**Avantages de l’utilisation de Forms Workspace pour la collecte de données hors ligne**

* Application d’espace de travail de HTML conviviale pour l’affectation et le suivi des tâches
* Environnement de conception de workflow par glisser-déposer
* Connecteurs de gestion de contenu d’entreprise (ECM)
* Prise en charge des normes ouvertes, notamment XML et SOAP, pour connecter les données de formulaires aux systèmes d’entreprise
* Les rapports de HTML d’usine surveillent les retards, les files d’attente de travail et les indicateurs de performance clés (KPI).
* Tableaux de bord personnalisables pour un aperçu en temps réel des opérations commerciales
* API pour la connexion à des outils de reporting tiers

![Troisième version](do-not-localize/3rd-draft.gif)

## Communication personnalisée {#personalized-communication}

Une composante importante d’une expérience numérique de libre-service efficace est la diffusion d’informations personnalisées en temps voulu, accessibles n’importe où et depuis n’importe quel périphérique. Les messages personnalisés diffusés en temps voulu peuvent améliorer les taux de conversion et la satisfaction des utilisateurs.

A l’aide d’AEM Forms, les utilisateurs professionnels peuvent créer des expériences utilisateur personnalisées attrayantes en personnalisant les modèles de document, en incorporant les informations des processus principaux et en incluant des composants interactifs. Une interface utilisateur intuitive permet aux utilisateurs non techniques de développer des règles métier qui déterminent à quel moment générer une communication en fonction d’une requête ou initier une réponse générée par l’utilisateur.

Les documents personnalisés, tels que les reçus, les kits de bienvenue et les instructions, peuvent facilement être diffusés sur plusieurs canaux. Les entreprises peuvent rediriger le trafic vers des portails Web personnalisés suite à une inscription ou à l’achat de services supplémentaires.

**Fonctions clés**

* Environnement de création de correspondance avec prise en charge des modèles, des blocs de contenu, des règles métier, etc.
* Conversion et assemblage de documents
* Prise en charge de la diffusion de documents à la demande ou par lots sur plusieurs canaux, notamment le web, le courrier électronique et le papier
* Suivi avec historique des modifications
* Prise en charge des signatures numériques pour valider l’intégrité du contenu et l’identité du signataire
* Module complémentaire de sécurité des documents pour AEM Forms comprenant le chiffrement, les politiques d’utilisation, le suivi et l’audit

![Disposition deux](do-not-localize/layout-02.png)

Processus de communication personnalisée rationalisée

