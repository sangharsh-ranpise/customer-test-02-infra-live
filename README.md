For testing on 1 repo follow below steps
copy atlantis.yaml.bk content and create a file - atlanstic.yaml and copy in this file(only for testing) 
Create SSH keys and in github go to  repos path/settings/deploy keys and add new key with the public ssh key
go to main settings/developer settings and create PAT classic and save the token 
start ngrok at 4141

 run this 
 docker run -it --rm \
  -p 4141:4141 \
  -v /home/sangharsh/sangharsh-workspace/test-01-delete/ssh_keys/atlantis_key:/atlantis_key \
  -v /home/sangharsh/sangharsh-workspace/test-01-delete/server.yaml:/etc/atlantis/server.yaml \
  -e ATLANTIS_GIT_SSH_KEY="$(cat /home/sangharsh/sangharsh-workspace/test-01-delete/ssh_keys/atlantis_key)" \
  -e ATLANTIS_GH_USER="USER_NAME" \
  -e ATLANTIS_GH_TOKEN="PAT" \
  -e ATLANTIS_GH_WEBHOOK_SECRET="SECRET" \
  runatlantis/atlantis server \
  --repo-allowlist="github.com/USER_NAME/customer-test-02-infra-live" \
  --config /etc/atlantis/server.yaml

  or 

  docker run -it --rm \
  -p 4141:4141 \
  -v /home/sangharsh/sangharsh-workspace/test-01-delete/ssh_keys/atlantis_key:/atlantis_key \
  -v /home/sangharsh/sangharsh-workspace/test-01-delete/server.yaml:/etc/atlantis/server.yaml \
  -e ATLANTIS_GIT_SSH_KEY="$(cat /home/sangharsh/sangharsh-workspace/test-01-delete/ssh_keys/atlantis_key)" \
  -e ATLANTIS_GH_USER="USER_NAME" \
  -e ATLANTIS_GH_TOKEN="PAT" \
  -e ATLANTIS_GH_WEBHOOK_SECRET="SECRET" \
  runatlantis/atlantis server \
  --repo-allowlist="github.com/sangharsh-ranpise/customer-test-02-infra-live" \
  --repo-config /etc/atlantis/server.yaml

  update a .tf file and create PR