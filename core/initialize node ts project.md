yarn init
yarn add typescript
yarn add -D node@types
yarn tsc --init

yarn add tsx --dev

tsconfig.json
set the module and target to be ESNext
"include": ["src", "server.ts"],
"exclude": ["node_modules"]

package.json
set the module to be type
add these on the "scripts" on package.json
"dev": "tsx watch src/index.ts",

or most simple

yarn init
yarn add typescript
yarn add -D node@types
yarn tsc --init

yarn add -D nodemon

in the script
"dev": "nodemon src/server.ts"
