---
marp: true
theme: uncover
class:
  - lead
---

![bg right:60% 90%](https://images.ctfassets.net/aq13lwl6616q/nI6ON3VtJH67WzcnmUV0H/3c49f45a74d3e0989c279976d22b5937/advanced_angular_interview_questions.png?w=655&fm=webp)

# Angular Best Practices

---

## Follow [Angular Style Guide](https://angular.io/guide/styleguide)

- **kebab-case** for component selectors, routes, filenames, and CSS classes.
- **lowerCamelCase** for properties and methods.
- **UpperCamelCase** for class names, interfaces, types and enums.

---

## Use a consistent folder structure.

```bash
src/
  app/
    services
    models
    pipes
    module1-name/
      component1-name/
        ts, html, css, spec.ts
      component2-name/
    module2-name/
      components
      services
      models...

```

---

## Break Down Components

---

## Lifecycle Hooks

[Change Detection Ref](https://angular.io/api/core/ChangeDetectorRef)

![bg right:60% 70%](https://miro.medium.com/v2/resize:fit:733/1*By7qWOomvpnCKxwX2ucmmw.png)

---

## Unsubscribe from Observables

```typescript
  ngOnInit() {
    this.subscription = this.authService.user$.subscribe(user => {
      this.user = user;
    });
  }
  ngOnDestroy() {
    this.subscription.unsubscribe();
  }
```

---

## Don't use jQuery

Use ViewChild instead.

```typescript
@ViewChild("myDiv") myDiv: ElementRef;
```

---

## Use TrackBy with ngFor

```html
<div *ngFor="let item of items; trackBy: trackByItem">{{ item.id }}</div>
```

```typescript
trackByItem(index, item) {
  return item.id;
}
```

---

## Use Angular CLI

```bash
ng new
ng serve
ng add
ng update
ng generate
ng lint
ng test
ng build
```

---

## Use Angular lint

```bash
ng lint
```

---

## Lazy Load Modules

```typescript
ng generate module customers --route customers --module app.module
```

---

## Use Angular Router

```typescript
const routes: Routes = [
  { path: "customers", component: CustomersComponent },
  { path: "orders", component: OrdersComponent },
  { path: "", redirectTo: "/customers", pathMatch: "full" },
  { path: "**", component: PageNotFoundComponent },
];
```

Getting Route Parameters

```typescript
constructor(private route: ActivatedRoute) {
  this.route.params.subscribe(params => {
    this.id = params.id;
  });
}
```

---

## Use Angular Reactive Forms

```typescript
import { FormBuilder, FormGroup, Validators } from "@angular/forms";
constructor(private fb: FormBuilder) {
  this.form = this.fb.group({
    name: ["", Validators.required],
    email: ["", [Validators.required, Validators.email]],
  });
}
```

```html
<form [formGroup]="form" (ngSubmit)="onSubmit()">
  <input formControlName="name" />
  <input formControlName="email" />
  <button type="submit">Submit</button>
</form>
```

---

## Use Angular Services

- For Model and Business Logic, sharing data between components.
- For HTTP Requests.

```typescript
UserService {
  user$: Observable<User>;
  getUser() {
    if (!this.user$.value) {
      this.http.get<User[]>("/api/users").subscribe(user => {
        this.user$.next(user);
      });
    }
  }
}
```

---

## Use Angular Pipes

- Use Angular Pipes to transform, format, filter data in the template.
- Refrain from calling methods in the template.

---

## Use Interceptors for HTTP Requests

```typescript
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService) {}
  intercept(req: HttpRequest<any>, next: HttpHandler) {
    const authToken = this.authService.getAuthToken();
    const authReq = req.clone({
      headers: req.headers.set("Authorization", authToken),
    });
    return next.handle(authReq);
  }
}
```

---

## Use Guards for Route Protection

```typescript
@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService) {}
  canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot) {
    return this.authService.isLoggedIn();
  }
}
```

---

## Use Resolvers for Data Fetching

```typescript
@Injectable({ providedIn: "root" })
export class UserResolver implements Resolve<User> {
  constructor(private userService: UserService) {}
  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot) {
    return this.userService.getUser();
  }
}
```

<style style="display:none">
:root {
    --color-background: linear-gradient(45deg, #000, #335);
    --color-foreground: #fff;
    --color-background-code: #222222ee;
    --color-highlight: #f00;
    --color-dimmed: #f00;
  }
  section{
    /* background-image: url('https://t4.ftcdn.net/jpg/04/89/68/23/360_F_489682374_ckc0OVyT6Av0NGcuYbwBSCxy62blF4CQ.jpg');
    background-size: cover; */
  }
  a{
    color:#fff;
    border-bottom: 1px dotted #fff;
  }
</style>
