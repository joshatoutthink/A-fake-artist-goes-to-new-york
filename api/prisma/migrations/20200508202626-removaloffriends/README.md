# Migration `20200508202626-removaloffriends`

This migration has been generated by Joshua Kennedy at 5/8/2020, 8:26:26 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql

```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200508155133-added-friends..20200508202626-removaloffriends
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource DS {
   provider = "sqlite"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator client {
   provider      = "prisma-client-js"
@@ -10,16 +10,9 @@
 // Define your own datamodels here and run `yarn redwood db save` to create
 // migrations for them.
 model User {
-  id       Int      @default(autoincrement()) @id
-  email    String   @unique
+  id       Int     @default(autoincrement()) @id
+  email    String  @unique
   name     String?
   password String
-  friends  Friend[]
-}
-
-model Friend {
-  id     Int  @default(autoincrement()) @id
-  user   User @relation(fields: [userId], references: [id])
-  userId Int
 }
```


