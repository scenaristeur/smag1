- https://communitysolidserver.github.io/CommunitySolidServer

! erreur d'adresse de login ! http://localhost:3000/idp/login/

following tuto
- https://github.com/CommunitySolidServer/tutorials/blob/main/getting-started.md#getting-started
```
git clone https://github.com/CommunitySolidServer/CommunitySolidServer.git
cd CommunitySolidServer
npm ci

npm start # memory

```
test 
```
curl http://localhost:3000/

curl -H "Accept: application/n-triples"  http://localhost:3000/


curl -v -X POST -H "Content-Type: text/plain" -d "abc" http://localhost:3000/
# see response.location
http://localhost:3000/7b46b9a1-5792-4407-9502-df14d4bb6193

curl -v -X POST -H "Slug: custom" -H "Content-Type: text/plain" -d "abc" http://localhost:3000/
# Location: http://localhost:3000/custom
curl -X PUT -H "Content-Type: text/turtle" -d "<ex:s> <ex:p> <ex:o>." http://localhost:3000/a/b/c
curl -X PUT -H "Content-Type: text/turtle" -d "<ex:s2> <ex:p2> <ex:o2>." http://localhost:3000/a/b/c
#append 
curl -X PATCH -H "Content-Type: text/n3" --data-raw "@prefix solid: <http://www.w3.org/ns/solid/terms#>. _:rename a solid:InsertDeletePatch; solid:inserts { <ex:s3> <ex:p3> <ex:o3>. }." http://localhost:3000/a/b/c
# same as curl -X PATCH -H "Content-Type: application/sparql-update" -d "INSERT DATA { <ex:s3> <ex:p3> <ex:o3> }" http://localhost:3000/a/b/c
# delete
curl -X DELETE http://localhost:3000/a/b/c
```
 ! attention à ./data ou ../.data -> ou mettre les data

- https://communitysolidserver.github.io/configuration-generator/
custom config `npm start -- -c config/file.json -f ../.data`

- give data access to autogpt
`npm start -- -c config/file.json -f ~/dev/Auto-GPT/autogpt/auto_gpt_workspace/solid_data `


exemple `npm run start:file # filesystem with ./data`


# mashlib or penny ? recipes
Not ok for me now
- https://github.com/CommunitySolidServer/recipes
- :~/dev/smag1/solid/CommunitySolidServer$ git clone https://github.com/CommunitySolidServer/Recipes

`npm start -- -c Recipes/penny/config-penny.json -f ../.data`

other solution  --> ok , mais after setup et création user pour mashlib, on devrait avoit spoggy.localhost, cat avec localhost:3000/spoggy le dossier public, le dossier test ne semblent pas conformes
- copy Recipes/mashlib/config-mashlib.json to config/
- npm install --save mashlib
`npm start -- -c config/config-mashlib.json -f ../.data`
 ou `npm run mashlib`
`npm start -- -c config/config-mashlib.json -f ~/dev/Auto-GPT/autogpt/auto_gpt_workspace/solid_data`
 `npm run autogpt`


# solid-client-authn
```
git clone https://github.com/inrupt/solid-client-authn-js.git
cd solid-client-authn-js
npm ci
```
--> see examples in packages
```
cd packages/browser/examples/demoClientApp
npm ci
npm start
```
# hello-world-component
- https://github.com/CommunitySolidServer/hello-world-component

# notification
- https://github.com/CommunitySolidServer/CommunitySolidServer/blob/main/documentation/markdown/usage/notifications.md


```
curl -v -H "Content-Type: text/plain" http://localhost:3000/.well-known/solid
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 3000 (#0)
> GET /.well-known/solid HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Type: text/plain
> 
< HTTP/1.1 200 OK
< Vary: Accept,Authorization,Origin
< X-Powered-By: Community Solid Server
< Access-Control-Allow-Origin: *
< Access-Control-Allow-Credentials: true
< Access-Control-Expose-Headers: Accept-Patch,Accept-Post,Accept-Put,Allow,ETag,Last-Modified,Link,Location,Updates-Via,WAC-Allow,Www-Authenticate
< Content-Type: text/turtle
< Date: Wed, 14 Jun 2023 13:50:21 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< Transfer-Encoding: chunked
< 
<http://localhost:3000/> a <http://www.w3.org/ns/pim/space#Storage>;
    <http://www.w3.org/ns/solid/notifications#subscription> <http://localhost:3000/.notifications/WebSocketChannel2023/>.
<http://localhost:3000/.notifications/WebSocketChannel2023/> <http://www.w3.org/ns/solid/notifications#channelType> <http://www.w3.org/ns/solid/notifications#WebSocketChannel2023>;
    <http://www.w3.org/ns/solid/notifications#feature> <http://www.w3.org/ns/solid/notifications#accept>, <http://www.w3.org/ns/solid/notifications#endAt>, <http://www.w3.org/ns/solid/notifications#rate>, <http://www.w3.org/ns/solid/notifications#startAt>, <http://www.w3.org/ns/solid/notifications#state>.
* Connection #0 to host localhost left intact

```