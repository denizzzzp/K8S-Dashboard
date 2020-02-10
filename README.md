# K8S-Dashboard

#### How to use
```sh
kubectl apply -f https://raw.githubusercontent.com/denizzzzp/K8S-Dashboard/master/dashboard-2.0.0-rc5.yml
kubectl apply -f https://raw.githubusercontent.com/denizzzzp/K8S-Dashboard/master/metrics-server.yml
```

#### How get token
```sh
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```

#### How login in web

  - https://IP-KUBER-HOST:31443/#/login
  - select "Token" and enter token for admin-user

> P.S. Metric chart will be displayed in a couple of minutes

![K8S-Dashboard](https://image.prntscr.com/image/_OJmIFOzRnCr9O1tLWb2tQ.png)


#### How to use your certificate
```sh
mkdir /root/certs/
openssl req -nodes -newkey rsa:2048 -keyout /root/certs/dashboard.key -out /root/certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kuber.dashboard"
openssl x509 -req -sha256 -days 3650 -in /root/certs/dashboard.csr -signkey /root/certs/dashboard.key -out /root/certs/dashboard.crt
kubectl create namespace kubernetes-dashboard
kubectl create secret generic kubernetes-dashboard-certs --from-file=/root/certs -n kubernetes-dashboard
```