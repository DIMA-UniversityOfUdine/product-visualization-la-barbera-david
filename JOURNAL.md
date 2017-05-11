# 22-04-2017
- Aggiunto file obj
- Corretto bug che impedisce di usare i controlli utente
- Presente bug che non fa eseguire sulla presente cartella, mentre in locale il codice esegue perfettamente.

# 01-05-2017
- Aggiunta e posizionamento luci 
- Modifica shader per includere le luci 
- Per ora uso di microfacet shader standard

to do: 
- altri materiali
- User Interface
- Sfondo
- Eventualmente: Due materiali diversi per manico e testa

# 09-05-2017
- Aggiunto Front-End by Foundation con relativa struttura web
- Applicato render a custom canvas di dimensioni ridotte
- Menù laterale composto da pulsanti che consentono di interagire con la scena
- Settaggio della finestra HTML con posizione adattiva a seconda delle dimensioni dello schermo
- Impostazione delle prime funzionalità come ShowBase e Metallic Mjolnir

to do:
- enviroment map corretto con materiali
- HideBase con relativo adattamento dei gradi di libertà della camera in relazione alla sua presenza o assenza
- Sistemare il codice three js con una struttura a funzioni per riutilizzare più codice
- Martello giocattolo con materiali a microfaccette adatti e relativo accesso da interfaccia

# 11-05-2017
- Implementata funzionalità hide base e corretto shader per la texture della base.
- Applicata texture definitiva per la base d'appoggio
- Creato martello giocattolo con parte diffusiva + speculare per materiale plastico credibile

to do:
- Enviroment mapping
- Limitare rotazione camera solo in caso di presenza della base e consentire una rotazione maggiore in sua assenza
- Eventualmente feature con rotazione automatica della camera