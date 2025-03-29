🧪 Bioactivity Extraction and Analysis from ChEMBL
This project retrieves bioactivity data for molecules similar to a given compound using the ChEMBL database. It extracts relevant information, such as chemical structures and biological activity values, to support research in medicinal chemistry and drug discovery.

🚀 Features
Searches for molecules similar to a given compound using the ChEMBL API.

Filters results based on a specified chemical similarity threshold.

Extracts bioactivity data, including assay type, standard values, and units.

Saves the results in a CSV file for further analysis.

Identifies the most frequently occurring assay description in the dataset.

🛠 Requirements
Python 3.8+

Pandas

ChEMBL Web Resource Client

📌 Installation
bash
Copiar
Editar
pip install pandas chembl_webresource_client
🔬 Usage
python
Copiar
Editar
python script.py
The script will query ChEMBL, retrieve bioactivity data, and generate a bioactivity_data_filtered.csv file with the results. It will also display the most frequently occurring assay description.

📊 Expected Output
A CSV file containing molecule and bioactivity information.

Console output showing the most repeated assay description and its frequency.

📜 License
This project is licensed under the MIT License.

import pandas as pd
from chembl_webresource_client.new_client import new_client
 
similarity = new_client.similarity
res = similarity.filter(smiles='C1[C@H]([C@H](OC2=CC(=CC(=C21)O)O)C3=CC(=C(C(=C3)O)O)O)O', similarity=40).filter(max_results=10000).only(['molecule_chembl_id', 'pref_name'])
bioactivity_data = []

for molecule in res:
    molecule_chembl_id = molecule['molecule_chembl_id']
    molecule_details = new_client.molecule.get(molecule_chembl_id)
    canonical_smiles = molecule_details.get('molecule_structures', {}).get('canonical_smiles', None)
    bioactivities = new_client.activity.filter(molecule_chembl_id=molecule_chembl_id).only(['activity_id', 'assay_type', 'standard_type', 'standard_value', 'standard_units', 'assay_description'])
    for bioactivity in bioactivities:
        if bioactivity.get('standard_units') == 'nM':
            bioactivity_data.append({
                'molecule_chembl_id': molecule_chembl_id,
                'canonical_smiles': canonical_smiles,
                'activity_id': bioactivity.get('activity_id'),
                'assay_type': bioactivity.get('assay_type'),
                'assay_description': bioactivity.get('assay_description'),
                'standard_type': bioactivity.get('standard_type'),
                'standard_value': bioactivity.get('standard_value'),
                'standard_units': bioactivity.get('standard_units')
            })

bioactivity_df = pd.DataFrame(bioactivity_data)
bioactivity_df.to_csv('bioactivity_data_filtered.csv', index=False)


assay_description_counts = bioactivity_df['assay_description'].value_counts()

most_common_description = assay_description_counts.idxmax()
most_common_count = assay_description_counts.max()

print(f"La descripción más repetida es: '{most_common_description}' con {most_common_count} repeticiones.")
