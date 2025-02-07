---
title: "ESLint: Find and Fix problems in your JavaScript code"
datePublished: Sat Sep 18 2021 05:21:42 GMT+0000 (Coordinated Universal Time)
cuid: cktpcfhpq051co5s12mz58jnr
slug: eslint-find-and-fix-problems-in-your-javascript-code
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1631942386190/evLlu7oGw.png
tags: software-development, programming-blogs, javascript, reactjs, eslint

---

## Step : 1
- Create a React.js project by running the below command in your terminal.
- 
```
npx create-react-app lint_example
```
- If you open the project in VSCode, you can see there is no `eslint` config file. So let's try to first configure the `eslint` for the project.
- 
![no-config.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631542137661/llim2Ec4E.png)
--------
## Step : 2
- If you've not installed the `eslint` package then run the below command in your terminal.
- 
```
npm install -g eslint
```
- This installs ESLint globally on your machine, so you can use it on any future project
- Now that it is installed. We can configure it in our project by running below command.
- 
```
eslint --init
```
- Now after running this command there are some questions which you need to answer -
- 
![answers.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631542610483/Wts-_ziVE.png)
- After answering all the questions the plugin **eslint-plugin-react** will be automatically installed in the `devDependencies`.

----------

## Step : 3 
- Now that all the configuration is done, the `.eslintrc.json` file is created in your root directory.
- 
![eslintrc.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631542859690/Ge0WSgjoF.png)
- To apply the eslint rules in all of the files that you will be creating, add the below script in the `package.json`'s `script` key.
- 
```
"lint": "eslint src/**/*.js",
```
- Now if you run the `npm run lint`, you will now see all the warnings and errors given by the eslint.
- 
![warnings&errors.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631543202267/Yfh6xYDpa.png)

--------
## Step : 4
- Now, To fix some of the warnings like For ex: `indent`, `spaces`, etc add the below script in the `package.json`
- 
```
"lint-fix": "eslint src/**/*.js --fix"
```
- And now run it using the below command
- 
```
npm run lint-fix
```
- This will automatically fix the warnings/errors.

---------
## Step : 5
- But there is still one error popping, which is `React must be in scope when using JSX`.
- To solve this error, add the below code in `eslintrc.json` file
- 
```
"settings": {
    "react": {
      "version": "detect" // or latest
    }
  },
```  
- **And also the below rules** in the `.eslintrc.json`'s "rules":{}
- 
```
"react/react-in-jsx-scope": "off",
```
- This will help eslint to detect the current react version you are running.
- After adding this, run again the `npm run lint-fix` command.
- **Final .eslintrc.json** file will look something like this - 
%[https://gist.github.com/red-star25/d2e2c2787e7a4db7259e0c2745745cc1]

---------
- **If you liked this article then make sure to share it with others.**
- **See you in the next article. Until then...**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631942118244/cb0x5vQ08.gif)
