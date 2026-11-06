# Power BI dashboard: qadamlar

Power BI Desktop faqat Windows'da ishlaydi (Microsoft'dan bepul yuklanadi). Ma'lumot fayli: `xodimlar_tozalangan.csv` (notebookdagi oxirgi katakdan chiqadi).

## 1. Ma'lumotni yuklash
1. Power BI Desktop > **Get data > Text/CSV** > `xodimlar_tozalangan.csv` > **Transform Data**.
2. Power Query'da turlarni tekshiring: `oylik`, `bonus` = Whole number, `kpi_ball`, `staj_yil` = Decimal, `ishga_kirgan_sana` = Date.
3. **Close & Apply**. Jadval nomini `xodimlar` qiling.

## 2. DAX o'lchovlar (Modeling > New measure)
```
Xodimlar soni = COUNTROWS(xodimlar)
Ortacha oylik = AVERAGE(xodimlar[oylik])
Jami bonus = SUM(xodimlar[bonus])
Yuqori KPI soni = CALCULATE(COUNTROWS(xodimlar), xodimlar[kpi_ball] >= 90)
Ayollar ulushi = DIVIDE(CALCULATE(COUNTROWS(xodimlar), xodimlar[jins] = "Ayol"), COUNTROWS(xodimlar))
```

## 3. Dashboard tuzilishi (1 sahifa)
- **Yuqorida 4 ta Card:** Xodimlar soni, Ortacha oylik, Jami bonus, Yuqori KPI soni.
- **Chap:** Bar chart, o'qi `bolim`, qiymati `Ortacha oylik`.
- **O'rtada:** Donut chart, `jins` bo'yicha `Xodimlar soni`.
- **O'ngda:** Bar chart, `malumoti` bo'yicha `Ortacha oylik`.
- **Pastda:** Line chart, `staj_yil` bo'yicha `Ortacha oylik`, yoki viloyatlar bo'yicha bar chart.
- **Slicer'lar:** `bolim`, `viloyat`, `ish_holati`.

## 4. Portfolioga chiqarish
1. Dashboardni `.pbix` qilib saqlang va GitHub'ga yuklang.
2. **File > Export > Export to PDF**, yoki sahifaning skrinshotini oling (`.png`).
3. Skrinshotni portfolio sahifasidagi Power BI kartochkasiga qo'shaman.
