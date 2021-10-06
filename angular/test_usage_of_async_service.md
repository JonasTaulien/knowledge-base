# Angular - Test usage of async service
## Problem
When a component makes calls to an async method of service in its `ngOnInit` like:

```ts
ngOnInit(): void {
    this.service
        .fetchFromServer()
        .subscribe(data => updateView(data))
}
```

If you then just simply create a spy like this in your test:

```ts
serviceMock = jasmine.createSpyObj<Service>('Service', ['fetchFromServer']);
serviceMock.fetchFromServer.and.returnValue(of(data))
```

You will not test the async nature of the real implementation of `fetchFromServer`.
That means, if you have an error because you are not able to handle some network delay, 
you will not detect that error

## Solution
1. Add an `delay(0)` to the observable to schedule it for the next tick
2. Wrap the test in `fakeAsync(() => { test })`
3. Call `tick(0)` followed by `componentFixture.detectChanges()`

Complete example:

```ts
describe('MyComponent', () => {
    let componentFixture = ComponentFixture<MyComponent>;
    let serviceMock: SpyObj<Service>;

    beforeEach(async () => {
        const someData = ...;
        serviceMock = jasmine.createSpyObj<Service>('Service', ['fetchFromServer']);
        serviceMock.fetchFromServer.and.returnValue(
            of(someData)
                // Mock network delay
                .pipe(delay(0))
        )

        await TestBed.configureTestingModule({
                         declarations: [MyComponent],
                         providers: [{provide: Service, useValue: serviceMock}]
                     })
                     .compileComponents()
                     .then(() => {
                         componentFixture = TestBed.createComponent(MyComponent);
                     })
    });
    
    it('should fetch and show data', fakeAsync(() => {
        // Execute ngOnInit of MyComponent
        componentFixture.detectChanges();
        // Let the Observable complete by ticking the time
        tick(0);
        // Detect changes that were made in the ngOnInit as a reaction of the completion of the Observable
        componentFixture.detectChanges();
        
        // TOOO: Assert data is correctly presented
    }));
});
```

## Additional information:
* https://angular.io/guide/testing-components-scenarios#async-test-with-fakeasync
