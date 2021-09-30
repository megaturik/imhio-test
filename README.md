# tcg to digitalocean

git clone git@github.com:megaturik/imhio-test.git

## Terraform
```
cd imhio-test/tf/

terraform init

terraform apply
```
terraform попросит определить токен полученный в digital ocean, вводим его,  затем подтвердить действия - yes.

Cмотрим значение ipv4_address для созданного инстанса в digital ocean:
```
terraform show 
```
## Ansible
```
cd ../ansible/
echo "ipv4_address:22" > hosts
```

Открывваем main.yml в любимом редакторе и в hosts указываем полученный в terraform ip.

запускаем плейбук:
```
ansible-playbook -i hosts main.yml
```
## Проверка
Проверяем результат:
```
curl -X POST ipv4_address:8084/v1/health/check
```
должен вернуться json вида:
{"last_check":"2021-09-30 07:24:39","version":"1.40"}

