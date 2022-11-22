- Под grafana_organizations:
добавляем вашу новую организацию, под ней экспортер или endpoint.

- Указываем инстанс метрики. Если это endpoint, то нужно указать ещё domain и user.

- password vault generation with command: `ansible-vault encrypt_string`
---
Example(endpoint): 

  . CargorunGeocoder:
     . endpoint:
       . - instance: geocoder-prod
        . domain: metrics.prod.app.geo.canada.smprojects.ru
         . user: pushgateway
         . password: !vault |
             . $ANSIBLE_VAULT;1.1;AES256
             . 65383637616264663833646634626564346333323965316231346161356338383932366534653237
             . 3036653637393266333738306236656636383431306436650a383161623735633066396165623162
             . 64356532663635643931333233623861356265336530316636376537366438313263303538366661
             . 3632623530653330310a386266623535653633636339396238653762356663306565626338366239
             . 33303536666237346137373532386332313339323232313831666335353838306636643363656266
             . 6336363936653532663461623135653335386665623235343935

---
Пример вывода структуры в консоли, после запуска роли /roles/monitioring :

  msg:
  - domain: cadvisor.ct.smprojects.ru
    exporter: cadvisor
    instance: cargorun-eam-prod-connecticut
    label: cadvisor-connecticut
    organization: CargorunEAM
    password: password
    user: cadvisor

---
Где(описание перменных, вывод значений и с помощью чего они генерируются):
Берутся данные из структуры организации, которая находится, путь: vars_smartpetrol/monitoring/ "grafana_organizations", 
c помощью роли: monitoring/define_vars/main.yml, и таска внутри роли: - name: Transform dict to array flatten_grafana_organizations,
получаем переменные:
для инстанса получаем переменные и значения:

---
> 1. exporter 
> 2. instance
> 3. organization
для endpoint получаем переменные и значения:
> 1. exporter 
> 2. instance
> 3. organization
> 4. domain 
> 5. user
> 6. label
> 7. password

---
Оставшиеся данные для переменных инстанса, генерируется с помощью тасков:
    - name: Generate passwords for basicAuth
    - name: Lookup exporters password for prometheus scrape_configs
> 4. domain 
> 5. user
> 6. label
> 7. password





<p>&nbsp;CargorunGeocoder:
&nbsp;&nbsp;&nbsp;&nbsp;endpoint:
      - instance: geocoder-prod
        domain: metrics.prod.app.geo.canada.smprojects.ru
        user: pushgateway</p>