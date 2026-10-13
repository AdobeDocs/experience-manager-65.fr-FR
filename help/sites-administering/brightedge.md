---
title: Intégration à BrightEdge Content Optimizer
description: Découvrez l’intégration d’AEM à BrightEdge Content Optimizer.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 99%
---
# Intégration à BrightEdge Content Optimizer{#integrating-with-brightedge-content-optimizer}

Créez une configuration de cloud BrightEdge afin qu’AEM puisse se connecter à l’aide des informations d’identification de votre compte BrightEdge. Vous pouvez créer plusieurs configurations si vous utilisez plusieurs comptes.

Lorsque vous créez la configuration, vous spécifiez un titre. Le titre doit être éloquent afin que les gens puissent corréler la configuration au compte BrightEdge. Lorsqu’un auteur, une autrice, un administrateur ou une administratrice de page associe une page web au compte BrightEdge, ce titre est présenté dans une liste déroulante.

1. Sur le rail, cliquez sur Outils > Opérations > Cloud > Services cloud.
1. Cliquez sur le lien qui s’affiche dans la section BrightEdge Content Optimizer. La création ou non d’une configuration BrightEdge détermine le texte du lien :

   * Configurer maintenant : ce lien s’affiche lorsqu’aucune configuration n’a été créée.
   * Afficher les configurations : ce lien s’affiche lorsqu’une ou plusieurs configurations ont été créées.

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. Si vous avez cliqué sur Afficher les configurations, cliquez sur le lien + en regard de Configurations disponibles.
1. Saisissez un titre pour la configuration. Éventuellement, saisissez un nom pour le nœud utilisé afin de stocker la configuration dans le référentiel. Cliquez sur Créer.
1. Dans la boîte de dialogue Configuration de BrightEdge Content Optimizer, saisissez le nom d’utilisateur ou d’utilisatrice et le mot de passe du compte BrightEdge, puis cliquez sur OK.

## Modifier une configuration BrightEdge {#editing-a-brightedge-configuration}

Modifiez le nom d’utilisateur et le mot de passe d’une configuration BrightEdge, au besoin. Les modifications affectent toutes les pages qui utilisent la configuration.

1. Sur le rail, cliquez sur Outils > Opérations > Cloud > Services cloud.
1. Dans la section BrightEdge Content Optimizer, cliquez sur Afficher les configurations.

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. Cliquez sur le nom de la configuration que vous souhaitez modifier.
1. Cliquez sur Modifier, modifiez les valeurs de propriété, puis cliquez sur OK.

## Associer des pages à une configuration BrightEdge {#associating-pages-with-a-brightedge-configuration}

Associez des pages à une configuration BrightEdge pour envoyer des données de page au service BrightEdge pour analyse. Lorsque vous associez une page à une configuration, les pages enfants héritent de l’association. En règle générale, vous associez la page d’accueil de votre site afin que les données de toutes les pages soient envoyées à BrightEdge.

1. Ouvrez la console Sites web classique. ([&#128279;](http://localhost:4502/siteadmin#/content))
1. Dans l’arborescence des sites web, sélectionnez le dossier ou la page qui contient la page à associer à la configuration BrightEdge.
1. Dans la liste des pages, cliquez avec le bouton droit sur la page à configurer, puis cliquez sur Propriétés.
1. Dans l’onglet Services cloud, cliquez sur le bouton Ajouter un service. Dans la boîte de dialogue Services cloud, sélectionnez BrightEdge Content Optimizer, puis cliquez sur OK.
1. Dans la liste BrightEdge Content Optimizer, sélectionnez la configuration BrightEdge à associer à la page, puis cliquez sur OK.

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## Activer une configuration BrightEdge {#activating-a-brightedge-configuration}

Activez une configuration BrightEdge pour la répliquer sur l’instance de publication et permettre aux pages publiées d’interagir avec le service BrightEdge.

1. Sur le rail, cliquez sur Sites, puis recherchez et sélectionnez la page que vous avez associée à la configuration BrightEdge.
1. Cliquez sur l’icône Publier, puis sur Publier.

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. Dans la liste des configurations qui s’affichent, assurez-vous que la configuration BrightEdge est sélectionnée, puis cliquez sur Publier.

   ![chlimage_1-8](assets/chlimage_1-8a.png)
