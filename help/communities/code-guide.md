---
title: Consignes de codage
seo-title: Consignes de codage
description: Conseils, astuces et astuces pour les développeurs de communautés
seo-description: Conseils, astuces et astuces pour les développeurs de communautés
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Consignes de codage {#coding-guidelines}

## Instructions, conseils et conseils {#guidelines-tips-and-tricks}

La collaboration avec les communautés AEM est passée d’une dépendance importante envers les pages de serveur Java à une flexibilité dans le choix des langages de script de modèles où la logique métier, le style et le contenu des pages sont différents les uns des autres.

L’API SocialResourceProvider offre une plus grande flexibilité dans l’utilisation du contenu généré par l’utilisateur (UGC). Il n’est donc pas nécessaire de savoir quelle option [SRP](srp.md) a été choisie pour le déploiement.

Vous trouverez ci-dessous diverses instructions de codage et bonnes pratiques pour les développeurs AEM Communities :

### Code {#code}

* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - comment éviter d&#39;écrire une application qui ne fonctionne que lorsque UGC est stocké dans JCR (JSRP).
* [SocialUtils Refactoring](socialutils.md) - méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Conventions](naming-conventions.md) de dénomination - conventions de dénomination pour les classes Java personnalisées.

### Scripts {#scripts}

* [Téléchargement des composants](sideloading.md) de communautés : comment ajouter dynamiquement un composant après le chargement de la page.
* [Rich Text Editor Essentials](rte.md) - Comment personnaliser l’interface utilisateur en texte enrichi fournie aux membres pour publier du contenu.

### IDE {#ide}

* [Utilisation de Maven pour les communautés](maven.md) : comment inclure le fichier jar de l’API Communities.
* [SocialUtils Refactoring](socialutils.md) - méthodes d’utilitaire pour SRP qui remplacent SocialUtils.

