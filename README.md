# Vite PWA Setup

A simple tutorial on how to create a PWA using Vite.

## Instructions

Create a Vite project (skip this step if you already have a project):

```bash
npm create vite@latest
```

Follow the displayed instructions to create the Vite Project and go to the project directory.

Install the dependencies:

```bash
npm install
```

Install the Vite PWA plugin:

```bash
npm i vite-plugin-pwa -D
```

Install the PWA Assets Generator plugin:

```bash
npm i @vite-pwa/assets-generator -D
```

Configure the Vite PWA plugin by adding the following code to the `vite.config.js` or `vite.config.ts` file:

```bash
import { VitePWA } from 'vite-plugin-pwa';
```

```bash
VitePWA({
      registerType: "autoUpdate", // Automatically update the service worker
      injectRegister: "auto", // Automatically include the service worker registration code in the application entry point
      includeAssets: ["favicon.ico", "apple-touch-icon.png", "mask-icon.svg"],
      manifest: {
        name: "Vite PWA",
        short_name: "PWA",
        description: "Description of your app",
        theme_color: "#ffffff",
        icons: [
          {
            src: "pwa-64x64.png",
            sizes: "64x64",
            type: "image/png",
          },
          {
            src: "pwa-192x192.png",
            sizes: "192x192",
            type: "image/png",
          },
          {
            src: "pwa-512x512.png",
            sizes: "512x512",
            type: "image/png",
            purpose: "any",
          },
          {
            src: "maskable-icon-512x512.png",
            sizes: "512x512",
            type: "image/png",
            purpose: "maskable",
          },
        ],
      },
    }),
```

This should be the final `vite.config.js` or `vite.config.ts` file if Vue was chosen when creating the Vite project:

```bash
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import { VitePWA } from "vite-plugin-pwa";

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: "autoUpdate", // Automatically update the service worker
      injectRegister: "auto", // Automatically include the service worker registration code in the application entry point
      includeAssets: ["favicon.ico", "apple-touch-icon.png", "mask-icon.svg"],
      manifest: {
        name: "Vite PWA",
        short_name: "PWA",
        description: "Description of your app",
        theme_color: "#ffffff",
        icons: [
          {
            src: "pwa-64x64.png",
            sizes: "64x64",
            type: "image/png",
          },
          {
            src: "pwa-192x192.png",
            sizes: "192x192",
            type: "image/png",
          },
          {
            src: "pwa-512x512.png",
            sizes: "512x512",
            type: "image/png",
            purpose: "any",
          },
          {
            src: "maskable-icon-512x512.png",
            sizes: "512x512",
            type: "image/png",
            purpose: "maskable",
          },
        ],
      },
    }),
  ],
});
```

Generate the PWA assets by adding the following script in `package.json`:

```bash
"generate-pwa-assets": "pwa-assets-generator --preset minimal public/logo.svg"
```

The `package.json` should now look something like this:

```bash
{
  "name": "vite-pwa",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "generate-pwa-assets": "pwa-assets-generator --preset minimal public/logo.svg"
  },
  "dependencies": {
    "vue": "^3.5.13"
  },
  "devDependencies": {
    "@vite-pwa/assets-generator": "^0.2.6",
    "@vitejs/plugin-vue": "^5.2.1",
    "vite": "^6.0.1",
    "vite-plugin-pwa": "^0.21.1"
  }
}
```

Add a custom `logo.svg` in the public folder or just copy the `vite.svg` in the public folder and rename it to `logo.svg`.

Create the PWA assets:

```bash
npm run generate-pwa-assets
```

Add the following code in the `<head>` of `index.html` file to include the assets in the web page:

```bash
<link rel="icon" href="/favicon.ico" />
<link rel="apple-touch-icon" href="/apple-touch-icon-180x180.png" sizes="180x180" />
<link rel="mask-icon" href="/mask-icon.svg" color="#FFFFFF">
<meta name="theme-color" content="#ffffff">
```

The `index.html` should now look something like this:

````bash
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <link rel="icon" href="/favicon.ico" />
    <link rel="apple-touch-icon" href="/apple-touch-icon-180x180.png" sizes="180x180" />
    <link rel="mask-icon" href="/mask-icon.svg" color="#FFFFFF">
    <meta name="theme-color" content="#ffffff">

    <title>Vite + Vue</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
````

Run and build the app:

```bash
npm run build
```

```bash
npm run preview
```
