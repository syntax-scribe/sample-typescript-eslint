[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-template-expression.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unnecessary-template-expression.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/no-unnecessary-template-expression` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |
| `invalidCases` | `readonly [{ readonly code: "`${1}`;"; readonly errors: readonly [{ readonly column: 2; readonly endColumn: 6; readonly line: 1; readonly messageId: "noUnnecessaryTemplateExpression"; }]; readonly output: "`1`;"; }, ... 99 more ..., { ...; }]` | const | `[
  {
    code: '`${1}`;',
    errors: [
      {
        column: 2,
        endColumn: 6,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`1`;',
  },
  {
    code: '`${1n}`;',
    errors: [
      {
        column: 2,
        endColumn: 7,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`1`;',
  },
  {
    code: '`${0o25}`;',
    errors: [
      {
        column: 2,
        endColumn: 9,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`21`;',
  },
  {
    code: '`${0b1010} ${0b1111}`;',
    errors: [
      {
        column: 2,
        endColumn: 11,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        column: 12,
        endColumn: 21,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`10 15`;',
  },
  {
    code: '`${0x25}`;',
    errors: [
      {
        column: 2,
        endColumn: 9,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`37`;',
  },
  {
    code: '`${/a/}`;',
    errors: [
      {
        column: 2,
        endColumn: 8,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`/a/`;',
  },
  {
    code: '`${/a/gim}`;',
    errors: [
      {
        column: 2,
        endColumn: 11,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`/a/gim`;',
  },

  {
    code: noFormat`\`\${    1    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`1`;',
  },

  {
    code: noFormat`\`\${    'a'    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `'a';`,
  },

  {
    code: noFormat`\`\${    "a"    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `"a";`,
  },

  {
    code: noFormat`\`\${    'a' + 'b'    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `'a' + 'b';`,
  },

  {
    code: '`${true}`;',
    errors: [
      {
        column: 2,
        endColumn: 9,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`true`;',
  },

  {
    code: noFormat`\`\${    true    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`true`;',
  },

  {
    code: '`${null}`;',
    errors: [
      {
        column: 2,
        endColumn: 9,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`null`;',
  },

  {
    code: noFormat`\`\${    null    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`null`;',
  },

  {
    code: '`${undefined}`;',
    errors: [
      {
        column: 2,
        endColumn: 14,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`undefined`;',
  },

  {
    code: noFormat`\`\${    undefined    }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`undefined`;',
  },

  {
    code: '`${Infinity}`;',
    errors: [
      {
        column: 2,
        endColumn: 13,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`Infinity`;',
  },

  {
    code: '`${NaN}`;',
    errors: [
      {
        column: 2,
        endColumn: 8,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`NaN`;',
  },

  {
    code: "`${'a'} ${'b'}`;",
    errors: [
      {
        column: 2,
        endColumn: 8,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        column: 9,
        endColumn: 15,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`a b`;',
  },

  {
    code: noFormat`\`\${   'a'   } \${   'b'   }\`;`,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`a b`;',
  },

  {
    code: "`use${'less'}`;",
    errors: [
      {
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`useless`;',
  },

  {
    code: '`use${`less`}`;',
    errors: [
      {
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`useless`;',
  },
  {
    code: noFormat`
\`u\${
  // hopefully this comment is not needed.
  'se'

}\${
  \`le\${  \`ss\`  }\`
}\`;
      `,
    errors: [
      {
        column: 2,
        endColumn: 2,
        endLine: 8,
        line: 6,
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        column: 6,
        endColumn: 17,
        endLine: 7,
        line: 7,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: [
      `
\`u\${
  // hopefully this comment is not needed.
  'se'

}le\${  \`ss\`  }\`;
      `,
      `
\`u\${
  // hopefully this comment is not needed.
  'se'

}less\`;
      `,
    ],
  },
  {
    code: noFormat`
\`use\${
  \`less\`
}\`;
      `,
    errors: [
      {
        column: 5,
        endColumn: 2,
        endLine: 4,
        line: 2,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `
\`useless\`;
      `,
  },

  {
    code: "`${'1 + 1 ='} ${2}`;",
    errors: [
      {
        column: 2,
        endColumn: 14,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        column: 15,
        endColumn: 19,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`1 + 1 = 2`;',
  },

  {
    code: "`${'a'} ${true}`;",
    errors: [
      {
        column: 2,
        endColumn: 8,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        column: 9,
        endColumn: 16,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`a true`;',
  },

  {
    code: "`${String(Symbol.for('test'))}`;",
    errors: [
      {
        column: 2,
        endColumn: 31,
        line: 1,
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: "String(Symbol.for('test'));",
  },

  {
    code: "`${'`'}`;",
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: "'`';",
  },

  {
    code: "`back${'`'}tick`;",
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`back\\`tick`;',
  },

  {
    code: "`dollar${'${`this is test`}'}sign`;",
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`dollar\\${\\`this is test\\`}sign`;',
  },

  {
    code: '`complex${\'`${"`${test}`"}`\'}case`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`complex\\`\\${"\\`\\${test}\\`"}\\`case`;',
  },

  {
    code: "`some ${'\\\\${test}'} string`;",
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some \\\\\\${test} string`;',
  },

  {
    code: "`some ${'\\\\`'} string`;",
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some \\\\\\` string`;',
  },

  {
    code: '`some ${/`/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\`/ string`;',
  },
  {
    code: '`some ${/\\`/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\`/ string`;',
  },
  {
    code: '`some ${/\\\\`/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\\\\\`/ string`;',
  },
  {
    code: '`some ${/\\\\\\`/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\\\\\\\\\`/ string`;',
  },
  {
    code: '`some ${/${}/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\${}/ string`;',
  },
  {
    code: '`some ${/$ {}/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /$ {}/ string`;',
  },
  {
    code: '`some ${/\\\\/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\\\/ string`;',
  },
  {
    code: '`some ${/\\\\\\b/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\\\\\\\b/ string`;',
  },
  {
    code: '`some ${/\\\\\\\\/} string`;',
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: '`some /\\\\\\\\\\\\\\\\/ string`;',
  },
  {
    code: "` ${''} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '`  `;',
  },
  {
    code: noFormat`\` \${""} \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '`  `;',
  },
  {
    code: '` ${``} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '`  `;',
  },
  {
    code: noFormat`\` \${'\\\`'} \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\` `;',
  },
  {
    code: "` ${'\\\\`'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\` `;',
  },
  {
    code: "` ${'$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: noFormat`\` \${'\\$'}{} \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: "` ${'\\\\$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\${} `;',
  },
  {
    code: "` ${'\\\\$ '}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\$ {} `;',
  },
  {
    code: noFormat`\` \${'\\\\\\$'}{} \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\${} `;',
  },
  {
    code: "` \\\\${'\\\\$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\\\\\${} `;',
  },
  {
    code: "` $${'{$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${\\${} `;',
  },
  {
    code: "` $${'${$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` $\\${\\${} `;',
  },
  {
    code: "` ${'foo$'}{} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` foo\\${} `;',
  },
  {
    code: '` ${`$`} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` $ `;',
  },
  {
    code: '` ${`$`}{} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: '` ${`$`} {} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` $ {} `;',
  },
  {
    code: '` ${`$`}${undefined}{} `;',
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` $${undefined}{} `;', '` $undefined{} `;'],
  },
  {
    code: '` ${`foo$`}{} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` foo\\${} `;',
  },
  {
    code: "` ${'$'}${''}{} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\$${''}{} `;", '` \\${} `;'],
  },
  {
    code: "` ${'$'}${``}{} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` \\$${``}{} `;', '` \\${} `;'],
  },
  {
    code: "` ${'foo$'}${''}${``}{} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` foo\\$${''}{} `;", '` foo\\${} `;'],
  },
  {
    code: "` $${'{}'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: "` $${undefined}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` $undefined${'{}'} `;", '` $undefined{} `;'],
  },
  {
    code: "` $${''}${undefined}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` $${undefined}{} `;', '` $undefined{} `;'],
  },
  {
    code: "` \\$${'{}'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: "` $${'foo'}${'{'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` $foo${'{'} `;", '` $foo{ `;'],
  },
  {
    code: "` $${'{ foo'}${'{'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\${ foo${'{'} `;", '` \\${ foo{ `;'],
  },
  {
    code: "` \\\\$${'{}'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\${} `;',
  },
  {
    code: "` \\\\\\$${'{}'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\\\\\${} `;',
  },
  {
    code: "` foo$${'{}'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` foo\\${} `;',
  },
  {
    code: "` $${''}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\$${'{}'} `;", '` \\${} `;'],
  },
  {
    code: "` $${''} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` $ `;',
  },
  {
    code: '` $${`{}`} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\${} `;',
  },
  {
    code: '` $${``}${`{}`} `;',
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` \\$${`{}`} `;', '` \\${} `;'],
  },
  {
    code: '` $${``}${`foo{}`} `;',
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` $${`foo{}`} `;', '` $foo{} `;'],
  },
  {
    code: "` $${`${''}${`${``}`}`}${`{a}`} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: [
      "` \\$${''}${`${``}`}${`{a}`} `;",
      '` \\$${``}{a} `;',
      '` \\${a} `;',
    ],
  },
  {
    code: "` $${''}${`{}`} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` \\$${`{}`} `;', '` \\${} `;'],
  },
  {
    code: "` $${``}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\$${'{}'} `;", '` \\${} `;'],
  },
  {
    code: "` $${''}${``}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ['` \\$${``}{} `;', '` \\${} `;'],
  },
  {
    code: "` ${'$'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` $ `;',
  },
  {
    code: "` ${'$'}${'{}'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\$${'{}'} `;", '` \\${} `;'],
  },
  {
    code: "` ${'$'}${''}${'{'} `;",
    errors: [
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
      { messageId: 'noUnnecessaryTemplateExpression' },
    ],
    output: ["` \\$${''}{ `;", '` \\${ `;'],
  },
  {
    code: '` ${`\n\\$`}{} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \n\\${} `;',
  },
  {
    code: '` ${`\n\\\\$`}{} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \n\\\\\\${} `;',
  },

  {
    code: "`${'\\u00E5'}`;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: "'\\u00E5';",
  },
  {
    code: "`${'\\n'}`;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: "'\\n';",
  },
  {
    code: "` ${'\\u00E5'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\u00E5 `;',
  },
  {
    code: "` ${'\\n'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\n `;',
  },
  {
    code: noFormat`\` \${"\\n"} \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\n `;',
  },
  {
    code: '` ${`\\n`} `;',
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\n `;',
  },
  {
    code: noFormat`\` \${ 'A\\u0307\\u0323' } \`;`,
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` A\\u0307\\u0323 `;',
  },
  {
    code: "` ${'👨‍👩‍👧‍👦'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` 👨‍👩‍👧‍👦 `;',
  },
  {
    code: "` ${'\\ud83d\\udc68'} `;",
    errors: [{ messageId: 'noUnnecessaryTemplateExpression' }],
    output: '` \\ud83d\\udc68 `;',
  },
  {
    code: `
\`
this code does not have trailing whitespace: \${' '}\\n even though it might look it.\`;
    `,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `
\`
this code does not have trailing whitespace:  \\n even though it might look it.\`;
    `,
  },
  {
    code: `
\`
this code has trailing position template expression \${'but it isn\\'t whitespace'}
    \`;
    `,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `
\`
this code has trailing position template expression but it isn\\'t whitespace
    \`;
    `,
  },
  {
    code: noFormat`
\`trailing whitespace followed by escaped windows newline: \${' '}\\r\\n\`;
    `,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: `
\`trailing whitespace followed by escaped windows newline:  \\r\\n\`;
    `,
  },
  {
    code: `
\`template literal with interpolations followed by newline: \${\` \${'interpolation'} \`}
\`;
    `,
    errors: [
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
      {
        messageId: 'noUnnecessaryTemplateExpression',
      },
    ],
    output: [
      `
\`template literal with interpolations followed by newline:  \${'interpolation'}${' '}
\`;
    `,
      `
\`template literal with interpolations followed by newline:  interpolation${' '}
\`;
    `,
    ],
  },
] as const satisfies readonly InvalidTestCase<
  'noUnnecessaryTemplateExpression',
  []
>[]` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---