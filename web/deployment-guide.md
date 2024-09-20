1. Test Django --> #python manage.py test

2. Build container
'''
docker build -f Dockerfile\
    -t registry.digitalocean.com/cfe-k8ss/image_name:version(v1-latest or etc) .
'''

3. Push the container to digital ocean(or other kubernetes service)

'''
    docker push registry.digitalocean.com/cfe-k8ss/image_name --all-tags

'''

4.update secrets

'''
kubectl delete secret name_of_secret - for DELETE
kubectl create secret generic devapp-web-prod-env(name what we will put to secret) --from-env-file=web/.env.prod(from where we will take .env.prod file for example) - for CREATE

'''

5 - update depoyment

'''
    kubectl apply -f path_to_yaml_file

'''

6. Wait rollout statu deployment finished

7. migrate Datbase

'''
first: kubectl exec -it pod_name -- /bin/bash
second: activate venv, then run  python manage.py migrate or use bash script (example migrate.sh)
-----------------------------------------------------
or : first: kubectl exec -it pod_name -- bash /app/migrate.sh
'''