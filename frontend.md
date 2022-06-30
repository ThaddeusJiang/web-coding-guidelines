# Frontend Coding guidelines

- [Frontend Coding guidelines](#frontend-coding-guidelines)
  - [Basic](#basic)
  - [Code Format](#code-format)
  - [Naming](#naming)
  - [CSS](#css)
  - [Testing](#testing)
    - [Must](#must)
      - [1. the logic code is nested.](#1-the-logic-code-is-nested)
    - [Unit Testing](#unit-testing)
      - [user-event](#user-event)
      - [custom render](#custom-render)
  - [Form](#form)
  - [React](#react)
    - [1. Write children in Props if it is necessary, Don't use `React.FC`.](#1-write-children-in-props-if-it-is-necessary-dont-use-reactfc)
    - [2. Primary handle functions should not be optional](#2-primary-handle-functions-should-not-be-optional)
    - [3. useEffect tip: don't](#3-useeffect-tip-dont)
  - [File Structure](#file-structure)
  - [i18n](#i18n)

## Basic

* JavaScript Style Guide: [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
* TypeScript coding guidelines: [jaredpalmer/typescript](https://github.com/jaredpalmer/typescript)
* [Naming cheatsheet](https://github.com/kettanaito/naming-cheatsheet)

## Code Format

1. JS file lines limit 400.

## Naming

- Data Sync use suffix `Query` and `Mutation`, like: userQuery, usersQuery, createUserMutation, updateUserMutation.

## CSS

1. Use utility-first CSS ([tailwindcss](https://tailwindcss.com/docs/utility-first)).
    1. Don't construct class names dynamically, Always use complete class names. see [tailwind document](https://tailwindcss.com/docs/content-configuration#dynamic-class-names)
    2. Use unprefixed utilities to target mobile, and override them at larger breakpoints. see [document](https://tailwindcss.com/docs/responsive-design#targeting-mobile-screens)
    3. Extracting classes with @apply is last resort [document](https://tailwindcss.com/docs/reusing-styles#avoiding-premature-abstraction)
2. Don't use SCSS, Less and CSS-in-JS.
3. Don't use `fontWeight: 500`, because a lot of issues.

## Testing

### Must

#### 1. the logic code is nested.

```ts
// Must write test
const onCheckedChange = (checked: boolean) => {
  updateTask.mutate({
    ...todo,
    tasks: todo.tasks?.map((t) =>
      t.id === task.id
        ? {
            ...t,
            items: t.items.map((taskItem, itemIndex) =>
              itemIndex === idx
                ? { ...taskItem, checked }
                : taskItem
            ),
          }
        : t
    ),
  });
};
```

### Unit Testing

https://testing-library.com/docs/react-testing-library/example-intro

1. mock and setup inside of the test itself.
2. recommend [user-event](https://testing-library.com/docs/user-event/intro)
3. don't use `test-id`

#### user-event

```js
import userEvent from "@testing-library/user-event";

test("renders", () => {
    const user = userEvent.setup();

    user.click(getByText("register"));
})
```

#### custom render

```js
import { render } from "../../utils/testUtils";
```


## Form

1. schema validation.
2. first validation after first submit.
3. real validation after submit.

## React

### 1. Write children in Props if it is necessary, Don't use `React.FC`.

https://stackoverflow.com/questions/71788254/react-18-typescript-children-fc/71809927#71809927

### 2. Primary handle functions should not be optional

bad code

```ts
type Props = {
  onOk?: Function
}

if (onOk) {
  onOk();
}
```

good code

```ts
type Props = {
  onOk: Function
}

onOk();
```

### 3. useEffect tip: don't

bad

```js
TODO:
```

good

```js
TODO:
```

## File Structure

- reference [Redwood File Structure](https://redwoodjs.com/docs/tutorial/chapter1/file-structure)
- Don’t overthink it.
- Structure files of changed together.

## i18n

* key must lowercase, like: "hello world", "system settings".
