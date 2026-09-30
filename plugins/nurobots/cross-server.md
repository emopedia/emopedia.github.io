---
title: Cross-Server
nav_order: 9
---

# Cross-Server

NuRobots can share robots across a network, so players see and count the same robots on every server.

## How it works

- Every server connects to the same MySQL, MariaDB or PostgreSQL database.
- **A robot belongs to the server it was placed on.** Only that server runs it, so robots can never produce twice or duplicate items between servers.
- Other servers still see the robot in `/robots manage`, in `/nurobots stats` and in placeholders. Players who try to manage it from the wrong server are told which server it's on.
- Robots that aren't placed can be managed from any server.
- Redis sends changes between servers straight away, so menus and placeholders stay up to date.

## Setup

1. Set up the same database on every server:

   ```yaml
   database:
     type: MYSQL
     host: db.example.com
     port: 3306
     name: nurobots
     user: nurobots
     password: "secret"
   ```

2. Turn on Redis on every server:

   ```yaml
   redis:
     enabled: true
     host: redis.example.com
     port: 6379
     password: "secret"
     channel: "nurobots"
   ```

3. Give each server its own id, or leave it on `auto`:

   ```yaml
   server-id: "survival-1"
   ```

4. Restart the servers.

`/nurobots version` shows the database type, whether Redis is connected and this server's id.

{: .warning }
> Two servers must never share a `server-id`. NuRobots logs an error if it spots another online server using the same one.

SQLite can't be shared between servers, so Redis stays off while SQLite is in use.

## Moving from SQLite

NuRobots doesn't copy data between databases for you. If you switch a single server from SQLite to MySQL, existing robots stay in the old `nurobots.db`.
