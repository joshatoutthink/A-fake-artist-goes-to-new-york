# Migration `20200513090709-removing-password`

This migration has been generated by Joshua Kennedy at 5/13/2020, 9:07:09 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "quaint"."new_User" (
    "email" TEXT NOT NULL  ,
    "id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,
    "inRoomId" INTEGER   ,
    "name" TEXT   ,FOREIGN KEY ("inRoomId") REFERENCES "Room"("id") ON DELETE SET NULL ON UPDATE CASCADE
) 

INSERT INTO "quaint"."new_User" ("email", "id", "inRoomId", "name") SELECT "email", "id", "inRoomId", "name" FROM "quaint"."User"

PRAGMA foreign_keys=off;
DROP TABLE "quaint"."User";;
PRAGMA foreign_keys=on

ALTER TABLE "quaint"."new_User" RENAME TO "User";

CREATE UNIQUE INDEX "quaint"."User.email" ON "User"("email")

PRAGMA "quaint".foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200511152350-d..20200513090709-removing-password
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
@@ -13,9 +13,8 @@
 model User {
   id       Int     @default(autoincrement()) @id
   email    String  @unique
   name     String?
-  password String
   rooms    Room[]
   inRoom   Room?   @relation("inRoom", fields: [inRoomId], references: [id])
   inRoomId Int?
 }
```


