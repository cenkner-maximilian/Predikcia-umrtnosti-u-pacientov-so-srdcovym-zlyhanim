# Využitie prediktívnych modelov strojového učenia na predikciu úmrtnosti pacientov so srdcovým zlyhaním
<h2>Abstrakt</h2>
Výskumný projekt so zameraním na predikovanie úmrtnosti pacientov s diagnostikovaným srdcovým zlyhaním podľa <a href="#dataset">dát</a>. Výskum zahŕňa tréning základných aj upravených modelov Decision Tree a Random Forest, ich evaluáciu a výsledky.

<h2>Popis datasetu</h2>
<ol>
<li><b>age</b> |                    Vek pacienta (celé číslo)</li>
<li><b>sex</b> |                    Muž/žena (binárna hodnota)</li>
<li><b>smoking</b> |                fajčiar/nefajčiar (binárna hodnota)</li>
<li><b>time</b> |                   Čas medzi vyšetreniami po diagnóze (celé číslo, dni)</li>
<li><b>anaemia</b> |                Zníženie hemoglobínu alebo počtu červených krviniek (erytrocytov) v krvi (binárna hodnota)</li>
<li><b>creatine_phosphokinase</b> | Hladina enzýmu CPK v krvi (celé číslo)</li>
<li><b>diabetes</b> |               Diagnostikovaný diabetes (binárna hodnota)</li>
<li><b>ejection_fraction</b> |      Percento krvi odchádzajúce zo srdca po každom vypumpovaní (celé číslo, %)</li>
<li><b>high_blood_pressure</b> |    Zvýšený tlak krvi, hypertenzia (binárna hodnota)</li>
<li><b>platelets</b> |              Počet krvných doštičiek v krvi (celé číslo)</li>
<li><b>serum_creatinine</b> |       Odpadová látka v krvi vypúšťaná svalmi a filtrovaná obličkami  (celé číslo)</li>
<li><b>serum_sodium</b> |           Koncentrácia sodíka v krvi (celé číslo)</li>
<li><b>DEATH_EVENT</b> |            Smrť pacienta (binárna hodnota)</li>
</ol>
Zdroj: <a href="#dataset">dataset</a>

<h2>Postup analýzy a tréningu</h2>
<ol>
<li>Príprava a základná analýza datasetu</li>
<li>Tréning a evaluácia základného modelu</li>
<li>Výsledky základného modelu</li>
<li>Tréning a evaluácia upraveného modelu (Threshold tuning)</li>
<li>Výsledky upraveného modelu</li>
<li>Experiment: Random Forest algoritmus</li>
<li>Výsledky experimentu</li>
<li>Finálne zohodnotenie výskumu</li>
</ol>
Dostupné podrobne v main.ipynb
<hr>
<h2>Príprava a základná analýza datasetu</h2>
Príprava a analýza pozostávala s naimportovania <a href="#dataset">dátového súboru</a> s 299 medicínskymi dátami o pacientoch, následnej analýze samotných vlastností (features) datasetu, zistenia ich spoločných korelácií a vyhodnotenia modelu, ktorý použijem.


<img width="869" height="695" alt="image" padding_top="25px" src="https://github.com/user-attachments/assets/cf4fbc05-d111-4085-830b-13aec13b9cd1" />

Obr. 1, Vizualizovaná korelačná matica, bez žiadnych výrazných lineárnych korelácií.

<h3>Záver</h3>
Nakoľko sa vlastnosti datasetu nevyznačujú koreláciami medzi sebou, rozhodol som sa pre využitie modelu Decision Tree na prvotné tréningy.

<hr>
<h2>Tréning a evaluácia základného modelu</h2>

<h2>Zdroje</h2>
<p id="dataset">Heart Failure Clinical Records [Dataset]. (2020). UCI Machine Learning Repository. https://doi.org/10.24432/C5Z89R.</p>
Chicco, D., Jurman, G. Machine learning can predict survival of patients with heart failure from serum creatinine and ejection fraction alone. BMC Med Inform Decis Mak 20, 16 (2020). https://doi.org/10.1186/s12911-020-1023-5
