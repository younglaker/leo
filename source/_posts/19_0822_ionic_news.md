---
layout: post
title: Angular Ionic News App Tutorial for Beginner
date: 2019-08-22 08:24:00
category: [Angular]
tags: [Angular, Ionic]
---

Github repo: [https://github.com/younglaker/CometLab/tree/ionic-news](https://github.com/younglaker/CometLab/tree/ionic-news)

## Command

Start serve

```
ionic serve
```

<!--more-->

## tabs

generate command：

```
ionic g [type: page/component/tabs/provider/service/provider]  [names]
```

generate page：

```
ionic g page  [names]
```

For example, after generating a `news` page, in `src/app/tabs/tabs.module.ts`, add:

```
import { NewsPageModule } from '../news/news.module';
// [page name] +PageModule

@NgModule({
  imports: [
    ...
    NewsPageModule
  ],
```

In `src/app/tabs/tabs.page.html`, add:

```
    <ion-tab-button tab="news">
      <ion-icon name="flash"></ion-icon>
      <ion-label>Tab One</ion-label>
    </ion-tab-button>
```

In `src/app/tabs/tabs.router.module.ts`, add:

```
const routes: Routes = [
  {
    ...
    children: [
      {
        path: "news",
        children: [
          {
            path: "",
            loadChildren: "../news/news.module#NewsPageModule"
          }
        ]
      }
```

## Get news list

### API

[https://newsapi.org/](https://newsapi.org/)

`https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=`

Set environment arguments. In `src/environments/environment.ts`:

```
export const environment = {
  ...
  apiUrl: "https://newsapi.org/v2/",
  apiKey: "c***********"
```

Create service:

```
$ ionic g service news
```

In `/src/app/app.module.ts`

```
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  ...
  imports: [
    ...
    HttpClientModule
```

In `src/app/news.service.ts`

```
import { HttpClient } from '@angular/common/http';

const API_URL = environment.apiUrl;
const API_KET = environment.apiKey;


export class NewsService {
  constructor(private http: HttpClient) {}

  getData(url) {
    return this.http.get(`${API_URL}/${url}?apiKey=?{ API_KEY }`);
  }
}
```

In `src/app/news/news.page.ts`

```
import { NewsService } from '../news.service';

export class NewsPage implements OnInit {
  constructor(private newsService: NewsService) {}

  ngOnInit() {
     // NewsService from news.service.ts
    this.newsService
      .getData('top-headlines?country=us&category=business')
      .subscribe(data => {
        console.log(data);
      });
  }
}
```

![data](https://github.com/aomine-sama/px/blob/master/2019/19082201.png?raw=true)

### Display news

In `src/app/news/news.page.ts` add

```

import { NewsService } from '../news.service';

export class NewsPage implements OnInit {
  // res: store the data from API, type is any
  res: any;

  ngOnInit() {
    this.newsService
      .getData('top-headlines?country=us&category=business')
      .subscribe(data => {
        // console.log(data);
        this.res = data;
      });
  }
}
```

In `src/app/news/news.page.html`

```
  <!-- Here is a '?',  rendering after getting data-->
  <ion-card *ngFor="let article of res?.articles">
    <ion-card-header>
      <ion-card-subtitle>Card Subtitle</ion-card-subtitle>
      <ion-card-title> {{ article.title }} </ion-card-title>
    </ion-card-header>
    <ion-img [src]="article.urlToImage"></ion-img>
    <ion-card-content>{{ article.description }} </ion-card-content>
  </ion-card>
```

![news lists](https://github.com/aomine-sama/px/blob/master/2019/19082202.png?raw=true)

## Link to details

`src/app/news/news.page.html`, bind click event

```
<ion-card
    *ngFor="let article of res?.articles"
    (click)="goToNewsSingle(article)"
  >
```

`src/app/app-routing.module.ts`, it generate routes path when generate the news-single page, we can use it directly:

```
const routes: Routes = [
  ...
  { path: 'news-single', loadChildren: './news-single/news-single.module#NewsSinglePageModule' }
];
```

`src/app/news/news.page.ts`, define goToNewsSingle() event

```
export class NewsPage implements OnInit {
  ...
  constructor(..., private router: Router) {}

  goToNewsSingle(article) {
    this.newsService.currentArticle = article;
    this.router.navigate(['/news-single']);
  }
```

`src/app/news-single/news-single.page.ts`

```
..
import { NewsService } from '../news.service';

export class NewsSinglePage implements OnInit {
  article; //store the content of current article

  constructor(private newsService: NewsService) {}

  ngOnInit() {
    this.article = this.newsService.currentArticle;
  }
}
```

`src/app/news-single/news-single.page.html` display the content of current article:

```
  <ion-card>
    <ion-card-header>
      <ion-card-subtitle>Card Subtitle</ion-card-subtitle>
      <ion-card-title> {{ article.title }} </ion-card-title>
    </ion-card-header>
    <ion-img [src]="article.urlToImage"></ion-img>
    <ion-card-content>{{ article.description }} </ion-card-content>
  </ion-card>
```

![news detail](https://github.com/aomine-sama/px/blob/master/2019/19082203.png?raw=true)

## Back button

```
<ion-buttons slot="start">
      <ion-back-button text="...." icon="....">
</ion-buttons>
```

> Exchange blogroll： [http://laker.me/blog](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
