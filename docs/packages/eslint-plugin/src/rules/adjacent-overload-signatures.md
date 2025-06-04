[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `adjacent-overload-signatures.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 3 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/adjacent-overload-signatures.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getNameFromMember` | `../util` |
| `MemberNameType` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `name` | `any` | const | `member.id?.name ?? null` | ✗ |
| `lastMethod` | `Method | null` | let/var | `null` | ✗ |
| `seenMethods` | `Method[]` | const | `[]` | ✗ |


---

## Functions

### `getMemberMethod(member: Member | MemberDeclaration): Method | null`

<details><summary>Code</summary>

```ts
function getMemberMethod(
      member: Member | MemberDeclaration,
    ): Method | null {
      switch (member.type) {
        case AST_NODE_TYPES.ExportDefaultDeclaration:
        case AST_NODE_TYPES.ExportNamedDeclaration: {
          // export statements (e.g. export { a };)
          // have no declarations, so ignore them
          if (!member.declaration) {
            return null;
          }

          return getMemberMethod(member.declaration);
        }
        case AST_NODE_TYPES.TSDeclareFunction:
        case AST_NODE_TYPES.FunctionDeclaration: {
          const name = member.id?.name ?? null;
          if (name == null) {
            return null;
          }
          return {
            name,
            type: MemberNameType.Normal,
            callSignature: false,
          };
        }
        case AST_NODE_TYPES.TSMethodSignature:
        case AST_NODE_TYPES.MethodDefinition:
          return {
            ...getNameFromMember(member, context.sourceCode),
            callSignature: false,
            static: member.static,
          };
        case AST_NODE_TYPES.TSCallSignatureDeclaration:
          return {
            name: 'call',
            type: MemberNameType.Normal,
            callSignature: true,
          };
        case AST_NODE_TYPES.TSConstructSignatureDeclaration:
          return {
            name: 'new',
            type: MemberNameType.Normal,
            callSignature: false,
          };
      }

      return null;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets the name and attribute of the member being processed.
     * @param member the member being processed.
     * @returns the name and attribute of the member or null if it's a member not relevant to the rule.
     */
```

- **Parameters**:
  - `member: Member | MemberDeclaration`
- **Return Type**: `Method | null`
- **Calls**:
  - `getMemberMethod`
  - `getNameFromMember (from ../util)`
- **Internal Comments**:
```
// export statements (e.g. export { a };)
// have no declarations, so ignore them
```

### `isSameMethod(method1: Method, method2: Method | null): boolean`

<details><summary>Code</summary>

```ts
function isSameMethod(method1: Method, method2: Method | null): boolean {
      return (
        !!method2 &&
        method1.name === method2.name &&
        method1.static === method2.static &&
        method1.callSignature === method2.callSignature &&
        method1.type === method2.type
      );
    }
```
</details>

- **Parameters**:
  - `method1: Method`
  - `method2: Method | null`
- **Return Type**: `boolean`
### `getMembers(node: RuleNode): Member[]`

<details><summary>Code</summary>

```ts
function getMembers(node: RuleNode): Member[] {
      switch (node.type) {
        case AST_NODE_TYPES.ClassBody:
        case AST_NODE_TYPES.Program:
        case AST_NODE_TYPES.TSModuleBlock:
        case AST_NODE_TYPES.TSInterfaceBody:
        case AST_NODE_TYPES.BlockStatement:
          return node.body;

        case AST_NODE_TYPES.TSTypeLiteral:
          return node.members;
      }
    }
```
</details>

- **Parameters**:
  - `node: RuleNode`
- **Return Type**: `Member[]`
### `checkBodyForOverloadMethods(node: RuleNode): void`

<details><summary>Code</summary>

```ts
function checkBodyForOverloadMethods(node: RuleNode): void {
      const members = getMembers(node);

      let lastMethod: Method | null = null;
      const seenMethods: Method[] = [];

      members.forEach(member => {
        const method = getMemberMethod(member);
        if (method == null) {
          lastMethod = null;
          return;
        }

        const index = seenMethods.findIndex(seenMethod =>
          isSameMethod(method, seenMethod),
        );
        if (index > -1 && !isSameMethod(method, lastMethod)) {
          context.report({
            node: member,
            messageId: 'adjacentSignature',
            data: {
              name: `${method.static ? 'static ' : ''}${method.name}`,
            },
          });
        } else if (index === -1) {
          seenMethods.push(method);
        }

        lastMethod = method;
      });
    }
```
</details>

- **Parameters**:
  - `node: RuleNode`
- **Return Type**: `void`
- **Calls**:
  - `getMembers`
  - `members.forEach`
  - `getMemberMethod`
  - `seenMethods.findIndex`
  - `isSameMethod`
  - `context.report`
  - `seenMethods.push`

---

## Interfaces

### `Method`

<details><summary>Interface Code</summary>

```ts
interface Method {
      callSignature: boolean;
      name: string;
      static?: boolean;
      type: MemberNameType;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `callSignature` | `boolean` | ✗ |  |
| `name` | `string` | ✗ |  |
| `static` | `boolean` | ✓ |  |
| `type` | `MemberNameType` | ✗ |  |


---

## Type Aliases

### `RuleNode`

```ts
type RuleNode = | TSESTree.BlockStatement
  | TSESTree.ClassBody
  | TSESTree.Program
  | TSESTree.TSInterfaceBody
  | TSESTree.TSModuleBlock
  | TSESTree.TSTypeLiteral;
```

### `Member`

```ts
type Member = | TSESTree.ClassElement
  | TSESTree.ProgramStatement
  | TSESTree.TypeElement;
```

### `MemberDeclaration`

```ts
type MemberDeclaration = | TSESTree.DefaultExportDeclarations
  | TSESTree.NamedExportDeclarations;
```


---