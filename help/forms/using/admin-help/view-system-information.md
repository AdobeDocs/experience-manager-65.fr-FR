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

**Machine virtuelle :** Version de la machine virtuelle Java (JVM) sur le serveur.

**Fournisseur d&#39;ordinateurs virtuels :** Fabricant de la JVM.

**Version de l&#39;ordinateur virtuel :** Numéro de version de la JVM

**Nom de la machine :** Nom d’hôte du serveur sur lequel AEM forms est installé.

**Durée de fonctionnement :** Heure, en heures et minutes, pendant laquelle le serveur est en cours d&#39;exécution.

**Compilateur juste à temps :** Nom du compilateur utilisé.

**Temps de compilation :** Durée de la compilation.

**Nombre de threads dynamiques :** Nombre total de threads actuellement présents dans le système de formulaires AEM.

**Pic du nombre de threads :** Plus grand nombre de threads dynamiques jamais enregistrés sur le système.

**Nombre de classes chargées :** Nombre de classes chargées dans la JVM.

**Nombre de classes déchargées :** Nombre de classes déchargées de la JVM.

**Tas minimum :** Quantité minimale de tas utilisée.

**Tas maximum :** Quantité maximale de tas utilisée.

**Nom du système d’exploitation :** Nom du système d’exploitation s’exécutant sur le serveur AEM forms.

**Version du système d’exploitation :** Numéro de version du système d’exploitation s’exécutant sur le serveur AEM forms.

**Arche du système d&#39;exploitation :** Architecture du système d’exploitation sur lequel la JVM s’exécute.

**Nombre de processeurs :** Nombre de processeurs sur le système.

**Arguments de la machine virtuelle :** Argument utilisé par la JVM.

**Chemin de classe :** Chemin de classe utilisé par la JVM.

**Chemin d’accès à la bibliothèque :** Chemin d’accès à la bibliothèque utilisé par la JVM.

**Chemin de classe de démarrage :** Chemin de classe de démarrage utilisé par la JVM.

**Type de serveur d’applications :** Type de serveur d’applications utilisé pour exécuter AEM formulaires.

**Version du serveur d’applications :** Numéro de version du serveur d’applications utilisé pour exécuter AEM formulaires.

**Fournisseur du serveur d’applications :** fabricant du serveur d’applications utilisé pour exécuter AEM formulaires.

**Date d&#39;installation :** Date (format aaaa-mm-jj) à laquelle AEM formulaires ont été installés.

**Version des formulaires AEM :** Version des formulaires AEM installés.

**Version du correctif :** aem numéro de correctif des formulaires.

**Nom de la base de données :** Type de base de données utilisée par AEM forms.

**Version de la base de données :** Numéro de version de la base de données utilisée par AEM forms.

**Database Drive Name :** nom du pilote utilisé par la JVM pour se connecter à la base de données.

**Version du pilote de base de données :** Version du pilote utilisé par la JVM pour se connecter à la base de données.

Le bouton **Enregistrer** permet d’enregistrer ces informations système dans un fichier de propriétés.
