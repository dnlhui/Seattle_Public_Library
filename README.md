# Seattle Public Library

Book Collection Management Strategy for the Seattle Public Library

This project seeks to predict which book titles are least likely to be checked out of the Seattle Public Library collection in a given 6 month period. Rather than sit unused on a branch library shelf, where shelf space is at a premium, underutilized books could be repositioned in the larger Central Library location and rotated through as predictive demand changes. Demand for titles can fluctuate due to seasonality (holiday books, children books, self-improvement), as well as wider social, political and cultural trends. 

Seattle Public Library releases comprehensive open data through the Seattle Data portal. Data is released in three key tables:

### Book Collections
https://data.seattle.gov/Community/Library-Collection-Inventory/6vkj-f5xf
Inventory of each book title in each branch location

### Checkout Records by Titl
https://data.seattle.gov/Community/Checkouts-by-Title/tmmm-ytt6
Checkouts by title 

### Data Dictionary
https://data.seattle.gov/Community/Integrated-Library-System-ILS-Data-Dictionary/pbt3-ytbc 
Codes used in the library dataset 

From the book collection data, I generated features using the inventory codes such as publication year, fiction/non-fiction/language categories, and genre (biography, mystery, picture books, children, teen, comic, African-American). From the checkout records, I generated features based on checkout density for different trailing periods - 30 days, 90 days, 180 days, and 365 days. 

I augmented the open data with other online sources:

### Bibliocommons
https://seattle.bibliocommons.com 
An online catalog that collects book information from libraries across North America, including Seattle

### Library of Congress
http://pcn.loc.gov/isbncnvt.html 
Tool to format ISBN numbers

From Bibliocommons, I generated features on average customer rating, number of reviews, page count and book size dimensions. This data is collected from many libraries and can be used to analyze books that are not currently in the Seattle Public Library collection. From the Library of Congress, I used the ISBN from the book collection inventory to generate a properly formatted code, which contains information on the book’s language, country of publication, and size of the publishing house. 

I generated two sets of models: 

(A) The full set of features, which can be used to evaluate books in the current collection to determine if a book should be relocated from a branch library to free up space.

(B) I create a second set of models for books that the library is evaluating for acquisition. These books would not have data for patron borrowing features or library branch collection features. However, the book details, ISBN, as well as information from the nationwide Bibliocommons would be available for any title.

Using Logistic Regression, the two sets of models created different feature weights. The full feature set is dominated by borrowing activity from the previous 180 days and prior 365 days, while genre, language, and format were less impactful. The book-only features have more elements contributing to the prediction, including non-fiction/fiction, total patron ratings, year of publication, format, and language. 

Online interactive tool created from this analysis: 
https://public.tableau.com/profile/dnlhui#!/vizhome/181029_Dashboard/Dashboard

Project Online: 
https://www.dnlhui.com/seattle-public-library-open-data 
