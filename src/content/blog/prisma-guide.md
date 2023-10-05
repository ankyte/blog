---
author: Ankit Sahu
pubDatetime: 2023-07-30T00:00:00Z
title: Mastering Prisma ( A Comprehensive Guide for Beginners )
postSlug: prisma-guide
featured: false
draft: false
tags:
  - typescript
  - prisma
  - react
description: Prisma - the ultimate tool that will revolutionize your backend development journey! This comprehensive guide will take you through every step, from the initial setup to mastering the art of database management with Prisma.
---

Prisma - the ultimate tool that will revolutionize your backend development journey! This comprehensive guide will take you through every step, from the initial setup to mastering the art of database management with Prisma.

## Table of contents

## 🚀 **Initializing the Project** 🚀

To kick off our journey with Prisma, let's start by creating a new project and installing the necessary dependencies. Open your terminal and run the following commands:

```bash
yarn init -y
yarn add --dev typescript ts-node @types/node nodemon
```

Next, let's initialize TypeScript in our project and add the Prisma CLI:

```bash
yarn tsc --init
yarn add --dev prisma
```

Now, we need to set up Prisma to work with PostgreSQL:

```bash
yarn prisma init --datasource-provider postgresql
```

## 📊 **Creating a Basic Model** 📊

Once Prisma is set up, let's create a simple model in the `_schema.prisma` file. In this example, we'll create a `User` model with an `id` and a `name`:

```prisma
model User {
  id   Int    @id @default(autoincrement())
  name String
}
```

After defining the model, it's time to create the corresponding database tables using Prisma Migrate:

```bash
yarn prisma migrate dev --name init
```

## 📝 **Sending Queries to the Database** 📝

Now, let's explore how to interact with the database using Prisma Client. Create a file called `script.ts` and add the following code:

```typescript
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

async function main() {
  // ... you will write your Prisma Client queries here
}

main()
  .catch(e => {
    console.log(e.message);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

In the `script.ts` file, you can use Prisma Client to send queries to the database. For example, to add a new user, you can use the following code:

```typescript
const user = await prisma.user.create({ data: { name: "Steve Rogers" } });
```

And to retrieve all users from the database:

```typescript
const users = await prisma.user.findMany();
console.log(users);
```

💡 **Tip**: Don't forget to install the Prisma Client and generate the Prisma Client code before running the script:

```bash
yarn add @prisma/client
yarn prisma generate
```

## 🎉 **Adding Nodemon for Automatic Refresh** 🎉

To make development more efficient, let's set up Nodemon to automatically refresh the script when changes are made. Add the following script to your `package.json`:

```json
"scripts": {
  "devStart": "nodemon script.ts"
}
```

Now, you can run the following command to start your development server:

```bash
yarn devStart
```

## ✨ **Advanced Schema with Relations and Enums** ✨

Now, let's dive into more advanced concepts in Prisma and create a schema with relations and an enum. You can use this as a reference for building more complex data models.

```prisma
// SCHEMA
model User {
  id               String          @id @default(uuid())
  name             String
  age              Int
  email            String          @unique
  isAdmin          Role            @default(BASIC)
  authoredPosts    Post[]          @relation("AuthoredPosts") // One to Many
  bookmarkedPosts  Post[]          @relation("BookmarkedPosts")
  userPreference   UserPreference? @relation(fields: [userPreferenceId], references: [id])
  userPreferenceId String?         @unique

  @@unique([email, name])
  @@index([email])
}

// One to One Relation
model UserPreference {
  id           String  @id @default(uuid())
  user         User?
  emailUpdates Boolean @default(false)
}

model Post {
  id             String     @id @default(uuid())
  title          String
  rating         Float
  createdAt      DateTime   @default(now())
  updatedAt      DateTime   @updatedAt
  author         User       @relation("AuthoredPosts", fields: [authorId], references: [id])
  authorId       String
  bookmarkedBy   User?      @relation("BookmarkedPosts", fields: [bookmarkedById], references: [id])
  bookmarkedById String?
  categories     Category[]
}

// Many to Many Relation
model Category {
  id    String @id @default(uuid())
  posts Post[]
}

enum Role {
  BASIC
  ADMIN
}
```

## 🛠️ **CRUD Operations with Prisma Client** 🛠️

To perform CRUD (Create, Read, Update, Delete) operations using Prisma Client, let's dive into some code examples.

**Creating a User:**

```typescript
async function create() {
  const user = await prisma.user.create({
    data: {
      name: "Lizard Zuck",
      email: "zuckiscuck@gmail.com",
      userPreference: {
        create: {
          emailUpdates: true,
        },
      },
    },
    select: {
      name: true,
      userPreference: { select: { id: true } },
    },
  });
  return user;
}
```

**Reading a User by Email:**

```typescript
const user = await prisma.user.findUnique({
  where: {
    email: "ankit1042002@gmail.com",
  },
});
console.log(user);
```

**Filtering Users with Complex Conditions:**

```typescript
const user = await prisma.user.findMany({
  where: {
    name: { not: "Ankit" },
    age: { lt: 20 }, // lt -> less than
    email: { contains: "@gmail.com", startsWith: "an" },
  },
});
```

**Updating User Data:**

```typescript
const updatedUser = await prisma.user.update({
  where: {
    email_name: {
      email: "ankit.ks@yahoo.com",
      name: "Ankit",
    },
  },
  data: {
    email: "ankit.ks@yahoo.com",
  },
});
console.log(updatedUser);
```

**Deleting a User:**

```typescript
const deletedUser = await prisma.user.delete({
  where: {
    email_name: {
      email: "ankit.ks@yahoo.com",
      name: "Ankit",
    },
  },
});
console.log(deletedUser);
```

## 🔗 **Connecting and Disconnecting Relations** 🔗

To connect and disconnect relations, such as connecting a `User` to their `UserPreference`, you can use the following examples:

**Connecting UserPreference:**

```typescript
const preference = await prisma.userPreference.create({
  data: {
    emailUpdates: true,
  },
});

const user = await prisma.user.update({
  where: {
    email_name: {
      email: "ankit.ks@yahoo.com",
      name: "Ankit",
    },
  },
  data: {
    userPreference: {
      connect: {
        id: preference.id,
      },
    },
  },
});
```

**Disconnecting UserPreference:**

```typescript
const user = await prisma.user.update({
  where: {
    email_name: {
      name: "Ankit",
      email: "ankit.ks@yahoo.com",
    },
  },
  data: {
    userPreference: {
      disconnect: true,
    },
  },
});
```

## 🔍 **Fetching Posts with Relations** 🔍

To fetch posts related to users, you can use Prisma Client to perform queries like this:

```typescript
async function main() {
  const posts = await prisma.user.findMany({
    where: {
      authoredPosts: {
        every: {
          title: {
            startsWith: "T",
          },
        },
      },
    },
  });
  console.log(posts);
}
```

## 📄 **Conclusion** 📄

Congratulations! You've now learned the essentials of using Prisma.
Now, my coding Jedi, may the Prisma force be with you. Remember, even Darth Bugs will fear your skills!.
