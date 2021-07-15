HackerNewsPwaTest

ng new ng-pwa-demo

npm start

app.module.ts
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, HttpClientModule],
  providers: [],
  bootstrap: [AppComponent]
})

ng g service api

import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

export interface Item {
  title: string;
  url: string;
}


@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private dataURL: string = 'https://api.hnpwa.com/v0/news/1.json';

  constructor(private httpClient: HttpClient) {}

  getData(): Observable<Item[]> {
    return <Observable<Item[]>this.httpClient.get(this.dataURL);
  }
}

//https://houssein.me/angular2-hacker-news
//https://medium.com/crowdbotics/learn-to-build-a-simple-progressive-web-app-pwa-with-angular-and-lighthouse-hacker-news-clone-51aca763032f
```
app.component.ts
```ts




import { Component, OnInit } from '@angular/core';
import { ApiService } from './api.service';
import { Item } from './api.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  title = 'ng-pwa-demo';
  items: Array<Item>;

  constructor(private apiService: ApiService) {}

  ngOnInit() {
    this.fetchData();
  }

  fetchData() {
    this.apiService.getData().subscribe(
      (data: Array<Item>) => {
        console.log(data);
        this.items = data;
      },
      err => {
        console.log(err);
      }
    );
  }
}
```


app.component.html


```html
<div style="text-align:center" class="header">
  <h1>
    Welcome to HN PWA Demo
  </h1>

</div>
<h2 class="subtext">Here are some links to Start Your Day:</h2>
<ul *ngFor="let item of items" class="title">
  <li>
    <h2><a href={{item.url}}>{{item.title}}</a></h2>
  </li>
</ul>
```

app.component.css


```css
.subtext {
  font-family: 'Lucida Grande', 'Segoe UI', Arial, Helvetica, sans-serif;
  font-size: 11px;
  height: 20px;
  vertical-align: top;
}

.title {
  color: #ccc;
  font-family: 'Lucida Grande', 'Segoe UI', Arial, Helvetica, sans-serif;
  font-size: 16px;
}

a {
  text-decoration: none;
  color: #000000;
}

a:hover {
  text-decoration: underline;
}

body {
  margin: 0;
}

.header {
  background-image: -webkit-linear-gradient(top, #f60, #f70);
  border-bottom: solid 1px #f60;
  box-shadow: 0 2px rgba(0, 0, 0, 0.1);
  align: center;
  padding: 5px;
  font-family: 'Lucida Grande', 'Segoe UI', Arial, Helvetica, sans-serif;
}

body
  > center
  > table
  > tbody
  > tr:first-child
  > td
  > table
  > tbody
  > tr
  > td:first-child {
  padding-right: 10px;
}

body
  > center
  > table
  > tbody
  > tr:nth-child(3)
  > td
  > table
  > tbody
  > tr:first-child
  > td:nth-child(2).title
  > a {
  font-size: 18px;
}

ul {
  font-family: 'Lucida Grande', 'Segoe UI', Arial, Helvetica, sans-serif;
  font-size: 15px;
}

li a {
  text-decoration: none;
  color: #4d4d4d;
}
```


ng build --prod

go to dir --> dist/ng-pwa-demo/

npm install -g serve

serve

ng add @angular/pwa

ng build --prod
