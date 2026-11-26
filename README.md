<p align="center">
  <a href="https://ag.tavardt.com/it/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# Rilevatore di Siti Hackerati e Spam SEO

[![Rilevatore Spam SEO](https://img.shields.io/badge/TAVARDT-Antispam%20SEO-5b3cf5.svg)](https://tools.tavardt.com/it/rilevatore-spam-seo-sito-hackerato/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Il **TAVARDT Rilevatore di Siti Hackerati e Spam SEO** fornisce ispezione forense per applicazioni web per individuare cloaking verso i motori di ricerca, iniezioni nascoste di link farmaceutici o casinò, iframe non autorizzati e codice offuscato in Italia.

***

## Architettura di Rilevamento e Matrice Forense dei Vettori

Il cloaking e le iniezioni di contenuti nascosti ingannano i bot di scansione pur rimanendo invisibili agli utenti comuni. Questa compromissione causa penalizzazioni manuali su Google, la perdita dell'indicizzazione e il danneggiamento della reputazione aziendale.

Questo strumento diagnostico analizza le divergenze di risposta tra User-Agent, ispeziona contenitori CSS nascosti e isola elementi di tracciamento furtivi senza librerie esterne.

Il motore diagnostico valuta l'integrità del DOM, la varianza dimensionale dei payload e le firme di script sospetti partendo da 100 punti base:

<table>
  <thead>
    <tr>
      <th>Vettore di Compromissione</th><th>Logica di Rilevamento</th><th>Deduzione</th><th>Impatto sull'Integrità</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Cloaking Differenziale</strong></td><td>Confronta User-Agent di un browser standard con Googlebot. Segnalato se il rapporto di divergenza in byte > 0,40 e il delta assoluto > 1000 byte.</td><td>-30 pts</td><td>Rischio critico di penalizzazione algoritmica e de-indicizzazione immediata nei motori.</td>
    </tr>
    <tr>
      <td><strong>Iniezione di Spam Nascosto</strong></td><td>Ispeziona contenitori con <code>display:none</code>, <code>opacity:0</code> o margini negativi contenenti parole chiave di farmacia e casinò.</td><td>-35 pts</td><td>Conferma inequivocabile di compromissione del database o dei file di template.</td>
    </tr>
    <tr>
      <td><strong>iframe Invisibili Sospetti</strong></td><td>Individua iframe con dimensioni pari a zero o stili nascosti non presenti nella whitelist dei servizi di sicurezza certificati.</td><td>-20 pts</td><td>Vettore comune per reindirizzamenti non autorizzati, drive-by download o furto di sessioni.</td>
    </tr>
    <tr>
      <td><strong>Codice Offuscato</strong></td><td>Rileva pattern ripetuti di esecuzione dinamica come <code>eval()</code>, <code>unescape()</code> e <code>base64_decode</code> (>2 occorrenze).</td><td>-15 pts</td><td>Comportamento tipico di droppers e backdoor persistenti iniettate nel codice sorgente.</td>
    </tr>
    <tr>
      <td><strong>Errore di Connessione</strong></td><td>Scadenza del timeout della richiesta o errore durante la negoziazione TLS/HTTP.</td><td>-20 pts</td><td>Inaccessibilità dell'host che impedisce la verifica forense completa.</td>
    </tr>
  </tbody>
</table>

### Scala di Integrità e Livelli di Stato

Il sistema calcola un punteggio complessivo di salute digitale classificando il dominio:

* <strong>85 a 100 (CLEAN)</strong>: Nessun indicatore di compromissione rilevato; integrità del markup e coerenza di risposta confermate.
* <strong>60 a 84 (SUSPICIOUS)</strong>: Rilevate anomalie nei blocchi CSS, iframe non autorizzati o divergenze che richiedono un audit immediato.
* <strong>0 a 59 (COMPROMISED)</strong>: Presenza accertata di cloaking, spam iniettato o script offuscati che richiedono bonifica urgente.

***

## Installazione ed Esecuzione

Sviluppato unicamente con moduli standard di Python 3.8+, senza dipendenze esterne.

```bash
git clone https://github.com/TAVARDT-Italia/hacked-site-seo-spam-detector-it.git
cd hacked-site-seo-spam-detector-it
```

### Esecuzione Standard CLI

```bash
python seo_spam_detector.py esempio.it
```

### Output Strutturato per Pipeline in JSON

```bash
python seo_spam_detector.py esempio.it -j
```

### Configurazione di Timeout Personalizzato

```bash
python seo_spam_detector.py esempio.it -j -t 15
```

***

## Linee Guida ACN e Protezione delle Applicazioni Web

Questa procedura rispetta le indicazioni dell'**Agenzia per la Cybersicurezza Nazionale (ACN)** e gli standard di sicurezza delle applicazioni web. Individuare tempestivamente alterazioni non autorizzate salvaguarda i dati aziendali e la conformità normativa.

Si raccomanda di inserire controlli automatici di cloaking e integrità DOM nelle routine periodiche di sicurezza digitale.

***

## Domande Frequenti Tecniche

### Come funziona l'algoritmo di rilevamento del cloaking differenziale?

Il motore invia due richieste HTTP consecutive all'URL bersaglio, prima con un User-Agent di browser convenzionale e poi simulando il Googlebot. Se la discrepanza proporzionale in byte supera 0,40 con una variazione assoluta maggiore di 1000 byte, viene notificato il cloaking con una penalità di 30 punti.

### Cosa qualifica un iframe nascosto come sospetto?

Qualsiasi iframe configurato con larghezza zero, altezza zero o stile inline <code>display:none</code> non appartenente a provider di sicurezza verificati (come Cloudflare, Google reCAPTCHA, Google Tag Manager o hCaptcha) è classificato come sospetto, comportando una penalità di 20 punti.

### Quali termini di spam vengono cercati nei blocchi CSS invisibili?

L'analizzatore esamina contenitori resi invisibili tramite <code>display:none</code>, <code>visibility:hidden</code>, <code>opacity:0</code> o posizionamenti negativi estremi cercando termini come viagra, cialis, casino, payday loan, replica watch, poker, roulette, baccarat, vape e ketamine, applicando 35 punti di penalità.

### Perché l'uso ripetuto di eval e unescape viene sanzionato?

Il codice di produzione affidabile non deve fare ricorso a <code>eval()</code> o <code>unescape()</code> nel frontend. Più di due occorrenze indicano la potenziale presenza di payload offuscati caricati dinamicamente, con una penalizzazione di 15 punti.

### Come si integra il report diagnostico nei sistemi di monitoraggio?

Invocando lo script con il parametro <code>-j</code>, la diagnostica emette un documento JSON formattato su stdout, ideale per l'ingestione automatica in piattaforme SIEM, pipeline CI/CD o cruscotti di sicurezza.

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
Rilasciato sotto licenza MIT.

***

© 2026 TAVARDT. Tutti i diritti riservati.
