# Rilevatore di Siti Hackerati e Spam SEO

[![Rilevatore Spam SEO](https://img.shields.io/badge/TAVARDT-Antispam%20SEO-5b3cf5.svg)](https://tools.tavardt.com/it/rilevatore-spam-seo-sito-hackerato/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Verifica tecnica per individuare attacchi cloaking mirati ai motori di ricerca, iniezioni occulte di link e reindirizzamenti fraudolenti.

Sviluppato e gestito dall'unita di analisi forense e risposta agli incidenti di **TAVARDT**.

***

## Funzionalita dell'Audit Forense e Rilevamento Intrusione

* **Rilevamento del Cloaking**: Analisi comparativa immediata tra il markup mostrato ai visitatori e quello riservato a Googlebot.
* **Iniezione di Link e Testo Nascosto**: Individuazione di elementi dissimulati tramite classi CSS, iframe occulti e aggregatori illeciti di link.
* **Reindirizzamenti Malevoli Condizionali**: Verifica di redirect fraudolenti applicati in base alla sorgente di traffico o al dispositivo dell'utente.
* **Punteggio di Integrita Forense**: Indice quantitativo da 0 a 100 con misure pratiche di disinfezione immediata.

***

## Installazione ed Esecuzione

Richiede Python 3.8 o superiore senza necessita di pacchetti esterni.

```bash
git clone https://github.com/TAVARDT-Italia/hacked-site-seo-spam-detector-it.git
cd hacked-site-seo-spam-detector-it
python seo_spam_detector.py esempio.it
```

Per l'output formattato in JSON:

```bash
python seo_spam_detector.py esempio.it -json
```

***

## Strumento di Diagnosi Online

Per verificare l'integrita delle pagine e individuare eventuali compromissioni:

* **Rilevatore di Spam SEO e Siti Hackerati Ufficiale**
* **[Portale Aziendale TAVARDT](https://ag.tavardt.com/it/)**

***

## Risposta agli Incidenti e Bonifica Digitale

Per interventi di bonifica forense e hardening dei sistemi in linea con Linee Guida ACN e Sicurezza Informatica, contattare gli esperti di **TAVARDT**.

***

## Link Utili

* **Portale Aziendale:** https://ag.tavardt.com/it/
* **Suite di Diagnostica:** https://tools.tavardt.com/it/
* **Contatto Tecnico:** https://ag.tavardt.com/it/contatto/

***

### Licenza
Rilasciato sotto licenza MIT. Per maggiori informazioni, consultare il file [LICENSE](LICENSE).

***

© 2026 TAVARDT. Tutti i diritti riservati.
