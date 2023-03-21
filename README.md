# grc-cms

### Branches
- dev - Development branch where the netlify cms will push the queries, controls and policies changes.
- main - Production branch where changes are going to be pushed by pull requests created from the development branch.

### Flow
When a new push event is sent to either `dev` or `main`, a new workflow is going to be executed. A job will take each 
changed file from the entities' directories (`queries`, `controls`, and `policies`) and will upload it to a storage account blob container. 
Then, for each file it will send an event message that contains the file name, the event type (`modified` or `deleted`), 
the entity slug, and the entity type (`query`, `control`, and `policy`) to a storage account queue.
