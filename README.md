# Fireangularblog 
## By James Dumitru


# Files needed to make it run, build and deploy doesn't work. 

`npm ci && npm run build` doesn't work as intended as it brings an error



```typescript
//firebase.app.module.d.ts
import { InjectionToken, ModuleWithProviders, NgZone, Version } from '@angular/core';

import firebase from 'firebase/app';

import * as ɵngcc0 from '@angular/core';

export interface FirebaseOptions { 

[key: string]: any;

}

export interface FirebaseAppConfig {

[key: string]: any;

}

export declare const FIREBASE_OPTIONS: InjectionToken<FirebaseOptions>;

export declare const FIREBASE_APP_NAME: InjectionToken<string | FirebaseAppConfig>;

export declare class FirebaseApp implements Partial<firebase.app.App> {

  name: string;

  options: {};

  analytics: () => firebase.analytics.Analytics;

  auth: () => firebase.auth.Auth;

  database: (databaseURL?: string) => firebase.database.Database;

  messaging: () => firebase.messaging.Messaging;

  performance: () => firebase.performance.Performance;

  storage: (storageBucket?: string) => firebase.storage.Storage;

  delete: () => Promise<void>;

  firestore: () => firebase.firestore.Firestore;

  functions: (region?: string) => firebase.functions.Functions;

  remoteConfig: () => firebase.remoteConfig.RemoteConfig;

}

export declare const VERSION: Version;

export declare function ɵfirebaseAppFactory(options: FirebaseOptions, zone: NgZone, nameOrConfig?: string | FirebaseAppConfig | null): FirebaseApp;

export declare const ɵlogAuthEmulatorError: () => void;

export declare function ɵfetchInstance<T>(cacheKey: any, moduleName: string, app: FirebaseApp, fn: () => T, args: any[]): T;

export declare class AngularFireModule {

  static initializeApp(options: FirebaseOptions, nameOrConfig?: string | FirebaseAppConfig): ModuleWithProviders<AngularFireModule>;

  constructor(platformId: Object);

  static ɵmod: ɵngcc0.ɵɵNgModuleDefWithMeta<AngularFireModule, never, never, never>;

  static ɵinj: ɵngcc0.ɵɵInjectorDef<AngularFireModule>;

}



//# sourceMappingURL=firebase.app.module.d.ts.map
```

```typescript
//interfaces.d.ts
import { Observable } from 'rxjs';
import firebase from 'firebase/app';
export declare type FirebaseOperation = string | firebase.database.Reference | firebase.database.DataSnapshot;
export interface AngularFireList<T> {
    query: DatabaseQuery;
    valueChanges(events?: ChildEvent[], options?: {}): Observable<T[]>;
    valueChanges<K extends string>(events?: ChildEvent[], options?: {
        idField: K;
    }): Observable<(T & {
        [T in K]?: string;
    })[]>;
    snapshotChanges(events?: ChildEvent[]): Observable<SnapshotAction<T>[]>;
    stateChanges(events?: ChildEvent[]): Observable<SnapshotAction<T>>;
    auditTrail(events?: ChildEvent[]): Observable<SnapshotAction<T>[]>;
    update(item: FirebaseOperation, data: Partial<T>): Promise<void>;
    set(item: FirebaseOperation, data: T): Promise<void>;
    push(data: T): firebase.database.ThenableReference;
    remove(item?: FirebaseOperation): Promise<void>;
}
export interface AngularFireObject<T> {
    query: DatabaseQuery;
    valueChanges(): Observable<T | null>;
    snapshotChanges(): Observable<SnapshotAction<T>>;
    update(data: Partial<T>): Promise<void>;
    set(data: T): Promise<void>;
    remove(): Promise<void>;
}
export interface FirebaseOperationCases {
    stringCase: () => Promise<void>;
    firebaseCase?: () => Promise<void>;
    snapshotCase?: () => Promise<void>;
    unwrappedSnapshotCase?: () => Promise<void>;
}
export declare type QueryFn = (ref: DatabaseReference) => DatabaseQuery;
export declare type ChildEvent = 'child_added' | 'child_removed' | 'child_changed' | 'child_moved';
export declare type ListenEvent = 'value' | ChildEvent;
export interface Action<T> {
    type: ListenEvent;
    payload: T;
}
export interface AngularFireAction<T> extends Action<T> {
    prevKey: string | null | undefined;
    key: string | null;
}
export declare type SnapshotAction<T> = AngularFireAction<DatabaseSnapshot<T>>;
export declare type Primitive = number | string | boolean;
export interface DatabaseSnapshotExists<T> extends firebase.database.DataSnapshot {
    exists(): true;
    val(): T;
    forEach(action: (a: DatabaseSnapshot<T>) => boolean): boolean;
}
export interface DatabaseSnapshotDoesNotExist<T> extends firebase.database.DataSnapshot {
    exists(): false;
    val(): null;
    forEach(action: (a: DatabaseSnapshot<T>) => boolean): boolean;
}
export declare type DatabaseSnapshot<T> = DatabaseSnapshotExists<T> | DatabaseSnapshotDoesNotExist<T>;
export declare type DatabaseReference = firebase.database.Reference;
export declare type DatabaseQuery = firebase.database.Query;
export declare type DataSnapshot = firebase.database.DataSnapshot;
export declare type QueryReference = DatabaseReference | DatabaseQuery;
export declare type PathReference = QueryReference | string;

```

``` typescript
//database.d.ts
import { InjectionToken, NgZone } from '@angular/core';
import { AngularFireList, AngularFireObject, PathReference, QueryFn } from './interfaces';
import { FirebaseAppConfig, FirebaseOptions, ɵAngularFireSchedulers } from '@angular/fire';
import { Observable } from 'rxjs';
import 'firebase/database';
import firebase from 'firebase/app';
import * as ɵngcc0 from '@angular/core';
export declare const URL: InjectionToken<string>;
declare type UseEmulatorArguments = [string, number];
export declare const USE_EMULATOR: InjectionToken<UseEmulatorArguments>;
export declare class AngularFireDatabase {
    readonly database: firebase.database.Database;
    readonly schedulers: ɵAngularFireSchedulers;
    readonly keepUnstableUntilFirst: <T>(obs$: Observable<T>) => Observable<T>;
    constructor(options: FirebaseOptions, nameOrConfig: string | FirebaseAppConfig | null | undefined, databaseURL: string | null, platformId: Object, zone: NgZone, _useEmulator: any, // tuple isn't working here
    useAuthEmulator: any);
    list<T>(pathOrRef: PathReference, queryFn?: QueryFn): AngularFireList<T>;
    object<T>(pathOrRef: PathReference): AngularFireObject<T>;
    createPushId(): string;
    static ɵfac: ɵngcc0.ɵɵFactoryDef<AngularFireDatabase, [null, { optional: true; }, { optional: true; }, null, null, { optional: true; }, { optional: true; }]>;
}
export { PathReference, DatabaseSnapshot, ChildEvent, ListenEvent, QueryFn, AngularFireList, AngularFireObject, AngularFireAction, Action, SnapshotAction } from './interfaces';

//# sourceMappingURL=database.d.ts.map

```



This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 11.0.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

If you need the node modules, make sure to Run `npm install` and if need be, change error of deprecated @angularfire2 to @angular/fire. 
I had to deal with a deprecated import for firebase. 

- If you are running into node modules errors, as I've seen dealing with `firebase.app.module.d.ts` or `interfaces.d.ts` or `database.d.ts` you must Run `ng add @angular/fire` correctly instead of what npm does by default and uninstall firebase and run that command. The imports are wacky but it should fix the issue.

IF you see firebase/app as an issue, I assure you it's not and is something vs code won't pickup. 

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.
