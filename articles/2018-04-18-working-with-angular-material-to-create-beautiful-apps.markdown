---
layout: post
title: "Working With Angular Material to Create Beautiful Apps"
description: "Angular Material provides you with prebuilt components that allows you to build beautiful user interface for your applications"
date: "2018-04-18 08:30"
author:
  name: "Oliver Mensah"
  url: "Oliver_Mensah"
  mail: "olivermensah96@gmail.com"
  avatar: "https://twitter.com/Oliver_Mensah/profile_image?size=original"
related:
- 2017-11-15-an-example-of-all-possible-elements
---

# Working With Angular Material to Create Beautiful Apps.

Angular is an amazing frontend framework with which you can build powerful web applications. 
In this article, we will explore Angular Material and use it to build an entire, fast, realistic app 
which looks absolutely beautiful. 
By then end of the article, you will have a brief refresher on Angular, detailed introduction into Angular Material, 
its docs and its usage as well as building a realistic app that uses many Angular Material components. 
What are you waiting for? Let's get started.

## So Exactly is Angular Material?

A is a third party package used in Angular project. 
At its core is an Angular Component Suite which is made pre-built styled angular components.
With angular the entire app is composition of components and instead of building and styling components from group up, 
you can leverage with Angular Material which provide out of the box styled components 
that follow the Material Design Spec. 
This is the Spec used by Google in the android operating system and also very popular on web due to it beautiful UI utilities.

## Get Setup.

Lets start building a prototype app with Angular and Angular Material. We need to make sure we have the following in place.

### Setting up our project environment.

For that we need `Node.js` and `Angular CLI` installed. `Node.js` will help to provide the packages needed by the `CLI` to work. 
For example the development server package.  
`Angular Command Line Interface (CLI)` is a tool that create  a new angular project for us. We need it because angular project is more than `js html and script` files.
Angular project uses `TypeScript` which needs to be optimized and run on some server, so we need a setup with more complex build workflow 
that uses third party packages for optimisation and build stuff, the `CLI` just give us the workflow out of the box. 

After installing nodejs, you can now install the cli with `npm install -g @angular/cli `.  
Depending on the setup of your commputer, you might need to install as an admin, unix users should start with `sudo`. 

### Create a project.

Once installation is finish, lets create angular project with `ng new  name_of_poject`.  Open the project with your favourite IDE or editor.  
The folder structure has a lot of files. But where will be working with a lot is the src folder. 

### Install Angular Material and Angular CDK.

Navigate to the root of the project in your terminal or command line with `cd name_of_poject` and run 
`npm install --save @angular/material @angular/cdk` commad. 

### Install Animations Module.

Next step is to install the angular animation package which is used by the some Material components to do more advanced transitions. 
**NB** : Before installing this package, check in `package.json` file. Sometimes, install angular material adds this package by default. 
If not then go ahead to install that with ` npm install --save @angular/animations`
In order to use the animation after installing it, we need to explicitly add it to our project. 
In angular we have to explicitly add what you what you want to use so your code can be optimize. Having said that , let’s add to our ` app.module.ts `file
the code below;
```js
import {BrowserAnimationsModule} from '@angular/platform-browser/animations' 
```
And we simply need to add the BrowserAnimationsModule to our imports property of `@NgModule`. 
This is what your appModule needs to look like at the end. 
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';
import { AppComponent } from './app.component';
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }  
```
Now, we are good to go; to make use of the angular material module we need in our project. 
I personally like to create a file where I import all the angular material components I will need in my project. 
So let's do that by creating `src/app/material.module.ts` file and add the following to it;
```ts
import {NgModule} from '@angular/core'
@NgModule({
	imports: [],
  exports: []
})
export class MaterialModule {}
```
`@NgModule` will turn this file into angular module. It has `imports` property to import all the modules needed from `Angular Material` and 
also `exports` property as well to outsource these modules.
We can now import this created module in the root definition file(` app.module.ts `) as;
```ts
import {MaterialModule} from './material.module.ts';
```
This helps to access to all those material components anywhere in our project. 
  
### Angular Material Theme.

We have to include a theme. Angular material use a theme which by default is just a color combination of 
* accent - pink
* warn - red
* background - grey
* primary - indigo
Just copy and paste into the style.css file the following content.
```css
@import "~@angular/material/prebuilt-themes/indigo-pink.css";
```
### Angular Material Gesture for Some components.

Some components (mat-slide-toggle, mat-slider, matTooltip) rely on HammerJS for gestures.  
So we need to install HammerJS  and load it into our application.  
From the command line/terminal in the root of your project, run `npm install --save hammerjs`. After installing,   
add to the project's entry point (`src/main.ts`) as
```js
import 'hammerjs'; 
``` 
### Making use of Material Icons.

With the angular material, we can also make use of the awesome icons that comes with it. 
To add that to angular project, just include the following in the in the `src/index.html` file. 
 ```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```
## What App  Will We Build With Angular Material?

We will be focusing on building a sample application that makes us of the default theme that comes with Angular Material.
We will build an an that serves like a content management system for blog posts. It will not use permanent data storage so will
make use of JavaScript arrays. 

Enough of the talking, let's get started!!!

### Creating Navigation bar of Our App.

We will make use of Angular Material Components to create our navigation bar. When you visit the [website]("https://material.angular.io"), you can have a look at the 
available components that we can make use of. For our navigation we will use `mat-sidenav` module. 
To make Angular Material components available in our application, we need to import that module.

#### Importing Material Components.

We will create a `material.module.ts` in the `src/app folder` where we will import all the modules from `Angular Material` we are going to make use of in our application.
Import the `MatSidenavModule` into created file.  The content of of `material.module.ts` must be like:
```ts 
import {NgModule} from '@angular/core'
import {
    MatSidenavModule,
} from '@angular/material';

@NgModule({
	imports: [
    MatSidenavModule,
   ],
  exports: [
    MatSidenavModule,
  ]
})
export class MaterialModule {}
```
Afterwards, we to make this module created available in our project, so we will import this file into `AppModule`
which is like a root definition file that defines all the pieces our angular app is made up off.
You can import the MaterialModule we created as
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

import { AppComponent } from './app.component';
import { MaterialModule } from './material.module';

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    MaterialModule,
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
We can now work with this imported module in our app. Let's work with that in our AppComponent where will be creating our Navigation bar.
### Working with Angular Material Components
```html
<mat-sidenav-container>
  <mat-sidenav  #sidenav role="navigation">
   <mat-nav-list>
    <a mat-list-item>
      <mat-icon class="icon">input</mat-icon>
      <span class="label">Login</span>
    </a>
    <a mat-list-item>
      <mat-icon class="icon">home</mat-icon>  
        <span class="label">Home</span>
    </a>
    <a mat-list-item>
      <mat-icon class="icon">dashboard</mat-icon>  
      <span class="label">Dashboard</span>
    </a>
    <a  mat-list-item type="button">
      <mat-icon class="icon">input</mat-icon>
      <span class="label">LogOut</span>
    </a>  
    </mat-nav-list>
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
     <div fxHide.gt-xs>
       <button mat-icon-button>
        <mat-icon>menu</mat-icon>
      </button>
    </div>
     <div>
       <a>
          Material Blog
       </a>
       
     </div>
     <div fxFlex fxLayout fxLayoutAlign="flex-end"  fxHide.xs>
        <ul fxLayout fxLayoutGap="20px" class="navigation-items">
            <li>
                <a>
                  <mat-icon class="icon">input</mat-icon>
                  <span  class="label">Login</span>
                 </a>
            </li>
            <li>
              <a >
                  <mat-icon class="icon">home</mat-icon>
                  <span class="label">Home</span>
              </a>
            </li>
            <li>
                <a>
                    <mat-icon class="icon">dashboard</mat-icon>
                    <span class="label">Dashboard</span>
                </a>
              </li>
            <li>
                <a
                >
                  <mat-icon class="icon">input</mat-icon>
                  <span class="label">LogOut</span>
                 </a>
            </li>
        </ul>
     </div>
    </mat-toolbar>
    <main>
    </main>
  </mat-sidenav-content>
</mat-sidenav-container>
```
While creating the navigation you, we are making use of other modules like `mat-icon`, `mat-toolbar`, `mat-list` and some directives 
like `fxLayout`. All the modules from `Angular Material` are prefixed with `mat` and you need to import them as we did earlier in our `material.module.ts` file.

### Controlling Layout of Angular Material Applications.

Grid system is not part of the Angular Material, we can use Flex Layout package to control that. This is where the directive `fxLayout` we made mentioned off
comes from.
It uses css flexbox. It positions these html elements nicely by passing the flexbox components as directives. 
Install it with `npm install @angular/flex-layout` and import into `src/app.module.ts` 
as `import {FlexLayoutModule} from '@angular/flex-layout';`  and as  we always do, add the imported module to the imports array in `@NgModule`. 
In our navigation bar we made use of some directives like alligning some elements to the its right end as well as hiding those element on 
smaller screen size. You can explore more on the package later.

But still the navigation is still not look nice, let's add the following stylesheets to your `app.component.css` file;
```css
mat-sidenav-container, mat-sidenav-content, mat-sidenav {
   height: 100%;
}
mat-sidenav {
  width: 250px;
}
a {
  text-decoration: none;
  color: white;
}
a:hover,
a:active {
  color: lightgray;
}
.navigation-items {
  list-style: none;
  padding: 0;
  margin: 0;
  cursor: pointer;
}
.icon{
  display: inline-block;
  height: 30px;
  margin: 0 auto;
  padding-right: 5px;
  text-align: center;
  vertical-align: middle;
  width: 15%;
}
.label{
  display: inline-block;
  line-height: 30px;
  margin: 0;
  width: 85%; 
}
```
### Adding More Components.

We just have one component that only renders the navigation. We can add extra components to this application by using the `CLI`
We will create the following components:
* Welcome - provides little details about the app
* dashboard - displays table of blog posts
* post-dialog - Modal to add new post
You can create these with the command `ng g c name_of_component`. Since we have two modules in the src folder, the command will not be 
able to identify which module it should import these created components.We can solve this by add `--module app.module` flag to our command.
Open  the html file of the `welcome component` and add the following content:
```html
<div style="text-align:center">
  <h1>Angular Content Management System</h1>
  <p>
    This is a platform for technical writers to manage their blog post contents related to angular.
    <br> Click on Login to get Start
  </p>
</div>
```

### Creating Routes for our App.

Now we have multiple components but we cannot access them in the browser. To do so, we need to create pages for our app using Routes.
To do so create  TypeScript file named `src/app/app.routes`  and add the following content to that file;
```ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { WelcomeComponent } from './welcome/welcome.component'
import {DashboardComponent} from './dashboard/dashboard.component'
const routes: Routes = [
  {path: '', component: WelcomeComponent },
  {path: "dashboard", component: DashboardComponent}
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRouters {}
```
Creating routes is basically about making use of angular router which will help you to create 
urls that corresponds to  specific components. This file will help create two routes for our app
which will be `http://localhost:4200 and http://localhost:4200/dashboard` 
We can now add links to our navigation bar items and also add `router-outlet` to let us navigate between pages. For example, the dashboard item can be linked to `dashboard` route.
Modify the `app.component.html` file to 
```html
  <mat-sidenav-container>
  <mat-sidenav  #sidenav role="navigation">
   <mat-nav-list>
    <a mat-list-item>
      <mat-icon class="icon">input</mat-icon>
      <span class="label">Login</span>
    </a>
    <a mat-list-item
        routerLink="/">
      <mat-icon class="icon">home</mat-icon>  
        <span class="label">Home</span>
    </a>
    <a mat-list-item
      routerLink="/dashboard">
      <mat-icon class="icon">dashboard</mat-icon>  
      <span class="label">Dashboard</span>
    </a>
    <a  mat-list-item 
        type="button">
      <mat-icon class="icon">input</mat-icon>
      <span class="label">LogOut</span>
    </a>  
    </mat-nav-list>
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
     <div fxHide.gt-xs>
       <button mat-icon-button (click)="sidenav.toggle()">
        <mat-icon>menu</mat-icon>
      </button>
    </div>
     <div>
       <a routerLink="/">
          Material Blog
       </a>
       
     </div>
     <div fxFlex fxLayout fxLayoutAlign="flex-end"  fxHide.xs>
        <ul fxLayout fxLayoutGap="20px" class="navigation-items">
            <li>
                <a>
                  <mat-icon class="icon">input</mat-icon>
                  <span  class="label">Login</span>
                 </a>
            </li>
            <li>
              <a
                routerLink="/"
              >
                  <mat-icon class="icon">home</mat-icon>
                  <span class="label">Home</span>
              </a>
            </li>
            <li>
                <a
                  routerLink="/dashboard"
                >
                    <mat-icon class="icon">dashboard</mat-icon>
                    <span class="label">Dashboard</span>
                </a>
              </li>
            <li>
                <a
                      >
                  <mat-icon class="icon">input</mat-icon>
                  <span class="label">LogOut</span>
                 </a>
            </li>
        </ul>
     </div>
    </mat-toolbar>
    <main>
      <router-outlet></router-outlet>
    </main>
  </mat-sidenav-content>
</mat-sidenav-container>
```
## Associating Data with the App -- Part 1.

Now when you visit the dashboard, we are not seeing what we said earlier about the dashboard.
So let's work on the dashboard now. Let's have a look at the kind of data we want to store in our app data store. Since it is about blog post we 
can define an `interface ` of a blog post as; 
```ts
export interface Post {
  title: string;
  category: string;
  date_posted: Date;
  position: number,
  body: string
}
```
Create a file as `srs/app/models/Post.ts` and add the interface code to it.  We can now use this blog post interface to build a data service that will help 
perform certain operations on our blog post data. To do so, we can make use of the `CLI`. Run `ng g s data --module app.module` command. Once the file is created, 
add to the `data.service.ts` file the code below;
```ts 
import { Injectable } from '@angular/core';
import { Post } from '../models/Post';
import { Observable }   from 'rxjs/Observable';
import 'rxjs/add/observable/of';
@Injectable()
export class DataService {

  ELEMENT_DATA: Post[] = [
    { position: 0, title: "Post One", category: "Web Development", date_posted: new Date() ,body: "Body 1"},
    { position: 1, title: "Post Two", category: "Android Development", date_posted: new Date() ,body: "Body 2"},
    { position: 2, title: "Post Three", category: "IOS Development", date_posted: new Date() ,body: "Body 3" },
    { position: 3, title: "Post Four", category: "Android Development", date_posted: new Date() ,body: "Body 4"},
    { position: 4, title: "Post Five", category: "IOS Development", date_posted: new Date() ,body: "Body 5"},
    { position: 5, title: "Post Six", category: "Web Development", date_posted: new Date() ,body: "Body 6"},
  ];
  categories = [
    { value: 'Web-Development', viewValue: 'Web Development' },
    { value: 'Android-Development', viewValue: 'Android Development' },
    { value: 'IOS-Development', viewValue: 'IOS Development' }
  ];
  constructor() { }

  getData(): Observable<Post[]> {
    return  Observable.of<Post[]>(this.ELEMENT_DATA);
  }

  getCategories() {
    return this.categories;
  }

  addPost(data){
    this.ELEMENT_DATA.push(data);
    
  }
  deletePost(index){
    this.ELEMENT_DATA = [...this.ELEMENT_DATA.slice(0, index), ...this.ELEMENT_DATA.slice(index +1)]
  }
  dataLength(){
    return this.ELEMENT_DATA.length;
  }
}
```
We can now create our dashboard to make use of the data service to render the data to our databoard page. 
In the `dashboard.component.ts` file, add the the following code;
```ts
import { Component, EventEmitter } from '@angular/core';
import { DataService } from '../data/data.service';
import { Post } from '../models/Post';
import { DataSource } from '@angular/cdk/table';
import {Observable} from 'rxjs/Observable';
@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.css']
})
export class DashboardComponent {
  constructor(private dataService: DataService) {
  }
  displayedColumns = ['date_posted', 'title', 'category', 'delete'];
  dataSource = new PostDataSource(this.dataService);
  deletePost(id){
    this.dataService.deletePost(id)
    this.dataSource = new PostDataSource(this.dataService);
  }
}
export class PostDataSource extends DataSource<any>{
  constructor(private dataService: DataService){
    super();
  }
  connect(): Observable<Post[]>{
    return this.dataService.getData();
  }
  disconnect(){}
}
```
In the `dashboard.component.html` replace everything with the following content;
```html
<div>
    <br>
      <div class="container">
          <div class="container">
            <div  fxLayout="column" fxLayout="column" fxLayoutGap="20px" fxLayout.gt-md="row"  fxLayoutAlign="space-around center" class="content">
                <div class="blocks" >
                    <button button="submit" mat-raised-button color="primary">
                        <mat-icon>add</mat-icon> Add Post
                    </button>
                </div>
          </div>
      </div>
      <br>
      <div class="container">
        <div fxLayout="row" fxLayoutAlign="center center" class="content">
          <mat-card class="card" >
            <mat-card-title fxLayout.gt-xs="row" fxLayout.xs="column">
             <h3>Recent Posts</h3>
            </mat-card-title>
            <mat-card-content>
                <div class="example-container mat-elevation-z8">
                    <mat-table #table [dataSource]="dataSource">
                  
                    <ng-container matColumnDef="date_posted">
                      <mat-header-cell *matHeaderCellDef> Date Posted </mat-header-cell>
                      <mat-cell *matCellDef="let element"> {{element.date_posted  | date: 'd/M/y'}} </mat-cell>
                    </ng-container>

                      <ng-container matColumnDef="title">
                        <mat-header-cell *matHeaderCellDef> Title </mat-header-cell>
                        <mat-cell *matCellDef="let element"> {{element.title}} </mat-cell>
                      </ng-container>

                      <ng-container matColumnDef="category">
                        <mat-header-cell *matHeaderCellDef> Category </mat-header-cell>
                        <mat-cell *matCellDef="let element"> {{element.category}} </mat-cell>
                      </ng-container>
                      
                      <ng-container matColumnDef="delete">
                        <mat-header-cell *matHeaderCellDef></mat-header-cell>
                        <mat-cell *matCellDef="let element">
                          <a
                             type="button">
                            <mat-icon class="icon">delete</mat-icon>
                          </a> 
                        </mat-cell>
                      </ng-container>     
                                   
                      <mat-header-row *matHeaderRowDef="displayedColumns"></mat-header-row>
                      <mat-row *matRowDef="let row; columns: displayedColumns;"></mat-row>
                    </mat-table>
                  </div> 
            </mat-card-content>
          </mat-card>
        </div>
      </div>
   </div>
   </div>
```
### Adding Data to our App.

We are almost there to have a complete working application. In our data service, we added the functionality to add and delete data but we have not done that 
yet. In order to add data, we will utilize material components to create a form. We also don't want to just know who added a blog post to our application so 
we will have to secure the app in a certain we. Let's make use of Auth0 authentication service. 

## Securing App  with Auth0.

Using Auth0 authentication service is easy, you just have to create an account at [Auth0.com](https://auth0.com). Once you have an account, we following the following procedure to 
provide authentication to our application;
* Create  a new application by clickin on `New Application` button in your dashboard page.
* Give a name to your App and select `Single Page Web Applications`. Then click on create. This will create a new application for you. 
* You will be asked to choose What technology are you using for your web app? Select `Angular2+`. Great we can now follow the instructions on the page 
to authenticate our app by 
 * installing the `auth0.js` library with `npm install --save auth0-js`
 * Under the settings section of the page, add `http://localhost:4200/callback` as the Allowed Callback URLs.
 * We will create an authentication service with `ng g s auth --module app.module` command. 
 * Once the auth.service file is created, add the following content to the file;
 ```ts
import { Injectable } from '@angular/core';
import { Router } from '@angular/router';
import { filter } from 'rxjs/operators';
import * as auth0 from 'auth0-js';

@Injectable()
export class AuthService {

  auth0 = new auth0.WebAuth({
    clientID: 'REPLACE WITH WHAT YOU HAVE IN YOUR APP DASHBOARD ',
    domain: 'REPLACE WITH WHAT YOU HAVE IN YOUR APP DASHBOARD',
    responseType: 'REPLACE WITH WHAT YOU HAVE IN YOUR APP DASHBOARD',
    audience: 'REPLACE WITH WHAT YOU HAVE IN YOUR APP DASHBOARD',
    redirectUri: 'http://localhost:4200/callback',
    scope: 'openid'
  });

  constructor(public router: Router) { }

  public login(): void {
    this.auth0.authorize();
  }

  public handleAuthentication(): void {
    this.auth0.parseHash((err, authResult) => {
      if (authResult && authResult.accessToken && authResult.idToken) {
        window.location.hash = '';
        this.setSession(authResult);
        this.router.navigate(['/dashboard']);
      } else if (err) {
        this.router.navigate(['/']);
        console.log(err);
      }
    });
  }

  private setSession(authResult): void {
    // Set the time that the Access Token will expire at
    const expiresAt = JSON.stringify((authResult.expiresIn * 1000) + new Date().getTime());
    localStorage.setItem('access_token', authResult.accessToken);
    localStorage.setItem('id_token', authResult.idToken);
    localStorage.setItem('expires_at', expiresAt);
  }

  public logout(): void {
    // Remove tokens and expiry time from localStorage
    localStorage.removeItem('access_token');
    localStorage.removeItem('id_token');
    localStorage.removeItem('expires_at');
    // Go back to the home route
    this.router.navigate(['/']);
  }

  public isAuthenticated(): boolean {
    // Check whether the current time is past the
    // Access Token's expiry time
    const expiresAt = JSON.parse(localStorage.getItem('expires_at'));
    return new Date().getTime() < expiresAt;
  }
}
```
We can now make use of the this auth.service in our app. We can now allow users to sign up and login in with this service. Let's modify our navigation to 
```html
<mat-sidenav-container>
  <mat-sidenav  #sidenav role="navigation">
   <mat-nav-list>
    <a mat-list-item 
        *ngIf="!auth.isAuthenticated()"
        (click)="auth.login()">
      <mat-icon class="icon">input</mat-icon>
      <span class="label">Login</span>
    </a>
    <a mat-list-item
        *ngIf="auth.isAuthenticated()"
        routerLink="/">
      <mat-icon class="icon">home</mat-icon>  
        <span class="label">Home</span>
    </a>
    <a mat-list-item
      routerLink="/dashboard">
      <mat-icon class="icon">dashboard</mat-icon>  
      <span class="label">Dashboard</span>
    </a>
    <a  mat-list-item 
      *ngIf="auth.isAuthenticated()"
      (click)="auth.logout()" type="button">
      <mat-icon class="icon">input</mat-icon>
      <span class="label">LogOut</span>
    </a>  
    </mat-nav-list>
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
     <div fxHide.gt-xs>
       <button mat-icon-button (click)="sidenav.toggle()">
        <mat-icon>menu</mat-icon>
      </button>
    </div>
     <div>
       <a routerLink="/">
          Material Blog
       </a>
       
     </div>
     <div fxFlex fxLayout fxLayoutAlign="flex-end"  fxHide.xs>
        <ul fxLayout fxLayoutGap="20px" class="navigation-items">
            <li>
                <a
                  *ngIf="!auth.isAuthenticated()"
                  (click)="auth.login()"
                >
                  <mat-icon class="icon">input</mat-icon>
                  <span  class="label">Login</span>
                 </a>
            </li>
            <li>
              <a
                *ngIf="auth.isAuthenticated()"
                routerLink="/"
              >
                  <mat-icon class="icon">home</mat-icon>
                  <span class="label">Home</span>
              </a>
            </li>
            <li>
                <a
                  routerLink="/dashboard"
                >
                    <mat-icon class="icon">dashboard</mat-icon>
                    <span class="label">Dashboard</span>
                </a>
              </li>
            <li>
                <a
                *ngIf="auth.isAuthenticated()"
                (click)="auth.logout()" type="button"
                >
                  <mat-icon class="icon">input</mat-icon>
                  <span class="label">LogOut</span>
                 </a>
            </li>
        </ul>
     </div>
    </mat-toolbar>
    <main>
      <router-outlet></router-outlet>
    </main>
  </mat-sidenav-content>
</mat-sidenav-container>
```
On the login item, we are showing it only if the user is not authenticated.  Some other navigation items are otherwise.
When the user clicks on that login button, we can use the Auth0 service to handle allow the user to register and be authaurized to use the app. 

Also, anyone can delete items in our dashboard, let's allow deletion if the user is authenticated. 
import the AuthService into the dashboard component as ;
```ts
import { AuthService } from '../auth/auth.service';
```
Inject it into the Dashboard class constructor as;
```ts 
constructor(public auth: AuthService, private dataService: DataService) {
    auth.handleAuthentication();
  }
```
Now  we can make use of the auth service innstance to check is the user is authenticated before deleting a post as;
```ts 
deletePost(id){
  if(this.auth.isAuthenticated()){
    this.dataService.deletePost(id)
    this.dataSource = new PostDataSource(this.dataService);
  }else{
      alert("Login in Before")
  }
}
```
As we mentioned earlier, we wanted to be able to add blog post to our data but we don't want anyone to add data just like that so we will have to 
also make sure the user can only add once authenticated. We can achieve this by adding `*ngIf="auth.isAuthenticated()"` directive to wrapping div of `Add Post`
button as;
```ts
<div class="blocks" *ngIf="auth.isAuthenticated()">
  <button button="submit" mat-raised-button color="primary">
    <mat-icon>add</mat-icon> Add Post
  </button>
</div>
```
## Associating Data with the App -- Part 2.
### Completing the Adding Data Functionality.

We will  make of `Angular Material Dialog` to create a modal that contains a form to add data to our data store. Let's create that with a component for this with 
`ng g c post-dialog --module app.module` command. 
Add the following to the `post-dialog-component.html` file;
```html
<h1 mat-dialog-title>{{data}}</h1>
<div mat-dialog-content>
  <form class="example-form" (ngSubmit)="onSubmit()">
    <mat-form-field>
      <input matInput placeholder="Post Title" type="text" required [(ngModel)]="blogPost.title" name="name">
    </mat-form-field>
    <mat-form-field>
      <textarea matInput placeholder="Post Body" required [(ngModel)]="blogPost.body" name="body"></textarea>
    </mat-form-field>
    <mat-form-field>
      <mat-select matInput placeholder="Post Category" required [(ngModel)]="blogPost.category" name="category">
        <mat-option *ngFor="let cat of categories" [value]="cat.value">
          {{ cat.viewValue }}
        </mat-option>
      </mat-select>
    </mat-form-field>
    <button mat-raised-button type="submit" color="primary">Save</button>
  </form>
</div>
<div mat-dialog-actions>
  <button mat-raised-button class="close" (click)="onNoClick()" color="warn">Cancel</button>
</div>
```
In the html file, you can see we are making use of `mat-dialog, mat-input, mat-select` from the `Angular Material`. You need to import them as we did earlier in our `material.module.ts` file.
In the component TypeScript file, `post-dialog-component.ts` add the following; 
```ts 
import { Component, Inject, EventEmitter, OnInit } from '@angular/core';
import { MatDialog, MatDialogRef, MAT_DIALOG_DATA } from '@angular/material';
import { DataService } from '../data/data.service';

@Component({
  selector: 'app-post-dialog',
  templateUrl: './post-dialog.component.html',
  styleUrls: ['./post-dialog.component.css']
})
export class PostDialogComponent {
  blogPost = {
    title: "",
    body: "",
    category: "",
    position: 0, 
    date_posted: new Date()
  };

  public event: EventEmitter<any> = new EventEmitter();
  constructor(
    public dialogRef: MatDialogRef<PostDialogComponent>,
    @Inject(MAT_DIALOG_DATA) public data: any,
    public dataService: DataService
  ) { }

  onNoClick(): void {
    this.dialogRef.close();
  }

  onSubmit(): void {
    this.blogPost.position = this.dataService.dataLength();
    this.event.emit({data: this.blogPost});
    this.dialogRef.close();
  }
  
  categories = this.dataService.getCategories();

}
```
Our `PostDialogComponent` component has a method to submit the data to our data service as well as a method to close the dialog. 
To make our button open up this dialog box, we need to tell it to do so by binding a click event to the button. Open the `dashboard.component.html` and 
modify the button we created before to;
```ts
<div class="blocks" *ngIf="auth.isAuthenticated()">
  <button button="submit" mat-raised-button color="primary" (click)="openDialog()">
    <mat-icon>add</mat-icon> Add Post
  </button>
</div>
```
In the TypeScript file of the `dashboard.component`, we can create the `openDialog` method as;
```ts 
openDialog(): void {
    let dialogRef = this.dialog.open(PostDialogComponent, {
      width: '600px',
      data: 'Add Post'
    });
    dialogRef.componentInstance.event.subscribe((result)=> {
      this.dataService.addPost(result.data)
      this.dataSource = new PostDataSource(this.dataService);
    })
}
```
We can infere the method makes use of `this.dialog` which is an instance of `MatDialog`. We can import and inject that into our constructor. Also, the method 
is making use of `PostDialogComponent` which we need to import.  Let's do so; 
```ts 
...
import { PostDialogComponent } from '../post-dialog/post-dialog.component';
import { MatDialog } from '@angular/material';
...
  constructor(public auth: AuthService, public dialog: MatDialog, private dataService: DataService) {
    auth.handleAuthentication();
  }
```
Now, we have a working adding blog post functionality. 


## Conclusion

