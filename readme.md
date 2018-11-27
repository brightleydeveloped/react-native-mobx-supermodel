react-supermodel
================
react-supermodel uses mobx to create observable models and collections
 


`npm install react-supermodel --save`

Model example:

```javascript
// src/models/user
import { Model } from 'react-supermodel';
import { observable } from 'mobx';

export class User extends Model {
    
    options() { 
        return {
            baseUrl: 'https://<api-server-url>',
            basePath: '/api/v1',
            resource: 'user'
        }
    }
    
    fields() {
        return {
            name: ''
        };
    }
}

// somewhere else


// this will make a request to https://<api-server-url>/api/v1/user/:id
// to fetch one model from the server
const user = new User();
user.id = 'some-uuid';
user.fetch();

// or, you can define the id as an option
const user = new User({
    fields: {
        id: 'some-uuid'
    }
});
user.fetch();


// to save, will make a POST request to https://<api-server-url>/api/v1/user
// or a PUT request to the https://<api-server-url>/api/v1/user/:id if id is set
user.save()
```


Collection:

```javascript
// src/collections/user
import { Collection } from 'react-supermodel';
import User from '../models/user';

export class UserCollection extends Model {
    static Model = User;
}

// somewhere else
const users = new UserCollection();
users.fetch();
```
