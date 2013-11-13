!SLIDE bullets small ============================

# JS CheatSheet

* [Objet](index.html#/2)
* [Graphisme](index.html#/3)
* [Test](index.html#/4)
* [Autre](index.html#/5)

!SLIDE bullets small ============================

# JS CheatSheet - objet

* [Classe](index.html#/6)
* [Héritage](index.html#/7)
* [Classe static](index.html#/8)

!SLIDE bullets small ============================

# JS CheatSheet - graphisme

* [Eléments graphiques](index.html#/9)
* [Ajout au DOM](index.html#/10)
* [Style des éléments graphiques](index.html#/11)

!SLIDE bullets small ============================

# JS CheatSheet - test

* [Test](index.html#/12)
* [Except](index.html#/13)
* [Mock](index.html#/14)

!SLIDE bullets small ============================

# JS CheatSheet - autre

* [Collection](index.html#/15)
* [Bootstrap](index.html#/16)
* [Callback](index.html#/17)
* [Click](index.html#/18)
* [Timeout, Interval](index.html#/19)

!SLIDE ============================

#Classe

```javascript
var ClassName = (function() {

  'use strict';

  //Constructeur
  function ClassName() {
    this.attribut = 'romain';
  }

  ClassName.prototype.method = function() {
    this.attribut = this.attribut + ' est cool :D';
  };
}
```

```javascript
var a = new ClassName();
a.method();
```

!SLIDE ============================

#Héritage

Copier la [classe static](https://github.com/Froggies/game-off-2013/blob/master/app/src/util/ObjectUtil.js)

```javascript
var ClassName = (function() {

  'use strict';

  //Constructeur
  function ClassName() {

  }

  ObjectUtil.inherit(ClassName, ClasseParent);

}
```

!SLIDE ============================

#Classe static

```javascript
var ClassName = (function() {

  'use strict';

  return {
    method: function() {

    }
  }

}
```

```javascript
ClassName.method();
```

!SLIDE ============================

#Graphisme

```javascript
var div = document.createElement('div');
var span = document.createElement('span');
var ul = document.createElement('ul');
```

!SLIDE ============================

#DOM

```javascript
var div = document.createElement('div');
var body = document.getElementsByTagName('body')[0];
body.appendChild(div);
```

```javascript
var div = document.createElement('div');
var container = document.getElementById('idContainer');
container.appendChild(div);
```

!SLIDE ============================

#Style

```javascript
var div = document.createElement('div');
div.className = 'classCss';
```

```javascript
var div = document.createElement('div');
div.style.nomStyle = 'valeur';
```

!SLIDE small ============================

#Test

```javascript
var dependencies = [
  'path/fileNoDotJs',
];

define(dependencies, function() {
  describe('my class', function() {

    var className;

    beforeEach(function() {
      className = new ClassName();
    });

    it('should make feature', function () {
      expect(className.myVar).toBeDefined();
    });
  });
});
```

!SLIDE bullets small ============================

#Expect

* expect(className.myVar).toBe(true);
* expect(className.myMethod()).toBe(1);
* expect(className.myMethod()).not.toBe('myString');

*Autres sur le [site](http://pivotal.github.io/jasmine/)*

!SLIDE ============================

#Mock

```javascript
foo = {
  setBar: function(value) {
    bar = value;
  }
};

spyOn(foo, 'setBar');
```

```javascript
expect(foo.setBar).toHaveBeenCalled();
```

!SLIDE small ============================

#Collection

```javascript
//create
var collection = [];
```

```javascript
//add
collection.push(1);
collection.push('a');
collection.push({a: undefined});
```

```javascript
//foreach
for(var i=0; i<collection.length; i++) {
  var elem = collection[i];
}
```

```javascript
//remove
collection.splice(index, 1);
```

!SLIDE ============================

#Bootstrap

```javascript
window.onload = function() {
  var globalContainer = document.getElementById('globalContainer');

  var myClass = new MyClass();
  myClass.start(globalContainer);
}
```

!SLIDE ============================

#Callback

```javascript
var MyClass = ...

MyClass.prototype.myMethod = function(callback) {
  callback();
}
```
```javascript
myClass.myMethod(function() {
  //exécuter quand c'est le moment
});
```

!SLIDE ============================

#Click

```javascript
var element = document.getElementById('globalContainer');
element = document.createElement('button');
var that = this;
element.onclick = function() {
  //exécuter quand on click
  //attention au context !!
  that.myMethod();
}
```

!SLIDE ============================

#Timeout, Interval

```javascript
var that = this;
var timeout = window.setTimeout(function() {
  //exécuter après time secondes
  window.clearTimeout(timeout);//pour l'annuler
  //attention au context !!
  that.myMethod();
}, time * 1000);
```

```javascript
var that = this;
var interval = window.setInterval(function() {
  //exécuter toutes les time secondes
  window.clearInterval(timeout);//pour l'annuler
  //attention au context !!
  that.myMethod();
}, time * 1000);
```
