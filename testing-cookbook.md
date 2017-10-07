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

**Test **the text of a button of a React component:

```javascript
import {mount, shallow} from "enzyme";
...
wrapper = mount(<MyComponent />)
...
let button = wrapper.find(Button);
expect(button.text()).toEqual("Button Text");
```

**Test **preventDefault functionality in Form components \(given onSubmit function has a `e.preventDefault()` call:

```js
import {spy} from 'sinon'
import {mount} from 'enzyme'
...
const preventDefault = spy();
const wrapper = mount(<Entry />);
wrapper.find(Form).simulate('submit', { preventDefault });
expect(preventDefault.calledOnce).toBeTruthy()
```



