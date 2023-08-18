# grc-cms

### Branches

- dev - Development branch where the netlify cms will push the queries, controls and policies changes.
- main - Production branch where changes are going to be pushed by pull requests created from the development branch.

### Flow

When a new push event is sent to either `dev` or `main`, a new workflow is going to be executed. A job will take each
changed file from the entities' directories (`queries`, `controls`, and `policies`) and will upload it to a storage account blob container.
Then, for each file it will send an event message that contains the file name, the event type (`modified` or `deleted`),
the entity slug, and the entity type (`query`, `control`, and `policy`) to a storage account queue.

### Deploy to Prod

We must rebase the changes from dev to main (or any other branch such as QA). This must be done **locally**, otherwise GitHub creates separate commits due to different authors.

- `git checkout dev`
- `git pull`
- `git checkout main`
- `git pull`
- `git rebase dev` (or the hash of a previous commit if you don't want to deploy the latest changes)
- `git push`

A deployment will automatically be created, but it has to be approved by @andreimilas or @AndreiStefanie.
