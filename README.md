# Mass-Shootings-and-Congressmen-on-X

# Anonymized Twitter Data of the 117th US Congress

## Overview
This dataset contains anonymized Twitter data of members of the 117th US Congress, along with Gun Violence Archive data. The data has been processed and split into smaller chunks for easier handling and sharing (original file is about 3GB). 
The Gun Violence Archive data can be accessed directly at [Gun Violence Archive](https://www.gunviolencearchive.org/).
GINI Coefficient Data can be accessed directly at [https://statehealthcompare.shadac.org/table/82/income-inequality-gini-coefficient#1,2,16,18,25/a/76/119]
Residential segregation data can be accessed directly at [https://hdpulse.nimhd.nih.gov/data-portal/physical/table?age=001&age_options=ageall_1&demo=01005&demo_options=res_seg_2&physicaltopic=100&physicaltopic_options=physical_2&race=00&race_options=raceall_1&sex=0&sex_options=sexboth_1&statefips=00&statefips_options=area_states]

## File Structure
- **Split Chunks**: The dataset is split into multiple `.gz` files located in the directory `/Users/dmytro/Documents/NYU/Congress_Tweets_Project/ORIGINALS/split_chunks`.
  - Each file is named `DSL_Gun_Violence_Congress_Tweets_chunk_<index>.gz`.
- **Combined File**: You can combine the split files into a single `.json.gz` file for further analysis.

## How to Use the Dataset

### Prerequisites
1. **Python**: Ensure Python is installed on your system (version 3.7 or higher recommended).
2. **Required Libraries**: gzip shutil pandas

#### Combining chunks into a single dataframe
import gzip
import os
import pandas as pd
split_dir = '/path/to/split_chunks'
output_file = '/path/to/reconstructed_dataset.json.gz'
with open(output_file, 'wb') as f_out:
    for chunk_file in sorted(os.listdir(split_dir)):
        chunk_path = os.path.join(split_dir, chunk_file)
        with open(chunk_path, 'rb') as f_in:
            f_out.write(f_in.read())
decompressed_file = output_file.replace('.gz', '')
with gzip.open(output_file, 'rb') as f_in:
    with open(decompressed_file, 'wb') as f_out:
        f_out.write(f_in.read())

df = pd.read_json(decompressed_file)

