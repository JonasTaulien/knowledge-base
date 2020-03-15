# Angular - Display all errors of reactive form
## Problem
`formGroup.errors` only includes errors that were added to the form itself, not those errors added to any form control inside of it.


## Solution
(Should only be used for debugging purposes)

In `x.component.ts`:
```typescript
@Component(/*...*/)
export class XComponent{
    Object = Object;

    form = new FormGroup(/*...*/);
}
```

In `x.component.html`:
```html
<ul>
    <li *ngFor="let controlName of Object.keys(form.controls)">
        {{controlName}}: {{ form.get(controlName).errors | json }}
    </li>
</ul>
```
