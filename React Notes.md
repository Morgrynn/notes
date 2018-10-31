# React Notes

* React is a JavaScript library
* React is not a framework (unlike Angular, which is more opinionated) :
* React is an open-source project created ny FB
* React is used to build user interfaces (UI) on the front end.
* React is the **view** layer of an MCV application (Model View Controller)

One of the most important aspects of React is the fact that you can create **components**,
which are like custom, reusable HTML elements, to quickly and efficiently build user interfaces.
React also streamlines how data is stored and handled, using **state** and **props**.


### Props

Passing **props** is how information flows in React apps, from parent to children.

```
{this.props.value}

```

### State

To "remember" things, components use **state**.

React components can have state by setting this.state in their constructors.
this.state should be considered as provate to a React component that it's defined in.

**Note**
In JavaScript classes, you need to always call _super_ when defining the constructor of a subclass.
All React components classes that have a _constructor_ should start it with a _super(props)_ call.

When you call _setState_ in a component, React automatically updates the child components inside of it too.

---
**Lifting State Up**
To collect data from multiple shildren, or to have two child components communicate
with each other, you need to declare the shared state in their parent component instead.
The parent component can pass the state back down to the children by props; this
keeps the child components in sync with each other and with the parent component.



**Note**
The DOM <button> element's onClick attribute has a special meaning to React because it is
a built-in component. For cusotm components like Square, the meaning is up to you. We could name the Square's onClick prop or Board's handleClick method differently. In React, however, it is a convention to use on[Event] names for props which represent events and handle[Events] for the mthods which handle the events.

A class component must include _render()_, and the _return_ can only return one parent element.

Let's compare a simple component with a class component.

```
Simple Component

const SimpleComponent = () => {
    return <div>Example</div>;
}

```

```
Class Component

class ClassComponent extends Component {
    render() {
        return <div>Example</div>;
    }
}

```

**Note** that the _return_ is contained to one line, it does not need parenthesis.

## Keys

Keys help React identify which items have changed, are added, or are removed.
Keys should be given to the elements inside the array to give the elements a stable identity:

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) => 
    <li key={number.toString()}>
    {number}
    </li>
);
```

The best way to pick a key is to use a string that uniquely identifies a list item among 
it's siblings. Most often you would use IDs from your data as keys:

```
const todoItems = todos.map((todo) =>
    <li key={todo.id}>
    {todo.text}
    </li>
);
```

A good rule of thumb is that elements inside the _map()_ call need keys.

## State

If you want to be able to delete an item from the array. We use state. With props, 
we have a one way data flow, but with state we can update provate data from a component.

You can think of state as any data that should be saved asn modified without necessarily being added 
to a database - for example, adding and removing items from a shopping cart before confirming your purchase.

You must use _this.setState()_ to modify an array. Simply applying a new value to 
_this.state.property_ will not work.

