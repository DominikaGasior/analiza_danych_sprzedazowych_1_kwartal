# Analiza danych sprzedażowych za 1 kwartał – Dashboard w Excel

## 🖥 Podgląd Dashboardu
![Demo Dashboardu](https://github.com/DominikaGasior/analiza_danych_sprzedazowych_1_kwartal/blob/15256b64881941389173fdc4cb31c80209e4f097/portfolio.gif)

## 📌 Opis projektu
Celem tej analizy było **sprawdzenie poprawności danych**, analiza oraz  
stworzenie **interaktywnego dashboardu sprzedażowego**, który umożliwia  
szybkie monitorowanie kluczowych wskaźników sprzedaży w pierwszym kwartale.

Analiza skupia się na:  
- 📊 Całkowitym przychodzie  
- 📦 Ilości zamówień  
- 🏷️ Sprzedaży wg kategorii i produktów  
- 📈 Trendzie sprzedaży w czasie  

Dane pochodzą z fikcyjnego zbioru obejmującego około 100 transakcji 
(m.in. informacje o produktach, cenach, rabatach, kategoriach), który 
najpierw zweryfikowałam pod kątem poprawności (np. duplikatów i 
błędnych wartości), a następnie wykorzystałam do stworzenia czytelnego 
raportu prezentującego m.in. **łączny przychód**, **liczbę zamówień**, 
sprzedaż w podziale na **kategorie produktu** oraz **miesiąc**.

---

## 📂 Spis treści
1. [Użyte narzędzia](#-użyte-narzędzia)  
2. [Czyszczenie danych w Power Query](#-czyszczenie-danych-w-power-query)  
3. [Wnioski i rekomendacje](#-wnioski-i-rekomendacje)  
4. [Kod Power Query](#-kod-power-query)  

---

## 🛠 Użyte narzędzia
- **Power Query (Excel)** – do sprawdzenia poprawności i czyszczenia danych  
- **Microsoft Excel** – do stworzenia interaktywnego dashboardu z wykorzystaniem fragmentatorów i wykresów  

---

## 🔎 Czyszczenie danych w Power Query
W trakcie przygotowywania danych:
- Usunęłam duplikaty,  
- Poprawiłam błędne wartości (np. `???` → `Unknown`),  
- Zamieniłam puste wartości na `0`,  
- Skonwertowałam typy kolumn (daty, waluty, procenty).  

---

## 💡 Wnioski i rekomendacje
- **Akcesoria** to największa kategoria (45% udziału) – potencjalnie warto zwiększyć ich ofertę.  
- **Średnia wartość zamówienia**: 1 234 zł – można wprowadzić rabaty powyżej tej kwoty.  
- **Najwyższa sprzedaż** w styczniu (42 805 zł).  
- **Produkt o największej liczbie sprzedanych jednostek** to Drukarka (48 sztuk).  
- Sprzedaż spadała w kolejnych miesiącach – możliwe efekty sezonowości.  
- Warto przeprowadzić **analizę sezonowości**, aby lepiej zrozumieć przyczyny najwyższej sprzedaży w styczniu.  
- Można wdrożyć **kampanie promocyjne** w lutym i marcu, aby zwiększyć sprzedaż w słabszych miesiącach.  
- Wprowadzenie programów lojalnościowych lub dodatkowych rabatów dla klientów z wysokimi zamówieniami mogłoby zwiększyć średnią wartość zamówień.  
- Analiza sprzedaży na **poziomie regionów** mogłaby ujawnić dodatkowe wzorce i rynki do ekspansji.  
- Warto **porównać dane z poprzednimi latami**, żeby ocenić długoterminowe trendy sprzedaży.

---

## 💻 Kod Power Query
[Zobacz plik z kodem](./power_query_code.m)
