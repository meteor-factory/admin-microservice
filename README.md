# Admin Microservice
Pipedream of an easy setup admin as a microservice.

Basically, everything has to be stored in a collection and accessed by a second app. (Or does it..?)

### Setup (optimisitc)

#### Existing Meteor app
1. Install `meteor add admin-microservice` on your main Meteor app

This adds server side code: admin methods, admin publish functions, roles package

#### Admin Meteor app
1. `npm install meteor-admin` installs cli tool
2. `meteor-amin init` generates skeleton admin app, based on github template
3. `MONGO_URL=mongodb://localhost:3001 meteor -p 3100`

Main app scans global variables and stores them in a collection: `AdminCollections`.
Admin app generates config file from this collection
Admin app generates CRUD functionality

### Advantage
* Frontend agnostic
* Much easier to edit code and add templates than in a a package

### The Challenges

#### Getting collection info
1. Via mongo driver
`_.keys(MongoInternals.defaultRemoteCollectionDriver().mongo._observeMultiplexers)` (sometimes misses some depending on state of app)

2. Cycle through top level objects
`Favorites = new Mongo.Collection('favorites');` -> `Favorites._name == 'favorites'`

#### Getting the schemas
##### SimpleSchema
`meteor add admin-collection-2`
`SimpleSchema` instances are converted to JSON and stored in collection

##### No schemas
Can generate Schemas and add create autoforms based on these

##### Astronomy
No idea

#### Other code
Even if the above worked flawlessly (unlikely) it would still be the case that custom publish functions, custom fields didn't work properly.
