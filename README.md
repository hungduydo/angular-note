# angular-note

This repository will note all knowledge about angular 4

# Dynamic template load.
- Using Component for create dynamic component
- Using NgModule for add decland for component
- Using Compiler for syn component

``` typescript
import { Component, OnInit, Injector, ComponentRef, ComponentFactoryResolver, ApplicationRef } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import {
    Compiler, VERSION, ViewChild, NgModule, NgModuleRef,
    ViewContainerRef
  } from '@angular/core';
declare var $: any;
declare var module: any;

@Component({
    selector: 'app-tutorial',
    templateUrl: './tutorial.component.html',
    styleUrls: ['./tutorial.component.css']
})

export class TutorialComponent {
    @ViewChild('vc', {read: ViewContainerRef}) vc;
    name = `Angular! v${VERSION.full}`;
  
    
    constructor(
        private _compiler: Compiler,
        private _injector: Injector,
        private _m: NgModuleRef<any>) { }

  
    ngAfterViewInit() {
        const tmpCmp = Component({
            moduleId: module.id, templateUrl: './e.component.html', styleUrls: ['./tutorial.component.css']})(class {
        });
        const tmpModule = NgModule({declarations: [tmpCmp]})(class {
        });
    
        this._compiler.compileModuleAndAllComponentsAsync(tmpModule).then((factories) => {
            const f = factories.componentFactories[0];
            const cmpRef = f.create(this._injector, [], null, this._m);
            cmpRef.instance.name = 'dynamic';
            this.vc.insert(cmpRef.hostView);
        })
    }
}
```
# String replace with input params

``` javascript
amendTheSentence = s => s
    .replace(/(.)(?=[A-Z])/g, '$1 ')
    .toLowerCase()
```
