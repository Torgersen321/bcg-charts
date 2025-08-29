flowchart TD
    A([Organisk vekst via salg & distribusjon]):::root

    A --> I[Interne distribusjonskanaler]
    A --> E[Eksterne distribusjonskanaler]

    %% Interne
    subgraph SGI[Interne kanaler]
      I1[Direkte digital (web/app/inbound)]:::node
      I2[Egen rådgivning/RM/callcenter]:::node
      I3[Kryss-salg & oppsalg til eksisterende kunder]:::node
    end

    %% Eksterne
    subgraph SGE[Eksterne kanaler]
      E1[Rådgiver-kanal (bank/IFA/privatbank)]:::node
      E2[Plattformer/nettmeglere]:::node
      E3[Forsikring/unit-linked]:::node
      E4[Institusjonelle (pensjon/treasury)]:::node
    end

    %% Felles gatingløp for alle kanaler
    I1 --> G1
    I2 --> G1
    I3 --> G1
    E1 --> G1
    E2 --> G1
    E3 --> G1
    E4 --> G1

    G1{Kanal-fit OK? <br/>Andelsklasse & pris riktig}:::gate
    G1 -- Ja --> G2{Dokumentasjon komplett? <br/>PRIIPs KID, EMT/EPT/EET, faktaark}:::gate
    G1 -- Nei --> A1[Opprett/endre andelsklasse <br/>+ prislogikk for kanalen]:::action --> G2

    G2 -- Ja --> G3{Avtale & shelf-space på plass? <br/>(listing/meny/modellportefølje)}:::gate
    G2 -- Nei --> A2[Publiser/oppdater KID/EMT/EPT/EET <br/>+ konsistent fondsside]:::action --> G3

    G3 -- Ja --> G4{Salgsinnhold klart? <br/>Deck, 1-sider, norsk web, Q&A}:::gate
    G3 -- Nei --> A3[Forhandle distribusjonsavtale <br/>+ få listing/menyplass]:::action --> G4

    G4 -- Ja --> G5{Aktivering klar? <br/>Kampanje/trening/webinar}:::gate
    G4 -- Nei --> A4[Produser salgsinnhold <br/>(pitch-deck, 1-sider, video, fondssider)]:::action --> G5

    G5 -- Ja --> RUN[Aktiver: kampanje, webinar, rådgivertrening, <br/>model-portefølje-inntak]:::action
    G5 -- Nei --> A5[Plan for aktivering & kalender <br/>(tema-uker, roadshows, QBR)]:::action --> RUN

    RUN --> M[Drift: Mål & læring (KPI-dashboard)]:::measure

    %% KPI-rammeverk
    subgraph KPIs[Målehierarki (per kanal)]
      K1[Aktivitet & dekning: <br/>#møter/#webinar/#trening, KAM-touchpoints]:::kpi
      K2[Hylleplass: <br/>#listinger, share-of-shelf, #modellportefølje]:::kpi
      K3[Flyt/konvertering: <br/>Leads→MQL→SQL→Win rate, tid-til-første-tegning]:::kpi
      K4[Net flows & beholdning: <br/>Brutto, Netto, churn/uttak, retention 6/12 mnd]:::kpi
      K5[Økonomi: <br/>Take-rate, TER-konkurranse, LTV/CAC, kampanje-ROI]:::kpi
    end

    M --> K1
    M --> K2
    M --> K3
    M --> K4
    M --> K5

    classDef root fill:#f5f5f5,stroke:#333,stroke-width:1px;
    classDef node fill:#ffffff,stroke:#666,stroke-width:1px;
    classDef gate fill:#FFF8E1,stroke:#C58B00,stroke-width:1px;
    classDef action fill:#E8F5E9,stroke:#2E7D32,stroke-width:1px;
    classDef measure fill:#E3F2FD,stroke:#1565C0,stroke-width:1px;
    classDef kpi fill:#E3F2FD,stroke:#1565C0,stroke-width:1px;
