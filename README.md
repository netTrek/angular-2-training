## Setup for Angular 2 Project with system.js
#### Based on https://angular.io/docs/ts/latest/quickstart.html

##make package.json
* npm init

###add devDependencies
* npm install concurrently --save-dev
> Gleichzeitiges Ausführen von Prozessen
* npm install lite-server --save-dev
> Server mit Reload Mechanismus
* npm install typescript --save-dev
> TypeScript für node.js
* npm install typings --save-dev
> TypeScript D.ts Steuern

###add polyfill dependencies
* npm install core-js --save
> es2015/E6 polyfills


###add vendor dependencies
* npm install rxjs --save
> Biliothek um Ereignis und Asynchrone Prozesse zu Überwachen. Wird für HTTP Aufrufe von Angular genutzt.
* npm install zone.js --save
> Ähnlich domains in Node, Ausführungskontext der uns ermöglicht die Ausführung zu überwachen und zu delegieren.
* npm install reflect-metadata --save
> Metadaten in konsistenter Weise zu einer Klasse hinzuzufügen.
* npm install systemjs --save
> Modul Loder für ES2015/ES6 Module


###add angular vendor dependencies
>details: https://angular.io/docs/ts/latest/guide/npm-packages.html

* npm install @angular/core --save
> Notwendige für jede Anwendung. Ist der Kern für Komponenten, Direktiven, Dependency Injection und  Komponentenlebenszyklus
* npm install @angular/common --save
> Häufig verwendete Direktiven, Pipes und Services
* npm install @angular/compiler --save
> Kompiniert Logik mit Vorlagen. Der Compiler wird autom. über die platform-browser-dynamic angestoßen
* npm install @angular/platform-browser --save
> Browser und DOM relevante Bestandteile, vor allem zum rendern neuer Elemente. Ermöglicht über bootstrapStatic as Bootstrapping vorkompilierter Vorlagen.
* npm install @angular/platform-browser-dynamic --save
> Verfügt über die Bootstrapping Methode
* npm install @angular/http --save
> Modul für HTTP Aufrufe
* npm install @angular/router --save
* npm install @angular/router-deprecated --save
> Module für den Komponenten Router

##add generate tsconfig and modify
* npm run tsc -- -init

        "module": "commonjs",
        "target": "es5",
        "moduleResolution": "node",
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true,
        "removeComments": false,
        "noImplicitAny": false,
        "sourceMap": true

##generate typings config
>see also: https://angular.io/docs/ts/latest/guide/typescript-configuration.html#!#typings

* npm run typings -- init

###add typings
* npm run typings -- install dt~node --save --global
* npm run typings -- install dt~core-js --save --global


##add npm scripts

    "postinstall": "typings install",
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "lite": "lite-server",
            "tsc": "tsc",
    "tsc:w": "tsc -w",
    
##finish
* create system.config.js
* Index html fertig stellen

<!--Pollyfills-->
    <script src="node_modules/core-js/client/shim.min.js"></script>

    <!--Vendor-->
    <script src="node_modules/zone.js/dist/zone.js"></script>
    <script src="node_modules/reflect-metadata/Reflect.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>

    <!--<script src="system.config.js"></script>-->
    <script>
        System.import ('system.config.js').then ( function () {
            System.import ('app')
        }).catch( function (err) {
            console.error(err);
        })
    </script>
    
* make main.ts
* npm run start

* nun app.component erstellen 
* und in main einbinden als Bootstrap!