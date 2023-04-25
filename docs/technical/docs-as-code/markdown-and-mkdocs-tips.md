# Markdown and MKDocs tips

## Links

### Linking to another `dev-docs` file

Use the markdown file name instead of providing a path.

Makes links more resilient when folders/files are moved.

```markdown
[link text](my-markdown-file.md)

[link text](my-markdown-file.md#header)
```

## Tables

-   Paste a Bookstack table into [Zettlr](https://www.zettlr.com/) or in a GitHub comment
    -   it will generate the Markdown for the table

## Images

### Pasting images

Make sure to upload images to the `./images` directory

-   Zettlr
    -   pasting an image from the clipboard will create an image file
-   VSCode
    -   use the [Paste Image extension](https://github.com/mushanshitiancai/vscode-paste-image) to paste images from the clipboard
-   PyCharm
    -   install the [Paste Images into Markdown](https://plugins.jetbrains.com/plugin/8446-paste-images-into-markdown) extension

### Image paths

Ensure that paths to images are relative

-   so that they can be found by both GitHub and MKDocs
    -   we need view images in GitHub for code review
    -   Example ✅ : `images/file_name.png`
    -   Bad example ❌ : `/assets/path_to_image.png`

### Changing the image size

Markdown understands HTML. 🧠 You can use the `img` tag.

```html
<img src="../image/file_name.png" alt="alt_text" height="300px" />
```

#### MKDocs way of adding a height or width

[You can apply a height or width on the image](https://github.com/mkdocs/mkdocs/issues/1678#issuecomment-455500757)

```markdown
![image alt text](https://example.com/an_image.img){: style="height:150px;width:150px"}
```

This will be resized in MKDocs but not in GitHub during code review.
