# Phase 1 Project - Film Studio - Initial Recommendations


### Business Problem

Microsoft has decided to create a new movie studio, but they are ill informed about the process of creating successful films. The relative "success" of a movie is a result of a variety of factors; even from viewer to viewer, there is an inherent subjectivity in reported satisfaction. While the profit a film makes is an undeniably objective metric of success, it rarely paints the picture of the impact a whole film can have on its audience. Data from online databases will be aggregated/summarized in order to determine defining characteristics of successful films. Isolating prime directors, actors/actresses, and genres to pursue will assist Microsoft in creating films that are profitable from both audience and financial standpoints.

### Data

A variety of data is pulled from the online movie databases IMDB and The Numbers. The imported data contains a variety of information related to films, their working crew, financial information, and audience reception. The transformation/combination of variables within these databases will be used to isolate factors of success.

From the perspective of the IMDB data, all tables can be linked with 2 variables/primary keys, 'tconst', which directly correlates to a movie's title, and 'nconst', which directly correlates to each staff who worked on a given movie (e.g. directors, actprs where records are available). The key metric of success for this dataset are the user ratings, judged from a scale of 1-10, the average taken for each distinct movie.

From the perspective of the The Numbers dataset, financial information is correlated to each movie in the dataset, including how much was spent to create the movie (production_budget), how much money the movie made domestically (in its respective country, domestic_gross), and how much money the movie made internationally (worldwide_gross).


__TITLE BASICS TABLE - IMDB__
This table contains the primary title the film is known for (primary_title), the year the film started aggregating data (start_year), and its genres. The primary variable, 'tconst', will be used to link the other tables in the IMDB database.


__NAME BASICS TABLE - IMDB__
The primary key of this table is 'nconst', which stores each cast/crew member who worked on any film in the IMDB database with a unique identifier. Birth year and death year, are self explanatory. Upon a look at the first 5 rows, it was observed that not all entries in these columns were populated by a value. As this database seems to be mostly user reported, some deceased members are not be logged.

__PRINCIPALS TABLE - IMDB__
This table links the film identifier 'tconst' with all people who worked in any given movie, using their 'nconst'value as an identifier, with 'category' describing their general role.

__RATINGS TABLE - IMDB__
The ratings table contains a critical metric relevant to our analysis, the aggregate ratings each film got. As this metric is user reported, there is inherently some subjectivity in success determination, as well as variance in the number of reviews each film had.

__FINANCIAL DATASET - The Numbers__
This table contains all financial information for each given film of the database. These numbers will be helpful in determining financial success of all movies in our dataset. 'production_budget' refers to the amount allocated to create the movie. 'domestic_gross' refers to the amount each movie made it its original respective release country. 'worldwide_gross' refers to the amount the movie made around the globe, 'domestic_gross' being included in this metric.


## Methodology


Within the cumulative IMDB database and TN database, there were several fields included which may be useful in other contexts, but not for the purpose of the identified business problem. The methodology for cleaning through the overall datasets can be found below.

While film runtime minutes may be an interesting metric to analyze for a different problem, it is safe to assume that film runtime likely has little correlation with financial/cultural success. Examples can be seen from relatively successful short films such as Disney+'s Us, Again, compared to terrible movies with long runtimes, such as Batman vs. Superman: Dawn of Justice.

In order to be as inclusive as possible while still remaining scrutinous with the data, null values were filled with 3000 for birth year, and 0 for the 'death_year'. The table was then filtered by 'birth_year', taking out all actors who were born before the year 1936, eliminating all actors over the age of 85. Film crew that have a definite populated death year are excluded from the table, in order to make sure all entries (as far as user reported status is concerned) depict live members.

Number of reviews for each film is an inherently flawed metric. As an example, some films that are targeted to a younger audience, may have viewers that are inherently be more tech savvy. This makes it it more likely for those films to have a higher amount of reviews. Despite this critical flaw, audience reviews are the only true metric to see how impactful a film was on its viewers.

Upon looking at the distribution of 'review_count' for the films in the database, the majority of films have less than 1000 reviews. 75% of the films in the table have data over 365 votes. In order to keep the bulk of the review data, which will end up being our main metric of analysis, movies with ratings over ~200 were chosen to keep over ~75% of the data, while still avoiding the films on the fringe that have too little reviews. This step will eliminate bias due to low review rates within any given film.

The dataset is limited to films that were made in the last ~40 years. This is done in order to keep the dataset relevant to the modern age of film. The year 1980 is chosen, as it is safe to assume that actors/directors who started their career in this decade would likely be done with their career by now. For the purpose of this analysis, and Microsoft wanting to make a brand new studio,potential records should be limited to working casts/film staff that are still relatively active.

The financial data is converted from strings into integers, so mathematical operations can be performed on the relevant columns. A column of 'profit_ratio' is created, which will be one of the critical metrics used to evaluate success. 'profit_ratio' is calculated by taking the overall 'worldwide_gross' that a movie accrued, divided by the initial 'production_budget'. This metric tells us how profitable a film ended up being; more profit is ideal for a fledgeling studio.


### Results

__DIRECTORS:__
The final table contains the top film directors I would recommend for Microsoft to pursue for their film studio, from both a financial perspective and an audience perspective.  Assuming Microsoft is seeking to make the largest amount of profit, while still taking a director's reputability into account, the data is sorted first by count of films that made a profit, then by profitability rating. Assuming there is a desired range of budgets for produced films within the studio, the average film budget is also included within the overall table, so they can pick and choose from a range of budget points.

Selections (in order of priority): Tim Story, Chris Renaud, Don Hall, Pierre Coffin, Steven Soderbergh, Steven Spielberg, Ariel Schulman, Henry Joost

__ACTORS/ACTRESSES:__
Unsurprisingly, the actors/actresses included in the overall dataset are reputable, and are known for starring in blockbuster franchises/films. The data is first sorted by film count, then binned rating to prioritize audience satisfaction to a secondary degree.

Selections (in order of priority): Mark Wahlberg, Dwayne Johnson, Robert De Niro, Joel Edgerton, Steve Carell, Jennifer Lawrence, Matthew McConaughey, Liam Neeson, Channing Tatum, Michael Fassbender, Amy Adams


__GENRES:__
The "big-screen" film genres like Horror, Mystery, and Thriller unsurprisingly take the top slots in terms of profitability. The data is sorted by binned profitability as the main metric, then by average production budget for additional screening.

Selections (in order of priority): Horror, Mystery, Thriller, Family, Documentary, Animation, Romance, Fantasy, Biography


##  Conclusions


Directors, actors and genres are critical elements that make films successful. The performed analysis of the datasets resulted in three sets of recommendations for ideal directors, actors, and genres to pursue in order to jump-start a successful movie studio. While the sets are helpful guidelines for choosing for each element, external research still needs to be done in order to find the combination that maximizes a film's profitability and audience reception.

I would recommend that Microsoft pursues directors, actors, and genres from a variety of budget ranges; there can only be so many big-budget films before money becomes a limiting factor for a studio. That being said, directors/actors who show promise (in terms of user ratings) who typically operate under a relatively lower budget should be pursued as well. Prioritizing lower risk investments would help budding members of the industry advance their careers through a bigger studio. For these films, user ratings should be prioritized in the overall selections. As long as the respective audience can see the value in a director's/actor's choices, success is inherent.

Below are the selections from the dataset that I have chosen to maximize the metrics of success:

__DIRECTORS:__

Selections (in order of priority): Tim Story, Chris Renaud, Don Hall, Pierre Coffin, Steven Soderbergh, Steven Spielberg, Ariel Schulman, Henry Joost

__ACTORS/ACTRESSES:__

Selections (in order of priority): Mark Wahlberg, Dwayne Johnson, Robert De Niro, Joel Edgerton, Steve Carell, Jennifer Lawrence, Matthew McConaughey, Liam Neeson, Channing Tatum, Michael Fassbender, Amy Adams


__GENRES:__

Selections (in order of priority): Horror, Mystery, Thriller, Family, Documentary, Animation, Romance, Fantasy, Biography


Despite this intuitive ranking system, there are several factors which might cause this system to be imperfect. External factors such as scandals may cause certain actors/directors to be excluded from consideration solely due to their reputation. For actors/directors/studios that have never worked together, clashing personalities and artistic vision could be the result of catastrophic failure. As an example, despite the success of its predecessor, 'Iron Man', 'Iron Man 2' was received poorly by its critics. Director Jon Favreau reported that he wasn't able to make the film he wanted to make because of limitations/restrictions imposed by Kevin Fiege, the residing president of Marvel Studios. Granular looks at interviews/articles may reveal hidden tensions like the aforementioned, but it is impossible to quantify/standardize that information in a dataset.

Limitations:
Through this project and the resulting analysis, there were several limitations, particularly when it came to the availability of information in the datasets.

First, a significant amount of data was missing in both the ratings dataset from IMDB and the financial dataset from The Numbers. If a film was not logged in IMDB's database and it ended up being a harshly critiqued/unprofitable film, the resulting metrics for that film's crew could be skewed due to exclusion. This makes it impossible to know the true holistic view of an actor's/director's capabilities. For some films that were present in IMDB's dataset, corresponding financial information was not available from Ihe Numbers dataset. The exclusion of films without financial data may result in a different priority rankings when it comes to aggregation.

With regard to the 'namebasics' table, the birth year & death year values were not populated for every 'nconst'. This inherently creates problems as directors/actors who have passed or retired could severely limit the resulting filtered dataset.

User rating is inherently a subjective/imperfect metric. For any given movie, it is impossible to determine if the user rating audience base is cmpletely unbiased. As an example, movies with particularly high fanbases such as the Marvel Cinematic Universe may have several users rate the movies highly as they are fans of the character portrayals. If the logged reviews are solely created by Marvel fans, it is natural for a Marvel film to have obscenely high ratings relative to other movies. If more critics with a more critical eye for artistic choices/acting in film were to review a Marvel movie, the overall rating would undoubtedly go down. Each film critic, whether casual or professional, has their own bias; they may choose to only watch certain movies over others.

Overall, when any movie title is searched via Google, a wide variety of review aggregation metrics can be seen from different companies, some with their own unique metrics. Since only IMDB was used to quantify user satisfaction, a successful film according to their available metrics may have done poorly on a different website.

Next Steps:
As previously mentioned, external research would have to be done in order to find the ideal combinations of genres, directors, and actors in a film.

Finding each director/actor's ideal genre would unveil ideal pairings between the two, resulting in well made films. On an more granular level, an additional flags/field designating actors and directors that have historically worked on movies together could be included. The new fields would identify if their resulting collaboration was successful, and this information would be used to prioritize ideal pairings.

Review aggregate data from websites other than IMDB should also be included in the overall dataset. Films present in IMDB may not be present in rotten tomatoes, and vice versa. Having a larger amount of review data from various sources to work with would eliminate some bias.

While directors and actors are vital to making a film successful, as recent years have shown, CGI (computer-generated imagery) can be a selling point for a film; isolating editors would be a point of interest to explore as well. Editors that can be trusted with big budgets can engage an audience with a movie to a greater degree. The same can be made for the case of writers. Good writers tell good stories, and no amount of good acting/directing cn fix a bad plot. In the end, every crew member has a direct contribution to a film's perceived success.


## For More Information

Please review the full analysis in the corresponding Jupyter Notebook and presentation.

For any additional questions, please contact Noah-John Hizon at noahiz917@gmail.com 


## Repository Structure


...
├── code
│   ├── __init__.py
│   ├── data_preparation.py
│   ├── visualizations.py
├── zippedData                                   #folder containing data used for analysis
├── README.md
├── Film Studio - Initial Recommendations.pdf    #pdf of presentation
├── phase_1_project_jupyternotebook              #pdf of jupyter notebook
└── student.ipynb                                #jupyter notebook containing all relevant summaries/analyses

