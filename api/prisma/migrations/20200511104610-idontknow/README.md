# Migration `20200511104610-idontknow`

This migration has been generated by Joshua Kennedy at 5/11/2020, 10:46:10 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "quaint"."new_Room" (
    "id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL  ,
    "ownerId" INTEGER   ,FOREIGN KEY ("ownerId") REFERENCES "User"("id") ON DELETE SET NULL ON UPDATE CASCADE
) 

INSERT INTO "quaint"."new_Room" ("id", "name", "ownerId") SELECT "id", "name", "ownerId" FROM "quaint"."Room"

PRAGMA foreign_keys=off;
DROP TABLE "quaint"."Room";;
PRAGMA foreign_keys=on

ALTER TABLE "quaint"."new_Room" RENAME TO "Room";

PRAGMA "quaint".foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200511102952-rename-room-field..20200511104610-idontknow
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
@@ -20,7 +20,7 @@
 model Room {
   id      Int    @default(autoincrement()) @id
   name    String
-  user    User   @relation(fields: [ownerId], references: [id])
-  ownerId Int
+  user    User?  @relation(fields: [ownerId], references: [id])
+  ownerId Int?
 }
```


