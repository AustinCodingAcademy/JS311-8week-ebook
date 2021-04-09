# How to Write in Markdown

As may be clear to you, Markdown(.md) is a wonderful language to write in because it's mostly plain text with lots of functionality. In fact, all of this ebook is written in markdown including the code snippets, charts and images.

To help you write in it a little faster here are some example to get you up to speed. You'll first see the "result" and then a code snippet of Markdown that makes it happen.

*****

# H1 Title

```markdown
  *****

  # H1 Title
```

*****

## H2 Title

```markdown
  *****

  ## H2 Title
```

*****

### H3 Title

```markdown
  *****

  ### H3 Title
```

*****

*Italicized words*

```markdown
  *****

  *Italicized words*
```

*****

**Bold words**

```markdown
  *****

  **Bold words**
```

*****

[A YouTube Video Link - How Not to Take Things Personally](https://www.youtube.com/watch?v=LnJwH_PZXnM)

```markdown
  *****

  [A YouTube Video Link - How Not to Take Things Personally](https://www.youtube.com/watch?v=LnJwH_PZXnM)

  <!-- if you want an image put a ! in-front of it -->
  ![my-image](./../images/my-image.png)
```

*****

| A Chart  | of Methods |
| -  | - |
| `GET` | Fetch resource  |
| `PUT` | Update resource |
| `DELETE` | Delete resource |

```markdown
  *****

  | A Chart  | of Methods | 
  | -  | - |
  | `GET` | Fetch resource  |
  | `PUT` | Update resource |
  | `DELETE` | Delete resource |
```

*****

```javascript
  // This is a JavaScript Code Fence
  const myFunction = () => {
    return something
  }
```

```markdown
  <!-- uncomment the line immediately below -->
  <!-- ```javascript -->
  // This is a JavaScript Code Fence
  const myFunction = () => {
    return something
    }
  <!-- ``` -->
  <!-- uncomment the line immediately above -->
```

*****

```sql
  -- this is a sql code fence
  SELECT * from users
```

```markdown
  <!-- uncomment the line immediately below -->
  <!-- ```sql -->
  -- this is a sql code fence
  SELECT * from users
  <!-- ``` -->
  <!-- uncomment the line immediately above -->
```

*****

1. Numbered Items
1. Numbered Items
1. Numbered Items
1. Numbered Items

```markdown
  1. Numbered Items
  1. Numbered Items
  1. Numbered Items
  1. Numbered Items
```

*****

* Bulleted Items
* Bulleted Items
* Bulleted Items
* Bulleted Items

```markdown
  * Bulleted Items
  * Bulleted Items
  * Bulleted Items
  * Bulleted Items
```

*****

## Tips

- [ ] In VS Code you can use ++cmd+shift+v++ to view a preview of the Markdown file(.md)
- [ ] Sorry, <--- these checkboxes (`- [ ]`) won't be supported in GitHub

```markdown
  - [ ] In VS Code you can use ++cmd+shift+v++ to view a preview of the Markdown file(.md)
  - [ ] Sorry, <--- these checkboxes (`- [ ]`) won't be supported in GitHub
  <!-- Make comments -->
  <!-- * Highlight your comments in VS Code -->
  <!-- TODO add more resources here... -->
  <!-- ? Should we add more resources? -->
  <!-- ! YES, add more resources -->
```
