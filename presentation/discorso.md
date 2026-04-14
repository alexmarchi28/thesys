# Traccia parlata per la presentazione

Durata stimata: circa 9-10 minuti.

## Slide 1 - Titolo e presentazione

"Buongiorno, sono Alex Marchi e oggi presento il mio lavoro di tesi, intitolato *Valutazione simulativa di un protocollo 5G-V2X per lo smantellamento sicuro di platoon*. Il lavoro nasce nel contesto delle comunicazioni V2X e, in particolare, del platooning cooperativo. L'idea di fondo è capire come mantenere sicuro un platoon quando la qualità della comunicazione peggiora. Per farlo ho preso come riferimento il meccanismo SafeSwitch, già proposto in letteratura, e l'ho ricostruito e aggiornato in una toolchain più recente, sostituendo la parte cellulare LTE con una modellazione 5G basata su Simu5G."

## Slide 2 - Il problema

"Il platooning è una modalità di guida cooperativa in cui più veicoli viaggiano molto vicini tra loro, seguendo un leader e scambiandosi periodicamente informazioni sul proprio stato. Questo approccio può portare benefici concreti: migliore capacità stradale, più regolarità del traffico e anche maggiore efficienza energetica. Però questi vantaggi dipendono dal fatto che i messaggi arrivino in modo regolare e affidabile. Se il link degrada, il problema non resta confinato alla rete, ma si trasferisce direttamente al controllo del veicolo. Quindi la domanda centrale della tesi è: cosa succede al platoon quando la comunicazione non è più abbastanza affidabile, e come possiamo evitare che una perdita di connettività si trasformi in un problema di sicurezza?"

## Slide 3 - Perché servono più interfacce

"La risposta proposta dal lavoro di riferimento è usare più interfacce contemporaneamente, perché nessuna tecnologia singola è affidabile in ogni scenario. IEEE 802.11p è molto utile perché consente comunicazione diretta tra veicoli, ma soffre contesa e interferenza. La VLC può essere molto precisa nelle comunicazioni tra veicoli vicini, ma dipende dalla linea di vista e dall'allineamento ottico. La rete cellulare, nel mio caso 5G, offre copertura più ampia e continuità, ma introduce dipendenza dall'infrastruttura e transitori dovuti agli handover. L'idea quindi non è scegliere una tecnologia migliore delle altre, ma sfruttare il fatto che hanno profili di guasto diversi. I beacon vengono inviati in parallelo sulle interfacce attive, così il sistema guadagna sia ridondanza sia complementarità."

## Slide 4 - Come funziona SafeSwitch

"Qui entra in gioco SafeSwitch. Il meccanismo monitora la qualità dei link tramite il PDR, cioè la frazione di pacchetti ricevuti correttamente in una finestra recente. Ogni follower osserva separatamente ciò che riceve dal leader e dal predecessore, e decide localmente se una o più interfacce stanno degradando oppure recuperando. Il punto chiave è che SafeSwitch non fa un cambio brusco di controllore. Se la comunicazione peggiora, il sistema non passa direttamente da una modalità cooperativa molto prestazionale a una modalità più conservativa. Prima entra in una fase intermedia di *gap control*: aumenta gradualmente la distanza tra veicoli e solo dopo consolida il nuovo controllore. In questo modo collega esplicitamente qualità della rete, legge di controllo e sicurezza fisica del platoon."

## Slide 5 - Il mio contributo

"Il mio contributo si può riassumere in tre parti. La prima è stata la ricostruzione dell'ambiente sperimentale, integrando OMNeT++, Veins, PLEXE, SUMO e Simu5G in una toolchain aggiornata e riproducibile. La seconda è stata riportare dentro questo nuovo ambiente la logica del lavoro di riferimento: scenari, metriche, monitoraggio del PDR e macchina a stati di SafeSwitch. La terza, che è anche la parte più caratterizzante della tesi, è stata la migrazione della componente cellulare da SimuLTE a Simu5G. In pratica ho aggiornato il terzo canale del sistema mantenendo invariata la logica superiore: il cellulare continua a essere una delle tre interfacce usate per il platooning, ma ora è modellato con uno stack 5G più attuale."

## Slide 6 - Risultato 1

"Questo è probabilmente il risultato più intuitivo della tesi. Qui confronto un fallback *naive* con SafeSwitch in uno scenario critico: si perde una tecnologia e subito dopo c'è una frenata di emergenza. Nel fallback naive il sistema passa direttamente a una modalità più conservativa senza adattare prima il gap, e infatti la simulazione si interrompe quasi subito per collisione. Con SafeSwitch, invece, il platoon riesce a evitare l'urto: il transitorio resta impegnativo, soprattutto verso la coda, ma rimane controllato. Questo risultato è importante perché mostra che la fase di gap control non è un dettaglio implementativo: è proprio il pezzo che rende il cambio di controllore dinamicamente coerente e quindi sicuro."

## Slide 7 - Risultato 2

"Qui invece mostro il confronto nello scenario più realistico, mettendo a sinistra il comportamento riportato nell'articolo e a destra quello ottenuto nella mia reimplementazione con 5G. Il punto non era riprodurre esattamente ogni numero, perché passando da SimuLTE a Simu5G cambiano inevitabilmente stack radio, modelli fisici e parametri di handover. Il punto era verificare se restasse la stessa catena causale. E la risposta è sì: i burst di perdita continuano a produrre un aumento temporaneo del gap e poi un ricompattamento del platoon quando la qualità del link torna sufficiente. Allo stesso tempo, nei risultati della tesi i picchi sono più contenuti e i transitori associati alla componente cellulare sembrano meno severi. Quindi il 5G non introduce regressioni funzionali e anzi sembra rendere più fluido almeno parte del comportamento durante gli handover."

## Slide 8 - Conclusioni

"In conclusione, questa tesi mostra che SafeSwitch rimane coerente anche dopo l'aggiornamento della toolchain e della componente cellulare a 5G. Il risultato principale non è dimostrare che il 5G sia in assoluto migliore dell'LTE, ma che l'architettura multi-interfaccia e la logica di degradazione controllata restano valide in un ambiente più attuale. Questo è utile perché, in sistemi V2X safety-critical, comunicazione e controllo non possono essere progettati separatamente. Come sviluppi futuri vedo soprattutto tre direzioni: scenari più realistici, con veicoli e canali meno semplificati; un confronto LTE-5G più controllato; e l'uso di questa base per ulteriori studi su sistemi V2X eterogenei. In pratica, il lavoro lascia un ambiente sperimentale già pronto per continuare a studiare come far degradare il platoon in modo sicuro, invece che brusco o pericoloso."
