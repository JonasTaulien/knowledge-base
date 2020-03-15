# To do - Things to add
* CSS: Real viewport height on ios-safari 
    * in typescript

        ```typescript
        export class AppComponent implements OnInit {
            ngOnInit(): void {
                this.setRealViewPortHeightProperty();
                
                fromEvent(window, 'resize')
                    .pipe(
                        debounceTime(100)
                    )
                    .subscribe(() => this.setRealViewPortHeightProperty());
        
            }
        
            setRealViewPortHeightProperty() {
                const vh = window.innerHeight * 0.01;
                document.documentElement.style.setProperty('--real-vh', `${vh}px`);
            }
        }
        ```
    * then in css: `calc(var(--real-vh, 1vh) * 100)`)
* Angular ViewChild/ContentChild & ViewChildren/ContentChildren
    * ContentChildren also selects the Host-Element if it matches the selector
    * Project ng-content through two levels and then selecting an element voa ContentChildren does not work
* Angular: Place content children separately using `<ng-template>` and a `TemplateMarkerDirective`
* Angular ChangeDetectorRef & ExpressionChangedAfterEvaluatedException
* Angular ControlValueAccessor
* Angular ControlValueAccessor having async validation
* Angular wrap ControlValueAccessor
* Angular height-adjusting textarea
* Angular unit testing
* Angular module-setup
* Angular guards (with parameters)
* Angular reactive forms
* Angular: load config before starting application
* Angular generating uid for custom input components
* Css styling input=range
* JS: luxon
* JS: rxjs
* Angular @angular/cdk/overlay
* HTML: Responsive SVG using viewBox and preserveAspectRatio
* JWT in vertx and angular
* Angular: Carousel
* JS flatMap array
* Java Dockerfile
* Vertx: OpenAPI3RouterFactory
* Java - Google Maps
* Vertx Json: Java-times (JavaTimeModule()) and SerializationFeature.WRITE_DATES_AS_TIMESTAMPS
* Java: Password hashing with argon2
* Java: hikari data source for jooq
* jooq: insert
* jooq: fetch simple
* jooq: fetch 1 to n
* jooq: learnings from big hirecat queries
* jooq: writing bindings for POINT
* IntelliJ: Learnings from 'https://github.com/JonasTaulienSolutions/idea-plugin-context-free-grammar'
* css: flexbox
* css: BEM
* css: stack items using `grid`
* detect IE11 / Edge
* learnings from 'https://github.com/JonasTaulienSolutions/playground' (then delete)
* Learnings from articles from https://www.nickkolenda.com
* opening localhost web-application on ios-device (with squidman or via cable)
* scss: `--var: $var` not working. Must be `--var: #{$var}`
* Shopify Dev
* Docker setup for https on apache
* Docker setup for https on vert.x application
* .htaccess
    * non-www to www
    * http -> https
    * using gzip
* local https with mkcert
* using flyway with jooq
* learnings from FM-Project
