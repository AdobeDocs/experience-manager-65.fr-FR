---
title: Affichage des informations du système
seo-title: Affichage des informations du système
description: Découvrez comment vous pouvez afficher les graphiques de contrôle des ressources et les informations sur le serveur exécutant AEM Forms.
seo-description: Découvrez comment vous pouvez afficher les graphiques de contrôle des ressources et les informations sur le serveur exécutant AEM Forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 37%

---


# Affichage des informations du système {#view-system-information}

L’onglet Système affiche des graphiques de contrôle des ressources ainsi que des informations sur le serveur exécutant AEM Forms. Pour accéder à ces informations, cliquez sur Health Monitor dans l’angle supérieur droit de la page. Si vous exécutez AEM Forms dans un environnement en grappe, les informations affichées concernent le nœud sélectionné dans la liste des serveurs.

Pour enregistrer les informations du système actuel en tant que fichier de propriétés, cliquez sur Enregistrer.

Le volet droit de l’onglet Système affiche une représentation graphique des éléments suivants :

* dénombrement des tâches et travaux ;
* utilisation du tas et du tas validé ;
* utilisation du non-tas et du non-tas validé.

Déplacez le curseur pour obtenir les valeurs d’un moment particulier.

>[!NOTE]
>
>les données graphiques, les valeurs d’information sur le serveur et l’heure de l’horloge sont mises à jour toutes les dix minutes. L’information n’est pas affichée en temps réel.

Le volet gauche de l’onglet Système affiche des renseignements relatifs au serveur et au nœud :

**Machine virtuelle : version de la machine virtuelle** Java (JVM) sur le serveur.

**Fournisseur d’ordinateurs virtuels :** fabricant de la JVM.

**Version de la machine virtuelle:numéro de version de** la JVM

**Nom de l’ordinateur : nom** d’hôte du serveur sur lequel AEM forms est installé.

**Heure d’activation :** heure, en heures et minutes, pendant laquelle le serveur est en cours d’exécution.

**Compilateur juste à temps :** nom du compilateur utilisé.

**Temps de compilation :** durée de la compilation.

**Nombre de threads dynamiques :** nombre total de threads actuellement présents dans le système de formulaires AEM.

**Nombre de threads Pic :** plus grand nombre de threads dynamiques jamais enregistrés sur le système.

**Nombre de classes chargées :** Nombre de classes chargées dans la JVM.

**Nombre de classes déchargées :** Nombre de classes déchargées de la JVM.

**Tas minimal :** quantité minimale de tas utilisée.

**Tas maximum :** quantité maximale de tas utilisée.

**Nom du système d’exploitation : nom** du système d’exploitation s’exécutant sur le serveur d’AEM forms.

**Version du système d’exploitation : numéro de** version du système d’exploitation s’exécutant sur le serveur d’AEM forms.

**Arche du système d’exploitation : architecture** du système d’exploitation sur lequel la JVM s’exécute.

**Nombre de processeurs :** nombre de processeurs sur le système.

**Arguments de la machine virtuelle : argument utilisé par** la JVM.

**Class Path : chemin** de classe utilisé par la JVM.

**Chemin d’accès à** la bibliothèque : chemin d’accès à la bibliothèque utilisé par la JVM.

**Chemin de classe de démarrage : chemin** de classe de démarrage utilisé par la JVM.

**Type de serveur d’applications :** type de serveur d’applications utilisé pour exécuter AEM formulaires.

**Version du serveur d’applications : numéro de** version du serveur d’applications utilisé pour exécuter AEM formulaires.

**Fournisseur du serveur d’applications :** fabricant du serveur d’applications utilisé pour exécuter AEM formulaires.

**Date d’installation :** date (au format aaaa-mm-jj) à laquelle AEM forms a été installé.

**AEM forms Version :** version des AEM forms installés.

**Version du correctif : numéro de correctif des formulaires** AEM.

**Database Name :** type de base de données utilisé par AEM forms.

**Version de la base de données : numéro de** version de la base de données utilisée par AEM forms.

**Database Drive Name : nom** du pilote utilisé par la JVM pour se connecter à la base de données.

**Version du pilote de base de données : version** du pilote utilisé par la JVM pour se connecter à la base de données.

Le bouton **Enregistrer** permet d’enregistrer ces informations système dans un fichier de propriétés.
