# Address-Standardization
Original WriteUp can be Found here (https://devpost.com/software/address-correct)

Inspiration

Have you ever received mail back that you thought was correctly labeled, or had mail that was delivered to the wrong address? A mild annoyance maybe, but what happens if this happens to critical items, like prescription medicine? We got inspired to create a Address Correction program that prevents mishaps like this from happening. We tackle the problem early on, by either fixing the address to a standardized format, or returning not-verifiable if the address does not exist.

What it does

This is a Address Standardization program that changes addresses to adhere to USPS standards. Additionally we verify whether the address exists and report back to the user.

How we built it

We initially considered using an external api like Google's. However we thought, in the specific case of a health care provider like Optum, an external service like Google could compromise confidential data to third parties and is reliant on a provider like Google. We believed an offline version that utilized real time access to a database would be safer and more reliable.
Once we understood the premise, our next step was to find a database of addresses in the United States to Standardize and Verify our input against. We searched government records and found a database that was over 4 gigabytes in size of current addresses. With a database to verify against, we could begin the next step.
Verifying addresses was the biggest challenge. We initially had no idea on how to determine similarity, but we kept reading about String Comparison and discovered Levenshtein Distance algorithms. Eventually we discovered an algorithm that utilized Levenshtein Distance to effectively calculate the differences between String sequences. With this, we set percent similarity thresholds, and if the input matched the database threshold, we would begin the Standardization process.
The way we formatted out database was that each complete address would have multiple tokens. These tokens could be either the street name, house number, street name abbreviation, city, state abbreviation, or zip code. With these tokens in the database, we output the match with tokens in a specific order, hence standardizing it. With our specific format, we could then return the verified match and standardized form. Any unverified match would be returned to the user and the user notified.

Challenges we ran into

Reliable Address Data
For our comparison method, we compared the input to our database. However most quality data was hard to come by for free, so we made do with the database we found. Over 95% of continental United States Addresses was obtained, so our program should work for the majority of inputs.
Utilizing an Effective Comparison Method for Standardization
Even with a database, how would we determine whether an address was similar to an existing one? The algorithm we utilized used Levenshtein Distance. This allowed us to calculate the the approximate differences between String sequences. With this we were able to compare the input to the MongoDB Database and make calculations to see whether if was indeed a valid address. From there, we take the database similarity and standardize it into USPS standards.

Accomplishments that we're proud of

Converting a .CSV file into a Database
The longest process of a project was the conversion of the .CSV file with all the addresses into a NOSQL Database. This alone took over 8 hours, however it was needed. Afterwards, we indexed the data base by street number to make searching even faster. This allowed for easy access later and allowed our comparison algorithm to work in the first place.

What we learned

Teamwork and how to work together effectively without colliding into each other.
Database Usage
None of us had experience with MongoDB, but we realized it was the right tool for the job. Therefore, we spent time learning from the MongoDB documentation. Reading the documentation allowed us to gather an increased appreciation for databases.

What's next for Address Correct

Real Time Database Updates
The United States is constantly changing with the creation of new addresses and sometimes even deletion. The most polished version would use the highest quality and most comprehensive Address Data Base with updates phased in, as these changes occur.
API Utilization/ Request Methods
Ideally we would want to create a way for either developers of the internal company, or even sometimes external clients to be able to automate the Address Correction Process. The current process is limited by the individual, and not yet practical for industrial use. However our current model is a good proof of concept.

