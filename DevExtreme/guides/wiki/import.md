---
title: Импорт данных
description: 
published: true
date: 2022-04-22T06:22:28.969Z
tags: 
editor: markdown
dateCreated: 2022-04-19T11:09:53.271Z
---

Самописная тулза для импорта страничек из гитхаба.

В приложенном архиве ([/wikiimporter.zip](/wikiimporter.zip)) содержится файл проекта на C# и сбилженное приложение (в директории .\\bin\\debug)

Для запуска просто запустить экзешник:

-   WikiImporter\\WikiImporter\\bin\\Debug\\net6.0\\WikiImporter.exe  
     

Технически работает через запросы [graphql](https://docs.requarks.io/dev/api) к вики.

## Настройки

В архиве с приложением находится файлик settings.json, в котором прописаны все настройки приложения.  
 

```javascript
{
	"RepoUrl":"https://github.com/DevExpress/devextreme-internal-docs",
	"GithubPersonalToken":"PASTE IT HERE",
	"GithubFromFolder":"docs",
	"GraphQlUrl":"http://3.139.39.183/graphql",
	"Locale": "en",
	"WikiAccessToken":"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcGkiOjIsImdycCI6MSwiaWF0IjoxNjQ5ODQ5NDYzLCJleHAiOjE2ODE0MDcwNjMsImF1ZCI6InVybjp3aWtpLmpzIiwiaXNzIjoidXJuOndpa2kuanMifQ.bFqOyW-mJYfb7fIgh93vuPDAxYFkr7v63AvPxQKlD_PdLvn7LTXbVbQCE6hwNE3eg7tjynDtFqfi_PukkS0UTKv3CorsOxp207TH1YbNoEocD-myV2Awv8eHHQ8PQQnFQ-_8WE3v8YnDHvTLDhljdoM8tPj3PI6H9MYFAKJvMWTtb7wYeeXwK5BT-wrpkw5T5CkKD86PhBxaflSX-YnqDibRyZ5XaYzBCJNxkC6B9VcdbUa-iCR534kJhLZyVVLQpjiX6YrHSzUcf8qpaUnxyJhTGSuuaXTbJYRIYfRuRyTklsiGHRLBsFjZw9Svjf3OfCnbEZUgw47ixrLfC4ZOtg",
	"WikiFolder":"DevExtreme/internal-docs"
}
```

  
где:

-   repoUrl - путь к гитхаб репозиторию.
-   GithubPersonalToken - персональный токен гитхаба для доступа к приватным репозиториям (получить можно [так](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)).
-   GithubFromFolder - с какой директории начинать импортировать странички. Например для `devextreme-internal-docs`  есть внутренняя директория [docs](https://github.com/DevExpress/devextreme-internal-docs/tree/master/docs), в которой содержится вся документация.
-   GraphQlUrl - путь к апи вики (на случай переезда)
-   WikiAccessToken - токен для авторизации и использования апи. Генерится в админке
-   WikiFolder - в какой директории создавать странички.