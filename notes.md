

### Slouceni vsech PDF vystupu:
`pdftk $(find . -name '*out.pdf') cat output sloucene.pdf`



### Vykresleni vsech spekter v gnuplotu:



```bash
PLOT="plot "
for FILE in $(find . -name '*.csv'); do PLOT+="\"$FILE\" using (abs(\$2)):3 every ::2 with lines, "; done
echo $PLOT

# Odebrání poslední čárky a mezery z příkazu

PLOT=${PLOT%, }
```

Spustit gnuplot
# Vytvoření Gnuplot skriptu
set datafile separator ','
set title 'Firework zoo'
set xlabel 'Wavelength'
set ylabel 'Intensity'
set xrange [400:800]
