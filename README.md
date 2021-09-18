<!-- <a href=""><img alt="Logo" align="right" width="200" src="https://raw.githubusercontent.com/hugo-mods/lazy/main/.github/logo.png"></a> -->

# lazyimg
## Lazy image loading made easy. With automatic image resizing and LQIP support.

- Lazy loading for images via `lazySizes`
- No-Script-safe: Fallback to browser's native method
- ...

> Used by the [Osprey Delight](https://github.com/kdevo/osprey-delight) theme, which directly benefits from this module!

## Go get it

Initialize [Hugo's mod system](https://gohugo.io/hugo-modules/) on your site:

`hugo mod init github.com/{username}/{repo}`

Add module to site's config (e.g. `config.yaml`):

```yaml
module:
  imports:
  - path: github.com/hugo-mods/lazyimg
```

Get the module (also upgrades existing one):

`hugo mod get -u`

## Quickstart 

1. Put the images which you want to use in the `assets` directory of your project. They should be in a high resolution and will be resized automatically.
2. Add the following boilerplate setup code to your site's `<head>`:
```
{{ partial "lazyimg-setup" }}
```
3. Load the image by calling the `lazyimg` partial where you would usually use an `img` tag:
```
{{ partial "lazyimg" "my-awesome-image.jpeg" }}
```

For more advanced usage, please refer to the [`exampleSite`](./exampleSite) for a practical approach or continue reading the theory as described in the next section.

## Configuration

### Resizers

| Name                        | Description
|:----------------------------|-------------------------------------------------------------
| `simple`                    | Produces default image with `maxSize`, LQIP with `lqipSize`.
| `responsive`                | Produces default image with `maxSize`, LQIP with `lqipSize` and responsive images based on `responsiveSizes`.
| `auto`                      | Produces default image with `maxSize`, LQIP with `lqipSize` and guesses responsive sizes based on an algorithm. Highly experimental.

### Renderers

| Name                        | Description
|:----------------------------|-------------------------------------------------------------
| `lqip`                      | All-around responsive lazy-loading with LQIP blur-up preview. Recommended: [`lazyimg.css`](#CSS).
| `lqip-webp`                 | `lqip` with additional WebP support. TODO(kdevo): not implemented yet.

### CSS

The `lazyimg.css` is the recommended boilderplate CSS. 
It contains rules for blur-up animation, hiding "broken image icon" on lazy-loading and [no-js](#disabled-js) selector.

### Disabled JS

Support for disabled JS can be accomplished by adding a "no-js" class to your `html` root tag, e.g.:

```html
<html lang="en" class="no-js"> <!-- ... --> </html>
```

Then, to remove the class when the client indeed supports JS, add the following script:

```html
<script>document.documentElement.className = "js"</script>
```

Alternatively, use `lazyimg-setup-nojs` instead of `lazyimg-setup` which will do the replacement for you.
In this case, you only need to add the `no-js` class to your `html` root tag.
