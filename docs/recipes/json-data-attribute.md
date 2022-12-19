# Json Data Attribute

<!-- fiddle Get Json Data Attribute -->

Imagine an element that keeps its data serialized inside the attribute `data-field`.

```html
<div id="person" data-field='{"name": "Joe", "age": 10}'>
  First person
</div>
```

Let's check if that object has specific property `age` with value `10`. We need to get the attribute, parse it, then compare the value with the expected one. We should use an assertion callback function to make sure we retry the check if the application changes the attribute value.

```js
cy.get('#person')
  .should('have.attr', 'data-field')
  // the above assertion yields the attribute's value
  .should('be.a', 'string')
  // we want to parse the string and then check
  // the property inside
  .and((s) => {
    const o = JSON.parse(s)
    expect(o, 'parsed').to.have.property('age', 10)
  })
```

<!-- fiddle-end -->
