# RxJS - Convert `Observable<A[]>` to `Observable<B[]>`
```java
import {from} from 'rxjs';
import {map, concatMap, toArray} from 'rxjs/operators';

observable                               // Observable<A[]>
    .pipe(
        concatMap(array => from(array)), // Observable<A>
        map(a => toB(a)),                // Observable<B>
        toArray()                        // Observable<B[]>
    )
```
