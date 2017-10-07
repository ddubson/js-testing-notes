# React testing cookbook

**Test **if a child component exists in a parent component \(enzyme\)

```js
import {shallow} from 'enzyme';
...

const wrapper = shallow(<ParentComponent/>);
expect(wrapper.find(ChildComponent).length).toEqual(1)
```

Test the contents of a variable in the component state

```js
const wrapper = mount(<App/>);
expect(wrapper.state().myStateVariable).toEqual(0)
```



