# RxJava - Convert `Single<List<A>>` to `Single<List<B>>`
```java
single                                                          // Single<List<A>>
    .flatMapObservable(list -> Observable.fromIterable(list))   // Observable<A>
    .map(a -> toB(a))                                           // Observable<B>
    .toList()                                                   // Single<List<B>>
```
