# Authentication
The main script is the [[Authentication]] application. This flask application will take in most of the requests from the website and see if the user trying to send that request has the level of clearance necessary. An example of this would be if a crew member is trying to make a change to a tournament, then the [[Authentication]] API will firstly validate the level of clearance of the user. Afterwards, the request will either be redirect to the [[Tournaments]] API or it will return an error and the front-end will tell the user that it cannot perform the action.

### Levels of clearance
| Value in database | Name of role  | Permissions granted (written)                                           | Routes granted                                                |
| ----------------- | ------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------- |
| 1                 | Default       | None                                                                    | None                                                          |
| 2                 | Program       | Ability to create, update and delete tournaments                        | 'createtourney', 'delete_tournament', and 'update_tournament' |
| 3                 | Program Leder | Create, remove, and update every single tournament                      | 'createtourney', 'delete_tournament', and 'update_tournament' |
| 4                 | Teknisk       | Same as Program Leder, but also gives access to use the ticket website. | 'createtourney', 'delete_tournament', 'update_tournament',    |
| 5                 | Admin         | Everything                                                              | All                                                           |

### What needs to happen
- Request reaches auth
- Find user that sent the request
- Get clearance of user
- Check if the user has access to the route they are trying to access
- Redirect request to appropriate API


# Tournaments
The Tournaments API is meant to only act as a CRUD application. It is responsible for taking in requests and either Creating tournaments, Returning all the tournaments, Updating a tournament, or Deleting a tournament from the database.