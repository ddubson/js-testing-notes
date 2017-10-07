# React testing cookbook

**Test**if child component exists in a parent component \(enzyme\)

```js
const wrapper = shallow(<ParentComponent/>);
expect(wrapper.find(ChildComponent).length).toEqual(1)
```



