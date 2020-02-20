# funk-sdk-nodejs
fun(k) SDK in Node.js

# demo version

Can use from any directory. Currently requires cloud build before deploy step (until buildpacks).

e.g. to build an http funk:

```
> mkdir playground
> cd playground
> kn funk init nodejs
> kn funk function create hello-nodejs --http=true
> cd funks/hello-nodejs
> gcloud builds submit --tag gcr.io/<your-project>/hello-nodejs
> cd ../..
> kn funk deploy
```
Then curl your http funk:
```
curl -v -H "Host: funk-hello-nodejs.default.example.com" <your IP>
```
