<div align="center">
<a href="[netlify-deploy-url]">
<img alt="ToDo App logo" width="490px" src="https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/logo.png?raw=true"/>
</a>
</div>

<!-- <img alt="Proffy" src="./github/banner.png"> -->
<p align="center">
  <img alt="Repository's size: " src="https://img.shields.io/github/repo-size/gabrielmmf/useReducer-calculator?style=for-the-badge">
  <img alt="Last commit" src="https://img.shields.io/github/last-commit/gabrielmmf/useReducer-calculator?style=for-the-badge">
  <a href="https://github.com/gabrielmmf">
    <img alt="Made by Gabriel Fialho" src="https://img.shields.io/badge/made%20by-Gabriel%20Fialho-%237519C1?style=for-the-badge">
  </a>
<p>

---

### :triangular_ruler: Project Status

<h4>
The project has already been completed!.
<br/>
But I'm always improving the code! 😀
<br/>
<br/>
<!-- 👇 -->
</h4>
<!-- 
### :computer: [Deploy at Netlify]([netlify-deploy-url]) -->

---

## :scroll: Table of contents

1. [About](#bookmark_tabs-about)
2. [Features](#heavy_check_mark-features)
3. [How to use](#crystal_ball-how-to-use)
4. [Database diagram](#file_cabinet-database-diagram)
5. [Technologies](#hammer-technologies)
6. [Services Used](#gear-services-used)
7. [Client Dependencies](#lock-client-dependencies)
8. [Server Dependencies](#closed_lock_with_key-server-dependencies)
9. [Project Roadmap](#round_pushpin-project-roadmap)
10. [Running the project](#dvd-running-the-project)
11. [Contributing](#memo-contributing)
12. [Author](#boy-author)
13. [Links](#link-links)
14. [License](#balance_scale-license)

---

## :bookmark_tabs: About

This is my project that allows you to login, logout and make a personal todo list. The user are allowed to add, delete or edit tasks

In this project, I reinforced my knowledge about:

- React
- Use Reducer React Hook
- CSS

---

## :heavy_check_mark: Features

The main features of the application are:

- Add digits to the current operand
- Choose operation, moving the current operand to the previous operand
- Clear the calculator state
- Delete a digit from the current operand
- Evaluate the operation

All the actions where stored in the object ACTIONS:

```javascript
export const ACTIONS = {
  ADD_DIGIT: "add-digit",
  CHOOSE_OPERATION: "choose-operation",
  CLEAR: "clear",
  DELETE_DIGIT: "delete-digit",
  EVALUATE: "evaluate",
};
```

Every button click calls a dispatch function, called reducer, that updates the calculator state according to the Action type and the action payload, which corresponds to the button pressed:

```javascript
function reducer(state, { type, payload }) {
  switch (type) {
    case ACTIONS.ADD_DIGIT:
      if (state.overwrite) {
        state.currentOperand = null;
        state.overwrite = false;
      }
      if (payload.digit === "0" && state.currentOperand === "0") return state;
      if (
        (!state.currentOperand && payload.digit === ".") ||
        (payload.digit === "." && state.currentOperand.includes("."))
      )
        return state;
      return {
        ...state,
        currentOperand: `${state.currentOperand || ""}${payload.digit}`,
      };

    case ACTIONS.CLEAR:
      return {};

    case ACTIONS.CHOOSE_OPERATION:
      if (state.previousOperand == null && state.currentOperand == null)
        return state;
      if (state.currentOperand == null) {
        return {
          ...state,
          operation: payload.operation,
        };
      }
      if (state.previousOperand == null) {
        return {
          ...state,
          operation: payload.operation,
          previousOperand: state.currentOperand,
          currentOperand: null,
        };
      }
      return {
        ...state,
        previousOperand: evaluate(state),
        operation: payload.operation,
        currentOperand: null,
      };

    case ACTIONS.EVALUATE:
      if (
        state.operation == null ||
        state.currentOperand == null ||
        state.previousOperand == null
      ) {
        return state;
      }
      return {
        ...state,
        overwrite: true,
        previousOperand: null,
        operation: null,
        currentOperand: evaluate(state),
      };

    case ACTIONS.DELETE_DIGIT:
      if (state.overwrite) return {};
      if (state.currentOperand == null) return state;
      if (state.currentOperand.length === 1)
        return {
          ...state,
          currentOperand: null,
        };

      return {
        ...state,
        currentOperand: state.currentOperand.slice(0, -1),
      };
  }
}
```

## :crystal_ball: How to use

### It's a classic calculator! 😉

![Main image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/main.png?raw=true)

---

<!--

### 1 - When you access, you will see the Login/SignUp page

![Login image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/login.png?raw=true)

![Signup image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/signup.png?raw=true)

### 2 - After the creation of your account, you will see your tasks

#### The completed tasks have a green accent color

![Signup image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/task_list.png?raw=true)

### 3 - When you create or edit a task, a popup is shown, allowing you to enter the information of the task and submit the changes

![Signup image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/create_or_edit.png?raw=true) -->

<!--
## :fire: Extra features

- [x] Feature 1
- [x] Feature 2
      -->

<!-- ### :file_cabinet: Database diagram

![Database image](https://github.com/gabrielmmf/useReducer-calculator/blob/main/public/readme/diagram.png?raw=true) -->

### :hammer: Technologies

The following tools were used in the construction of the project:

- [React](https://reactjs.org/)

---

## :gear: Services Used

- [Github](https://github.com/) - Code Versioning
<!-- - [Netlify](https://www.netlify.com/) - Frontend deploy -->

---

<!-- ## :lock: Client dependencies

- [Dotenv](https://www.npmjs.com/package/dotenv)
  - Setup environment variables
- [React-cookie](https://www.npmjs.com/package/react-cookie)
  - Setup browser cookies to store the user session with an authentication token

## :closed_lock_with_key: Server dependencies

- [Bcrypt](https:closed_lock_with_key://www.npmjs.com/package/bcrypt)
  - Password encryption and decryption
- [Express](https://www.npmjs.com/package/express)
  - Backend design
- [Dotenv](https://www.npmjs.com/package/dotenv)
  - Setup environment variables
- [Jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)
  - Create authentication token
- [PG](https://www.npmjs.com/package/pg)
  - Connection with PostgreSQL
- [Dotenv](https://www.npmjs.com/package/dotenv)
  - Setup environment variables
- [Uuid](https://www.npmjs.com/package/uuid)
  - Unique id generation

--- -->

### :round_pushpin: Project roadmap

- [x] Create Calculator design
  - [x] Create output div
  - [x] Create Digit and Operation buttons components
- [x] Program calculator logic
  - [x] Create Reducer function for dispatching the action
  - [x] Create evaluate function

---

### :dvd: Running the Project:

<!-- #### You can test the application deployed [here]([netlify-deploy-url])

#### Or you can run it in your system: -->

```bash

$ git clone https://github.com/gabrielmmf/useReducer-calculator

# Access the project folder in terminal/cmd
$ cd useReducer-calculator
# Install the project dependencies
$ npm install
# or
$ yarn install

# Run the development server
$ npm start
# or
$ yarn start
```

Open [http://localhost:3000](http://localhost:3000) to access the app in your browser

---

### :memo: Contributing

Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

After forking the project:

```bash
# Create your Feature Branch:
$ git checkout -b feature/NewFeature
# Commit your change:
$ git commit -m 'Add some Feature'
# Push to the Branch
$ git push origin feature/NewFeature
# Open a Pull Request
```

---

### :boy: Author

<div align="center"> Made with ❤️ by </div>
&nbsp;

<div align="center">
<a href="https://github.com/gabrielmmf">
 <img  width="120px" src="https://avatars.githubusercontent.com/u/77760042?v=4" alt="Gabriel Fialho profile photo"/>
 <br />
 <br />

 <a href="https://github.com/gabrielmmf">
    <img alt="Made by Gabriel Fialho" src="https://img.shields.io/badge/-Gabriel%20Fialho-%237519C1?style=for-the-badge">
  </a>
</div>
&nbsp;
  
 
<div align="center">
    👋🏽 Contact me!
<br/>
<br/>

[![Linkedin Badge](https://img.shields.io/badge/-Gabriel_Fialho-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/gabrielmmfialho/)](https://www.linkedin.com/in/gabrielmmfialho/)

[![Github Badge](https://img.shields.io/badge/-Gabriel_Fialho-000?style=flat-square&logo=Github&logoColor=white&link=https://github.com/gabrielmmf)](https://github.com/gabrielmmf)

</div>

---

### :link: Links

<!-- - Deploy on Netlify: [netlify-deploy-url] -->

- Repository: https://github.com/gabrielmmf/useReducer-calculator

---

### :balance_scale: License

Distributed under the MIT License. See [LICENSE.txt](https://github.com/gabrielmmf/useReducer-calculator/blob/main/LICENSE.txt) for more information.
