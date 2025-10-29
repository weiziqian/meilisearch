# Description
Modified the behaviour of "TermsMatchingStrategy::Frequency",

Usage example:
```
const searchResults = await index.search(keyword, {
    matchingStrategy: 'frequency',
    ...
});
```

The original behaviour removes the search word from the most frequent one, this will remove from the most infrequent one instead.

The change is based on Meilisearch v1.24.0

# Docker build
```
git checkout git@github.com:weiziqian/meilisearch.git
cd meilisearch
podman build -t meilisearch:latest .

# push to docker hub
docker login
docker tag meilisearch:latest aylwinear/meilisearch:latest
docker push aylwinear/meilisearch:latest

# use
IMAGE="aylwinear/meilisearch:latest"
CONTAINER_NAME=meilisearch
DATA_DIR=./data
MASTER_KEY="MASTER_KEY_XXX"
PORT=7700

podman pull $IMAGE
podman create \
  --name $CONTAINER_NAME \
  -p $PORT:7700 \
  -v $DATA_DIR:/meili_data \
  -e MEILI_MASTER_KEY="$MASTER_KEY" \
  $IMAGE
podman start $CONTAINER_NAME
```
