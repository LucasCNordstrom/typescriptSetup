# &lt;/ SALT&gt;
​
## Setting up a new Typescript project
​
### Including- Testing, Linting and Typescript
​
#### Linting
In order for you to start lets make a folder followed by creating a new project-
`mkdir 'nameOfProject'` then `cd 'nameOfProject'` and finaly `npm init -y`. This will create the projects with all defaults.
​
Run `npm install -- save-dev typescript` to install typescript as a dev-dependency. After that, run `touch tsconfig.json` - open that file.
Paste :
​
```json
{
  "extends": "@tsconfig/node16/tsconfig.json",
  "compilerOptions": {
    "outDir": "dist",
    "lib": ["es2021", "DOM"]
  },
  "include": ["src"],
  "exclude": ["node_modules"],
}
```
​
into that file.
​
You now have a typescript config-file. Now lets create a typescript file and a test-file. Place these in a folder called `src` (This is just by convention.) and `cd` into it.
​
Run `touch index.ts` followed by `touch index.test.ts`. Great, copy the following code into the testfile- 
​
```javascript
import { expect } from 'chai';
import testMethod from './index';
​
describe('typescript tests', () => {
  it('Should return a something cool in test', () => {
    const testValue = testMethod();
    expect(testValue).equal('someThingCool');
  });
​
  it('Should return somethingCool also in test but with other syntax', () => {
    expect(testMethod()).equal('someThingCool');
  });
});
```
​
and this into the index-file
​
```javascript
const testMethod = () => {
  console.log('this is written from the code');
  return 'someThingCool';
};
​
export default testMethod;
​
```
​
This should give you some warnings or errors- eg you need to install `chai@/types` , `mocha@types` or such.
​
Run these commands `npm i @types/mocha --save-dev` , `npm i chai --save-dev` , `npm i @types/chai --save-dev` , `npm i mocha --save-dev` and finally `npm install ts-node --save-dev`. Now you should be able to write `npm test`. You'll see `no test specified`- Copy these lines into your `package.json` below the `script` section- 
​
```json
 "test": "mocha -r ts-node/register src/**/*.test.ts",
```
Now you can actually test your code!!!
​
Ouff, that was a lot of work but now we can write tests and code that will be typesafe, which is great! Now we only have one last part to fix, the dreaded linting, making sure we write code following certain guidelines.
​
Run this command `touch .eslintrc`, this will create your eslint will all the rules for linting (this will not really contain any rules but rather point to somewhere else). In that file, copy this-
​
```json
{
  "extends": "salt-typescript",
  "parserOptions": {
    "project": "tsconfig.json"
  }
}
```
​
After that run `npm i eslint-config-salt-typescript --save-dev` to install the linter we're going to use during this bootcamp!
​
Now we're in the absolute last part of this tutorial on how to set things up- this is optional but it is something I find very useful atleast and that is making the linter run before running my tests. Replace what we had before at `test` in your script-section of package.json 
```json
"test": "eslint ./src/**/*.ts --fix && mocha -r ts-node/register src/**/*.test.ts",
"lint": "eslint ./src/**/*.ts --fix"
```
​
You've now reached the end of this tutorial, really great job!
