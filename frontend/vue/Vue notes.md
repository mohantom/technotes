Vue notes
------------

- All components are Vue instances? 
- Do not use arrow function in life cycles; 
- can use JFX for template; call function inside template expression? Yes. 
- Dynamic argument binding; 
- computed properties are cached! Watch with denounce; 
- <template v-if>; 
- add key in element to not reuse it;
- v-if and v-for together is not recommended.
- <li is="todo-item">
- Components basics: Using v-model on Components ?
- <slot></slot>: show text inside component <my-comp> some alert </my-comp>
- Dynamic component

```shell script
  <component
    v-bind:is="currentTabComponent"
    class="tab"
  ></component>
```

- Note that objects and arrays in JavaScript are passed by reference, so if the prop is an array or object, mutating the object or array itself inside the child component will affect parent state.
- Binding Native Events to Components: $listeners??.
- Two way binding of attribute: <text-document v-bind:title.sync="doc.title"></text-document>
- Dynamic component: <keep-alive>, keep the state even component is switched off by :is
- Dependency injection: provide, inject  -> Vuex
- Transition: <transition name="fade">
- Mixins
- Webpack: https://webpack.js.org/concepts/modules/#what-is-a-webpack-module
- Vue-test-utils: https://webpack.js.org/concepts/modules/#what-is-a-webpack-module