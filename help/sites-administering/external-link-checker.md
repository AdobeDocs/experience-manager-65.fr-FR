---
title: Vérificateur de lien externe
description: Le vérificateur de liens permet de valider les liens internes et externes et de réécrire les liens.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 100%

---

# Vérificateur de lien externe {#the-link-checker}

Les auteurs de contenu ne doivent pas avoir besoin de valider chaque lien qu’ils incluent dans leurs pages de contenu.

Le vérificateur de liens s’exécute automatiquement pour aider les créateurs et créatrices de contenu à gérer leurs liens, en prenant notamment en charge les tâches suivantes :

* La validation des liens lorsqu’ils sont ajoutés au contenu
* L’affichage d’une liste de tous les liens externes dans le contenu
* La réalisation des transformations de lien

Le vérificateur de liens comporte un certain nombre d’[options de configuration](#configuring), par exemple la définition de la validation interne, le pouvoir d’omettre certains liens ou certains modèles de liens de la validation, et la réécriture des règles de réécriture de liens.

Le vérificateur de liens valide les [liens internes](#internal) comme les [liens externes.](#external)

>[!NOTE]
>
>Le vérificateur de liens vérifiant les liens de chaque page de contenu, il peut avoir un impact sur les performances des référentiels volumineux. Dans ce cas, vous devrez peut-être [configurer la fréquence d’exécution du vérificateur de liens](#configuring) ou [le désactiver.](#disabling)

## Vérification des liens internes {#internal}

Les liens internes sont des liens vers d’autres contenus de votre référentiel AEM. Vous pouvez ajouter des liens internes à l’aide du sélecteur de chemin d’accès de l’éditeur de texte enrichi ou d’un composant personnalisé. Par exemple :

* Votre page `/content/wknd/us/en/adventures/ski-touring.html`
* contient un lien vers `/content/wknd/us/en/adventures/extreme-ironing.html` dans un [Composant Texte.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=fr)

Les liens internes sont validés dès que l’auteur du contenu ajoute un lien interne à une page. Si le lien devient non valide :

* il est supprimé de l’éditeur ; le texte du lien est conservé, mais le lien lui-même est supprimé ;
* il s’affiche sous la forme d’un lien rompu dans l’interface de création.

![Lien interne rompu lors de la création d’une page](assets/link-checker-invalid-link-internal.png)

## Vérification de lien externe {#external}

Les liens externes sont des liens vers du contenu placé en dehors de votre référentiel AEM. Vous pouvez ajouter des liens externes à l’aide de l’éditeur de texte enrichi ou d’un composant personnalisé. Par exemple :

* Votre page `/content/wknd/us/en/adventures/ski-touring.html`
* contient un lien vers `https://bunwarmerthermalunderwear.com` dans un [Composant Texte.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=fr)

Les liens externes sont validés en termes de syntaxe et de disponibilité. Cette vérification est effectuée de manière asynchrone sur un système interne configurable. Si le vérificateur de liens trouve un lien externe non valide :

* il est supprimé de l’éditeur ; le texte du lien est conservé, mais le lien lui-même est supprimé ;
* il s’affiche sous la forme d’un lien rompu dans l’interface de création.

![Lien interne rompu lors de la création d’une page](assets/link-checker-invalid-link-external.png)

En outre, l’interface du [Vérificateur de lien externe](#external-link-checker) fournit un aperçu de tous les liens externes de vos pages de contenu.

### Utilisation du Vérificateur de lien externe {#external-link-checker}

Pour utiliser le Vérificateur de lien externe, procédez comme suit :

1. À l’aide de la **navigation**, sélectionnez **Outils**, puis **Sites**.
1. Sélectionnez **Vérificateur de lien externe** et une liste de tous les liens externes est affichée.

![Fenêtre du Vérificateur de lien externe](assets/external-link-checker.png)

Les informations suivantes s’affichent :

* **Statut** - Le statut de validation du lien, qui peut être l’un des suivants :
   * **Valide** - Le lien externe est accessible par le vérificateur de liens.
   * **En attente** - Le lien externe a été ajouté au contenu du site, mais n’a pas encore été validé par le vérificateur de liens.
   * **Non valide** - Le vérificateur de liens ne peut pas accéder au lien externe.
* **URL** - Lien externe
* **Référent** - Page de contenu contenant le lien externe
   * Celle-ci n’est renseignée que [si elle est configurée.](#configuring)
* **Dernière vérification** - Dernière fois que le vérificateur de lien a validé le lien externe
   * La fréquence de vérification des liens [est configurable.](#configuring)
* **Dernier statut** - Dernier code de statut HTML renvoyé lors de la dernière vérification du lien effectuée sur le lien externe
* **Dernier disponible** - Temps écoulé depuis la dernière fois que le lien était disponible pour le vérificateur de liens
* **Dernier accès** - Temps écoulé depuis le dernier accès à la page contenant le lien externe dans l’interface de création

Vous pouvez manipuler le contenu de la fenêtre en utilisant les deux boutons situés en haut de la liste des liens :

* **Actualiser** - Pour actualiser le contenu de la liste
* **Vérifier** - Pour vérifier un lien externe individuel sélectionné dans la liste

### Fonctionnement du Vérificateur de lien externe {#how-it-works}

Bien qu’il soit facile à utiliser, le Vérificateur de lien externe repose sur plusieurs services, et comprendre leur fonctionnement peut vous aider à comprendre comment [configurer le Vérificateur de lien](#configuring) pour qu’il réponde à vos besoins.

1. Chaque fois qu’un auteur de contenu enregistre un lien vers une page, un gestionnaire d’événements est déclenché.
1. Le gestionnaire d’événements parcourt tout le contenu sous `/content` et recherche les liens nouveaux ou mis à jour et les ajoute à un cache pour le Vérificateur de liens.
1. Le **Service de vérification de lien Day CQ** s’exécute ensuite selon un calendrier régulier afin de vérifier les entrées du cache et la validité de leur syntaxe.
1. Les liens validés par la syntaxe s’affichent alors dans la fenêtre [Vérificateur de lien externe](#external-link-checker). Cependant, ils conserveront un statut **En attente**.
1. La **Tâche de vérification de lien Day CQ** s’exécute ensuite régulièrement pour valider les liens en effectuant un appel GET.
1. La **Tâche de vérification de lien Day CQ** met ensuite à jour les entrées de la fenêtre du Vérificateur de lien externe avec les résultats des appels GET.

## Configuration du Vérificateur de lien {#configuring}

Le Vérificateur de lien est automatiquement disponible dans AEM. Cependant, plusieurs configurations OSGi peuvent être modifiées pour modifier son comportement :

* **Service de stockage d’informations du Vérificateur de lien Day CQ** - Ce service définit la taille du cache du Vérificateur de liens dans le référentiel.
* **Service de vérification de lien Day CQ** - Ce service effectue une vérification asynchrone de la syntaxe des liens externes. Vous pouvez définir la période de vérification et les types de liens qui sont ignorés par le Vérificateur, parmi d’autres options.
* **Tâche de vérification de lien Day CQ** - Ce service effectue la validation GET des liens externes. Il permet de définir des intervalles distincts pour vérifier les liens bons et mauvais, parmi d’autres options.
* **Transformateur du Vérificateur de liens Day CQ** - Permet de convertir des liens en fonction d’un jeu de règles défini par l’utilisateur.

Consultez le document [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md) pour plus d’informations sur la modification des paramètres OSGi.

## Désactivation du Vérificateur de liens {#disabling}

Vous pouvez choisir de désactiver entièrement le Vérificateur de liens. Pour ce faire :

1. ouvrez la console OSGi ;
1. modifiez le **Transformateur du Vérificateur de liens Day CQ** ;
1. cochez la ou les options que vous souhaitez désactiver :
   * **Désactiver la vérification** - Pour désactiver la validation des liens
   * **Désactiver la réécriture** - Pour désactiver les transformations des liens

>[!NOTE]
>
>Si vous désactivez la vérification des liens après avoir commencé à créer votre contenu, il se peut que des entrées apparaissent toujours dans la [fenêtre du Vérificateur de lien externe](#external-link-checker), mais elles ne seront plus mises à jour.
