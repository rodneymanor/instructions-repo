# Component Extraction and Publishing Guide for Cursor AI

## File Structure

```
component-package/
├── src/
│   ├── components/
│   │   └── YourComponent/
│   │       ├── index.tsx
│   │       ├── styles.css
│   │       └── types.ts
├── package.json
├── tsconfig.json
├── README.md
└── .gitignore
```

## Step 1: Component Extraction

```typescript
// src/components/YourComponent/index.tsx

import React from 'react';
import './styles.css';
import { YourComponentProps } from './types';

export const YourComponent: React.FC<YourComponentProps> = (props) => {
  // Your component logic here
};

export default YourComponent;
```

```typescript
// src/components/YourComponent/types.ts

export interface YourComponentProps {
  // Define your prop types here
}
```

## Step 2: Package Configuration

```json
// package.json
{
  "name": "@your-username/your-component",
  "version": "1.0.0",
  "main": "dist/index.js",
  "module": "dist/index.esm.js",
  "types": "dist/index.d.ts",
  "files": [
    "dist"
  ],
  "scripts": {
    "build": "rollup -c",
    "test": "jest",
    "prepare": "npm run build"
  },
  "peerDependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0"
  },
  "devDependencies": {
    "@types/react": "^18.0.0",
    "@types/react-dom": "^18.0.0",
    "typescript": "^4.9.0",
    "rollup": "^2.79.1",
    "@rollup/plugin-typescript": "^8.5.0",
    "@rollup/plugin-commonjs": "^22.0.0",
    "@rollup/plugin-node-resolve": "^14.1.0"
  }
}
```

```typescript
// tsconfig.json
{
  "compilerOptions": {
    "target": "es5",
    "module": "esnext",
    "jsx": "react",
    "declaration": true,
    "declarationDir": "dist",
    "sourceMap": true,
    "outDir": "dist",
    "strict": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

## Step 3: Build Configuration

```javascript
// rollup.config.js
import typescript from '@rollup/plugin-typescript';
import commonjs from '@rollup/plugin-commonjs';
import resolve from '@rollup/plugin-node-resolve';
import pkg from './package.json';

export default {
  input: 'src/index.ts',
  output: [
    {
      file: pkg.main,
      format: 'cjs',
      sourcemap: true,
    },
    {
      file: pkg.module,
      format: 'esm',
      sourcemap: true,
    },
  ],
  plugins: [
    typescript({
      tsconfig: './tsconfig.json',
    }),
    resolve(),
    commonjs(),
  ],
  external: ['react', 'react-dom'],
};
```

## Publishing Instructions

1. Initialize the package:
```bash
mkdir component-package
cd component-package
npm init -y
```

2. Install dependencies:
```bash
npm install --save-dev typescript @types/react @types/react-dom rollup @rollup/plugin-typescript @rollup/plugin-commonjs @rollup/plugin-node-resolve
```

3. Build the package:
```bash
npm run build
```

4. Login to npm:
```bash
npm login
```

5. Publish the package:
```bash
npm publish --access public
```

## Component Documentation Template

```markdown
# YourComponent

Brief description of your component and its purpose.

## Installation

```bash
npm install @your-username/your-component
```

## Usage

```jsx
import YourComponent from '@your-username/your-component';

function App() {
  return <YourComponent prop1="value1" prop2="value2" />;
}
```

## Props

| Prop Name | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| prop1 | string | Yes | - | Description of prop1 |
| prop2 | number | No | 0 | Description of prop2 |

## Examples

Provide usage examples here.

## License

MIT
```

## Version Control

1. Initialize git:
```bash
git init
```

2. Add .gitignore:
```
node_modules/
dist/
.DS_Store
*.log
```

3. Create initial commit:
```bash
git add .
git commit -m "Initial component setup"
```

4. Create GitHub repository and push:
```bash
git remote add origin https://github.com/your-username/your-component.git
git push -u origin main
```

## Semantic Versioning Guidelines

- MAJOR version (1.0.0): Breaking changes
- MINOR version (0.1.0): New features, backward-compatible
- PATCH version (0.0.1): Bug fixes, backward-compatible

To update version:
```bash
npm version patch # for bug fixes
npm version minor # for new features
npm version major # for breaking changes
```

## Testing Setup (Optional)

```json
// package.json additions
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch"
  },
  "devDependencies": {
    "@testing-library/react": "^13.0.0",
    "@testing-library/jest-dom": "^5.16.0",
    "jest": "^29.0.0"
  }
}
```

```javascript
// jest.config.js
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: ['@testing-library/jest-dom/extend-expect'],
  moduleNameMapper: {
    '\\.(css|less|scss|sass)$': 'identity-obj-proxy',
  },
};
```

## Cursor AI Commands

To use these instructions in Cursor AI:

1. Create a new project
2. Copy the entire structure above
3. Use Cursor AI's code completion to help implement specific parts
4. Use commands like:
   - `/explain` to understand specific parts
   - `/generate` to create new component features
   - `/refactor` to improve code structure
   - `/test` to generate test cases

Remember to replace `your-username` and `YourComponent` with your actual values throughout the files.
