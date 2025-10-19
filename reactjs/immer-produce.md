### How to Update State Objects in React using immer library's produce

Updating state objects in React can be cumbersome when dealing with nested structures, requiring multiple spread operators and careful immutability handling. The Immer library's `produce` function simplifies this by allowing you to write "mutating" code that automatically produces immutable updates. This makes state management more intuitive and less error-prone, especially for complex nested objects.

The `produce` function takes a draft state and a recipe function. Inside the recipe, you can "mutate" the draft as if it were mutable, and Immer will create a new immutable state based on those changes. This approach is particularly powerful for updating deeply nested objects without the verbose spread syntax.

#### Link
https://immerjs.github.io/immer/

#### Example: Updating Nested State with Immer's produce

```typescript
import { useState } from 'react';
import { produce } from 'immer';

interface User {
  id: number;
  name: string;
  address: {
    street: string;
    city: string;
    country: string;
  };
  hobbies: string[];
}

function UserProfile() {
  const [user, setUser] = useState<User>({
    id: 1,
    name: 'John Doe',
    address: {
      street: '123 Main St',
      city: 'Anytown',
      country: 'USA'
    },
    hobbies: ['reading', 'coding']
  });

  const updateUserName = (newName: string) => {
    setUser(produce(draft => {
      draft.name = newName;
    }));
  };

  const updateAddress = (newStreet: string, newCity: string) => {
    setUser(produce(draft => {
      draft.address.street = newStreet;
      draft.address.city = newCity;
    }));
  };

  const addHobby = (hobby: string) => {
    setUser(produce(draft => {
      draft.hobbies.push(hobby);
    }));
  };

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.address.street}, {user.address.city}, {user.address.country}</p>
      <ul>
        {user.hobbies.map((hobby, index) => (
          <li key={index}>{hobby}</li>
        ))}
      </ul>
      
      <button onClick={() => updateUserName('Jane Doe')}>
        Change Name to Jane
      </button>
      <button onClick={() => updateAddress('456 Oak Ave', 'New City')}>
        Update Address
      </button>
      <button onClick={() => addHobby('gaming')}>
        Add Gaming Hobby
      </button>
    </div>
  );
}
```

<p align="center">
  <a href="https://www.youtube.com/watch?v=zum_ujxFY1Y" target="_blank">
    <img src="https://img.youtube.com/vi/zum_ujxFY1Y/0.jpg" alt="Watch the video" width="600" />
  </a>
</p>

https://www.youtube.com/watch?v=zum_ujxFY1Y