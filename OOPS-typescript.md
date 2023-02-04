---
marp: true
theme: uncover
class:
  - lead
---

![](https://miro.medium.com/max/500/1*-dmHYcAiphpWe6m0pcd-AA.png)

### Using Typescript & Angular

---

## Core Concepts

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

---

## Encapsulation

```typescript
class Player {
  private _health = 100;
  get health() {
    return this._health;
  }
}
const player = new Player();
console.log(player.health);
// 100
console.log(player._health);
// compile error
```

---

## Abstraction

```typescript
class Player {
  private _health = 100;
  get health() {
    return this._health;
  }
  setHealth(hpChange: number) {
    this._health = this._health + hpChange;
  }
}
const player = new Player();
player.setHealth(-10);
console.log(player.health);
// 90
```

---

## Inheritance

```typescript
class TrialPlayer extends Player {
  private timeRemaining = 0.1 * 60 * 1000; // minutes
  constructor() {
    super();
    console.log("timer");
    setTimeout(() => {
      console.log("End");
    }, this.timeRemaining);
  }
}
const trialPlayer = new TrialPlayer();
```

---

## Polymorphism

```typescript
class GodModePlayer extends Player {
  setHealth(hpChange: number) {
    // Invincible
  }
}
const godModePlayer = new GodModePlayer();
console.log(godModePlayer.health); // 100
godModePlayer.setHealth(-20);
console.log(godModePlayer.health); // 100
```

---

## Advanced Concepts

1. Decorators
2. Dependency Injection
3. Mixins
4. Rethinking Types

---

## Decorators

```typescript
@Component({
  selector: "an-angular-component",
})
export class AppComponent {
  // ...
}
```

```typescript
@Injectable({
  providedIn: "root",
})
export class UserService {
  // ...
}
```

---

## Dependency Injection

```typescript
@Component({
  selector: "an-angular-component",
})
export class AppComponent {
  constructor(private userService: UserService) {}
  // ...
}
```

---

## Mixins

```typescript
function WithDestroy(Base) {
  return class extends Base implements OnDestroy {
    destroy$ = new Subject();

    ngOnDestroy() {
      super.ngOnDestroy();
      this.destroy();
    }
  };
}
```

---

## Rethinking Types

TypeScript's understanding of a type is actually quite different from C# or Java's.

- No Runtime type check.

```c#
// C#
static void LogType<T>() {
  Console.WriteLine(typeof(T).Name);
}
```

---

## Union & Intersection types

```typescript
// Union
const userID: string | number;
// Intersection
interface User {
  name: string;
}
interface Employee {
  salary: number;
}
let employee: User & Employee = {
  name: "Shan",
  salary: 10000,
};
```

---

## Erased Structural Types.

```typescript
interface Pointlike {
  x: number;
  y: number;
}
interface Named {
  name: string;
}

function logPoint(point: Pointlike) {
  console.log("x = " + point.x + ", y = " + point.y);
}

function logName(x: Named) {
  console.log("Hello, " + x.name);
}

const obj = {
  x: 0,
  y: 0,
  name: "Origin",
};

logPoint(obj);
logName(obj);
```

---

## Identical Types

```typescript
class Car {
  drive() {
    // hit the gas
  }
}
class Golfer {
  drive() {
    // hit the ball far
  }
}
// No error?
let w: Car = new Golfer();
```

---

## Type Assertion

![bg left](https://img.devrant.com/devrant/rant/r_3015646_HZCi4.jpg)

```typescript
const myCanvas =
document.getElementById("main_canvas")
 as HTMLCanvasElement;

const x = "hello" as number;
// Conversion of type 'string' to type 'number' may be a mistake
// because neither type sufficiently overlaps with the other.

```

<style>
    :root {
    --color-background: #0f0;
    --color-foreground: #fff;
    --color-background-code: #00000088;
    --color-highlight: #f00;
    --color-dimmed: #f00;
  }
  section{
    background-image: url('https://images.unsplash.com/photo-1620641788421-7a1c342ea42e?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2748&q=80');
  }
</style>
