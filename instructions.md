### Curl example

docker run --rm alpine/curl -fsSL https://www.google.com

### Build image

```shell
docker build -t damasosanoja/flask-api .
docker push damasosanoja/flask-api
```

```shell
docker build -t flask-api .
docker tag flask-api:latest damasosanoja/flask-api:latest
# docker login --username=damasosanoja
docker push damasosanoja/flask-api:latest
```

### Deploy app

```shell
docker run -p 5000:5000 damasosanoja/flask-api:latest
```

```shell
kubectl apply -f flask-api-secrets.yaml -n flask
kubectl apply -f flask-app-deployment.yaml -n flask
kubectl get all -n flask
```

### Delete app

```shell
kubectl delete -f flaskapi-secrets.yaml -n flask
kubectl delete -f flaskapp-deployment.yaml -n flask
```

### Test app

```shell
kubectl port-forward svc/flask-app-service 5000:5000
curl http://localhost/create
```

```shell

curl -H "Content-Type: application/json" -d '{"name": "<user_name>", "email": "<user_email>", "pwd": "<user_password>"}' <flask-service_URL>/create.
```

docker run -p 5000/tcp damasosanoja/flask-api:latest