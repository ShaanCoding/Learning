# Prisma Tutorial - Modelling Relationships

Source: https://www.youtube.com/watch?v=fpBYj55-zd8

## 1 to 1 Relationship

```prisma
model User {
    id Int @id @default(autoincrement())
    email String @unique
    profile Profile?
}

model Profile {
    name String
    gender String
    age String

    userId Int @unique
    user User @relation(fields: [userId], references: [id])
}
```

- A user can have one profile and a profile can have one user
  - It references profile model
  - and on the profile field we have the user field that references the user model
    - Then we have an extra field called the userId which links the two models together

```ts
prisma.user.findMany({
  include: {
    profile: true,
  },
});
```

## 1 to Many Relationship

```prisma
model User {
    id Int @id @default(autoincrement())
    email String @unique
    posts Post[]
}

model Post {
    title String
    userId Int @unique
    user User @relation(fields: [userId], references: [id])
}
```

- User can have many posts but a post can only have one user

```ts
prisma.user.findMany({
  include: {
    posts: true,
  },
});
```

## Implicit Many to Many Relationship

```prisma
model Post {
    id Int @id @default(autoincrement())
    title String
    tags Tag[]
}

model Tag {
    id Int @id @default(autoincrement())
    posts Post[]
}
```

- Many different posts to many different tags
  - Normally when you model something like this you'll have an intermediary table which will have the post id and the tag id
  - In Implicit Many to Many Relationship, Prisma will create this intermediary table for you
    - Under the hood Prisma will create a table called PostTag

```ts
prisma.post.findMany({
  include: {
    tags: true,
  },
});
```

## Explicit Many to Many Relationship

```prisma
model Post {
    id Int @id @default(autoincrement())
    title String
    tags PostTag[]
}

model Tag {
    id Int @id @default(autoincrement())
    name String
    posts PostTag[]
}

model PostTag {
    postId Int
    post Post @relation(fields: [postId], references: [id])

    tagId Int
    tag Tag @relation(fields: [tagId], references: [id])
}
```

- In the explicit many to many relationship, we have a PostTag model
  - This model has a postId and a tagId
  - It also has a post field which references the post model
  - and a tag field which references the tag model

```ts
prisma.post.findMany({
  include: {
    tags: true,
  },
});
```
