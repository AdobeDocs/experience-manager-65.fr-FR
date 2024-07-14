---
title: Consignes de codage
description: Conseils, astuces et conseils pour les développeurs de communautés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Consignes de codage {#coding-guidelines}

## Conseils, astuces et astuces {#guidelines-tips-and-tricks}

L’utilisation d’AEM Communities est passée d’une dépendance importante à Java Server Pages à une flexibilité dans le choix de langages de script de modèle dans lesquels la logique commerciale, le style et le contenu de page sont différents les uns des autres.

L’API SocialResourceProvider offre une plus grande flexibilité pour l’utilisation du contenu généré par l’utilisateur, ce qui évite d’avoir à savoir quelle option [SRP](srp.md) a été sélectionnée pour le déploiement.

Vous trouverez ci-dessous diverses instructions de codage et bonnes pratiques pour les développeurs AEM Communities :

### Code {#code}

* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Comment éviter d’écrire une application qui ne fonctionne que lorsque le contenu créé par l’utilisateur est stocké dans JCR (JSRP).
* [Refactorisation de SocialUtils](socialutils.md) - Méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Conventions d’affectation de nom](naming-conventions.md) : conventions d’affectation de nom pour les classes Java personnalisées.

### Scripts  {#scripts}

* [Transfert de composants de communautés](sideloading.md) - Comment ajouter dynamiquement un composant après le chargement de la page.
* [Rich Text Editor Essentials](rte.md) - Comment personnaliser l’interface utilisateur de texte enrichi fournie aux membres pour la publication de contenu.

### IDE {#ide}

* [Utilisation de Maven pour Communities](maven.md) - Comment inclure le fichier JAR de l’API Communities.
* [Refactorisation de SocialUtils](socialutils.md) - Méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
