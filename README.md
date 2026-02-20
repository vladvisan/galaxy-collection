# Galaxy Collection for Ansible

## Development

Currently, all roles (inside `roles/`) are Git submodules, and work on the roles themselves should take place in the upstream Role repository.

They are, for now, only the ones mentioned in https://training.galaxyproject.org/training-material/topics/admin/tutorials/ansible-galaxy/tutorial.html and https://training.galaxyproject.org/training-material/topics/admin/tutorials/job-destinations/tutorial.html, and are also available as publishes roles at https://galaxy.ansible.com/ui/standalone/namespaces/2450 and https://galaxy.ansible.com/ui/standalone/namespaces/10048

### Pushing a new version

Before tagging a new version, make sure all the git submodules are up to date:

    git submodule update --recursive --remote

Then commit and push all changes, and make sure all tests are passing.

Then tag the new version of the collection, push the tag, and deploy the new collection version using the playbook in `scripts/deploy.yml`. That directory also contains the `galaxy.yml` template that will be used to build the collection metadata.

**NB: if you want to publish using a different namespace and/or collection-name, modify scripts/deploy.yml and scripts/templates/galaxy.yml.j2**

Example (you get the Ansible-Galaxy token here: https://galaxy.ansible.com/ui/token/)
``` 
tag=0.1.0
git tag $tag
git push origin --tags
source ~/venv_ansible/bin/activate
ANSIBLE_GALAXY_TOKEN=X ansible-playbook scripts/deploy.yml --extra-vars "tag=$tag"
```
TODO: add a script for this?

## Synchronising the github repo from our gitlab repo

```
git remote add origin2 git@github.com:vladvisan/galaxy-collection.git
git push -u origin2 main
```

## Credits

The structure, and non-galaxy-specific content of this repo is greatly based on https://github.com/geerlingguy/ansible-collection-k8s
