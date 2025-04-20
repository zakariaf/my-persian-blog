# RTL Support for Jekyll Theme Chirpy

This document describes how the Right-to-Left (RTL) support works in the Chirpy theme.

## Table of Contents

- [Overview](#overview)
- [Configuration](#configuration)
- [How It Works](#how-it-works)
- [Creating RTL Content](#creating-rtl-content)
- [Language-Specific Fonts](#language-specific-fonts)
- [Customization](#customization)
- [Known Limitations](#known-limitations)

## Overview

The Chirpy theme provides support for Right-to-Left (RTL) languages such as Arabic, Hebrew, Persian, Urdu, and more. This support is implemented with minimal changes to the theme's core functionality and ensures a seamless experience for users reading content in RTL languages.

## Configuration

RTL support can be configured in your `_config.yml` file:

```yaml
# RTL Support Configuration
# Set this to true to enable RTL support for all languages
# If false, RTL will only be applied to RTL languages (ar, he, fa, etc.)
rtl_support: false

# RTL Languages array - add more languages if needed
rtl_languages:
  - ar
  - fa-IR
  - he
  - ku-IQ
  - ur-PK
  - ps-AF
  - dv-MV
```

- `rtl_support`: If set to `true`, all pages will be rendered in RTL mode regardless of language. If `false` (default), only pages with languages listed in `rtl_languages` will be in RTL mode.
- `rtl_languages`: An array of language codes that should be rendered in RTL mode. Add your RTL language code to this list if needed.

## How It Works

The RTL support works by:

1. Detecting the page language using the `lang` attribute in the front matter or the site's default language.
2. Checking if the language is in the RTL languages list (or if `rtl_support` is set to `true`).
3. Setting the `dir="rtl"` attribute on the HTML tag when appropriate.
4. Applying RTL-specific styles that override the default LTR styles.
5. Loading language-specific fonts for the detected RTL language.

## Creating RTL Content

To create content in an RTL language:

- Add the appropriate `lang` attribute in the front matter of your post or page:

  ```yaml
  ---
  title: عنوان المقال
  author: اسم الكاتب
  date: 2023-01-01
  lang: ar
  # other front matter...
  ---

  محتوى المقال هنا...
  ```

- The theme will automatically detect the language and apply RTL styling and appropriate fonts.
- When using RTL languages, the whole page will be displayed in RTL mode, including navigation, sidebar, and other UI elements.
- If you've provided a localization file for the language (e.g., `_data/locales/ar.yml`), the theme will use it for UI text.

## Language-Specific Fonts

The theme includes built-in support for several RTL language fonts:

- **Arabic**: Noto Sans Arabic
- **Persian (Farsi)**: Vazirmatn
- **Hebrew**: Noto Sans Hebrew
- **Urdu**: Noto Nastaliq Urdu

These fonts are automatically applied based on the page's language attribute. For example, if your page has `lang: fa-IR`, the Vazirmatn font will be used.

## Customization

If you need to customize the RTL styles:

1. The main RTL styles are in `_sass/rtl.scss`.
2. Language-specific font definitions are in `_sass/rtl-fonts.scss`.
3. You can add additional styles to these files or create your own custom styles in your theme.

To change or add RTL fonts:

1. Modify the `rtl-fonts.scss` file to include your preferred fonts.
2. Update the font assignments for specific language codes.

## Known Limitations

- Code blocks are always displayed left-to-right (LTR) for better readability of code.
- Some third-party components or embedded content might not respect RTL layout.
- RTL mode is applied on a per-page basis based on the language attribute. If you want consistent RTL layout across your entire site, set `rtl_support: true` in your configuration.
- When switching between RTL and LTR pages, there might be a brief moment before fonts are fully loaded.
