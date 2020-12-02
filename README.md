# Minimum setup to use TailwindCSS with create-react-app

1. Create CRA project

```
npx create-react-app cra-tailwind --template typescript
```

2. Install and configure CRACO

TailwndCSS requires PostCSS so that you have to install CRACO to override create-react-app configuration.

```
cd cra-tailwind
npm i -D @craco/craco
```

Then, create `craco.config.js` as below.

```
module.exports = {
  style: {
    postcss: {
      plugins: [
        require("tailwindcss")("./tailwind.config.js"),
        require("autoprefixer")
      ],
    },
  },
};
```

3. Install and configure TailwindCSS

Install PostCSS 7 compatibility packages.
For some reason, some errors could occur when using PostCSS 8 for now. See more details in [PostCSS 7 compatibility build](https://tailwindcss.com/docs/installation#post-css-7-compatibility-build).

```
npm i tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

Then, create `tailwind.config.js` files by `tailwindcss` command.

```
npx tailwindcss init
```

Add any files that reference any tailwindcss classes to `purge` option.

```
module.exports = {
  purge: ['./src/**/*.tsx'], // add any files that reference any tailwindcss classes.
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```

4. Include Tailwind styles in you CSS

```
/* index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

That's it!
