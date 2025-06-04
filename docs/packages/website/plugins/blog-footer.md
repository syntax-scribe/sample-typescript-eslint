[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `blog-footer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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