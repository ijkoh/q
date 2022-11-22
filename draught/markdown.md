<main>
<h2>Добавление/создание нового инстанса/домена в организации.</h2>
</main>
Данные берутся из структуры организации, которая находится, путь: vars_smartpetrol/monitoring/ "grafana_organizations", 
выполняются c помощью роли: monitoring/define_vars/main.yml

1. Под grafana_organizations:
добавляем вашу новую организацию, под ней экспортер или endpoint.

2. Указываем инстанс метрики. Если это endpoint, то нужно указать ещё domain и user.

3. Password vault generation with command: `ansible-vault encrypt_string`


Example(endpoint): 

<pre>&nbsp;CargorunGeocoder:
&nbsp;&nbsp;&nbsp;&nbsp;endpoint:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- instance: geocoder-prod
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domain: metrics.prod.app.geo.canada.smprojects.ru
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user: pushgateway
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;password: !vault |
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ANSIBLE_VAULT;1.1;AES256
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;65383637616264663833646634626564346333323965316231346161356338383932366534653237
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3036653637393266333738306236656636383431306436650a383161623735633066396165623162
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;64356532663635643931333233623861356265336530316636376537366438313263303538366661
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3632623530653330310a386266623535653633636339396238653762356663306565626338366239
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;33303536666237346137373532386332313339323232313831666335353838306636643363656266
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6336363936653532663461623135653335386665623235343935</pre>


Пример вывода структуры в консоли, после запуска роли /roles/monitioring :

<pre>&nbsp;&nbsp;msg:
&nbsp;&nbsp;- domain: cadvisor.ct.smprojects.ru
&nbsp;&nbsp;&nbsp;&nbsp;exporter: cadvisor
&nbsp;&nbsp;&nbsp;&nbsp;instance: cargorun-eam-prod-connecticut
&nbsp;&nbsp;&nbsp;&nbsp;label: cadvisor-connecticut
&nbsp;&nbsp;&nbsp;&nbsp;organization: CargorunEAM
&nbsp;&nbsp;&nbsp;&nbsp;password: password
&nbsp;&nbsp;&nbsp;&nbsp;user: cadvisor</pre>

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



