# React testing cookbook

Access a component function:

```javascript
const wrapper = mount(<App />)
wrapper.instance().myComponentFunction
```

## Test Scenarios

**Test **if a child component exists in a parent component \(enzyme\)

```js
import {shallow} from 'enzyme';
...
const wrapper = shallow(<ParentComponent/>);
expect(wrapper.find(ChildComponent).length).toEqual(1)
```

**Test** the contents of a variable in the component state

```js
import {mount} from 'enzyme';
...
const wrapper = mount(<App/>);
expect(wrapper.state().myStateVariable).toEqual("my state variable")
```

**Test **if a child component has a function passed down via props from the parent component

```js
import {mount} from 'enzyme';
...

class App extends React.Component {
    myFunction() { console.log("does something"): }
    
    render() {
        return ( <div><MyComponent myFunction={this.myFunction} /></div> )
    }
}

...
const wrapper = mount(<App/>);
expect(wrapper.find(MyComponent).prop('myFunction')).toBe(wrapper.instance().myFunction)
```



