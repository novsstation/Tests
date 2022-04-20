---
title: ASP.NET MVC/Core Manual - Wrappers, Wizards, Scaffolders
description: 
published: true
date: 2022-04-20T08:02:16.820Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:53:59.180Z
---

# 1. MVC Врапперы

Запускаем солюшн:  *<HG>\\DevExtreme.AspNet.Mvc\\DevExtreme.AspNet.Mvc.Lib-Dev.sln*

Солюшн имеет три основных проекта:

**AspNet.Mvc.Generator** - Проект предназначен для генерации врапперов ( .cs файлов описывающих виджеты по генерённой из документации декларации )

**AspNet.Mvc** - генерит ДЛЛку для ASP.NET MVC проектов

**AspNet.Core** - генерит ДЛЛку для ASP.NET Core проектов

![](https://lh6.googleusercontent.com/f-k2EMLqc51Iy35z3Vmi9E5eOcj8xq7ACl3kk44ZIYX_d8TzPj0CyBQwbBfDqc3eAw5FSE45Q66IoWkdxJWNhMQGLgmO-wTJ8I8PnkAGivp7DQ6w-j10B1TKXkqF1T-ZrfgKxCcN)

## 1.1 Генератор

На событии “PostBuildSteps” обновляет StrongMetaData.json файл, на основании контента генерит MVC/Core врапперы.

Открываем “Program.cs” и смотрим чего он делает.

## 1.2 ASP.NET MVC/Core Врапперы и Тесты

Для MVC и Core врапперов общие файлы кода. Все отличия между MVC/Core разделяются через конструкцию:

```cs
#if ASPNETCORE
#else
#endif
```

Только часть файлов генерённая, они помечены расширением \[.g.cs\]. Большая часть самописная, та логика которая специфична MVC подходу.

Некоторые моменты:

**Локализация** Реализуется объектом CldrDataScriptBuilder.cs пример можно увидеть в демке

[_https://demos.devexpress.com/ASPNetCore/Demo/Localization/UsingGlobalize/_](https://demos.devexpress.com/ASPNetCore/Demo/Localization/UsingGlobalize/)

**DataAnnotation** Реализутся объектом DataAnnotationsHelper.cs

**Рендер функция** этот объект рендерит виджет Renderer.cs

Ферма:

Таска   <name>DevExtreme MVC Unit tests ($(Version) tip)</name>

            <name>DevExtreme MVC.AspNetCore Unit tests ($(Version) tip)</name>

Файл   ./Sever/config/devextreme-22.1.xml

## 1.3 AspNet.Data

**GitHub проект DevExtreme.AspNet.Data**

[_https://github.com/DevExpress/DevExtreme.AspNet.Data_](https://github.com/DevExpress/DevExtreme.AspNet.Data)

**Апдейт версии ДЛЛки используемой в проекте.**

Запусти PS файл, в аргумент передать актуальную версию:

<HG>\\DevExtreme.AspNet.Mvc\\Update-AspNet-Data.ps1  
Открыть ченьжи в TortoiseHg и проверить правильность изменений.

Также в репозитории демок выполнить этот файл, для демок:

[_https://github.com/DevExpress/devextreme-demos/blob/22\_1/utils/internal/update-aspnet-data.js_](https://github.com/DevExpress/devextreme-demos/blob/22_1/utils/internal/update-aspnet-data.js)

# 2. VisualStudio VS 2019 and older

Запускаем солюшн: *<HG\_MOBILE>\\DevExtreme.AspNet.Mvc\\ DevExtreme.AspNet.Mvc.VisualStudio.sln*

## 2.1 Инсталяха и распаковка VSIX экстеншнов в установленные студии

*<HG>\\DevExtreme.AspNet.Mvc\\DevExtreme.AspNet.Mvc.Installer\\DevExtreme.AspNet.Mvc.Installer.csproj*

Назначение: Выполнение дополнительных действий связанных с инсталляцией (Запускается из основной setup-инсталяхи):

-   Определение списка установленных экземпляров студий
-   Распаковка VSIX,VSIX\_VS2022 экстеншнов в необходимые каталоги этих студий
-   Распаковка необходимых прожект-темплейтов в зависимости от версии VS

## 2.2 Генерация проектов ProjectWizards

Путь: *<HG\_MOBILE>\\DevExtreme.AspNet.Mvc\\DevExtreme.AspNet.Mvc.ProjectWizards\\*

Назначение: Генерация прожект темплейтов.  
 

### 2.2.1 Шаблоны проектов

Все шаблоны проектов расположены в директории “ProjectTemplates”

-   CSharpMvc5App
-   VBasicMvc5App
-   CSharpAspNetCoreApp

Конфигурации находится в файлах с расширением ”\*.vstemplate”

Имплементация прожект темплейтов находится в файле **Wizard.cs**

```cs
class Wizard : IWizard { }
```

Проекты из шаблонов **CSharpMvc5App**, **VBasicMvc5App** генерятся с минимальными изменениями и модификациями.

Шаблон **CSharpAspNetCoreApp** генерится на основании выбранной пользователем конфигурации.

При выборе пользователем проекта **CSharpAspNetCoreApp** будет запущен ProjectWizard диалоговое окно по окончании генерится проект.

Файл **WizardDialog.xaml** содержит форму и описывает логику диалогового окна.  
 

### 2.2.2 Эмбедед CS-файлы и ресурсы

Все необходимые файлы из которых конфигурируется содержимое проектов находится в директории “TemplateFiles” и структурированы относительно платформ/версий/layout’a

В файле **Wizard.cs** в методе:

```cs
public void ProjectFinishedGenerating(Project project) {
```

осуществляется добавление проекта необходимыми файлами.  
 

### 2.2.3 ProjectWizard тесты

<./DevExtreme.AspNet.Mvc.ProjectWizards.Tests.csproj>

Ферма:

Таска   <name>DevExtreme MVC VS Wizards Unit tests ($(Version) tip)</name>

Файл   ./Sever/config/devextreme-22.1.xml   
 

## 2.3 Скафолдинг

Вся необходимая логика касательно скаффолеров находится в проекте **DevExtreme.AspNet.Mvc.Scaffolding**

Проекты перечисленные ниже являются оверрайдами вышеуказанного и необходимы для работы скаффолдеров в студиях конкретных версий:

```plaintext
DevExtreme.AspNet.Mvc.Scaffolding.NetCore
DevExtreme.AspNet.Mvc.Scaffolding.NetCore.Legacy
DevExtreme.AspNet.Mvc.Scaffolding.NetCore.VS16
DevExtreme.AspNet.Mvc.Scaffolding.NetCore.VS16.1
DevExtreme.AspNet.Mvc.Scaffolding.VS16.6
DevExtreme.AspNet.Mvc.Scaffolding.VS16.9
```

Для компилирования их также используются референсы на зависимые ДЛЛки которые содержат необходимые базовые классы и методы

```plaintext
<HG>\DevExtreme.AspNet.Mvc\dlls\Microsoft.AspNet.Scaffolding
```

Скаффолдеры предназначены для генерации дополнительного контента:

-   Файлы с HTML разметкой в директории View/Page со биндингом с основными DX виджетами. DataGrid, TreeList, Form
-   API контроллеры c реализованными CRUD операциями. Поддерживаемые базы EntityFramework, XPO
-   Angular компоненты, работает только с проектом “ASP.NET Core with Angular”

Основные объекты скаффолдеров:

-   Фабрики. Нужны для регистрирования “Scaffolded Item” в соответствующем окне VS и создание инстанса соответствующего коде-генератора
-   Генераторы кода ( CodeGenerator ) непосредственно создают необходимые файлы и наполняют их контентом.
-   Шаблоны ( система TextTemplateEngine, файлы с расширением .t4 ) являются шаблонами по которому генерится контент.  
     

### 2.3.1 Фабрики

Объекты необходимые для регистрации скаффолдер айтемов в диалоговом окне:

**AngularComponentFactory.cs** - фабрика скаффолдеров для ASP.NET Core With Angular проектов

**ApiControllerWithActionsFactory.cs** - фабрика скаффолдеров для API контроллеров

**ViewWithModelBindingFactory.cs** - фабрика скаффолдеров для Views/Pages

**DevExtremeCodeGeneratorFactory.cs** - базовый класс

![](https://lh4.googleusercontent.com/d2Pwf8xUHkbY_KM-1jKY8A_9VBh-oS5Bv_-VK4VjcU5m8W87WG9cBdZQd2F5y5IAuP3sOX_o_R3JOtRQ0vb4DFxrG0qojGoM8hMCXjWtsKkSqake2Kxp1Prmgeik2z27VJ81J9uv)

Фабрики имеют ключевые/переопределённые методы::

**IsSupported** - здесь определяется тип выбранного проекта и результат true/false в зависимости от назначения фабрики.

**CreateInstance** - возвращает экземпляр скаффолдера  
 

### 2.3.2 Генераторы

Это объекты унаследованные от объекта CodeGenerator.

**AngularComponentScaffolder.cs** - генерирует необходимый контент для ASP.NET Core With Angular проектов

**ApiControllerWithActionsScaffolder.cs** - генерирует необходимый контент для API контроллеров

**XpoControllerWithActionsScaffolder.cs** - генерирует необходимый контент для XPO контроллеров

**ViewWithModelBindingScaffolder.cs** - генерирует необходимый контент для Views/Pages

**DevExtremeDependencyCodeGenerator.cs** - генерирует зависимый DevExtreme контент ( devextreme.aspnet.mvc.dll, devextreme.aspnet.data.dll )

**ApiDependencyCodeGenerator.cs** - генерирует зависимый контент, необходимый для работы контроллеров ( при необходимости, DLL’s)

Ключевые/переопределённые методы:

```cs
public override bool ShowUIAndValidate() {
```

Проверка, возможность показа какого-то диалогового окна, валидация. Проверяет булевское значение.

```cs
public override void GenerateCode() {
```

Генерация файлов и контента. Вызовется если ShowUIAndValidate() === true  
 

### 2.3.3 Шаблоны

Директория “Templates” содержит файлы с расширением .t4

Используются в КодеГенераторах, через метод “AddFileFromTemplate”

В аргументах метода передается модель соответствующая типу скаффолдера.

Эти модели генерятся специальными генераторами в файле “Generators/TextTemplateModelGenerator.cs”

Шаблоны расположенные в директории для Angular проектов, предназначены для формирования структуры данных которые впоследствии будут переданы в Schematics’ы. Подробности в соответствующей главе.  
 

>  Schematics - это механизм схожий со скаффолдерами, но только для среды Angular

### 2.3.4 Диалоговые окна

Директория UI содержит xaml формы сбора пользовательской информации:

**AddControllerDialog.xaml** - Окно генерации API контроллеров

**AddViewDialog.xaml** - Окно генерации View/Pages

**NewControllerDialog.xaml** - Небольшая форма для выбора имени контроллера

**SelectLayoutDialog.xaml** - Выбор лейаута  
 

### 2.3.5 ViewModel

Объект “DialogViewModel” самая главная часть скаффолдеров,

Содержит всю необходимую информацию о:

-   заселекченом проекте ( имя, расположение, тип проекта, всех объектах \[DbContext, DbModel\] которые содержит проект )
-   конфигурацию указанную пользователем: ДБ контекст, модель, контроллер, виджет для связывания с CRUD контроллером  
     

### 2.3.6 Roslyn - анализ файлов в проекте

> DevExtreme’ские коде-генераторы основаны на **Microsoft.AspNet.Scaffolding** и тянут за собой все необходимые сервисы, в том числе сервисы которые возвращают типы объектов ( DbContext, DbModel ). Для случаев когда необходимо использовать DevExtreme’ский скаффолдинг в обход стандартных механизмов, то получать типы объектов необходимо самостоятельно через анализ кода Microsoft.Analysis ( Roslyn )  
>   
> Есть следующие анализилки:

-   Для всех объектов
-   Для EntityFramework объектов
-   Для XPO объектов

![](https://lh6.googleusercontent.com/iVsdG4GINP29_ICmVQmn1L3XleBfxaR_eXBmX-e3RhK28Z8McS9yIeAquZBZI_7rLo7zArY_X8g8cv8noqAlVP9ROWkzWeKLpITy-STAJfI95Yprk8X9zs9VdAWksZO2Hb7pqSgI)

### 2.3.7 Скаффолдеры Тесты

<DevExtreme.AspNet.Mvc.Scaffolding.Tests.csproj>

Это Юнит тесты. В тестах в основном проверяется ( каталог “ScaffoldersTests” ) правильность генерации

-   моделей для скаффолинг шаблонов на основе каких-то вводных
-   и непосредственно сама генерация разметки из шаблонов и сравнение с эталонами

Файлы-тесты в каталоге “ScaffoldersTests” тестируют основные сценарии для шаблонов.

Файлы-тесты в рутовой директории тестируют частные сценарии, в том числе пользовательские сценарии из тикетов.

Для тестов используются тестовые проекты в солюшн-фолдере “Scaffolding.Tests.Projects”

![](https://lh5.googleusercontent.com/xf_g7U7FCvsbvHftElk6kX-jsz1yLm2lAOmEtytvl5ajgR-Q4Q_Ahy_O-Yv9-tWc7SAi0ZK1FEYwDliskhvih9LuiG0lqv1qoTJXWPt0E1YHurPGz5rKKvHCd3rENtquB-DPBs4D)

В тестах реализована кастомная имплементация движка TextTemplateEngine :

![](https://lh5.googleusercontent.com/zId7jO2dENo5RtiDyz1aZsL3avQ5dxpubNrk3WExmbYD55j4aVaSy63olQhBauuvXYSze7exj9Fj0bGtG5MANbLC1GzlpZTnzC1PAIp6YTtAJLKTlMwfnMT0FMPLUA90Kxcojl-B)

Для работы TextTemplateEngine ипмплементации в этих тестах, в частности на ферме, необходимо в GAC’е иметь следующие ассембли:

-   Microsoft.CodeAnalysis.dll
-   Microsoft.CodeAnalysis.CSharp.dll
-   System.Reflection.Metadata.dll

Эти сборки размещаются в GAC’е консольными командами на ПостБилд событии проекта.

![](https://lh5.googleusercontent.com/z2G10-EiT7xwkhNXHL5mqz2fbKm24BPPDSHXduxsTJq-ZqfutgNP0dOrnKvjBffNQys1oqOnzjflfOLhDA0JKa98_exVgSzgrEr5dZN8KF8JdFC2IphG21__WT95xuAmcKBT1nh8)

Ферма:

Таска   <name>DevExtreme MVC VS Scaffolding Unit tests ($(Version) tip)</name>

Файл   ./Sever/config/devextreme-22.1.xml   
 

### 2.4 Schematics

Каталог  *<HG>\\DevExtreme.AspNet.Mvc\\DevExtreme.AspNet.Mvc.Schematics*

Это CLI тулза для генерации компонентов для Angular проектов.

Компонент, аналогично вьюхам в “ASP.NET Core” проектах, будет содержать контент с выбранным виджетом и биндингом к API контроллеру.

Схематик будет сбилжен, запакован в tgz архив и добавлен в каталог к VisualStudio проекту на PreBuild эвенте VisualStudio проекта:

![](https://lh3.googleusercontent.com/RRCUwgVGS_NsZ_dIeBZmDPUHLpXnoTsczMnNeDeSTaAssN_p3FqeGZ1VsNguuNH0j-JGNH9Ua6eEkXxW2jnUDCNoT27uVYhDb99sHdnoDXWwKu2mTVYNYCf1dx-rD2FveTUaFUn4)

### 2.5 Экстеншн VSIX

Проект **DevExtreme.AspNet.Mvc.VisualStudio**

Этот проект осуществляет сборку VSIX файла.

Важные файлы:

**\- source.extension.vsixmanifest**

содержит конфигурацию VSIX файла

**\- Monikers.imagemanifest**

содержит ссылки на иконки необходимые для отображения UI элементов

**\- ConvertToDevExtremeCommand.cs**

настройка элемента контекстного меню для Добавления/Апдейта DevExtreme ресурсов”"Add/Upgrade DevExtreme to the Project"”

**\- InsertDevExtremeControlCommand.cs**

настройка элемента контекстного меню для скаффолдеров “Insert a DevExtreme Control Here”  
 

### 2.5 Экстеншн VSIX 2022

DevExtreme.AspNet.Mvc.VisualStudio.VS2022.sln

Для сборки VSIX’а под VS2022 были сделаны следующие проекты:

-   DevExtreme.AspNet.Mvc.ProjectWizards.VS17
-   DevExtreme.AspNet.Mvc.Scaffolding.NetCore.VS17
-   DevExtreme.AspNet.Mvc.Scaffolding.VS17
-   DevExtreme.AspNet.Mvc.VisualStudio.VS17

Эти проекты имеют общий код с проектами со схожим именем без постфикса “.VS17”

То бишь проекты для VS2022 имеют только конфиг и референсы на NuGet пакеты отличные от предыдущих студий.

Все отличия между VS2022/VS2019 разделяются через конструкцию:

```cs
#if DXVS2022
#else
#endif
```

> Для экономия на времени сборки в VS2022 солюшене нет сборки Schematics на PreBuild эвенте.
> 
> Перед сборкой экстеншна  VS2022.VSIX необходимо хотя бы раз запустить сборку VSIX для предыдущих версий.  
> Такая же последовательность и в процессе сборки VSIX на ферме.  
>  

# 3. MVC Инсталяха Ферма

## 3.1 Сборка инсталяхи и ZIP архивов

Таска сборки инсталяхи начинается здесь:

![](https://lh5.googleusercontent.com/GemiP1oeqKNK4mg1F1LtO4SICSbrWYOueez1PnsP3M7gla8kiDfoBYyZ1l6mCDteYgjXz-iDzmIpS0bxEf1u2kM9VwY-fceCUYgUur2CQFj-t4XsUGNNWTBFACqV9xx49PduKzBc)

Некоторые моменты:

1\. В файле ‘Product.DevExtreme.xml’ определены два подпродукта:

```xml
  <SubProductInfos>  
    <SubProductInfo VSSFileLocation="$/CCNetConfig/LocalProjects/DevExtreme/22.1/Build/Product.DevExtreme.HTMLJS.xml" VSSName="dxvcs" />  
    <SubProductInfo VSSFileLocation="$/CCNetConfig/LocalProjects/DevExtreme/22.1/Build/Product.DevExtreme.MVC.xml" VSSName="dxvcs" />  
  </SubProductInfos>    
```  

2\. Добавить контент в инсталяху можно в этом блоке:

<InstallationComponents SetupDataFolder=".\\">  
    <Component Name="DevExtreme">  
      <Sources>

3\. Добавить контент в ZIP архив:

*custom-tasls.js*

// Make ZIPs  
sh.exec(\`7z a ${HG\_ROOT}/InstallationArtifacts/ZipInstallation/DevExpressDevExtreme-Complete-${VERSION}.zip -r ${HG\_ROOT}/InstallationArtifacts/ZipInstallationFiles\_Complete/\*.\*\`);  
sh.exec(\`7z a ${HG\_ROOT}/InstallationArtifacts/ZipInstallation/PackerResult-${VERSION}.zip -r ${HG\_ROOT}/GitHub/artifacts/\*.\* -xr!${HG\_ROOT}/GitHub/artifacts/transpiled\`);  
sh.exec(\`7z a ${HG\_ROOT}/InstallationArtifacts/ZipInstallation/Sources-${VERSION}.zip -r ${HG\_ROOT}/GitHub/js/\*.\*\`);

также в файле “*custom-tasls.js”* выполняется много другого функционала:

Сборка и копирование NuGet пакетов, ASP.NET длл'ок, NPM пакетов, Help Assemblies, раскопирование общих ДЛЛок, выполнение внутренних тулзов …

# 4. Функциональные тесты

Есть функциональные тесты написанные на основе TestComplete тулзах и на APPIUM фреймворке.

1 - TestComplete - отдельная тулза. Изначально его выбрали.

   Недостатки: долгий период вхождения. Сложный процесс тестирования.

2 - APPIUM - XUnit тесты c Silenium фреймворком и специальным “Windows Application Driver’ом”.

   Более удобен для тестирования. И порог вхождения более быстрый.

## 4.1 TestComplete

Каталог <HG>\\Tools\\Design\_FT\\

Для отладки необходимо установить тулзу “\\\\corp\\internal\\inst\\!Licensed Software\\AQA tools\\TestComplete 12\\TestComplete1260.exe”.

Изменять следует JS файлы в каталоге “<HG>\\Tools\\Design\_FT\\project\\Design\_FT\\Design\_FT\\Script\\\*.js”

> Осторожно со вспомогательными файлами. Так как надо учитывать окружение на ферме и на локальной машине разработчика.  
>   
> Косяк. Инсталяха устанавливается через UI интерфейс. Возможны падения в тестах (the element with this XPath is not found) так как у инсталяхи в UI лейауте могут быть изменения в названиях панелей/кнопок.  
> Нужно закоментить эту часть кода. А устанавливать через командную строку в сайлент-моде  
>  

## 4.2 APPIUM

Солюшн “<HG>\\Tools\\Appium\_FT\\AppiumFuncTests.sln”

Требует запущенного приложения “Windows Application Driver”

[_https://github.com/microsoft/WinAppDriver/releases/tag/v1.2.1_](https://github.com/microsoft/WinAppDriver/releases/tag/v1.2.1)  
 

> Косяк. Инсталяха устанавливается через UI интерфейс. Возможны падения в тестах (the element with this XPath is not found) так как у инсталяхи в UI лейауте могут быть изменения в названиях панелей/кнопок.  
>   
> Нужно закоментить эту часть кода. А устанавливать через командную строку в сайлент-моде 

# 5, Ферма

Описания тасок на ферме здесь:

$/CCNetConfig/Server/Config/devextreme-22.1.xml

Список MVC тасок:

```plaintext
DevExtreme MVC Unit tests ($(Version) tip)
DevExtreme MVC.AspNetCore Unit tests ($(Version) tip)
DevExtreme MVC VS Wizards Unit tests ($(Version) tip)
DevExtreme MVC VS Scaffolding Unit tests ($(Version) tip)
DevExtreme Design Functional tests MVC Wrappers($(Version) tip)
DevExtreme MVC Appium tests ($(Version) tip)
Конфиги для этих тасок находятся по такому пути:
$/CCNetConfig/LocalProjects/DevExtreme/21.2/*
```

Основные моменты:

\- за ходом прохождения теста можно следить в консольном окне ( contextMenu -> show console )

\- можно выбрать виртуалку с кастомными параметрами ( CPU, MEM, TIME LIMIT )

## 5.2 Падения и Маргалки

MVC направление уже давно заморожено, нового ничего не разрабатывалось, все баги пофикшены и т.д.

Но падения всё же могут быть и это в первую очередь связано с какими то апдейтами самой студии.

Также они могут быть из-за тормозов самой тестовой виртуалки, либо по таймауту либо падений самой студии.

Далее варианты озеленения тасок:

### 5.2.1 How to resolve DevExtreme Design Functional tests MVC Wrappers(XX.X tip)

За прохождением функ.тестов можно наблюдать через консоль: ( RightButtonClick -> Show Console )

Здесь можно увидеть явные падения студии, наличие/отсутствие установленных экстеншнов, прожект темплейтов.

_Куда смотреть если есть падение на ферме:_

1) Посмотреть на время прохождения тестов (Running time).

    Если больше часа, то тесты завершились по таймауту с красным статусом.

    - На это влияет загруженность фермы, и в частности конкретные виртуалки на которой прогонялась таска ( есть тормозные виртуалки )

    - Либо "TestComplete" подвис на каком-то процессе ( маловероятно, но бывает )

    Следует пререзапустить.

2) Если не по таймауту.

    Идём в статистику по тесту DXCCTray. Вкладка XmlLog. Ближе к концу лога ищем строку, что-то типа:

    */ExportLog:"\\\\corp\\builds\\Release\\Build.v21.1.DevExtreme.Release\\DevExtreme.v21.1\\2021-04-20\_03-01\\Installations\\ft\_results\_TestMVC\_2021-04-20\_10-00.mht"*

    Открываем файл в браузере и видим лог прохождения "TestComplete" тестов.

    Если были падения, то мы их увидим в конце "TestLog" списка. Для примера могут быть следующие ошибки:  
 

_Какие проблемы могут быть:_

1) Проблемы со студией, браузером, ... окружением:

    - Unable to find the object Sys.Browser("iexplore")

    - Unable to find the object devenv.exe

    Здесь следует перезапустить тест.

2) Проблемы с нашей инсталяхой:

    - Unable to find the "DevExpress 20.1 ASP.NET Core ..."

    ...

    Возможно что экстеншны не установлены. -> Следует проверить инсталяху. Прожект темплейты, скафолдеры.

    Возможно изменилось окружение. Новая VS студия. Изменилось расположение. Элементы приложения не находятся. -> Следует установить TestComplete и настроить(подкорректировать) тесты на запуск в новой студии.

Здесь установщик:

 \\\\corp\\internal\\inst\\!Licensed Software\\AQA tools\\TestComplete 12\\TestComplete1260.exe

 Здесь тесты:

 HG\\Tools\\Design\_FT\\...  
 

### 5.2.2 How to resolve DevExtreme MVC Appium tests (XX.X tip)

За прохождением функ.тестов можно наблюдать через консоль: ( RightButtonClick -> Show Console )

Здесь можно увидеть явные падения студии, наличие/отсутствие установленных экстеншнов, прожект темплейтов.

_Куда смотреть если есть падение на ферме:_

1) Посмотреть на время прохождения тестов (Running time).

Если больше часа, то тесты завершились по таймауту с красным статусом.

\- На это влияет загруженность фермы, и в частности конкретные виртуалки на которой прогонялась таска ( есть тормозные виртуалки )

\- Также может быть из-за проблем в скаффолдерах. На каждый тест даётся 3 попытки. Если все тесты будут падать то выйдем за временные рамки.

Следует пререзапустить. Через ShowConsole посмотреть момент ошибки.

2) Если не по таймауту.

Эти функ.тесты на базе QUnit тестов, по этому статус конкретного теста можем увидеть в статистике тестов DXCCTray. Вкладка Tests. Не должно быть красных.

  
_Какие проблемы могут быть:_

1) Проблемы в инсталяхе. Отсутствие (не правильная работа) экстеншнов, скаффолдеров.

    Поставить инсталяху. Либо остановить тестовую виртуалку. Потестить в студии руками.

2) Проблемы со студией. Изменилось окружение.

    Возможно новая студия, изменилось расположение элементов, нужно под неё настраивать.

    Здесь тесты:

    HG\\Tools\\Appium\_FT\\...

    Запускаются из студии.

    Для работы необходим запущенный "Windows Application Driver"

    https://github.com/microsoft/WinAppDriver/releases/tag/v1.2-RC

# 6, Известные сценарии ( Known Issues )

Популярные траблы

## 6.1 Нет прожект темплейтов в “New Project Dialog” окне

Открыть менеджер экстеншнов и проверить что установлен DevExtreme экстеншн и не является задизабленным. В противном случае раздизаблить/переустановить.

![](https://lh6.googleusercontent.com/Vb8xIAhnsodAHFsIspbRDw7ApOEmHOyXVx45_GAmD2I61JXBqlhMA-UrLOwjfUfimQwaZ6rKavFudDQZOd42za5dUYN5qAP7h210zvbaS-IARKNbHi3L7D7DDp-MB_jjzmwU-DlL)

## 6.2 Нет в контекстном меню элемента “Add/Upgrade DevExtreme Resource to the Project”

1\. Тоже что и в предыдущем пункте.

2\. Также проверить что тестируемый проект является поддерживаемым: ASP.NET MVC/Core

Core-ские проекты созданные как Blazor не поддерживается.

<Project Sdk="Microsoft.NET.Sdk.Blazor">

3\. Для Core проектов, если кастомер обновил DevExtreme.AspNet.Mvc через NuGet Manager, то CSS/JS не обновятся, так как такие функции доступны только если есть разница в версиях DLL’ок проекта и в директории с инсталяцией.

## 6.3 При попытке сгенерить проект появляется эксепшн "One or more required DevExtreme files were not found"

Такое сообщение может быть только в случае когда js/css сорцы не были найдены.

Необходимо глянуть в реестре куда устанавливалась инсталяха.

![](https://lh6.googleusercontent.com/p5hCBQJO3KlWijJ5x5425uFoYwIArijtcQW71IWFJKKmVmYTf1XlZWLwpqQLkkStwdD3QW6oZ77_LpiXwkMZclP_WlZk1mha3kPoBS_B-QOjmOjEbg7iH4yF_1ycOF4W4AlkjsNX)

  
И проверить физически на диске, есть ли требуемые файлы там.

## 6.4 Как сбилдить проект

Сбилдить можно в том числе с использованием MSBuild через коммандную строку:
```cs
D:\HG\DevExtreme.AspNet.Mvc>"C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\MSBuild\Current\Bin\MSBuild.exe" DevExtreme.AspNet.Mvc.VisualStudio.sln -t:restore,build -p:RestorePackagesConfig=true
```

# 7, Как проверить/фиксить проблему пользователя 

Если кастомер пришёл, и никакие советы не помогают. То первым делом попробовать воспроизвести его проблему на нашей стороне:

1.  поставить инсталяху указанной версии в указанной пользователем студии
2.  запустить его проект или попробовать пройти по его шагам

Как отладить багу:

1.  Открываем солюшн  DevExtreme.AspNet.Mvc.VisualStudio.sln

или

DevExtreme.AspNet.Mvc.VisualStudio.VS2022.sln

в зависимости тикета

1.  Компилим всё
2.  Идём в каталог

DevExtreme.AspNet.Mvc.VisualStudio\\bin\\Debug

или

DevExtreme.AspNet.Mvc.VisualStudio.VS17\\bin\\Debug

1.  Ищем файл с расширением .VSIX
2.  Меняем ему расширение на ZIP
3.  Контент копируем в каталог с экстеншнами требуемой студии

например для VS 2019 путь будет такой:

“C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Professional\\Common7\\IDE\\Extensions\\DevExtreme\_22.1”

1.  Далее файл “extensions.configurationchanged” апдейтим - открыть  внотепаде, добавить пробел, сохранить и закрыть
2.  Открыть кастомный проект в требуемой студии
3.  Проект с исходниками ( не билдим, иначе отладка будет невозможно ), выбираем команду “Debug -> Attach to process”, выбираем студию с кастомным проекто
4.  Подождали чтоб всё прогрузилось. И в кастомном проекте делаем описанные кастомером действия. В студии с исходниками будет отображена отладочная информация в случае косяков ( Некоторые куски кода находятся в конструкции try { } catch { } - это нормально, не надо ничего менять :-) )

# 8 Ссылки

1.  [_https://docs.devexpress.com/DevExtremeAspNetMvc/400943/devextreme-aspnet-mvc-controls_](https://docs.devexpress.com/DevExtremeAspNetMvc/400943/devextreme-aspnet-mvc-controls)
2.  [_https://docs.devexpress.com/AspNetCore/400263/aspnet-core-controls_](https://docs.devexpress.com/AspNetCore/400263/aspnet-core-controls)