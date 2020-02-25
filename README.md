# funk-sdk-nodejs
fun(k) SDK in Node.js

Can use from any directory. Currently requires separate gcloud build (or docker build) before deploy step (until buildpacks integrated).

# demo http funk

```
$ mkdir playground
$ cd playground
$ kn funk init nodejs
$ kn funk function create hello-nodejs --http=true
$ gcloud builds submit funks/hello-nodejs --tag $KO_DOCKER_REPO/hello-nodejs
$ kn funk deploy
```
Then curl your http funk:
```
$ curl -v -H "Host: funk-hello-nodejs.default.example.com" <your IP>
```

# demo event funk
(the first 3 steps aren't necessary if this is the 2nd funk)
```
$ mkdir playground
$ cd playground
$ kn funk init nodejs
$ kn funk function create nodejs-hello-event --t com.mikehelmick.eventutils.user.user
$ gcloud builds submit funks/nodejs-hello-event --tag $KO_DOCKER_REPO/nodejs-hello-event
$ kn funk deploy
```
then create an event to test your funk. This assumes you've created a curl pod per https://knative.dev/docs/eventing/getting-started/
```
$ kubectl --namespace default attach curl -it
[ root@curl:/ ]$ curl -v "http://default-broker.default.svc.cluster.local" \
  -X POST \
  -H "Ce-Id: foo" \
  -H "Ce-Type: com.mikehelmick.eventutils.user.user" \
  -H "Ce-Source: /bar" \
  -H "Content-Type: application/cloudevents+json; charset=utf-8" \
  -d '{"specversion": "1.0", "id": "foo", "source": "/bar", "type": "com.mikehelmick.eventutils.user.user", "datacontenttype": "application/json", "data": {"first_name":"Paul", "last_name":"Blart"}}'
