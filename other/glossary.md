---
description: Main concepts about UGF
---

# Glossary

## UGF

Abbreviation of A10 Unified GUI Framework, used to share GUI architecture across teams, and used to unify Javascript code and CSS style.

## A10 GUI Framework

The main repository of UGF. Defines how to use React, Redux, and other well-known opensource softwares.

The bootstrap code should use the framework code to boot up.

## A10 GUI Widgets

To maintain a cohesive GUI action behavior and design/style across teams. We abstract all React UI components as widgets.

## A10 GUI Common Library

To save a GUI and to share business code with each other, we defined this library where we can access common code--especially common container code!

## A10Provider

A10Provider is a wrapper for React-Redux Provider . A10Provider makes the Redux store available to redux.connect\(\) calls in the component hierarchy below it. We use this wrapper to wire up some global middleware to help system monitor global data \(theme, debug\) or to log critical information.

## A10Root

The place where we can define some global variables like theme, debug toggle, locale etc. and pass them to the whole Virtual-DOM context. A10Root is the ideal place to accept initial configurations defined in a JS file and to send to 1\) Redux and 2\) a component context so that every descendent can access the global variables.

## A10Router

A10Router is a React Router wrapper, simplified from React Router for ease of use.

## A10 Container Interface

A10Container is the heavy-hitter. It is a stateful component that is connected to Redux store. A10Container contains page elements, and could include another A10Container, or A10Widgets, or external \(external to this Framework\) React Components. A10Container is an abstract class that must be implemented.

## A10 Widget Interface

A10 Widgets is a stateless React UI Component library. It is not connected with Redux store and is only concerned with UI ̶ i.e., they are mainly concerned with how things look. Stateless here means that it has nothing to do with data or business logic. It is contained in A10Container or another A10Widget. Generally we can use any possible design pattern to build a A10Widget, example, we can use Adapter design pattern to adapt to Ant Design UI, or use Composite design pattern to compose several other React components or A10Widgets.

## A10 Redux

We imported Redux and added the garbage collection. We can easily revoke all garbages from Redux store. Also, to unify the Redux store namespace, we added Action Type Namespace called redux-action-namespacer.

## Redux Observable

We use it as a middleware of Redux to inject Actions. For example, if we need to handle HTTP request error, we can write Epics to accept the request actions and then have it send out another actions. We use this way to eliminate side effects of Redux.

Detail info see [redux-observable](https://redux-observable.js.org/) official site.

## Redux Namespace

To better organize action type names, the Framework imports an action type name manager called redux-action-namespacer . This NPM package allows developers to structure action types in a logical way.

```jsx
import { createA10ActionTypes } from 'a10-gui-framework'
const actionTypes = [
    'table', [
        'loading',
        'data',
        'query', [
            'sort',
            'limit',
            'search'
        ]
    ]
];
export const ACTIONS = createA10ActionTypes(actionTypes);
```

## Redux with HTTP Request

1. GUI Framework provides a reusable Redux action for asynchronous HTTP data processing.
2. Developers can get a variety of HTTP status actions such as successful HTTP response, HTTP error handling, and gain the ability to cancel previous HTTP requests.
3. GUI Framework manages the life cycle of data in the Redux store for HTTP responses and takes care of their garbage collection when the containers get unmounted.

## A10 Less CSS

CSS infrastructure is important too. A well-maintained and designed CSS infrastructure sustains our GUI products with a unified, cohesive look. A10 GUI framework has a commonly-used LESS CSS \(Referred as Less\) library that allows you to customize some basic design aspects to meet the needs of UI diversity. UI units include primary color, border radius, border color, etc.

Detail info about Less CSS see [http://lesscss.org/](http://lesscss.org/)

