# Angular - Display all errors of reactive form
(Only ment for debug purposes)

In `x.component.ts`:
```typescript
@Component(/*...*/)
export class XComponent{
    Object = Object;

    form = new FormGroup(/*...*/);
}
```

In `x.component.html`:
```angular2html
<ul>
    <li *ngFor="let controlName of Object.keys(form.controls)">
        {{controlName}}: {{ form.get(controlName).errors | json }}
    </li>
</ul>
```