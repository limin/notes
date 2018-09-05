Updated with giki  
 A component is changing a controlled input of type text to be uncontrolled
 
 
 if you initially pass undefined or null as the value prop, the component starts life as an "uncontrolled" component. Once you interact with the component, we set a value and react changes it to a "controlled" component, and issues the warning.
 
 solved it by changing value={user.name} to value={user.name || ""} (this.state.location can be empty).
