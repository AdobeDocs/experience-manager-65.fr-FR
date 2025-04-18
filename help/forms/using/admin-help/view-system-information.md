---
title: Afficher les informations du système
description: Découvrez comment afficher des graphiques de surveillance des ressources et des informations sur le serveur qui exécute AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 100%

---

# Afficher les informations du système {#view-system-information}

L’onglet Système affiche des graphiques de surveillance des ressources et des informations sur le serveur qui exécute AEM Forms. Pour accéder à ces informations, dans la console d’administration, cliquez sur Health Monitor en haut à droite de la page. Si vous exécutez AEM Forms dans un environnement organisé en clusters, les informations affichées concernent le nœud sélectionné dans la liste des serveurs.

Pour enregistrer les informations système actuelles en tant que fichier de propriétés, cliquez sur Enregistrer.

Le volet de droite de l’onglet Système affiche des représentations graphiques des informations suivantes :

* Dénombrement des tâches et des travaux
* Utilisation du tas et du tas validé
* Utilisation de non-tas et de non-tas validés

Déplacez le curseur pour obtenir les valeurs d’un moment particulier.

>[!NOTE]
>
>Les données graphiques, les valeurs des informations sur le serveur et l’heure de l’horloge sont mises à jour toutes les 10 minutes. Les informations ne sont pas affichées en temps réel.

Le volet gauche de l’onglet Système affiche les informations suivantes sur le serveur ou le nœud :

**Machine virtuelle :** version de la machine virtuelle Java (JVM) sur le serveur.

**Fournisseur de la machine virtuelle :** fabricant de la JVM.

**Version de la machine virtuelle :** numéro de version JVM.

**Nom de la machine :** nom d’hôte du serveur sur lequel AEM Forms est installé.

**Durée de fonctionnement :** durée (en heures et minutes) pendant laquelle le serveur a fonctionné.

**Compilateur à la volée :** nom du compilateur en cours d’utilisation.

**Temps de compilation :** quantité de temps passé pour la compilation.

**Nombre de threads actifs :** nombre total de threads actuellement présents dans le système AEM forms.

**Pic du nombre de threads :** le plus grand nombre de threads en direct jamais enregistrés sur le système.

**Nombre de classes chargées :** nombre de classes chargées dans la JVM.

**Nombre de classes déchargées :** nombre de classes déchargées de la JVM.

**Tas minimum :** quantité minimale de tas utilisée.

**Tas maximum :** quantité maximale de tas utilisée.

**Nom du système d’exploitation :** nom du système d’exploitation s’exécutant sur le serveur AEM Forms.

**Version du système d’exploitation :** numéro de version du système d’exploitation s’exécutant sur le serveur AEM Forms.

**Architecture du système d’exploitation :** architecture du système d’exploitation sur lequel la JVM est en cours d’exécution.

**Nombre de processeurs :** nombre de processeurs sur le système.

**Arguments de la machine virtuelle :** argument utilisé par la JVM.

**Chemin d’accès de la classe :** chemin d’accès de classe utilisé par la JVM.

**Chemin d’accès à la bibliothèque :** chemin d’accès à la bibliothèque utilisé par la JVM.

**Chemin d’accès de la classe de démarrage :** chemin d’accès de la classe de démarrage utilisé par la JVM.

**Type de serveur d’applications :** type de serveur d’applications utilisé pour exécuter AEM forms.

**Version du serveur d’application :** numéro de version du serveur d’application utilisé pour exécuter AEM forms.

**Fabricant du serveur d’application :** fabricant du serveur d’application utilisé pour exécuter AEM Forms.

**Date d’installation :** date (format aaaa-mm-jj) à laquelle AEM Forms a été installé.

**Version d’AEM forms :** version d’AEM forms installée.

**Version du correctif :** numéro du correctif d’AEM forms.

**Nom de base de données :** type de base de données utilisée par AEM Forms.

**Version de la base de données :** numéro de version de la base de données utilisée par AEM forms.

**Nom du pilote de la base de données :** nom du pilote utilisé par la JVM pour vous connecter à la base de données.

**Version du pilote de la base de données :** version du pilote utilisé par la JVM pour vous connecter à la base de données.

Le bouton **Enregistrer** permet d’enregistrer ces informations système dans un fichier de propriétés.
