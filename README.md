# Original script
https://github.com/elcheio/sass-map-get-next-prev
This repo is a fork of the original source. It only adds the basic requirements that are necessary to enable installation npm. 

## Sass map-get functions

Enhancement functions map-get-next and map-get-prev.
For example when Sass map is used with a `@each` loop.

## Installation with npm

For usage in node simply add
```json
"sass-map-get-next-prev": "git+https://github.com/rowild/sass-map-get-next-prev.git",
```
to your package.json, then run `npm install`.

## Tutorial on how to use these functions
- [Sass map-get functions](#sass-map-get-functions)
  - [Installation with npm](#installation-with-npm)
  - [Tutorial on how to use these functions](#tutorial-on-how-to-use-these-functions)
  - [map-get-next](#map-get-next)
    - [Basic usage](#basic-usage)
      - [CSS output](#css-output)
    - [Practical usage](#practical-usage)
      - [CSS output](#css-output-1)
    - [Parameters](#parameters)
  - [map-get-prev](#map-get-prev)
    - [Basic usage](#basic-usage-1)
      - [CSS output](#css-output-2)
    - [Parameters](#parameters-1)

## map-get-next

Function to get next map item.
Returns next map item or fallback value if map, key or next item does not exist.

### Basic usage

```sass
$map: (
    s: 320px,
    m: 768px,
);

.foo {
  width: map-get-next($map, s);
}

.bar {
  width: map-get-next($map, m, 1024px);
}
```

#### CSS output

```css
.foo {
  width: 768px;
}

.bar {
  width: 1024px;
}
```

### Practical usage

Set min- and max with for all breakpoints in Sass map.

```sass
$map: (
    s: 320px,
    m: 768px,
);

@each $breakpoint, $width in $map {
  @media (min-width: $width) and (max-width: map-get-next($map, $breakpoint, 1024px) - 1px) {
    ...
  }
}
```

#### CSS output

```css
@media (min-width: 320px) and (max-width: 767px) {
  ...
}

@media (min-width: 768px) and (max-width: 1023px) {
  ...
}
```

### Parameters

* **$map** - Sass list map
* **$key** - List map key
* **$fallback** (false) - Fallback value if map, key or next item does not exist
* **$debug** (false) - Debug option

## map-get-prev

Equivalent to map-get-next

Function to get previous map item.
Returns previous map item or fallback value if map, key or previous item does not exist.

### Basic usage

```sass
$map: (
    s: 320px,
    m: 768px,
);

.foo {
    width: map-get-prev($map, m);
}

.bar {
    width: map-get-prev($map, s, 240px);
}
```

#### CSS output

```css
.foo {
    width: 320px;
}

.bar {
    width: 240px;
}
```

### Parameters

* **$map** - Sass list map
* **$key** - List map key
* **$fallback** (false) - Fallback value if map, key or previous item does not exist
