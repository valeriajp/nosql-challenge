# nosql-challenge
The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

# Part 1: Database and Jupyter Notebook Set Up
Use ![image](https://github.com/user-attachments/assets/03f2df53-2928-40a2-a35e-e796332ea9a4) for this section of the challenge.
  1. Import the data provided in the ![image](https://github.com/user-attachments/assets/dfd77059-f35d-41ed-9989-e962d07ae3ec) file from your Terminal. Name the database ![image](https://github.com/user-attachments/assets/d740ce05-ece6-4c2c-bc29-1a69bcdee3b5) and the collection ![image](https://github.com/user-attachments/assets/609a8265-874e-4149-a75a-a1ed1e741804).
  2.  Copy the text you used to import your data from your Terminal to a markdown cell in your notebook. Within your notebook, import the libraries you need: PyMongo and Pretty Print (![image](https://github.com/user-attachments/assets/c683733b-52d0-48ed-9898-ebd81903995f)).
  3.  Create an instance of the Mongo Client.
  4.  Confirm that you created the database and loaded the data properly:
     - List the databases you have in MongoDB. Confirm that ![image](https://github.com/user-attachments/assets/d740ce05-ece6-4c2c-bc29-1a69bcdee3b5) is listed.
     - List the collection(s) in the database to ensure that ![image](https://github.com/user-attachments/assets/95bc822d-809f-4f13-88f7-becc832df2bc) is there.
     - Find and display one document in the ![image](https://github.com/user-attachments/assets/896d2638-6b14-468c-8dff-3e1cbaf514cd) collection using ![image](https://github.com/user-attachments/assets/5fba71ad-8643-4d87-bb4c-1460c63276cb) and display with ![image](https://github.com/user-attachments/assets/37c3e554-5e7d-4f87-bd86-015746002def).
  5. Assign the ![image](https://github.com/user-attachments/assets/607ce34b-7bf1-49cb-a724-10983f63f2c8) collection to a variable to prepare the collection for use.

# Part 2: Update the Database
Use ![image](https://github.com/user-attachments/assets/3cdf951d-a607-4cb2-8add-4e5ac91242a5) for this section of the challenge.

The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the ![image](https://github.com/user-attachments/assets/bb9ba9cc-e9c1-407c-8ba2-884624c7df96) collection:
1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:


            {
            "BusinessName":"Penang Flavours",
            "BusinessType":"Restaurant/Cafe/Canteen",
            "BusinessTypeID":"",
            "AddressLine1":"Penang Flavours",
            "AddressLine2":"146A Plumstead Rd",
            "AddressLine3":"London",
            "AddressLine4":"",
            "PostCode":"SE18 7DY",
            "Phone":"",
            "LocalAuthorityCode":"511",
            "LocalAuthorityName":"Greenwich",
            "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
            "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
            "scores":{
                    "Hygiene":"",
                    "Structural":"",
                    "ConfidenceInManagement":""
            },
            "SchemeType":"FHRS",
            "geocode":{
                "longitude":"0.08384000",
                "latitude":"51.49014200"
            },
            "RightToReply":"",
            "Distance":4623.9723280747176,
            "NewRatingPending":True
          }  
2. Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the ![image](https://github.com/user-attachments/assets/d78e2c8a-e22b-4b7f-b464-eb7ef24c1c30) and ![image](https://github.com/user-attachments/assets/9c1cc907-ec51-4282-a0a0-41f58aa440e2) fields.
3. Update the new restaurant with the ![image](https://github.com/user-attachments/assets/d78e2c8a-e22b-4b7f-b464-eb7ef24c1c30) you found.
4. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.
5. Some of the number values are stored as strings, when they should be stored as numbers.
   1. Use ![image](https://github.com/user-attachments/assets/9ca85c9f-7e82-48f5-ab81-0d2fff9ef8a9)  to convert ![image](https://github.com/user-attachments/assets/ffb2d91d-b618-4252-988e-34a7ecf465ff) and ![image](https://github.com/user-attachments/assets/64a75d4d-38d3-42a3-a19e-797926c8f2ed) to decimal numbers.
   2. Use ![image](https://github.com/user-attachments/assets/05c0dcc6-542d-4397-84eb-1f5c2c9dd12b) to convert ![image](https://github.com/user-attachments/assets/11566544-b9c8-4216-b47b-6a98a051958b) to integer numbers.
  
# Part 3: Exploratory Analysis
*Eat Safe, Love* has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use ![image](https://github.com/user-attachments/assets/ce0cd5a4-a93c-4755-aec9-d30628be44c8) for this section of the challenge.

Some notes to be aware of while you are exploring the dataset:

* ![image](https://github.com/user-attachments/assets/11566544-b9c8-4216-b47b-6a98a051958b) refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.

  * **Note:** This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.
  
* The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors. Unless otherwise stated, for each question:
* Use ![image](https://github.com/user-attachments/assets/9c84fb0c-7470-47f2-9ad7-57092c6468e6) to display the number of documents contained in the result.
* Display the first document in the results using ![image](https://github.com/user-attachments/assets/016c7809-e6be-4b81-a124-4322170772ae).
* Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

1. Which establishments have a hygiene score equal to 20?
2. Which establishments in London have a  ![image](https://github.com/user-attachments/assets/11566544-b9c8-4216-b47b-6a98a051958b) greater than or equal to 4?
   **Hint:** The London Local Authority has a longer name than "London" so you will need to use ![image](https://github.com/user-attachments/assets/d1bddd97-740d-43fd-8044-e73ec1a022d4) as part of your search.
3. What are the top 5 establishments with a  ![image](https://github.com/user-attachments/assets/11566544-b9c8-4216-b47b-6a98a051958b) of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
  **Hint:** You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.
4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.
  **Hint:** You will need to use the ![image](https://github.com/user-attachments/assets/f10ed9a5-857f-4cfb-bd21-fe119d3a8ae0) method to answer this.
The first 5 rows of your resulting DataFrame should look something like this:


|            | 	_id     | count    |
|------------|----------|----------|
|0           | 	Thanet  | 1130     |
|1           | Greenwich| 882      |
|2           | Maidstone| 713      |
|3           | Newham   | 712      |
|4           | Swale    | 686      |

# Responses
1. There are 41 establishments with a hygiene score of 20 from the uk_food dataset.
2. There are 34 establishments in London that have a RatingValue greater than or equal to 4 from the uk_food dataset.
3. The top 5 establishments with a RatingValue of '5' sorted by lowest hygiene score nearest to "Penang Flavours" are: "Seaford Pizza", "Golden Palace", "Brenalwood", "The Chase Rest Home", and "Melrose Hotel".
4. There are 55 rows in the DataFrame. This is the preview of the first 10 rows:

|            | 	_id     | count    |
|------------|----------|----------|
|0           | 	Thanet  | 1130     |
|1           | Greenwich| 882      |
|2           | Maidstone| 713      |
|3           | Newham   | 712      |
|4           | Swale    | 686      |
|5           |Chelmsford| 680      |
|6           | Medway   | 672      |
|7           | Bexley   | 607      |
|8           | Swale    | 686      |
|9      |Southend-On-Sea| 586      |
|10          | Tendring | 542      |


# References
[UK Food Standards Agency](https://www.food.gov.uk/). (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GBLinks to an external site.. Contains public sector information licensed under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).
