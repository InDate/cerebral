# Views
Cerebral supports numerous view layers. They conceptually work the same way, but has different implementation details. Choose the view layer that makes sense to you and your team.

**Cerebrals documentation uses React**

## React
[Website](https://facebook.github.io/react/)

### install

**NPM**

`npm install react react-dom babel-preset-react --save`

**YARN**

`yarn add react react-dom babel-preset-react`

### instantiate
```js
import React from 'react'
import {render} from 'react-dom'
import {Controller} from 'cerebral'
import {Container} from 'cerebral/react'
import App from './App'

const controller = Controller({
  state: {
    foo: 'bar'
  }
})

render((
  <Container controller={controller}>
    <App />
  </Container>
), document.querySelector('#app'))
```

### connect
```js
import React from 'react'
import {connect} from 'cerebral/react'
import {state} from 'cerebral/tags'

// Stateless
export default connect({
  foo: state`foo`
},
  function MyComponent ({foo}) {
    return <div>{foo}</div>
  }
)

// Stateful
export default connect({
  foo: state`foo`
},
  class MyComponent extends React.Component {
    render () {
      return <div>{this.props.foo}</div>
    }
  }
)
```

## Inferno
[Website](http://infernojs.org/)

### install

**NPM**

`npm install inferno inferno-component inferno-create-element babel-plugin-inferno --save`

**YARN**

`yarn add inferno inferno-component inferno-create-element babel-plugin-inferno`

### instantiate
```js
import Inferno from 'react'
import {Controller} from 'cerebral'
import {Container} from 'cerebral/inferno'
import App from './App'

const controller = Controller({
  state: {
    foo: 'bar'
  }
})

Inferno.render((
  <Container controller={controller}>
    <App />
  </Container>
), document.querySelector('#app'))
```

### connect
```js
import Inferno from 'inferno'
import Component from 'inferno-component'
import {connect} from 'cerebral/inferno'
import {state} from 'cerebral/tags'

// Stateless
export default connect({
  foo: state`foo`
},
  function MyComponent ({foo}) {
    return <div>{foo}</div>
  }
)

// Stateful
export default connect({
  foo: state`foo`
},
  class MyComponent extends Component {
    render () {
      return <div>{this.props.foo}</div>
    }
  }
)
```

## Preact (BETA)
[Website](https://github.com/developit/preact)

### install

**NPM**

`npm install preact babel-plugin-transform-react-jsx --save`

**YARN**

`yarn add preact babel-plugin-transform-react-jsx`

### instantiate
```js
import {h, render} from 'preact'
import {Controller} from 'cerebral'
import {Container} from 'cerebral/preact'
import App from './App'

const controller = Controller({
  state: {
    foo: 'bar'
  }
})

render((
  <Container controller={controller}>
    <App />
  </Container>
), document.querySelector('#app'))
```

### connect
```js
import {h, Component} from 'preact'
import {connect} from 'cerebral/preact'
import {state} from 'cerebral/tags'

export default connect({
  foo: state`foo`
},
  class MyComponent extends Component {
    render ({foo}) {
      return <div>{foo}</div>
    }
  }
)
```

## Angularjs (BETA)
[Website](https://angularjs.org/)

### install

**NPM**

`npm install angular --save`

**YARN**

`yarn add angular`

### instantiate
```js
import angular from 'angular'
import {addModule} from 'cerebral/angularjs'

addModule(angular)

angular.module('app', ['cerebral'])
  .config(function (cerebralProvider) {
    cerebralProvider.configure({
      state: {
        foo: 'bar'
      },

      // Special controller property to expose core
      // angular services to your signals
      services: ['$http', '$timeout']
    })
  })
```

### connect
```js
import angular from 'angular'
import {connect} from 'cerebral/angularjs'
import {state} from 'cerebral/tags'

angular.component('myComponent', {
  template: '<div>{{foo}}</div>',
  controller: connect({
    foo: state`foo`
  }, function MyController () {
    // Optionally add custom behaviour to controller
  })
})
```

## Vue (BETA)
[Website](https://vuejs.org/)

### install

**NPM**

`npm install vue --save`

**YARN**

`yarn add vue`

### instantiate
```js
import Vue from 'vue/dist/vue'
import {Controller} from 'cerebral'
import {Container, connect} from 'cerebral/vue'

const controller = Controller({
  state: {
    foo: 'bar'
  }
})

 var app = new Vue({
  el: '#app',
  components: {
    container: Container(controller),
    'my-component': MyComponent
  }
})
```

**Note!** The HTML of the root element must use the *container*:

```html
<div id="app">
  <container>
    <my-component></my-component>
  </container>
</div>
```

### connect
```js
import {connect} from 'cerebral/vue'
import {state} from 'cerebral/tags'

export default connect({
  foo: state`foo`
}, {
  template: '<div>{{foo}}</div>'
})
```
