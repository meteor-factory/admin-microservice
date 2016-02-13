# Admin Microservice
Pipedream of a one-click admin second Meteor instance.

Basically, everything has to be stored in a collection and accessed by a second app. (Or does it..?)

### The Dream
1. Clone repo
2. `MONGO_URL=mongodb://localhost:3001 meteor -p 3100`
3. Enjoy a sexy admin dashboard with schemas, forms and everything else


### The Challenges

#### Getting collection info
1. Via mongo driver
`_.keys(MongoInternals.defaultRemoteCollectionDriver().mongo._observeMultiplexers)` (sometimes misses some depending on state of app)

2. Cycle through top level objects
`Favorites = new Mongo.Collection('favorites');` -> `Favorites._name == 'favorites'`

#### Getting the schemas
`SimpleSchema` is not JSON so difficult to stringify and save in db, but can use [serialize-javascript](https://www.npmjs.com/package/serialize-javascript) to solve this. Although, you need to remove all native functions, replacing `String` with `strings` and then changing back again when you generate schema

#### Other code
Even if the above worked flawlessly (unlikely) it would still be the case that custom publish functions, custom fields didn't work properly .
