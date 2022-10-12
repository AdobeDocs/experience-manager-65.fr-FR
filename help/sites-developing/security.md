---
title: Sécurité
seo-title: Security
description: La sécurité des applications débute lors de la phase de développement.
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 76%

---

# Sécurité{#security}

La sécurité des applications débute lors de la phase de développement. Adobe recommande d’appliquer les méthodes de sécurité suivantes.

## Utilisation de la session de requête {#use-request-session}

En suivant le principe de moindre privilège, Adobe recommande que chaque accès au référentiel soit effectué en utilisant la session liée à la demande de l’utilisateur et au contrôle d’accès approprié.

## Protection contre les scripts de site à site (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette faille de sécurité peut être exploitée par des internautes malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de l’ensemble du contenu fourni par l’utilisateur lors de la sortie. La prévention du script intersite (XSS) se voit accorder la priorité la plus élevée lors des phases de développement et de test.

Le mécanisme de protection XSS proposé par AEM est basé sur la [Bibliothèque Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fournie par [OWASP (The Open Web Application Security Project)](https://www.owasp.org/). La configuration par défaut d’AntiSamy se trouve à l’adresse

`/libs/cq/xssprotection/config.xml`

Il est important que vous adaptiez cette configuration à vos besoins en matière de sécurité en recouvrant le fichier de configuration. Vous trouverez, dans la [documentation officielle d’AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project), toutes les informations nécessaires pour satisfaire vos exigences en matière de sécurité.

>[!NOTE]
>
>Il est vivement conseillé de toujours accéder à l’API de protection XSS en utilisant l’interface [XSSAPI fournie par AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

En outre, un pare-feu d’application Web, tel que [mod_security pour Apache](https://www.modsecurity.org), peut fournir un contrôle centralisé fiable sur la sécurité de l’environnement de déploiement, ainsi qu’une protection contre les attaques XSS qui n’étaient pas détectées précédemment.

## Accès aux informations de service cloud {#access-to-cloud-service-information}

>[!NOTE]
>
>Les listes de contrôles d’accès (ACL) relatives aux informations de service cloud, ainsi que les paramètres OSGi requis pour sécuriser votre instance sont automatisés dans le cadre du [mode Prêt pour la production](/help/sites-administering/production-ready.md). Cela signifie que vous ne devez pas apporter de modifications manuelles à la configuration. Cependant, il est conseillé de les passer en revue avant le déploiement proprement dit.

Lorsque vous [intégrez votre instance AEM dans Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md), vous utilisez des [configurations de service cloud](/help/sites-developing/extending-cloud-config.md). Les informations relatives à ces configurations, ainsi que les éventuelles statistiques collectées, sont stockées dans le référentiel. Si vous utilisez cette fonctionnalité, il est recommandé de vérifier si le niveau de sécurité par défaut relatif à ces informations répond à vos besoins.

Le module webservicesupport enregistre des statistiques et des informations de configuration sous :

`/etc/cloudservices`

Avec les autorisations par défaut :

* Environnement de création : `read` pour `contributors`

* Environnement de publication : `read` pour `everyone`

## Protection contre les attaques par falsification de requête intersite {#protect-against-cross-site-request-forgery-attacks}

Pour plus d’informations sur les mécanismes de sécurité utilisés par AEM pour atténuer les attaques CSRF, voir la section [Filtre de référent Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la liste de contrôle de sécurité et de la section [Documentation du framework de protection CSRF](/help/sites-developing/csrf-protection.md).
