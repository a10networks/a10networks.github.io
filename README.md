# A10 Unified GUI Framework

UGF is a GUI framework used to build A10networks GUI projects, and is composed of open source software coded in React.js. Our framework promotes for easier debugging, higher performance, and is business-adapted.

Here are the key features from our current release:

1. Design patterns are seamlessly integrated using essential front-end technologies such as React.js, Redux+Observable, Immutable.js, and general logic used by the GUI team. 
2. A separate widgets library called a10-gui-widgets, where all the components inside this library are stateless. These components can only accept data to display. 
3. A stateful components library called a10-gui-common. Our many stateful components in this library result in a small app components of sorts. For example, a Log Auto Gen component, combined with our framework and some parameters, result in an awesome feature!
4. A generator that can help you easily integrate everything together. It can generate frameworks in one key, and can also generate your module containers with your components initial model.  
5. Using our integrated UT framework Jest and E2E testing framework, Nightwatch, developer's can follow examples to easily write your own test cases under your modules!

