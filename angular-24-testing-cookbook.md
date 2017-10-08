# Angular 2 Testing

## Setting Up Angular with Jasmine

Create the suite

```typescript
import "babel-polyfill";
import "reflect-metadata";
import "zone.js";
import "zone.js/dist/long-stack-trace-zone";
import "zone.js/dist/async-test";
import "zone.js/dist/fake-async-test";
import "zone.js/dist/sync-test";
import "zone.js/dist/proxy";
import "zone.js/dist/jasmine-patch";


require('./TestBedInit.js');

var requireTest = require.context('.', true, /\.test\.(js|ts)$/);
requireTest.keys().forEach(requireTest);
```

Before the test suite runs \(TestBedInit.js\):

```typescript
import {TestBed} from "@angular/core/testing";
import {BrowserDynamicTestingModule, platformBrowserDynamicTesting} from "@angular/platform-browser-dynamic/testing";

TestBed.initTestEnvironment( BrowserDynamicTestingModule, platformBrowserDynamicTesting() );
```

## Component Test Example

The following tests a Form input and submission, and mocks a service that triggers an action based on the submit:

```typescript
import {TestBed, ComponentFixture, ComponentFixtureAutoDetect} from "@angular/core/testing";
import {By} from "@angular/platform-browser";
import {Observable} from "rxjs";
import {ReactiveFormsModule} from "@angular/forms";

describe("Component: SomeForm", () => {
  let component: SomeForm;
  let fixture: ComponentFixture<SomeForm>;

  beforeEach(() => {
    let SomeServiceSpy = {
      addModel: jasmine.createSpy('createModel').and.returnValue(Observable.of(SomeService)),
    };

    TestBed.configureTestingModule({
      declarations: [SomeForm],
      providers: [
        { provide: SomeService, useValue: SomeServiceSpy},
        { provide: ComponentFixtureAutoDetect, useValue: true}
      ],
      imports: [
        ReactiveFormsModule,
      ],
    });

    fixture = TestBed.createComponent(SomeForm);
    component = fixture.componentInstance;
  });

  describe("create a model", () => {
    it("calls createModel in SomeService", () => {
      // In the 'input' text field, set it to 'Hello'
      const inputCtrl = fixture.debugElement.query(By.css("input")).nativeElement;
      inputCtrl.value= "Hello";

      // Dispatch the event for the 'input' text
      inputCtrl.dispatchEvent(new Event("input"));

      // Important! make sure Angular is aware of the form changes.
      fixture.detectChanges();


      fixture.debugElement.query(By.css("form")).triggerEventHandler("submit", null);
      fixture.detectChanges();

      const someServiceSpy = fixture.debugElement.injector.get(SomeService);
      expect(someServiceSpy.createModel).toHaveBeenCalledWith("Hello");
    });
  });
});
```



