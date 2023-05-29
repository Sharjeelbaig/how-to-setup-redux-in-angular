# how-to-setup-redux-in-angular
## step 1
```bash
npm install @ngrx/store @ngrx/store-devtools
```
## step 2
```bash
ng generate module name-something --routing
```
## step 3
inside that `name-something` module, add new directory known as `state`
## step 4
inside `state`, create three files:
- `name-something.actions.ts`: Defines the actions for the counter.
- `name-something.reducer.ts`: Implements the reducer function for the counter.
- `name-something.state.ts`  : Defines the interface for the counter state.
## step 5

<table>
  <tr>
    <th>name-something.actions.ts</th>
    <th>name-something.reducer.ts</th>
    <th>name-something.state.ts</th>
  </tr>
  <tr>
    <td>
      <pre>
import { createAction } from '@ngrx/store';
export const someFunction = createAction('somethig');
export const anotherFunction = createAction('something');
      </pre>
    </td>
    <td>
      <pre>
import { createReducer, on } from '@ngrx/store';
import { someFunction, anotherFunction } from './name-something.actions';

export interface NameSomethingState {
  variable: any;
}

export const initialState: NameSomethingState = {
  variable: 'any value',
};

export const nameSomethingReducer = createReducer(
  initialState,
  on(someFunction, (state) => ({ variable: 'some function is executed' })),
  on(anotherFunction, (state) => ({ variable: 'another function is created' })),
);
      </pre>
    </td>
    <td>
      <pre>
export interface NameSomethingState {
  variable: any;
}
      </pre>
    </td>
  </tr>
</table>

#### make sure to replace that something with your module name

## step 6

in `name-something.module.ts`, 

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { StoreModule } from '@ngrx/store';
import { nameSometingReducer } from './state/name-something.reducer';
```

## step 7
in in the import of ng module located in `name-something/name-someting.module.ts`
```ts
StoreModule.forFeature('name-something', name-somethingReducer) 
```
## step 8

```bash
ng generate component name-something
```

## step 9
in name-something.component.ts or the component you want to use redux in (the following code is assuming that you have generated the component of the same name as module):
```ts
import { Component } from '@angular/core';
import { Store, select } from '@ngrx/store';
import { Observable } from 'rxjs';
import { NameSomethingState } from './state/name-something.state';
import { someFunction, anotherFunction } from './state/name-something.actions';

@Component({
  selector: 'app-counter',
  templateUrl: './name-something.component.html',
  styleUrls: ['./name-something.component.css']
})
export class NameSomethingComponent {
  variable$: Observable<number>;

  constructor(private store: Store<NameSomethingState>) {
    this.variable$ = new Observable<number>(observer => {
      this.store.pipe(select(state => state.name-something)).subscribe(variable => {
        observer.next(variable);
      });
    });
  }

  someFunction() {
    this.store.dispatch(someFunction());
  }

  anotherFunction() {
    this.store.dispatch(anotherFunction());
  }
}
```

## step 10
use the html code like this:

```html
<button (click)="someFunction()">Increment</button>
```
