Development
--------------

- will be dropping Message table in Postgres; fuck it, let the messages roll into Cassandra
- Fixed discussion insertion, and sync up with the Message(Post in Cass)
- Refactored the Background task to select data from Cassandra rather than Postgres
