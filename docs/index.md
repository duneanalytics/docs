---
tytuł: Dune Quickstart
opis: Zacznij od wydmy za pięć minut!
---

### Dlaczego warto nauczyć się korzystać z wydmy?

Prawdopodobnie jesteś tutaj, ponieważ zdałeś sobie sprawę, że:

1. Chociaż dane blockchain są otwarte i przejrzyste, ** nie jest łatwo zrozumieć, spożyć i zsumować.** Każdy łańcuch ma różne niuanse, dekodowanie funkcji kontraktowych i zdarzeń nie jest tak proste, jak się wydaje.

2). Albo twój własny protokół, albo czyjś protokół nie został zbudowany z myślą o inżynierze / analityku danych. **Osiągnąłeś granice tego, jak nadążać za funkcjami odczytu kontraktu i najnowszymi wydarzeniami.**

3). Chcesz przeprowadzić ciężką analizę kontekstu krzyżowego, łącząc tokeny, portfele i protokoły w łańcuchach. Wymaga to kompleksowej hurtowni danych, która może skalować się na żądanie - i pełnego zespołu, który ją utrzyma. **To setki terabajtów danych do przechowywania i wykładnicze ilości obliczeń ( $ $ $ $ ) <TAG1>.**

4. Jesteś analitykiem, który chce ** pokazać swoją pracę dziesiątkom tysięcy użytkowników**, i zarabiaj gwiazdy, aby wspiąć się na tablicę wyników czarodzieja, aby znaleźć role niezależne lub pełnoetatowe.

Masz szczęście! Dune i społeczność tysięcy czarodziejów są tutaj, aby dostarczyć Ci zaawansowanej analizy wszystkich danych na temat łańcucha. Jeśli po prostu pójdziesz i poszukasz czegoś związanego z Web3, jestem pewien **, że znajdziesz [ co najmniej jeden pulpit nawigacyjny na ten temat ] ( https://dune.com/browse/dashboards?q=dex&order=favorites&time_range=all)**. Dotyczy to każdego łańcucha, który mamy, w tym maszyny elektryczne, takie jak ** Ethereum, Polygon, Goerli i Optimism ** oraz łańcuchy inne niż EVM, takie jak ** Solana i Bitcoin.**

Możesz szybko zbadać [ NFT marketplaces ] ( https://dune.com/hildobby/NFTs), [ DEX metryk ] ( https://dune.com/hagaetc/dex-metrics), Bridges [ ] ( Rachunkowość https://dune.com/eliasimos/Bridge-Away-(from-Ethereum)),!

Dość gadania, pokażmy trochę magii. ✨

### Analizuj dane Web3: Woluminy DEX

W tej krótkiej części omówimy, jak uzyskać tygodniowy wolumen USD sprzedawany przez DEX w ciągu ostatnich sześciu miesięcy na Ethereum. Kliknij poniżej interaktywny przewodnik, aby zrozumieć, w jaki sposób korzystamy z tabeli `dex.trades`, aby:

- Znajdź i wyświetl podgląd danych dla tabel, którymi jesteśmy zainteresowani

- Napisz i uruchom podstawowe zapytanie dotyczące silnika Dune SQL

- Utwórz i sformatuj ułożoną wizualizację wykresu słupkowego

< div style = "pozycja: względna; padding-bottom: calc ( 67.14527027027% + 41px ); wysokość: 0;" > < ładowanie "= ramka; góra: 0; lewo: 0; szerokość: 100%; wysokość: 100%; schemat kolorów: światło; ”tytuł =„ Pulpity nawigacyjne ”> < / iframe > < / div >

[ zapytanie można znaleźć tutaj ] ( https://dune.com/queries/2168290).

Teraz `dex.trades` to tabela księgi zaklęć, co oznacza, że jest to tabela wyodrębniona, która ”'zostały zebrane przez setki gwiazdorskich analityków w społeczności, wspieranych przez zespół Dune. Opisy kolumn tabeli pisowni [ zdefiniowane tutaj ] ( https://spellbook-docs.dune.com/#!/model/model.spellbook.dex_trades). <TAG1> Tabele niższego poziomu, z którymi często będziesz pracować, to tabele `raw` i `decoded`. Surowe tabele są zdefiniowane [ tutaj ] ( tabele danych / raw / index.md ), ale dla tabel zdekodowanych należy znaleźć dokumentację protokołu, taką jak [ ta dla Uniswap V3 ] ( https:/.uniswap.org/contracts/v3/referencja / rdzeń / UniswapV3Factory ). Dowiesz się, jak z nimi pracować w przewodnikach wymienionych w sekcji [ zaawansowanej ] ( analytics_guidelines.md ).

### Nauka podstaw SQL i Blockchain

Powyższe zapytanie może być dla Ciebie mylące, jeśli nie znasz podstaw SQL lub Blockchain. Oto kilka zasobów dla początkujących i przewodników na początek:

- [ Wydma Oficjalne rozpoczęcie serii wideo ] ( https://www.youtube.com/watch?v=S-cctFmR828&list=PLK3b5d4iK10ext4v-GBySekaA8-GP8quD&index=1) aby dowiedzieć się, jak przepływają dane i jak poruszać się po aplikacji Dune, aby tworzyć zapytania, wizualizacje i pulpity nawigacyjne. 

- [ Tygodniowe problemy SQL Web3 ] ( https://daodatadesign.notion.site/Web3-SQL-Weekly-0bababb5e59a412bb73594c512db8cc1), aby nauczyć się wskazówek i wskazówek kreatora w bitach wielkości bajtu. Obejmuje takie rzeczy, jak salda tokenów, integracje protokołów, wskaźniki produktów i wiele więcej.

- [ Wszystkie podstawy Ethereum i SQL ] ( https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql), aby poznać wszystkie podstawowe pojęcia SQL i tabele Ethereum, których potrzebujesz w swojej analizie.

- Aby ćwiczyć czysto SQL, spróbuj przejść przez „łatwe” problemy [ na hackerrank ] ( https://www.hackerrank.com/domains/sql).

Dołącz do społeczności i ucz się razem [ w Discord ] ( https://discord.com/invite/ErrzwBz), uczestnicząc w `# 🐥 ︱ początkujących` i `# 🙋 ︱ pytania- kanały.

A kiedy poczujesz się gotowy do przeprowadzenia zaawansowanej analizy, zapoznaj się z [ next guide ] ( analytics_guidelines.md ).

Powinieneś także przeczytać o pojęciach specyficznych dla Dune SQL, takich jak niestandardowe typy i funkcje oraz różnego rodzaju tabele w naszej bazie danych.

### Nadal utknąłeś lub chcesz zatrudnić kogoś innego do pomocy?

W branży kryptograficznej jest sporo osób, które specjalizują się w budowaniu na wydmie lub posiadają umiejętności niezbędne do szybkiego dostosowania się do szczegółów.

Aby dotrzeć do tej puli ekspertów freelancerów, możesz [ wypełnić ten kwestionariusz ] ( http://bounties.dune.com) i poczekać, aż freelancerzy wrócą do ciebie w krótkim lub krótkim czasie. Jeśli nie przyniesie to żadnych rezultatów, może pomóc w opublikowaniu nagrody na odpowiednich kanałach społecznościowych i rozpowszechnieniu jej w sieciach.
