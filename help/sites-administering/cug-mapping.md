---
title: Mappage d’un groupe d’utilisateurs personnalisé dans AEM 6.5
seo-title: Mappage d’un groupe d’utilisateurs personnalisé dans AEM 6.5
description: Découvrez le fonctionnement du mappage d’un groupe d’utilisateurs personnalisé dans AEM.
seo-description: Découvrez le fonctionnement du mappage d’un groupe d’utilisateurs personnalisé dans AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 74%

---

# Mappage d’un groupe d’utilisateurs personnalisé dans AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparaison du contenu JCR associé aux groupes d’utilisateurs fermés {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Anciennes versions d’AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugEnabled</p> <p>Type de nœud indiqué : N/A, propriété résiduelle</p> </td>
   <td><p>Autorisation :</p> <p>Nœud : rep:cugPolicy, type de nœud : rep:CugPolicy</p> <p>Type de nœud indiqué : rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Authentification:</p> <p>Type de mixin : granite:AuthenticationRequired</p> </td>
   <td><p>Pour restreindre l’accès en lecture, une stratégie de CUG dédiée est appliquée au nœud cible.</p> <p>REMARQUE : les stratégies s’appliquent uniquement aux chemins d’accès pris en charge.</p> <p>Les nœuds rep:cugPolicy de type rep:CugPolicy sont protégés et ne peuvent pas être écrits à l’aide des appels standard de l’API JCR. Vous devrez utiliser la fonctionnalité de gestion du contrôle d’accès JCR.</p> <p>Pour plus d’informations, consultez <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">cette page</a>.</p> <p>Afin d’appliquer les exigences d’authentification sur un noeud, il suffit d’ajouter le type de mixin granite:AuthenticationRequired.</p> <p>REMARQUE : valable uniquement sous les chemins d’accès pris en charge qui sont configurés.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugPrincipals</p> <p>Type de nœud indiqué : N/A, propriété résiduelle</p> </td>
   <td><p>Propriété : rep:principalNames</p> <p>Type de nœud indiqué : rep:CugPolicy</p> </td>
   <td><p>La propriété contenant les noms des principaux autorisés à lire le contenu sous le CUG restreint est protégée et ne peut pas être écrite à l’aide des appels standard de l’API JCR. Vous devrez utiliser la fonctionnalité de gestion du contrôle d’accès JCR.</p> <p>Pour en savoir plus sur l’implémentation, consultez <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">cette page</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugLoginPage</p> <p>Type de nœud indiqué : N/A, propriété résiduelle</p> </td>
   <td><p>Propriété : granite:loginPath (facultative)</p> <p>Type de nœud indiqué : granite:AuthenticationRequired</p> </td>
   <td><p>Un noeud JCR dont le type de mixin granite:AuthenticationRequired est défini peut éventuellement définir un autre chemin de connexion.</p> <p>REMARQUE : valable uniquement sous les chemins d’accès pris en charge qui sont configurés.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugRealm</p> <p>Type de nœud indiqué : N/A, propriété résiduelle</p> </td>
   <td>NA</td>
   <td>Plus pris en charge depuis la nouvelle implémentation.</td>
  </tr>
 </tbody>
</table>

## Comparaison des services OSGI {#comparison-of-osgi-services}

**Anciennes versions d’AEM**

Étiquette : prise en charge des groupes d’utilisateurs fermés (CUG) par Adobe Granite

Nom : com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Étiquette : configuration de CUG Apache Jackrabbit Oak

   Nom : org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* Étiquette : liste d’exclusion de CUG Apache Jackrabbit Oak

   Nom : org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* Nom : com.adobe.granite.auth.requirement.impl.RequirementService
* Étiquette : gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite

   Nom : com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**Commentaires**

* Configuration de l’autorisation de CUG et activation/désactivation de l’évaluation.
Service permettant de configurer la liste d’exclusion des entités qui ne doivent pas être affectées par l’autorisation CUG.

   >[!NOTE]
   > 
   >Si `CugExcludeImpl` n&#39;est pas configuré, `CugConfiguration` revient à la valeur par défaut.

   Il est possible de connecter une implémentation CugExclude personnalisée en cas de besoins spéciaux.

* Composant OSGI implémentant LoginPathProvider, qui expose un chemin de connexion correspondant à LoginSelectorHandler. Il comporte une référence obligatoire à RequirementHandler, utilisé pour enregistrer l’observateur qui surveille les exigences d’authentification modifiées stockées dans le contenu via le type de mixin granite:AuthenticationRequired.
* Composant OSGi implémentant RequirementHandler qui avertit SlingAuthenticator des modifications apportées aux exigences d’authentification.

   Comme la stratégie de configuration de ce composant est REQUISE, elle ne sera activée que si un ensemble de chemins pris en charge est spécifié.

   L’activation du service lance RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
