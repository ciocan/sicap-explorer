# sicap-explorer

**sicap-explorer** este un tablou de vizualizare a licitatiilor publice si achizitiilor directe cu ajutorul aplicatiei open-source [Kibana](https://www.elastic.co/kibana)

Datele sunt preluate din portalul de licitatii publice SEAP/SICAP în baza **Licenței pentru Guvernare Deschisa v1.0**

Seturile de date contin **22,101,610 achizitii directe** si **470,811 licitatii publice** incepand cu anul 2007 pana in data de 31 iulie 2020

[![Achizitii directe](images/achizitii-directe.png)](#)

[![Achizitii directe](images/licitatii-publice.png)](#)

[![Dashboard](images/dashboard.png)](#)

Cateva exemple cu tabloul in actiune pe canalul de [YouTube](https://www.youtube.com/channel/UCLmNkO-z3KeZDYmkp-u2u_Q/featured):

[![Canal YouTube](images/youtube.png)](https://www.youtube.com/channel/UCLmNkO-z3KeZDYmkp-u2u_Q/featured)

## Cum se instaleaza pe masina proprie

Cerinte minime pentru o functionare de baza

- 100gb liberi pe disc
- 4 core / 8gb ram
- Sistem de operare: Windows / MacOS / Linux

<u>Cerinte recomandate</u>

- 100 gb liberi pe disc
- 8 core / 16gb ram
- Sistem de operare: MacOS / Linux

**Pasul 1:**

Descarca arhiva SICAP folosind [link-ul torrent](arhiva-sicap.torrent).

**Pasul 2:**

Instaleaza [Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html) si [Kibana](https://www.elastic.co/guide/en/kibana/current/install.html) pentru sistemul de operare folosit.

Alternativ se poate instala si folosid [Docker](https://docs.docker.com/engine/install/) folosid fisierul de configurare [docker-compose.yml](docker/docker-compose.yml).

**Pasul 3:**

Verifica daca totul este instalat si Kibana porneste la adresa http://localhost:5601

In functie de ce sistem de operare ai, gaseste fisierul **elasticsearch.yml** si adauga urmatoarea linie reprezentand locatia pe disc a arhivei snapshot descarcata de pe torent

```
path.repo: /folder/backup
```

Dezarhiveaza arhiva in folderul de mai sus si incepe procesul de "restore" din Kibana.

Un tutorial video cum poti face asta gasesti pe canalul de YouTube [aici](https://www.youtube.com/watch?v=piD_sQH1I98)

**Pasul 4:**

Importa [dashboardul](dashboards/achizitii-directe.json) in Kibana

```
$ curl -H "Content-Type: application/json" -d @dashboards/achizitii-directe.json -X POST http://localhost:5601/api/kibana/dashboards/import\?exclude\=index-pattern -H 'kbn-xsrf: true'
```

**Nota:**

Setarile initiale pentru Elasticsearch includ o memorie folosita de 2gb iar pentru Kibana de 1.4gb.
Este recomandat sa modifici memoria heap pentru Elasticsearch sa nu depaseasca jumatate din memoria disponibila.
Mai mult detalii [aici](https://www.elastic.co/guide/en/elasticsearch/reference/master/heap-size.html) iar pentru Kibana [aici](https://www.elastic.co/guide/en/kibana/current/production.html#memory)

Acest proiect adopta principiile [Public Money / Public Code](https://publiccode.eu/) si doreste ca institutiile publice sa ofere access catre informatiile cu caracter public intr-un mod cat mai usor.

[![Public Money / Public Code](./images/pmpc.jpg)](https://publiccode.eu/)
