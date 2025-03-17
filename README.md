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
```powerquery
let
 Źródło = Excel.Workbook(File.Contents("/Users/mac/Downloads/portfolio1.xlsx"),
null, true),
 #"Nawigacja 1" = Źródło{[Item = "Sheet1", Kind = "Sheet"]}[Data],
 #"Nagłówki o podwyższonym poziomie" = Table.PromoteHeaders(#"Nawigacja 1",
[PromoteAllScalars = true]),
 #"Zmieniono typ kolumny" = Table.TransformColumnTypes(#"Nagłówki o podwyższonym
poziomie", {{"Order_ID", Int64.Type}, {"Date", type date}, {"Customer_ID",
Int64.Type}, {"Product", type text}, {"Category", type text}, {"Quantity",
Int64.Type}, {"Unit_Price", Int64.Type}, {"Total_Sales", type number}, {"Discount",
Int64.Type}, {"Sales_Rep", type text}}, "pl"),
 #"Usunięto duplikaty" = Table.Distinct(#"Zmieniono typ kolumny", {"Order_ID"}),
 #"Zamienione błędy" = Table.ReplaceErrorValues(#"Usunięto duplikaty",
{{"Customer_ID", 0}}),
 #"Zamieniono wartość" = Table.ReplaceValue(#"Zamienione błędy", null, 000,
Replacer.ReplaceValue, {"Customer_ID"}),
 #"Zamieniono wartość 1" = Table.ReplaceValue(#"Zamieniono wartość", "???",
"Laptop", Replacer.ReplaceText, {"Product"}),
 #"Zamieniono wartość 2" = Table.ReplaceValue(#"Zamieniono wartość 1", "Unknown",
"Akcesoria", Replacer.ReplaceText, {"Category"}),
 #"Zmieniono typ kolumny 1" = Table.TransformColumnTypes(#"Zamieniono wartość 2",
{{"Unit_Price", type text}}),
 #"Zamieniono wartość 3" = Table.ReplaceValue(#"Zmieniono typ kolumny 1", "-", "",
Replacer.ReplaceText, {"Unit_Price"}),
 #"Zmieniono typ kolumny 2" = Table.TransformColumnTypes(#"Zamieniono wartość 3",
{{"Unit_Price", Currency.Type}}),
 #"Zamieniono wartość 4" = Table.ReplaceValue(#"Zmieniono typ kolumny 2", null, 0,
Replacer.ReplaceValue, {"Discount"}),
 #"Zmieniono typ kolumny 3" = Table.TransformColumnTypes(#"Zamieniono wartość 4",
{{"Total_Sales", type text}}),
 #"Zamieniono wartość 5" = Table.ReplaceValue(#"Zmieniono typ kolumny 3", "-", "",
Replacer.ReplaceText, {"Total_Sales"}),
 #"Zmieniono typ kolumny 4" = Table.TransformColumnTypes(#"Zamieniono wartość 5",
{{"Total_Sales", type number}}),
 #"Usunięto kolumny" = Table.RemoveColumns(#"Zmieniono typ kolumny 4",
{"Total_Sales"}),
 #"Kolumna używana podczas dzielenia" = Table.TransformColumns(#"Usunięto
kolumny", {{"Discount", each _ / 100, type number}}),
 #"Zmieniono typ kolumny 5" = Table.TransformColumnTypes(#"Kolumna używana podczas
dzielenia", {{"Discount", Percentage.Type}}),
 #"Dodano niestandardowe" = Table.TransformColumnTypes(Table.AddColumn(#"Zmieniono
typ kolumny 5", "Total_Order", each ([Quantity]*[Unit_Price])-
([Quantity]*[Unit_Price]*[Discount])), {{"Total_Order", Currency.Type}}),
 #"Zmieniono kolejność kolumn" = Table.ReorderColumns(#"Dodano niestandardowe",
{"Order_ID", "Date", "Customer_ID", "Product", "Category", "Quantity",
"Unit_Price", "Total_Order", "Discount", "Sales_Rep"}),
 #"Zamieniono wartość 6" = Table.ReplaceValue(#"Zmieniono kolejność kolumn",
"nan", "Unknown", Replacer.ReplaceText, {"Sales_Rep"}),
 #"Zmieniono nazwy kolumn" = Table.RenameColumns(#"Zamieniono wartość 6",
{{"Sales_Rep", "Customer_Name"}})
in
 #"Zmieniono nazwy kolumn"
