[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `blog-footer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/plugins/blog-footer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Plugin` | `unified` |
| `nodeIsParent` | `./utils/nodes` |


---

## Functions

### `blogFooter(): (root: any, file: any) => void`

<details><summary>Code</summary>

```ts
() => {
  return (root, file) => {
    if (
      !nodeIsParent(root) ||
      !(file.value as string).includes('<!--truncate-->')
    ) {
      return;
    }

    root.children.push(
      {
        children: [
          {
            type: 'text',
            value: 'Supporting typescript-eslint',
          },
        ],
        depth: 2,
        type: 'heading',
      } as mdast.Heading,
      {
        children: [
          {
            type: 'text',
            value:
              'If you enjoyed this blog post and/or use typescript-eslint, please consider ',
          },
          {
            children: [
              {
                type: 'text',
                value: 'supporting us on Open Collective',
              },
            ],
            type: 'link',
            url: 'https://opencollective.com/typescript-eslint',
          },
          {
            type: 'text',
            value: `. We're a small volunteer team and could use your support to make the ESLint experience on TypeScript great. Thanks! 💖`,
          },
        ],
        type: 'paragraph',
      } as mdast.Paragraph,
    );
  };
}
```
</details>

- **Return Type**: `(root: any, file: any) => void`
- **Calls**:
  - `nodeIsParent (from ./utils/nodes)`
  - `(file.value as string).includes`
  - `root.children.push`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---