# Notes Angular

## Angular, vidéo 1

    Angular est un framework open-source soutenu par Google qui permet
    de faire des single page application.

    Le javascript sera exécuté sur le navigateur du coté client
    (utilisateur) et non pas sur le serveur.

    l'application se charge de mettre a à jour le html.

    L'application single page doit communiquer avec un serveur
    via des requettes http.

    Les projets d'applications web qui ont des interfaces
    complexes et qui necessitent des interactions sont
    facilités avec Angular. Les sites e-commerces
    par exemple ou des dashboard sont des projets typiquement
    facilités avec Angular.

    Angular n'est pas fait pour des sites avec du contenus.
    Des anciens navigateurs ou certains moteurs de recherche
    ne sont pas adaptés pour le javascript.

    Angular n'est pas adapté pour la mise à jour de sites web
    car il faut charger tout le framework qui est lourd.

    Progressive web application signigie que l'on peut
    télécharger l'application. Il y un seul code accessible
    sur ordinateur, mobile ect...

    Il y a différents api pour l'animation, le testing...

## Installation Angular, vidéo 2

    npm install -g @angular/cli

    ng new my-app

## Dossier e2e, vidéo 3

    Le dossier e2e signifie "end to end". C'est un dossier qui va contenir des tests end to end.
    Des tests "end to end" sont des tests qui ont été écris coté navigateur.
    On va tester le fait d'avoir des réactions coté navigateur.

    Exemple :

    getTitleText(): Promise<string> {
        return element(by.css('app-root .content span')).getText() as Promise<string>;
      }
    }

    Récupérer le titre de l'élement app.root, qui se trouve dans l'élément qui contient la class ".content"
    dans la span.

    On va tester ça, on va créer une nouvelle AppPage() :

    import { AppPage } from './app.po';
    import { browser, logging } from 'protractor';

    describe('workspace-project App', () => {
      let page: AppPage;

      beforeEach(() => {
        page = new AppPage();
      });

      it('should display welcome message', () => {
        page.navigateTo();
        expect(page.getTitleText()).toEqual('my-app app is running!'); // On va récupérer son getTitleText
      });

      afterEach(async () => {
        // Assert that there are no errors emitted from the browser
        const logs = await browser.manage().logs().get(logging.Type.BROWSER);
        expect(logs).not.toContain(jasmine.objectContaining({
          level: logging.Level.SEVERE,
        } as logging.Entry));
      });
    });

    On a le dossier node_modules qui contient toutes les dépendances.
    On a le dossier source src qui contient notre projet.

    On a le fichier angular.json, c'est un fichier qui contient les informations sur notre projet.

    Il va contenir les projets qui sont présents dans notre dossier.

    Avec CTRL+C on arrete le serveur.

    Exécuter la commande start : npm run start

    Exécuter la commande build : npm run build

    src/styles.scss contient tout les styles de l'application.styles

    src/environments/environments.ts : fichier qui contient les varialbes d'environement
    dans un objet environement :

## Installation Bootstrap, vidéo 4

    npm install bootstrap

    Fermer tous les onglets et ouvrir le fichier angular.json

    aller dans styles et ajouter le fichier de styles de bootstrap :

    "styles": [
                  "node_modules/bootstrap/dist/css/bootstrap.min.css", //ajouter le fichier de styles de bootstrap
                  "src/styles.scss"
                ],

    Arreter le serveur avec CTRL+C et le relancer avec la commande : ng serve

    Dans src/app/app.component.html ajout du bouton bootstrap suivant :

    <button type="button" class="btn btn-primary">Primary</button>


## Notre Premier composant

    src/app, faire clique droit sur app, cliquer sur Directory, pour créer un nouveau dossier
    qui sera appelé :  components, qui contiendra tous les composants.
    Dans le dossier components, ont créé un dossier que l'on nomme : app.
    déplacer dans le dossier app :  app.component.html, app.component.scss, app.component.specs.ts, app.component.ts .component

    Définition d'un composant : dans angular, un composant est une class.
    Il se définit comme une class que l'on exporte et qui est annotée d'une directive
     qui s'appelle Component:
    Exemple :
    import { Component } from '@angular/core'; //Directive importée du core de angular
    @Component({                              //directive
      selector: 'app-root',                   //directive
      templateUrl: './app.component.html',    //directive, templateUrl : quel est le chemin d'acèss pour son url
      styleUrls: ['./app.component.scss']     //directive, styleUrls : fichier SCSS de base
    })                                        //directive
    export class AppComponent {
      title = 'my-app';
    }

    On va créer un nouveau composant : on va aller dans components, faire new Directory
    et le nommer : home.

    On créer ensuite un fichier qui sera le logique du composant qui sera
    le fichier .ts : home.component.ts

    Ajout du style : home.component.scss

    Ajout de la page html : home.component.html

    Dans home.component.ts :

    import  { Component } from '@angular/core';

    @Component({
      selector:'app-home',
      templateUrl:'./home.component.html',
      styleUrls: ['./home.component.scss']
    })
    export class HomeComponent {

    }

    Aller dans le fichier app.modules.ts et déclarer HomeComponent :

    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './components/app/app.component';
    import { HomeComponent } from './components/home/home.component'; // importation de HomeComponent
    @NgModule({
      declarations: [
        AppComponent,
        HomeComponent                                                 // Déclaration de HomeComponent
      ],
      imports: [
        BrowserModule,
        AppRoutingModule
      ],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule { }


    Grace au selector selector:'app-home', on peut dans home.component.html
    utiliser app-home comme une balise html : <app-home></app-home>

    Création de composant dans la console  : ng generate component about


## Interpolation property binding

    L'interpolation :

    L'interpolation, c'est l'effet d'afficher le contenu d'une variable
    dans html.

    On veut afficher AppComponent dans le fichier html app.component.html
    pour cela dans app.component.html on a l'interpolation :

    {{ title }}

    Le Property Binding :

    <h2 [innerText]="title"></h2>

    <h2 [innerHTML]="title"></h2>

    <div [style.backgroundColor]="bgColor"> {{ user.name }}</div>

    Dans app.component.html on a :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';
      bgColor: string = 'red';
      user: {name:string} = {name:"Hadi"};

      getTitle():string {
        return this.title;
      }
    }


## Event Binding

    Dans app.component.html :

    <h1>{{ title }}</h1>

    <input type="text">

    <button (click)="changeColor()">Click</button>


    Dans app.component.ts :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';

      public changeColor() {
            alert('Bouton cliqué');
      }

    }


    Changement de titre :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';

      public changeColor() {
            this.title="Event Binding Cliqué";
      }

    }


    Changement d'input :

    <h1>{{ title }}</h1>


    <input (change)="setText()" type="text">

    <button (click)="changeColor()">Click</button>

    <p>{{ text }}</p>


    Afficher le input :

    <h1>{{ title }}</h1>


    <input #inputRef (change)="setText(inputRef)" type="text">

    <button (click)="changeColor()">Click</button>

    <p>{{ text }}</p>


    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';
      text:string = '';

      public changeColor() {
            this.title="Event Binding Cliqué";
      }

      public setText(input) {
             this.text = input.value;
             console.dir(input.value);
      }

    }

    Récupérer un évènement avec $event :

    <h1>{{ title }}</h1>


    <input #inputRef (change)="setText(inputRef, $event)" type="text">

    <button (click)="changeColor($event)">Click</button>

    <p>{{ text }}</p>


    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';
      text:string = '';

      public changeColor(event) {
            this.title="Event Binding Cliqué";
            console.log(event);
      }

      public setText(input, event) {
             this.text = input.value;
             console.dir(input.value);
      }

    }


## Two way data binding

    app.component.html :
    <h1>{{ title }}</h1>


    <input [(ngModel)]="text" type="text">

    <button (click)="changeColor($event)">Click</button>

    <p [style.color]="text">{{ text }} </p>


    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = '<a>Interpolation et Property Binding</a>';
      text:string = 'red';


    }



## Structural directive ngIf

    app.component.html :

    <h1>{{ title }}</h1>



    <p *ngIf="user; else userIsNull">{{ user.name }} </p>

    <ng-template #userIsNull>
      <p>User est null</p>
    </ng-template>

    app.component.ts :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = 'Structural  Directive : ngIf';
      user: { name: string } = null;
      show: boolean = true;

      isShown(): boolean{
        return this.show;
      }
    }


## Structural directive ngfor

    app.component.html :

    <h1 *ngIf="show">{{ title }}</h1>

    <ng-container *ngFor="let user of users; let id = index">
    <div *ngIf="user.color">
      <div>{{ id }}  - {{ user.name }} | {{ user.color}}</div>

      <button (click)="deleteUser(id)">Afficher</button>
    </div>
    </ng-container>


    <button (click)="show= !show">Toggle Title</button>



    app.component.ts :

    title:string = 'Structural  Directive : ngFor';
      show: boolean = false;

      users: { name: string, color?: string}[]=[
        {name: 'Hadi',color: 'grey'},
        {name: 'Kayaam'},
        {name: 'hadi2',color: 'green'}
      ];

      deleteUser(id): void {
        let arr = [...this.users];
        arr.splice(id, 1);
        this.users = [...arr] ;

        console.log(id);
      }

    }


## Mise en pratique


    app.component.html :

    <div class="container">
      <h1 class="my-5">{{ title }}</h1>


    <div class="form-group">
    <input [(ngModel)]="text" #inputRef id="input" placeholder="Le nom de la tache" type="text" >
    <button type="button" id="btn" class="btn btn-primary" (click)="addTask(inputRef)">Ajouter</button>
    </div>


      <p *ngIf="text !=='' && text">La prochaine tache  : {{ text }} </p>

      <div id="tasks">
        <div class="task" *ngFor="let task of tasks; let id = index" (click)="deleteTask(id)"> {{ id }} - {{ task }}</div>
      </div>

      <button type="button" id="btn-save" class="btn btn-primary"
      (click)="save()">Enregistrer</button>

    </div>


    app.component.ts :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = 'Mettre en pratique les bases';

      tasks: string[] = [
           'Sortir le chien',
           'Nettoyer le salon',
           'Jetter les poubelles'
      ];

      text:string = '';

      addTask(inputRef: HTMLInputElement): void {
        console.dir(inputRef);
        this.tasks.push(this.text);
        inputRef.value = '';
        this.text = '';
    }

      deleteTask(id:number): void{
        let arr =  [...this.tasks];
        arr.splice(id,1);
        this.tasks = [...arr];
        console.log(id, this.tasks[id]);
      }

      save():void {
        this.tasks.forEach(function (task) {
           console.log(task);
        });
      }

    }


    app.component.scss   :

    .form-group {
      display: flex;
      margin-bottom: 30px;
    }


    .btn {
      padding: 10px;
      background: darkblue;
      border: none;
      color: white;
      cursor: pointer;
    }

    #input  {
      width: 100%;
      height: 50px;
      border-radius: 5px;
      border: 1px solid #cecece;
      padding: 0 20px;
    }

    #tasks {

    }

    .task {
      padding: 30px;
      display: flex;
      align-items: center;
      background-color: #caeecd;
      margin-bottom: 20px;
      border-radius: 5px;
      transition: all .3s ease-in-out;
      cursor: pointer;
    }

    .task:hover {
      background-color: lightgreen;
      transform: translateX(2px);
    }


## Découpage des composants

    app.component.html  :

    <div class="container">
      <h1 class="my-5">{{ title }}</h1>



      <app-add-task></app-add-task>


      <app-task *ngFor="let task of tasks; let id = index"></app-task>


      <button type="button" id="btn-save" class="btn btn-primary"
      (click)="save()">Enregistrer</button>

    </div>


    app.component.ts  :

    import { Component} from '@angular/core';

    @Component({
      selector: 'app-add-task',
      templateUrl: './add-task.component.html',
      styleUrls: ['./add-task.component.scss']
    })
    export class AddTaskComponent {

      text: string ='';

      addTask():void {

      }

    }


    app.component.scss  :

    .form-group {
      display: flex;
      margin-bottom: 30px;
    }


    .btn {
      padding: 10px;
      background: darkblue;
      border: none;
      color: white;
      cursor: pointer;
    }

    #input  {
      width: 100%;
      height: 50px;
      border-radius: 5px;
      border: 1px solid #cecece;
      padding: 0 20px;
    }

    #tasks {

    }

    .task {
      padding: 30px;
      display: flex;
      align-items: center;
      background-color: #caeecd;
      margin-bottom: 20px;
      border-radius: 5px;
      transition: all .3s ease-in-out;
      cursor: pointer;
    }

    .task:hover {
      background-color: lightgreen;
      transform: translateX(2px);
    }



## Partager des données à un composant enfant - Input decorator

    task.component.ts  :

    import {Component, Input} from "@angular/core";


    @Component({
      selector: 'app-task',
      template: `<div class="task"> {{ id }} - {{ task }}</div>`,
      styleUrls:  ['./task.component.scss'],
    })
    export class TaskComponent {

        @Input('index')
        id:number;
        @Input() task:string;

    }


    app.component.html  :

    <div class="container">
      <h1 class="my-5">{{ title }}</h1>



      <app-add-task></app-add-task>


      <app-task *ngFor="let task of tasks; let id = index" [task]="task"  [index]="id">

      </app-task>


      <button type="button" id="btn-save" class="btn btn-primary"
      (click)="save()">Enregistrer</button>

    </div>


## Émettre des données au composant parent

    app.component.ts  :

    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title:string = 'Mettre en pratique les bases';

      tasks: string[] = [
           'Sortir le chien',
           'Nettoyer le salon',
           'Jetter les poubelles'
      ];



      addTask(task: string): void {
        this.tasks.push(task);
    }

      deleteTask(id:number): void{
        let arr =  [...this.tasks];
        arr.splice(id,1);
        this.tasks = [...arr];
        console.log(id, this.tasks[id]);
      }

      save():void {
        this.tasks.forEach(function (task) {
           console.log(task);
        });
      }

    }


    app.component.html  :

    <div class="container">
      <h1 class="my-5">{{ title }}</h1>



      <app-add-task (task)="addTask($event)"></app-add-task>


      <app-task *ngFor="let task of tasks; let id = index"
                [task]="task"  [index]="id"
                (click)="deleteTask(id)">
      </app-task>


      <button type="button" id="btn-save" class="btn btn-primary"
      (click)="save()">Enregistrer</button>

    </div>

    add-task.component.ts  :

    import {Component, EventEmitter, Output} from '@angular/core';

    @Component({
      selector: 'app-add-task',
      templateUrl: './add-task.component.html',
      styleUrls: ['./add-task.component.scss']
    })
    export class AddTaskComponent {

      text: string ='';

      @Output('task') taskEmit = new EventEmitter();

      addTask():void {

            this.taskEmit.emit(this.text);
      }

    }


## Modules dans Angular

    Dans tous les language, un module sert à compartimenter le code, à l'encapsuler.

    Il s'agit de séparer les fonctionnalités d'un programme et de les mettres chacun dans
    un seul module.
    On passe par exemple d'un module  avec 5 fonctionnalités à 5 modules avec chacun une fonctionnalité.

    On définit les dépendances et les éléments notre module.

    import {BrowserModule} from '@angular/platform-browser';
    import {NgModule} from '@angular/core';

    import {AppRoutingModule} from './app-routing.module';
    import {AppComponent} from './components/app/app.component';
    import {HomeComponent} from './components/home/home.component';
    import {AboutComponent} from './components/about/about.component';
    import {FormsModule} from "@angular/forms";
    import {TaskComponent} from "./components/task/task.component";
    import {AddTaskComponent} from './components/add-task/add-task.component';

    @NgModule({
      declarations: [
        AppComponent,
        HomeComponent,
        AboutComponent,
        TaskComponent,
        AddTaskComponent
      ],
      imports: [
        BrowserModule,
        AppRoutingModule,
        FormsModule
      ],
      providers: [],
      exports: [], //Permet d'exporter des services et des composants de notre module
      bootstrap: [AppComponent]
    })
    export class AppModule {
    }


## Routing

    navbar.component.html

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>


      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active" routerLink="/" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">
            <a class="nav-link">Dashboard</a>
          </li>
          <li class="nav-item" routerLink="/users" routerLinkActive="active">
            <a class="nav-link">Users</a>
          </li>
          <li class="nav-item" routerLink="/users/info" routerLinkActive="active">
            <a class="nav-link">Info</a>
          </li>
          <li class="nav-item" routerLink="/contact" routerLinkActive="active">
            <a class="nav-link">Contact</a>
          </li>
        </ul>
      </div>
    </nav>


    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>


      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active" routerLink="/" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">
            <a class="nav-link">Dashboard</a>
          </li>
          <li class="nav-item" routerLink="/users" routerLinkActive="active">
            <a class="nav-link">Users</a>
          </li>
          <li class="nav-item" routerLink="/users/info" routerLinkActive="active">
            <a class="nav-link">Info</a>
          </li>
          <li class="nav-item" routerLink="/contact" routerLinkActive="active">
            <a class="nav-link">Contact</a>
          </li>
        </ul>
      </div>
    </nav>

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>


  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active" routerLink="/" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">
        <a class="nav-link">Dashboard</a>
      </li>
      <li class="nav-item" routerLink="/users" routerLinkActive="active">
        <a class="nav-link">Users</a>
      </li>
      <li class="nav-item" routerLink="/users/info" routerLinkActive="active">
        <a class="nav-link">Info</a>
      </li>
      <li class="nav-item" routerLink="/contact" routerLinkActive="active">
        <a class="nav-link">Contact</a>
      </li>
    </ul>
  </div>
</nav>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>


      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active" routerLink="/" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">
            <a class="nav-link">Dashboard</a>
          </li>
          <li class="nav-item" routerLink="/users" routerLinkActive="active">
            <a class="nav-link">Users</a>
          </li>
          <li class="nav-item" routerLink="/users/info" routerLinkActive="active">
            <a class="nav-link">Info</a>
          </li>
          <li class="nav-item" routerLink="/contact" routerLinkActive="active">
            <a class="nav-link">Contact</a>
          </li>
        </ul>
      </div>
    </nav>

    Routing : Params

    users.component.ts

    import {Component, OnInit} from "@angular/core";


    @Component({
      selector: 'app-users',
      templateUrl: './users.component.html',

    })
    export class UsersComponent implements OnInit{

        users: {id: number, name:string} [] = [
          {id:1, name:'John'},
          {id:2, name:'Sam'}
        ];


        constructor() {
        }

        ngOnInit() {
        }

    }


    info.component.ts

    import {ActivatedRoute} from "@angular/router";


    @Component({
      selector: 'app-info',
      templateUrl: './info.component.html',

    })
    export class InfoComponent implements OnInit {

      constructor(private route: ActivatedRoute) {
      }

      public id: string;

      ngOnInit() {
        console.log(this.route.snapshot.params.id);
        this.id = this.route.snapshot.params.id;
      }


    }

    <h1>Info works!</h1>

    <p>Id de l'utilisateur : {{ id }}</p>

    <button class="btn btn-primary" routerLink="..">Retour</button>


##   Routing : Router service

    user.component.html

    <h1>Users works !</h1>

    <ul>
      <li *ngFor="let user of users" (click)="showInfo(user.id)">
        {{ user.id }}.  {{ user.name }}</li>
    </ul>


    user.component.ts

    import {Component, OnInit} from "@angular/core";
    import {timeout} from "rxjs/operators";
    import {Router} from "@angular/router";


    @Component({
      selector: 'app-users',
      templateUrl: './users.component.html',

    })
    export class UsersComponent implements OnInit {

      users: { id: number, name: string } [] = [
        {id: 1, name: 'John'},
        {id: 2, name: 'Sam'}
      ];


      constructor(private router: Router) {
      }

      ngOnInit() {

        setTimeout(() => {
          // Au bout de 3 secondes
          // Redirige vers les info de l'utilisateur 1
          //  this.router.navigateByUrl('/users/1');
        })
      }

      public showInfo(id: number) {

        this.router.navigateByUrl('/users'+ id);

      }


    }


    info.component.html

    <h1>Info works!</h1>

    <p>Id de l'utilisateur : {{ id }}</p>

    <button class="btn btn-primary" (click)="goBack()">Retour</button>

## Component LifeCycle

    app.component.html




<div class="container">

  <app-navbar></app-navbar>

  <app-lifecycle [title]="title"   [var1]="'A'"></app-lifecycle>

  <router-outlet></router-outlet>

</div>


    lifecycle.component.ts

    import {
      AfterContentChecked,
      AfterContentInit, AfterViewChecked,
      AfterViewInit,
      Component,
      DoCheck, Input,
      OnChanges, OnDestroy,
      OnInit, SimpleChanges
    } from '@angular/core';

    @Component({
      selector: 'app-lifecycle',
      templateUrl: './lifecycle.component.html',
      styleUrls: ['./lifecycle.component.scss']
    })
    export class LifecycleComponent implements OnChanges, OnInit, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

      @Input() title = '';
      @Input() var1 = '';


      constructor() {
      }

      ngOnChanges(changes: SimpleChanges): void {
        console.log('On Changes - LifeCycle', changes.title.previousValue, changes.title.currentValue);
      }

      ngOnInit(): void {
        console.log('On Init - LifeCycle');
      }

      ngAfterContentChecked(): void {
        console.log('On Init - LifeCycle');
      }

      ngDoCheck(): void {
        console.log('Do Check - LifeCycle');
      }

      ngAfterContentInit(): void {
        console.log('After Content - LifeCycle');
        if(this.title === this.var1){
          //Notre code
        }
      }

      ngAfterViewInit(): void {
        console.log('After View Init - LifeCycle');
      }

      ngAfterViewChecked(): void {
        console.log('After View Checked - LifeCycle');
      }

      ngOnDestroy(): void {
        console.log('On Destroy - LifeCycle');
      }

    }


## Programmation réactive avec la librairie RxJs

    index.html

    <!doctype html>
    <html lang="en">
    <head>

    </head>
    <meta charset="UTF-8">
    <title>Rxjs</title>
    <body>
    <div class="container">

      <h1 class="my-5">Programmation reactive avec la librairie RxJs</h1>

      <button class="btn btn-primary">Button</button>


    </div>

    <script  src="https://unpkg.com/rxjs/bundles/rxjs.umd.min.js"></script>

    <script src="index.js"></script>
    </body>
    </html>


    index.js

    const {Observable, fromEvent} = rxjs;
    const {map} = rxjs.operators;

    const button = document.querySelector('button');

    let count = 0;
    const subscription = fromEvent(button,'click')
      .pipe(map((value)=> {
        console.log('value', value);
        return 50;
      }),)
      .subscribe(
      (value)=> { console.log(++count, value); },
      ()=> {},
      ()=> {});

    // Un flux de données
    const flux = new Observable(function (observer) {
      observer.next(1);
      observer.next(10);
      observer.next(100);


      setTimeout(()=> {
        observer.next(20);
        observer.complete();

      }, 2000);
    });

    const abonnement = flux.subscribe(

      function(value) {
        console.log('La valeur est :',value);
      },
      function(err) {
        console.log('Erreur :', err);
      },
      function(complete) {
        console.log('Complet');
      }
    );

    abonnement.unsubscribe();
    subscription.unsubscribe();











































