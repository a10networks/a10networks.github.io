# Technology Check List

## What technology should I use?

### 1.When should I use  redux ?

**case 1:** 

If view need get data from one more data source.

eg: There is a data list, which includes three types data and those data has different data source.

**Case2:**

If the UI can vary significantly depending on the state of the application.

eg: There are some traffic charts, which will rendered depending on the time period.

**Case3:**

The state is updated in many different ways.

eg: TODO

**Case4:**

The state tree is not simple

eg: TODO

* When should I use Observable?

**Case5:**

Many unrelated components update state in the same way

eg:TODO

**Case6:**

It doesn't always flow in a linear.

eg: TODO

**Case7:**

Need to be able to undo previous user actions.

eg: TODO

