---
title: Sécurité
description: La sécurité des applications commence pendant la phase de développement.
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 48%

---

# Sécurité{#security}

La sécurité des applications commence pendant la phase de développement. Adobe recommande d’appliquer les bonnes pratiques de sécurité suivantes.

## Utilisation de la session de requête {#use-request-session}

Selon le principe de moindre privilège, Adobe recommande d’effectuer chaque accès au référentiel en utilisant la session liée à la requête de l’utilisateur et au contrôle d’accès approprié.

## la fonctionnalité Protection contre les failles cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette vulnérabilité de sécurité peut être exploitée par des utilisateurs et utilisatrices web malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de tout le contenu fourni par l’utilisateur ou l’utilisatrice en sortie. La prévention contre les failles XSS se voit accorder la priorité la plus élevée lors des phases de développement et de test.

Le mécanisme de protection XSS fourni par AEM est basé sur le [Bibliothèque Java™ AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fourni par [OWASP (The Open Web Application Security Project)](https://owasp.org/). La configuration par défaut d’AntiSamy se trouve à l’adresse

`/libs/cq/xssprotection/config.xml`

Il est important que vous adaptiez cette configuration à vos besoins en matière de sécurité en recouvrant le fichier de configuration. Le fonctionnaire [Documentation AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fournit toutes les informations dont vous avez besoin pour mettre en oeuvre vos exigences de sécurité.

>[!NOTE]
>
>Adobe vous recommande de toujours accéder à l’API de protection XSS à l’aide du [XSSAPI fourni par AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

En outre, un pare-feu d’application web, tel que le [mod_security pour Apache](https://www.modsecurity.org), peut fournir un contrôle centralisé fiable sur la sécurité de l’environnement de déploiement, ainsi qu’une protection contre les attaques XSS qui n’étaient pas détectées précédemment.

## Accès aux informations du Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Les listes de contrôle d’accès des informations du Cloud Service et les paramètres OSGi requis pour sécuriser votre instance sont automatisés dans le cadre de la [Mode Prêt pour la production](/help/sites-administering/production-ready.md). Cela signifie que vous n’avez pas besoin de modifier la configuration manuellement, mais il est toujours recommandé de les passer en revue avant de passer en ligne à votre déploiement.

Lorsque vous [intégrer votre instance AEM à Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md), vous utilisez [Configurations Cloud Service](/help/sites-developing/extending-cloud-config.md). Les informations relatives à ces configurations, ainsi que les statistiques collectées, sont stockées dans le référentiel. Adobe recommande que, si vous utilisez cette fonctionnalité, vous déterminiez si la sécurité par défaut de ces informations correspond à vos besoins.

Le module webservicesupport écrit des statistiques et des informations de configuration sous :

`/etc/cloudservices`

Avec les autorisations par défaut :

* Environnement de création : `read` pour `contributors`

* Environnement de publication : `read` pour `everyone`

## Protection contre les attaques CRSF {#protect-against-cross-site-request-forgery-attacks}

Pour plus d’informations sur les mécanismes de sécurité mis en œuvre par AEM pour limiter les attaques CSRF, reportez-vous à la section [Filtre du référent Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la liste de contrôle de sécurité et à la [documentation du framework de protection CSRF](/help/sites-developing/csrf-protection.md).
