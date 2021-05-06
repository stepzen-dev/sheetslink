# sheetslink

This is an example schema that links two Google sheets together via the StepZen @materializer directive. We've added a field named `Players` to the `Team` type like so:
```
Players: [Player]
  @materializer(query:"playersByTeam" arguments:[{name:"team" field:"Team__A"}])
```

In the schema for the `Player` type we've added a query that searches the sheet for players matching the given team: 
```
playersByTeam(team: String!): [Player]
  @rest(endpoint:"https://sheets.apis.stepzen.com/159aOCvUOumcKE1kdRZ-6ohTkbjs2VfSEbSLdUjXDqMk/383008360?q=where%20C%20%3D%20%22$team;%22")

```

The trickiest part is url-encoding the "where" clause we use to define the query. It decodes to:

`where C = "$team;"`