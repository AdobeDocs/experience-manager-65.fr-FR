---
title: Consignes de codage
description: Conseils, astuces et instructions pour les développeurs de communautés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%
---
# Consignes de codage {#coding-guidelines}

## Conseils, astuces et astuces {#guidelines-tips-and-tricks}

L’utilisation d’AEM Communities a évolué, passant d’une forte dépendance aux pages de serveur Java à une flexibilité dans le choix des langages de script de modèle où la logique commerciale, le style et le contenu des pages sont distincts les uns des autres.

Pour plus de flexibilité dans l’utilisation du contenu généré par l’utilisateur (UGC), utilisez l’API SocialResourceProvider, ce qui élimine la nécessité de connaître l’option [SRP](srp.md) choisie pour le déploiement.

Voici quelques instructions et bonnes pratiques en matière de codage pour les développeurs AEM Communities :

### Code {#code}

* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Comment éviter d’écrire une application qui ne fonctionne que lorsque le contenu créé par l’utilisateur est stocké dans JCR (JSRP).
* [SocialUtils Refactoring](socialutils.md) - méthodes d&#39;utilitaire pour SRP qui remplacent SocialUtils.
* [Conventions de nommage](naming-conventions.md) - conventions de nommage pour les classes Java personnalisées.

### Scripts {#scripts}

* [Chargement latéral des composants de communautés](sideloading.md) - Comment ajouter dynamiquement un composant après le chargement de la page.
* [Principes de base de l’éditeur de texte enrichi](rte.md) - Comment personnaliser l’interface utilisateur de texte enrichi fournie aux membres pour la publication de contenu.

### IDE {#ide}

* [Utilisation de Maven pour Communities](maven.md) - Comment inclure le fichier jar de l’API Communities.
* [SocialUtils Refactoring](socialutils.md) - méthodes d&#39;utilitaire pour SRP qui remplacent SocialUtils.
