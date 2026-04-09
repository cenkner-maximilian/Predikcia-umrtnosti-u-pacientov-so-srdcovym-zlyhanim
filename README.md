# Využitie prediktívnych modelov strojového učenia na predikciu úmrtnosti pacientov so srdcovým zlyhaním
<h2>Abstrakt</h2>
<p>Výskumný projekt so zameraním na predikovanie úmrtnosti pacientov s diagnostikovaným srdcovým zlyhaním podľa dát. Výskum zahŕňa tréning základných aj upravených modelov Decision Tree a Random Forest, ich evaluáciu a výsledky.</p>

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
<p>Zdroj: <a href="#dataset">dataset (1)</a></p>

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
<p>Príprava a analýza pozostávala s naimportovania <a href="#dataset">dátového súboru</a> s 299 medicínskymi dátami o pacientoch, následnej analýze samotných vlastností (features) datasetu, zistenia ich spoločných korelácií a vyhodnotenia modelu, ktorý použijem.</p>

<img width="869" height="695" alt="image" padding_top="25px" src="https://github.com/user-attachments/assets/cf4fbc05-d111-4085-830b-13aec13b9cd1"/>

<p>Obr. 1, Vizualizovaná korelačná matica, bez žiadnych výrazných lineárnych korelácií.</p>

<h3>Záver</h3>
<p>Vlastnosti (features) datasetu sa podľa vizualizovanej korelačnej matice nevyznačujú veľkými koreláciami medzi sebou. Jedinou vyššou koreláciou je tá medzi pohlavím a stavom fajčenia, čo som však pre môj výskum považoval za irelevantné (obe features sú binárne, hodnoty v nich sú 1/0)</p>

<hr>
<h2>Tréning a evaluácia: základný model</h2>
<p>Keďže dáta spolu nekorelujú, rozhodol som sa pre algoritmus Decision Tree. Pri tréningu som hľadal ideálnu hĺbku stromu (max_depth), pri ktorej má model najvyššie Recall skóre (Recall je jedna z metrík používaná na posúdenie, ako dobre model funguje, viac info <a href="https://developers.google.com/machine-learning/glossary#recall">tu</a>). Po hľadaní ideálnej max_depth som si vytvoril vizualizáciu niźšie, aby som lepšie pochopil, ako sa recall pri max_depth vyvíjal.</p>

<img width="576" height="460" alt="image" src="https://github.com/user-attachments/assets/c34513a8-d92b-4e23-bc8d-5a6a5c401c99" />
<p>Obr. 2, Líniový graf, závislosť max_depth (hĺbka modelu) od Recall (evaluačná metrika)</p>

<p>Podľa grafu vyššie som zisitl, že recall je najvyšší pri hodnote max_depth=2. Natrénoval som preto model s takouto hĺbkou a taktiež som si vyhodnotil celkové skóre modelu pomocou rôznych evaluačných metrík. (Vizualizácia modelu a tabuľka s evaluačnými testami nižšie)</p>

<img width="515" height="412" alt="image" src="https://github.com/user-attachments/assets/4eb9c87f-34b5-40df-b198-5d0df602769e" />
<p>Obr. 3, Vizualizovaný Rozhodovací Strom s maximálnou hĺbkou 2, upravený pre ideálny Recall.</p>

<table border="1" cellpadding="8" cellspacing="0">
    <thead>
        <tr>
            <th>Class</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F1-score</th>
            <th>Support</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0 (prežitie)</td>
            <td>0.73</td>
            <td>0.87</td>
            <td>0.79</td>
            <td>53</td>
        </tr>
        <tr>
            <td>1 (smrť)</td>
            <td>0.74</td>
            <td>0.54</td>
            <td>0.62</td>
            <td>37</td>
        </tr>
        <tr>
            <td><strong>Accuracy</strong></td>
            <td colspan="3">0.73</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Macro avg</strong></td>
            <td>0.74</td>
            <td>0.70</td>
            <td>0.71</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Weighted avg</strong></td>
            <td>0.73</td>
            <td>0.73</td>
            <td>0.72</td>
            <td>90</td>
        </tr>
    </tbody>
</table>
<p>Obr. 4, Evaluačný report #1 pre základný model.</p>

<h3>Záver</h3>
<p>Základný Decision Tree dosiahol pri class 1 (smrť) Recall skóre 54% a F1 skóre 62%. Recall na 54% znamená, že ak model určil pri konkrétnom pacientovi, že umrie, mal pravdu len v 54% prípadoch. Tento výsledok som zhodnotil ako <b>neuspokojivý</b> a preto som s tréningom pokračoval ďalej.</p>

<hr>
<h2>Tréning a evaluácia: Upravený model</h2>
<p>Pred týmto tréningom som jasne určil, ako model má vyzerať: Recall skóre vyššie aspoň ako 65%. Tento cieľ som dosiahol takto: model som natrénoval s upraveným klasifikačným thresholdom. Viac o thresholdingu nájdete <a href="https://developers.google.com/machine-learning/glossary#classification-threshold">tu</a>.<br> Na upravenie thresholdu som použil funkciu TunedThresholdClassifierCV, do ktorej som vložil môj model a evaluačnú metriku ktorú chcem zlepšiť. Po vložení metriky Recall som zistil, že model začal predpovedať smrť v každom jednom prípade. Toto nie je ideálne, keďže existujú aj pacienti jasne určiteľní ako preživší srdcového zlyhania, túto skupinu však model minie vždy, keďže v 100% prípadoch predpovedá smrť. Zameral som sa teda na evaluačnú metriku F1 skóre a so zameraním na jej zlepšenie som natrénoval model cez TunedThresholdClassifierCV. Opäť som hľadal ideálnu hĺbku, nižšie je vizualizovaný graf z hľadania ideálnej hĺbky.<br></p>

<img width="584" height="460" alt="image" src="https://github.com/user-attachments/assets/886da5ba-a020-47c4-a789-11a328aa7bb5" />
<p>Obr. 5, Vizualizovaný líniový graf, závislosť rôznych hĺbok modelu od hodnoty metriky F1 skóre.</p>

<p>Na základe vizualizácie som našiel ideálnu hĺbku (hodnota 2) a s ňou natrénoval model aj pomocou TunedThresholdClassifierCV. Vizualizáciu algoritmu a aj evaluačný report sú priložené nižšie.</p>

<img width="515" height="411" alt="image" src="https://github.com/user-attachments/assets/d79c4170-de4b-4190-8e6d-64bad7e25bf7" />
<p>Obr. 6, Vizualizácia upraveného rozhodovacieho stromu, hĺbka 2.</p>

<table border="1" cellpadding="8" cellspacing="0">
    <thead>
        <tr>
            <th>Class</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F1-score</th>
            <th>Support</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0 (prežitie)</td>
            <td>0.78</td>
            <td>0.81</td>
            <td>0.80</td>
            <td>53</td>
        </tr>
        <tr>
            <td>1 (smrť)</td>
            <td>0.71</td>
            <td>0.68</td>
            <td>0.69</td>
            <td>37</td>
        </tr>
        <tr>
            <td><strong>Accuracy</strong></td>
            <td colspan="3">0.76</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Macro avg</strong></td>
            <td>0.75</td>
            <td>0.74</td>
            <td>0.75</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Weighted avg</strong></td>
            <td>0.75</td>
            <td>0.76</td>
            <td>0.75</td>
            <td>90</td>
        </tr>
    </tbody>
</table>
<p>Obr. 7, evaluačný report #2 pre upravený model.</p>

<h2>Záver</h2>
Natrénovaný upravený model vykazuje zlepšenie v F1 skóre skoro o 20% a pri Recall skóre o viac ako 10%. Tento fakt hodnotím pozitívne. Model predpovie smrť správne v skoro 70% prípadov.

<hr>
<h2>EXPERIMENT: Tréning algoritmu Random Forest</h2>
<p>Random Forest je algoritmus zložený z <b>n</b> rozhodovacích stromov, ktorým sú dodané rôzne dáta z datasetu. Každý strom následne rozhodne, či priradí konkrétnemu pacientovi na základe dát hodnotu 0 (v tomto prípade prežitie) alebo 1 (smrť). Celkovo potom Random Forest určí class modelu podľa väčšiny. Natrénoval som aj základný aj upravený model. Výsledky upraveného modelu sú vidno nižšie.</p>

<table border="1" cellpadding="8" cellspacing="0">
    <thead>
        <tr>
            <th>Class</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F1-score</th>
            <th>Support</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0 (prežitie)</td>
            <td>0.80</td>
            <td>0.81</td>
            <td>0.80</td>
            <td>53</td>
        </tr>
        <tr>
            <td>1 (smrť)</td>
            <td>0.72</td>
            <td>0.70</td>
            <td>0.71</td>
            <td>37</td>
        </tr>
        <tr>
            <td><strong>Accuracy</strong></td>
            <td colspan="3">0.77</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Macro avg</strong></td>
            <td>0.76</td>
            <td>0.76</td>
            <td>0.76</td>
            <td>90</td>
        </tr>
        <tr>
            <td><strong>Weighted avg</strong></td>
            <td>0.77</td>
            <td>0.77</td>
            <td>0.77</td>
            <td>90</td>
        </tr>
    </tbody>
</table>
<p>Obr. 8, Evaluačný report #3 pre upravený Random Forest.</p>

<h2>EXPERIMENT: Záver</h2>
<p>Random Forest vykazuje mierne zlepšenie prediktívnosti pri class 1 ako upravený decision tree.</p>

<hr>
<h2>ZHODNOTENIE VÝSKUMU</h2>
<p>V tomto výskume som natrénoval niekoľko inštancií modelu Decision Tree na predikovanie úmrtnosti pacientov na zlyhanie srdca, pričom som sa zameral na metriku Recall a F1 skóre. Ich maximalizovaním som dosiahol, že model klasifikoval častejšie prípady ako úmrtné, čím sa síce znížila jeho presnosť, keďže častejšie vyhodnotil aj neúmrtné prípady ako úmrtné, no zachytil aj menej jasné prípady, ktoré boli stále úmrtné. So zaujímavosti som pokračoval neskôr s experimentálnym tréningom modelu Random Forest, ktorý aj po úpravách ukázal minimálne vylepšenia, ale stále dobrý výsledok.</p>

<hr>
<h2>VYUŽITÉ TECHNOLÓGIE</h2>
<ul>
    <li><b>Python 3.12</b></li>
    <li><b>Seaborn</b> | Vizualizácie</li>
    <li><b>Matplotlib</b> | Vizualizácie</li>
    <li><b>Scikit-learn</b> | Tréning modelov a evaluačné metriky</li>
</ul>
<p><b>Detailné vysvetlivky a teória je zahrnutá v prezentácii slide-deck.pptx</b></p>
<hr>
<h1>Zdroje</h1>
<p id="dataset">1 | Heart Failure Clinical Records [Dataset]. (2020). UCI Machine Learning Repository. https://doi.org/10.24432/C5Z89R.</p>
<p>2 | Chicco, D., Jurman, G. Machine learning can predict survival of patients with heart failure from serum creatinine and ejection fraction alone. BMC Med Inform Decis Mak 20, 16 (2020). https://doi.org/10.1186/s12911-020-1023-5</p>
