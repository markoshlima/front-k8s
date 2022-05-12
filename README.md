# front-k8s

**Build** <br />
npm run build

**Start** <br />
npm run serve

**Build docker container** <br />
docker build . -t markoshlima/front-k8s<br />
docker build . -t markoshlima/front-k8s --platform linux/amd64 //EKS

**Start docker container** <br />
docker run -it -p 5006:8080 -d markoshlima/front-k8s

**Logs docker container** <br />
docker logs [img]

**Inspect docker image** <br />
docker inspect [img] <br />
docker exec -it [img] /bin/bash

**Stop docker container** <br />
docker stop [img]