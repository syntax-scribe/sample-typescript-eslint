[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `member-ordering.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/member-ordering.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RunTests` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../src/rules/member-ordering` |
| `Options` | `../../src/rules/member-ordering` |
| `rule` | `../../src/rules/member-ordering` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |
| `grouped` | `RunTests<MessageIds, Options>` | const | `{
  valid: [
    `
// no accessibility === public
interface Foo {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  new ();
  G();
  H();
  I();
  J();
  K();
  L();
}
    `,
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  J();
  K();
  D: string;
  E: string;
  F: string;
  new ();
  G();
  H();
  [Z: string]: any;
  B: string;
  C: string;
  I();
  L();
}
      `,
      options: [{ default: 'never' }],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  new ();
  G();
  H();
  I();
  J();
  K();
  L();
}
      `,
      options: [{ default: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
interface X {
  (): void;
  a: unknown;
  b(): void;
}
      `,
      options: [{ default: ['call-signature', 'field', 'method'] }],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  J();
  K();
  D: string;
  [Z: string]: any;
  E: string;
  F: string;
  new ();
  G();
  B: string;
  C: string;
  H();
  I();
  L();
}
      `,
      options: [{ interfaces: 'never' }],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  [Z: string]: any;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
}
      `,
      options: [
        { interfaces: ['signature', 'method', 'constructor', 'field'] },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  [Z: string]: any;
}
      `,
      options: [
        {
          default: ['signature', 'field', 'constructor', 'method'],
          interfaces: ['method', 'constructor', 'field', 'signature'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  G();
  H();
  I();
  new ();
  [Z: string]: any;
  D: string;
  E: string;
  F: string;
  G?: string;
  J();
  K();
  L();
  A: string;
  B: string;
  C: string;
}
      `,
      options: [
        {
          default: [
            'private-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  G();
  H();
  I();
  J();
  K();
  L();
  [Z: string]: any;
  D: string;
  E: string;
  F: string;
  new ();
  A: string;
  B: string;
  C: string;
}
      `,
      options: [
        {
          default: ['method', 'public-constructor', 'protected-static-field'],
        },
      ],
    },
    `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  new ();
  G();
  H();
  I();
  J();
  K();
  L();
};
    `,
    {
      code: `
// no accessibility === public
type Foo = {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  [Z: string]: any;
  G();
  H();
  I();
  J();
  K();
  L();
};
      `,
      options: [{ default: 'never' }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
};
      `,
      options: [{ default: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  new ();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
};
      `,
      options: [{ default: ['field', 'method'] }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  G();
  H();
  [Z: string]: any;
  K();
  L();
  A: string;
  B: string;
  I();
  J();
  C: string;
  D: string;
  E: string;
  F: string;
};
      `,
      options: [{ typeLiterals: 'never' }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  G();
  H();
  I();
  J();
  K();
  L();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  [Z: string]: any;
};
      `,
      options: [{ typeLiterals: ['method', 'field', 'signature'] }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  G();
  H();
  I();
  J();
  K();
  L();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  [Z: string]: any;
};
      `,
      options: [
        { typeLiterals: ['method', 'constructor', 'field', 'signature'] },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  G();
  H();
  I();
  J();
  K();
  L();
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  [Z: string]: any;
};
      `,
      options: [
        {
          default: ['signature', 'field', 'constructor', 'method'],
          typeLiterals: ['method', 'constructor', 'field', 'signature'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  D: string;
  E: string;
  F: string;
  A: string;
  B: string;
  C: string;
  G();
  H();
  I();
  J();
  K();
  L();
};
      `,
      options: [
        {
          default: [
            'public-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
          typeLiterals: ['signature', 'field', 'method'],
        },
      ],
    },
    `
class Foo {
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  constructor() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
}
    `,
    {
      code: `
class Foo {
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  constructor() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
}
      `,
      options: [{ default: 'never' }],
    },
    {
      code: `
class Foo {
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  constructor() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
}
      `,
      options: [{ default: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
class Foo {
  [Z: string]: any;
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
}
      `,
      options: [{ default: ['field', 'method'] }],
    },
    {
      code: `
class Foo {
  public static G() {}
  protected K() {}
  private L() {}
  private static I() {}
  public J() {}
  public D: string = '';
  [Z: string]: any;
  protected static H() {}
  public static A: string;
  protected static B: string = '';
  constructor() {}
  private static C: string = '';
  protected E: string = '';
  private F: string = '';
}
      `,
      options: [{ classes: 'never' }],
    },
    {
      code: `
class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  constructor() {}
}
      `,
      options: [{ classes: ['method', 'field'] }],
    },
    {
      code: `
class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  [Z: string]: any;
}
      `,
      options: [{ classes: ['method', 'constructor', 'field', 'signature'] }],
    },
    {
      code: `
class Foo {
  private required: boolean;
  private typeChecker: (data: any) => boolean;
  constructor(validator: (data: any) => boolean) {
    this.typeChecker = validator;
  }
  check(data: any): boolean {
    return this.typeChecker(data);
  }
}
      `,
      options: [{ classes: ['field', 'constructor', 'method'] }],
    },
    {
      code: `
class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  [Z: string]: any;
}
      `,
      options: [
        {
          classes: ['method', 'constructor', 'field', 'signature'],
          default: ['signature', 'field', 'constructor', 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  public J() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  protected K() {}
  private L() {}
  [Z: string]: any;
  constructor() {}
  public D: string = '';
  public static A: string;
  private static C: string = '';
  private F: string = '';
  static #M: string = '';
  #N: string = '';
  protected static B: string = '';
  protected E: string = '';
}
      `,
      options: [
        {
          classes: [
            'public-method',
            'signature',
            'constructor',
            'public-field',
            'private-field',
            '#private-field',
            'protected-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public static G() {}
  private static I() {}
  protected static H() {}
  public J() {}
  private L() {}
  protected K() {}
  [Z: string]: any;
  constructor() {}
  public D: string = '';
  public static A: string;
  protected static B: string = '';
  protected E: string = '';
  private static C: string = '';
  private F: string = '';
  #M: string = '';
}
      `,
      options: [
        {
          classes: [
            'public-static-method',
            'static-method',
            'public-instance-method',
            'instance-method',
            'signature',
            'constructor',
            'public-field',
            'protected-field',
            'private-field',
            '#private-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public J() {}
  public static G() {}
  public D: string = '';
  public static A: string = '';
  constructor() {}
  protected K() {}
  private L() {}
  #P() {}
  protected static H() {}
  private static I() {}
  static #O() {}
  protected static B: string = '';
  private static C: string = '';
  static #N: string = '';
  protected E: string = '';
  private F: string = '';
  #M: string = '';
  [Z: string]: any;
}
      `,
      options: [
        {
          default: [
            'public-method',
            'public-field',
            'constructor',
            'method',
            'field',
            'signature',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public J() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  protected K() {}
  private L() {}
  #L() {}
  constructor() {}
  [Z: string]: any;
  public static A: string;
  private F: string = '';
  #F: string = '';
  protected static B: string = '';
  public D: string = '';
  private static C: string = '';
  static #C: string = '';
  protected E: string = '';
}
      `,
      options: [
        {
          classes: [
            'public-method',
            'protected-static-method',
            '#private-static-method',
            'protected-instance-method',
            'private-instance-method',
            '#private-instance-method',
            'constructor',
            'signature',
            'field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  protected static B: string = '';
  public static G() {}
  public J() {}
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
  [Z: string]: any;
}
      `,
      options: [
        {
          classes: ['private-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  private static I() {}
  static #H() {}
  static #B: string = '';
  public static G() {}
  public J() {}
  #K() {}
  private static C: string = '';
  private F: string = '';
  #E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
  [Z: string]: any;
}
      `,
      options: [
        {
          classes: ['private-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
  [Z: string]: any;
}
      `,
      options: [
        {
          default: ['public-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
  [Z: string]: any;
}
      `,
      options: [
        {
          classes: ['public-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  [Z: string]: any;
  public D: string = '';
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  private constructor() {}
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
}
      `,
      options: [
        {
          classes: [
            'public-instance-field',
            'private-constructor',
            'protected-instance-method',
          ],
          default: [
            'public-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public constructor() {}
  public D: string = '';
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  [Z: string]: any;
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
}
      `,
      options: [
        {
          classes: [
            'public-instance-field',
            'private-constructor',
            'protected-instance-method',
          ],
          default: [
            'public-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
        },
      ],
    },
    `
const foo = class Foo {
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
};
    `,
    {
      code: `
const foo = class Foo {
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static I() {}
  public J() {}
  private F: string = '';
  [Z: string]: any;
  public static G() {}
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  protected static H() {}
  protected K() {}
  private L() {}
};
      `,
      options: [{ default: 'never' }],
    },
    {
      code: `
const foo = class Foo {
  [Z: string]: any;
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
};
      `,
      options: [{ default: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
const foo = class Foo {
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  [Z: string]: any;
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
};
      `,
      options: [{ default: ['field', 'method'] }],
    },
    {
      code: `
const foo = class Foo {
  private L() {}
  protected static H() {}
  constructor() {}
  private static I() {}
  public J() {}
  private static C: string = '';
  [Z: string]: any;
  public D: string = '';
  protected K() {}
  public static G() {}
  public static A: string;
  protected static B: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      options: [{ classExpressions: 'never' }],
    },
    {
      code: `
const foo = class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
  [Z: string]: any;
};
      `,
      options: [{ classExpressions: ['method', 'field'] }],
    },
    {
      code: `
const foo = class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  [Z: string]: any;
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      options: [
        { classExpressions: ['method', 'signature', 'constructor', 'field'] },
      ],
    },
    {
      code: `
const foo = class Foo {
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  [Z: string]: any;
  constructor() {}
  public static A: string;
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      options: [
        {
          classExpressions: ['method', 'signature', 'constructor', 'field'],
          default: ['field', 'constructor', 'method'],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  [Z: string]: any;
  private L() {}
  private static I() {}
  protected static H() {}
  protected static B: string = '';
  public static G() {}
  public J() {}
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
};
      `,
      options: [
        {
          classExpressions: [
            'private-instance-method',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  [Z: string]: any;
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
};
      `,
      options: [
        {
          default: ['public-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  [Z: string]: any;
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
};
      `,
      options: [
        {
          classExpressions: [
            'public-instance-method',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  public D: string = '';
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  [Z: string]: any;
  private constructor() {}
  protected static B: string = '';
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
};
      `,
      options: [
        {
          classes: [
            'public-instance-method',
            'protected-constructor',
            'protected-static-method',
          ],
          classExpressions: [
            'public-instance-field',
            'private-constructor',
            'protected-instance-method',
          ],
          default: [
            'public-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  public constructor() {}
  public D: string = '';
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  public J() {}
  protected static B: string = '';
  protected K() {}
  [Z: string]: any;
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
};
      `,
      options: [
        {
          classes: [
            'public-instance-method',
            'protected-constructor',
            'protected-static-method',
          ],
          classExpressions: [
            'public-instance-field',
            'private-constructor',
            'protected-instance-method',
          ],
          default: [
            'public-instance-method',
            'public-constructor',
            'protected-static-field',
          ],
        },
      ],
    },
    `
class Foo {
  [Z: string]: any;
  A: string;
  constructor() {}
  J() {}
  K = () => {};
}
    `,
    {
      code: `
class Foo {
  J() {}
  K = () => {};
  constructor() {}
  A: string;
  [Z: string]: any;
}
      `,
      options: [{ default: ['method', 'constructor', 'field', 'signature'] }],
    },
    {
      code: `
class Foo {
  J() {}
  K = () => {};
  constructor() {}
  [Z: string]: any;
  A: string;
  L: () => {};
}
      `,
      options: [{ default: ['method', 'constructor', 'signature', 'field'] }],
    },
    {
      code: `
class Foo {
  static {}
  m() {}
  f = 1;
}
      `,
      options: [{ default: ['static-initialization', 'method', 'field'] }],
    },
    {
      code: `
class Foo {
  m() {}
  f = 1;
  static {}
}
      `,
      options: [{ default: ['method', 'field', 'static-initialization'] }],
    },
    {
      code: `
class Foo {
  f = 1;
  static {}
  m() {}
}
      `,
      options: [{ default: ['field', 'static-initialization', 'method'] }],
    },
    `
interface Foo {
  [Z: string]: any;
  A: string;
  K: () => {};
  J();
}
    `,
    {
      code: `
interface Foo {
  [Z: string]: any;
  J();
  K: () => {};
  A: string;
}
      `,
      options: [{ default: ['signature', 'method', 'constructor', 'field'] }],
    },
    `
type Foo = {
  [Z: string]: any;
  A: string;
  K: () => {};
  J();
};
    `,
    {
      code: `
type Foo = {
  J();
  [Z: string]: any;
  K: () => {};
  A: string;
};
      `,
      options: [{ default: ['method', 'constructor', 'signature', 'field'] }],
    },
    {
      code: `
abstract class Foo {
  B: string;
  abstract A: () => {};
}
      `,
    },
    {
      code: `
interface Foo {
  [A: string]: number;
  B: string;
}
      `,
    },
    {
      code: `
abstract class Foo {
  [Z: string]: any;
  private static C: string;
  B: string;
  private D: string;
  protected static F(): {};
  public E(): {};
  public abstract A(): void;
  protected abstract G(): void;
}
      `,
    },
    {
      code: `
abstract class Foo {
  protected typeChecker: (data: any) => boolean;
  public abstract required: boolean;
  abstract verify(): void;
}
      `,
      options: [{ classes: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
class Foo {
  @Dec() B: string;
  @Dec() A: string;
  constructor() {}
  D: string;
  C: string;
  E(): void;
  F(): void;
}
      `,
      options: [{ default: ['decorated-field', 'field'] }],
    },
    {
      code: `
class Foo {
  A: string;
  B: string;
  @Dec() private C: string;
  private D: string;
}
      `,
      options: [
        {
          default: ['public-field', 'private-decorated-field', 'private-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  constructor() {}
  @Dec() public A(): void {}
  @Dec() private B: string;
  private C(): void;
  private D: string;
}
      `,
      options: [
        {
          default: [
            'decorated-method',
            'private-decorated-field',
            'private-method',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  @Dec() private A(): void {}
  @Dec() private B: string;
  constructor() {}
  private C(): void;
  private D: string;
}
      `,
      options: [
        {
          default: [
            'private-decorated-method',
            'private-decorated-field',
            'constructor',
            'private-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public A: string;
  @Dec() private B: string;
}
      `,
      options: [
        {
          classes: ['public-instance-field', 'private-decorated-field'],
          default: ['private-decorated-field', 'public-instance-field'],
        },
      ],
    },
    // class + ignore decorator
    {
      code: `
class Foo {
  public A(): string;
  @Dec() public B(): string {}
  public C(): string;

  d: string;
}
      `,
      options: [
        {
          default: ['public-method', 'field'],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  constructor() {}
  get B() {}
  set B() {}
  get C() {}
  set C() {}
  D(): void;
}
      `,
      options: [
        {
          default: ['field', 'constructor', ['get', 'set'], 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  constructor() {}
  B(): void;
}
      `,
      options: [
        {
          default: ['field', 'constructor', [], 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  constructor() {}
  @Dec() private B: string;
  private C(): void;
  set D() {}
  E(): void;
}
      `,
      options: [
        {
          default: [
            'public-field',
            'constructor',
            ['private-decorated-field', 'public-set', 'private-method'],
            'public-method',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  constructor() {}
  get B() {}
  get C() {}
  set B() {}
  set C() {}
  D(): void;
}
      `,
      options: [
        {
          default: ['field', 'constructor', ['get'], ['set'], 'method'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  imPublic() {}
  #imPrivate() {}
}
      `,
      name: 'with private identifier',
      options: [
        {
          default: {
            memberTypes: ['public-method', '#private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  private imPrivate() {}
  #imPrivate() {}
}
      `,
      name: 'private and #private member order',
      options: [
        {
          default: {
            memberTypes: ['private-method', '#private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  #imPrivate() {}
  private imPrivate() {}
}
      `,
      name: '#private and private member order',
      options: [
        {
          default: {
            memberTypes: ['#private-method', 'private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  [A: string]: any;
  [a: string]: any;
  static C: boolean;
  static d: boolean;
  b: any;
  B: any;
  get e(): string {}
  get E(): string {}
  private imPrivate() {}
  private ImPrivate() {}
}
      `,
      name: 'default member types with alphabetically-case-insensitive order',
      options: [
        {
          default: {
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
class Foo {
  readonly B: string;
  readonly A: string;
  constructor() {}
  D: string;
  C: string;
  E(): void;
  F(): void;
}
      `,
      options: [{ default: ['readonly-field', 'field'] }],
    },
    {
      code: `
class Foo {
  A: string;
  B: string;
  private readonly C: string;
  private D: string;
}
      `,
      options: [
        {
          default: ['public-field', 'private-readonly-field', 'private-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private readonly A: string;
  constructor() {}
  private B: string;
}
      `,
      options: [
        {
          default: ['private-readonly-field', 'constructor', 'private-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  public A: string;
  private readonly B: string;
}
      `,
      options: [
        {
          classes: ['public-instance-field', 'private-readonly-field'],
          default: ['private-readonly-field', 'public-instance-field'],
        },
      ],
    },
    // class + ignore readonly
    {
      code: `
class Foo {
  public A(): string;
  public B(): string;
  public C(): string;

  d: string;
  readonly e: string;
  f: string;
}
      `,
      options: [
        {
          default: ['public-method', 'field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private readonly A: string;
  readonly B: string;
  C: string;
  constructor() {}
  @Dec() private D: string;
  private E(): void;
  set F() {}
  G(): void;
}
      `,
      options: [
        {
          default: [
            'readonly-field',
            'public-field',
            'constructor',
            ['private-decorated-field', 'public-set', 'private-method'],
            'public-method',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  public static readonly SA: string;
  protected static readonly SB: string;
  private static readonly SC: string;
  static readonly #SD: string;

  public readonly IA: string;
  protected readonly IB: string;
  private readonly IC: string;
  readonly #ID: string;

  public abstract readonly AA: string;
  protected abstract readonly AB: string;

  @Dec public readonly DA: string;
  @Dec protected readonly DB: string;
  @Dec private readonly DC: string;
}
      `,
      options: [
        {
          default: [
            'public-static-readonly-field',
            'protected-static-readonly-field',
            'private-static-readonly-field',
            '#private-static-readonly-field',

            'static-readonly-field',

            'public-instance-readonly-field',
            'protected-instance-readonly-field',
            'private-instance-readonly-field',
            '#private-instance-readonly-field',

            'instance-readonly-field',

            'public-readonly-field',
            'protected-readonly-field',
            'private-readonly-field',
            '#private-readonly-field',

            'readonly-field',

            'public-abstract-readonly-field',
            'protected-abstract-readonly-field',

            'abstract-readonly-field',

            'public-decorated-readonly-field',
            'protected-decorated-readonly-field',
            'private-decorated-readonly-field',
            'decorated-readonly-field',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly DA: string;
  @Dec protected readonly DB: string;
  @Dec private readonly DC: string;

  public static readonly SA: string;
  protected static readonly SB: string;
  private static readonly SC: string;
  static readonly #SD: string;

  public readonly IA: string;
  protected readonly IB: string;
  private readonly IC: string;
  readonly #ID: string;

  public abstract readonly AA: string;
  protected abstract readonly AB: string;
}
      `,
      options: [
        {
          default: [
            'decorated-readonly-field',
            'static-readonly-field',
            'instance-readonly-field',
            'abstract-readonly-field',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly DA: string;
  @Dec protected readonly DB: string;
  @Dec private readonly DC: string;

  public static readonly SA: string;
  public readonly IA: string;
  public abstract readonly AA: string;

  protected static readonly SB: string;
  protected readonly IB: string;
  protected abstract readonly AB: string;

  private static readonly SC: string;
  private readonly IC: string;

  static readonly #SD: string;
  readonly #ID: string;
}
      `,
      options: [
        {
          default: [
            'decorated-readonly-field',
            'public-readonly-field',
            'protected-readonly-field',
            'private-readonly-field',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly DA: string;
  @Dec protected readonly DB: string;
  @Dec private readonly DC: string;

  public static readonly SA: string;
  public readonly IA: string;
  static readonly #SD: string;
  readonly #ID: string;

  protected static readonly SB: string;
  protected readonly IB: string;

  private static readonly SC: string;
  private readonly IC: string;

  public abstract readonly AA: string;
  protected abstract readonly AB: string;
}
      `,
      options: [
        {
          default: [
            'decorated-readonly-field',
            ['public-readonly-field', 'readonly-field'],
            'protected-readonly-field',
            'private-readonly-field',
            'abstract-readonly-field',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly A: string;
  @Dec public B: string;

  public readonly C: string;
  public static readonly D: string;
  public E: string;
  public static F: string;

  static readonly #G: string;
  readonly #H: string;
  static #I: string;
  #J: string;
}
      `,
      options: [
        {
          default: [
            ['decorated-field', 'decorated-readonly-field'],
            ['field', 'readonly-field'],
            ['#private-field', '#private-readonly-field'],
          ],
        },
      ],
    },
    {
      code: `
interface Foo {
  readonly A: string;
  readonly B: string;

  C: string;
  D: string;
}
      `,
      options: [
        {
          default: ['readonly-field', 'field'],
        },
      ],
    },
    {
      code: `
interface Foo {
  readonly [i: string]: string;
  readonly A: string;

  [i: number]: string;
  B: string;
}
      `,
      options: [
        {
          default: [
            'readonly-signature',
            'readonly-field',
            'signature',
            'field',
          ],
        },
      ],
    },
    {
      code: `
interface Foo {
  readonly [i: string]: string;
  [i: number]: string;

  readonly A: string;
  B: string;
}
      `,
      options: [
        {
          default: [
            'readonly-signature',
            'signature',
            'readonly-field',
            'field',
          ],
        },
      ],
    },
    {
      code: `
interface Foo {
  readonly A: string;
  B: string;

  [i: number]: string;
  readonly [i: string]: string;
}
      `,
      options: [
        {
          default: ['readonly-field', 'field', 'signature'],
        },
      ],
    },
    // https://github.com/typescript-eslint/typescript-eslint/issues/6812
    {
      code: `
class Foo {
  #bar: string;

  get bar(): string {
    return this.#bar;
  }

  set bar(value: string) {
    this.#bar = value;
  }
}
      `,
      options: [
        {
          default: {
            memberTypes: [['get', 'set']],
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  [A: string]: any;
  [B: string]: any;
  [a: string]: any;
  [b: string]: any;
  static C: boolean;
  static d: boolean;
  get E(): string {}
  get e(): string {}
  private ImPrivate() {}
  private imPrivate() {}
}
      `,
      name: 'default member types with alphabetically order',
      options: [
        {
          default: {
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  B: string;
  [Z: string]: any;
  c();
  new ();
  r();
}
      `,
      name: 'alphabetically order without member types',
      options: [{ default: { memberTypes: 'never', order: 'alphabetically' } }],
    },
    {
      code: `
class Foo {
  #bar: string;

  get bar(): string {
    return this.#bar;
  }

  set bar(value: string) {
    this.#bar = value;
  }
}
      `,
      options: [
        {
          default: {
            memberTypes: [['get', 'set']],
            order: 'natural',
          },
        },
      ],
    },
    {
      code: `
class Foo {
  accessor bar;

  baz() {}
}
      `,
      options: [
        {
          default: ['accessor', 'method'],
        },
      ],
    },
    {
      code: `
interface Foo {
  get x(): number;
  y(): void;
}
      `,
      options: [
        {
          default: ['get', 'method'],
        },
      ],
    },
    {
      code: `
interface Foo {
  y(): void;
  get x(): number;
}
      `,
      options: [
        {
          default: ['method', 'get'],
        },
      ],
    },
    {
      code: `
class Foo {
  public baz(): void;
  @Decorator() public baz() {}

  @Decorator() bar() {}
}
      `,
      options: [
        {
          default: ['public-decorated-method', 'public-instance-method'],
        },
      ],
    },
    {
      code: `
class Foo {
  public bar(): void;
  @Decorator() bar() {}

  public baz(): void;
  @Decorator() public baz() {}
}
      `,
      options: [
        {
          default: ['public-instance-method', 'public-decorated-method'],
        },
      ],
    },
    {
      code: `
class Foo {
  @Decorator() bar() {}

  public baz(): void;
  @Decorator() public baz() {}
}
      `,
      options: [
        {
          default: ['public-instance-method', 'public-decorated-method'],
        },
      ],
    },
  ],
  invalid: [
    {
      code: `
// no accessibility === public
interface Foo {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'method',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
interface X {
  a: unknown;
  (): void;
  b(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'call',
            rank: 'field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['call-signature', 'field', 'method'] }],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  [Z: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'field',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['signature', 'method', 'constructor', 'field'] }],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  [Z: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'field',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        { interfaces: ['method', 'signature', 'constructor', 'field'] },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  [Z: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'field',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['field', 'method', 'constructor', 'signature'],
          interfaces: ['method', 'signature', 'constructor', 'field'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
interface Foo {
  [Z: string]: any;
  new ();
  A: string;
  G();
  B: string;
  H();
  C: string;
  I();
  D: string;
  J();
  E: string;
  K();
  F: string;
  L();
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'method',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'method',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'method',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'E',
            rank: 'method',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'method',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          interfaces: ['signature', 'constructor', 'field', 'method'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'method',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  [Z: string]: any;
  new ();
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'field',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'constructor', 'signature', 'field'] }],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  [Z: string]: any;
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'signature',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'signature',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'signature',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'signature',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'signature',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'signature',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'signature',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        { typeLiterals: ['method', 'constructor', 'signature', 'field'] },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  A: string;
  B: string;
  C: string;
  D: string;
  E: string;
  F: string;
  G();
  H();
  I();
  J();
  K();
  L();
  new ();
  [Z: string]: any;
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'new',
            rank: 'field',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['field', 'method', 'constructor', 'signature'],
          typeLiterals: ['signature', 'method', 'constructor', 'field'],
        },
      ],
    },
    {
      code: `
// no accessibility === public
type Foo = {
  new ();
  [Z: string]: any;
  A: string;
  G();
  B: string;
  H();
  C: string;
  I();
  D: string;
  J();
  E: string;
  K();
  F: string;
  L();
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'method',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'method',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'method',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'E',
            rank: 'method',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'method',
          },
          line: 16,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          typeLiterals: ['constructor', 'signature', 'field', 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  [Z: string]: any;
  public static A: string = '';
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  constructor() {}
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'public instance method',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'public instance method',
          },
          line: 18,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'public instance method',
          },
          line: 19,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'public instance method',
          },
          line: 20,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
class Foo {
  constructor() {}
  public static A: string = '';
  protected static B: string = '';
  private static C: string = '';
  static #C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  #F: string = '';
  public J() {}
  protected K() {}
  private L() {}
  #L() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  static #I() {}
  [Z: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'constructor',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'constructor',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'constructor',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'constructor',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'constructor',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'E',
            rank: 'constructor',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'constructor',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'constructor',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['field', 'constructor', 'method', 'signature'] }],
    },
    {
      code: `
class Foo {
  constructor() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  public static G() {}
  public static A: string;
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'method',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['field', 'method'] }],
    },
    {
      code: `
class Foo {
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  public static A: string;
  public static G() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'field'] }],
    },
    {
      code: `
class Foo {
  public static G() {}
  protected static H() {}
  protected static B: string = '';
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  public static A: string;
  constructor() {}
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ classes: ['method', 'constructor', 'field'] }],
    },
    {
      code: `
class Foo {
  public static A: string;
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  constructor() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: ['method', 'constructor', 'field'],
          default: ['field', 'constructor', 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  public J() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  protected K() {}
  constructor() {}
  public D: string = '';
  private static C: string = '';
  public static A: string;
  private static C: string = '';
  protected static B: string = '';
  private F: string = '';
  protected static B: string = '';
  protected E: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'private field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'protected field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: [
            'public-method',
            'constructor',
            'public-field',
            'private-field',
            'protected-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public static G() {}
  private static I() {}
  public J() {}
  protected static H() {}
  private L() {}
  protected K() {}
  public D: string = '';
  constructor() {}
  public static A: string;
  protected static B: string = '';
  protected E: string = '';
  private static C: string = '';
  private F: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'public instance method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'public field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: [
            'public-static-method',
            'static-method',
            'public-instance-method',
            'instance-method',
            'constructor',
            'public-field',
            'protected-field',
            'private-field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public J() {}
  public static G() {}
  public D: string = '';
  public static A: string = '';
  private L() {}
  constructor() {}
  protected K() {}
  protected static H() {}
  private static I() {}
  protected static B: string = '';
  private static C: string = '';
  protected E: string = '';
  private F: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'method',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'public-method',
            'public-field',
            'constructor',
            'method',
            'field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  public J() {}
  private static I() {}
  public static G() {}
  protected static H() {}
  protected K() {}
  private L() {}
  constructor() {}
  public static A: string;
  private F: string = '';
  protected static B: string = '';
  public D: string = '';
  private static C: string = '';
  protected E: string = '';
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'private static method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'private static method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: [
            'public-method',
            'protected-static-method',
            'private-static-method',
            'protected-instance-method',
            'private-instance-method',
            'constructor',
            'field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  private static I() {}
  protected static H() {}
  protected static B: string = '';
  public static G() {}
  public J() {}
  protected K() {}
  private static C: string = '';
  private L() {}
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'protected static field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: ['private-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  protected static B: string = '';
  public J() {}
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'protected static field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['public-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
const foo = class Foo {
  public static A: string = '';
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
  public J() {}
  protected K() {}
  private L() {}
  public static G() {}
  protected static H() {}
  private static I() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'public instance method',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'public instance method',
          },
          line: 14,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'public instance method',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
const foo = class {
  [Z: string]: any;
  constructor() {}
  public static A: string = '';
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  public J() {}
  protected K() {}
  private L() {}
  public static G() {}
  protected static H() {}
  private static I() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'constructor',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'constructor',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'constructor',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'constructor',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'E',
            rank: 'constructor',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'constructor',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['signature', 'field', 'constructor', 'method'] }],
    },
    {
      code: `
const foo = class {
  constructor() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  [Z: string]: any;
  public static G() {}
  public static A: string;
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'method',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['field', 'method'] }],
    },
    {
      code: `
const foo = class {
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  public static A: string;
  public static G() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
  constructor() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'field'] }],
    },
    {
      code: `
const foo = class {
  public static G() {}
  protected static H() {}
  protected static B: string = '';
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  public static A: string;
  constructor() {}
  [Z: string]: any;
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'field',
          },
          line: 11,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ classExpressions: ['method', 'constructor', 'field'] }],
    },
    {
      code: `
const foo = class {
  public static A: string;
  public static G() {}
  protected static H() {}
  private static I() {}
  public J() {}
  protected K() {}
  private L() {}
  constructor() {}
  protected static B: string = '';
  private static C: string = '';
  public D: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classExpressions: ['method', 'constructor', 'field'],
          default: ['field', 'constructor', 'method'],
        },
      ],
    },
    {
      code: `
const foo = class {
  private L() {}
  public J() {}
  public static G() {}
  protected static H() {}
  private static I() {}
  protected K() {}
  constructor() {}
  public D: string = '';
  private static C: string = '';
  public static A: string;
  private static C: string = '';
  protected static B: string = '';
  private F: string = '';
  protected static B: string = '';
  protected E: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'private field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'protected field',
          },
          line: 15,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classExpressions: [
            'public-method',
            'constructor',
            'public-field',
            'private-field',
            'protected-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class {
  public static G() {}
  private static I() {}
  public J() {}
  protected static H() {}
  private L() {}
  protected K() {}
  public D: string = '';
  constructor() {}
  public static A: string;
  protected static B: string = '';
  protected E: string = '';
  private static C: string = '';
  private F: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'public instance method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'public field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classExpressions: [
            'public-static-method',
            'static-method',
            'public-instance-method',
            'instance-method',
            'constructor',
            'public-field',
            'protected-field',
            'private-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class {
  public J() {}
  public static G() {}
  public D: string = '';
  public static A: string = '';
  private L() {}
  constructor() {}
  protected K() {}
  protected static H() {}
  private static I() {}
  protected static B: string = '';
  private static C: string = '';
  protected E: string = '';
  private F: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'method',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'public-method',
            'public-field',
            'constructor',
            'method',
            'field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class {
  public J() {}
  private static I() {}
  public static G() {}
  protected static H() {}
  protected K() {}
  private L() {}
  constructor() {}
  public static A: string;
  private F: string = '';
  protected static B: string = '';
  public D: string = '';
  private static C: string = '';
  protected E: string = '';
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'G',
            rank: 'private static method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'H',
            rank: 'private static method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classExpressions: [
            'public-method',
            'protected-static-method',
            'private-static-method',
            'protected-instance-method',
            'private-instance-method',
            'constructor',
            'field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class {
  private static I() {}
  protected static H() {}
  protected static B: string = '';
  public static G() {}
  public J() {}
  protected K() {}
  private static C: string = '';
  private L() {}
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'L',
            rank: 'protected static field',
          },
          line: 10,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classExpressions: [
            'private-instance-method',
            'protected-static-field',
          ],
        },
      ],
    },
    {
      code: `
const foo = class {
  private L() {}
  private static I() {}
  protected static H() {}
  public static G() {}
  protected static B: string = '';
  public J() {}
  protected K() {}
  private static C: string = '';
  private F: string = '';
  protected E: string = '';
  public static A: string;
  public D: string = '';
  constructor() {}
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'protected static field',
          },
          line: 8,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['public-instance-method', 'protected-static-field'],
        },
      ],
    },
    {
      code: `
class Foo {
  K = () => {};
  A: string;
  constructor() {}
  [Z: string]: any;
  J() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'public instance method',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'public instance method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'Z',
            rank: 'public instance method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
class Foo {
  J() {}
  constructor() {}
  K = () => {};
  A: string;
  [Z: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'constructor',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'constructor', 'field', 'signature'] }],
    },
    {
      code: `
class Foo {
  J() {}
  constructor() {}
  K = () => {};
  L: () => {};
  A: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'K',
            rank: 'constructor',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'constructor', 'field'] }],
    },
    {
      code: `
interface Foo {
  K: () => {};
  J();
  A: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
type Foo = {
  K: () => {};
  J();
  A: string;
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
type Foo = {
  A: string;
  K: () => {};
  J();
};
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'constructor', 'field'] }],
    },
    {
      code: `
abstract class Foo {
  abstract A(): void;
  B: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'public abstract method',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
abstract class Foo {
  abstract A: () => {};
  B: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'public abstract field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
abstract class Foo {
  abstract A: () => {};
  B: string;
  public C() {}
  private D() {}
  abstract E() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'public abstract field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
    },
    {
      code: `
class Foo {
  C: number;
  [A: string]: number;
  public static D() {}
  static [B: string]: number;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'signature',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'field',
            'method',
            'public-static-method',
            'private-static-method',
            'signature',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  abstract B: string;
  abstract A(): void;
  public C() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'constructor', 'field'] }],
    },
    {
      code: `
// no accessibility === public
class Foo {
  B: string;
  @Dec() A: string = '';
  C: string = '';
  constructor() {}
  D() {}
  E() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['decorated-field', 'field'] }],
    },
    {
      code: `
class Foo {
  A() {}

  @Decorator()
  B() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'method',
          },
          line: 5, // Symbol starts at the line with decorator
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['decorated-method', 'method'] }],
    },
    {
      code: `
class Foo {
  @Decorator() C() {}
  A() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'decorated method',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['public-method', 'decorated-method'] }],
    },
    {
      code: `
class Foo {
  A(): void;
  B(): void;
  private C() {}
  constructor() {}
  @Dec() private D() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'private method',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          classes: ['public-method', 'decorated-method', 'private-method'],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  get B() {}
  constructor() {}
  set B() {}
  get C() {}
  set C() {}
  D(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'get, set',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['field', 'constructor', ['get', 'set'], 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  private C() {}
  constructor() {}
  @Dec() private B: string;
  set D() {}
  E(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'private decorated field, public set, private method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'public-field',
            'constructor',
            ['private-decorated-field', 'public-set', 'private-method'],
            'public-method',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  A: string;
  constructor() {}
  get B() {}
  set B() {}
  get C() {}
  set C() {}
  D(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'set',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['field', 'constructor', 'get', ['set'], 'method'],
        },
      ],
    },
    {
      code: `
class Foo {
  static {}
  m() {}
  f = 1;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'm',
            rank: 'static initialization',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'f',
            rank: 'static initialization',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['method', 'field', 'static-initialization'] }],
    },
    {
      code: `
class Foo {
  m() {}
  f = 1;
  static {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'static block',
            rank: 'method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['static-initialization', 'method', 'field'] }],
    },
    {
      code: `
class Foo {
  f = 1;
  static {}
  m() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'static block',
            rank: 'field',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['static-initialization', 'field', 'method'] }],
    },
    {
      code: `
class Foo {
  static {}
  f = 1;
  m() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'f',
            rank: 'static initialization',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['field', 'static-initialization', 'method'] }],
    },
    {
      code: `
class Foo {
  private mp() {}
  static {}
  public m() {}
  @dec
  md() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'static block',
            rank: 'method',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'md',
            rank: 'method',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        { default: ['decorated-method', 'static-initialization', 'method'] },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  #imPrivate() {}
  imPublic() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'imPublic',
            rank: '#private method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      name: 'with private identifier',
      options: [
        {
          default: {
            memberTypes: ['public-method', '#private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  #imPrivate() {}
  private imPrivate() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'imPrivate',
            rank: '#private method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      name: 'private and #private member order',
      options: [
        {
          default: {
            memberTypes: ['private-method', '#private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  static C: boolean;
  [B: string]: any;
  private A() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'public static field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      name: 'default member types with alphabetically order',
      options: [
        {
          default: {
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  static C: boolean;
  [B: string]: any;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            beforeMember: 'C',
            member: 'B',
          },
          line: 5,
          messageId: 'incorrectOrder',
        },
      ],
      name: 'alphabetically order without member types',
      options: [{ default: { memberTypes: 'never', order: 'alphabetically' } }],
    },
    {
      code: `
// no accessibility === public
class Foo {
  private imPrivate() {}
  #imPrivate() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'imPrivate',
            rank: 'private method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      name: '#private and private member order',
      options: [
        {
          default: {
            memberTypes: ['#private-method', 'private-method'],
            order: 'alphabetically-case-insensitive',
          },
        },
      ],
    },
    {
      code: `
// no accessibility === public
class Foo {
  B: string;
  readonly A: string = '';
  C: string = '';
  constructor() {}
  D() {}
  E() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'A',
            rank: 'field',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [{ default: ['readonly-field', 'field'] }],
    },
    {
      code: `
class Foo {
  A: string;
  private C() {}
  constructor() {}
  private readonly B: string;
  set D() {}
  E(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'constructor',
            rank: 'public set, private method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'public field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'private-readonly-field',
            'public-field',
            'constructor',
            ['public-set', 'private-method'],
            'public-method',
          ],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly A: string;
  public readonly B: string;
  public static readonly C: string;
  static readonly #D: string;
  readonly #E: string;

  @Dec public F: string;
  public G: string;
  public static H: string;
  static readonly #I: string;
  readonly #J: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'F',
            rank: 'readonly field',
          },
          line: 9,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'I',
            rank: 'field',
          },
          line: 12,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'J',
            rank: 'field',
          },
          line: 13,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['decorated-field', 'readonly-field', 'field'],
        },
      ],
    },
    {
      code: `
abstract class Foo {
  @Dec public readonly DA: string;
  @Dec protected readonly DB: string;
  @Dec private readonly DC: string;

  public static readonly SA: string;
  protected static readonly SB: string;
  private static readonly SC: string;
  static readonly #SD: string;

  public readonly IA: string;
  protected readonly IB: string;
  private readonly IC: string;
  readonly #ID: string;

  public abstract readonly AA: string;
  protected abstract readonly AB: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'AA',
            rank: 'static readonly field',
          },
          line: 17,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'AB',
            rank: 'static readonly field',
          },
          line: 18,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'decorated-readonly-field',
            'abstract-readonly-field',
            'static-readonly-field',
            'instance-readonly-field',
          ],
        },
      ],
    },
    {
      code: `
interface Foo {
  readonly A: string;
  readonly B: string;

  C: string;
  D: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'C',
            rank: 'readonly field',
          },
          line: 6,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'D',
            rank: 'readonly field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['field', 'readonly-field'],
        },
      ],
    },
    {
      code: `
interface Foo {
  [i: number]: string;
  readonly [i: string]: string;

  A: string;
  readonly B: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'i',
            rank: 'signature',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
        {
          column: 3,
          data: {
            name: 'B',
            rank: 'field',
          },
          line: 7,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: [
            'readonly-signature',
            'signature',
            'readonly-field',
            'field',
          ],
        },
      ],
    },
    {
      code: `
class Foo {
  accessor bar;

  baz() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'baz',
            rank: 'accessor',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['method', 'accessor'],
        },
      ],
    },
    {
      code: `
interface Foo {
  y(): void;
  get x(): number;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'x',
            rank: 'method',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['get', 'method'],
        },
      ],
    },
    {
      code: `
interface Foo {
  get x(): number;
  y(): void;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'y',
            rank: 'get',
          },
          line: 4,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        {
          default: ['method', 'get'],
        },
      ],
    },
    {
      code: `
class Foo {
  static foo() {}
  foo(): void;
  foo() {}
}
      `,
      errors: [
        {
          column: 3,
          data: {
            name: 'foo',
            rank: 'public static method',
          },
          line: 5,
          messageId: 'incorrectGroupOrder',
        },
      ],
      options: [
        { default: ['public-instance-method', 'public-static-method'] },
      ],
    },
  ],
}` | ✗ |


---