```
"use strict"

class User{
  // methods that will run once class is instanciated(object is created)
  constructor(username, email, password) {
    this.username = username;
    this.email = email;
    this.password = password;
  }

  // static method
  static countUsers() {
    console.log('You are all platypi');
  }

  // you can create methods inside a class.
  register(){
    console.log(this.username + ' is now registered.')
  }
}

let bob = new User('bob', 'buckfob@shit.net', '12345');

bob.register(); // bob is now registered. 
User.countUsers(); // You are all platypi

class Member extends User {
  constructor(username, email, password, Package) {
  	// must use super in derived classes.
    super(username, email, password);
    this.package = Package;
  }

  getPackage() {
    console.log(this.username + ' is a fucking ' + this.package)
  }
}

let earl = new Member('earl', 'dfas@ei.net', '12345', 'lunatic');

earl.getPackage(); // earl is a fucking lunatic 
earl.register(); // earl is now registered. 
```