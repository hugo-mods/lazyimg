<a href="https://hugo-mods.github.io/#lazyimg"><img alt="Logo" align="right" width="200" src="https://raw.githubusercontent.com/hugo-mods/lazyimg/main/.github/logo.png"></a>

# lazyimg
## Lazy image loading with superpowers.

- Lazy loading for images via `lazySizes`
- No-Script/No-JS safe: Fallback to browser's native method
- Image previews: Blur-up Low Quality Image Placeholder (LQIP) technique
- Automatic responsive image [resizing](#resizers)
- Multiple supported [renderers](#renderers) (e.g. LQIP with WebP support)

> Used by the [Osprey Delight](https://github.com/kdevo/osprey-delight) theme, which directly benefits from this module!


## Quickstart <a href="#quickstart"></a>

### Go get it

Initialize [Hugo's mod system](https://gohugo.io/hugo-modules/) on your site (replace username and repo):

```sh
hugo mod init github.com/{username}/{repo}
```

Add module to site's config (e.g. `config.yaml`):

```yaml
module:
  imports:
  - path: github.com/hugo-mods/lazyimg
```

Get the module (also upgrades existing one):

```sh
hugo mod get -u
```

### Usage

1. Put the images which you want to use in the `assets` directory of your project. They should be in a high resolution and will be resized automatically.
2. Add the following boilerplate setup code to your site's `<head>`:
```
{{ partial "lazyimg-setup" }}
```
3. Load the image:
    - In a template file: Call the `lazyimg` partial where you would usually use an `img` tag:
    ```
    {{ partial "lazyimg" "awesome-image.jpeg" }}
    ```
    - In a content file: Call the `lazyimg` shortcode: 
    ```
    {{< lazyimg img="awesome-image.jpeg" >}}
    ```

For more advanced usage, please refer to the [`exampleSite`](./exampleSite) for a practical approach or continue reading the theory as described in the next section.

## Configuration

Please check out the [example site's config](exampleSite/config.yaml) for all options.

### Resizers <a href="#resizers"></a>

Allowed values for `resizer`:

| Name                        | Description
|:----------------------------|-------------------------------------------------------------
| `simple`                    | Produces default image with `maxSize`, LQIP with `lqipSize`.
| `responsive`                | Produces default image with `maxSize`, LQIP with `lqipSize` and responsive images based on `responsiveSizes`.
| `auto`                      | Produces default image with `maxSize`, LQIP with `lqipSize` and partitions (max. of 5) responsive sizes based on an algorithm.

### Renderers <a href="#renderers"></a>

Allowed values for `renderer`:

| Name                        | Description
|:----------------------------|-------------------------------------------------------------
| `simple`                    | Responsive image lazy-loading.
| `lqip`                      | Responsive image lazy-loading with LQIP blur-up preview. Use with [`lazyimg.css`](#CSS).
| `lqip-webp`                 | Responsive image lazy-loading `lqip` with additional WebP support.
| `native`                    | [Browser-native loading](https://web.dev/browser-level-image-lazy-loading/) via `loading="lazy"`. Does not require JS, used as fallback in other renderers when `noscript` is true.

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
