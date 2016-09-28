# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
  Join tables allow you to access information in two tables by only having to
  access one of the tables.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
Profiles
  given_name
  surname
  email
  nickname


 Movies
  title
  relsease_date
  length

Favorites
  movie_id
  profile_id



```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
has_many: Movies through: Favorites
has_many: Favorites
end
```

```rb
class Movie < ActiveRecord::Base
has_many: Profiles through: Favorites
has_many: Favorites
end
```

```rb
class Favorite < ActiveRecord::Base
belongs_to :profile, inverse_of: :Favorites
belongs_to :movie, inverse_of: :Favorites
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh


 A Serializer is like a filter that only allows the client to see what you want
```

```rb
class ProfileSerializer < ActiveModel::Serializer
  attributes :id, :title, :profile_id
  has_many :favorites
  has_many :movies
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
bundle exec rails g scaffold favorites movie:references profile:references

```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
  When you delete a class you also want to delete any associated objects.
  Like patients and records.
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
  Many to one - A online journal where the user can have many entries but
  entries can only be made by one user.

  Many to many- A 
```
