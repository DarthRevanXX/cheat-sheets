- Create an entity file, and create a class in it that lists all the properties that your entity will have
- Connect the entity to it parent module. This creates a repository
- Connect the entity to the root connection (in app module)

Entity naming, for example for use "class User"

Example User

```
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

  

@Entity()

export class User {

  @PrimaryGeneratedColumn()

  id: number;

  

  @Column()

  name: string;

  

  @Column()

  email: string;

  

  @Column()

  password: string;

}
```

