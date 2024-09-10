# WrenDoc
A documentation generator for the [Wren](https://wren.io/) scripting language.
 
## Usage
Uses perl v5.30.3
```
perl WrenDoc.pl -out Doc.md -in Behaviour.wren -v
```
### Flags
> - \-i | in: comma separated .wren inputs
> - \-o | out: .md output filename
> - \-v | verbose: gives detailed information during script runtime

## How To Use
To document your code just add documentation comments before a code symbol.
```js
///(Arg Type A), (Arg Type B), ... -> (Return Type)
///Descriptions can be typed as well and will append to-
///the next available code symbol.
```
If no documentation comments are found no worries your code will still generate a document, however, there will not be any type annotations or descriptions. Any missing type annotation will appear as a ``_``

Here's an example of some wren code that has been documented:
```js
///Behaviours allow for custom code to run on GameObjects during the game loop.
class Behaviour is Serializable {
    ///_ -> Any
    ///Global data for behaviours
    static data { __data }
    ///Any -> _
    static data=(v) { __data = v }
    
    ///Num -> Num
    static [i] {
        return __data[i]
    }

    ///Any, Any -> _
    static [i] = (v) {
        __data[i] = v
    }
	
    ///_ -> Num
    frame {
        if(_frame == null) {
            _frame = 0
        }
        return _frame
    }
	
    ///Num -> _
    frame=(v) {_frame=v}
	
    ///_ -> ComponentBehaviour
    as_behaviour { _behaviour }
	
    ///GameObject, ComponentBehaviour -> Behaviour
    construct new(g, c) {
        if(__data == null) {
            __data = {}
        }
        if(__data[g.uuid] == null) {
            __data[g.uuid] = {}
        }
        if(__data[g.uuid]["%(c)"] == null) {
            __data[g.uuid]["%(c)"] = {}
        }
        

        var b = ComponentBehaviour.new("%(c)")
        _behaviour = b.as_component
        __data[g.uuid]["%(c)"][b.uuid] = c.new()
    }
	
    ///_ -> null
    ///Runs the frame after setup.
    static start() {}
    ///_ -> null
    ///Run every frame.
    static update() {}
    ///Map -> null
    ///Runs every frame after start that the Behaviour has a collision given a Rigidbody and Transform is attached.
    static onCollision(collision) {}

    ///_ -> null
    ///Runs the first frame regardless of whether or not the Behaviour is attached.
    setup() {}
    ///_ -> null
    ///Runs the second frame regardless of whether or not the Behaviour is attached.
    start() {}
    ///_ -> null
    ///Runs every frame after start regardless of whether or not the Behaviour is attached.
    update() {}
}
```
When run through WrenDoc we will get an output like this:

```
$ perl WrenDoc.pl -out Doc.md -in Behaviour.wren -v
WrenDoc: building Doc.md
  WrenDoc: starting Behaviour.txt
    WrenDoc Found: class
    WrenDoc Found: static getter
    WrenDoc Found: static setter
    WrenDoc Found: static getter
    WrenDoc Found: static setter
    WrenDoc Found: getter
    WrenDoc Found: setter
    WrenDoc Found: getter
    WrenDoc Found: constructor
    WrenDoc Found: static method
    WrenDoc Found: static method
    WrenDoc Found: static method
    WrenDoc Found: method
    WrenDoc Found: method
    WrenDoc Found: method
  WrenDoc: built doc => Behaviour.txt
WrenDoc: Finished
```

# Doc
### Modules
> - [Behaviour](#module-behaviour)
## Module ``Behaviour``
### Classes
> - [Behaviour](#class-behaviour)
### Class ``Behaviour``
> Inherits from ``Serializable``
>
> Behaviours allow for custom code to run on GameObjects during the game loop.

#### Constructors
> - [new](#Behaviour-0-c-1)
#### Getters
> - [data](#Behaviour-0-g-1)
> - [[i]](#Behaviour-0-g0)
> - [frame](#Behaviour-0-g1)
> - [as_behaviour](#Behaviour-0-g2)
#### Setters
> - [data](#Behaviour-0-s-1)
> - [[i]](#Behaviour-0-s0)
> - [frame](#Behaviour-0-s1)
#### Methods
> - [start](#Behaviour-0-m-1)
> - [update](#Behaviour-0-m0)
> - [onCollision](#Behaviour-0-m1)
> - [setup](#Behaviour-0-m2)
> - [start](#Behaviour-0-m3)
> - [update](#Behaviour-0-m4)
##### Static Getter ``data`` <a id='Behaviour-0-g-1'></a>
``return Any``
> Global data for behaviours

##### Static Setter ``data = v: Any`` <a id='Behaviour-0-s-1'></a>

##### Static Getter ``[i]: Num`` <a id='Behaviour-0-g0'></a>
``return Num``

##### Static Setter ``[i]: Any = v: Any`` <a id='Behaviour-0-s0'></a>

##### Getter ``frame`` <a id='Behaviour-0-g1'></a>
``return Num``

##### Setter ``frame = v: Num`` <a id='Behaviour-0-s1'></a>

##### Getter ``as_behaviour`` <a id='Behaviour-0-g2'></a>
``return ComponentBehaviour``

##### Constructor ``new(g: GameObject, c: ComponentBehaviour)`` <a id='Behaviour-0-c-1'></a>
``return Behaviour``

##### Static Method ``start()`` <a id='Behaviour-0-m-1'></a>
``return null``
> Runs the frame after setup.

##### Static Method ``update()`` <a id='Behaviour-0-m0'></a>
``return null``
> Run every frame.

##### Static Method ``onCollision(collision: Map)`` <a id='Behaviour-0-m1'></a>
``return null``
> Runs every frame after start that the Behaviour has a collision given a Rigidbody and Transform is attached.

##### Method ``setup()`` <a id='Behaviour-0-m2'></a>
``return null``
> Runs the first frame regardless of whether or not the Behaviour is attached.

##### Method ``start()`` <a id='Behaviour-0-m3'></a>
``return null``
> Runs the second frame regardless of whether or not the Behaviour is attached.

##### Method ``update()`` <a id='Behaviour-0-m4'></a>
``return null``
> Runs every frame after start regardless of whether or not the Behaviour is attached.
\
\
\
## Organization
When documenting multiple modules and classes WrenDoc will organize a list of modules at the top of the page and at each module it will list all classes in the module.
