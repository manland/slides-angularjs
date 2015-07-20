/*!SLIDE bullets ============================

Plan :

* Angular2 spoiler 15min
  * moi
    * 3 ans d'angular1, fait passer itk de gwt à angular
    * 2 mois d'angular2 -> toujours pas réussi à faire ng2 emebed !! Pas stable du tout !! Look le gitter d'angular pour avoir des infos ;)
  * Why ? 
    * reproches : angular1 2009, lent controller, scope..., watch, difficile à comprendre = trop de concepts (service, factory, provider... directive, watch de propriété)
    * en parallèle : html5 (toujours pas de localStorage dans ng1), es6 (sucre syntaxique mais...), web component, web worker
  * Nouveautés
    * tout découpé pour sortir d'angular, chacun embarque ce qu'il veut et/ou sa propre implémentation (router, di, templating...)
    * nouveau templating (beurk mais on s'y fait :D)
    * plus de double binding (1 way binding à la react)
    * Zone
    * Typescript !!! (ça existait mais pas sûr du future puis nouveau CTO microsoft et effort de google)
  * du code (en live !?) :
    * angular1 petite app vs angular2

* Angular1 project 15min
  * en attendant on peut
    * vieux, voir très vieux projet : from controller to directive
    * moyen vieux voir vieux : ajouter typescript
    * nouveau : typescript + ng1 mimic ng2
    * prochain projet (entre 3 et 6 mois) : si on se sent bien directement en ng2

*/

!SLIDE ============================

# ItSaucisse : Angular2

![](img/arc-en-ciel.gif)

*Il n'y a que 2 types de languages, ceux qu'on critique tout le temps, et ceux dont on ne parle pas !*

!SLIDE bullets ============================

# Moi

![](img/supermoi.jpg)

* Développeur *qui aime bien le front*
* 3 ans d'Angular 1, *Fait notable : à propulser ITK de GWT à AngularJs*
* 2 mois d'Angular 2... *Pour s'amuser*

!SLIDE ============================

# Pourquoi tout changer ?

!SLIDE bullets smaller ============================

* Angular est vieux : 2009
* Angular est lent
  * controller, scope, watch
* Angular est compliqué
  * controller
  * services : service, factory, provider, value...
  * directive : E, A, link, controller

!SLIDE bullets smaller ============================

# Pendant ce temps, dans un pays ~~sans IE~~

* HTML 5
* ES 6
* WebWorker
* WebComponent

!SLIDE small ============================

# Réunion de crise chez Google

IMAGE POWER R

!SLIDE small bullets ============================

# Un meilleurs monde

On garde les même concepts mais on refait mieux

* Un framework JS qui permet de tester facilement
* Qui comprend tout ce dont on a besoin pour faire une SPA (DI, router, call http...)
* Qui est le moins intrusif possible (pas de MyFramework.model(['id', 'name']))

!SLIDE small ============================

# Ok mais si on refait, on fait bien

Découplage au maximum de tout

!SLIDE small ============================

# Nouveau templating

```html
<div ng-for="provider in providers" ng-class="provider.classes">
    <img ng-if="provider.name" src="{{provider.name}}.png">
    <p ng-click="providerClick(provider)">{{provider.name}}</p>
</div>
```

```html
<div *ng-for="#provider of providers" [class]="provider.classes">
    <img *ng-if="provider.name" src="{{provider.name}}.png">
    <p (click)="providerClick(provider)">{{provider.name}}</p>
</div>
```

!SLIDE small ============================

# Aurevoir double binding

```html
<input type="text" ng-model="myValue">
```

```html
<input type="text" [value]="myValue" (keyup)="myValue=$event.target.value">
```

!SLIDE small ============================

# Zones.js : aurevoir $digest, $apply, $asyncApply, $timeout...

!SLIDE small ============================

# Typescript

!SLIDE small ============================

# On veut voir du code !

!SLIDE small ============================

# Que faire de nos applis Angular 1 ?