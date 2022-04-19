---
title: Home
description: 
published: true
date: 2022-04-18T11:44:45.973Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:37:19.117Z
---

```plantuml
package "devextreme-internal-tools" {
  (Declarations Discoverer) as Discoverer
  (TS Declarations Discoverer) as TsDiscoverer
  (Topics Generator) as TopicsGen
  (StrongMetaData Generator) as SmdGen
  (IntegrationData Generator) as IntegrationDataGen
  (NGMetaData Generator) as NGMetaDataGen
  (Descriptions Injector) as Injector
  (TS Bundler) as Bundler

  artifact "ts-member-meta.json" as TsDeclarationsJson
  artifact "Declarations.json" as DeclarationsJson
  artifact "Descriptions.json" as DescriptionsJson

}

database "devexteme" {
  artifact ".d.ts modules" as TSModules
  artifact ".js modules" as JSModules
  artifact "dx.all.d.ts" as TSBundle
}


database "devexteme-documentation" {
  artifact ".md files" as topics
}

rectangle "Integrations" {
  artifact "IntegrationData.json" as IntegrationData
  artifact NGMetaData.json as NGMetaData
  artifact StrongMetaData.json as StrongData  
  
  database Angular {
    (NG-wrappers Gen) as NgGen
    artifact "Angular Wrappers" as NgWrappers
  }  

  database React {
    artifact "React Wrappers" as ReactWrappers
    (React-wrappers Gen) as ReactGen
    
    IntegrationData --> ReactGen
    ReactGen --> ReactWrappers
  }
  
  database Vue {
    artifact "Vue Wrappers" as VueWrappers
    (Vue-wrappers Gen) as VueGen
  }
  
  database "hg/mobile" {
    artifact "ASP.NET Wrappers" as AspWrappers
    artifact "ASP.NET Core Wrappers" as AspCoreWrappers
    
    (MvcHelpers Gen) as MvcGen
  }

}

rectangle "Packages" {
  artifact "ASP.NET Nuget" as AspPackage
  artifact "ASP.NET Core Nuget" as AspCorePackage
  artifact "Angular Npm" as NgPackage
  artifact "React Npm" as ReactPackage
  artifact "Vue Npm" as VuePackage
}

TSModules -down---> TsDiscoverer
JSModules -down---> Discoverer

TsDiscoverer --> TsDeclarationsJson
TsDeclarationsJson --> Discoverer

topics -----> TopicsGen
topics <--.-- TopicsGen
TopicsGen --> DescriptionsJson
DescriptionsJson --> Injector


Discoverer --> DeclarationsJson

DeclarationsJson -left--> TopicsGen
DeclarationsJson ---> IntegrationDataGen
DeclarationsJson ---> (SmdGen)
DeclarationsJson ---> (NGMetaDataGen)
DeclarationsJson ---> Injector

IntegrationDataGen --> IntegrationData

ReactWrappers --> ReactPackage

IntegrationData --> VueGen
VueGen --> VueWrappers
VueWrappers --> VuePackage

(SmdGen) --> StrongData
(NGMetaDataGen) --> NGMetaData

TSModules -down-> Bundler
Bundler --> TSBundle

StrongData --> MvcGen
MvcGen --> AspWrappers
MvcGen --> AspCoreWrappers
AspWrappers --> AspPackage
AspCoreWrappers --> AspCorePackage

NGMetaData --> NgGen
NgGen --> NgWrappers
NgWrappers --> NgPackage
 
Injector --.--> NgWrappers
Injector -up-.-> TSModules
Injector -up-.-> TSBundle
Injector -.> AspWrappers
Injector -.-> AspCoreWrappers

```
