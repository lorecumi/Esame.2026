L'applicazione usa le informazioni fornite da un API in tempo reale

Nome: TheMealDB
Link: https://www.themealdb.com/api.php
Endpoint: https://www.themealdb.com/api/json/v1/1/search.php?s=pasta

I dati dell' API vengono mostrati in tutte le pagine:
1) index.html mostra nella HOME la griglia iniziale di ricette
2) ricette.html mostra la griglia completa (in questo caso, solo la pasta)
3) ingredienti.html mostra i dati della ricetta selezionata

Il sito funzionan anche in caso i server di TheMealDB siano in crash, o non ci sia una connessione ad internet, grazie alla seguente funzione di gestione dell'errore nel file script.js:


async function init() {
  try {
    setStatus("Caricamento dati dalla API remota...", "info");
    const items = await loadRemote();
    render(items);
    clearStatus();
  } catch (error) {
    console.warn(error);
    setStatus("API non disponibile: uso i dati locali di fallback da data.json.", "warning");
    try {
      const items = await loadFallback();
      render(items);
    } catch (fallbackError) {
      console.error(fallbackError);
      setStatus("Errore: non riesco a caricare né la API remota né data.json.", "danger");
    }
  }
