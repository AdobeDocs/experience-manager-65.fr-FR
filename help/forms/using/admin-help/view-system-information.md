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
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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

**Machine virtuelle : version** de la machine virtuelle Java (JVM) sur le serveur.

**Fournisseur de la machine virtuelle :** fabricant de la JVM.

**Version de la machine virtuelle :** numéro de version de la JVM

**Nom de la machine :** nom d’hôte du serveur sur lequel AEM forms est installé.

**Heure d’activation :**  heure (en heures et minutes) pendant laquelle le serveur a été exécuté.

**Compilateur juste à temps :** nom du compilateur utilisé.

**Temps de compilation :** temps passé à la compilation.

**Nombre de threads en direct :** nombre total de threads actuellement présents dans le système AEM forms.

**Pic du nombre de threads :** plus grand nombre de threads en direct jamais enregistrés sur le système.

**Nombre de classes chargées :** nombre de classes chargées dans la JVM.

**Nombre de classes déchargées :** nombre de classes déchargées de la JVM.

**Tas minimal :** quantité minimale de tas utilisée.

**Maximum Heap :** quantité maximale de tas utilisée.

**Nom du système d’exploitation :** nom du système d’exploitation s’exécutant sur le serveur AEM forms.

**Version du système d’exploitation :**  numéro de version du système d’exploitation s’exécutant sur le serveur AEM forms.

**Arche du système d’exploitation :** architecture du système d’exploitation sur laquelle la JVM est en cours d’exécution.

**Nombre de processeurs :** nombre de processeurs du système.

**Arguments de la machine virtuelle :** argument utilisé par la JVM.

**Chemin d’accès à la classe :** chemin d’accès à la classe utilisé par la JVM.

**Chemin d’accès à la bibliothèque :**  chemin d’accès à la bibliothèque utilisé par la JVM.

**Chemin d’accès de la classe de démarrage** : chemin d’accès de la classe de démarrage utilisé par la JVM.

**Type de serveur d’applications :** type de serveur d’applications utilisé pour exécuter AEM forms.

**Version du serveur d’applications :**  numéro de version du serveur d’applications utilisé pour exécuter AEM forms.

**Fournisseur du serveur d’applications :** fabricant du serveur d’applications utilisé pour exécuter AEM forms.

**Date d’installation :** date d’installation d’AEM forms (au format aaaa-mm-jj).

**AEM forms Version :** version d’AEM forms installée.

**Version du correctif :** AEM numéro de correctif des formulaires.

**Database Name :** type de base de données utilisé par AEM forms.

**Version de la base de données :** numéro de version de la base de données utilisée par AEM forms.

**Database Drive Name :** nom du pilote utilisé par la JVM pour se connecter à la base de données.

**Version du pilote de base de données :**  version du pilote utilisé par la JVM pour se connecter à la base de données.

Le bouton **Enregistrer** permet d’enregistrer ces informations système dans un fichier de propriétés.
