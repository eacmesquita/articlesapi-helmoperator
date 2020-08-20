mkdir -p /opt/helm/helm-charts

ln -s helm-charts/article/ /opt/helm/helm-charts

oc apply -f deploy/crds/example.com_articles_crd.yaml

operator-sdk run --local


oc create -f deploy/crds/example.com_v1_article_cr.yaml

#populate the postgres database

psql -U user articlesdb
create table articles(Id serial primary key, Title varchar(20), Description varchar(30), Content varchar(100));
insert into articles(Title,Description,Content) values('Docker','Overview of Docker','Docker is a software used for building and running containers');
