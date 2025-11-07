Hier kann och jederzeit, eine neue VErsion der Json Datei hochladen....

Umwandlung funktioniert so: 

import pandas as pd
import json

# Excel-Datei einlesen
# WICHTIG: Ersetzen Sie 'ihre_datei.xlsx' mit dem tatsächlichen Dateinamen
df = pd.read_excel('Schuko_Version_081025_2.xlsx')

# Spaltennamen anpassen (von Ihrer Excel-Struktur zum JSON-Format)
df_renamed = df.rename(columns={
    'BildURL': 'BildUrl',
    'Author': 'Autor',
    'Title': 'Title',
    'Year': 'Jahr',
    'Journal': 'Journal',
    'Pagenumbers': 'Seiten',
    'Volume': 'Volume',
    'Number': 'Number',
    'Handwritten': 'Handwritten',
    'Notiz': 'Notiz'
})

# Nur die benötigten Spalten auswählen
columns_to_keep = ['BildUrl', 'Autor', 'Title', 'Jahr', 'Journal', 
                   'Seiten', 'Volume', 'Number', 'Handwritten', 'Notiz']

df_final = df_renamed[columns_to_keep]

# NaN-Werte durch leere Strings ersetzen
df_final = df_final.fillna('')

# In JSON konvertieren
literature_data = df_final.to_dict('records')

# JSON-Datei speichern (schön formatiert)
with open('literature-data.json', 'w', encoding='utf-8') as f:
    json.dump(literature_data, f, ensure_ascii=False, indent=2)

print(f"Erfolgreich {len(literature_data)} Einträge konvertiert!")
print("Datei gespeichert als: literature-data.json")
