# K8S-Dashboard

#### How to use
```sh
mkdir /root/certs/
openssl req -nodes -newkey rsa:2048 -keyout /root/certs/dashboard.key -out /root/certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kuber.dashboard"
openssl x509 -req -sha256 -days 3650 -in /root/certs/dashboard.csr -signkey /root/certs/dashboard.key -out /root/certs/dashboard.crt
kubectl create namespace kubernetes-dashboard
kubectl create secret generic kubernetes-dashboard-certs --from-file=/root/certs -n kubernetes-dashboard
kubectl apply -f dashboard-2.0.0b.yml
```

#### How get tokken
```sh
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```

#### How to use your certificate
```sh
mkdir /root/certs/
openssl req -nodes -newkey rsa:2048 -keyout /root/certs/dashboard.key -out /root/certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kuber.dashboard"
openssl x509 -req -sha256 -days 3650 -in /root/certs/dashboard.csr -signkey /root/certs/dashboard.key -out /root/certs/dashboard.crt
kubectl create namespace kubernetes-dashboard
kubectl create secret generic kubernetes-dashboard-certs --from-file=/root/certs -n kubernetes-dashboard
```