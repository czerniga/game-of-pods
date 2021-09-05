1. 
ssh node01
mkdir /drupal-data
mkdir /drupal-mysql-data

2.
kubectl create secret generic drupal-mysql-secret --from-literal=MYSQL_ROOT_PASSWORD=root_password --from-literal=MYSQL_DATABASE=drupal-database --from-literal=MYSQL_USER=mysql

3. 
kubectl expose deployment drupal-mysql --type=ClusterIP --port=3306 --name=drupal-mysql-service