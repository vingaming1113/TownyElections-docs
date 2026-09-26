---
icon: wrench
---

# Konfiguration

`config.yml` har en masse indstillinger til at redigere opførslen af din server, såsom at indstille valgsystemet.

I konfigurationen finder du en masse indstillinger. De forklares inde i konfigurationen.

Du kan se den fulde standardkonfiguration nedenfor:

```yml
# ============================================================================
#  TownyElections - Konfiguration
# ============================================================================
#  Et formelt, konfigurerbart valgsystem for Towny byer.
#  Dokumentation & support: se README.md
# ============================================================================

# Rediger ikke. Bruges internt til at migrere konfigurationen ved opdateringer.
config-version: 1

# Generelle plugin-indstillinger.
general:
  # Lokale for meddelelsesfilen (messages_<locale>.yml). Standard er "en".
  locale: "en"
  # Hvis true, logges ekstra debug-information til konsollen.
  debug: false
  # Aktiver anonym brugsstatistik via bStats (https://bstats.org).
  metrics: true

# ----------------------------------------------------------------------------
#  Opdateringskontrol
# ----------------------------------------------------------------------------
# Ved opstart kan TownyElections kontrollere GitHub Releases for en nyere *stabil* version
# (beta- og alpha-versioner ignoreres). Kontrollen kører asynkront og blokerer aldrig
# serveren. Den logger kun til konsollen og meddeler under visse omstændigheder
# administratorer ved tilslutning. Den downloader eller installerer aldrig noget.
update-checker:
  # Hovedkontakt for GitHub Releases opdateringskontrol.
  enabled: true
  # GitHub-repository i ejer/navn-format.
  github-repository: "vingaming1113/TownyElections"
  # Meddel administratorer med townyelections.admin, når de tilslutter sig, hvis en opdatering findes.
  notify-admins-on-join: true

# ----------------------------------------------------------------------------
#  Valgindstillinger
# ----------------------------------------------------------------------------
election:
  # Hvor lang tid *nominations-/kampagnefasen* varer, hvori beboere kan registrere sig som kandidater.
  # Accepterer en varighed som f.eks.: 30s, 10m, 2h, 3d, 1w.
  nomination-duration: "2d"

  # Hvor lang tid *afstemningsfasen* varer, når nomineringerne lukker.
  voting-duration: "3d"

  # Mindste antal kandidater, der kræves for, at et valg kan gå videre til afstemning.
  # Hvis færre kandidater registrerer sig, annulleres valget (eller vinder automatisk, se "auto-win-single-candidate").
  min-candidates: 2

  # Maksimale antal kandidater, der er tilladt pr. valg. 0 = ubegrænset.
  max-candidates: 0

  # Hvis kun én kandidat registrerer sig, og min-candidates ellers ville mislykkes,
  # skal den kandidat så automatisk vinde?
  auto-win-single-candidate: true

  # Mindste antal beboere, en by skal have, før et valg kan afholdes.
  min-town-residents: 2

  # Hver beboer kan afgive dette antal stemmer pr. valg (normalt 1).
  votes-per-resident: 1

  # Hvis true, kan spillere ændre deres stemme, mens afstemningsfasen er åben.
  allow-vote-changes: true

  # Hvis true, kan beboere se live stemmetællinger under afstemningen. Hvis false, gemmes
  # tællingerne, indtil valget afsluttes (hemmelig afstemning).
  public-live-results: true

  # Må kandidater stemme på sig selv?
  allow-self-vote: false

  # Valgsystem, der bruges til at indsamle og tælle stemmesedler:
  #   PLURALITY - hver vælger vælger én kandidat; den med flest stemmer vinder
  #   RANKED_CHOICE - vælgere rangerer kandidaterne efter præference
  #                   (/election vote First Second Third ...). Tællingen kører
  #                   øjeblikkelige udslettelsesrunder: den svageste kandidat
  #                   elimineres, og deres stemmesedler overføres til hver vælgers
  #                   næste præference, indtil nogen har et flertal.
  #   APPROVAL - vælgere godkender et hvilket som helst antal kandidater
  #              (/election vote Alice Bob ...); flest godkendelser vinder
  # Systemet låses, når et valg starter. Ændring af denne værdi fortolker aldrig
  # stemmesedlerne fra et allerede kørende valg på ny.
  voting-system: "PLURALITY"

  # Strategi til at bryde uafgjort, når de bedste kandidater er ude af stand til at vinde:
  #   RANDOM - vælg en tilfældig vinder fra de uafgjorte kandidater
  #   EARLIEST - den kandidat, der registrerede sig først, vinder
  #   INCUMBENT - den nuværende borgmester vinder, hvis uafgjort, ellers RANDOM
  #   RUNOFF - start en ny kort afstemningsrunde mellem de uafgjorte kandidater
  #   NONE - erklær ingen vinder (valg annulleret)
  tie-breaker: "RUNOFF"

  # Varighed af en runoff-afstemningsrunde (bruges kun, når tie-breaker er RUNOFF).
  runoff-duration: "1d"

  # Start automatisk et nyt valg i hver berettigede by på et fast interval.
  # Indstil enabled til false for kun at køre valg, der startes manuelt via kommandoer.
  auto-schedule:
    enabled: true
    # Interval mellem *slutningen* af ét valg og den automatiske start af det
    # næste (pr. by). Eksempel: 30d for en månedlig cyklus.
    interval: "14d"

  # Hvis true, bliver byens økonomikonto belastet/belønninger håndteret (kræver en økonomi).
  # Ren valutfunktion.
  economy:
    # Omkostning for en beboer at registrere sig som kandidat. 0 = gratis.
    candidacy-cost: 10.0
    # Belønning, der gives til vinderen fra ingen steder (0 = deaktiveret).
    winner-reward: 500.0

  # Grænse for stemmer pr. IP for at forhindre misbrug af alt-konti. Når aktiveret,
  # kan én konto pr. fingeraftryk (IP) få en stemmeseddel, op til det konfigurerede
  # antal fingeraftryk. IP-adresser hashes (SHA-256). Kun hashene og vælgerens UUID
  # gemmes, så beskyttelsen forbliver effektiv efter en servergenstart.
  ip-vote-limit:
    # Hovedkontakt for grænsen for stemmer pr. IP. false = deaktiveret (nuværende adfærd).
    enabled: false
    # Maksimale antal forskellige IP-fingeraftryk, der må stemme ved ét valg.
    # 0 = ubegrænset (effektivt deaktiveret, selvom enabled: true).
    max-votes: 0

# ----------------------------------------------------------------------------
#  Kampagneindstillinger
# ----------------------------------------------------------------------------
campaign:
  # Maksimal længde (tegn) af en kandidats kampagnemeddelelse.
  max-message-length: 128
  # Standard kampagnemeddelelse, der bruges, når en kandidat ikke sætter nogen.
  default-message: "I would be honored to serve this town."
  # Maksimal længde (tegn) af et partinavn, der indtastes med /election party.
  # Dette beskyttelse af chatoutput og tab-fuldførelse mod meget lange labels.
  max-party-name-length: 32
  # Standardparti, der vises, indtil en kandidat vælger et.
  # Dette er, hvad spillere returnerer til, når de bruger /election party leave.
  default-party-name: "Independent"
  # Hvis true, skjules standardpartiet fra /election parties og partiresultatsummeringer.
  # Kandidater beholder stadig labelen i kandidatlister.
  hide-default-party-from-standings: false
  # Maksimale antal ikke-standardpartier, der kan eksistere i ét aktivt valg.
  # 0 = ubegrænset. Dette begrænser kun oprettelsen af helt nye partilabels.
  # Spillere kan altid slutte sig til et parti, der allerede eksisterer, eller forlade tilbage til standarden.
  max-parties: 0
  # Hvis true, kan kandidater ikke ændre deres kampagnemeddelelse, profil, parti eller
  # partifarve, når afstemningsfasen er begyndt. Disse kan kun redigeres under
  # nominationsfasen. Indstil til false for at tillade redigering på ethvert tidspunkt.
  lock-edits-during-voting: true

  # En simpel blokeringsliste. Kampagnemeddelelser, der indeholder nogen af disse (ikke case-sensitiv)
  # undersøgelser, afvises.
  blocked-words:
    - "slur1"
    - "slur2"

# ----------------------------------------------------------------------------
#  Vinderbelønninger - hvad den valgte kandidat modtager
# ----------------------------------------------------------------------------
# Når et valg afsluttes, tildeles vinderen de konfigurerede Towny-by-ranger
# og (valgfrit) gøres til borgmester. Rænger skal eksistere i Townys
# townyperms.yml (standard inkluderer: helper, councillor, sheriff, treasurer, osv.
# og brugerdefinerede rænger). Ugyldige rænger springes over med en konsoladvarsel.
winner:
  # Gør den vindende kandidat til byens borgmester. Dette overfører borgmesterembedet.
  set-as-mayor: true

  # Towny-by-rænger, der tildeles vinderen af et *byvalg*. Disse mapper til
  # tilladelsesnoder, der er defineret i Townys townyperms.yml (f.eks. plot administration).
  grant-town-ranks:
    - "assistant"

  # Hvis true, fjernes rænger, der er tildelt af en tidligere valgsejr, fra den
  # afgående embedsholder(e), når en ny vinder overtager embedet. Gælder for byrænger
  # for byvalg og nationsrænger for nationsvalg.
  revoke-previous-winner-ranks: false

  # Ekstra native/Bukkit konsolkommandoer, der køres, når en vinder er afgjort.
  # Placeholders: {winner} {winner_uuid} {winner_party} {party} {town} {votes} {total_votes}
  # Køres fra konsollen. Godt til LuckPerms, meddelelser, give genstande, osv.
  # Lad stå tom for at køre ingenting. Eksempler (fjern kommentar for at bruge):
  #   - "lp user {winner} parent addtemp mayor 30d"
  #   - "give {winner} minecraft:golden_helmet 1"
  commands-on-win: []

  # Komandoer, der køres for hver *tabende* kandidat, når valget afsluttes.
  # Placeholders: {loser} {loser_uuid} {loser_party} {party} {town} {votes}
  commands-on-loss: []

# ----------------------------------------------------------------------------
#  Kommando tilpasning
# ----------------------------------------------------------------------------
# Omdøb underkommandoerne for /election til hvad som helst, der passer til din server.
# Nøglerne er interne handlingsnavne; værdierne er, hvad spillere skriver i chatten.
# Eksempel: sæt parties: "blocs" for at gøre /election blocs til at liste partistillinger.
# Hold hver bogstavelig unikt, så kommandoer kan løses entydigt.
commands:
  run: "run"          # registrer som kandidat
  withdraw: "withdraw"  # træk sig fra valget
  campaign: "campaign"  # sæt din kampagnemeddelelse
  profile: "profile"    # sæt din kandidatprofil/bio
  party: "party"        # slut dig til, opret, forlad eller admin-omdøb et parti
  parties: "parties"  # list aktuelle partistillinger
  vote: "vote"          # afgiv en stemme
  status: "status"      # se aktuel valgstatus
  candidates: "candidates"  # list kandidater
  results: "results"    # se resultaterne af det sidste afsluttede valg
  start: "start"        # (admin) start et valg
  stop: "stop"          # (admin) afslut afstemning tidligt og optæl
  cancel: "cancel"      # (admin) annuller et valg uden vinder
  reload: "reload"      # (admin) genindlæs konfiguration
  help: "help"
  nation: "nation"      # præfiks for at målrette din nation, f.eks. /election nation vote

# ----------------------------------------------------------------------------
#  Meddelelser
# ----------------------------------------------------------------------------
notifications:
  # Send valgstart/-slut til hele serveren (udover byen).
  broadcast-server-wide: false
  # Mind vælgere, der endnu ikke har stemt, dette lang tid før afstemningens slutning.
  # Indstil til "0" for at deaktivere påmindelser.
  voting-reminder-before-end: "6h"
  # Meddel beboere, når de logger ind, hvis der er et aktivt valg, de kan deltage i.
  notify-on-join: true

```
