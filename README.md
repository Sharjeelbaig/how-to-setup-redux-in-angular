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
in `name-something/name-someting.module.ts`
```ts
import StoreModule.forFeature('name-something', name-somethingReducer) in the ng module located .
```
## step 8

```bash
ng generate component name-something
```

## step 9
in name-something.component.ts:
```ts
import { Store } from '@ngrx/store';
```
```ts
import { someFunction, anotherFunction } from '../state/name-something.actions';
```
```ts
import { NameSomethingState } from '../state/name-something.state';
```
```ts
export class NameSomethingComponent {
  variable$: Observable<number>;

  constructor(private store: Store<NameSomethingState>) {
    this.variable$ = this.store.select((state) => state.name-something.variable);
  }

  someFunction() {
    this.store.dispatch(someFunction());
  }

  anotherFunction() {
    this.store.dispatch(anotherFunction());
  }
}
```

## step 7
use the html code like this:

```html
<button (click)="someFunction()">Increment</button>
```
