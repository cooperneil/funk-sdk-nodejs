# funk-sdk-nodejs
fun(k) SDK in Node.js

# demo version

Can use from any directory. Currently requires cloud build before deploy step (until buildpacks).

e.g.

```
> mkdir playground
> cd playground
> kn funk init nodejs
> kn funk function create hello-nodejs --http=true
> cd funks/hello-nodejs
> gcloud builds submit --tag gcr.io/neilcooper-knative-dev2/hello-nodejs
> cd ../..
> kn funk deploy
```
