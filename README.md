# React mini store

React mini store for simply project.

# Installation

```
npm install react-mini-store
```
# How to use

#### 1. Write your store action, this is important for you to changed your state.

```javascript
const todos = (state, action) => {
  const type = action.type  
  action['FETCH_TODOS'] = Object.assign({}, state, { todos: action.payload.todos })
  return action[type]
}
export {
  todos
}
```

#### 2. Create your own component store, it wasn't like as redux to auto combine all the reducer in a store.

```javascript
import { createStore } from 'react-mini-store'
import { todos as todo_actions } from './todo-actions'

const ProductStore = new createStore({
  todos: [] // initial state
}, todo_actions)

class TODO extends Component {
  constructor(props, context) {
    super(props, context)

    ProductStore.subscribe(() => { //subscribe your event when you changed the state
      const storeState = ProductStore.getState()
      this.setState(storeState)
    })

    this.state = ProductStore.getState()
  }

  fetch_todos() {
    ProductStore.dispatch({ //only use dispatch to changed your store
      type: 'FETCH_TODOS',
      payload: { todos: [{ name: 'foo' }] }
    })
  }

  render() {
    <div>
      <button onClick={this.fetch_todos}>get todos</button>
      <div>{ this.state.todos }</div>
    </div>
  }
}
```

# License

MIT
