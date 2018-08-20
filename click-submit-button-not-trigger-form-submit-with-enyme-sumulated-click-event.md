http://airbnb.io/enzyme/docs/api/ShallowWrapper/simulate.html

event simulation for the shallow renderer does not propagate as one would normally expect in a real environment. As a result, one must call .simulate() on the actual node that has the event handler set.

so the form's submit event has to be sumulated to trigger submit action. e.g. 
```
component.find('form').first().simulate('submit');
```
