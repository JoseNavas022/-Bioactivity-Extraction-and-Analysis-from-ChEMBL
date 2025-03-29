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


