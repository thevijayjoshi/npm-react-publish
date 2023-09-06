# Publishing a React Component as an NPM Package

This guide will walk you through the process of publishing a React component as an NPM package. Publishing packages on the NPM registry comes with several benefits, including code sharing, collaboration, and reusability within your projects and the wider developer community.

## Prerequisites

Before you begin, make sure you have the following prerequisites installed:

- Node.js
- npm
- [npm account](https://www.npmjs.com/) (Create one if you don't have an account)

Ensure that you have a unique name for your package. You can verify the uniqueness of your proposed package name on the npm website or through the terminal using the following command:

```bash
npm search <your-package-name>
```

## Initializing the Package

To initialize your package, run the following command, replacing <your-package-name> with your desired package name:

```bash
npx create-react-library <your-package-name>
```

## Your package.json file will look like this:

```json
{
  "name": "demo",
  "version": "1.2.7",
  "description": "Demo",
  "author": "Vijay Joshi",
  "license": "MIT",
  "repository": "https://github.com/thevijayjoshi/npm-react-publish",
  "main": "dist/index.js",
  "module": "dist/index.modern.js",
  "source": "src/index.js",
  "engines": {
    "node": ">=10"
  },
  "scripts": {
    "build": "microbundle-crl --no-compress --format modern,cjs",
    "start": "microbundle-crl watch --no-compress --format modern,cjs",
    "prepare": "run-s build",
    "test": "run-s test:unit test:lint test:build",
    "test:build": "run-s build",
    "test:lint": "eslint .",
    "test:unit": "cross-env CI=1 react-scripts test --env=jsdom",
    "test:watch": "react-scripts test --env=jsdom",
    "predeploy": "cd example && npm install && npm run build",
    "deploy": "gh-pages -d example/build"
  },
  "peerDependencies": {
     // Add your peerDependencies here
  },
  "devDependencies": {
    // Add your devDependencies here
  },
  "files": [
    "dist"
  ]
}
```

## Adding Dependencies

Make sure to add the dependencies your component needs in the peerDependencies section.

## Folder Structure
Here's the recommended folder structure:

```text
- dist
- example
- node_modules
- src
  - Components
    - DemoComponent
      - index.js (Write your component code here)
    - index.js
  - index.js
- .editorconfig
- .eslintignore
- .eslintrc
- .gitignore
- .prettierrc
- .travis.yml
- package-lock.json
- package.json
- README.md
```

## How to import and export?

```jsx
// src/index.js code
export * from './Components';

// src/components/index.js
export { default as DemoComponent } from './DemoComponent';
```

## Publishing the Package
To publish your package, follow these steps:

1.Build your package:
```bash
npm run build
```

2.Publish your package:
```bash
npm publish
```

Hooray! Your React component is now published as an NPM package.

## Making Changes
If you want to make changes after publishing, update the version in your package.json file, and then run the following commands:

1.Build your package:
```bash
npm run build
```

2.Publish your package:
```bash
npm publish
```

That's it! Your changes will be reflected in the latest version of your package on NPM.
