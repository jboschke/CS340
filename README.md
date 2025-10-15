# CS340
CS340 Client/Server Development
About the Project/Project Title
This mini‑library provides a reusable Python wrapper around the Austin Animal Center “animals” collection stored in MongoDB. At this stage the class supports the Create (insert) and Read (query) operations; Update and Delete will be added in Project One. The wrapper hides connection details so that future dashboards or scripts can work with the data set by calling two simple methods: create() and read().


Motivation
Duplicating raw PyMongo connection code in every notebook is fragile and violates the DRY principle. Encapsulating those calls in a class gives us a single place to store credentials, concise functions that are easy to unit‑test, and a foundation we can extend with update/delete later.

Getting Started
1. Database & authentication (set up in Module 3)
   • Database: AAC — Collection: animals
   • User: aacuser with role readWrite on AAC
   • Data source: aac_shelter_outcomes.csv imported via mongoimport

2. Copy animal_shelter.py into the same folder where you will run your Jupyter notebook or Python script.

3. Instantiate the helper:
   from animal_shelter import AnimalShelter
   shelter = AnimalShelter(pwd="YOUR_PASSWORD")

4. Run test_crud.ipynb to verify that create() returns True and read() retrieves the inserted document.

Installation
Tools used:
• Python 3.10 (Apporto default)
• MongoDB Community 6.0 (pre‑configured in Apporto)
• PyMongo 4.6 (official driver)
• Jupyter Notebook 6.x (interactive demo)

Install dependencies (if not already available):
    pip install --upgrade "pymongo>=4.6,<5" jupyter

Usage

Code Example
Example — insert then read:

from animal_shelter import AnimalShelter
s = AnimalShelter(pwd=" uT9~kV3-Pw1_Lz7.qR5nY2sB8 ")

doc = {
    "animal_id": "TEST9999",
    "breed": "Module Four Terrier",
    "animal_type": "Dog",
    "outcome_type": "Adoption"
}
print(s.create(doc))           # → True
print(s.read({"animal_id":"TEST9999"}))

Tests
             from animal_shelter import AnimalShelter
s = AnimalShelter(pwd=" uT9~kV3-Pw1_Lz7.qR5nY2sB8 ")

# round-trip: insert then read
assert s.create({"animal_id": "TEST_INLINE",
                 "breed": "Inline Beagle",
                 "animal_type": "Dog",
                 "outcome_type": "Adoption"})

doc = s.read({"animal_id": "TEST_INLINE"})[0]
assert doc["breed"] == "Inline Beagle"

print("✓ inline tests passed")
