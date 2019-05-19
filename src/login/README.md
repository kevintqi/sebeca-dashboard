
### configuration file
````
<local-path>/src/configuration/login-config.json
````
example:
````
{
  "userPoolId": "us-west-2_02Example",
  "clientId": "1iuo0nj25igfm6s0mExample",
  "identityPoolId": "us-west-2:0e36de8d-Example",
  "region": "us-west-2"
}
````
### Listen to events for updates
````
window.dispatchEvent(new CustomEvent('aws-login-user-update', {
  detail: {
    'email': user.email,
    'role': user.role,
    'userPoolId': user.userPoolId,
    'userIdToken': user.userIdToken
  }
}));
````
Code to register for the update event
````
ready() {
  super.ready();
  window.addEventListener('aws-login-user-update', e => {
    this._handleUserUpdate(e.detail);
  });
}

_handleUserUpdate(user) {
  this.set('user', user);
  console.log("new user <echo>: ", this.user.email);
  console.log("new role <echo>: ", this.user.role);
  console.log("new userPoolId <echo>: ", this.user.userPoolId);
  console.log("new userIdToken <echo>: ", this.user.userIdToken);
}
````