## Setup for Angular 2 Project with system.js
#### Based on https://angular.io/docs/ts/latest/quickstart.html

##make package.json
* npm init

###add devDependencies
* npm install concurrently --save-dev
* npm install lite-server --save-dev
* npm install typescript --save-dev
* npm install typings --save-dev

###add polyfill dependencies
* npm install core-js --save

###add vendor dependencies
* npm install rxjs --save
* npm install zone.js --save
* npm install reflect-metadata --save
* npm install systemjs --save


###add angular vendor dependencies
####details: https://angular.io/docs/ts/latest/guide/npm-packages.html

* npm install @angular/core --save
* npm install @angular/common --save
* npm install @angular/compiler --save
* npm install @angular/platform-browser --save
* npm install @angular/platform-browser-dynamic --save
* npm install @angular/http --save
* npm install @angular/router --save
* npm install @angular/router-deprecated --save

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