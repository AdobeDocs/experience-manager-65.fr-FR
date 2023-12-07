---
title: Mappage d’un groupe d’utilisateurs personnalisé dans AEM 6.5
description: Découvrez comment fonctionne le mappage de groupes d’utilisateurs personnalisés dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 97%

---

# Mappage d’un groupe d’utilisateurs personnalisé dans AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparaison du contenu JCR associé au groupe d’utilisateurs personnalisé {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Anciennes versions d’AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugEnabled.</p> <p>Type de nœud déclaré : S/O, propriété résiduelle.</p> </td>
   <td><p>Autorisation :</p> <p>Nœud : rep:cugPolicy de type de nœud rep:CugPolicy.</p> <p>Type de nœud déclaré : rep:CugMixin.</p> <p> </p> <p> </p> <p> </p> Authentification :</p> <p>Type de Mixin : granite:AuthenticationRequired.</p> </td>
   <td><p>Pour restreindre l’accès en lecture, une politique de groupe d’utilisateurs personnalisé (CUG) dédiée est appliquée au nœud cible.</p> <p>REMARQUE : les politiques ne peuvent être appliquées qu’aux chemins d’accès pris en charge qui sont configurés.</p> <p>Les nœuds portant le nom rep:cugPolicy et de type rep:CugPolicy sont protégés et ne peuvent pas être écrits en utilisant des appels d’API JCR standard ; utilisez plutôt la gestion du contrôle d’accès JCR.</p> <p>Pour plus d’informations, consultez <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">cette page</a>.</p> <p>Pour exiger une authentification sur un nœud, il suffit d’ajouter le type de Mixin : granite:AuthenticationRequired.</p> <p>REMARQUE : valable uniquement sous les chemins d’accès pris en charge qui sont configurés.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugPrincipals.</p> <p>Type de nœud déclaré : S/O, propriété résiduelle.</p> </td>
   <td><p>Propriété : rep:principalNames.</p> <p>Type de nœud déclaré : rep:CugPolicy.</p> </td>
   <td><p>La propriété contenant les noms des entités de sécurité autorisées à lire le contenu sous le CUG restreint est protégée et ne peut pas être écrite à l’aide d’appels d’API JCR standard ; utilisez plutôt la gestion du contrôle d’accès JCR.</p> <p>Consultez <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">cette page</a> pour plus d’informations sur l’implémentation.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugLoginPage.</p> <p>Type de nœud déclaré : S/O, propriété résiduelle.</p> </td>
   <td><p>Propriété : granite:loginPath (facultatif).</p> <p>Type de nœud déclaré : granite:AuthenticationRequired.</p> </td>
   <td><p>Il est possible de définir un chemin de connexion alternatif pour un nœud JCR dont le type de mixin est granite:AuthenticationRequired.</p> <p>REMARQUE : valable uniquement sous les chemins d’accès pris en charge qui sont configurés.</p> </td>
  </tr>
  <tr>
   <td><p>Propriété : cq:cugRealm.</p> <p>Type de nœud déclaré : S/O, propriété résiduelle.</p> </td>
   <td>S/O</td>
   <td>Cela n’est plus pris en charge dans la nouvelle implémentation.</td>
  </tr>
 </tbody>
</table>

## Comparaison des services OSGi {#comparison-of-osgi-services}

**Anciennes versions d’AEM**

Libellé : prise en charge du groupe d’utilisateurs fermé (CUG) d’Adobe Granite.

Nom : com.day.cq.auth.impl.CugSupportImpl.

**AEM 6.5**

* Libellé : configuration de CUG Apache Jackrabbit Oak.

  Nom : org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration.

  ConfigurationPolicy = REQUIRED

* Libellé : liste d’exclusion de CUG Apache Jackrabbit Oak.

  Nom : org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl.

  ConfigurationPolicy = REQUIRED

* Nom : com.adobe.granite.auth.requirement.impl.RequirementService.
* Libellé : gestionnaire d’exigence d’authentification et de chemin de connexion d’Adobe Granite.

  Nom : com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler.

  ConfigurationPolicy = REQUIRED

**Commentaires**

* Configuration de l’autorisation de CUG et activation/désactivation de l’évaluation.
Service permettant de configurer la liste d’exclusion des principaux qui ne doivent pas être affectés par l’autorisation de CUG.

  >[!NOTE]
  > 
  >Si `CugExcludeImpl` n’est pas configuré, la configuration `CugConfiguration` revient à la valeur par défaut.

  Il est possible de réaliser une implémentation CugExclude personnalisée en cas de besoins spécifiques.

* Composant OSGI implémentant LoginPathProvider, qui expose un chemin de connexion correspondant à LoginSelectorHandler. Il comporte une référence obligatoire à RequirementHandler, qui est utilisé pour enregistrer l’observateur qui écoute les modifications des exigences d’authentification stockées dans le contenu par le biais du type de Mixin granite:AuthenticationRequired.
* Composant OSGI implémentant RequirementHandler qui informe SlingAuthenticator des modifications apportées à authrequirements.

  Comme la politique de configuration pour ce composant est obligatoire, elle n’est activée que si un ensemble de chemins pris en charge est spécifié.

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
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation if there are special needs.</p> </td>
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
