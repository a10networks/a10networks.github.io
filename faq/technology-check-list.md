# Technology Check List

## What technology should I use?

### 1.When should I use redux?

**case 1:** 

If view needs to get data from more than one data source.

eg: There is a data list that includes three types of data, each with a different data source. 

**Case2:**

If the UI can vary significantly depending on the state of the application.

eg: There are some traffic charts that will be rendered depending on the time period.

**Case3:**

The state is updated in many different ways.

**Case4:**

The state tree is not simple

**Case5:**

Many unrelated components update state in the same way

**Case6:**

It doesn't always flow in a linear fashion.

**Case7:**

Allow undo for previous user actions.

### 2. When should I use Observable?

#### Case1:

When your architecture has two entity classes, one dependent on the other, and you want them to be non-influential or reusable independently.

#### Case2:

When a changed object notifies an unknown number of objects associated with its own changes

#### Case3:

When a changed object notifies objects that do not need to infer a specific type

refer to: [https://cn.rx.js.org/manual/overview.html\#h12](https://cn.rx.js.org/manual/overview.html#h12)

