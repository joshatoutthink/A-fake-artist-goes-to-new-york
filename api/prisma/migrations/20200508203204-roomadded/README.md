# Migration `20200508203204-roomadded`

This migration has been generated by Joshua Kennedy at 5/8/2020, 8:32:04 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "quaint"."Room" (
    "active" BOOLEAN NOT NULL  ,
    "id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL  ,
    "ownderId" INTEGER NOT NULL  ,FOREIGN KEY ("ownderId") REFERENCES "User"("id") ON DELETE CASCADE ON UPDATE CASCADE
) 

CREATE UNIQUE INDEX "quaint"."Room.name" ON "Room"("name")

PRAGMA "quaint".foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200508202626-removaloffriends..20200508203204-roomadded
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
@@ -14,5 +14,14 @@
   id       Int     @default(autoincrement()) @id
   email    String  @unique
   name     String?
   password String
+  Room     Room[]
+}
+
+model Room {
+  id       Int     @default(autoincrement()) @id
+  name     String  @unique
+  owner    User    @relation(fields: [ownderId], references: [id])
+  ownderId Int
+  active   Boolean
 }
```


